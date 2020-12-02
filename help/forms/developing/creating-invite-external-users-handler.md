---
title: Invite External Usersハンドラーの作成
description: Invite External Usersハンドラーの作成
translation-type: tm+mt
source-git-commit: 92e5cc0b1934dad641357a22894e70a3660b774a
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 1%

---


# Invite External Usersハンドラーの作成{#create-invite-external-users-handler}

Rights Managementサービス用のInvite External Usersハンドラーを作成できます。 「Invite External Users」ハンドラーを使用すると、Rights Managementサービスは外部ユーザーをRights Managementユーザーに招待できます。 ユーザーがRights Managementユーザーになった後は、ポリシーで保護されたPDFドキュメントを開くなどのタスクを実行できます。 外部ユーザーの招待ハンドラーをAEM Formsにデプロイすると、管理コンソールを使用して外部ユーザーハンドラーを操作できます。

>[!NOTE]
>
>Invite External Usersハンドラーは、AEM Formsコンポーネントです。 「外部ユーザーの招待ハンドラー」を作成する前に、コンポーネントの作成について理解しておくことをお勧めします。

**手順の概要**

外部ユーザーの招待ハンドラーを作成するには、次の手順を実行する必要があります。

1. 開発環境を設定します。
1. 外部ユーザーの招待ハンドラーの実装を定義します。
1. コンポーネントのXMLファイルを定義します。
1. Invite External Usersハンドラーをデプロイします。
1. 外部ユーザーの招待ハンドラーをテストします。

## 開発環境のセットアップ{#setting-up-development-environment}

開発環境を設定するには、Eclipseプロジェクトなどの新しいJavaプロジェクトを作成する必要があります。 サポートされるEclipseのバージョンは`3.2.1`以降です。

Rights ManagementSPIでは、プロジェクトのクラスパスに`edc-server-spi.jar`ファイルを設定する必要があります。 このJARファイルを参照しない場合、JavaプロジェクトでRights ManagementSPIを使用できません。 このJARファイルは、`[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi`フォルダーのAEM FormsSDKと共にインストールされます。

プロジェクトのクラスパスに`edc-server-spi.jar`ファイルを追加するだけでなく、Rights ManagementサービスAPIの使用に必要なJARファイルも追加する必要があります。 これらのファイルは、Invite External Usersハンドラー内でRights ManagementサービスAPIを使用するために必要です。

## Invite External Usersハンドラーの実装の定義{#define-invite-external-users-handler}

招待外部ユーザーハンドラーを開発するには、`com.adobe.edc.server.spi.ersp.InvitedUserProvider`インターフェイスを実装するJavaクラスを作成する必要があります。 このクラスには`invitedUser`という名前のメソッドが含まれています。このメソッドは、管理コンソールからアクセスできる&#x200B;**追加ユーザーの招待**&#x200B;ページを使用して電子メールアドレスが送信されたときにRights Managementサービスが呼び出します。

`invitedUser`メソッドは、**ユーザーの追加招待**&#x200B;ページから送信された、文字列で型指定された電子メールアドレスを含む`java.util.List`インスタンスを受け入れます。 `invitedUser`メソッドは、`InvitedUserProviderResult`オブジェクトの配列を返します。これは、通常、Userオブジェクトへの電子メールアドレスのマッピングです（nullは返しません）。

>[!NOTE]
>
>この節では、Invite External Usersハンドラーの作成方法を説明するだけでなく、AEM FormsAPIも使用します。

外部ユーザーの招待ハンドラーの実装には、`createLocalPrincipalAccount`という名前のユーザー定義メソッドが含まれています。 このメソッドは、電子メールアドレスをパラメーター値として指定する文字列値を受け取ります。 `createLocalPrincipalAccount`メソッドは、`EDC_EXTERNAL_REGISTERED`というローカルドメインが存在することを前提としています。 このドメイン名は任意の名前に設定できます。ただし、実稼働用アプリケーションの場合は、エンタープライズドメインと統合する必要があります。

`createUsers`メソッドは、各電子メールアドレスを反復し、対応するUserオブジェクト（`EDC_EXTERNAL_REGISTERED`ドメインのローカルユーザー）を作成します。 最後に、`doEmails`メソッドが呼び出されます。 このメソッドは、意図的にサンプル内にスタブとして残されます。 実稼働環境では、新しく作成したユーザーに招待用の電子メールメッセージを送信するアプリケーションロジックが含まれます。 実際のアプリケーションのアプリケーションロジックのフローを示すために、サンプルに残しておきます。

### Invite External Usersハンドラーの実装の定義{#user-handler-implementation}

次のinvite external usersハンドラーの実装は、管理コンソールからアクセスできる追加ユーザーの招待ページから送信された電子メールアドレスを受け付けます。

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
>このJavaクラスは、InviteExternalUsersSample.javaという名前のJAVAファイルとして保存されます。

## 認証ハンドラー{#define-component-xml-authorization-handler}のコンポーネントXMLファイルを定義する

invite external users handlerコンポーネントをデプロイするには、コンポーネントXMLファイルを定義する必要があります。 コンポーネントXMLファイルは各コンポーネントに対して存在し、コンポーネントに関するメタデータを提供します。

次の`component.xml`ファイルは、外部ユーザーの招待ハンドラーに使用されます。 サービス名が`InviteExternalUsersSample`で、このサービスが公開する操作の名前は`invitedUser`です。 入力パラメーターは`java.util.List`インスタンスで、出力値は`com.adobe.edc.server.spi.esrp.InvitedUserProviderResult`インスタンスの配列です。

### Invite External UsersハンドラーのコンポーネントXMLファイルの定義{#component-xml-invite-external-users-handler}

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

## Invite External Usersハンドラーのパッケージ化{#packaging-invite-external-users-handler}

Invite外部ユーザーハンドラーをAEM Formsにデプロイするには、JavaプロジェクトをJARファイルにパッケージ化する必要があります。 `edc-server-spi.jar`ファイルや`adobe-rightsmanagement-client.jar`ファイルなど、invite外部ユーザーハンドラーのビジネスロジックが依存する外部JARファイルもJARファイルに含める必要があります。 また、コンポーネントのXMLファイルが存在する必要があります。 `component.xml`ファイルと外部JARファイルは、JARファイルのルートに配置する必要があります。

>[!NOTE]
>
>下の図では、`BootstrapImpl`クラスが示されています。 この節では、`BootstrapImpl`クラスの作成方法については説明しません。

次の図に、Javaプロジェクトのコンテンツを示します。このコンテンツは、invite external usersハンドラーのJARファイルにパッケージ化されています。

![ユーザーの招待](assets/ci_ci_InviteUsers.png)

A.コンポーネントに必要な外部JARファイルB. JAVAファイル

invite外部ユーザーハンドラーは、JARファイルにパッケージ化する必要があります。 上の図では、.JAVAファイルが表示されています。 JARファイルにパッケージ化した後は、対応する.CLASSファイルも指定する必要があります。 .CLASSファイルがない場合、認証ハンドラは機能しません。

>[!NOTE]
>
>外部認証ハンドラーをJARファイルにパッケージ化した後、コンポーネントをAEM Formsにデプロイできます。 1度に1つの招待外部ユーザーハンドラーのみを展開できます。

>[!NOTE]
>
>プログラムによってコンポーネントをデプロイすることもできます。

## Invite External Usersハンドラー{#testing-invite-external-users-handler}のテスト

招待外部ユーザーハンドラーをテストするには、管理コンソールを使用して、招待する外部ユーザーを追加します。

管理コンソールを使用して招待する外部ユーザーを追加するには：

1. Workbenchを使用して、invite外部ユーザーハンドラーのJARファイルをデプロイします。
1. アプリケーションサーバーを再起動します。
1. 管理コンソールにログインします。
1. **[!UICONTROL サービス]**/**[!UICONTROL Rights Management]**/**[!UICONTROL 設定]**/招待&#x200B;**[!UICONTROL ユーザー登録]**&#x200B;をクリックします。
1. 「**[!UICONTROL 招待ユーザーの登録を有効にする]**」ボックスをオンにして、招待ユーザーの登録を有効にします。 「**[!UICONTROL 組み込みの登録システム]**&#x200B;を使用」で、「**[!UICONTROL いいえ]**」をクリックします。 設定を保存します。
1. 管理コンソールホームページで、**[!UICONTROL 設定]**/**[!UICONTROL User Management]**/**[!UICONTROL ドメインの管理]**&#x200B;をクリックします。
1. 「**[!UICONTROL 新しいローカルドメイン]**」をクリックします。 次のページで、名前と識別子の値`EDC_EXTERNAL_REGISTERED`を持つドメインを作成します。 変更を保存します。
1. 管理コンソールホームページで、**[!UICONTROL サービス]**/**[!UICONTROL Rights Management]**/**[!UICONTROL 招待ユーザーおよびローカルユーザー]**&#x200B;をクリックします。 **[!UICONTROL 追加ユーザーの招待]**&#x200B;ページが表示されます。
1. 電子メールアドレスを入力します（現在の招待外部ユーザーハンドラーは、実際に電子メールメッセージを送信しないので、電子メールアドレスを有効にする必要はありません）。 「**[!UICONTROL OK]**」をクリックします。ユーザーがシステムに招待されます。
1. 管理コンソールホームページで、**[!UICONTROL 設定]**/**[!UICONTROL ユーザー管理]**/**[!UICONTROL ユーザーとグループ]**&#x200B;をクリックします。
1. 「**[!UICONTROL 検索]**」フィールドに、指定した電子メールアドレスを入力します。 「**[!UICONTROL 検索]**」をクリックします。招待したユーザーは、ローカル`EDC_EXTERNAL_REGISTERED`ドメインにユーザーとして表示されます。

>[!NOTE]
>
>コンポーネントが停止またはアンインストールされている場合、Invite External Usersハンドラーは失敗します。
