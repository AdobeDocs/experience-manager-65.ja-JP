---
title: JEE 上の AEM Forms 管理者設定のセキュリティ保護の設定
seo-title: Configuring Secure Administration Settings for AEM Forms on JEE
description: 非公開の開発環境では必要ですが、AEM Forms on JEE の実稼動環境では必要とされないユーザーアカウントやサービスの管理方法を学びます。
seo-description: Learn how to administer user accounts and services that, although required in a private development environment, are not required in a production environment of AEM Forms on JEE.
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
role: Admin
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 16%

---

# JEE 上の AEM Forms 管理者設定のセキュリティ保護の設定 {#configuring-secure-administration-settings-for-aem-forms-on-jee}

非公開の開発環境では必要ですが、AEM Forms on JEE の実稼動環境では必要とされないユーザーアカウントやサービスの管理方法を学びます。

一般に、開発者は、実稼動環境を使用してアプリケーションをビルドおよびテストしません。 したがって、実稼動環境では必要ない、プライベート開発環境では必要なユーザーアカウントやサービスを管理する必要があります。

この記事では、JEE 上のAEM Formsが提供する管理オプションを使用して、攻撃の対象となる領域を全体的に減らす方法について説明します。

## サービスへの不要なリモートアクセスの無効化 {#disabling-non-essential-remote-access-to-services}

JEE 上のAEM Formsをインストールし、設定した後、SOAP および Enterprise JavaBeans™ (EJB) を介したリモート呼び出しに多くのサービスを使用できます。この場合、リモートとは、アプリケーションサーバーの SOAP、EJB、または Action Message Format (AMF) ポートにネットワークアクセスできる呼び出し元を指します。

JEE 上のAEM Formsサービスでは、許可された呼び出し元に対して有効な資格情報を渡す必要がありますが、リモートからアクセスする必要のあるサービスへのリモートアクセスのみを許可する必要があります。 アクセシビリティを制限するには、リモートからアクセス可能なサービスのセットを、システムが機能するのに最小限に抑え、必要な追加のサービスのリモート呼び出しを有効にする必要があります。

AEM Forms on JEE サービスには、少なくとも SOAP アクセスが常に必要です。 これらのサービスは、通常、Workbench での使用に必要ですが、Workspace Web アプリケーションによって呼び出されるサービスも含まれます。

管理コンソールのアプリケーションおよびサービス web ページを使用して、次の手順を実行してください。

1. Web ブラウザーに次の URL を入力して管理コンソールにログインします。

   ```java
            https://[host name]:'port'/adminui
   ```

1. クリック **サービス/アプリケーションおよびサービス/環境設定**.
1. 環境設定を設定して、同じページ上の最大 200 個のサービスとエンドポイントを表示できます。
1. クリック **サービス** > **アプリケーションとサービス** > **エンドポイント管理**.
1. 選択 **EJB** から **プロバイダー** リストを開き、をクリックします。 **フィルター**.
1. すべての EJB エンドポイントを無効にするには、リスト内の各エンドポイントの横にあるチェックボックスを選択し、 **無効にする**.
1. クリック **次へ** をクリックし、すべての EJB エンドポイントに対して前の手順を繰り返します。 エンドポイントを無効にする前に、EJB が「プロバイダー」列に表示されていることを確認します。
1. 選択 **SOAP** から **プロバイダー** リストを開き、をクリックします。 **フィルター**.
1. SOAP エンドポイントを削除するには、リスト内で各エンドポイントの横にあるチェックボックスを選択し、 **削除**. 次のエンドポイントを削除しないでください。

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

1. クリック **次へ** 上記のリストにない SOAP エンドポイントに対して、前の手順を繰り返します。 エンドポイントを削除する前に、SOAP が「プロバイダー」列に表示されていることを確認してください。

## サービスへの不要な匿名アクセスの無効化 {#disabling-non-essential-anonymous-access-to-services}

一部のForms Server サービスでは、未認証（匿名）の呼び出しを一部の操作に対して許可しています。 つまり、サービスによって公開されている 1 つ以上の操作が、認証済みユーザーとして呼び出される場合も、認証済みユーザーとして呼び出される場合も、まったく呼び出されない場合もあります。

1. Web ブラウザーに次の URL を入力して、管理コンソールにログインします。

   ```java
            https://[host name]:'port'/adminui
   ```

1. クリック **[ サービス ] > [ アプリケーションとサービス ] > [ サービスの管理 ]**.
1. 無効にするサービスの名前（AuthenticationManagerService など）をクリックします。
1. **「セキュリティ」タブ**&#x200B;をクリックし、**匿名アクセスが許可されました**&#x200B;の選択を解除して、「**保存**」をクリックしてください。
1. 次のサービスの手順 3 と 4 を実行します。

   * AuthenticationManagerService
   * EJB
   * メール
   * JobManager
   * WatchedFolder
   * UsermanagerUtilService
   * リモート
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

   リモート呼び出し用にこれらのサービスのいずれかを公開する場合は、これらのサービスの匿名アクセスを無効にすることも検討してください。 そうしないと、このサービスへのネットワークアクセス権を持つ呼び出し元が、有効な資格情報を渡さずにサービスを呼び出す可能性があります。

   不要なサービスに対しては、匿名アクセスを無効にする必要があります。 多くの内部サービスでは、匿名認証を有効にする必要があります。これは、事前認証を受けずにシステム内の任意のユーザーが呼び出す必要があるからです。

## デフォルトグローバルタイムアウトの変更 {#changing-the-default-global-time-out}

エンドユーザーが AEM Forms に対して認証を行う手段としては、Workbench、AEM Forms web アプリケーションや、AEM Forms サーバーサービスを呼び出すカスタムアプリケーションがあります。1 つのグローバルタイムアウト設定を使用して、再認証を強制される前にユーザーがAEM Formsと（SAML ベースのアサーションを使用して）やり取りできる時間を指定します。 デフォルト設定は 2 時間です。 実稼動環境では、時間を許容できる最小分数に減らす必要があります。

### 再認証時間制限の最小化 {#minimize-reauthentication-time-limit}

1. Web ブラウザーに次の URL を入力して、管理コンソールにログインします。

   ```java
            https://[host name]:'port'/adminui
   ```

1. クリック **設定/User Management /設定/設定ファイルの読み込みと書き出し**.
1. クリック **書き出し** 既存のAEM Forms設定を含む config.xml ファイルを生成する場合。
1. エディターで XML ファイルを開き、次のエントリを探します。

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. 値を 5（分単位）より大きい数に変更し、ファイルを保存します。
1. 管理コンソールで、設定ファイルの読み込みと書き出しページに移動します。
1. 変更した config.xml ファイルのパスを入力するか、「参照」をクリックしてこのファイルに移動します。
1. クリック **インポート** 変更した config.xml ファイルをアップロードし、「 **OK**.
