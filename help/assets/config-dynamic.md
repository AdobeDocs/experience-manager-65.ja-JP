---
title: Dynamic Media - ハイブリッドモードの設定
description: Dynamic Media - ハイブリッドモードの設定方法を学習します。
uuid: 39ad7d83-d310-4baf-9d85-5532c2f201f3
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 7d8e7273-29f3-4a45-ae94-aad660d2c71d
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/config-dynamic
role: Business Practitioner, Administrator
exl-id: 5719d32c-4f19-47c1-bea9-8fd0bc8439ed
feature: Configuration,Hybrid mode
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '7843'
ht-degree: 38%

---

# Dynamic Media - ハイブリッドモードの設定 {#configuring-dynamic-media-hybrid-mode}

Dynamic Mediaハイブリッドを有効にし、使用するように設定する必要があります。 Dynamic Media では、使用例に応じて、[サポートされる設定](#supported-dynamic-media-configurations)がいくつか用意されています。

>[!NOTE]
>
>Scene7 実行モードの Dynamic Media を設定して実行する場合は、[Dynamic Media - Scene7 モードの設定](/help/assets/config-dms7.md)を参照してください。
>
>ハイブリッド実行モードの Dynamic Media を設定して実行する場合は、このページの手順に従ってください。

Dynamic Media での[ビデオ](/help/assets/video.md)の操作方法を参照してください。

>[!NOTE]
>
>開発用、ステージング用、実稼動用など、異なる環境用に設定されたAdobe Experience Managerを使用する場合は、各環境用にDynamic MediaCloud Servicesを設定します。

>[!NOTE]
>
>Dynamic Mediaの設定に問題がある場合は、Dynamic Mediaに固有のログファイルを確認してください。 これらのファイルは、Dynamic Mediaを有効にすると自動的にインストールされます。
>
>* `s7access.log`
>* `ImageServing.log`

>
>
これらは、[Experience Managerインスタンスの監視と保守](/help/sites-deploying/monitoring-and-maintaining.md)に記載されています。

ハイブリッド公開および配信は、Adobe Experience Manager に対して Dynamic Media によって追加される中心機能です。ハイブリッドパブリッシングでは、画像、セット、ビデオなどのDynamic Mediaアセットを、Experience Managerのパブリッシングノードからではなく、クラウドから配信できます。

Dynamic Mediaビューア、サイトページ、静的コンテンツなどの他のコンテンツは、Experience Managerの公開ノードから引き続き提供されます。

Dynamic Mediaをご利用の場合は、すべてのDynamic Mediaコンテンツの配信メカニズムとしてハイブリッド配信を使用する必要があります。

## ビデオのハイブリッド公開アーキテクチャ {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## 画像のハイブリッド公開アーキテクチャ {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## サポートされる Dynamic Media 設定 {#supported-dynamic-media-configurations}

各設定タスクで参照される用語を次に示します。

| **用語** | **ダイナミックメディア有効** | **説明** |
|---|---|---|
| Experience Manager作成者ノード | 緑色の円の中に白色のチェックマーク | オンプレミスまたはManaged Services経由でデプロイする作成者ノードです。 |
| Experience Manager発行ノード | 赤色の四角の中に白色の「X」 | オンプレミスまたはManaged Services経由でデプロイする発行ノードです。 |
| 画像サービスのパブリッシュノード | 緑色の円の中に白色のチェックマーク | Adobeが管理するデータセンターで実行する発行ノード。画像サービスのURLを指します。 |

Dynamic Mediaは、画像処理のみ、ビデオのみ、または画像処理とビデオの両方に実装できます。 特定のシナリオに合わせてDynamic Mediaを設定する手順については、次の表を参照してください。

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
     <li>Experience Manager<strong>author</strong>ノードで、<a href="#enabling-dynamic-media">Dynamic Media</a>を有効にします。</li>
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
   <td>画像は、Experience Manager公開ノードを通じて配信されます。 このシナリオでは、トラフィックは最小限なので、Adobeのデータセンターに画像を配信する必要はありません。 また、実稼動開始前にコンテンツを安全にプレビューすることができます。</td>
   <td>
    <ol>
     <li>Experience Manager<strong>author</strong>ノードで、<a href="#enabling-dynamic-media">Dynamic Media</a>を有効にします。</li>
     <li>Experience Manager<strong>publish</strong>ノードで、<a href="#enabling-dynamic-media">Dynamic Media</a>を有効にします。</li>
     <li><a href="#replicating-viewer-presets">ビューアプリセットをレプリケート</a>します。</li>
     <li><a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">実稼動環境以外の画像用のアセットフィルター</a>をセットアップします。</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Dynamic Media Image Server を設定します。</a></li>
     <li><a href="#delivering-assets">アセットを配信します。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>任意の環境（実稼動、開発、品質評価、ステージングなど）にビデオのみを配信する</td>
   <td>画像は CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。ビデオポスター画像（再生の開始前に表示されるビデオのサムネール）は、Experience Managerの発行インスタンスによって配信されます。</td>
   <td>
    <ol>
     <li>Experience Manager<strong>author</strong>ノードで、<a href="#enabling-dynamic-media">Dynamic Media</a>を有効にします。</li>
     <li>Experience Manager<strong>publish</strong>ノードで、<a href="#enabling-dynamic-media">enableDynamic Media</a>（公開インスタンスはビデオポスター画像を提供し、ビデオ再生用のメタデータを提供）。</li>
     <li><a href="#configuring-dynamic-media-cloud-services">Dynamic Media クラウドサービス</a>でビデオを設定します。</li>
     <li><a href="#replicating-viewer-presets">ビューアプリセットをレプリケート</a>します。</li>
     <li><a href="#setting-up-asset-filters-for-video-only-deployments">ビデオ専用のアセットフィルター</a>をセットアップします。</li>
     <li><a href="#delivering-assets">アセットを配信します。</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>実稼動環境に画像とビデオの両方を配信する</td>
   <td><p>画像は CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。画像やビデオのポスター画像は世界各地のアドビのデータセンターのサーバーを介して配信されます。CDN を使用してキャッシュすることで、スケーラブルなパフォーマンスで全世界に展開できます。</p> <p>実稼動前の画像またはビデオを設定するには、前の節を参照してください。 </p> </td>
   <td>
    <ol>
     <li>Experience Manager<strong>author</strong>ノードで、<a href="#enabling-dynamic-media">Dynamic Media</a>を有効にします。</li>
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

## Dynamic Media の有効化 {#enabling-dynamic-media}

[Dynamic Media はデフォルトで無効になっています。](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html)Dynamic Mediaの機能を利用するには、`publish`実行モードのように`dynamicmedia`実行モードを使用してDynamic Mediaを有効にする必要があります。 有効にする前に、[技術要件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on)を確認してください。

>[!NOTE]
>
>実行モードを使用してDynamic Mediaを有効にすると、Experience Manager6.1とExperience Manager6.0で`dynamicMediaEnabled`フラグを&#x200B;**[!UICONTROL trueに設定してDynamic Mediaを有効にした機能が置き換えられます。]** このフラグは、Experience Manager6.2以降では機能しません。また、クイックスタートを再起動しなくてもDynamic Mediaを有効にできます。

Dynamic Mediaを有効にすると、Dynamic Mediaの機能がUIで使用可能になり、アップロードされた各画像アセットに、動的な画像レンディションの高速配信に使用される&#x200B;*cqdam.pyramid.tiff*&#x200B;レンディションが提供されます。 これらのPTIFFには、次のような大きな利点があります。

* 1つのプライマリソースストレージのみを管理し、無限のレンディションをオンザフライで生成する機能。追加のは必要ありません。
* ズーム、パン、スピンなどのインタラクティブなビジュアライゼーションを使用する機能。

Experience ManagerでDynamic Mediaクラシックを使用する場合は、[特定のシナリオ](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media)を使用しない限り、Dynamic Mediaを有効にしないでください。 Dynamic Mediaは、実行モードを使用してDynamic Mediaを有効にしない限り無効です。

Dynamic Mediaを有効にするには、コマンドラインまたはクイックスタートファイル名からDynamic Mediaの実行モードを有効にする必要があります。

**Dynamic Mediaを有効にするには**

1. コマンドラインでクイックスタートを起動するときに、次のようにします。

   * 追加`-r dynamicmedia`を指定します。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   s7配信に公開する場合は、次のtrustStore引数も含める必要があります。

   ```
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. `https://localhost:4502/is/image`を要求し、Image Serverが実行中であることを確認します。

   >[!NOTE]
   >
   >Dynamic Mediaの問題のトラブルシューティングを行うには、`crx-quickstart/logs/`ディレクトリの次のログを参照してください。
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log - ImageServerログは、内部ImageServerプロセスの動作を分析する際に使用する統計情報と分析情報を提供します。

   Image Serverログファイル名の例：`ImageServer-57346-2020-07-25.log`
   * s7access-&lt;yyyy>&lt;mm>&lt;dd>.log - s7accessログは、`/is/image`と`/is/content`を介してDynamic Mediaに対して行われた各リクエストを記録します。

   これらのログは、Dynamic Media が有効の場合のみ使用されます。これらは、`system/console/status-Bundlelist`ページから生成された&#x200B;**完全なダウンロード**&#x200B;パッケージには含まれません。Dynamic Mediaの問題がある場合は、カスタマーサポートに問い合わせる際に、これらのログを両方問題に追加します。

### Experience Managerを別のポートまたはコンテキストパスにインストールした場合… {#if-you-installed-aem-to-a-different-port-or-context-path}

[Experience Managerをアプリケーションサーバー](/help/sites-deploying/application-server-install.md)にデプロイし、Dynamic Mediaを有効にする場合は、外部化子で&#x200B;**self**&#x200B;ドメインを設定する必要があります。 そうしないと、アセットのサムネール生成がDynamic Mediaアセットで正しく機能しません。

さらに、異なるポートまたはコンテキストパスで quickstart を実行する場合、**self** ドメインを変更する必要もあります。

ダイナミックメディアが有効の場合、画像アセットの静的サムネールレンディションがダイナミックメディアを使用して生成されます。サムネールの生成がDynamic Mediaで正しく機能するには、Experience Managerが自身に対してURLリクエストを実行し、ポート番号とコンテキストパスの両方を知っている必要があります。

Experience Manager内：

* [Externalizer](/help/sites-developing/externalizer.md) の **self** ドメインがポート番号とコンテキストパスの両方を取得するために使用されます。
* **self**&#x200B;ドメインが設定されていない場合、ポート番号とコンテキストパスはJetty HTTPサービスから取得されます。

Experience ManagerQuickStart WARデプロイメントでは、ポート番号とコンテキストパスを取得できないので、**自己**&#x200B;ドメインを構成する必要があります。 **self** ドメインの設定方法については、[Externalizer のドキュメント](/help/sites-developing/externalizer.md)を参照してください。

>[!NOTE]
[Experience Managerクイックスタートスタンドアロン展開](/help/sites-deploying/deploy.md)では、**self**&#x200B;ドメインは、ポート番号とコンテキストパスを自動構成できるので、通常は構成する必要はありません。 ただし、すべてのネットワークインターフェイスがオフになっている場合は、**self**&#x200B;ドメインを構成する必要があります。

## Dynamic Media の無効化  {#disabling-dynamic-media}

Dynamic Mediaはデフォルトでは有効になっていません。 ただし、以前にDynamic Mediaを有効にした場合は、後でオフにすることができます。

Dynamic Mediaを有効にした後に無効にするには、`-r dynamicmedia`実行モードフラグを削除します。

**有効にした後でDynamic Mediaを無効にするには**

1. コマンドラインでクイックスタートを起動するときに、次のいずれかを実行します。

   * jarファイルを起動する際は、コマンドラインに`-r dynamicmedia`を追加しないでください。

   ```shell
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. リクエスト `https://localhost:4502/is/image`. Dynamic Media が無効化されたことを示すメッセージが表示されます。

   >[!NOTE]
   Dynamic Mediaの実行モードが無効になると、`cqdam.pyramid.tiff`レンディションを生成するワークフロー手順は自動的にスキップされます。 また、動的レンディションのサポートやその他のDynamic Mediaの機能も無効になります。
   また、Experience Managerサーバーの設定後にDynamic Mediaの実行モードが無効になった場合、その実行モードでアップロードされたすべてのアセットが無効になります。

## （オプション）Dynamic Media のプリセットおよび設定を 6.3 から 6.5 にダウンタイムなしで移行{#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Experience ManagerDynamic Mediaを6.3から6.5にアップグレードする場合（ダウンタイムをゼロにする機能が含まれるようになりました）、次のcurlコマンドを実行する必要があります。 このコマンドは、すべてのプリセットと設定をCRXDE Lite内で`/etc`から`/conf`に移行します。

>[!NOTE]
Experience Managerインスタンスを互換モードで実行する場合（つまり、互換性パッケージがインストールされている場合）、これらのコマンドを実行する必要はありません。

互換性パッケージの有無にかかわらず、すべてのアップグレードでは、次のLinux® curlコマンドを実行して、Dynamic Mediaに付属の初期設定の標準搭載ビューアプリセットをコピーできます。

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

`/etc`から`/conf`に作成したカスタムビューアプリセットと設定を移行するには、次のLinux® curlコマンドを実行します。

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 画像レプリケーションの設定 {#configuring-image-replication}

Dynamic Media画像配信は、ビデオサムネールなどのExperience Managerアセットを作成者から公開し、Adobeのオンデマンドレプリケーションサービス(Replication Service URL)に複製することで機能します。 その後、アセットはオンデマンド画像配信サービス(Image Service URL)を介して配信されます。

次の操作を実行します。

1. [認証を設定します](#setting-up-authentication)。
1. [レプリケーションエージェントを構成します](#configuring-the-replication-agent)。

Replication Agentは、画像、ビデオメタデータなどのDynamic Mediaアセットを公開し、AdobeがホストするImage Serviceにセットを公開します。 レプリケーションエージェントはデフォルトでは有効でありません。

レプリケーションエージェントを設定した後、[正常にセットアップされたことを](#validating-the-replication-agent-for-dynamic-media)検証し、テストする必要があります。 ここでは、これらの手順について説明します。

>[!NOTE]
PTIFF 作成のデフォルトのメモリ制限は、すべてのワークフローで 3 GB です。例えば、他のワークフローを一時停止して、3 GB のメモリを必要とする 1 個の画像を処理できます。または、それぞれ 300 MB のメモリを必要とする 10 個の画像を並行して処理できます。
メモリ制限は設定可能で、システムリソースの可用性と、処理される画像コンテンツの種類に合わせて調整されます。 大量のアセットが存在し、システムに十分なメモリがある場合は、この制限を増やして、画像が並行して処理されるようにできます。
メモリの上限を超える画像が拒否されます。
PTIFF 作成のメモリ制限を変更するには、**[!UICONTROL ツール／運営／Web コンソール／Adobe CQ Scene7 PTiffManager]** に移動して、**[!UICONTROL maxMemory]** の値を変更します。

### 認証の設定 {#setting-up-authentication}

作成者のレプリケーション認証を設定し、イメージをDynamic Mediaイメージ配信サービスにレプリケートできるようにします。 最初にKeyStoreを取得し、次に&#x200B;**[!UICONTROL dynamic-media-replication]**&#x200B;ユーザーの下に保存して、設定します。 会社管理者が、プロビジョニングプロセス中にKeyStoreファイルと必要な資格情報を記載したご案内の電子メールを受け取りました。 この情報を受け取っていない場合は、Adobeカスタマーケアにお問い合わせください。

**認証を設定するには**

1. キーストアのファイルとパスワードがまだない場合は、Adobeカスタマーケアにお問い合わせください。 この情報は、プロビジョニングに必要な部分です。 キーがアカウントに関連付けられます。
1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール/セキュリティ/ユーザーをタップします。]**
1. ユーザー管理ページで、**[!UICONTROL dynamic-media-replication]**&#x200B;ユーザーに移動し、をタップして開きます。

   ![dm複製](assets/dm-replication.png)

1. Edit User Settings For dynamic-media-replicationページで、「**[!UICONTROL キーストア]**」タブをタップし、「**[!UICONTROL キーストアを作成」をクリックします。]**

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. **[!UICONTROL キーストアアクセスパスワードを設定]**&#x200B;ダイアログボックスでパスワードを入力し、パスワードを確認します。

   >[!NOTE]
   パスワードは、後でレプリケーションエージェントを構成する際に再入力する必要があるので、覚えておいてください。

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. **[!UICONTROL dynamic-media-replication のユーザー設定を編集]**&#x200B;ページで「**秘密鍵をキーストアファイルから追加**」領域を展開し、以下の情報を追加します（下の画像を参照）。

   * [**[!UICONTROL 新しいエイリアス]**]フィールドに、後でレプリケーション構成で使用するエイリアスの名前を入力します。 例えば、`replication`をエイリアスとして使用できます。
   * 「**[!UICONTROL キーストアファイル」をタップします。]**&#x200B;アドビから提供されたキーストアファイルに移動して選択し、「**[!UICONTROL 開く」をタップします。]**
   * 「**[!UICONTROL KeyStore File Password]**」フィールドに、KeyStore Fileのパスワードを入力します。 このパスワードは、手順5で作成したKeyStoreパスワードではなく&#x200B;****、プロビジョニング時に送信されるご案内の電子メールに記載されたKeyStore File PasswordAdobeです。 キーストアファイルパスワードを受け取っていない場合は、アドビのカスタマーケアに問い合わせてください。
   * 「**[!UICONTROL 秘密鍵のパスワード]**」フィールドに、秘密鍵のパスワードを入力します（前の手順で指定したのと同じ秘密鍵のパスワードを使用できます）。 秘密鍵のパスワードは、プロビジョニング中にアドビから送信されたようこそメールに記載されています。秘密鍵のパスワードを受け取っていない場合は、アドビのカスタマーケアに問い合わせてください。
   * 「**[!UICONTROL 秘密鍵のエイリアス]**」フィールドに、秘密鍵のエイリアスを入力します。例えば、`*companyname*-alias`です。 秘密鍵のエイリアスは、プロビジョニング中にアドビから送信されたようこそメールに記載されています。秘密鍵のエイリアスを受け取っていない場合は、アドビのカスタマーケアに問い合わせてください。

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. 「**[!UICONTROL 保存して閉じる]**」をタップして、このユーザーに対する変更を保存します。

   次に、[レプリケーションエージェントを構成する必要があります。](#configuring-the-replication-agent)

### レプリケーションエージェントの設定 {#configuring-the-replication-agent}

1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール/導入/レプリケーション/作成者のエージェントをタップします。]**
1. 作成者ページのエージェントで、**[!UICONTROL Dynamic Mediaハイブリッド画像レプリケーション(s7配信)をタップします。]**
1. 「**[!UICONTROL 編集」をタップします。]**
1. 「**[!UICONTROL 設定]**」タブをタップし、次のように入力します。

   * **[!UICONTROL 有効]** - レプリケーションエージェントを有効にするには、このチェックボックスを選択します。
   * **[!UICONTROL 地域]**  — 適切な地域に設定します。北米、ヨーロッパ、アジア
   * **[!UICONTROL テナントID]** ：この値は、レプリケーションサービスに発行する会社またはテナントの名前です。この値は、プロビジョニング時にAdobeから送信されるお知らせメールに含まれるテナントIDです。 この情報を受け取っていない場合は、Adobeカスタマーケアにお問い合わせください。
   * **[!UICONTROL Key Store Alias]**  — この値は、「認証の [設定」でキーを生成する際に設定される「**新しいエイリアス**」の値と同じです](#setting-up-authentication)。例えば、 `replication`。（[認証の設定](#setting-up-authentication)の手順7を参照）。
   * **[!UICONTROL Key Store Password]**  — キーストアの **[!UICONTROL 作成をタップしたときに作成されたキーストアのパスワードです。]**&#x200B;このパスワードはアドビが提供するものではありません。[認証の設定](#setting-up-authentication)の手順5を参照してください。

   次の画像はサンプルデータが入力されたレプリケーションエージェントを示します。

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. 「**[!UICONTROL OK]**」をタップします。

### Dynamic Media 用のレプリケーションエージェントの検証 {#validating-the-replication-agent-for-dynamic-media}

Dynamic Mediaのレプリケーションエージェントを検証するには、次の手順を実行します。

「**[!UICONTROL 接続のテスト」をタップします。]**&#x200B;次のように出力されます。

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
* レプリケーションログを確認し、アセットがレプリケートされていることを確認します。
* 画像を公開する。画像をタップし、ドロップダウンメニューで「**[!UICONTROL ビューア]**」を選択し、ビューアプリセットを選択します。 「**[!UICONTROL URL]**」をクリックします。 画像が表示されることを確認するには、ブラウザーでURLパスをコピーして貼り付けます。



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

**解決方法**:が `KeyStore` dynamic-media- **** replicationuserに保存され、正しいパスワードが指定されていることを確認してください。

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

**解決策**：パスワードを確認します。レプリケーションエージェントに保存されたパスワードがキーストアの作成に使用されたパスワードと同じでありません。

#### 問題：InvalidAlgorithmParameterException  {#problem-invalidalgorithmparameterexception}

この問題は、Experience Manager作成者インスタンスの設定エラーが原因で発生します。 作成者のJava™プロセスで正しい`javax.net.ssl.trustStore`が取得されていません。 このエラーは次のレプリケーションログで確認できます。

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

**解決方法**:Experience Manager作成者のJava™プロセスのsystemプロパティが有効なtruststoreに `-Djavax.net.ssl.trustStore=` 設定されていることを確認します。

#### 問題：キーストアが設定されていないか初期化されていない {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

この問題は、ホットフィックスが原因で発生するか、機能パックがdynamic-media-userまたはkeystoreノードを上書きしている可能性があります。

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

**解決策**:

1. ユーザー管理ページに移動します。
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. ユーザー管理ページで`dynamic-media-replication`ユーザーに移動し、をタップして開きます。
1. 「**[!UICONTROL キーストア]**」タブをクリックします。「**[!UICONTROL キーストアを作成]**」ボタンが表示された場合は、「[認証の設定](#setting-up-authentication)」の手順をやり直す必要があります。
1. KeyStoreの設定をやり直す必要がある場合は、[Replication Agent](/help/assets/config-dynamic.md#configuring-the-replication-agent)の設定を再度行う必要があります。

   s7delivery レプリケーションエージェントを再設定します。
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. 「**[!UICONTROL 接続のテスト]**」をタップして、設定が有効であることを確認します。

#### 問題：公開エージェントが OAuth ではなく SSL を使用している {#problem-publish-agent-is-using-ssl-instead-of-oauth}

この問題は、ホットフィックスまたは機能パックが正しくインストールされなかったか、設定が上書きされていなかったことが原因と考えられます。

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

1. Experience Managerで、**[!UICONTROL ツール/一般/CRXDE Liteをクリックします。]**

   `localhost:4502/crx/de/index.jsp`

1. s7delivery レプリケーションエージェントノードに移動します。
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. この設定をレプリケーションエージェントに追加します（値が **[!UICONTROL True]** に設定されたブール値）。

   `enableOauth=true`

1. ページの左上隅近くにある「**[!UICONTROL すべて保存」をタップします。]**

### 設定のテスト {#testing-your-configuration}

設定にはエンドツーエンドのテストを実行することをお勧めします。

このテストを開始する前に、既に次の作業を行っていることを確認してください。

* 画像プリセットを追加した。
* クラウドサービスの下の **[!UICONTROL Dynamic Media 設定（6.3 以前）]**&#x200B;を設定する。このテストでは画像サービスの URL が必要です。

**設定をテストするには**

1. 画像アセットをアップロードします（アセットで、**[!UICONTROL 作成/ファイル]**&#x200B;をタップし、ファイルを選択します）。
1. ワークフローが完了するまで待ちます。
1. 画像アセットを公開します（アセットを選択し、「**[!UICONTROL クイック発行」をタップします。]**）
1. 画像を開き、**[!UICONTROL レンディションをタップして、その画像のレンディションに移動します。]**

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. 任意の動的レンディションを選択します。
1. このアセットのURLを取得するには、「**[!UICONTROL URL]**」をクリックします。
1. 選択した URL に移動して画像が期待どおりに動作するかどうかを確認します。

アセットが配信されたことをテストするもう 1 つの方法は、URL に req=exists を追加することです。

## Dynamic Media クラウドサービスの設定  {#configuring-dynamic-media-cloud-services}

Dynamic MediaCloud Serviceは、画像やビデオ、ビデオ分析、ビデオエンコーディングなどのハイブリッドな投稿や配信をサポートしています。

設定の一部として、登録ID、ビデオサービスURL、イメージサービスURL、レプリケーションサービスURLを入力し、認証を設定する必要があります。 この情報は、アカウントプロビジョニングプロセスの一環として電子メールで送信されます。 この情報を受け取っていない場合は、Adobe Experience Manager管理者またはAdobeカスタマーケアに連絡して、入手してください。

>[!NOTE]
Dynamic MediaCloud Servicesを設定する前に、発行インスタンスを設定しておく必要があります。 また、Dynamic MediaCloud Servicesを構成する前に、レプリケーションを設定する必要があります。

Dynamic MediaCloud Servicesを設定するには：

1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール/Cloud Services/Dynamic Media設定（6.3より前）をタップします。]**
1. [Dynamic Media構成ブラウザ]ページの左ペインで、**[!UICONTROL グローバル]**&#x200B;を選択し、**[!UICONTROL 作成]**&#x200B;をタップします。
1. **[!UICONTROL Dynamic Media 設定を作成]**&#x200B;ダイアログボックスで、「タイトル」フィールドにタイトルを入力します。
1. ビデオ用に Dynamic Media を設定する場合は、次の操作をおこないます。

   * 「**[!UICONTROL 登録 ID]**」フィールドに登録 ID を入力します。
   * 「**[!UICONTROL ビデオサービスの URL]**」フィールドに、Dynamic Media ゲートウェイのビデオサービス URL を入力します。

1. 画像用に Dynamic Media を設定する場合は、「**[!UICONTROL 画像サービスの URL]**」フィールドに Dynamic Media ゲートウェイの画像サービスの URL を入力します。
1. 「**[!UICONTROL 保存]**」をタップして Dynamic Media 設定ブラウザーページに戻ります。
1. グローバルナビゲーションコンソールにアクセスするには、Experience Managerのロゴをタップします。

## ビデオレポートの設定 {#configuring-video-reporting}

Dynamic Mediaハイブリッドを使用すると、複数のExperience Managerをインストールしてビデオレポートを設定できます。

**用途：** Dynamic Media 設定（6.3 以前）を設定すると、ビデオレポートを含む様々な機能が開始されます。設定時には、地域の Analytics 企業内にレポートスイートが作成されます。複数のオーサーノードを設定すると、ノードごとに異なるレポートスイートが作成されます。このため、インストール間でレポートデータの整合性が取れなくなります。さらに、すべてのオーサーノードが同じハイブリッドパブリッシュサーバーを参照している場合、最後のオーサーノードでのインストール時に、すべてのビデオレポートの報告先となるレポートスイートが変更されてしまいます。この問題が発生すると、過剰な数のレポートスイートによって Analytics システムが過負荷状態に陥ります。

**手順概要：**&#x200B;ビデオレポートを設定するには、以下の 3 つのタスクを実行します。

1. 最初のオーサーノードで Dynamic Media 設定（6.3 以前）を設定した後、ビデオ分析プリセットパッケージを作成します。この最初のタスクは重要です。これにより、新しい設定でも引き続き同じレポートスイートを使用できるからです。
1. 「新しい」オーサーノードで Dynamic Media 設定（6.3 以前）を設定する「前」に、それらのノードのすべてにビデオ分析プリセットパッケージをインストールします。************
1. パッケージインストールの確認やデバッグをおこないます。

### 最初のオーサーノードの設定後にビデオ分析プリセットパッケージを作成する {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

このタスクが完了すると、ビデオ分析プリセットを含むパッケージファイルが作成されます。 これらのプリセットには、レポートスイート、トラッキングサーバー、トラッキング名前空間および Marketing Cloud 組織 ID（利用可能な場合）が含まれます。

1. Dynamic Media 設定（6.3 以前）をまだ設定していない場合は、設定します。
1. （オプション）レポートスイート ID を表示してコピーします（JCR へのアクセス権が必要）。レポートスイート ID は必須ではありませんが、あると確認が容易になります。
1. パッケージマネージャーを使用してパッケージを作成します。
1. パッケージを編集してフィルターを含めます。

   Experience Manager内：`/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. パッケージをビルドします。
1. ビデオ分析プリセットパッケージを後続の新しいオーサーノードで共有できるように、パッケージをダウンロードまたは共有します。

### 追加の作成者ノードを設定する前にVideo Analyticsプリセットパッケージをインストールする{#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

このタスクは必ず、Dynamic Media 設定（6.3 以前）を設定する「前」に実行してください。******&#x200B;これに失敗すると、未使用のレポートスイートが別に作成されます。 また、ビデオレポートが引き続き正しく機能しますが、データ収集は最適化されません。

最初のオーサーノードからのビデオ分析プリセットパッケージに新しいオーサーノードからアクセスできることを確認してください。

1. 前に作成したVideo AnalyticsプリセットパッケージをPackage Managerにアップロードします。
1. ビデオ分析プリセットパッケージをインストールします。
1. Dynamic Media 設定（6.3 以前）を設定します。

### パッケージインストールの確認やデバッグ  {#verifying-and-debugging-the-package-installation}

1. 以下のいずれかをおこなってパッケージのインストールを確認し、必要に応じてそのデバッグをおこないます。

   * **JCR 経由でビデオ分析プリセットをチェックする** JCR 経由でビデオ分析プリセットをチェックするには、CRXDE Lite にアクセスできる必要があります。

      Experience Manager-CRXDE Liteで`/conf/global/settings/
dam/dm/presets/analytics/jcr:content/userdata`に移動

      `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`と同様

      作成者ノードのCRXDE Liteにアクセスできない場合は、公開サーバを使用してプリセットを確認できます。

   * **Image ServerでのVideo Analyticsプリセットの確認**

      Image Server req=userdataをリクエストして、Video Analyticsプリセットを直接検証できます。
例えば、作成者ノードでAnalyticsプリセットを表示するには、次のように要求します。

      `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

      公開サーバでプリセットを検証する場合は、公開サーバに対しても同様の直接要求を行うことができます。 応答はオーサーノードとパブリッシュノードで同じになります。応答は次のようになります。

      ```
      marketingCloudOrgId=0FC4E86B573F99CC7F000101
       reportSuite=aemaem6397618-2018-05-23
       trackingNamespace=aemvideodal
       trackingServer=aemvideodal.d2.sc.omtrdc.net
      ```

   * **Experience ManagerのビデオレポートツールでVideo Analyticsプリセットをチェックします。**
ツール/ **[!UICONTROL アセット/ビデオレポートをタップします。]**

      `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

      次のエラーメッセージが表示された場合は、レポートスイートは使用可能ですが、入力されていません。 新しいインストールでは、システムがデータの収集を開始するまでこのエラーは正しく、むしろ望ましいと言えます。
   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   レポートデータを生成するには、1 つのビデオをアップロードして公開します。「**[!UICONTROL URL をコピー]**」を使用し、ビデオを 1 回以上再生します。

   ビデオビューアの使用状況に基づいてレポートデータが入力されるまで、最大12時間かかる場合があります。

    エラーが発生し、レポートスイートの設定が正しくない場合は、次のアラートが表示されます。

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   このエラーは、Dynamic Media 設定（6.3 以前）サービスの設定前にビデオレポートが実行された場合にも表示されます。

### ビデオレポートの設定のトラブルシューティング  {#troubleshooting-the-video-reporting-configuration}

* インストール中に Analytics API サーバーへの接続がタイムアウトすることがあります。インストール中に接続が 20 回再試行されますが、それでも失敗します。この状況が発生すると、ログファイルに複数のエラーが記録されます。`SiteCatalystReportService` を検索。
* 最初に分析プリセットパッケージをインストールしないと、新しいレベルスイートが作成されてしまう可能性があります。
* Experience Manager6.3からExperience Manager6.4またはExperience Manager6.4.1にアップグレードし、Dynamic Media設定（6.3より前）を設定した後でも、レポートスイートは作成されます。 この問題は既知で、Experience Manager6.4.2で修正される予定です。

### ビデオ分析プリセットについて {#about-the-video-analytics-preset}

ビデオ分析プリセット（単に分析プリセットと呼ばれることもある）は、Dynamic Media 内でビューアプリセットの隣に格納されます。これは基本的にはビューアプリセットと同じですが、AppMeasurement および Video Heartbeat レポートの設定に使用される情報が付加されています。

このプリセットのプロパティは次のとおりです。

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (古いバージョンのExperience Managerには存在しません)

Experience Manager6.4以降のバージョンでは、このプリセットは`/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`に保存されます。

## カタログ設定のレプリケート {#replicating-catalog-settings}

JCRを介して、設定プロセスの一部として独自のデフォルトのカタログ設定を公開します。 カタログ設定をレプリケートするには：

1. ターミナルウィンドウで以下を実行します。

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. Experience Managerで、CRXDE Lite内の次の場所に移動します（管理者権限が必要です）。

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. 「**[!UICONTROL レプリケーション]**」タブをタップします。
1. **[!UICONTROL 複製]**&#x200B;をタップします。

## ビューアプリセットのレプリケート {#replicating-viewer-presets}

ビューアプリセットを使用して&#x200B;*アセットを配信するには、ビューアプリセットを複製/公開*&#x200B;する必要があります。 (アセットのURLまたは埋め込みコードを取得するには、すべてのビューアプリセットを&#x200B;*および*複製する必要があります。
詳しくは、[ビューアプリセットの公開](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)を参照してください。

>[!NOTE]
初期設定では、アセットの詳細表示で&#x200B;**[!UICONTROL レンディション]**&#x200B;を選択したときに様々なレンディションが表示され、アセットの詳細フォルダで&#x200B;**[!UICONTROL ビューア]**&#x200B;を選択したときに様々なビューアプリセットが表示されます。 表示される数を増減させることができます。詳しくは、[表示する画像プリセットの数の増加](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)または[表示するビューアプリセットの数の増加](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)を参照してください。

## レプリケーション用のアセットのフィルタリング {#filtering-assets-for-replication}

Dynamic Media以外のデプロイメントでは、Experience Manager作成者環境からExperience Manager発行ノードに、*すべての*&#x200B;アセット（画像とビデオの両方）を複製します。 このワークフローは、Experience Managerのパブリッシュサーバーがアセットも配信するので必要です。

ただし、Dynamic Mediaのデプロイメントでは、アセットはクラウド経由で配信されるので、同じアセットをExperience Managerの発行ノードに複製する必要はありません。 このような「ハイブリッドパブリッシング」ワークフローは、アセットの複製に伴うストレージの余分なコストと処理時間を回避します。 Dynamic Mediaビューア、サイトページ、静的コンテンツなどの他のコンテンツは、Experience Managerの公開ノードから引き続き提供されます。

アセットの複製の他に、次の非アセットも複製されます。

* Dynamic Media配信設定：`/conf/global/settings/dam/dm/imageserver/jcr:content`
* 画像プリセット: `/conf/global/settings/dam/dm/presets/macros`
* ビューアプリセット: `/conf/global/settings/dam/dm/presets/viewer`

フィルターを使用すると、Experience Managerの発行ノードにアセットがレプリケートされないように&#x200B;*除外*&#x200B;できます。

### レプリケーション用のデフォルトのアセットフィルターの使用 {#using-default-asset-filters-for-replication}

実稼働版&#x200B;**または** (2)のイメージングとビデオで(1)イメージングにDynamic Mediaを使用している場合は、Adobeがそのまま提供する初期設定のフィルターを使用できます。 次のフィルターがデフォルトでアクティブです。

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
     <li>レプリケーション用のプロキシビデオレンディション、ビデオサムネール/ポスター画像、メタデータ（親ビデオとビデオレンディションの両方）を含めます（<strong>cqdam</strong>で始まるレンディションを使用）。</li>
     <li>元のビデオと静的なサムネールレンディションを複製から除外します。<br /> <br /> <strong>注意：プロキシビデオレンディション</strong> にはバイナリは含まれず、単なるノードプロパティです。このため、公開者のリポジトリサイズには影響しません。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Mediaクラシック(Scene7)統合</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p>filter-video</p> </td>
   <td><p><strong>image/</strong> で始まる</p> <p><strong>application/</strong> を含み、<strong>set</strong> で終わる</p> <p><strong>video/</strong> で始まる</p> </td>
   <td><p>AdobeのDynamic MediaクラウドレプリケーションサービスのURLではなく、Experience Managerの発行サーバーを指すようにトランスポートURIを設定します。 このフィルターを設定すると、Dynamic Mediaクラシックで、Experience Managerの発行インスタンスの代わりにアセットを配信できます。</p> <p>標準搭載の「filter-images」、「filter-sets」、「filter-video」は次のようになります。</p>
    <ul>
     <li>PTIFF 画像、プロキシビデオのレンディションおよびメタデータがレプリケーションに含まれます。ただし、Experience Managerを実行しているユーザーのJCRには存在しないため、Dynamic Mediaクラシック統合では効果的に何も行いません。</li>
     <li>オリジナル画像、静的画像レンディション、オリジナルビデオおよび静的サムネールレンディションがレプリケーションから除外されます。代わりに、Dynamic Mediaクラシックは画像やビデオのアセットを配信します。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
フィルターはMIME型に適用され、パスに固有のものにすることはできません。

### ビデオ専用デプロイメントでのアセットフィルターのセットアップ {#setting-up-asset-filters-for-video-only-deployments}

Dynamic Media をビデオのみに使用している場合は、次の手順に従ってレプリケーション用のアセットフィルターを設定します。

1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール/導入/レプリケーション/作成者のエージェントをタップします。]**
1. 作成者ページのエージェントで、**[!UICONTROL デフォルトのエージェント（発行）をタップします。]**
1. 「**[!UICONTROL 編集」をタップします。]**
1. **[!UICONTROL エージェント設定]**&#x200B;ダイアログボックスの「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL 有効]**」をオンにしてエージェントを有効にします。
1. 「**[!UICONTROL OK]**」をタップします。
1. Experience Managerで、**[!UICONTROL ツール/一般/CRXDE Liteをタップします。]**
1. 左のフォルダーツリーで、`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`に移動します
1. **[!UICONTROL filter-video]**&#x200B;を探し、右クリックして「**[!UICONTROL コピー」を選択します。]**
1. 左のフォルダーツリーで、`/etc/replication/agents.author/publish`に移動します
1. **[!UICONTROL jcr:content]**&#x200B;を探して右クリックし、「**[!UICONTROL 貼り付け]**」を選択します。

次の手順では、ビデオ自体がDynamic MediaCloud Serviceによって配信されるのに対し、ビデオポスターExperience Managerと再生に必要なビデオメタデータを配信する画像発行インスタンスを設定します。 また、元のビデオと静的サムネールレンディション（パブリッシュインスタンスでは不要）を複製から除外します。

### 実稼動環境以外のデプロイメントでの画像用のアセットフィルターのセットアップ {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

実稼動環境以外のデプロイメントで画像に Dynamic Media を使用している場合は、次の手順に従ってレプリケーション用のアセットフィルターを設定します。

1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール/導入/レプリケーション/作成者のエージェントをタップします。]**
1. 作成者ページのエージェントで、**[!UICONTROL デフォルトのエージェント（発行）をタップします。]**
1. 「**[!UICONTROL 編集」をタップします。]**
1. **[!UICONTROL エージェント設定]**&#x200B;ダイアログボックスの「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL 有効]**」をオンにしてエージェントを有効にします。
1. 「**[!UICONTROL OK]**」をタップします。
1. Experience Managerで、**[!UICONTROL ツール/一般/CRXDE Liteをタップします。]**
1. 左のフォルダーツリーで、`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`に移動します

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. **[!UICONTROL filter-images]**&#x200B;を探し、右クリックして「**[!UICONTROL コピー」を選択します。]**
1. 左のフォルダーツリーで、`/etc/replication/agents.author/publish`に移動します
1. **[!UICONTROL jcr:content]**&#x200B;を探して右クリックし、**[!UICONTROL 作成/ノードを作成を選択します。]** タイプ名 `damRenditionFilters` を入力し `nt:unstructured`ます。
1. `damRenditionFilters`を探し、右クリックして「**[!UICONTROL 貼り付け」を選択します。]**

以下の手順で、Experience Manager公開インスタンスを設定し、画像を実稼働以外の環境に配信します。 また、元の画像と静的レンディション（パブリッシュインスタンスでは不要）を複製から除外します。

>[!NOTE]
1 人の作成者に異なるフィルターが多数ある場合は、各エージェントに異なるユーザーを割り当てる必要があります。Granite コードでは、ユーザーごとに 1 つのフィルターというモデルが適用されます。フィルターを設定するたびに、必ず、異なるユーザーを使用してください。
1つのサーバーで複数のフィルターを使用している場合 例えば、複製を公開するフィルターとs7配信を2つ目のフィルターとで示します。 その場合は、これらの2つのフィルターに異なる&#x200B;**userId**&#x200B;が&#x200B;**jcr:content**&#x200B;ノードで割り当てられていることを確認する必要があります。 次の画像を参照してください。

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### レプリケーション用のアセットフィルターのカスタマイズ {#customizing-asset-filters-for-replication}

（オプション）レプリケーション用のアセットフィルターをカスタマイズするには：

1. Experience Managerで、Experience Managerのロゴをタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール/一般/CRXDE Liteをタップします。]**
1. 左のフォルダーツリーで、`/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`に移動してフィルターを確認します。

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. フィルターの MIME タイプを定義するために、次のように MIME タイプを特定することができます。

   左側のレールで`content > dam > <locate_your_asset> >  jcr:content > metadata`を展開し、テーブルで&#x200B;**[!UICONTROL dc:format.]**&#x200B;を探します。

   次の図は、あるアセットの dc:format へのパスの例を示しています。

   ![chlimage_1-512](assets/chlimage_1-512.png)

   アセット`Fiji Red.jpg`の`dc:format`は`image/jpeg`です。

   このフィルターをすべての画像に適用するには、その形式に関係なく、値を`image/*`に設定します。`*`は、任意の形式のすべての画像に適用される正規式です。

   JPEG形式の画像にのみフィルターを適用するには、`image/jpeg`の値を入力します。

1. レプリケーションに含めるレンディションまたは除外するレンディションを定義します。

   レプリケーション用のフィルターに使用できる文字は次のとおりです。

<table>
 <tbody>
  <tr>
   <td><strong>使用する文字</strong></td>
   <td><strong>レプリケーション用のアセットのフィルター方法</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>ワイルドカード文字<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>レプリケーション用にアセットを含める</td>
  </tr>
  <tr>
   <td>-</td>
   <td>レプリケーションからアセットを除外する</td>
  </tr>
 </tbody>
</table>

`content/dam/<locate your asset>/jcr:content/renditions` に移動します。

次の図は、あるアセットのレンディションの例を示しています。

![chlimage_1-513](assets/chlimage_1-4.png)

上記の例を使用して、PTIFF（ピラミッドTIFF）を複製するだけの場合は、`+cqdam,*`と入力します。この中には、`cqdam`と開始するすべてのレンディションが含まれます。 この例では、`cqdam.pyramid.tiff`がレンディションです。

オリジナルを複製したい場合は、`+original`と入力します。

## Dynamic Media 画像サーバーの設定 {#configuring-dynamic-media-image-server-settings}

Dynamic Media 画像サーバーの設定では、Adobe CQ Scene7 ImageServer バンドルと Adobe CQ Scene7 PlatformServer バンドルの編集をおこないます。

>[!NOTE]
Dynamic Mediaは、](#enabling-dynamic-media)を有効にした後、すぐに使える[で動く。 ただし、特定の仕様や要件を満たすようにDynamic MediaImage Serverを設定することで、インストールを微調整することもできます。

**前提条件**: *Dynamic MediaImage Serverを設定する* 前に、VM of Windows®にMicrosoft® Visual C++ライブラリがインストールされていることを確認してください。Dynamic Media 画像サーバーを実行するには、このライブラリが必要です。[Microsoft® Visual C++ 2010再頒布可能パッケージ(x64)は、](https://www.microsoft.com/ja-jp/download/details.aspx?id=14632)こちらからダウンロードできます。

Dynamic Media 画像サーバーを設定するには：

1. Experience Managerの左上隅にある&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;をタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール/操作/Webコンソールをタップします。]**
1. Adobe Experience ManagerのWebコンソール設定ページで、**[!UICONTROL OSGi >設定]**&#x200B;をタップし、Experience Manager内で現在実行中のすべてのバンドルをリストします。

   Dynamic Media配信サーバは、リスト内の次の名前で検出されます。

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. バンドルのリストで、Adobe CQ Scene7 ImageServer の右にある編集アイコンをタップします。
1. Adobe CQ Scene7 ImageServer ダイアログボックスで、次の設定値を指定します。

   >[!NOTE]
   通常、デフォルト値を変更する必要はありません。 ただし、デフォルト値を変更した場合は、変更を有効にするために、バンドルを再起動する必要があります。

<table>
 <tbody>
  <tr>
   <td><strong>Property</strong></td>
   <td><strong>デフォルト値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>TcpPort.name</td>
   <td><code><em>empty</em></code></td>
   <td>ImageServerプロセスとの通信に使用するポート番号。デフォルトでは、自動的に空きポートが検出されます。</td>
  </tr>
  <tr>
   <td>AllowRemoteAccess.name</td>
   <td><code><em>empty</em></code></td>
   <td><p>ImageServerプロセスへのリモートアクセスを許可または禁止します。falseの場合、Image Serverはlocalhostのみをリッスンします。</p> <p>localhostを指す既定の外部化設定では、特定のVMインスタンスの実際のドメインまたはIPアドレスを指定する必要があります。 この理由は、localhostがVMの親システムを指しているからです。</p> <p>VMのドメインまたはIPアドレスは、ホストファイルのエントリを持っている必要があり、ホストファイルのエントリを解決できます。</p> </td>
  </tr>
  <tr>
   <td>MaxRenderRgnPixels</td>
   <td>16 MPixels</td>
   <td>レンダリングされる最大サイズ（メガピクセル単位）。</td>
  </tr>
  <tr>
   <td>MaxMessageSize</td>
   <td>16 MBytes</td>
   <td>配信されるメッセージの最大サイズ（メガピクセル単位）。</td>
  </tr>
  <tr>
   <td>RandomAccessUrlTimeout</td>
   <td>20</td>
   <td>幅のあるタイル要求に対してJCRが応答するのをImage Serverが待機する時間（秒）のタイムアウト値。</td>
  </tr>
  <tr>
   <td>WorkerThreads</td>
   <td>10</td>
   <td>ワーカースレッドの数。</td>
  </tr>
 </tbody>
</table>

1. 「**[!UICONTROL 保存]**」をタップします。
1. バンドルのリストで、Adobe CQScene7プラットフォームサーバーの右側にある&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンをタップします。
1. Adobe CQ Scene7 PlatformServer ダイアログボックスで、次のデフォルト値のオプションを設定します。

   >[!NOTE]
   Dynamic Media Image Server は、独自のディスクキャッシュを使用して応答をキャッシュします。Experience ManagerのHTTPキャッシュとディスパッチャーは、Dynamic Media Image Serverからの応答をキャッシュするのに使用できません。

   | **プロパティ** | **デフォルト値** | **説明** |
   |---|---|---|
   | Cache enabled | チェック | 応答キャッシュが有効かどうか |
   | Cache roots | cache | 応答キャッシュフォルダーへの 1 つ以上のパス。相対パスは、内部の s7imaging バンドルフォルダーを基準として解決されます。 |
   | Cache Max Size | 200000000 | 応答キャッシュの最大サイズ（バイト単位）。 |
   | Cache Max Entries | 100000 | キャッシュで許可される最大エントリ数。 |

### デフォルトのマニフェスト設定 {#default-manifest-settings}

デフォルトのマニフェストを使用して、Dynamic Media 配信の応答を生成するために使用する公開を設定できます。画質（JPEGの画質、解像度、リサンプリングモード）、キャッシュ（有効期限）を微調整して、大きすぎる画像のレンダリングを防ぐことができます(defaultpix、defaultthumbpix、maxpix)。

デフォルトのマニフェスト設定の場所は、**[!UICONTROL Adobe CQ Scene7 PlatformServer]** バンドルの **[!UICONTROL Catalog root]** デフォルト値から取得されます。デフォルトでは、この値は&#x200B;**[!UICONTROL ツール/一般/CRXDE Lite]**&#x200B;内の次のパスにあります。

`/conf/global/settings/dam/dm/imageserver/`

![CRXDE LiteでのImage Serverの設定](assets/configimageservercrxdelite.png)

下の表に記載されているプロパティの値を変更するには、新しい値を入力します。

デフォルトのマニフェストの変更が完了したら、ページの左上隅にある「**[!UICONTROL すべて保存]**」をタップします。

「プロパティ」タブの右にある「**[!UICONTROL アクセス制御]**」タブをタップし、全員およびDynamic Media Replicationユーザーのアクセス制御権限を`jcr:read`に設定してください。

![CRXDE LiteでのImage Serverの設定と「アクセス制御」タブの設定](assets/configimageservercrxdeliteaccesscontroltab.png)

マニフェスト設定とそのデフォルト値の表：

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>デフォルト値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>bkgcolor</td>
   <td>FFFFFF</td>
   <td><p>デフォルトの背景色。実際の画像データが含まれない返信画像のすべての領域を埋めるために使用される RGB 値。</p> <p>画像サービング API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html#image-serving-api">BkgColor</a> も参照してください。</p> </td>
  </tr>
  <tr>
   <td>defaultpix</td>
   <td>300,300</td>
   <td><p>デフォルトの表示サイズ。サーバーによって、返信画像がこの幅と高さ以内になるように制限されます（要求で wid=、hei= または scl= を使用して表示サイズが明示的に指定されていない場合）。</p> <p>2 つの整数値（0 以上）をコンマ区切りで指定します。幅と高さをピクセル単位で指定します。どちらかまたは両方の値を0に設定して、拘束を適用しないようにできます。 ネストされた要求または埋め込まれた要求に対しては適用されません。</p> <p>画像サービング API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html#image-serving-api">DefaultPix</a> も参照してください。</p> <p>ただし、通常はビューアプリセットまたは画像プリセットを使用してアセットを配信します。DefaultPix はビューアプリセットや画像プリセットを使用していないアセットに適用されます。</p> </td>
  </tr>
  <tr>
   <td>defaultthumbpix</td>
   <td>100,100</td>
   <td><p>デフォルトのサムネールのサイズ。サムネール要求（req=tmb）の attribute::DefaultPix の代わりに使用されます。</p> <p>サーバは、この幅と高さ以下に返信画像を制限します。 サムネールリクエスト(req=tmb)がサイズを明示的に指定せず、'wid='、'hei='または'scl='を使用して表示サイズを明示的に指定しない場合、このアクションはtrueです。</p> <p>2 つの整数値（0 以上）をコンマ区切りで指定します。幅と高さをピクセル単位で指定します。どちらかまたは両方の値を0に設定して、拘束を適用しないようにできます。 </p> <p>ネストされた要求または埋め込まれた要求に対しては適用されません。</p> <p>画像サービング API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html#image-serving-api">DefaultThumbPix</a> も参照してください。 </p> </td>
  </tr>
  <tr>
   <td>expiration</td>
   <td>36000000</td>
   <td><p>デフォルトのクライアントキャッシュの存続時間。特定のカタログレコードに有効な catalog::Expiration 値が含まれていない場合のデフォルトの有効期限間隔を指定します。</p> <p>0 以上の実数。返信データが生成されてから有効期限が切れるまでの時間数（ミリ秒単位）。0 に設定すると、常に返信画像が即座に有効期限切れになります。実質的に、クライアントキャッシュが無効になります。デフォルトでは、この時間は 10 時間に設定されています。つまり、新しい画像が公開される場合に、古い画像がユーザーのキャッシュから削除されるまで 10 時間かかります。より早くキャッシュをクリアする必要がある場合は、カスタマーケアに問い合わせてください。</p> <p>画像サービング API の<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html">有効期限</a>も参照してください。</p> </td>
  </tr>
  <tr>
   <td>jpegquality</td>
   <td>80</td>
   <td><p>デフォルトの JPEG エンコード属性。JPEG 返信画像のデフォルト属性を指定します。</p> <p>整数とフラグをコンマ区切りで指定します。1 つ目の値には 1～100 の範囲で画質を定義します。2つ目の値は、通常の動作の場合は0に、JPEGエンコーダーで使用されるRGB色度ダウンサンプリングを無効にする場合は1に設定します。</p> <p>画像サービング API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html#image-serving-api">JpegQuality</a> も参照してください。</p> </td>
  </tr>
  <tr>
   <td>maxpix</td>
   <td>2000,2000</td>
   <td><p>返信画像のサイズ制限。クライアントに返される返信画像の最大の幅と高さ。</p> <p>リクエストが原因で、幅または高さがattribute::MaxPixより大きい応答イメージを返す場合、サーバはエラーを返します。</p> <p>画像サービング API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html?lang=en#image-serving-api">MaxPix</a> も参照してください。</p> </td>
  </tr>
  <tr>
   <td>resmode</td>
   <td>SHARP2</td>
   <td><p>デフォルトの再サンプリングモード。画像データの拡大縮小に使用するデフォルトの再サンプリングおよび補間属性を指定します。</p> <p>resMode= が要求内で指定されていない場合に使用されます。</p> <p>指定できる値は、BILIN、BICUB、またはSHARP2です。</p> <p>列挙。bilinの場合は2、bicubの場合は3、sharp2補間モードの場合は4に設定します。最良の結果を得るにはsharp2を使用します。</p> <p>画像サービング API の <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html#image-serving-api">ResMode</a> も参照してください。</p> </td>
  </tr>
  <tr>
   <td>resolution</td>
   <td>72</td>
   <td><p>デフォルトのオブジェクト解像度。特定のカタログレコードに有効な catalog::Resolution 値が含まれていない場合のデフォルトのオブジェクト解像度を指定します。</p> <p>0より大きい実数。 通常はピクセル/インチで表されますが、他の単位（ピクセル/メートルなど）でも指定できます。</p> <p>画像サービング API の<a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html#image-serving-api">解像度</a>も参照してください。</p> </td>
  </tr>
  <tr>
   <td>thumbnailtime</td>
   <td>1%,11%,21%,31%,41%,51%,61%,71%,81%,91%</td>
   <td>これらの値は、ビデオ再生時間のスナップショットを表し、<a href="https://www.encoding.com/">encoding.com</a>に渡されます。 詳しくは、<a href="/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode">ビデオサムネールについて</a>を参照してください。</td>
  </tr>
 </tbody>
</table>

## Dynamic Media カラーマネジメントの設定  {#configuring-dynamic-media-color-management}

Dynamic Mediaのカラーマネジメントを使用すると、正しいアセットをプレビュー用にカラーマネジメントできます。

カラー補正により、取り込まれたアセットは、生成された Pyramid TIFF レンディションにカラースペース（RGB、CMYK、グレー）および埋め込みカラープロファイルを維持します。動的レンディションを要求した場合、画像の色は、ターゲットのカラースペースに補正されます。出力カラープロファイルは、JCRのDynamic Mediaパブリッシュ設定で設定します。

Adobeのカラーマネジメントは、ICC(International Color Consortium)プロファイルを使用します。これは、ICCが定義する形式です。

Dynamic Mediaのカラーマネジメントを設定し、CMYK、RGBまたはグレーの出力を使用して画像プリセットを設定できます。 [画像プリセットの設定](/help/assets/managing-image-presets.md)を参照してください。

高度な使用例では、手動設定`icc=`修飾子を使用して出力色プロファイルを明示的に選択することができます。

* `icc` -  [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html)

* `iccEmbed` -  [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html)

>[!NOTE]
標準のAdobeカラープロファイルセットは、Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445)の[Feature Pack 12445がインストールされている場合にのみ使用できます。 すべての機能パックとサービスパックは、[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)で入手できます。 機能パック 12445 は、Adobe カラープロファイルを提供します。


### 機能パック 12445 のインストール  {#installing-feature-pack}

Dynamic Mediaのカラーマネジメント機能を使用するには、機能パック12445をインストールします。

**機能パック12445をインストールするには**

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)に移動し、`cq-6.3.0-featurepack-12445`をダウンロードします。

   [!DNL Adobe Experience Manager]でのパッケージの使い方の詳細は、[パッケージの使い方](/help/sites-administering/package-manager.md)を参照してください。

1. 機能パックをインストールします。

### デフォルトカラープロファイルの設定 {#configuring-the-default-color-profiles}

機能パックをインストールした後、RGBまたはCMYK画像データを要求するときに色補正を有効にするように、適切な初期設定の色プロファイルを設定します。

**デフォルトのカラープロファイルを設定するには**

1. **[!UICONTROL ツール/一般/CRXDE Lite]**&#x200B;で、デフォルトのAdobe Colorプロファイルが含まれる`/conf/global/settings/dam/dm/imageserver/jcr:content`に移動します。

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. 「追加&#x200B;**[!UICONTROL プロパティ]**」タブの下部にスクロールして、色を修正するプロパティです。 次の表に示すプロパティ名、タイプ、値を手動で入力します。 値を入力したら、**[!UICONTROL 追加]**&#x200B;をタップし、次に&#x200B;**[!UICONTROL すべて保存]**&#x200B;をタップして値を保存します。

   カラー補正プロパティは、**カラー補正プロパティ**&#x200B;の表に記載しています。カラー補正プロパティに割り当てることができる値は、**カラープロファイル**&#x200B;の表に記載しています。

   例えば、**[!UICONTROL 名前]**&#x200B;に`iccprofilecmyk`を追加し、**[!UICONTROL タイプ]** `String`を選択して、`WebCoated`を&#x200B;**[!UICONTROL 値として追加します。]** 次に、「 **** 追加」をタップし、「 **[!UICONTROL すべて保存」]** をタップして値を保存します。

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **カラー補正プロパティの表**

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>型</strong></td>
   <td><strong>デフォルト</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html">icprofilergb</a></td>
   <td>String</td>
   <td>&lt;空白&gt;</td>
   <td>初期設定の RGB カラープロファイルの名前。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html">icprofilecmyk</a></td>
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
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html">icprofilesrcrgb</a></td>
   <td>文字列</td>
   <td>&lt;空白&gt;</td>
   <td>カラープロファイルが埋め込まれていないRGBプロファイルに使用される初期設定のRGBカラー画像の名前</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html">iccprofilesrccmyk</a></td>
   <td>文字列</td>
   <td>&lt;空白&gt;</td>
   <td>カラープロファイルが埋め込まれていないCMYKプロファイルに使用される初期設定のCMYKカラー画像の名前です。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html">iccprofilesrcgray</a></td>
   <td>文字列</td>
   <td>&lt;空白&gt;</td>
   <td>カラープロファイルが埋め込まれていないCMYKプロファイルに使用される初期設定のグレー画像の名前です。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html">iccblackpointcompension</a></td>
   <td>ブール型</td>
   <td>True</td>
   <td>カラー補正中に黒点の補正を行うかどうかを指定します。 Adobeでは、この設定をオンにすることを推奨します。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html">icdither</a></td>
   <td>ブール型</td>
   <td>False</td>
   <td>カラー補正中にディザリングを行うかどうかを指定します。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html">icrenderintent</a></td>
   <td>文字列</td>
   <td>relative</td>
   <td><p>レンダリングインテントを指定します。指定できる値は次のとおりです。<strong>知覚的、相対的、飽和、絶対的。 </strong><i></i>アドビでは、デフォルトとして<strong>相対</strong><i></i>をお勧めします。</p> </td>
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
   <th><p>カラースペース</p> </th>
   <th><p>説明</p> </th>
  </tr>
  <tr>
   <td>AdobeRGB</td>
   <td>RGB</td>
   <td>Adobe RGB(1998)</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
   <td>RGB</td>
   <td>Apple RGB</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>CIE RGB</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMYK</td>
   <td>Coated FOGRA27 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>Coated FOGRA39 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMYK</td>
   <td>Coated GRACoL 2006 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>ColorMatch RGB</td>
  </tr>
  <tr>
   <td>EuropeISOCoated</td>
   <td>CMYK</td>
   <td>Europe ISO Coated FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Euroscale Coated v2</td>
  </tr>
  <tr>
   <td>EuroscaleUncoated</td>
   <td>CMYK</td>
   <td>Euroscale Uncoated v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMYK</td>
   <td>Japan Color 2001 Coated</td>
  </tr>
  <tr>
   <td>JapanColorNewspaper</td>
   <td>CMYK</td>
   <td>Japan Color 2002新聞</td>
  </tr>
  <tr>
   <td>JapanColorUncoated</td>
   <td>CMYK</td>
   <td>Japan Color 2001 Uncoated</td>
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
   <td>新聞印刷SNAP2007</td>
   <td>CMYK</td>
   <td>US Newsprint(SNAP 2007)</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RGB</td>
   <td>NTSC(1953)</td>
  </tr>
  <tr>
   <td>PAL</td>
   <td>RGB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RGB</td>
   <td>ProPhoto RGB</td>
  </tr>
  <tr>
   <td>PS4Default</td>
   <td>CMYK</td>
   <td>Photoshop4のデフォルトCMYK</td>
  </tr>
  <tr>
   <td>PS5Default</td>
   <td>CMYK</td>
   <td>Photoshop5のデフォルトCMYK</td>
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
   <td>Uncoated FOGRA29 (ISO 12647-2:2004)</td>
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
   <td>Web Coated SWOP 2006 Grade 3 Paper</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Web Coated SWOP 2006 Grade 5 Paper</td>
  </tr>
  <tr>
   <td>WebUncoated</td>
   <td>CMYK</td>
   <td>U.S. Web Uncoated v2</td>
  </tr>
  <tr>
   <td>WideGamotRGB</td>
   <td>RGB</td>
   <td>広域RGB</td>
  </tr>
 </tbody>
</table>

1. 「**[!UICONTROL すべて保存」をタップします。]**

例えば、**[!UICONTROL iccprofilergb]**&#x200B;を`sRGB`に設定し、**[!UICONTROL iccprofilecmyk]**&#x200B;を&#x200B;**[!UICONTROL WebCoated.]**&#x200B;に設定できます。

それには、次のようにします。

* RGB および CMYK 画像のカラー補正を有効にします。
* カラープロファイルのないRGB画像は、*sRGB*&#x200B;カラースペースにあると見なされます。
* カラープロファイルのないCMYK画像は、*WebCoated*&#x200B;のカラースペースにあると見なされます。
* RGB出力を返すダイナミックレンディションを*sRGB *カラースペースに返します。
* CMYK出力を返すダイナミックレンディションを&#x200B;*WebCoated*&#x200B;のカラースペースに戻します。

## Delivering Assets {#delivering-assets}

上記のすべてのタスクを完了すると、アクティブ化されたDynamic Mediaアセットは画像またはビデオサービスから提供されます。 Experience Managerでは、この機能は、「画像URLをコピー&#x200B;]**」、「**[!UICONTROL &#x200B;ビューアのURLをコピー&#x200B;]**」、「**[!UICONTROL &#x200B;埋め込みビューアコード&#x200B;]**」、およびWCMに表示されます。**[!UICONTROL 

[Dynamic Media アセットの配信](/help/assets/delivering-dynamic-media-assets.md)を参照してください。

<table>
 <tbody>
  <tr>
   <td><strong>実行する操作...</strong></td>
   <td><strong>結果</strong></td>
  </tr>
  <tr>
   <td>画像 URL のコピー</td>
   <td><p>URLをコピーダイアログボックスには、次のようなURLが表示されます（URLはデモ目的のみです）。</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p><code>IMAGESERVICEPUBLISHNODE</code> は画像サービスの URL を表します。</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media アセットの配信</a>も参照してください。</p> </td>
  </tr>
  <tr>
   <td>ビューア URL のコピー</td>
   <td><p>URLをコピーダイアログボックスには、次のようなURLが表示されます（URLはデモ目的のみです）。</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&amp;config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&amp;serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&amp;contentRoot=%2F</code></p> <p>ここで<code>PUBLISHNODE</code>は通常のExperience Manager発行ノードを、<code>IMAGESERVICEPUBLISHNODE</code>はImage Service URLを表します。</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media アセットの配信</a>も参照してください。</p> </td>
  </tr>
  <tr>
   <td>ビューアの埋め込みコードのコピー</td>
   <td><p>埋め込みコードをコピーダイアログボックスには、次のようなコードスニペットが表示されます（コードサンプルはデモ用です）。</p> <p><code class="code">&lt;style type="text/css"&gt;
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
       &lt;/script&gt;</code></p> <p>ここで<code>PUBLISHNODE</code>は通常のExperience Manager発行ノードを、<code>IMAGESERVICEPUBLISHNODE</code>はImage Service URLを表します。</p> <p><a href="/help/assets/delivering-dynamic-media-assets.md">Dynamic Media アセットの配信</a>も参照してください。</p> </td>
  </tr>
 </tbody>
</table>

### WCM の Dynamic Media コンポーネントとインタラクティブメディアコンポーネント  {#wcm-dynamic-media-and-interactive-media-components}

Dynamic Media コンポーネントとインタラクティブメディアコンポーネントを参照する WCM ページは、配信サービスを参照します。
