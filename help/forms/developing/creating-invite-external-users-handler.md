---
title: 外部ユーザー招待ハンドラーの作成
description: 外部ユーザー招待ハンドラーの作成
role: Developer
exl-id: b0416716-dcc9-4f80-986a-b9660a7c8f6b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1116'
ht-degree: 100%

---

# 外部ユーザー招待ハンドラーの作成 {#create-invite-external-users-handler}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Rights Management サービス用に外部ユーザー招待ハンドラーを作成できます。外部ユーザー招待ハンドラーを使用すると、Rights Management サービスは外部ユーザーを招待して Rights Management ユーザーにすることができます。Rights Management ユーザーになると、ポリシーで保護された PDF ドキュメントを開くなどのタスクを実行できるようになります。外部ユーザー招待ハンドラーが AEM Forms にデプロイされたら、管理コンソールを使用してハンドラーを操作できます。

>[!NOTE]
>
>外部ユーザー招待ハンドラーは、AEM Forms のコンポーネントです。外部ユーザー招待ハンドラーを作成する前に、コンポーネントの作成について理解しておくことをお勧めします。

**手順の概要**

外部ユーザー招待ハンドラーを作成するには、次の手順を実行する必要があります。

1. 開発環境を設定します。
1. 外部ユーザー招待ハンドラーの実装を定義します。
1. コンポーネントの XML ファイルを定義します。
1. 外部ユーザー招待ハンドラーをデプロイします。
1. 外部ユーザー招待ハンドラーをテストします。

## 開発環境の設定 {#setting-up-development-environment}

開発環境を設定するには、Eclipse プロジェクトなどの新しい Java プロジェクトを作成する必要があります。サポートしている Eclipse のバージョンは `3.2.1` 以降です。

Rights Management SPI にはプロジェクトのクラスパスに設定する `edc-server-spi.jar` ファイルが必要です。この JAR ファイルを参照しない場合、Java プロジェクトで Rights Management SPI を使用できません。この JAR ファイルは、AEM Forms SDK と共に `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` フォルダーにインストールされています。

また、`edc-server-spi.jar` ファイルをプロジェクトのクラスパスに追加する場合は、Rights Management サービス API の使用に必要な JAR ファイルも追加する必要があります。これらのファイルは、外部ユーザー招待ハンドラー内で Rights Management サービス API を使用するために必要です。

## 外部ユーザー招待ハンドラー実装の定義 {#define-invite-external-users-handler}

外部ユーザー招待ハンドラーを開発するには、 `com.adobe.edc.server.spi.ersp.InvitedUserProvider` インターフェイスを実装する Java クラスを作成する必要があります。このクラスには、管理コンソールからアクセスできる&#x200B;**招待ユーザーの追加**&#x200B;ページを使用してメールアドレスが送信されたときに Rights Management サービスが呼び出す `invitedUser` という名前のメソッドが含まれています。

`invitedUser` メソッドは `java.util.List` インスタンスを受け入れます。これには、**招待ユーザーの追加**&#x200B;ページから送信される、文字列型のメールアドレスが含まれます。`invitedUser` メソッドは、 `InvitedUserProviderResult` オブジェクトの配列を返します。これは通常、メールアドレスからユーザーオブジェクトへのマッピングです（null を返さない）。

>[!NOTE]
>
>この節では、外部ユーザー招待ハンドラーの作成方法を示すだけでなく、AEM Forms API も使用します。

外部ユーザー招待ハンドラーの実装には、`createLocalPrincipalAccount` という名前のユーザー定義メソッドが含まれます。このメソッドは、メールアドレスをパラメーター値として指定する文字列値を受け入れます。 `createLocalPrincipalAccount` メソッドは、 `EDC_EXTERNAL_REGISTERED` と呼ばれるローカルドメインがすでに存在することを前提としています。このドメイン名は任意の名前に設定できます。ただし、本番アプリケーションの場合は、エンタープライズドメインと統合する必要がある場合があります。

`createUsers` メソッドは、すべてのメールアドレスを反復処理し、対応するユーザーオブジェクト（`EDC_EXTERNAL_REGISTERED` ドメインのローカルユーザー）を作成します。最後に、`doEmails` メソッドが呼び出されます。このメソッドは、サンプル内でスタブとして意図的に残されています。本番環境の実装では、新しく作成したユーザーに招待用のメールメッセージを送信するアプリケーションロジックが含まれます。実際のアプリケーションのアプリケーションロジックフローを示すために、サンプルに残しておきます。

### 外部ユーザー招待ハンドラー実装の定義 {#user-handler-implementation}

次の外部ユーザー招待ハンドラーの実装は、管理コンソールからアクセスできる招待ユーザーの追加ページから送信される電子メールアドレスを受け付けます。

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
>この Java クラスは、InviteExternalUsersSample.java という名前の JAVA ファイルとして保存されます。

## 承認ハンドラー用のコンポーネント XML ファイルの定義 {#define-component-xml-authorization-handler}

外部ユーザー招待ハンドラーコンポーネントをデプロイするには、コンポーネント XML ファイルを定義する必要があります。 コンポーネントの XML ファイルは、コンポーネントごとに存在し、コンポーネントに関するメタデータを提供します。

以下の `component.xml` ファイルは、外部ユーザー招待ハンドラーに使用されます。 サービス名は `InviteExternalUsersSample` でこのサービスが公開する操作の名前は `invitedUser` です。入力パラメーターは `java.util.List` インスタンスで、出力値は `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` インスタンスの配列です。

### 外部ユーザー招待ハンドラー用のコンポーネント XML ファイルの定義 {#component-xml-invite-external-users-handler}

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

## 外部ユーザー招待ハンドラーのパッケージ化 {#packaging-invite-external-users-handler}

外部ユーザー招待ハンドラーを AEM Forms にデプロイするには、Java プロジェクトを JAR ファイルにパッケージ化する必要があります。外部ユーザー招待ハンドラーのビジネスロジックが依存する外部 JAR ファイル（`edc-server-spi.jar` および `adobe-rightsmanagement-client.jar` ファイル）は、JAR ファイルにも含まれます。 また、コンポーネントの XML ファイルが存在する必要があります。`component.xml` ファイルと外部 JAR ファイルは、JAR ファイルのルートに配置する必要があります。

>[!NOTE]
>
>下の図では、 `BootstrapImpl` クラスが表示されます。この節では、`BootstrapImpl` クラスを作成する方法については説明しません。

次の図は、外部ユーザー招待ハンドラーの JAR ファイルにパッケージ化された Java プロジェクトのコンテンツを示しています。

![ユーザーの招待](assets/ci_ci_InviteUsers.png)

A.コンポーネントに必要な外部 JAR ファイル B. JAVA ファイル

外部ユーザー招待ハンドラーを JAR ファイルにパッケージ化する必要があります。前の図では、.JAVA ファイルが表示されています。JAR ファイルにパッケージ化した後は、対応する .CLASS ファイルも指定する必要があります。.CLASS ファイルがないと、認証ハンドラーは機能しません。

>[!NOTE]
>
>外部認証ハンドラーを JAR ファイルにパッケージ化したら、そのコンポーネントを AEM Forms にデプロイできます。一度に 1 つの外部ユーザー招待ハンドラーのみをデプロイできます。

>[!NOTE]
>
>また、コンポーネントをプログラムでデプロイすることもできます。

## 外部ユーザー招待ハンドラーのテスト {#testing-invite-external-users-handler}

外部ユーザー招待ハンドラーをテストするには、管理コンソールを使用して、招待する外部ユーザーを追加します。

管理コンソールを使用して、招待する外部ユーザーを追加するには、次をおこないます。

1. Workbench を使用して、外部ユーザー招待ハンドラーの JAR ファイルをデプロイします。
1. アプリケーションサーバーを再起動します。
1. 管理コンソールにログインします。
1.  **[!UICONTROL サービス]**／**[!UICONTROL Rights Management]**／**[!UICONTROL 設定]**／ 招待済み&#x200B;**[!UICONTROL ユーザーの登録]**&#x200B;をクリックします。
1. 招待ユーザーの登録を有効にするには、**[!UICONTROL 招待ユーザーの登録を有効にする]**&#x200B;ボックスをオンにします。**[!UICONTROL 組み込み登録システムを使用]**&#x200B;の下で「**[!UICONTROL いいえ]**」をクリックします。設定を保存します。
1. 管理コンソールホームページで、**[!UICONTROL 設定]**／**[!UICONTROL User Management]**／**[!UICONTROL ドメイン管理]**&#x200B;をクリックします。
1. 「**[!UICONTROL 新規ローカルドメイン]**」をクリックします。次のページで、名前と識別子の値が `EDC_EXTERNAL_REGISTERED` のドメインを作成します。変更を保存します。
1. 管理コンソールホームページで、**[!UICONTROL サービス]**／**[!UICONTROL Rights Management]**／**[!UICONTROL 招待ユーザーとローカルユーザー]**&#x200B;をクリックします。**[!UICONTROL 招待ユーザーの追加]**&#x200B;ページが表示されます。
1. メールアドレスを入力します（現在の外部ユーザー招待ハンドラーは、メールメッセージを実際に送信しないので、アドレスが有効である必要はありません）。 「**[!UICONTROL OK]**」をクリックします。ユーザーがシステムに招待されます。
1. 管理コンソールホームページで、 **[!UICONTROL 設定]**／**[!UICONTROL User Management]**／**[!UICONTROL ユーザーとグループ]**&#x200B;をクリックします。
1. 「**[!UICONTROL 検索]**」フィールドに、指定したメールアドレスを入力します。「**[!UICONTROL 検索]**」をクリックします。招待したユーザーは、ローカルの `EDC_EXTERNAL_REGISTERED` ドメインに表示されます。

>[!NOTE]
>
>コンポーネントが停止またはアンインストールされると、外部ユーザー招待ハンドラーが失敗します。
