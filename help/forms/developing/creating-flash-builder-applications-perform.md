---
title: HTTPトークンを使用したSSO認証を実行するFlash Builderアプリケーションの作成
seo-title: HTTPトークンを使用したSSO認証を実行するFlash Builderアプリケーションの作成
description: HTTPトークンを使用してシングルサインオン(SSO)認証を実行するFlash Builderを使用して、クライアントアプリケーションを作成します。 操作のユーザーを1回認証し、その認証を使用して複数のAEM Forms操作を実行します。
seo-description: HTTPトークンを使用してシングルサインオン(SSO)認証を実行するFlash Builderを使用して、クライアントアプリケーションを作成します。 操作のユーザーを1回認証し、その認証を使用して複数のAEM Forms操作を実行します。
uuid: 273db00a-a665-4e52-88fa-4fca06d05f8c
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0ff30df7-b3ad-4c34-9644-87c689acc294
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 0%

---


# HTTPトークン{#creating-flash-builder-applicationsthat-perform-sso-authentication-using-http-tokens}を使用したSSO認証を実行するFlash Builderアプリケーションの作成

HTTPトークンを使用してシングルサインオン(SSO)認証を実行するFlash Builderを使用して、クライアントアプリケーションを作成できます。 例えば、Flash Builderを使用してWebベースのアプリケーションを作成するとします。 次に、アプリケーションに様々な表示が含まれ、各表示が異なるAEM Forms操作を呼び出すとします。 Formsの各操作でユーザーを認証する代わりに、ユーザーが1回認証できるログインページを作成できます。 認証が完了すると、ユーザーは再度認証を行うことなく、複数の操作を呼び出すことができます。 例えば、ユーザーがWorkspace(または他のFormsアプリケーション)にログインした場合、ユーザーは再認証する必要はありません。

クライアントアプリケーションにはSSO認証を実行するために必要なアプリケーションロジックが含まれていますが、AEM forms User Managementは実際のユーザー認証を実行します。 HTTPトークンを使用してユーザーを認証するために、クライアントアプリケーションはAuthentication Managerサービスの`authenticateWithHTTPToken`操作を呼び出します。 User Managementは、HTTPトークンを使用してユーザーを認証できます。 それ以降のAEM FormsへのリモートまたはWebサービスの呼び出しでは、認証用の資格情報を渡す必要はありません。

>[!NOTE]
>
>この節を読む前に、Remotingを使用したAEM Formsの呼び出しに詳しいことをお勧めします。 (「[AEM Formsリモートを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)」を参照)。

以下の`MyApplication/EncryptDocument`というAEM Formsの短時間のみ有効なプロセスは、ユーザーがSSOを使用して認証された後に呼び出されます。 （入力値や出力値など、このプロセスについて詳しくは、[短時間のみ有効なプロセスの例](/help/forms/developing/aem-forms-processes.md)を参照してください）。

![cf_cf_encryptdocumentprocess2](assets/cf_cf_encryptdocumentprocess2.png)

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このプロセスの呼び出し方法について説明するコード例に従うには、Workbenchを使用して`MyApplication/EncryptDocument`という名前のプロセスを作成します。 （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

Flash Builderを使用して構築されたクライアントアプリケーションは、`/um/login`および`/um/logout`に設定されたUser Managerのセキュリティサーブレットとやり取りします。 つまり、クライアントアプリケーションは、起動時に`/um/login` URLに要求を送信して、ユーザーのステータスを判断します。 次に、User Managerはユーザーステータスで応答します。 クライアントアプリケーションとUser Managerセキュリティサーブレットは、HTTPを使用して通信します。

**要求の形式**

セキュリティサーブレットには、次の入力変数が必要です。

* `um_no_redirect`  — この値はにする必要があり `true`ます。この変数は、User Managerセキュリティサーブレットに対して行われたすべての要求に付随します。 また、セキュリティサーブレットは、Flexクライアントや他のWebアプリケーションからの着信要求を区別するのに役立ちます。
* `j_username`  — この値は、ログインフォームで指定されたユーザーのログイン識別子の値です。
* `j_password`  — この値は、ログインフォームで指定されたユーザーの対応するパスワードです。

`j_password`値は、秘密鍵証明書の要求にのみ必要です。 パスワード値が指定されていない場合、セキュリティサーブレットは、使用しているアカウントが既に認証済みかどうかを確認します。 その場合は、次に進むことができます。ただし、セキュリティサーブレットは再びユーザーを認証しません。

>[!NOTE]
>
>i18nを適切に処理するために、これらの値がPOST形式になっていることを確認してください。

**応答の形式**

`/um/login`に設定されたセキュリティサーブレットは、`URLVariables`形式を使用して応答します。 この形式では、コンテンツタイプの出力はtext/plainです。 出力には、名前と値のペアがアンパサンド(&amp;)文字で区切られて含まれます。 応答には次の変数が含まれます。

* `authenticated`  — 値は `true` またはです `false`。
* `authstate`  — この値には、次のいずれかの値を含めることができます。

   * `CREDENTIAL_CHALLENGE`  — この状態は、User ManagerがユーザーのIDをどの手段を使用しても判断できないことを示します。認証を行うには、ユーザーのユーザー名とパスワードが必要です。
   * `SPNEGO_CHALLENGE` — この状態は、と同じように扱われ `CREDENTIAL_CHALLENGE`ます。
   * `COMPLETE`  — この状態は、User Managerがユーザーを認証できることを示します。
   * `FAILED`  — この状態は、User Managerがユーザーを認証できなかったことを示します。この状態への応答として、flexクライアントはユーザーにエラーメッセージを表示できます。
   * `LOGGED_OUT`  — この状態は、ユーザーが正常にログアウトしたことを示します。

* `assertionid`  — 状態がその `COMPLETE` 場合、ユーザーの `assertionId` 値が含まれます。クライアントアプリケーションは、ユーザーの`AuthResult`を取得できます。

**ログインプロセス**

クライアントアプリケーションの開始時に、`/um/login`セキュリティサーブレットにPOSTリクエストを行うことができます。 例えば、`https://<your_serverhost>:<your_port>/um/login?um_no_redirect=true` のようになります。要求がUser Managerセキュリティサーブレットに到達すると、次の手順を実行します。

1. `lcAuthToken`という名前のcookieを探します。 ユーザーが既に別のFormsアプリケーションにログインしている場合、このcookieが存在します。 Cookieが見つかった場合、その内容が検証されます。
1. ヘッダーベースのSSOが有効な場合、サーブレットは設定済みのヘッダーを探してユーザーのIDを特定します。
1. SPNEGOが有効な場合、サーブレットはSPNEGOの開始を試み、ユーザーのIDの確認を試みます。

セキュリティサーブレットがユーザーに一致する有効なトークンを見つけた場合、セキュリティサーブレットは`authstate=COMPLETE`を使用して処理を続行し、応答します。 それ以外の場合は、セキュリティサーブレットが`authstate=CREDENTIAL_CHALLENGE`で応答します。 次のリストで、これらの値について説明します。

* `Case authstate=COMPLETE`:ユーザーが認証され、 `assertionid` 値にユーザーのアサーション識別子が含まれていることを示します。この段階で、クライアントアプリケーションはAEM Formsに接続できます。 そのURLに対して設定されたサーブレットは、`AuthenticationManager.authenticate(HttpRequestToken)`メソッドを呼び出して、ユーザーの`AuthResult`を取得できます。 `AuthResult`インスタンスは、User Managerコンテキストを作成して、セッションに格納できます。
* `Case authstate=CREDENTIAL_CHALLENGE`:セキュリティサーブレットがユーザーの資格情報を必要とすることを示します。応答として、クライアントアプリケーションはログイン画面をユーザに表示し、取得した秘密鍵証明書をセキュリティサーブレット（例えば`https://<your_serverhost>:<your_port>/um/login?um_no_redirect=true&j_username=administrator&j_password=password)`）に送信できます。 認証に成功した場合、セキュリティサーブレットは`authstate=COMPLETE`を使用して応答します。

認証が成功しない場合は、セキュリティサーブレットは`authstate=FAILED`を使用して応答します。 この値に応答するために、クライアントアプリケーションはメッセージを表示して、秘密鍵証明書を再取得できます。

>[!NOTE]
>
>`authstate=CREDENTIAL_CHALLENGE`に対しては、クライアントは取得した秘密鍵証明書をPOST形式でセキュリティサーブレットに送信することをお勧めします。

**ログアウトプロセス**

クライアントアプリケーションがログアウトした場合、次のURLにリクエストを送信できます。

`https://<your_serverhost>:<your_port>/um/logout?um_no_redirect=true`

このリクエストを受け取ると、User Managerセキュリティサーブレットは`lcAuthToken` cookieを削除し、`authstate=LOGGED_OUT`を使用して応答します。 この値を受け取ったクライアントアプリケーションは、クリーンアップタスクを実行できます。

## SSO {#creating-a-client-application-that-authenticates-aem-forms-users-using-sso}を使用してAEM formsユーザーを認証するクライアントアプリケーションの作成

SSO認証を実行するクライアントアプリケーションの作成方法を示すために、クライアントアプリケーションの例が作成されます。 次の図に、クライアントアプリケーションがSSOを使用してユーザーを認証するために実行する手順を示します。

![cf_cf_flexsso](assets/cf_cf_flexsso.png)

上の図は、クライアントアプリケーションの開始時に発生するアプリケーションフローを示しています。

1. クライアントアプリケーションが`applicationComplete`イベントをトリガーします。
1. `ISSOManager.singleSignOn`への呼び出しが行われます。 クライアントアプリケーションは、User Managerセキュリティサーブレットに要求を送信します。
1. セキュリティサーブレットがユーザーを認証すると、`ISSOManager`は`SSOEvent.AUTHENTICATION_SUCCESS`をディスパッチします。 応答として、クライアントアプリケーションはメインページを表示します。 この例では、メインページがMyApplication/EncryptDocumentという名前のAEM Formsの短時間のみ有効なプロセスを呼び出します。
1. セキュリティサーブレットがユーザーが有効かどうかを判断できない場合、アプリケーションはユーザー資格情報を再要求します。 `ISSOManager`クラスは、`SSOEvent.AUTHENTICATION_REQUIRED`イベントをディスパッチします。 クライアントアプリケーションにログインページが表示されます。
1. ログインページで指定された資格情報が`ISSOManager.login`メソッドに送信されます。 認証が成功した場合は、手順3に進みます。 それ以外の場合は、`SSOEvent.AUTHENTICATION_FAILED`イベントがトリガされます。 クライアントアプリケーションにログインページと適切なエラーメッセージが表示されます。

### クライアントアプリケーション{#creating-the-client-application}の作成

クライアントアプリケーションは、次のファイルで構成されます。

* `SSOStandalone.mxml`:クライアントアプリケーションを表すメインMXMLファイル。（[SSOStandalone.mxmlファイルの作成](creating-flash-builder-applications-perform.md#creating-the-ssostandalone-mxml-file)を参照）。
* `um/ISSOManager.as`:シングルサインオン(SSO)に関連する操作を公開します。（「[ISSOManager.asファイルの作成](creating-flash-builder-applications-perform.md#creating-the-issomanager-as-file)」を参照）。
* `um/SSOEvent.as`:は、SSO関連のイベントに対し `SSOEvent` てディスパッチされます。（[SSOEvent.asファイルの作成](creating-flash-builder-applications-perform.md#creating-the-ssoevent-as-file)を参照）。
* `um/SSOManager.as`:SSO関連の操作を管理し、適切なイベントをディスパッチします。（「[SOManager.asファイルの作成](creating-flash-builder-applications-perform.md#creating-the-ssomanager-as-file)」を参照）。
* `um/UserManager.as`:WSDLを使用してAuthentication Managerサービスを呼び出すアプリケーションロジックが含まれます。（「[UserManager.asファイルの作成](creating-flash-builder-applications-perform.md#creating-the-usermanager-as-file)」を参照）。
* `views/login.mxml`:ログイン画面を表します。（「[login.mxmlファイルの作成](creating-flash-builder-applications-perform.md#creating-the-login-mxml-file)」を参照）。
* `views/logout.mxml`:ログアウト画面を表します。（「[logout.mxmlファイルの作成](creating-flash-builder-applications-perform.md#creating-the-logout-mxml-file)」を参照）。
* `views/progress.mxml`:進行状況の表示を表します。（「[progress.mxmlファイルの作成](creating-flash-builder-applications-perform.md#creating-the-progress-mxml-file)」を参照）。
* `views/remoting.mxml`:リモート処理を使用して、MyApplication/EncryptDocumentという名前のAEM Formsの短時間のみ有効なプロセスを呼び出す表示を表します。（「[remoting.mxmlファイルの作成](creating-flash-builder-applications-perform.md#creating-the-remoting-mxml-file)」を参照）。

次の図は、クライアントアプリケーションを視覚的に表したものです。

![cf_cf_sso_project](assets/cf_cf_sso_project.png)

>[!NOTE]
>
>umと表示という名前の2つのパッケージがあることに注意してください。 クライアントアプリケーションを作成する場合は、ファイルを適切なパッケージに配置してください。 また、adobe-remoting-provider.swcファイルをプロジェクトのクラスパスに追加していることを確認してください。 ([AEM FormsFlexライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)を参照)。

### SSOStandalone.mxmlファイルの作成{#creating-the-ssostandalone-mxml-file}

次のコードは、SSOStandalone.mxmlファイルを表しています。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application
                 layout="absolute"
                 applicationComplete="initApp()"
                 height="400" width="550"
                 xmlns:v="views.*"
                 backgroundColor="#EDE8F0" viewSourceURL="srcview/index.html">
     <mx:Script>
         <![CDATA[
             import mx.utils.URLUtil;
             import um.SSOEvent;
             import mx.core.UIComponent;
             import um.SSOManager;
             import mx.rpc.events.ResultEvent;
             import mx.utils.ObjectUtil;
             import mx.controls.Alert;
 
             [Bindable]
             private var _serverURL:String;
 
             private var _ssoManager:SSOManager;
 
             private var _progress:UIComponent;
 
             private var _loginPage:UIComponent;
 
             private function initApp():void{
                 _serverURL = determineServerUrl();
                 _ssoManager = new SSOManager(_serverURL);
 
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_FAILED,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_SUCCESS,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_REQUIRED,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.LOGOUT_COMPLETE,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_FAULT,loginHandler);
 
                 trace("[Main] Add the required event handlers for authentication");
                 _ssoManager.singleSignOn();
 
                 showBusy();
             }
 
             private function determineServerUrl():String
             {
                 var s:String ;
                 var appUrl:String = Application.application.url;
                 var givenUrl:String  = ExternalInterface.call("serverUrl.toString");
                 trace("[Main] Application url ["+appUrl+"] Given url ["+givenUrl+"]");
                 if(appUrl != null && appUrl.search("^http") != -1){
                     s = appUrl;
                 }
                 if(s == null){
                     s = givenUrl;
                 }
                 if(s== null){
                     s = "https://hiro-xp:8080/";
                 }
                 s = URLUtil.getFullURL(s,"/");
                 trace("[Main] Would be using ["+s+"] as serverUrl");
                 return s;
             }
 
             private function loginHandler(event:SSOEvent):void
             {
                 trace("[Main] Handling event "+event.type);
                 switch(event.type)
                 {
                     case SSOEvent.AUTHENTICATION_FAILED:
                         viewContent.selectedChild = login;
                         login.showLoginFailed();
                         break;
                     case SSOEvent.AUTHENTICATION_SUCCESS:
                         viewContent.selectedChild = remoting;
                         break;
                     case SSOEvent.AUTHENTICATION_REQUIRED:
                         viewContent.selectedChild = login;
                         break;
                     case SSOEvent.LOGOUT_COMPLETE:
                         viewContent.selectedChild = logout;
                         break;
                     case SSOEvent.AUTHENTICATION_FAULT:
                         Alert.show("Error doing authentication. Root error ["+event.rootEvent+"]","Authentication Fault",Alert.OK);
                 }
             }
 
             public function get ssoManager():SSOManager
             {
                 return _ssoManager;
             }
 
             public function showBusy():void
             {
                 viewContent.selectedChild = progress;
             }
 
             public function get serverUrl():String
             {
                 return _serverURL;
             }
 
         ]]>
     </mx:Script>
     <mx:ViewStack x="0" y="0" id="viewContent" >
         <v:login id="login" />
         <v:remoting id="remoting"  />
         <v:progress id="progress" />
         <v:logout id="logout"/>
     </mx:ViewStack>
 </mx:Application>
 
```

### ISSOManager.asファイル{#creating-the-issomanager-as-file}を作成しています

次のコードは、ISSOManager.asファイルを表しています。

```java
 package um
 {
     import flash.events.IEventDispatcher;
 
     /**
      * The <code>ISSOManager</code> expose operations related to Single Sign On (SSO) in AEM Forms
      * environment. The application should register appropriate <code>SSOEvent</code> handlers prior
      * to calling any of the following operations
      */
     public interface ISSOManager extends IEventDispatcher
     {
         /**
          * Tries to validate whether the user has an already existing session or not (SSO Scenarios). The application
          * may call this method during the initialization. In general this call would lead to one of the
          * following events getting dispatched
          * <ul>
          * <li>SSOEvent.AUTHENTICATION_SUCCESS - If a SSO session was found and valid
          * <li>SSOEvent.AUTHENTICATION_REQUIRED - No SSO session was found and as such authentication is required in
          * the form of username and password.
          * <li>SSOEvent.AUTHENTICATION_FAULT - Some error has occured while connecting to the server
          * </ul>
          */
         function singleSignOn():void;
 
         /**
          * Authenticates the user using username and password. It may lead to one of the following events
          * <ul>
          * <li>SSOEvent.AUTHENTICATION_SUCCESS - The authentication is successful and a session is established
          * <li>SSOEvent.AUTHENTICATION_FAILED - Authentication has failed
          * </ul>
          */
         function login(username:String, password:String):void;
 
         /**
          * Terminates the current session and logs out the user.
          */
         function logout():void;
 
         /**
          * Get the assertionId for the logged in user
          */
         function get assertionId():String;
     }
 }
```

### SSOEvent.asファイル{#creating-the-ssoevent-as-file}を作成しています

次のコードは、SSOEvent.asファイルを表しています。

```java
 package um
 {
     import flash.events.Event;
 
     /**
      * The <code>SSOEvent</code> is dispatched for SSO related events
      */
     public class SSOEvent extends Event
     {
         /**
          * This type of event would be dispatched when the Authentication process is successful. Authentication
          * might have been done with SSO or username and password. As a response to this event the application
          * can show the welcome page to the user
          * The application may want to perform specific check for permission/role so as to verify the user is allowed.
          * So as a response to this event the application would do those checks and then only show the welcome page
          */
         public static const AUTHENTICATION_SUCCESS:String = "authenticationSuccess";
 
         /**
          * This type of event would be dispatched when authentication fails using the username, password.
          * As a response to this type of event an application can show an error message to the user.
          * This event would only happen when authentication is done using username and password and NOT in
          * SSO case.
          */
         public static const AUTHENTICATION_FAILED:String = "authenticationFailed";
 
         /**
          * This type of event would be dispatched when authentication using SSO is not achieved. And due to
          * that we require the user's username and password for authentication. As a response to this event
          * the application can show the login page to the user.
          */
         public static const AUTHENTICATION_REQUIRED:String = "authenticationRequired";
 
         /**
          * This type of event would be dispatched when logout is complete. As a response to this event the
          * application may show a logout page informing the user that he has been logged out. Or the application
          * can take the user back to login page
          */
         public static const LOGOUT_COMPLETE:String = "logoutComplete";
 
         /**
          * This type of event would be dispatched when ever there is a problem in doing Authentication. The root cause
          * can be obtained from the <code>rootEvent</code>.
          */
         public static const AUTHENTICATION_FAULT:String = "authenticationFault";
 
         private var _rootEvent:Event;
 
         public function SSOEvent(type:String, rootEvent:Event=null)
         {
             super(type,true,false);
             _rootEvent = rootEvent;
         }
 
         /**
          * The root event. If current event type is <code>AUTHENTICATION_FAULT</code> then it would be an
          * <code>IOErrorEvent</code> in other cases it would be complete event. Its basic use is to extract the root
          * cause in case of an authentication fault.
          */
         public function get rootEvent():Event
         {
             return _rootEvent;
         }
     }
 }
```

### SOManager.asファイル{#creating-the-ssomanager-as-file}を作成しています

次のコードは、SSOManager.asファイルを表しています。

```java
 package um
 {
     import flash.events.Event;
     import flash.events.EventDispatcher;
     import flash.events.IOErrorEvent;
     import flash.external.ExternalInterface;
     import flash.net.URLLoader;
     import flash.net.URLLoaderDataFormat;
     import flash.net.URLRequest;
     import flash.net.URLVariables;
 
     import mx.utils.ObjectUtil;
 
     /**
      * Manages the SSO related operations and dispatches appropriate events. It would connect to the UM Filter/Servlet
      * at <code>um/login</code> The UM response would be of form of url encoded variables. It would look for
      * <code>authstate</code> value in the response and depending on that it would proceed.
      *
      * <p>If there is an IO_Error while initial attempt to UM then it would assume it as a 401 response. And it would
      * be assumed that SPNEGO based authenticatin is not working and therefore user would be shown a login page.
      */
     public class SSOManager extends EventDispatcher implements ISSOManager
     {
         private static const SSO_URL:String = "um/login";
         private static const SSO_LOGOUT_URL:String = "um/logout";
         private static const AUTH_COOKIE_NAME:String = "lcAuthToken";
 
         private var _serverUrl:String;
         private var _assertionId:String;
 
         /**
          * Constructs an SSOManager with the given server url.
          *
          * @param serverUrl - The uri of the server to connect to. it must be without any context path e.g
          * http://localhost:8080/. The SSOManager would directly append the path of UM exposed SSO url to it
          * for its operations
          */
         public function SSOManager(serverUrl:String)
         {
             _serverUrl = serverUrl;
         }
 
         public function singleSignOn():void
         {
             sendRequest(SSO_URL,true);
         }
 
         public function login(username:String, password:String):void
         {
             sendRequest(SSO_URL,false,
                 function(request:URLRequest,vars:URLVariables):void
                 {
                     vars.j_username = username;
                     vars.j_password = password;
                 }
             );
         }
 
         public function logout():void
         {
             sendRequest(SSO_LOGOUT_URL);
         }
 
         public function get assertionId():String
         {
             return _assertionId;
         }
 
 
 
         /**
          * Connects to the UM security service.
          */
         private function sendRequest(relativeUrl:String,authenticationRequest:Boolean=false, requestProcessor:Function=null):void
         {
             var loader:URLLoader = new URLLoader();
             loader.dataFormat = URLLoaderDataFormat.VARIABLES;
             var request:URLRequest = new URLRequest(_serverUrl + relativeUrl);
             trace("[SSOmanager] Contacting ["+request.url+"]");
             var vars:URLVariables = new URLVariables();
             vars.um_no_redirect = "true";
             request.data = vars;
             if(requestProcessor != null){
                 requestProcessor(request,vars);
             }
 
             loader.addEventListener(Event.COMPLETE,authHandler);
             //if its an authentication request then only treat io error as a possible 401
             //for others treat them as faults
             if(authenticationRequest){
                 loader.addEventListener(IOErrorEvent.IO_ERROR,httpAuthenticationHandler);
             }else{
                 loader.addEventListener(IOErrorEvent.IO_ERROR,authFaultHandler);
             }
             trace("[SSOmanager] Sending request "+ ObjectUtil.toString(request));
             loader.load(request);
         }
 
         private function authHandler(event:Event):void
         {
             var loader:URLLoader = URLLoader(event.target);
             var response:URLVariables = URLVariables(loader.data);
             trace("[SSOmanager] Processing response ["+ObjectUtil.toString(response)+"]");
             handleAuthResult(response["authstate"],response);
         }
 
         /**
          * Handles the IOErrorEvent. Flash would dispatch IOEvent in response to HTTP 401.
          * There is no way to distinguish it from the genuine IOError.
          */
         private function httpAuthenticationHandler(event:IOErrorEvent):void
         {
             trace("[SSOmanager] Processing IOErrorEvent ["+ObjectUtil.toString(event)+"]");
             handleAuthResult("CREDENTIAL_CHALLENGE");
 
         }
 
         /**
          * Dispatches appropriate <code>SSOEvent</code> on the basis of the <code>authstate</code>
          * value of the response.
          * The response is url encoded in for of
          * <pre>
          * authenticated=false&authstate=SPNEGO_CHALLENGE
          * </pre>
          * Depending on <code>authstate</code> the SSOEvent is dispatched
          */
         private function handleAuthResult(authState:String,response:URLVariables = null):void
         {
             trace("[SSOmanager] processing state "+authState);
             switch(authState)
             {
                 case "FAILED"  :
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_FAILED));
                     break;
                 case "COMPLETE" :
                     _assertionId = response ? response["assertionid"] : null;
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_SUCCESS));
                     break;
                 case "CREDENTIAL_CHALLENGE" :
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_REQUIRED));
                     break;
                 case "LOGGED_OUT" :
                     dispatchEvent(new SSOEvent(SSOEvent.LOGOUT_COMPLETE));
                     break;
                 default:
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_REQUIRED));
                     break;
             }
         }
 
         private function authFaultHandler(event:Event):void
         {
             dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_FAULT,event));
         }
 
     }
 }
```

### UserManager.asファイル{#creating-the-usermanager-as-file}の作成

次のコードは、UserManager.asファイルを表しています。

```java
 package um
 {
     import flash.events.Event;
     import mx.rpc.soap.WebService;
     import mx.rpc.soap.Operation;
     import mx.rpc.IResponder;
     import mx.rpc.events.FaultEvent;
     import mx.rpc.events.ResultEvent;
     import mx.rpc.soap.LoadEvent;
 
     public class UserManager
     {
         private var _ssoManager:ISSOManager;
         private var _serverUrl:String;
 
         public function UserManager(ssoManager:ISSOManager,serverUrl:String)
         {
             _serverUrl = serverUrl;
             _ssoManager = ssoManager;
         }
 
         public function retrieveAssertion(responder:IResponder):String
         {
             var assertionId:String = _ssoManager.assertionId;
             if(!assertionId)
             {
                 trace("[UserManager] AssertionId not found");
                 return null;
             }
 
             var ws:WebService = new WebService();
             var wsdl:String = _serverUrl+'soap/services/AuthenticationManagerService?wsdl&lc_version=8.2.1';
             ws.loadWSDL(wsdl);
             ws.addEventListener(LoadEvent.LOAD,
                 function(event:Event):void
                 {
                     trace("[UserManager] WSDL loaded");
                     var authenticate:Operation = ws.authenticateWithHttpToken as Operation;
                     authenticate.resultFormat = "e4x";
                     authenticate.addEventListener(ResultEvent.RESULT,
                         function(event:Event):void
                         {
                             responder.result(event);
                         }
                     );
                     authenticate.send({assertionId:assertionId});
                 }
             );
 
             ws.addEventListener(FaultEvent.FAULT,
                 function(event:Event):void
                 {
                     responder.fault(event);
                 }
             );
             return null;
         }
     }
 }
```

### login.mxmlファイル{#creating-the-login-mxml-file}の作成

次のコードは、login.mxmlファイルを表しています。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="500" height="400">
     <mx:Script>
         <![CDATA[
             import mx.core.Application;
             public function showLoginFailed():void
             {
                 loginMessage.text = "Username or Password incorrect";
             }
 
             private function doLogin():void
             {
                 Application.application.ssoManager.login(j_username.text,j_password.text);
                 Application.application.showBusy();
             }
 
         ]]>
     </mx:Script>
 
     <mx:VBox height="113" width="244" x="128" y="144" horizontalAlign="center" verticalGap="10">
         <mx:HBox width="100%">
             <mx:HBox width="100%" verticalAlign="middle" horizontalAlign="center" height="32">
                 <mx:Label text="Username" fontWeight="bold"/>
                 <mx:TextInput id="j_username"/>
             </mx:HBox>
         </mx:HBox>
         <mx:HBox width="100%" height="33" horizontalAlign="center" horizontalGap="10" verticalAlign="middle">
             <mx:Label text="Password" fontWeight="bold"/>
             <mx:TextInput displayAsPassword="true" id="j_password"/>
         </mx:HBox>
         <mx:Button label="Login" click="doLogin()"/>
     </mx:VBox>
     <mx:Text x="128" y="122" id="loginMessage" width="230" height="14"/>
     <mx:Label x="154" y="65" text="AEM Forms SSO Demo" fontFamily="Georgia" fontSize="20" color="#0A0A0A"/>
 </mx:Canvas>
 
```

### logout.mxmlファイル{#creating-the-logout-mxml-file}を作成しています

次のコードは、logout.mxmlファイルを表しています。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="500" height="400">
     <mx:Label x="97" y="188" text="You have successfully logged out from the application"/>
 
 </mx:Canvas>
 
```

### progress.mxmlファイル{#creating-the-progress-mxml-file}を作成しています

次のコードは、progress.mxmlファイルを表しています。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas >
     <mx:Label x="151" y="141" text="Wait...."/>
     <mx:SWFLoader source="LoadingCircle.swf" width="50" height="50" horizontalCenter="0" verticalCenter="0"/>
 </mx:Canvas>
```

### remoting.mxmlファイル{#creating-the-remoting-mxml-file}を作成しています

次のコードは、`MyApplication/EncryptDocument`プロセスを呼び出すremoting.mxmlファイルを表しています。 ドキュメントがプロセスに渡されるので、セキュリティで保護されたドキュメントをAEM Formsに渡すアプリケーションロジックはこのファイル内にあります。 ([Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)を使用して、保護されたドキュメントを呼び出してプロセスを呼び出すを参照)。

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="664" height="400" creationComplete="initializeChannelSet()" xmlns:views="views.*">
     <mx:Script>
 
         <![CDATA[
 
             import mx.rpc.livecycle.DocumentReference;
             import flash.net.FileReference;
             import flash.net.URLRequest;
             import flash.events.Event;
             import flash.events.DataEvent;
             import mx.messaging.ChannelSet;
             import mx.messaging.channels.AMFChannel;
             import mx.rpc.events.ResultEvent;
             import mx.collections.ArrayCollection;
             import mx.rpc.AsyncToken;
             import um.UserManager;
             import mx.rpc.events.ResultEvent;
             import mx.rpc.events.FaultEvent;
             import mx.core.Application;
             import mx.rpc.Responder;
             import mx.utils.ObjectUtil;
 
             // Classes used in file retrieval
             private var fileRef:FileReference = new FileReference();
             private var docRef:DocumentReference = new DocumentReference();
             private var parentResourcePath:String = "/";
             //private var serverPort:String = "'[server]:[port]'";
             private var serverPort:String = "'[server]:[port]'";
             private var now1:Date;
             private var userManager:UserManager;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Holds information returned from AEM Forms
             [Bindable]
             public var progressList:ArrayCollection = new ArrayCollection();
 
 
             // Set up channel set to invoke AEM Forms.
             // This must be done before calling any service or process, but only
             // once for the entire application.
             private function initializeChannelSet():void {
                 cs = new ChannelSet();
                 cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
                 EncryptDocument.channelSet = cs;
 
             //Get the user that is authenticated
             userManager = new UserManager(Application.application.ssoManager,Application.application.serverUrl);
             userManager.retrieveAssertion(
                     new mx.rpc.Responder(
                         function(event:ResultEvent):void
                         {
                             var name:String = XML(event.currentTarget.lastResult)..*::authenticatedUser.*::userid.text();
                             username.text = "Welcome "+name;
                         },
                         function(event:FaultEvent):void
                         {
                             mx.controls.Alert.show(event.fault.faultString,'Error')
                         }
                     )
                 );
 
             }
 
             // Call this method to upload the file.
             // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
             private function uploadFile():void {
                 fileRef.addEventListener(Event.SELECT, selectHandler);
                 fileRef.addEventListener(DataEvent.UPLOAD_COMPLETE_DATA,completeHandler);
                 fileRef.browse();
             }
 
             // Gets called for selected file. Does the actual upload via the file upload servlet.
             private function selectHandler(event:Event):void {
                 var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
                 authTokenService.addEventListener("result", authTokenReceived);
                 authTokenService.channelSet = cs;
                 authTokenService.getFileUploadToken();
             }
 
             private function authTokenReceived(event:ResultEvent):void
             {
                 var token:String = event.result as String;
                 var request:URLRequest = DocumentReference.constructRequestForUpload("https://hiro-xp:8080", token);
 
                 try
                 {
                     fileRef.upload(request);
                 }
                 catch (error:Error)
                 {
                     trace("Unable to upload file.");
                 }
             }
 
             // Called once the file is completely uploaded.
             private function completeHandler(event:DataEvent):void {
 
                 // Set the docRefs url and referenceType parameters
                 docRef.url = event.data as String;
                 docRef.referenceType=DocumentReference.REF_TYPE_URL;
                 executeInvokeProcess();
             }
 
             //This method invokes the EncryptDocument process
             public function executeInvokeProcess():void {
                 //Create an Object to store the input value for the EncryptDocument process
                 now1 = new Date();
 
                 var params:Object = new Object();
                 params["inDoc"]=docRef;
 
                 // Invoke the EncryptDocument process
                 var token:AsyncToken;
                 token = EncryptDocument.invoke(params);
                 token.name = name;
             }
 
 
             // This method handles a successful conversion invocation
             public function handleResult(event:ResultEvent):void
             {
 
                 //Retrieve information returned from the service invocation
                 var token:AsyncToken = event.token;
                 var res:Object = event.result;
                 var dr:DocumentReference = res["outDoc"] as DocumentReference;
                 var now2:Date = new Date();
 
                 // These fields map to columns in the DataGrid
                 var progObject:Object = new Object();
                 progObject.filename = token.name;
                 progObject.timing = (now2.time - now1.time).toString();
                 progObject.state = "Success";
                 progObject.link = "<a href='" + dr.url + "'> open </a>";
                 progressList.addItem(progObject);
             }
 
 
             private function resultHandler(event:ResultEvent):void {
             // Do anything else here.
 
             }
 
             private function logout():void
             {
                 Application.application.ssoManager.logout();
                 Application.application.showBusy();
             }
 
 
         ]]>
 
     </mx:Script>
 
     <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
             <mx:method name="invoke" result="handleResult(event)"/>
     </mx:RemoteObject>
 
 
     <!--//This consists of what is displayed on the webpage-->
     <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"
           paddingBottom="10">
         <mx:Label width="100%" color="blue"
                   id="username"/>
 
         <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"
                          dataProvider="{progressList}" height="231" selectable="false" >
         <mx:columns>
                 <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/>
                 <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/>
                 <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/>
                 <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" >
                 <mx:itemRenderer>
 
                         <mx:Component>
                         <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/>
                         </mx:Component>
                     </mx:itemRenderer>
             </mx:DataGridColumn>
         </mx:columns>
     </mx:DataGrid>
     <mx:Button label="Select File" click="uploadFile()" />
     <mx:Button label="Logout"  click="logout()" />
     </mx:Panel>
 </mx:Canvas>
 
 
```

### 追加情報 {#additional-information}

次の節では、クライアントアプリケーションとUser Managerセキュリティサーブレット間の通信に関する詳細を説明します。

### 新しい認証が発生{#a-new-authentication-occurs}

この場合、ユーザーはクライアントアプリケーションからAEM Formsに初めてログインしようとします。 （ユーザーに関係する以前のセッションは存在しません）。 `applicationComplete`イベントで、User Managerにリクエストを送信する`SSOManager.singleSignOn`メソッドが呼び出されます。

`GET /um/login?um%5Fno%5Fredirect=true HTTP/1.1`

User Managerセキュリティサーブレットは、次の値を返します。

`HTTP/1.1 200 OK`

`authenticated=false&authstate=CREDENTIAL_CHALLENGE`

この値に応答して、`SSOEvent.AUTHENTICATION_REQUIRED`値がディスパッチされます。 その結果、クライアントアプリケーションはユーザに対してログイン画面を表示する。 秘密鍵証明書がUser Managerセキュリティサーブレットに送り返されます。

`GET /um/login?um%5Fno%5Fredirect=true&j%5Fusername=administrator&j%5Fpassword=password HTTP/1.1`

User Managerセキュリティサーブレットは、次の値を返します。

```verilog
 HTTP/1.1 200 OK
 Set-Cookie: lcAuthToken=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A; Path=/
 authenticated=true&authstate=COMPLETE&assertionid=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

その結果、`authstate=COMPLETE the SSOEvent.AUTHENTICATION_SUCCESS`がディスパッチされます。 クライアントアプリケーションは、必要に応じてさらなる処理を実行できます。 例えば、ユーザーが認証された日時を追跡するログを作成できます。

### ユーザーは既に{#the-user-is-already-authenticated}認証されています

この場合、ユーザーは既にAEM Formsにログインしていて、クライアントアプリケーションに移動しています。 クライアントアプリケーションは、起動時にUser Managerセキュリティサーブレットに接続します。

```verilog
 GET /um/login?um%5Fno%5Fredirect=true HTTP/1.1
 Cookie: JSESSIONID=A4E0BCC2DD4BCCD3167C45FA350BD72A; lcAuthToken=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

ユーザーは既に認証されているので、User Manager cookieが存在し、User Managerセキュリティサーブレットに送信されます。 次に、サーブレットは`assertionId`値を取得し、有効かどうかを検証します。 有効な場合は、`authstate=COMPLETE`が返されます。 それ以外の場合は`authstate=CREDENTIAL_CHALLENGE`が返されます。 一般的な応答を次に示します。

```verilog
 HTTP/1.1 200 OK
        authenticated=true&authstate=COMPLETE&assertionid=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

この場合、ユーザーにログイン画面が表示されず、直接スタートアップスクリーンが表示されます。
