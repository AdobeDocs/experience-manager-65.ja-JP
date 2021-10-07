---
title: Dynamic Media — ハイブリッドモードの設定
description: Dynamic Media - ハイブリッドモードの設定方法を学習します。
mini-toc-levels: 3
uuid: 39ad7d83-d310-4baf-9d85-5532c2f201f3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 7d8e7273-29f3-4a45-ae94-aad660d2c71d
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: User, Admin
exl-id: 5719d32c-4f19-47c1-bea9-8fd0bc8439ed
feature: Configuration,Hybrid Mode
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '7792'
ht-degree: 33%

---

# Dynamic Media — ハイブリッドモードの設定 {#configuring-dynamic-media-hybrid-mode}

Dynamic Media — ハイブリッドを使用するには、有効にし、設定する必要があります。 Dynamic Media では、使用例に応じて、[サポートされる設定](#supported-dynamic-media-configurations)がいくつか用意されています。

>[!NOTE]
>
>Scene7実行モードでDynamic Mediaを設定して実行する場合は、「[Dynamic Media - Scene7モードの設定 ](/help/assets/config-dms7.md)」を参照してください。
>
>ハイブリッド実行モードの Dynamic Media を設定して実行する場合は、このページの手順に従ってください。

Dynamic Media での[ビデオ](/help/assets/video.md)の操作方法を参照してください。

>[!NOTE]
>
>開発、ステージング、実稼動用など、様々な環境用にAdobe Experience Managerを設定して使用する場合は、各環境用にDynamic MediaCloud Servicesを設定します。

>[!NOTE]
>
>Dynamic Mediaの設定に問題がある場合は、Dynamic Mediaに固有のログファイルを確認します。 Dynamic Mediaを有効にすると、これらのファイルは自動的にインストールされます。
>
>* `s7access.log`
>* `ImageServing.log`

>
>これらは [Experience Managerインスタンスの監視と保守 ](/help/sites-deploying/monitoring-and-maintaining.md) に記載されています。

ハイブリッド公開および配信は、Adobe Experience Manager に対して Dynamic Media によって追加される中心機能です。ハイブリッド公開を使用すると、画像、セット、ビデオなどのDynamic Mediaアセットを、Experience Managerの公開ノードからではなく、クラウドから配信できます。

Dynamic Mediaビューア、サイトページ、静的コンテンツなどのその他のコンテンツは、引き続きExperience Managerのパブリッシュノードから提供されます。

Dynamic Mediaをご利用の場合は、すべてのDynamic Mediaコンテンツの配信メカニズムとしてハイブリッド配信を使用する必要があります。

## ビデオのハイブリッド公開アーキテクチャ {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## 画像のハイブリッド公開アーキテクチャ {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## サポートされる Dynamic Media 設定 {#supported-dynamic-media-configurations}

各設定タスクで参照される用語を次に示します。

| **用語** | **ダイナミックメディア有効** | **説明** |
|---|---|---|
| Experience Manager作成者ノード | 緑色の円の中に白色のチェックマーク | オンプレミスまたはManaged Servicesを通じてデプロイするオーサーノード。 |
| Experience Manager発行ノード | 赤色の四角の中に白色の「X」 | オンプレミスまたはManaged Servicesを通じてデプロイするパブリッシュノード。 |
| 画像サービスの公開ノード | 緑色の円の中に白色のチェックマーク | データセンター上で実行するパブリッシュノードで、Adobeが管理する。画像サービスの URL を参照します。 |

Dynamic Mediaは、画像のみ、ビデオのみ、または画像とビデオの両方に実装できます。 特定のシナリオに合わせてDynamic Mediaを設定する手順を判断するには、次の表を参照してください。

<table>
 <tbody>
  <tr>
   <td><strong>シナリオ</strong></td>
   <td ><strong>仕組み</strong></td>
   <td><strong>設定手順</strong></td>
  </tr>
  <tr>
   <td>実稼動環境に画像のみを配信する</td>
   <td>画像は世界各地のアドビのデータセンターのサーバーを介して配信されます。CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。</td>
   <td>
    <ol>
     <li>Experience Manager<strong>author</strong> ノードで、<a href="#enabling-dynamic-media">Dynamic Media</a> を有効にします。</li>
     <li>画像を<a href="#configuring-dynamic-media-cloud-services"> Dynamic Media クラウドサービス</a>で設定します。</li>
     <li><a href="#configuring-image-replication">画像のレプリケーションを設定</a>します。</li>
     <li><a href="#replicating-catalog-settings">カタログ設定をレプリケート</a>します。</li>
     <li><a href="#replicating-viewer-presets">ビューアプリセットをレプリケート</a>します。</li>
     <li><a href="#using-default-asset-filters-for-replication">レプリケーションにデフォルトのアセットフィルターを使用</a>します。</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media Image Server を設定</a>します。</li>
     <li><a href="#delivering-assets">アセットを配信</a>します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>実稼動前の環境（開発、品質評価、ステージングなど）に画像のみを配信する</td>
   <td>画像は、公開ノードを使用してExperience Managerに配信されます。 このシナリオでは、トラフィックは最小限なので、Adobeのデータセンターに画像を配信する必要はありません。 また、実稼動環境を起動する前に、コンテンツの安全なプレビューを可能にします。</td>
   <td>
    <ol>
     <li>Experience Manager<strong>author</strong> ノードで、<a href="#enabling-dynamic-media">Dynamic Media</a> を有効にします。</li>
     <li>Experience Manager<strong>publish</strong> ノードで、<a href="#enabling-dynamic-media">Dynamic Media</a> を有効にします。</li>
     <li><a href="#replicating-viewer-presets">ビューアプリセットをレプリケート</a>します。</li>
     <li><a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">実稼動環境以外の画像用のアセットフィルター</a>をセットアップします。</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media Image Server を設定します。</a></li>
     <li><a href="#delivering-assets">アセットを配信します。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>任意の環境（実稼動、開発、品質評価、ステージングなど）にビデオのみを配信する</td>
   <td>画像は CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。ビデオポスター画像（再生が開始される前に表示されるビデオのサムネール）は、Experience Managerのパブリッシュインスタンスによって配信されます。</td>
   <td>
    <ol>
     <li>Experience Manager<strong>author</strong> ノードで、<a href="#enabling-dynamic-media">Dynamic Media</a> を有効にします。</li>
     <li>Experience Manager<strong>publish</strong> ノードで、<a href="#enabling-dynamic-media">enable Dynamic Media</a> を有効にします（発行インスタンスはビデオポスター画像を提供し、ビデオ再生用のメタデータを提供します）。</li>
     <li><a href="#configuring-dynamic-media-cloud-services">Dynamic Media クラウドサービス</a>でビデオを設定します。</li>
     <li><a href="#replicating-viewer-presets">ビューアプリセットをレプリケート</a>します。</li>
     <li><a href="#setting-up-asset-filters-for-video-only-deployments">ビデオ専用のアセットフィルター</a>をセットアップします。</li>
     <li><a href="#delivering-assets">アセットを配信します。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>実稼動環境に画像とビデオの両方を配信する</td>
   <td><p>画像は CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。画像やビデオのポスター画像は世界各地のアドビのデータセンターのサーバーを介して配信されます。CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。</p> <p>実稼動前に画像またはビデオを設定するには、前の節を参照してください。 </p> </td>
   <td>
    <ol>
     <li>Experience Manager<strong>author</strong> ノードで、<a href="#enabling-dynamic-media">Dynamic Media</a> を有効にします。</li>
     <li><a href="#configuring-dynamic-media-cloud-services">Dynamic Media クラウドサービス</a>でビデオを設定します。</li>
     <li>画像を<a href="#configuring-dynamic-media-cloud-services"> Dynamic Media クラウドサービス</a>で設定します。</li>
     <li><a href="#configuring-image-replication">画像のレプリケーションを設定</a>します。</li>
     <li><a href="#replicating-catalog-settings">カタログ設定をレプリケート</a>します。</li>
     <li><a href="#replicating-viewer-presets">ビューアプリセットをレプリケート</a>します。</li>
     <li><a href="#using-default-asset-filters-for-replication">レプリケーションにデフォルトのアセットフィルターを使用します。</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media Image Server を設定します。</a></li>
     <li><a href="#delivering-assets">アセットを配信します。</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Dynamic Mediaを有効にする {#enabling-dynamic-media}

[Dynamic Media はデフォルトで無効になっています。](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)Dynamic Mediaの機能を活用するには、`dynamicmedia` 実行モードなど、実行モードと同様に `publish` を使用してDynamic Mediaを有効にする必要があります。 有効にする前に、[ 技術要件 ](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on) を確認してください。

>[!NOTE]
>
>実行モードでDynamic Mediaを有効にすると、`dynamicMediaEnabled` フラグを **[!UICONTROL true]** に設定してDynamic Mediaを有効にしたExperience Manager6.1 とExperience Manager6.0 の機能が置き換えられます。 このフラグは、Experience Manager6.2 以降では機能しません。 また、Dynamic Mediaを有効にするためにクイックスタートを再起動する必要はありません。

Dynamic Mediaを有効にすると、Dynamic Media機能が UI で使用でき、アップロードされたすべての画像アセットに、動的な画像レンディションの高速配信に使用される *cqdam.pyramid.tiff* レンディションが届きます。 これらの PTIFF には、次のような大きな利点があります。

* 1 つのプライマリソース画像のみを管理し、追加のストレージを必要とせずに無限のレンディションをオンザフライで生成する機能。
* ズーム、パン、スピンなどのインタラクティブなビジュアライゼーションを使用する機能。

Experience ManagerでDynamic Media Classicを使用する場合は、[ 特定のシナリオ ](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media) を使用しない限り、Dynamic Mediaを有効にしないでください。 Dynamic Mediaは、実行モードでDynamic Mediaを有効にしない限り、無効になります。

Dynamic Mediaを有効にするには、コマンドラインまたはクイックスタートファイル名からDynamic Media実行モードを有効にする必要があります。

**ダイナミックメディアを有効にするには：**

1. コマンドラインでクイックスタートを起動するときに、次のようにします。

   * jar ファイルを起動する際に、コマンドラインの最後に `-r dynamicmedia` を追加します。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   s7delivery に公開する場合は、次の trustStore 引数も含める必要があります。

   ```
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. `https://localhost:4502/is/image` を要求し、Image Server が実行中であることを確認します。

   >[!NOTE]
   >
   >Dynamic Mediaの問題のトラブルシューティングについては、`crx-quickstart/logs/` ディレクトリの次のログを参照してください。
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log - ImageServer ログは、内部の ImageServer プロセスの動作を分析するための統計情報と分析情報を提供します。

   Image Server ログファイル名の例：`ImageServer-57346-2020-07-25.log`
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - s7access ログは、`/is/image` と `/is/content` を通じてDynamic Mediaに対しておこなわれた各要求を記録します。

   これらのログは、Dynamic Media が有効の場合のみ使用されます。`system/console/status-Bundlelist` ページから生成される **完全ダウンロード** パッケージには含まれません。Dynamic Mediaの問題がある場合は、カスタマーサポートに問い合わせる際に、これらのログを両方とも問題に追加します。

### Experience Managerを別のポートまたはコンテキストパスにインストールした場合 {#if-you-installed-aem-to-a-different-port-or-context-path}

[Experience Managerをアプリケーションサーバー ](/help/sites-deploying/application-server-install.md) にデプロイし、Dynamic Mediaを有効にしている場合は、Externalizer で **self-domain** を設定する必要があります。 そうしないと、アセットのサムネールの生成がDynamic Media Assets で正しく機能しません。

また、別のポートやコンテキストパスで quickstart を実行する場合は、**self-domain** も変更する必要があります。

ダイナミックメディアが有効の場合、画像アセットの静的サムネールレンディションがダイナミックメディアを使用して生成されます。サムネールの生成がDynamic Mediaで正しく機能するには、Experience Managerが自身に対して URL リクエストを実行し、ポート番号とコンテキストパスの両方を把握している必要があります。

Experience Manager:

* [Externalizer](/help/sites-developing/externalizer.md) の **self-domain** は、ポート番号とコンテキストパスの両方を取得するために使用されます。
* **self-domain** が設定されていない場合、ポート番号とコンテキストパスは Jetty HTTP サービスから取得されます。

Experience Managerの QuickStart WAR デプロイメントでは、ポート番号とコンテキストパスを導き出すことができないので、**self-domain** を設定する必要があります。 **自己ドメイン** の設定方法については、[Externalizer のドキュメント ](/help/sites-developing/externalizer.md) を参照してください。

>[!NOTE]
[Experience Managerクイックスタートのスタンドアロンデプロイメント ](/help/sites-deploying/deploy.md) では、**self-domain** は通常、設定する必要はありません。これは、ポート番号とコンテキストパスを自動設定できるからです。 ただし、すべてのネットワークインターフェイスがオフになっている場合は、**self-domain** を設定する必要があります。

## Dynamic Mediaを無効にする  {#disabling-dynamic-media}

Dynamic Mediaはデフォルトでは有効になっていません。 ただし、以前にDynamic Mediaを有効にしている場合は、後でオフにすることができます。

Dynamic Mediaを有効にした後で無効にするには、`-r dynamicmedia` 実行モードフラグを削除します。

**ダイナミックメディアを無効にするには：**

1. コマンドラインでクイックスタートを起動するときに、次のいずれかを実行します。

   * jar ファイルを起動する際に、コマンドラインに `-r dynamicmedia` を追加しないでください。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. リクエスト `https://localhost:4502/is/image`. Dynamic Media が無効化されたことを示すメッセージが表示されます。

   >[!NOTE]
   Dynamic Mediaの実行モードが無効になると、`cqdam.pyramid.tiff` レンディションを生成するワークフロー手順は自動的にスキップされます。 また、動的レンディションのサポートやその他のDynamic Mediaの機能も無効になります。
   また、Experience Managerサーバーを設定した後、Dynamic Mediaの実行モードが無効になった場合、その実行モードでアップロードされたすべてのアセットが無効になります。

## （オプション）Dynamic Mediaのプリセットと設定を 6.3 から 6.5 にダウンタイムなしで移行 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Experience Manager(Dynamic Media) を 6.3 から 6.5 にアップグレードする場合（ダウンタイムなしのデプロイメント機能が含まれるようになりました）、次の curl コマンドを実行する必要があります。 このコマンドは、すべてのプリセットと設定をCRXDE Liteの `/etc` から `/conf` に移行します。

>[!NOTE]
互換モードでExperience Managerインスタンスを実行する場合（つまり、互換パッケージがインストールされている場合）は、これらのコマンドを実行する必要はありません。

互換性パッケージの有無にかかわらず、すべてのアップグレードについて、次の Linux® curl コマンドを実行して、Dynamic Mediaに付属していたデフォルトの標準提供ビューアプリセットをコピーできます。

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

`/etc` から `/conf` に作成したカスタムビューアプリセットと設定を移行するには、次の Linux® curl コマンドを実行します。

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## イメージレプリケーションの設定 {#configuring-image-replication}

Dynamic Mediaの画像配信は、ビデオサムネールを含む画像アセットをExperience Managerオーサーから公開し、Adobeのオンデマンドレプリケーションサービス（レプリケーションサービスの URL）にレプリケートすることで機能します。 アセットは、オンデマンドの画像配信サービス（画像サービスの URL）を通じて配信されます。

以下の操作を実行します。

1. [認証の設定](#setting-up-authentication)を参照してください。
1. [レプリケーションエージェントを設定します](#configuring-the-replication-agent)。

レプリケーションエージェントは、画像、ビデオメタデータ、セットなどのDynamic MediaアセットをAdobeがホストする画像サービスに公開します。 レプリケーションエージェントはデフォルトでは有効でありません。

レプリケーションエージェントを設定したら、[ 検証し、正常に設定されたことをテストする必要があります。](#validating-the-replication-agent-for-dynamic-media) ここでは、これらの手順について説明します。

>[!NOTE]
PTIFF 作成のデフォルトのメモリ制限は、すべてのワークフローで 3 GB です。例えば、他のワークフローを一時停止して、3 GB のメモリを必要とする 1 個の画像を処理できます。または、それぞれ 300 MB のメモリを必要とする 10 個の画像を並行して処理できます。
メモリ制限は設定可能で、システムリソースの可用性と処理される画像コンテンツのタイプに合わせて調整されます。 大きなアセットが多く、システムに十分なメモリがある場合は、この制限を増やして、画像が並行して処理されるようにすることができます。
最大メモリ制限を超える画像が拒否されます。
PTIFF 作成のメモリ制限を変更するには、**[!UICONTROL ツール]**／**[!UICONTROL 運営]**／**[!UICONTROL Web コンソール]**／**[!UICONTROL Adobe CQ Scene7 PTiffManager]** に移動して、**[!UICONTROL maxMemory]** の値を変更します。

### 認証の設定 {#setting-up-authentication}

オーサー環境でレプリケーション認証を設定し、画像をDynamic Mediaの画像配信サービスにレプリケートできるようにします。 最初にキーストアを取得し、**[!UICONTROL dynamic-media-replication]** ユーザーの下に保存して、設定します。 会社の管理者に、KeyStore ファイルとプロビジョニングプロセス中に必要な資格情報が記載された「ようこそ」の電子メールが届きました。 この情報を受け取っていない場合は、Adobeカスタマーサポートにお問い合わせください。

**認証を設定するには：**

1. Adobeのカスタマーサポートに問い合わせて、キーストアのファイルとパスワードをまだお持ちでない場合はお問い合わせください。 この情報は、プロビジョニングに必要な部分です。 キーがアカウントに関連付けられます。

1. Experience Managerで、Experience Managerのロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]** / **[!UICONTROL セキュリティ]** / **[!UICONTROL ユーザー]** に移動します。

1. ユーザー管理ページで、**[!UICONTROL dynamic-media-replication]** ユーザーに移動し、「 」を選択して開きます。

   ![dm-replication](assets/dm-replication.png)

1. Edit User Settings For dynamic-media-replication ページで、「**[!UICONTROL キーストア]**」タブを選択し、「**[!UICONTROL キーストアを作成]**」を選択します。

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. **[!UICONTROL キーストアアクセスパスワードを設定]**&#x200B;ダイアログボックスでパスワードを入力し、パスワードを確認します。

   >[!NOTE]
   パスワードは覚えておいてください。後でレプリケーションエージェントを設定する際に、パスワードを再入力する必要があります。

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. **[!UICONTROL dynamic-media-replication のユーザー設定を編集]**&#x200B;ページで「**秘密鍵をキーストアファイルから追加**」領域を展開し、以下の情報を追加します（下の画像を参照）。

   * [**[!UICONTROL 新しいエイリアス]**] フィールドに、レプリケーション設定の後で使用するエイリアスの名前を入力します。 例えば、`replication` をエイリアスとして使用できます。
   * **[!UICONTROL キーストアファイル]** を選択します。 Adobeから提供されたキーストアファイルに移動し、ファイルを選択して、「**[!UICONTROL 開く]**」を選択します。
   * 「**[!UICONTROL キーストアファイルのパスワード]**」フィールドに、キーストアファイルのパスワードを入力します。 このAdobeは、手順 5 で作成したキーストアパスワードではなく ****、プロビジョニング中に送信されるようこそメールに記載されたキーストアファイルパスワードパスワードです。 キーストアファイルのパスワードを受け取っていない場合は、Adobeカスタマーサポートにお問い合わせください。
   * 「**[!UICONTROL 秘密鍵のパスワード]**」フィールドに、秘密鍵のパスワードを入力します（前の手順で指定したのと同じ秘密鍵のパスワードを入力できます）。 秘密鍵のパスワードは、プロビジョニング中にアドビから送信されたようこそメールに記載されています。秘密鍵のパスワードを受け取っていない場合は、Adobeカスタマーサポートにお問い合わせください。
   * 「**[!UICONTROL 秘密鍵のエイリアス]**」フィールドに、秘密鍵のエイリアスを入力します。例： `*companyname*-alias`。 秘密鍵のエイリアスは、プロビジョニング中にアドビから送信されたようこそメールに記載されています。秘密鍵のエイリアスを受け取っていない場合は、Adobeカスタマーサポートにお問い合わせください。

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. 「**[!UICONTROL 保存して閉じる]**」を選択して、このユーザーに対する変更を保存します。

   次に、[ レプリケーションエージェント ](#configuring-the-replication-agent) を設定する必要があります。

### レプリケーションエージェントの設定 {#configuring-the-replication-agent}

1. Experience Managerで、Experience Managerのロゴを選択してグローバルナビゲーションコンソールにアクセスし、 **[!UICONTROL ツール]** / **[!UICONTROL デプロイ]** / **[!UICONTROL レプリケーション]** / **[!UICONTROL 作成者のエージェント]** に移動します。
1. 作成者のエージェントページで、「 **[!UICONTROL Dynamic Mediaハイブリッド画像レプリケーション (s7delivery)]** 」を選択します。
1. 「**[!UICONTROL 編集]**」を選択します。
1. 「**[!UICONTROL 設定]**」タブを選択し、次のように入力します。

   * **[!UICONTROL 有効]** - レプリケーションエージェントを有効にするには、このチェックボックスを選択します。
   * **[!UICONTROL 地域]**  — 適切な地域に設定します。北米、ヨーロッパ、アジア
   * **[!UICONTROL テナント ID]**  — この値は、レプリケーションサービスに公開している会社またはテナントの名前です。この値は、プロビジョニング中にAdobeから送信されたようこそ電子メールに含まれるテナント ID です。 この情報を受け取っていない場合は、Adobeカスタマーサポートにお問い合わせください。
   * **[!UICONTROL Key Store Alias]**  — この値は、認証の設定でキーを生成する際に **設** 定された新しいエイリアス [値と同じです](#setting-up-authentication)。例：  `replication`。（[ 認証の設定 ](#setting-up-authentication) の手順 7 を参照）。
   * **[!UICONTROL キーストアのパスワード]**  - 「キーストアを作成」をタップして作成したキースト **[!UICONTROL アのパスワード]**。このパスワードはアドビが提供するものではありません。[ 認証の設定 ](#setting-up-authentication) の手順 5 を参照してください。

   次の画像はサンプルデータが入力されたレプリケーションエージェントを示します。

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. 「**[!UICONTROL OK]**」を選択します。

### Dynamic Mediaのレプリケーションエージェントの検証 {#validating-the-replication-agent-for-dynamic-media}

Dynamic Mediaのレプリケーションエージェントを検証するには、次の手順を実行します。

「**[!UICONTROL 接続をテスト]**」を選択します。 次のように出力されます。

```shell
11.03.2016 10:57:55 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
11.03.2016 10:57:55 - * Auth User: replication-receiver
11.03.2016 10:57:55 - * HTTP Version: 1.1
11.03.2016 10:57:55 - * Using OAuth 2.0 Authorization Grants
11.03.2016 10:57:55 - * OAuth 2.0 User: dynamic-media-replication
11.03.2016 10:57:55 - * OAuth 2.0 Token: '*****' initialized
11.03.2016 10:57:55 - Publishing: POST[https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=xfpuu-6613]
11.03.2016 10:57:55 - Publish response: OK[]
11.03.2016 10:57:55 - Transfer succeeded in 141 ms for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
-------------------------------------------------------------------------------------------------------------------------------
Replication test succeeded
```

>[!NOTE]
次のいずれかを実行してチェックすることもできます。
* レプリケーションログを調べて、アセットがレプリケートされていることを確認します。
* 画像を公開する。画像を選択し、ドロップダウンメニューで「**[!UICONTROL ビューア]**」を選択して、ビューアプリセットを選択します。 **[!UICONTROL URL]** を選択します。 画像が表示されていることを確認するには、URL パスをコピーしてブラウザーに貼り付けます。


### 認証のトラブルシューティング {#troubleshooting-authentication}

認証を設定する際に、ソリューションで発生する可能性のある問題を以下に示します。 これらの問題を確認する前に、レプリケーションが設定されていることを確認してください。

#### 問題：HTTP ステータスコード 401 メッセージ - 認証が必要 {#problem-http-status-code-with-message-authorization-required}

この問題は、`dynamic-media-replication` ユーザーのキーストアの設定に失敗したことによって発生する可能性があります。

```shell
Replication test to s7delivery:https://s7bern.macromedia.com:8580/is-publish/
17.06.2016 18:54:43 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}
17.06.2016 18:54:43 - * Auth User: replication-receiver
17.06.2016 18:54:43 - * HTTP Version: 1.1
17.06.2016 18:54:43 - * Using OAuth 2.0 Authorization Grants
17.06.2016 18:54:43 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 18:54:43 - No OAuth token available. OAuth not initialized
17.06.2016 18:54:43 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 18:54:43 - Publishing: POST[https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough]
17.06.2016 18:54:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
17.06.2016 18:54:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309,
 userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
```

**解決方法：**
が `KeyStore` dynamic-media-replicationuser に保存さ **れ、正しいパスワードが指定されていることを確認しま** す。

#### 問題：鍵を復号化できない - データを復号化できない {#problem-could-not-decrypt-key-could-not-decrypt-data}

```xml
Replication test to s7delivery:https://<localhost>:8580/is-publish/
17.06.2016 19:00:16 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}
17.06.2016 19:00:16 - * Auth User: replication-receiver
17.06.2016 19:00:16 - * HTTP Version: 1.1
17.06.2016 19:00:16 - * Using OAuth 2.0 Authorization Grants
17.06.2016 19:00:16 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 19:00:16 - No OAuth token available. OAuth not initialized
17.06.2016 19:00:16 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 19:00:16 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}. java.lang.SecurityException: java.security.UnrecoverableKeyException: Could not decrypt key: Could not decrypt data.
```

**解決方法：**
パスワードを確認してください。レプリケーションエージェントに保存されたパスワードがキーストアの作成に使用されたパスワードと同じでありません。

#### 問題：InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

この問題は、Experience Managerオーサーインスタンスの設定エラーが原因で発生します。 オーサー上の Java™プロセスが正しい `javax.net.ssl.trustStore` を取得していません。 このエラーは次のレプリケーションログで確認できます。

```shell
14.04.2016 09:37:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
14.04.2016 09:37:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
```

または、次のエラーログで確認できます。

```shell
07.25.2019 12:00:59.893 *ERROR* [sling-threadpool-db2763bb-bc50-4bb5-bb64-10a09f432712-(apache-sling-job-thread-pool)-90-com_day_cq_replication_job_s7delivery(com/day/cq/replication/job/s7delivery)] com.day.cq.replication.Agent.s7delivery.queue Error during processing of replication.

java.io.IOException: Failed to execute request 'https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
        at com.scene7.is.catalog.service.publish.atomic.PublishingServiceHttp.executePost(PublishingServiceHttp.scala:195)
```

**解決方法：**
Experience Manager作成者の Java™プロセスで、システムプロパティが有効なトラストストアに設定さ `-Djavax.net.ssl.trustStore=` れていることを確認してください。

#### 問題：キーストアが設定されていないか初期化されていない {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

この問題は、ホットフィックスや、機能パックが dynamic-media-user ノードまたはキーストアノードを上書きしたことが原因で発生する可能性があります。

レプリケーションログの例は次のとおりです。

```shell
Replication test to s7delivery:https://replicate-na.assetsadobe.com/is-publish
02.08.2016 14:37:44 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}
02.08.2016 14:37:44 - * Auth User: replication-receiver
02.08.2016 14:37:44 - * HTTP Version: 1.1
02.08.2016 14:37:44 - * Using OAuth 2.0 Authorization Grants
02.08.2016 14:37:44 - * OAuth 2.0 User: dynamic-media-replication
02.08.2016 14:37:44 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}. com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised key store for user dynamic-media-replication
```

**解決策:**

1. ユーザー管理ページに移動します。
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. ユーザー管理ページで、`dynamic-media-replication` ユーザーに移動し、「 」を選択して開きます。
1. 「**[!UICONTROL キーストア]**」タブを選択します。 「**[!UICONTROL キーストアを作成]**」ボタンが表示された場合は、前の「[ 認証の設定 ](#setting-up-authentication)」の手順をやり直す必要があります。
1. KeyStore の設定をやり直す必要がある場合は、[ レプリケーションエージェントの設定 ](/help/assets/config-dynamic.md#configuring-the-replication-agent) もう一度行う必要があります。

   s7delivery レプリケーションエージェントを再設定します。
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. 「**[!UICONTROL 接続をテスト]**」を選択して、設定が有効であることを確認できます。

#### 問題：公開エージェントが OAuth ではなく SSL を使用している {#problem-publish-agent-is-using-ssl-instead-of-oauth}

この問題は、ホットフィックスまたは機能パックが正しくインストールされなかったか、設定を上書きしたことが原因で発生する可能性があります。

レプリケーションログの例は次のとおりです。

```shell
01.08.2016 18:42:59 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}
01.08.2016 18:42:59 - * Auth User: replication-receiver
01.08.2016 18:42:59 - * HTTP Version: 1.1
01.08.2016 18:42:59 - * Using Client Auth SSL alias - replication-receiver *
01.08.2016 18:42:59 - Publishing: POST[https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=altayerstaging]
01.08.2016 18:42:59 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
01.08.2016 18:42:59 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
```

**解決策:**

1. Experience Managerで、**[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]** に移動します。

   `localhost:4502/crx/de/index.jsp`

1. s7delivery レプリケーションエージェントノードに移動します。
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. この設定をレプリケーションエージェントに追加します（値が **[!UICONTROL True]** に設定されたブール値）。

   `enableOauth=true`

1. ページの左上隅近くにある「**[!UICONTROL すべて保存]**」を選択します。

### 設定のテスト {#testing-your-configuration}

設定にはエンドツーエンドのテストを実行することをお勧めします。

このテストを開始する前に、既に次の作業を完了していることを確認してください。

* 画像プリセットを追加した。
* クラウドサービスの下の **[!UICONTROL Dynamic Media 設定（6.3 以前）]**&#x200B;を設定する。このテストでは画像サービスの URL が必要です。

**設定をテストするには：**

1. 画像アセットをアップロードします（Assets で、**[!UICONTROL 作成]** / **[!UICONTROL ファイル]** に移動し、ファイルを選択します）。
1. ワークフローが完了するまで待ちます。
1. 画像アセットを公開します（アセットを選択し、「**[!UICONTROL クイック公開]**」を選択します）。
1. 画像を開いて、その画像のレンディションに移動し、「**[!UICONTROL レンディション]**」をタップします。

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. 任意の動的レンディションを選択します。
1. このアセットの URL を取得するには、「**[!UICONTROL URL]**」を選択します。
1. 選択した URL に移動して画像が期待どおりに動作するかどうかを確認します。

アセットが配信されたことをテストするもう 1 つの方法は、URL に req=exists を追加することです。

## Dynamic MediaCloud Services {#configuring-dynamic-media-cloud-services}

Dynamic MediaCloud Serviceは、画像やビデオ、ビデオ分析、ビデオエンコーディングなどのハイブリッド公開および配信をサポートします。

設定の一環として、登録 ID、ビデオサービス URL、画像サービス URL、レプリケーションサービス URL を入力し、認証を設定する必要があります。 この情報は、アカウントのプロビジョニングプロセスの一環として電子メールでお送りしました。 この情報を受け取っていない場合は、Adobe Experience Manager管理者またはAdobeカスタマーサポートに問い合わせて、情報を入手してください。

>[!NOTE]
Dynamic MediaCloud Servicesを設定する前に、パブリッシュインスタンスを必ず設定しておいてください。 また、Dynamic MediaCloud Servicesを設定する前に、レプリケーションを設定する必要があります。

**Dynamic MediaCloud Servicesを設定するには：**

1. Experience Managerで、Experience Managerのロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]** / **[!UICONTROL Cloud Services]** / **[!UICONTROL Dynamic Media設定（6.3 以前）]** に移動します。
1. Dynamic Media設定ブラウザーページの左側のウィンドウで、「**[!UICONTROL グローバル]**」を選択し、「**[!UICONTROL 作成]**」を選択します。
1. **[!UICONTROL Dynamic Media 設定を作成]**&#x200B;ダイアログボックスで、「タイトル」フィールドにタイトルを入力します。
1. ビデオ用に Dynamic Media を設定する場合は、次の操作をおこないます。

   * 「**[!UICONTROL 登録 ID]**」フィールドに登録 ID を入力します。
   * 「**[!UICONTROL ビデオサービスの URL]**」フィールドに、Dynamic Media ゲートウェイのビデオサービス URL を入力します。

1. 画像用に Dynamic Media を設定する場合は、「**[!UICONTROL 画像サービスの URL]**」フィールドに Dynamic Media ゲートウェイの画像サービスの URL を入力します。
1. 「**[!UICONTROL 保存]**」を選択して、「Dynamic Media設定ブラウザー」ページに戻ります。
1. グローバルナビゲーションコンソールにアクセスするには、Experience Managerロゴを選択します。

## ビデオレポートの設定 {#configuring-video-reporting}

Dynamic Mediaハイブリッドを使用して、複数のインストールのExperience Managerにわたってビデオレポートを設定できます。

**用途：** Dynamic Media 設定（6.3 以前）を設定すると、ビデオレポートを含む様々な機能が開始されます。設定時には、地域の Analytics 企業内にレポートスイートが作成されます。複数のオーサーノードを設定すると、ノードごとに異なるレポートスイートが作成されます。このため、インストール間でレポートデータの整合性が取れなくなります。さらに、すべてのオーサーノードが同じハイブリッドパブリッシュサーバーを参照している場合、最後のオーサーノードでのインストール時に、すべてのビデオレポートの報告先となるレポートスイートが変更されてしまいます。この問題が発生すると、過剰な数のレポートスイートによって Analytics システムが過負荷状態に陥ります。

**手順概要：**&#x200B;ビデオレポートを設定するには、以下の 3 つのタスクを実行します。

1. 最初のオーサーノードで Dynamic Media 設定（6.3 以前）を設定した後、ビデオ分析プリセットパッケージを作成します。この最初のタスクは重要です。これにより、新しい設定でも引き続き同じレポートスイートを使用できるからです。
1. 「新しい」オーサーノードで Dynamic Media 設定（6.3 以前）を設定する「前」に、それらのノードのすべてにビデオ分析プリセットパッケージをインストールします。************
1. パッケージインストールの確認やデバッグをおこないます。

### 最初のオーサーノードを設定した後に、ビデオ分析プリセットパッケージを作成します。 {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

このタスクが完了すると、ビデオ分析プリセットを含むパッケージファイルが作成されます。 これらのプリセットには、レポートスイート、トラッキングサーバー、トラッキング名前空間およびExperience Cloud組織 ID（使用可能な場合）が含まれます。

1. Dynamic Media 設定（6.3 以前）をまだ設定していない場合は、設定します。
1. （オプション）レポートスイート ID を表示してコピーします（JCR へのアクセス権が必要）。レポートスイート ID は必須ではありませんが、あると確認が容易になります。
1. パッケージマネージャーを使用してパッケージを作成します。
1. パッケージを編集してフィルターを含めます。

   Experience Manager:`/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. パッケージをビルドします。
1. ビデオ分析プリセットパッケージを後続の新しいオーサーノードで共有できるように、パッケージをダウンロードまたは共有します。

### 他のオーサーノードを設定する前に、ビデオ分析プリセットパッケージをインストールします {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

このタスクは必ず、Dynamic Media 設定（6.3 以前）を設定する「前」に実行してください。******&#x200B;そうしないと、別の未使用レポートスイートが作成されます。 また、ビデオレポートは引き続き正しく機能しますが、データの収集は最適化されません。

最初のオーサーノードからのビデオ分析プリセットパッケージに新しいオーサーノードからアクセスできることを確認してください。

1. 先ほど作成したビデオ分析プリセットパッケージをパッケージマネージャーにアップロードします。
1. ビデオ分析プリセットパッケージをインストールします。
1. Dynamic Media 設定（6.3 以前）を設定します。

### パッケージのインストールの確認とデバッグ {#verifying-and-debugging-the-package-installation}

1. 以下のいずれかをおこなってパッケージのインストールを確認し、必要に応じてそのデバッグをおこないます。

   * **JCR 経由でビデオ分析プリセットをチェックする** JCR 経由でビデオ分析プリセットをチェックするには、CRXDE Lite にアクセスできる必要があります。

      Experience Manager-CRXDE Liteで、`/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata` に移動します。

      `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata` のように

      オーサーノードのCRXDE Liteにアクセスできない場合は、パブリッシュサーバーを通じてプリセットを確認できます。

   * **Image Server でのビデオ分析プリセットの確認**

      Image Server の req=userdata リクエストを実行することで、ビデオ分析プリセットを直接検証できます。
例えば、オーサーノードで Analytics プリセットを表示するには、次のリクエストを実行します。

      `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      パブリッシュサーバーでプリセットを検証するには、パブリッシュサーバーに対して同様の直接要求を行います。 応答はオーサーノードとパブリッシュノードで同じになります。応答は次のようになります。

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **Experience Manager のビデオレポートツールを使用してビデオ分析プリセットを**
確認します **[!UICONTROL ツール]** / **[!UICONTROL アセット]** /ビデオレポ **[!UICONTROL ートに移動します]**

      `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      次のエラーメッセージが表示された場合は、レポートスイートは使用可能ですが、未入力です。 新しいインストールでは、システムがデータの収集を開始するまでこのエラーは正しく、むしろ望ましいと言えます。
   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   レポートデータを生成するには、1 つのビデオをアップロードして公開します。「**[!UICONTROL URL をコピー]**」を使用し、ビデオを 1 回以上再生します。

   ビデオビューアの使用状況からレポートデータが入力されるまで、最大 12 時間かかる場合があります。

    エラーが発生し、レポートスイートの設定が正しくない場合は、次のアラートが表示されます。

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   このエラーは、Dynamic Media 設定（6.3 以前）サービスの設定前にビデオレポートが実行された場合にも表示されます。

### ビデオレポート設定のトラブルシューティング {#troubleshooting-the-video-reporting-configuration}

* インストール中に Analytics API サーバーへの接続がタイムアウトすることがあります。インストール中に接続が 20 回再試行されますが、それでも失敗します。この状況が発生すると、ログファイルに複数のエラーが記録されます。`SiteCatalystReportService` を検索。
* 最初に分析プリセットパッケージをインストールしないと、新しいレベルスイートが作成されてしまう可能性があります。
* Experience Manager6.3 からExperience Manager6.4 またはExperience Manager6.4.1 にアップグレードし、Dynamic Media設定（6.3 より前）を設定しても、レポートスイートが作成されます。 この問題は既知で、Experience Manager6.4.2 で修正される予定です。

### ビデオ分析プリセットについて {#about-the-video-analytics-preset}

ビデオ分析プリセット（単に分析プリセットと呼ばれることもある）は、Dynamic Media 内でビューアプリセットの隣に格納されます。これは基本的にはビューアプリセットと同じですが、AppMeasurement および Video Heartbeat レポートの設定に使用される情報が付加されています。

このプリセットのプロパティは次のとおりです。

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` ( 古いバージョンのExperience Managerには存在しない )

Experience Manager6.4 以降のバージョンでは、このプリセットは `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata` に保存されます。

## カタログ設定のレプリケート {#replicating-catalog-settings}

JCR を通じて、設定プロセスの一部として独自のデフォルトカタログ設定を公開します。 カタログ設定をレプリケートするには：

1. ターミナルウィンドウで以下を実行します。

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. Experience Managerで、CRXDE Liteの次の場所に移動します（管理者権限が必要です）。

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. 「**[!UICONTROL レプリケーション]**」タブを選択します。
1. 「**[!UICONTROL 複製]**」を選択します。

## ビューアプリセットの複製 {#replicating-viewer-presets}

ビューアプリセットを使用して *アセットを配信するには、ビューアプリセットをレプリケート/公開* する必要があります。 (URL を取得したりアセットのコードを埋め込んだりするには、すべてのビューアプリセットをアクティベートして ** をレプリケートする必要があります。
詳しくは、[ ビューアプリセットの公開 ](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) を参照してください。

>[!NOTE]
デフォルトでは、アセットの詳細表示で「**[!UICONTROL レンディション]**」を選択すると様々なレンディションが表示され、「**[!UICONTROL ビューア]**」を選択すると様々なビューアプリセットが表示されます。 表示される数を増減させることができます。[ 表示される画像プリセットの数を増やす ](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) または [ 表示されるビューアプリセットの数を増やす ](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display) を参照してください。

## レプリケーション用のアセットのフィルタリング {#filtering-assets-for-replication}

Dynamic Media以外のデプロイメントでは、Experience Managerオーサー環境からExperience Managerパブリッシュノードに *すべての* アセット（画像とビデオの両方）をレプリケートします。 アセットの公開サーバーもExperience Managerを配信するので、このワークフローが必要です。

ただし、Dynamic Mediaデプロイメントでは、アセットはクラウド経由で配信されるので、同じアセットをExperience Managerのパブリッシュノードにレプリケートする必要はありません。 このような「ハイブリッド公開」ワークフローを使用すると、余分なストレージコストと、アセットをレプリケートするための処理時間が長くなります。 Dynamic Mediaビューア、サイトページ、静的コンテンツなどのその他のコンテンツは、引き続きExperience Managerのパブリッシュノードから提供されます。

アセットをレプリケートする以外に、次の非アセットもレプリケートされます。

* Dynamic Media配信設定：`/conf/global/settings/dam/dm/imageserver/jcr:content`
* 画像プリセット: `/conf/global/settings/dam/dm/presets/macros`
* ビューアプリセット: `/conf/global/settings/dam/dm/presets/viewer`

フィルターを使用すると、Experience Managerのパブリッシュノードにアセットをレプリケート *除外* できます。

### レプリケーションにデフォルトのアセットフィルターを使用 {#using-default-asset-filters-for-replication}

実稼動環境でDynamic Media(1) の画像処理に *または*(2) の画像処理とビデオ処理を使用する場合、Adobeがそのまま提供するデフォルトのフィルターを使用できます。 次のフィルターがデフォルトでアクティブです。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>フィルター</strong></td>
   <td><strong>MIME タイプ</strong></td>
   <td><strong>レンディション</strong></td>
  </tr>
  <tr>
   <td>ダイナミックメディア画像配信</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p><strong>image/</strong> で始まる</p> <p><strong>application/</strong> を含み、<strong>set</strong> で終わる</p> </td>
   <td>標準提供の「filter-images」（インタラクティブな画像などの単一の画像アセットに適用）および「filter-sets」（スピンセット、画像セット、混在メディアセットおよびカルーセルセット）では、次のようになります。
    <ul>
     <li>PTIFF 画像とメタデータ（<strong>cqdam</strong> で始まるすべてのレンディション）がレプリケーションに含まれます。</li>
     <li>オリジナル画像と静的画像レンディションがレプリケーションから除外されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>ダイナミックメディアビデオ配信</td>
   <td>filter-video</td>
   <td><strong>video/</strong> で始まる</td>
   <td>標準提供の「filter-video」では、次のようになります。
    <ul>
     <li>プロキシビデオレンディション、ビデオサムネール/ポスター画像、メタデータ（親ビデオとビデオレンディションの両方）をレプリケーション用に含めます（<strong>cqdam</strong> で始まるすべてのレンディション）。</li>
     <li>元のビデオと静的なサムネールのレンディションをレプリケーションから除外します。<br /> <br /> <strong>注意：</strong> プロキシビデオレンディションにはバイナリは含まれず、代わりにノードプロパティが含まれます。このため、公開者のリポジトリサイズには影響しません。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Classic(Scene7) の統合</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p>filter-video</p> </td>
   <td><p><strong>image/</strong> で始まる</p> <p><strong>application/</strong> を含み、<strong>set</strong> で終わる</p> <p><strong>video/</strong> で始まる</p> </td>
   <td><p>トランスポート URI を、AdobeDynamic Media Cloud Replication Service の URL ではなく、Experience Managerのパブリッシュサーバーを指すように設定します。 このフィルターを設定すると、Dynamic Media Classicは、アセットパブリッシュインスタンスではなくExperience Managerを配信できます。</p> <p>標準の「filter-images」、「filter-sets」および「filter-video」では、次の処理がおこなわれます。</p>
    <ul>
     <li>PTIFF 画像、プロキシビデオのレンディションおよびメタデータがレプリケーションに含まれます。ただし、Experience Manager- Dynamic Media Classic統合を実行しているユーザーの JCR には存在しないので、実際には何も実行しません。</li>
     <li>オリジナル画像、静的画像レンディション、オリジナルビデオおよび静的サムネールレンディションがレプリケーションから除外されます。代わりに、Dynamic Media Classicは画像およびビデオアセットを配信します。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
フィルターは MIME タイプに適用され、パス固有にすることはできません。

### ビデオのみのデプロイメント用のアセットフィルターの設定 {#setting-up-asset-filters-for-video-only-deployments}

Dynamic Media をビデオのみに使用している場合は、次の手順に従ってレプリケーション用のアセットフィルターを設定します。

1. Experience Managerで、Experience Managerのロゴを選択してグローバルナビゲーションコンソールにアクセスし、 **[!UICONTROL ツール]** / **[!UICONTROL デプロイ]** / **[!UICONTROL レプリケーション]** / **[!UICONTROL 作成者のエージェント]** に移動します。
1. 作成者のエージェントページで、「**[!UICONTROL デフォルトエージェント (publish)]**」を選択します。
1. 「**[!UICONTROL 編集]**」を選択します。
1. [**[!UICONTROL エージェントの設定]**] ダイアログボックスの [**[!UICONTROL 設定]**] タブで、[**[!UICONTROL 有効]**] をオンにしてエージェントをオンにします。
1. 「**[!UICONTROL OK]**」を選択します。
1. Experience Managerで、**[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]** に移動します。
1. 左のフォルダーツリーで、`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` に移動します。
1. **[!UICONTROL filter-video]** を探して右クリックし、「**[!UICONTROL コピー]**」を選択します。
1. 左のフォルダーツリーで、`/etc/replication/agents.author/publish` に移動します。
1. `jcr:content` を探して右クリックし、**[!UICONTROL 貼り付け]** を選択します。

次の手順では、ビデオのポスター画像と再生に必要なビデオメタデータを配信し、ビデオ自体はDynamic MediaCloud Serviceによって配信するExperience Managerの公開インスタンスを設定します。 また、このフィルターは、元のビデオと静的なサムネールのレンディションをレプリケーションから除外します。これらは、パブリッシュインスタンスでは不要です。

### 実稼動環境以外のデプロイメントでの画像用のアセットフィルターのセットアップ {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

実稼動環境以外のデプロイメントで画像に Dynamic Media を使用している場合は、次の手順に従ってレプリケーション用のアセットフィルターを設定します。

1. Experience Managerで、Experience Managerのロゴを選択してグローバルナビゲーションコンソールにアクセスし、 **[!UICONTROL ツール]** / **[!UICONTROL デプロイ]** / **[!UICONTROL レプリケーション]** / **[!UICONTROL 作成者のエージェント]** に移動します。
1. 作成者のエージェントページで、「**[!UICONTROL デフォルトエージェント (publish)]**」を選択します。
1. 「**[!UICONTROL 編集]**」を選択します。
1. [**[!UICONTROL エージェントの設定]**] ダイアログボックスの [**[!UICONTROL 設定]**] タブで、[**[!UICONTROL 有効]**] をオンにしてエージェントをオンにします。
1. 「**[!UICONTROL OK]**」を選択します。
1. Experience Managerで、**[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]** に移動します。
1. 左のフォルダーツリーで、`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` に移動します。

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. **[!UICONTROL filter-images]** を探し、右クリックして「**[!UICONTROL コピー]**」を選択します。
1. 左のフォルダーツリーで、`/etc/replication/agents.author/publish` に移動します。
1. `jcr:content` を探して右クリックし、**[!UICONTROL 作成]** /**[!UICONTROL ノードを作成]** に移動します。 タイプ `nt:unstructured` の名前 `damRenditionFilters` を入力します。
1. `damRenditionFilters` を探して右クリックし、**[!UICONTROL 貼り付け]** を選択します。

次の手順では、Experience Managerパブリッシュインスタンスを設定して、実稼動以外の環境に画像を配信します。 また、このフィルターは、元の画像と静的レンディションをレプリケーションから除外します。静的レンディションはパブリッシュインスタンスでは不要です。

>[!NOTE]
1 人の作成者に異なるフィルターが多数ある場合は、各エージェントに異なるユーザーを割り当てる必要があります。Granite コードでは、ユーザーごとに 1 つのフィルターというモデルが適用されます。フィルターの設定ごとに必ず異なるユーザーを使用してください。
1 つのサーバーで複数のフィルターを使用しているか。 例えば、公開するレプリケーション用のフィルターと、s7delivery 用の 2 番目のフィルターがあります。 その場合は、これら 2 つのフィルターに異なる **userId** が `jcr:content` ノードで割り当てられていることを確認する必要があります。 次の画像を参照してください。

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### レプリケーション用のアセットフィルターのカスタマイズ（オプション） {#customizing-asset-filters-for-replication}

1. Experience Managerで、Experience Managerのロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]** / **[!UICONTROL 一般]** / **[!UICONTROL CRXDE Lite]** に移動します。
1. 左側のフォルダーツリーで `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` に移動し、フィルターを確認します。

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. フィルターの MIME タイプを定義するために、次のように MIME タイプを特定することができます。

   左側のレールで `content > dam > <locate_your_asset> >  jcr:content > metadata` を展開し、表内で `dc:format` を探します。

   次の図は、`dc:format` へのアセットのパスの例です。

   ![chlimage_1-512](assets/chlimage_1-512.png)

   アセット `Fiji Red.jpg` の `dc:format` は `image/jpeg` です。

   このフィルターをすべての画像に適用するには、形式に関係なく、値を `image/*` に設定します。`*` は、任意の形式のすべての画像に適用される正規表現です。

   フィルターをタイプJPEGの画像にのみ適用するには、値 `image/jpeg` を入力します。

1. レプリケーションに含める、またはレンディションから除外するレンディションを定義します。

   レプリケーション用のフィルターに使用できる文字は次のとおりです。

   | 使用する文字 | レプリケーション用のアセットのフィルター方法 |
   | --- | --- |
   | `*` | ワイルドカード文字 |
   | `+` | レプリケーション用のアセットを含む |
   | `-` | レプリケーションからアセットを除外 |

   `content/dam/<locate your asset>/jcr:content/renditions` に移動します。

   次の図は、あるアセットのレンディションの例を示しています。

   ![chlimage_1-513](assets/chlimage_1-4.png)

   上記の例を使用して、PTIFF( ピラミッドTIFF) のみをレプリケートする場合は、`cqdam` で始まるすべてのレンディションを含む `+cqdam,*` と入力します。 この例では、そのレンディションは `cqdam.pyramid.tiff` です。

   オリジナルを複製するだけの場合は、`+original` と入力します。

## Dynamic Media 画像サーバーの設定 {#configuring-dynamic-media-image-server-settings}

Dynamic Media 画像サーバーの設定では、Adobe CQ Scene7 ImageServer バンドルと Adobe CQ Scene7 PlatformServer バンドルの編集をおこないます。

>[!NOTE]
Dynamic Mediaは、有効にした後に [ 標準で動作します。](#enabling-dynamic-media) ただし、必要に応じて、特定の仕様または要件を満たすようにDynamic Media Image Server を設定して、インストールを微調整することもできます。

**前提条件**  -  ** Dynamic Media Image Server を設定する前に、Windows®の VM にMicrosoft® Visual C++ライブラリのインストールが含まれていることを確認してください。Dynamic Media 画像サーバーを実行するには、このライブラリが必要です。[Microsoft® Visual C++ 2010 再頒布可能パッケージ (x64) は、こちら ](https://www.microsoft.com/ja-jp/download/details.aspx?id=26999) からダウンロードできます。

Dynamic Media 画像サーバーを設定するには：

1. Experience Managerの左上隅で、**[!UICONTROL Adobe Experience Manager]** を選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**/**[!UICONTROL 操作]**/**[!UICONTROL Web コンソール]** に移動します。
1. Adobe Experience Manager Web コンソールの設定ページで、**[!UICONTROL OSGi]** / **[!UICONTROL Configuration]** に移動し、Experience Manager内で現在実行中のすべてのバンドルを一覧表示します。

   Dynamic Media Delivery Server は、リスト内の次の名前の下にあります。

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. バンドルのリストで、Adobe CQ Scene7 ImageServer の右側にある **[!UICONTROL 編集]** アイコンを選択します。
1. Adobe CQ Scene7 ImageServer ダイアログボックスで、次の設定値を指定します。

   >[!NOTE]
   通常は、デフォルト値を変更する必要はありません。 ただし、デフォルト値を変更した場合、変更を有効にするには、バンドルを再起動する必要があります。

   | プロパティ | デフォルト値 | 説明 |
   | --- | --- | --- |
   | `TcpPort.name` | *`empty`* | ImageServer プロセスとの通信に使用するポート番号。デフォルトでは、空きポートが自動的に検出されます。 |
   | `AllowRemoteAccess.name` | *`empty`* | ImageServer プロセスへのリモートアクセスを許可または禁止します。false の場合、画像サーバーは localhost でのみリッスンします。<br> ローカルホストを指すデフォルトの Externalizer 設定では、特定の VM インスタンスの実際のドメインまたは IP アドレスを指定する必要があります。理由は、localhost が VM の親システムを指しているからです。<br>VM のドメインまたは IP アドレスは、自分自身を解決できるように、ホスト・ファイル・エントリを持つ必要があります。 |
   | `MaxRenderRgnPixels` | 16 MP | レンダリングされる最大サイズ（メガピクセル単位）。 |
   | `MaxMessageSize` | 16 MB | 配信されるメッセージの最大サイズ（メガピクセル単位）。 |
   | `RandomAccessUrlTimeout` | 20 | Image Server が幅のあるタイル要求への応答を JCR が待機する時間（秒）のタイムアウト値。 |
   | `WorkerThreads` | 10 | ワーカースレッドの数。 |

1. 「**[!UICONTROL 保存]**」を選択します。
1. バンドルのリストで、Adobe CQ Scene7 PlatformServer の右側にある「**[!UICONTROL 編集]**」アイコンを選択します。
1. Adobe CQ Scene7 PlatformServer ダイアログボックスで、次のデフォルト値のオプションを設定します。

   >[!NOTE]
   Dynamic Media Image Server は、独自のディスクキャッシュを使用して応答をキャッシュします。Experience Managerの HTTP キャッシュと Dispatcher は、Dynamic Media Image Server からの応答をキャッシュするのに使用できません。

   | プロパティ | デフォルト値 | 説明 |
   |---|---|---|
   | Cache enabled | チェック | 応答キャッシュが有効かどうか |
   | Cache roots | cache | 応答キャッシュフォルダーへの 1 つ以上のパス。相対パスは、内部の s7imaging バンドルフォルダーを基準として解決されます。 |
   | Cache Max Size | 200000000 | 応答キャッシュの最大サイズ（バイト単位）。 |
   | Cache Max Entries | 100000 | キャッシュで許可されるエントリの最大数。 |

### デフォルトのマニフェスト設定 {#default-manifest-settings}

デフォルトのマニフェストを使用して、Dynamic Media 配信の応答を生成するために使用する公開を設定できます。画質 (JPEGの画質、解像度、再サンプリングモード )、キャッシュ（有効期限）を微調整し、大きすぎる画像のレンダリングを防ぐことができます (defaultpix、defaultthumbpix、maxpix)。

デフォルトのマニフェスト設定の場所は、**[!UICONTROL Adobe CQ Scene7 PlatformServer]** バンドルの **[!UICONTROL Catalog root]** デフォルト値から取得されます。デフォルトでは、この値は **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]** 内の次のパスにあります。

`/conf/global/settings/dam/dm/imageserver/`

![CRXDE Liteでの Image Server の設定](assets/configimageservercrxdelite.png)

下の表に記載されているプロパティの値を変更するには、新しい値を入力します。

デフォルトのマニフェストの変更が完了したら、ページの左上隅にある「**[!UICONTROL すべて保存]**」を選択します。

必ず「**[!UICONTROL アクセス制御]**」タブ（「プロパティ」タブの右側）を選択し、全員および dynamic-media-replication ユーザーのアクセス制御権限を `jcr:read` に設定してください。

![「CRXDE Lite」での Image Server の設定と「アクセス制御」タブの設定](assets/configimageservercrxdeliteaccesscontroltab.png)

マニフェスト設定とそのデフォルト値の表：

| プロパティ | デフォルト値 | 説明 |
| --- | --- | --- |
| `bkgcolor` | `FFFFFF` | デフォルトの背景色。実際の画像データが含まれない返信画像のすべての領域を埋めるために使用される RGB 値。画像サービング API の [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html#image-serving-api) も参照してください。 |
| `defaultpix` | `300,300` | デフォルトの表示サイズ。サーバーによって、返信画像がこの幅と高さ以内になるように制限されます（要求で wid=、hei= または scl= を使用して表示サイズが明示的に指定されていない場合）。<br>0 以上の 2 つの整数で指定し、コンマで区切ります。幅と高さ（ピクセル単位）。値を 0 に設定すると、その値を制約なしに保つことができます。 ネストされた要求または埋め込まれた要求に対しては適用されません。<br>画像サービング API の [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html#image-serving-api) も参照してください。<br>ただし、通常はビューアプリセットまたは画像プリセットを使用してアセットを配信します。DefaultPix はビューアプリセットや画像プリセットを使用していないアセットに適用されます。 |
| `defaultthumbpix` | `100,100` | デフォルトのサムネールのサイズ。サムネール要求 (`req=tmb`) に attribute::DefaultPix の代わりに使用されます。<br>サーバーは、返信画像の幅と高さをこの値以下に制限します。サムネール要求 (`req=tmb`) でサイズが明示的に指定されておらず、`wid=`、`hei=` または `scl=` を使用してビューサイズが明示的に指定されていない場合、このアクションは true です。<br>0 以上の 2 つの整数で指定し、コンマで区切ります。幅と高さ（ピクセル単位）。値を 0 に設定すると、その値を制約なしに保つことができます。<br>ネストされた要求または埋め込まれた要求に対しては適用されません。<br>画像サービング API の [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html#image-serving-api) も参照してください。 |
| `expiration` | `36000000` | デフォルトのクライアントキャッシュの存続時間。特定のカタログレコードに有効な catalog::Expiration 値が含まれていない場合のデフォルトの有効期限間隔を指定します。<br>0 以上の実数。返信データが生成されてから有効期限が切れるまでの時間数（ミリ秒単位）。0 に設定すると、常に返信画像が即座に有効期限切れになります。実質的に、クライアントキャッシュが無効になります。デフォルトでは、この時間は 10 時間に設定されています。つまり、新しい画像が公開される場合に、古い画像がユーザーのキャッシュから削除されるまで 10 時間かかります。キャッシュを早くクリアする必要がある場合は、カスタマーサポートにお問い合わせください。<br>画像サービング API の[有効期限](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html)も参照してください。 |
| `jpegquality` | `80` | デフォルトの JPEG エンコード属性。JPEG 返信画像のデフォルト属性を指定します。<br>整数とフラグ（コンマ区切り）。最初の値は 1 ～ 100 の範囲で、品質を定義します。2 番目の値は、通常の動作の場合は 0、JPEGエンコーダーで使用されるRGB色度のダウンサンプリングを無効にする場合は 1 です。<br>画像サービング API の [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html#image-serving-api) も参照してください。 |
| `maxpix` | `2000,2000` | 返信画像のサイズ制限。クライアントに返される返信画像の最大の幅と高さ。<br>要求によって、返信イメージの幅または高さが attribute::MaxPix より大きい場合、サーバはエラーを返します。<br>画像サービング API の [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html#image-serving-api) も参照してください。 |
| `resmode` | `SHARP2` | デフォルトの再サンプリングモード。画像データの拡大縮小に使用するデフォルトの再サンプリングおよび補間属性を指定します。<br>リクエストで `resMode=` が指定されていない場合に使用されます。<br>使用できる値には、 `BILIN` 、 、 `BICUB`またはがありま `SHARP2`す。<br>列挙`bilin` の場合は 2、`bicub` の場合は 3、`sharp2` の場合は 4 に設定します。 `sharp2` を使用すると最適な結果が得られます。<br>画像サービング API の [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html#image-serving-api) も参照してください。 |
| `resolution` | `72` | デフォルトのオブジェクト解像度。特定のカタログレコードに有効な catalog::Resolution 値が含まれていない場合のデフォルトのオブジェクト解像度を指定します。<br>0 より大きい実数。通常は 1 インチあたりのピクセル数で表されますが、他の単位（1 メートルあたりのピクセル数など）で表すこともできます。<br>画像サービング API の[解像度](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html#image-serving-api)も参照してください。 |
| `thumbnailtime` | `1%,11%,21%,31%,41%,51%,61%,71%,81%,91%` | これらの値は、ビデオ再生時間のスナップショットを表し、 [encoding.com](https://www.encoding.com/) に渡されます。 詳しくは、[ ビデオのサムネール ](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode) についてを参照してください。 |

## Dynamic Media カラーマネジメントの設定 {#configuring-dynamic-media-color-management}

Dynamic Mediaカラーマネジメントを使用すると、プレビュー用にアセットをカラー補正できます。

カラー補正により、取り込まれたアセットは、生成された Pyramid TIFF レンディションにカラースペース（RGB、CMYK、グレー）および埋め込みカラープロファイルを維持します。動的レンディションを要求した場合、画像の色は、ターゲットのカラースペースに補正されます。JCR のDynamic Mediaパブリッシュ設定で、出力カラープロファイルを設定します。

Adobeのカラーマネジメントは、ICC(International Color Consortium) プロファイルを使用します。このプロファイルは、ICC で定義された形式です。

Dynamic Mediaのカラーマネジメントを設定し、CMYK、RGBまたはグレー出力を使用して画像プリセットを設定できます。 [画像プリセットの設定](/help/assets/managing-image-presets.md)を参照してください。

高度なユースケースでは、手動設定の `icc=` 修飾子を使用して出力カラープロファイルを明示的に選択できます。

* `icc` -  [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` -  [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
Adobeの標準のカラープロファイルセットは、ソフトウェアディストリビューション ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445) の [ 機能パック12445がインストールされている場合にのみ使用できます。 すべての機能パックとサービスパックは、[ ソフトウェア配布 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) で入手できます。 機能パック12445は、Adobeのカラープロファイルを提供します。


### 機能パック 12445 のインストール {#installing-feature-pack}

Dynamic Mediaのカラーマネジメント機能を使用するには、機能パック12445をインストールします。

**機能パック 12445 をインストールするには：**

1. [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) に移動し、`cq-6.3.0-featurepack-12445` をダウンロードします。

   [!DNL Adobe Experience Manager] でのパッケージの使用について詳しくは、[ パッケージの使用方法 ](/help/sites-administering/package-manager.md) を参照してください。

1. 機能パックをインストールします。

### デフォルトカラープロファイルの設定 {#configuring-the-default-color-profiles}

機能パックをインストールした後、適切なデフォルトカラープロファイルを設定して、RGBまたは CMYK 画像データを要求する際のカラー補正を有効にします。

**デフォルトカラープロファイルを設定するには：**

1. **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]** で、デフォルトのAdobe Colorプロファイルを含む `/conf/global/settings/dam/dm/imageserver/jcr:content` に移動します。

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. 「**[!UICONTROL プロパティ]**」タブの下までスクロールして、色補正プロパティを追加します。 次の表に示すプロパティ名、タイプ、値を手動で入力します。 値を入力したら、「**[!UICONTROL 追加]**」を選択し、「**[!UICONTROL すべて保存]**」を選択して値を保存します。

   カラー補正プロパティは、**カラー補正プロパティ**&#x200B;の表に記載しています。カラー補正プロパティに割り当てることができる値は、**カラープロファイル**&#x200B;の表に記載しています。

   例えば、**[!UICONTROL 名前]** に `iccprofilecmyk` を追加し、**[!UICONTROL 型]** `String` を選択して、`WebCoated` を **[!UICONTROL 値]** として追加します。 次に、「**[!UICONTROL 追加]**」を選択し、「**[!UICONTROL すべて保存]**」を選択して値を保存します。

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **カラー補正プロパティの表**

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>デフォルト</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html">icprofilergb</a></td>
   <td>文字列</td>
   <td>&lt;空白&gt;</td>
   <td>初期設定の RGB カラープロファイルの名前。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html">iccprofilemyk</a></td>
   <td>文字列</td>
   <td>&lt;空白&gt;</td>
   <td>初期設定の CMYK カラープロファイルの名前。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html">icprofilegray</a></td>
   <td>文字列</td>
   <td>&lt;空白&gt;</td>
   <td>初期設定のグレーカラープロファイルの名前。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html">iccprofilesrcrgb</a></td>
   <td>文字列</td>
   <td>&lt;空白&gt;</td>
   <td>埋め込みカラーRGBを持たないRGB画像に使用されるデフォルトのプロファイルカラープロファイルの名前</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">iccprofilesrcmyk</a></td>
   <td>文字列</td>
   <td>&lt;空白&gt;</td>
   <td>埋め込みカラープロファイルを持たない CMYK 画像に使用されるデフォルトの CMYK カラープロファイルの名前。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">icprofilesrcgray</a></td>
   <td>文字列</td>
   <td>&lt;空白&gt;</td>
   <td>埋め込みカラープロファイルを持たない CMYK 画像に使用されるデフォルトのグレーカラープロファイルの名前。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">iccblackpointcompensation</a></td>
   <td>ブール値</td>
   <td>True</td>
   <td>カラー補正中に黒点補正を行うかどうかを指定します。 Adobeでは、この設定をオンにすることをお勧めします。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">icdither</a></td>
   <td>ブール値</td>
   <td>False</td>
   <td>カラー補正中にディザリングを行うかどうかを指定します。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">icrenderintent</a></td>
   <td>文字列</td>
   <td>relative</td>
   <td><p>レンダリングインテントを指定します。指定できる値は次のとおりです。<strong> 知覚的、相対的、彩度、絶対的 </strong><i></i>アドビでは、デフォルトとして<strong>相対</strong><i></i>をお勧めします。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
プロパティ名は大文字と小文字が区別され、すべて小文字にする必要があります。

**カラープロファイルの表**

次のカラープロファイルがインストールされます。

<table>
 <tbody>
  <tr>
   <th><p>名前</p> </th>
   <th><p>色の間隔</p> </th>
   <th><p>説明</p> </th>
  </tr>
  <tr>
   <td>Adobe RGB</td>
   <td>RGB</td>
   <td>Adobe RGB(1998)</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
   <td>RGB</td>
   <td>AppleRGB</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>CIERGB</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMYK</td>
   <td>被覆 FOGRA27 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>被覆 FOGRA39 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMYK</td>
   <td>Coated GRACoL 2006 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>ColorMatchRGB</td>
  </tr>
  <tr>
   <td>EuropeISOCoated</td>
   <td>CMYK</td>
   <td>Europe ISO Coated FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Euro Scale Coated v2</td>
  </tr>
  <tr>
   <td>EuroscaleUncoated</td>
   <td>CMYK</td>
   <td>ユーロスケール非コート v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMYK</td>
   <td>Japan Color 2001 Coated</td>
  </tr>
  <tr>
   <td>JapanColorNewspaer</td>
   <td>CMYK</td>
   <td>日本カラー 2002 年新聞</td>
  </tr>
  <tr>
   <td>JapanColorUncoated</td>
   <td>CMYK</td>
   <td>日本カラー 2001 未塗装</td>
  </tr>
  <tr>
   <td>JapanColorWebCoated</td>
   <td>CMYK</td>
   <td>Japan Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMYK</td>
   <td>Japan Web Coated (Ad)</td>
  </tr>
  <tr>
   <td>新聞印刷 SNAP2007</td>
   <td>CMYK</td>
   <td>米国新聞印刷 (SNAP 2007)</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RGB</td>
   <td>NTSC (1953)</td>
  </tr>
  <tr>
   <td>PAL</td>
   <td>RGB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RGB</td>
   <td>ProPhotoRGB</td>
  </tr>
  <tr>
   <td>PS4Default</td>
   <td>CMYK</td>
   <td>Photoshop 4 のデフォルト CMYK</td>
  </tr>
  <tr>
   <td>PS5Default</td>
   <td>CMYK</td>
   <td>Photoshop 5 デフォルト CMYK</td>
  </tr>
  <tr>
   <td>SheetfedCoated</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Coated v2</td>
  </tr>
  <tr>
   <td>SheetfedUncoated</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Uncoated v2</td>
  </tr>
  <tr>
   <td>SMPTE</td>
   <td>RGB</td>
   <td>SMPTE-C</td>
  </tr>
  <tr>
   <td>sRGB</td>
   <td>RGB</td>
   <td>sRGB IEC61966-2.1</td>
  </tr>
  <tr>
   <td>UncoatedFogra29</td>
   <td>CMYK</td>
   <td>非コート FOGRA29 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoated</td>
   <td>CMYK</td>
   <td>U.S. Web Coated (SWOP) v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>Web Coated FOGRA28 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>Web Coated SWOP 2006 Grade 3 用紙</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Web Coated SWOP 2006 Grade 5 用紙</td>
  </tr>
  <tr>
   <td>WebUncoated</td>
   <td>CMYK</td>
   <td>U.S. Web Uncoated v2</td>
  </tr>
  <tr>
   <td>WideGamutRGB</td>
   <td>RGB</td>
   <td>広域RGB</td>
  </tr>
 </tbody>
</table>

1. 「**[!UICONTROL すべて保存]**」を選択します。

例えば、**[!UICONTROL iccprofilergb]** を `sRGB` に、**[!UICONTROL iccprofilecmyk]** を **[!UICONTROL WebCoated]** に設定できます。

それには、次のようにします。

* RGB および CMYK 画像のカラー補正を有効にします。
* カラープロファイルを持たない RGB 画像は、*sRGB* カラースペースにあると見なされます。
* カラープロファイルを持たない CMYK 画像は、*WebCoated* カラースペースにあると見なされます。
* RGB出力を返す動的レンディションは、その出力を sRGB カラースペースで返します。
* CMYK 出力を返す動的レンディションは、CMYK 出力を *WebCoated* カラースペース内で返します。

## アセットの配信 {#delivering-assets}

上記のすべてのタスクを完了すると、アクティベートされたDynamic Mediaアセットが画像またはビデオサービスから提供されます。 Experience Managerでは、この機能は、 **[!UICONTROL 画像のコピー URL]**、 **[!UICONTROL ビューアのコピー URL]**、 **[!UICONTROL ビューアの埋め込みコード]** および WCM に表示されます。

[Dynamic Media アセットの配信](/help/assets/delivering-dynamic-media-assets.md)を参照してください。

<table>
 <tbody>
  <tr>
   <td><strong>実行する操作...</strong></td>
   <td><strong>結果</strong></td>
  </tr>
  <tr>
   <td>画像 URL のコピー</td>
   <td><p>URL をコピーダイアログボックスに、次のような URL が表示されます（URL はデモ用です）。</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p><code>IMAGESERVICEPUBLISHNODE</code> は画像サービスの URL を表します。</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media アセットの配信</a>も参照してください。</p> </td>
  </tr>
  <tr>
   <td>ビューア URL のコピー</td>
   <td><p>URL をコピーダイアログボックスに、次のような URL が表示されます（URL はデモ用です）。</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>ここで、<code>PUBLISHNODE</code> は通常のExperience Managerのパブリッシュノードを、<code>IMAGESERVICEPUBLISHNODE</code> は画像サービスの URL を指します。</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media アセットの配信</a>も参照してください。</p> </td>
  </tr>
  <tr>
   <td>ビューアの埋め込みコードのコピー</td>
   <td><p>埋め込みコードをコピーダイアログボックスに、次のようなコードスニペットが表示されます（コードサンプルはデモ目的のものです）。</p> <p><code class="code">&lt;style type="text/css"&gt;
       #s7basiczoom_div.s7basiczoomviewer{
       width:100%;
       height:auto;
       }
       &lt;/style&gt;
       &lt;script
       type="text/javascript" src="https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/js/BasicZoomViewer.js"&gt;&lt;/script&gt;
       &lt;div id="s7basiczoom_div"&gt;&lt;/div&gt;
       &lt;script type="text/javascript"&gt;
       var s7basiczoomviewer = new s7viewers.BasicZoomViewer({
       "containerId" : "s7basiczoom_div",
       "params" : {
       "serverurl" : "https://IMAGESERVICEPUBLISHNODE/is/image/",
       "contenturl" : "https://PUBLISHNODE/",
       "config" : "/conf/global/settings/dam/dm/presets/viewer/Zoom_dark",
       "asset" : "/content/dam/path/to/Image.jpg" }
       }).init();
       &lt;/script&gt;</code></p> <p>ここで、<code>PUBLISHNODE</code> は通常のExperience Managerのパブリッシュノードを、<code>IMAGESERVICEPUBLISHNODE</code> は画像サービスの URL を指します。</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media アセットの配信</a>も参照してください。</p> </td>
  </tr>
 </tbody>
</table>

### WCM の Dynamic Media コンポーネントとインタラクティブメディアコンポーネント {#wcm-dynamic-media-and-interactive-media-components}

Dynamic Media コンポーネントとインタラクティブメディアコンポーネントを参照する WCM ページは、配信サービスを参照します。
