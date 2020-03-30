---
title: JEE上のAEM Formsのセキュア管理設定の指定
seo-title: JEE上のAEM Formsのセキュア管理設定の指定
description: JEE上のAEM Formsの実稼働環境で必要とされない、プライベート開発環境で必要なユーザーアカウントやサービスを管理する方法を説明します。
seo-description: JEE上のAEM Formsの実稼働環境で必要とされない、プライベート開発環境で必要なユーザーアカウントやサービスを管理する方法を説明します。
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configuring Secure Administration Settings for AEM Forms on JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

JEE上のAEM Formsの実稼働環境で必要とされない、プライベート開発環境で必要なユーザーアカウントやサービスを管理する方法を説明します。

通常、開発者は、アプリケーションのビルドとテストに 実稼働環境は使用しません。したがって、プライベートな開発環境には必要でも実稼働環境には必要のないユーザーアカウントとサービスを管理する必要があります。

この記事では、JEE 上の AEM Forms の管理オプションを使用して、攻撃の対象となる脆弱性を全体的に減らす方法について説明します。

## サービスへの不要なリモートアクセスの無効化 {#disabling-non-essential-remote-access-to-services}

JEE 上の AEM Forms のインストールと設定が完了したら、SOAP および Enterprise JavaBeans™（EJB）経由で、多くのサービスをリモートで起動できるようになります。「リモート」という用語は、この場合、アプリケーションサーバーの SOAP、EJB または Action Message Format（AMF）のポートにネットワークアクセス可能なすべての呼び出し元を意味します。

JEE 上の AEM Forms サービスを呼び出すには、承認された呼び出し元であることを示す有効な資格情報が要求されます。それでも、リモートアクセスを認める必要がないサービスをリモートアクセス可能な状態にしておくことは望ましくありません。アクセスを制限するには、まず、システムとして機能するために必要な最小限のサービス群だけをリモートアクセス可能にします。その後、必要に応じて他のサービスのリモート起動を許可していくようにします。

JEE 上の AEM Forms サービスには、少なくとも SOAP アクセスが常に必要です。これらのサービスは、通常は Workbench で使用するために必要とされますが、Workspace Web アプリケーションによって呼び出されるサービスである場合もあります。

管理コンソールのアプリケーションおよびサービスWebページを使用して、次の手順を実行します。

1. Webブラウザーに次のURLを入力して、管理コンソールにログインします。

   ```as3
            https://[host name]:'port'/adminui
   ```

1. **サービス／アプリケーションおよびサービス／環境設定**&#x200B;をクリックします。
1. 環境設定で、同じページにサービスとエンドポイントを 200 個まで表示するように設定します。
1. **サービス**／**アプリケーションおよびサービス**／**エンドポイントの管理**&#x200B;をクリックします。
1. **プロバイダー**&#x200B;リストから「**EJB**」を選択して、「**フィルター**」をクリックします。
1. すべての EJB エンドポイントを無効にするには、リスト内でそれぞれの横にあるチェックボックスを選択して、「**無効にする**」をクリックします。
1. 「**次へ**」をクリックして、すべての EJB エンドポイントに関して、前述の手順を繰り返します。エンドポイントを無効にする前に、「プロバイダー」列に EJB が表示されていることを確認してください。
1. **プロバイダー**&#x200B;リストから「**SOAP**」を選択して、「**フィルター**」をクリックします。
1. SOAP エンドポイントを削除するには、リスト内でそれぞれの横にあるチェックボックスを選択して、「**削除**」をクリックします。以下のエンドポイントは削除しないでください。

   * AuthenticationManagerService
   * DirectoryManagerService
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * TaskQueueManager
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * ApplicationManager

1. 「**次へ**」をクリックして、上記のリストにない SOAP エンドポイントに関して、前述の手順を繰り返します。エンドポイントを削除する前に、「プロバイダー」列に SOAP が表示されていることを確認してください。

## サービスへの不要な匿名アクセスの無効化 {#disabling-non-essential-anonymous-access-to-services}

一部の forms サーバーサービスについては、未承認（匿名）ユーザーが呼び出して一部の操作を実行することが許可されます。つまり、サービスによって公開されている一部の操作は、認証された任意のユーザーだけでなく、認証されていない任意のユーザーによって呼び出される可能性があります。

1. Web ブラウザーに次の URL を入力して管理コンソールにログインします。

   ```as3
            https://[host name]:'port'/adminui
   ```

1. **サービス／アプリケーションおよびサービス／サービスの管理**&#x200B;をクリックします。
1. 無効にするサービスの名前（AuthenticationManagerService など）をクリックします。
1. Click the **Security tab**, deselect **Anonymous Access Allowed**, and click **Save**.
1. 以下のサービスに関して手順 3 と 4 を繰り返します。

   * AuthenticationManagerService
   * EJB
   * 電子メール
   * JobManager
   * WatchedFolder
   * UsermanagerUtilService
   * Remoting
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * TaskManagerService
   * TaskManagerConnector
   * TaskManagerQueryService
   * TaskQueueManager
   * TaskEndpointManager
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService
   これらのサービスをリモート起動できるようする場合は、匿名アクセスを無効にすることを考慮してください。そうしないと、これらのサービスにネットワークアクセス可能な任意の呼び出し元が、有効な資格情報を渡さずにサービスを起動するおそれがあります。

   匿名アクセスは、必要でないサービスでは無効にすることをお勧めします。内部サービスは、原則的にシステム内のすべてのユーザーが認証なしで呼び出せる必要があるので、多くの場合、内部サービスでは匿名認証を有効にする必要があります。

## デフォルトグローバルタイムアウトの変更 {#changing-the-default-global-time-out}

エンドユーザーは、Workbench、AEM Forms Webアプリケーション、またはAEM Formsサーバーサービスを呼び出すカスタムアプリケーションを通じて、AEM Formsに対して認証を行うことができます。 グローバルタイムアウト設定を使用すると、再認証を要求されるまでにユーザーが（SAML ベースアサーションを使用して）AEM Forms とやり取りできる時間を指定することができます。デフォルト設定は 2 時間です。実稼働環境では、この時間を、設定可能な分単位の最小値に変更する必要があります。

### 再認証時間制限の最小化 {#minimize-reauthentication-time-limit}

1. Web ブラウザーに次の URL を入力して管理コンソールにログインします。

   ```as3
            https://[host name]:'port'/adminui
   ```

1. **設定／User Management／設定／既存の設定ファイルの読み込みと書き出し**&#x200B;をクリックします。
1. 「**書き出し**」をクリックして、既存の AEM Forms の設定を含んだ config.xml ファイルを生成します。
1. エディターで XML ファイルを開き、次のエントリを見つけます。

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. 値を 5（分単位）より大きい任意の数に変更し、ファイルを保存します。
1. 管理コンソールで、既存の設定ファイルの読み込みと書き出しページに戻ります。
1. 変更された config.xml ファイルへのパスを入力するか、「参照」をクリックしてこのファイルに移動します。
1. 「**読み込み**」をクリックし、変更された config.xml ファイルをアップロードして、「**OK**」をクリックします。

