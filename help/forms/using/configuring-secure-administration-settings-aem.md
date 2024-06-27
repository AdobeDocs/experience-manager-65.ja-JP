---
title: JEE 上の AEM Forms 管理者設定のセキュリティ保護の設定
description: 非公開の開発環境では必要ですが、AEM Forms on JEE の実稼動環境では必要とされないユーザーアカウントやサービスの管理方法を学びます。
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin,User
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '847'
ht-degree: 100%

---

# JEE 上の AEM Forms 管理者設定のセキュリティ保護の設定 {#configuring-secure-administration-settings-for-aem-forms-on-jee}

非公開の開発環境では必要ですが、AEM Forms on JEE の実稼動環境では必要とされないユーザーアカウントやサービスの管理方法を学びます。

通常、開発者は、アプリケーションのビルドとテストに 実稼動環境は使用しません。したがって、プライベートな開発環境には必要でも実稼動環境には必要のないユーザーアカウントとサービスを管理する必要があります。

この記事では、JEE 上の AEM Forms の管理オプションを使用して、攻撃の対象となる脆弱性を全体的に減らす方法について説明します。

## サービスへの不要なリモートアクセスの無効化 {#disabling-non-essential-remote-access-to-services}

JEE 上の AEM Forms のインストールと設定が完了したら、SOAP および Enterprise JavaBeans™（EJB）経由で、多くのサービスをリモートで起動できるようになります。「リモート」という用語は、この場合、アプリケーションサーバーの SOAP、EJB または Action Message Format（AMF）のポートにネットワークアクセス可能なすべての呼び出し元を意味します。

JEE 上の AEM Forms サービスでは、承認された呼び出し元であることを示す有効な資格情報が要求されますが、リモートアクセスが必要なサービスに対してのみリモートアクセスを許可する必要があります。限定的なアクセシビリティを実現するには、まず、システムとして機能するために必要な最小限のサービス群だけをリモートアクセス可能にします。その後、必要に応じて他のサービスのリモート起動を許可する必要があります。

JEE 上の AEM Forms サービスには、少なくとも SOAP アクセスが常に必要です。これらのサービスは、通常は Workbench で使用するために必要とされますが、Workspace web アプリケーションによって呼び出されるサービスである場合もあります。

管理コンソールのアプリケーションおよびサービス web ページを使用して、次の手順を実行してください。

1. Web ブラウザーに次の URL を入力して管理コンソールにログインします。

   ```java
            https://[host name]:'port'/adminui
   ```

1. **サービス／アプリケーションおよびサービス／環境設定**&#x200B;をクリックします。
1. 環境設定で、同じページにサービスとエンドポイントを最大 200 個まで表示するように設定します。
1. **サービス**／**アプリケーションおよびサービス**／**エンドポイントの管理**&#x200B;をクリックします。
1. **プロバイダー**&#x200B;リストから「**EJB**」を選択して、「**フィルター**」をクリックします。
1. すべての EJB エンドポイントを無効にするには、リスト内でそれぞれの横にあるチェックボックスをオンにして、「**無効にする**」をクリックします。
1. 「**次へ**」をクリックして、すべての EJB エンドポイントに関して、前述の手順を繰り返します。エンドポイントを無効にする前に、「プロバイダー」列に EJB が表示されていることを確認します。
1. **プロバイダー**&#x200B;リストから「**SOAP**」を選択して、「**フィルター**」をクリックします。
1. SOAP エンドポイントを削除するには、リスト内でそれぞれの横にあるチェックボックスをオンにして、「**削除**」をクリックします。次のエンドポイントは削除しないでください。

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

1. 「**次へ**」をクリックして、上記のリストにない SOAP エンドポイントに関して、前述の手順を繰り返します。エンドポイントを削除する前に、「プロバイダー」列に SOAP が表示されていることを確認します。

## サービスへの不要な匿名アクセスの無効化 {#disabling-non-essential-anonymous-access-to-services}

一部の Forms サーバーサービスについては、未承認（匿名）ユーザーが呼び出して一部の操作を実行することが許可されます。つまり、サービスによって公開されている 1 つまたは複数の操作は、認証された任意のユーザーだけでなく、認証されていない任意のユーザーによって呼び出される可能性があります。

1. Web ブラウザーに次の URL を入力して、管理コンソールにログインします。

   ```java
            https://[host name]:'port'/adminui
   ```

1. **サービス／アプリケーションおよびサービス／サービスの管理**&#x200B;をクリックします。
1. 無効にするサービスの名前（AuthenticationManagerService など）をクリックします。
1. **「セキュリティ」タブ**&#x200B;をクリックし、**匿名アクセスが許可されました**&#x200B;の選択を解除して、「**保存**」をクリックしてください。
1. 次のサービスに関して手順 3 と 4 を完了させます。

   * AuthenticationManagerService
   * EJB
   * メール
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

   これらのサービスをリモート起動できるようする場合は、匿名アクセスを無効にすることを考慮する必要があります。そうしないと、これらのサービスにネットワークアクセス可能な任意の呼び出し元が、有効な資格情報を渡さずにサービスを起動するおそれがあります。

   匿名アクセスは、必要でないサービスでは無効にすることをお勧めします。内部サービスは、原則的にシステム内のすべてのユーザーが認証なしで呼び出せる必要があるので、多くの場合、内部サービスでは匿名認証を有効にする必要があります。

## デフォルトグローバルタイムアウトの変更 {#changing-the-default-global-time-out}

エンドユーザーが AEM Forms に対して認証を行う手段としては、Workbench、AEM Forms web アプリケーションや、AEM Forms サーバーサービスを呼び出すカスタムアプリケーションがあります。グローバルタイムアウト設定を使用すると、再認証を要求されるまでにユーザーが（SAML ベースアサーションを使用して）AEM Forms とやり取りできる時間を指定できます。デフォルト設定は 2 時間です。実稼動環境では、この時間を、設定可能な分単位の最小値に変更する必要があります。

### 再認証時間制限の最小化 {#minimize-reauthentication-time-limit}

1. Web ブラウザーに次の URL を入力して、管理コンソールにログインします。

   ```java
            https://[host name]:'port'/adminui
   ```

1. **設定／User Management／設定／既存の設定ファイルの読み込みと書き出し**&#x200B;をクリックします。
1. 「**書き出し**」をクリックして、既存の AEM Forms の設定を含んだ config.xml ファイルを生成します。
1. エディターで XML ファイルを開き、次のエントリを見つけます。

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. 値を 5（分単位）より大きい任意の数に変更し、ファイルを保存します。
1. 管理コンソールで、既存の設定ファイルの読み込みと書き出しページに移動します。
1. 変更された config.xml ファイルへのパスを入力するか、「参照」をクリックしてこのファイルに移動します。
1. 「**読み込み**」をクリックし、変更された config.xml ファイルをアップロードして、「**OK**」をクリックします。
