---
title: SharePoint コネクター
seo-title: SharePoint コネクター
description: Microsoft SharePoint 2010 および Microsoft SharePoint 2013 用 Day JCR コネクター（バージョン 4.0）
seo-description: AEM の SharePoint コネクターについて説明します。
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
translation-type: tm+mt
source-git-commit: 5d74f3510ff20e062f1e78f61d98e9c2e7a0414f
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 69%

---


# SharePoint コネクター{#sharepoint-connector}

この記事には、Adobe JCR Connector for Microsoft SharePoint 2010およびMicrosoft SharePoint 2013バージョン4.0に関する詳細が含まれています。

SharePoint コネクターでは次の基本機能がサポートされています。

* SharePoint からのコンテンツおよびメタデータの読み取り
* ネイティブな SharePoint 認証および承認を適用することによる、アクセスされるコンテンツの SharePoint セキュリティ設定の確認
* コンテンツファインダーを使用したコンテンツ統合
* 外部リソースなどの AEM コンポーネントを使用した SharePoint 画像およびビデオの表示
* SharePoint と AEM Assets の同期

これらの機能はすべて、ネイティブな SharePoint Web サービスを SharePoint のコンテンツおよびサービスへのインターフェイスとして使用して実装されています。

>[!NOTE]
>
>SharePoint コネクターは AEM 6.1 サービスパック 2 でもサポートされています。コネクタは、仮想リポジトリのマウントをサポートしなくなったため、マウントできません。 Java APIを使用してSharepointリポジトリにアクセスする場合は、プロジェクトでSharepoint ConnectorのJCRリポジトリ実装を使用します。
>
>このドキュメントでは、SharePoint サーバーおよび関連する IT インフラストラクチャのインストール、設定、管理および IT 運営については取り上げていません。See vendor documentation on [SharePoint](https://www.microsoft.com/sharepoint) for information about these topics. コネクターを使用するには、これらのインフラストラクチャ要素を適切にインストール、設定および運用する必要があります。


## はじめに {#getting-started}

コネクターを導入する際には、次の作業をおこなってください。

* Java 7 以降がインストールされていることを確認します。
* パッケージ共有からコネクターパッケージ配布ファイルをダウンロードします。
* *cq-quickstart-6.4.0.jar* ファイルが格納されたディレクトリに有効な *license.properties* ファイルをコピーします。

* .jar ファイルをダブルクリックまたはタップして AEM を起動するか、コマンドラインから AEM を起動します。
* パッケージマネージャーからコネクターパッケージをインストールします。
* コネクターオプションを設定します。

## SharePoint コネクターのインストール {#installing-sharepoint-connector}

このコネクターは、インストールが容易なコンテンツパッケージとして提供されています。パッケージマネージャーを使用してパッケージをインストールし、SharePointサーバーのURLおよびその他の構成オプションを設定します。 SharePoint コンテンツは AEM リポジトリに格納されています。

### インストール要件 {#installation-requirements}

このコネクターを使用するための要件は次のとおりです。

* Java Runtime Environment 1.7 以降
* ネットワークから SharePoint Web サービスを使用できること
* SharePoint サーバーの URL
* CRX および SharePoint リポジトリに対するユーザー資格情報と権限
* [サポートされているプラットフォーム](#supported-platforms)

The SharePoint connector is available for downloading from [packageshare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### サポートされているプラットフォーム {#supported-platforms}

このコネクターでは次のプラットフォームがサポートされています。

* AEM バージョン：

   * AEM 6.5、6.4、6.3

* Microsoft SharePoint バージョン：

   * Microsoft Office SharePoint Server（MOSS）2010
   * Microsoft Office SharePoint Server（MOSS）2013

* コネクターのカスタムデプロイメント（OEM、特殊要件、認証方式のカスタマイズ）のサポートが必要な場合は、製品を使用している地域のアドビオフィスまでお問い合わせください。

>[!NOTE]
>
>コネクターでは、Microsoft で公式にサポートされている設定のみがサポートされています。[MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) および [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) のシステム要件を参照してください。

### 標準インストール {#standard-installation}

AEM パッケージ共有は、製品の機能、例およびホットフィックスを配布するために使用されています。For details, see the [Package Share documentation](/help/sites-administering/package-manager.md#package-share).

To access Package Share on the AEM Welcome page, tap/click **Tools** and then select **Package Share**. 会社の電子メールアドレスを含む有効なAdobe IDが必要です。 また、アカウントへのログイン後に、パッケージ共有へのアクセスを申請してください。

#### AEM との統合 {#integrating-with-aem}

コネクターのコンテンツパッケージをインストールするには：

1. アドビサポートチケットを作成して、コネクターの機能パックを要求します。
1. パッケージが使用可能になったらそれをダウンロードし、対象の AEM インスタンスでパッケージマネージャーを開きます。
1. Tap/click **Install** from the package description page.
1. From the **Install Package** dialog, tap/click **Install**.

   **注意**: 管理者としてログインしていることを確認します。

1. When the package is installed, tap/click **Close**.

## SharePoint コネクターの設定 {#configuring-sharepoint-connector}

SharePoint コネクターのインストール後、そのコネクター用にアプリケーションおよび SharePoint レイヤーを設定します。

SharePoint リポジトリが JCR に準拠するように SharePoint サーバーの URL を設定します。追加のパラメーターを使用して、SharePoint サーバーとの接続を設定します。また、SharePoint コネクターでの認証を設定します。

### SharePoint サーバーとの接続の設定 {#configuring-the-connection-with-the-sharepoint-server}

SharePoint サーバーの URL および高度なオプションを設定するには、次の手順を実行します。

1. Navigate to the OSGi Management Console: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Search for the **Day JCR Connector for Microsoft Sharepoint** bundle.
1. 設定値を編集します。
1. 「**Workspaces**」の値として SharePoint サーバーの URL を設定します。
1. 「**Save**」をタップまたはクリックします。

![chlimage_1-62](assets/chlimage_1-62.png)

「Workspaces」および「Default Workspace Name」パラメーター：

コネクターによってデフォルトで公開される JCR ワークスペースは 1 つです。このワークスペースで公開される SharePoint サーバーは、「Sharepoint Server URL」設定パラメーターを使用して設定します。

 コネクターは複数のワークスペースに対して設定することもできます。この場合、各ワークスペースは、それによって公開されるそれぞれの SharePoint サーバーの URL に関連付けられます。ワークスペースを追加するには、「Workspaces」パラメーターにワークスペース定義を追加します。A workspace definition has the following format:
`<name>`= `<url>` where
`<name>` is the name of the JCR workspace and
`<url>` is the URL of the SharePoint server for that workspace.

AEM では、前述の設定手順とは別に、もう 1 つ手順を実行します。「**com.day.cq.dam.cq-dam-jcr-connectors**」バンドルの許可リスト。

AEMで許可リストバンドルを作成するには、次の手順を実行します。

1. OSGi管理コンソールに移動します。 http://localhost:4502/system/console/configMgr
1. 「Apache Sling Login Admin Whitelist」サービスを検索します。
1. Select **Bypass the whitelist**.
1. Add `com.day.cq.dam.cq-dam-jcr-connectors` in whitelist bundles default
1. 「保存」をクリックします。

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>複数のワークスペースを設定する場合は、「Default Workspace Name」パラメーターにデフォルトワークスペースの名前を指定します。

For additional information around authentication-related parameters, see [Authentication](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### SharePoint 設定の検証 {#verifying-the-sharepoint-setup}

コネクターを設定した後、次の点を検証してください。

* SharePoint サーバーが実行されており、コネクターインスタンスから Web サービスにアクセスできること
* SharePoint ユーザー資格情報が有効であり、ユーザーが必要な SharePoint 権限を持っていること
* コネクターが適切にインストールおよび設定されていること

### SharePoint サーバーとの DAM 同期の設定 {#configuring-dam-sync-with-the-sharepoint-server}

SharePoint Assets を AEM と同期するには、次の手順を実行します。

1. Navigate to the OSGi Management Console: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. 「Default DAMAssetSynchronization」サービスを探します。
1. 設定値を編集します。
1. SharePoint サイトへのアクセス権を持つユーザーのユーザー名とそれに対応するパスワードを設定します。
1. 「保存」をクリックします。

DAM 同期サービスを有効にします（デフォルトでは無効になっています）。

1. Navigate to the OSGi Web Console Components: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. 「com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService」を探します。
1. 「Enable」をクリックします。

オプションで、異なる同期サイクル間の同期遅延を設定できます。

1. Navigate to the OSGi Management Console: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. 「DAY CQ DAM JCR Connector Asset Synchronization Service」を探します。
1. 設定値を編集します。
1. 「Synchronization Period」（秒単位）の値を設定します。
1. 「Save」をクリックします。

### 認証の設定 {#configuring-authentication}

SharePoint ではクラシック認証方式と要求ベースの認証方式を使用でき、いずれの認証方式でも次の認証タイプがサポートされています。

* 基本
* フォームベース

特に、次の認証タイプを使用できます。

* クラシック-基本
* クラシック-フォームベース
* 要求-基本
* 要求-フォームベース

AEM JCR Connector for Microsoft SharePoint 2010およびMicrosoft SharePoint 2013バージョン4.0.は、次のモードで動作する要求ベースの認証（Microsoftによって推奨される）をサポートしています。

* **基本／NTLM 認証**：コネクターでの最初の接続試行では、基本認証が使用されます。基本認証が使用できない場合は、NTLM ベースの認証に切り替えられます。
* **フォームベースの認証**: Sharepointは、ログインフォーム（通常はWebページ）にユーザーが入力した資格情報に基づいてユーザーを検証します。 認証された要求にはシステムによってトークンが発行されます。このトークンには、後続要求で ID の再確立に使用されるキーが含まれています。

**フォームベースの認証の設定**

Go to: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. OSGI／設定をクリックします。
1. 「Day JCR Connector for Microsoft Sharepoint」を探します。
1. 「Edit the configuration values」をクリックします。
1. 「Sharepoint Connection Factory」の値として「com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory」を設定します。
1. 「**保存**」をクリックします。

**基本認証の設定(Windows)**

1. [トークン認証を無効にします](#disable-token-authentication)。
1. Go to [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. OSGI／Configuration をクリックします。
1. **Day JCR Connector for Microsoft Sharepoint** を探します。
1. 「`Edit the configuration values`」をクリックします。
1. 「Sharepoint Connection Factory」の値として「`com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`」を設定します。
1. 「**保存**」をクリックします。

コネクターから SharePoint コンテンツにアクセスできるのは、AEM と SharePoint の両方で認証されたユーザーのみです。

認証用のコネクター拡張を使用してカスタム認証モジュールを作成することもできます。例えば、AEM ユーザーによるアクセスを特定の SharePoint ユーザーにマッピングできます。SharePoint ユーザーに対応する AEM ユーザーを作成して（ユーザー名とパスワードが一致する必要があります）、コネクターインスタンスにマッピングされた SharePoint コンテンツを確認できるようにします。

AEMでユーザーを作成するには：

1. admin ユーザーとして http://localhost:9502/ にログインします。
1. 「ツール」をクリックします。
1. 「セキュリティ」をクリックします。
1. 「ユーザー」をクリックします。
1. 「**ユーザーを作成**」をクリックします。
1. ユーザーID （SharePointでアクセスできるユーザー名）を指定します。
1. 対応するパスワードを指定します。
1. 緑の目盛り記号をクリックして、ユーザを作成します。

admin グループにユーザーを追加するには：

1. グループ管理に移動します。。
1. 「a」ノードをクリックします。
1. 「管理者」をクリックします。
1. Type the user ID create above in the text box before **Browse** button.
1. 緑の目盛り記号をクリックして、ユーザを管理者グループに追加します。

### トークン認証の無効化 {#disable-token-authentication}

1. Download and install the package `basic auth`. `zip` をパッケージ共有から取得します。

1. クイックスタートを閉じます。
1. ファイル *\crx-quickstart\repository\repository.xml* を開きます。
1. タグの検索 `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Insert the tag `<param name="disableTokenAuth" value="true"/>` inside the tag mentioned in step 4.
1. xml ファイルを保存して閉じます。
1. QuickStartを再起動し、資格情報を使用してログインします。

#### SharePoint サーバーの別の認証方式のサポート {#supporting-different-authentication-methods-of-the-sharepoint-server}

標準バージョンのコネクターでは、標準の IIS **Windows** 認証（基本）とフォームベースの認証（トークンベース）がサポートされています。拡張メカニズムを使用して[その他の認証方式](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2)をサポートすることもできます。

次の手順では、標準認証を拡張して SharePoint サーバーの各種認証方式をサポートするためのガイドラインを示します。

1. クライアント側の特定の認証プロセスを処理するための `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` を実装します。
1. Install the `SharepointConnectionFactory` implementation as a fragment bundle with fragment host `com.day.crx.spi.crx2sharepoint-bundle`.

   Maven を使用する際には、次の `maven-bundle-plugin` 設定をプロジェクトの要件に合わせて調整します。

   ```xml
              <plugin>
                  <groupId>org.apache.felix</groupId>
                  <artifactId>maven-bundle-plugin</artifactId>
                  <extensions>true</extensions>
                  <configuration>
                      <instructions>
                          <Export-Package />
                          <Private-Package>
                              <!-- your private package here -->
                          </Private-Package>
                          <Fragment-Host>
                              com.day.crx.spi.crx2sharepoint-bundle
                          </Fragment-Host>
                       </instructions>
                  </configuration>
              </plugin>
   ```

1. `SharepointConnectionFactory` 実装をコネクター設定に登録します。コネクターの設定ウィンドウで、「**Advanced options**」をクリックします。In the for **Sharepoint Connection Factory** field, specify the name of the implementation `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. コネクターを再起動します。

