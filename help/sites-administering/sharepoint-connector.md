---
title: SharePoint コネクター
seo-title: SharePoint Connector
description: Microsoft SharePoint 2010 および Microsoft SharePoint 2013 用 Day JCR コネクター（バージョン 4.0）
seo-description: Learn about the Sharepoint Connector in AEM.
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 100%

---

# SharePoint コネクター{#sharepoint-connector}

この記事では、Microsoft SharePoint 2010 および Microsoft SharePoint 2013 バージョン 4.0用の Adobe JCR コネクタの詳細をまとめています。

SharePoint コネクターでは次の基本機能がサポートされています。

* SharePoint からのコンテンツおよびメタデータの読み取り
* ネイティブな SharePoint 認証および承認を適用することによる、アクセスされるコンテンツの SharePoint セキュリティ設定の確認
* コンテンツファインダーを使用したコンテンツ統合
* 外部リソースなどの AEM コンポーネントを使用した SharePoint 画像およびビデオの表示
* SharePoint と AEM Assets の同期

これらの機能はすべて、ネイティブな SharePoint Web サービスを SharePoint のコンテンツおよびサービスへのインターフェイスとして使用して実装されています。

>[!NOTE]
>
>SharePoint コネクターは AEM 6.1 サービスパック 2 でもサポートされています。ただし、仮想リポジトリのマウントのサポートは廃止され、マウントできなくなりました。Java API を使用して SharePoint リポジトリにアクセスする場合は、プロジェクトで SharePoint コネクタの JCR リポジトリ実装を使用してください。
>
>このドキュメントでは、SharePoint サーバーおよび関連する IT インフラストラクチャのインストール、設定、管理および IT 運営については取り上げていません。これらのトピックについて詳しくは、[SharePoint](https://www.microsoft.com/ja-jp/microsoft-365/sharepoint/collaboration) に関するベンダードキュメントを参照してください。コネクターを使用するには、これらのインフラストラクチャ要素を適切にインストール、設定および運用する必要があります。

## 概要 {#getting-started}

コネクターを導入する際には、次の作業をおこなってください。

* Java 7 以降がインストールされていることを確認します。
* ソフトウェア配布からコネクタパッケージ配布ファイルをダウンロードします。
* *cq-quickstart-6.4.0.jar* ファイルが格納されたディレクトリに有効な *license.properties* ファイルをコピーします。

* .jar ファイルをダブルクリックまたはタップして AEM を起動するか、コマンドラインから AEM を起動します。
* パッケージマネージャーからコネクターパッケージをインストールします。
* コネクターオプションを設定します。

## SharePoint コネクターのインストール {#installing-sharepoint-connector}

このコネクターは、インストールが容易なコンテンツパッケージとして提供されています。パッケージマネージャーを使用してパッケージをインストールし、SharePoint サーバーの URL 
およびその他の設定オプションを設定します。SharePoint コンテンツは AEM リポジトリに格納されています。

### インストール要件 {#installation-requirements}

このコネクターを使用するための要件は次のとおりです。

* Java Runtime Environment 1.7 以降
* ネットワークから SharePoint Web サービスを使用できること
* SharePoint サーバーの URL
* CRX および SharePoint リポジトリに対するユーザー資格情報と権限
* [サポートされているプラットフォーム](#supported-platforms)

SharePoint コネクタは[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673)からダウンロードできます。

### サポートされているプラットフォーム {#supported-platforms}

このコネクターでは次のプラットフォームがサポートされています。

* AEM バージョン：

   * AEM 6.4、6.3

* Microsoft SharePoint バージョン：

   * Microsoft Office SharePoint Server（MOSS）2010
   * Microsoft Office SharePoint Server（MOSS）2013

* コネクターのカスタムデプロイメント（OEM、特殊要件、認証方式のカスタマイズ）のサポートが必要な場合は、製品を使用している地域のアドビオフィスまでお問い合わせください。

>[!NOTE]
>
>コネクターでは、Microsoft で公式にサポートされている設定のみがサポートされています。[MOSS 2010](https://technet.microsoft.com/ja-jp/library/cc262485(office.14).aspx) および [MOSS 2013](https://docs.microsoft.com/ja-jp/SharePoint/install/hardware-and-software-requirements?redirectedfrom=MSDN) のシステム要件を参照してください。

### 標準インストール {#standard-installation}

ソフトウェア配布は、製品の機能、例およびホットフィックスを配布するために使用されます。詳しくは、[ソフトウェア配布のドキュメント](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)を参照してください。


#### AEM との統合 {#integrating-with-aem}

コネクターのコンテンツパッケージをインストールするには：

1. アドビサポートチケットを作成して、コネクターの機能パックを要求します。
1. パッケージが使用可能になったらそれをダウンロードし、対象の AEM インスタンスでパッケージマネージャーを開きます。
1. パッケージ説明ページで&#x200B;**インストール**&#x200B;をタップまたはクリックします。
1. **パッケージをインストール**&#x200B;ダイアログで、**インストール**&#x200B;をタップまたはクリックします。

   **メモ**：管理者としてログインしていることを確認してください

1. パッケージがインストールされたら、**閉じる**&#x200B;をタップまたはクリックします。

## SharePoint コネクターの設定 {#configuring-sharepoint-connector}

SharePoint コネクターのインストール後、そのコネクター用にアプリケーションおよび SharePoint レイヤーを設定します。

SharePoint リポジトリが JCR に準拠するように SharePoint サーバーの URL を設定します。追加のパラメーターを使用して、SharePoint サーバーとの接続を設定します。また、SharePoint コネクターでの認証を設定します。

### SharePoint サーバーとの接続の設定 {#configuring-the-connection-with-the-sharepoint-server}

SharePoint サーバーの URL および高度なオプションを設定するには、次の手順を実行します。

1. OSGi Management コンソール（[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)）に移動します。
1. **Day JCR Connector for Microsoft Sharepoint** バンドルを探します。
1. 設定値を編集.
1. 「**Workspaces**」の値として SharePoint サーバーの URL を設定します。
1. 「**保存**」をタップまたはクリックします。

![chlimage_1-62](assets/chlimage_1-62.png)

「Workspaces」および「Default Workspace Name」パラメーター：

コネクターによってデフォルトで公開される JCR ワークスペースは 1 つです。このワークスペースで公開される SharePoint サーバーは、「Sharepoint Server URL」設定パラメーターを使用して設定します。

 コネクターは複数のワークスペースに対して設定することもできます。この場合、各ワークスペースは、それによって公開されるそれぞれの SharePoint サーバーの URL に関連付けられます。ワークスペースを追加するには、「Workspaces」パラメーターにワークスペース定義を追加します。ワークスペース定義の形式は次の通りです。
`<name>`=`<url>`
ここで、`<name>` は JCR ワークスペースの名前で
`<url>` はそのワークスペース用の SharePoint サーバーの URL です。

AEM では、前述の設定手順とは別に、もう 1 つ手順を実行します。「**com.day.cq.dam.cq-dam-jcr-connectors**」バンドルを許可リストに追加します。

AEM でバンドルを許可リストに追加するには、次の手順を実行します。

1. OSGi Management コンソール（http://localhost:4502/system/console/configMgr）に移動します。
1. 「Apache Sling Login Admin Whitelist」サービスを探します。
1. **許可リストをスキップ**&#x200B;を選択します。
1. 許可リストバンドルのデフォルトに `com.day.cq.dam.cq-dam-jcr-connectors` を追加します。
1. 「保存」をクリックします。

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>複数のワークスペースを設定する場合は、「Default Workspace Name」パラメーターにデフォルトワークスペースの名前を指定します。

認証関連のパラメーターについて詳しくは、[認証](/help/sites-administering/sharepoint-connector.md#configuring-authentication)を参照してください。

### SharePoint 設定の検証 {#verifying-the-sharepoint-setup}

コネクターを設定した後、次の点を検証してください。

* SharePoint サーバーが実行されており、コネクターインスタンスから Web サービスにアクセスできること
* SharePoint ユーザー資格情報が有効であり、ユーザーが必要な SharePoint 権限を持っていること
* コネクターが適切にインストールおよび設定されていること

### SharePoint サーバーとの DAM 同期の設定 {#configuring-dam-sync-with-the-sharepoint-server}

SharePoint Assets を AEM と同期するには、次の手順を実行します。

1. OSGi Management Console（[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)）に移動します。
1. 「Default DAMAssetSynchronization」サービスを探します。
1. 設定値を編集.
1. SharePoint サイトへのアクセス権を持つユーザーのユーザー名とそれに対応するパスワードを設定します。
1. 「保存」をクリックします。

DAM 同期サービスを有効にします（デフォルトでは無効になっています）。

1. OSGi web コンソールのコンポーネント（[http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)）に移動します。
1. 「com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService」を探します。
1. 「Enable」をクリックします。

オプションで、異なる同期サイクル間の同期遅延を設定できます。

1. OSGi Management Console（[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)）に移動します。
1. 「DAY CQ DAM JCR Connector Asset Synchronization Service」を探します。
1. 設定値を編集.
1. 「Synchronization Period」（秒単位）の値を設定します。
1. 「保存」をクリックします。

### 認証の設定 {#configuring-authentication}

SharePoint ではクラシック認証方式と要求ベースの認証方式を使用でき、いずれの認証方式でも次の認証タイプがサポートされています。

* 基本
* フォームベース

特に、次の認証タイプを使用できます。

* クラシック-基本
* クラシック-フォームベース
* 要求-基本
* 要求-フォームベース

Microsoft SharePoint 2010 および Microsoft SharePoint 2013 のバージョン 4.0 用 AEM JCR Connector は、次のモードで動作する要求ベースの認証 (Microsoftが推奨 ) をサポートしています。

* **基本／NTLM 認証**：コネクターでの最初の接続試行では、基本認証が使用されます。基本認証が使用できない場合は、NTLM ベースの認証に切り替えられます。
* **フォームベースの認証**：SharePoint では、ユーザーがログインフォーム（通常は web ページ）に入力した資格情報に基づいてユーザーの検証が行われます。認証された要求にはシステムによってトークンが発行されます。このトークンには、後続要求で ID の再確立に使用されるキーが含まれています。

**フォームベースの認証の設定**

[http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles) に移動します。

1. OSGI／設定をクリックします。
1. 「Day JCR Connector for Microsoft Sharepoint」を探します。
1. 「Edit the configuration values」をクリックします。
1. 「Sharepoint Connection Factory」の値として「com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory」を設定します。
1. 「**保存**」をクリックします。

**基本認証の設定（Windows）**

1. [トークン認証を無効にします](#disable-token-authentication)。
1. [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles) に移動します。
1. OSGI／Configuration をクリックします。
1. **Day JCR Connector for Microsoft Sharepoint** を探します。
1. 「`Edit the configuration values`」をクリックします。
1. 「Sharepoint Connection Factory」の値として「`com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`」を設定します。
1. 「**保存**」をクリックします。

コネクターから SharePoint コンテンツにアクセスできるのは、AEM と SharePoint の両方で認証されたユーザーのみです。

認証用のコネクター拡張を使用してカスタム認証モジュールを作成することもできます。例えば、AEM ユーザーによるアクセスを特定の SharePoint ユーザーにマッピングできます。SharePoint ユーザーに対応する AEM ユーザーを作成して（ユーザー名とパスワードが一致する必要があります）、コネクターインスタンスにマッピングされた SharePoint コンテンツを確認できるようにします。

AEM でユーザーを作成するには、以下の手順に従います。

1. admin ユーザーとして http://localhost:9502/ にログインします。
1. 「ツール」をクリックします。
1. 「セキュリティ」をクリックします。
1. 「ユーザー」をクリックします。
1. 「**ユーザーを作成**」をクリックします。
1. ユーザー ID（SharePoint へのアクセス権限を持つユーザー名）を指定します。
1. 対応するパスワードを指定します。
1. 緑色のチェックマークをクリックして、ユーザーを作成します。

admin グループにユーザーを追加するには：

1. グループ管理に移動します。。
1. 『a』ノードをクリックします。
1. 『administrators』をクリックします。
1. 「**参照**」ボタンの前のテキストボックスに、先ほど作成したユーザー ID を入力します。
1. 緑色のチェックマークをクリックして、admin グループにユーザーを追加します。

### トークン認証の無効化 {#disable-token-authentication}

1. パッケージ `basic auth` をダウンロードし、インストールします。`zip` をソフトウェア配布からダウンロードおよびインストールします。

1. クイックスタートを閉じます。
1. ファイル *\crx-quickstart\repository\repository.xml* を開きます。
1. タグ `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.` を検索
1. ステップ 4 で示したタグ内に、タグ `<param name="disableTokenAuth" value="true"/>` を挿入します。
1. xml ファイルを保存して閉じます。
1. クイックスタートを再起動してから、自分の資格情報を使用してログインしてください。

#### SharePoint サーバーの別の認証方式のサポート {#supporting-different-authentication-methods-of-the-sharepoint-server}

標準バージョンのコネクターでは、標準の IIS **Windows** 認証（基本）とフォームベースの認証（トークンベース）がサポートされています。拡張メカニズムを使用して[その他の認証方式](https://technet.microsoft.com/ja-jp/library/cc262350.aspx#section2)をサポートすることもできます。

次の手順では、標準認証を拡張して SharePoint サーバーの各種認証方式をサポートするためのガイドラインを示します。

1. クライアント側の特定の認証プロセスを処理するための `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` を実装します。
1. フラグメントホスト `com.day.crx.spi.crx2sharepoint-bundle` を使用して、`SharepointConnectionFactory` 実装をフラグメントバンドルとしてインストールします。

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

1. `SharepointConnectionFactory` 実装をコネクター設定に登録します。コネクターの設定ウィンドウで、「**Advanced options**」をクリックします。**Sharepoint Connection Factory** フィールドで、`com.day.crx.spi.sharepoint.auth.CustomConnectionFactory` 実装の名前を指定します。

1. コネクターを再起動します。
