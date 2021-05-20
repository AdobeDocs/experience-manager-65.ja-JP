---
title: 外部ユーザー招待ハンドラーの作成
description: 外部ユーザー招待ハンドラーの作成
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 1%

---

# 外部ユーザー招待ハンドラーの作成{#create-invite-external-users-handler}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

Invite External Users Handlerは、Invite External Users Handlerサービス用にRights Managementできます。 Invite External Users Handlerを使用すると、Rights Managementサービスは外部ユーザーを招待してRights Managementユーザーにします。 ユーザーがRights Managementユーザーになると、ポリシーで保護されたPDFドキュメントを開くなどのタスクを実行できます。 Invite External Users HandlerがAEM Formsにデプロイされたら、管理コンソールを使用してハンドラーを操作できます。

>[!NOTE]
>
>外部ユーザー招待ハンドラーは、AEM Formsコンポーネントです。 外部ユーザー招待ハンドラーを作成する前に、コンポーネントの作成について理解しておくことをお勧めします。

**手順の概要**

外部ユーザー招待ハンドラーを作成するには、次の手順を実行する必要があります。

1. 開発環境を設定します。
1. 外部ユーザー招待ハンドラーの実装を定義します。
1. コンポーネントのXMLファイルを定義します。
1. 外部ユーザー招待ハンドラーをデプロイします。
1. 外部ユーザー招待ハンドラーをテストします。

## 開発環境の設定{#setting-up-development-environment}

開発環境を設定するには、Eclipseプロジェクトなどの新しいJavaプロジェクトを作成する必要があります。 サポートされているEclipseのバージョンは`3.2.1`以降です。

Rights ManagementSPIでは、プロジェクトのクラスパスに`edc-server-spi.jar`ファイルを設定する必要があります。 このJARファイルを参照しない場合、JavaプロジェクトでRights ManagementSPIを使用できません。 このJARファイルは、AEM Forms SDKと共に`[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi`フォルダーにインストールされます。

プロジェクトのクラスパスに`edc-server-spi.jar`ファイルを追加する以外に、Rights ManagementサービスAPIを使用するために必要なJARファイルも追加する必要があります。 これらのファイルは、Invite External Users Handler内でRights ManagementサービスAPIを使用するために必要です。

## 招待外部ユーザーハンドラー実装の定義{#define-invite-external-users-handler}

外部ユーザー招待ハンドラーを開発するには、`com.adobe.edc.server.spi.ersp.InvitedUserProvider`インターフェイスを実装するJavaクラスを作成する必要があります。 このクラスには、Rights Managementコンソールからアクセス可能な&#x200B;**招待ユーザーを追加**&#x200B;ページを使用して電子メールアドレスが送信されたときに、管理サービスが呼び出す`invitedUser`メソッドが含まれています。

`invitedUser`メソッドは、`java.util.List`インスタンスを受け取ります。このインスタンスには、**招待ユーザーの追加**&#x200B;ページから送信される、文字列型の電子メールアドレスが含まれています。 `invitedUser`メソッドは、`InvitedUserProviderResult`オブジェクトの配列を返します。通常、これは、Userオブジェクトへの電子メールアドレスのマッピングです（nullは返しません）。

>[!NOTE]
>
>この節では、招待外部ユーザーハンドラーの作成方法を示すだけでなく、AEM Forms APIも使用します。

外部ユーザー招待ハンドラーの実装には、`createLocalPrincipalAccount`という名前のユーザー定義メソッドが含まれます。 このメソッドは、電子メールアドレスをパラメーター値として指定する文字列値を受け取ります。 `createLocalPrincipalAccount`メソッドは、`EDC_EXTERNAL_REGISTERED`と呼ばれるローカルドメインが存在することを前提としています。 このドメイン名は任意の名前に設定できます。ただし、実稼動アプリケーションの場合は、をエンタープライズドメインと統合する必要が生じる場合があります。

`createUsers`メソッドは、電子メールアドレスごとに反復処理を行い、対応するUserオブジェクト（`EDC_EXTERNAL_REGISTERED`ドメインのローカルユーザー）を作成します。 最後に、`doEmails`メソッドが呼び出されます。 この方法は、意図的にサンプル内にスタブとして残されます。 実稼動環境の実装では、新しく作成したユーザーに招待の電子メールメッセージを送信するアプリケーションロジックが含まれます。 実際のアプリケーションのアプリケーションロジックフローを示すために、サンプルに残されています。

### 招待外部ユーザーハンドラー実装の定義{#user-handler-implementation}

次の招待外部ユーザーハンドラー実装は、管理コンソールからアクセスできる招待ユーザーの追加ページから送信される電子メールアドレスを受け取ります。

```as3
package com.adobe.livecycle.samples.inviteexternalusers.provider; 
 
import com.adobe.edc.server.spi.ersp.*; 
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
import com.adobe.idp.um.api.*; 
import com.adobe.idp.um.api.infomodel.*; 
import com.adobe.idp.um.api.impl.UMBaseLibrary; 
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient; 
 
import java.util.ArrayList; 
import java.util.Iterator; 
import java.util.List; 
 
public class InviteExternalUsersSample implements InvitedUserProvider 
{ 
       private ServiceClientFactory _factory = null; 
 
       private User createLocalPrincipalAccount(String email_address) throws Exception 
       { 
    String ret = null; 
 
    //  Assume the local domain already exists! 
    String domain = "EDC_EXTERNAL_REGISTERED"; 
         
    List aliases = new ArrayList(); 
    aliases.add( email_address ); 
         
    User local_user = UMBaseLibrary.createUser( email_address, domain, email_address ); 
    local_user.setCommonName( email_address ); 
    local_user.setEmail( email_address ); 
    local_user.setEmailAliases( aliases ); 
         
    //  You may wish to disable the local user until, for example, his registration is processed by a confirmation link 
    //local_user.setDisabled( true ); 
 
    DirectoryManager directory_manager = new DirectoryManagerServiceClient( _factory ); 
    String ret_oid = directory_manager.createLocalUser( local_user, null ); 
     
    if( ret_oid == null ) 
    { 
        throw new Exception( "FAILED TO CREATE PRINCIPAL FOR EMAIL ADDRESS: " + email_address ); 
    } 
 
    return local_user; 
       } 
 
       protected User[] createUsers( List emails ) throws Exception 
       { 
    ArrayList ret_users = new ArrayList(); 
 
    _factory = ServiceClientFactory.createInstance(); 
 
    Iterator iter = emails.iterator(); 
 
    while( iter.hasNext() ) 
    { 
        String current_email = (String)iter.next(); 
 
        ret_users.add( createLocalPrincipalAccount( current_email ) ); 
    } 
 
    return (User[])ret_users.toArray( new User[0] ); 
       } 
 
       protected void doInvitations(List emails) 
       { 
    //  Here you may choose to send the users who were created an invitation email 
    //  This step is completely optional, depending on your requirements.   
       } 
 
       public InvitedUserProviderResult[] invitedUser(List emails) 
       { 
    //  This sample demonstrates the workflow for inviting a user via email 
 
    try 
    { 
 
        User[] principals = createUsers(emails); 
 
        InvitedUserProviderResult[] result = new InvitedUserProviderResult[principals.length]; 
        for( int i = 0; i < principals.length; i++ ) 
        { 
        result[i] = new InvitedUserProviderResult(); 
 
        result[i].setEmail( (String)emails.get( i ) ); 
        result[i].setUser( principals[i] ); 
        } 
 
        doInvitations(emails); 
 
        System.out.println( "SUCCESSFULLY INVITED " + result.length + " USERS" ); 
 
        return result; 
 
    } 
    catch( Exception e ) 
    { 
        System.out.println( "FAILED TO INVITE USERS FOR INVITE USERS SAMPLE" ); 
        e.printStackTrace(); 
 
        return new InvitedUserProviderResult[0]; 
    } 
       } 
}
 
```

>[!NOTE]
>
>このJavaクラスは、 InviteExternalUsersSample.javaという名前のJAVAファイルとして保存されます。

## 承認ハンドラー{#define-component-xml-authorization-handler}のコンポーネントXMLファイルを定義する

外部ユーザー招待ハンドラーコンポーネントをデプロイするには、コンポーネントXMLファイルを定義する必要があります。 コンポーネントのXMLファイルは、コンポーネントごとに存在し、コンポーネントに関するメタデータを提供します。

次の`component.xml`ファイルは、外部ユーザー招待ハンドラーに使用されます。 サービス名は`InviteExternalUsersSample`で、このサービスが公開する操作の名前は`invitedUser`です。 入力パラメーターは`java.util.List`インスタンスで、出力値は`com.adobe.edc.server.spi.esrp.InvitedUserProviderResult`インスタンスの配列です。

### 招待外部ユーザーハンドラー{#component-xml-invite-external-users-handler}のコンポーネントXMLファイルを定義します

```as3
<component xmlns="http://adobe.com/idp/dsc/component/document"> 
<component-id>com.adobe.livecycle.samples.inviteexternalusers</component-id> 
<version>1.0</version> 
<bootstrap-class>com.adobe.livecycle.samples.inviteexternalusers.provider.BootstrapImpl</bootstrap-class> 
<descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
<services> 
<service name="InviteExternalUsersSample"> 
<specifications> 
<specification spec-id="com.adobe.edc.server.spi.ersp.InvitedUserProvider"/> 
</specifications> 
<specification-version>1.0</specification-version> 
<implementation-class>com.adobe.livecycle.samples.inviteexternalusers.provider.InviteExternalUsersSample</implementation-class> 
<auto-deploy category-id="Samples" service-id="InviteExternalUsersSample" major-version="1" minor-version="0"/> 
<operations> 
<operation name="invitedUser"> 
<input-parameter name="input" type="java.util.List" required="true"/> 
<output-parameter name="result" type="com.adobe.edc.server.spi.esrp.InvitedUserProviderResult[]"/> 
</operation> 
</operations> 
</service> 
</services> 
</component> 
```

## 招待外部ユーザーハンドラーのパッケージ化{#packaging-invite-external-users-handler}

外部ユーザー招待ハンドラーをAEM Formsにデプロイするには、JavaプロジェクトをJARファイルにパッケージ化する必要があります。 `edc-server-spi.jar`ファイルや`adobe-rightsmanagement-client.jar`ファイルなど、招待外部ユーザーハンドラーのビジネスロジックが依存する外部JARファイルもJARファイルに含める必要があります。 また、コンポーネントのXMLファイルが存在する必要があります。 `component.xml`ファイルと外部JARファイルは、JARファイルのルートに配置する必要があります。

>[!NOTE]
>
>下の図では、`BootstrapImpl`クラスが示されています。 この節では、`BootstrapImpl`クラスの作成方法については説明しません。

次の図に、外部ユーザー招待ハンドラーのJARファイルにパッケージ化されたJavaプロジェクトのコンテンツを示します。

![ユーザーの招待](assets/ci_ci_InviteUsers.png)

A.コンポーネントに必要な外部JARファイルB. JAVAファイル

外部ユーザー招待ハンドラーをJARファイルにパッケージ化する必要があります。 上の図では、.JAVAファイルが一覧表示されています。 JARファイルにパッケージ化したら、対応する.CLASSファイルも指定する必要があります。 .CLASSファイルがないと、承認ハンドラーは機能しません。

>[!NOTE]
>
>外部認証ハンドラーをJARファイルにパッケージ化した後、そのコンポーネントをAEM Formsにデプロイできます。 一度にデプロイできる招待外部ユーザーハンドラーは1つだけです。

>[!NOTE]
>
>また、コンポーネントをプログラムでデプロイすることもできます。

## 招待外部ユーザーハンドラーのテスト{#testing-invite-external-users-handler}

外部ユーザー招待ハンドラーをテストするには、管理コンソールを使用して、招待する外部ユーザーを追加します。

管理コンソールを使用して、招待する外部ユーザーを追加するには：

1. Workbenchを使用して、招待外部ユーザーハンドラーのJARファイルをデプロイします。
1. アプリケーションサーバーを再起動します。
1. 管理コンソールにログインします。
1. **[!UICONTROL サービス]** / **[!UICONTROL Rights Management]** / **[!UICONTROL 設定]** /招待&#x200B;**[!UICONTROL ユーザーの登録]**&#x200B;をクリックします。
1. 「**[!UICONTROL 招待ユーザーの登録を有効にする]**」ボックスをオンにして、招待ユーザーの登録を有効にします。 「**[!UICONTROL 組み込み登録システムを使用]**」で、「**[!UICONTROL いいえ]**」をクリックします。 設定を保存します。
1. 管理コンソールのホームページで、**[!UICONTROL 設定]** /**[!UICONTROL User Management]** /**[!UICONTROL ドメイン管理]**&#x200B;をクリックします。
1. 「**[!UICONTROL 新しいローカルドメイン]**」をクリックします。 次のページで、名前と識別子の値が`EDC_EXTERNAL_REGISTERED`のドメインを作成します。 変更を保存します。
1. 管理コンソールのホームページで、**[!UICONTROL サービス]** /**[!UICONTROL Rights Management]** /**[!UICONTROL 招待ユーザーおよびローカルユーザー]**&#x200B;をクリックします。 **[!UICONTROL 招待ユーザーの追加]**&#x200B;ページが表示されます。
1. 電子メールアドレスを入力します（現在の招待外部ユーザーハンドラーは、実際に電子メールメッセージを送信しないので、アドレスを有効にする必要はありません）。 「**[!UICONTROL OK]**」をクリックします。ユーザーがシステムに招待されます。
1. 管理コンソールのホームページで、**[!UICONTROL 設定]** /**[!UICONTROL User Management]** /**[!UICONTROL ユーザーとグループ]**&#x200B;をクリックします。
1. 「**[!UICONTROL 検索]**」フィールドに、指定した電子メールアドレスを入力します。 「**[!UICONTROL 検索]**」をクリックします。招待したユーザーは、ローカルの`EDC_EXTERNAL_REGISTERED`ドメインにユーザーとして表示されます。

>[!NOTE]
>
>コンポーネントが停止またはアンインストールされると、外部ユーザー招待ハンドラーは失敗します。
