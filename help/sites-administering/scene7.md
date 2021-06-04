---
title: Dynamic Media Classicとの統合
description: Adobe Experience ManagerとDynamic Media Classicを統合する方法について説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f244cfb5-5550-4f20-92f0-bb296e2bf76e
source-git-commit: 99230f2b9ce8179de4034d8bd739a5535b2cc0da
workflow-type: tm+mt
source-wordcount: '5517'
ht-degree: 12%

---

# Dynamic Media Classicとの統合{#integrating-with-dynamic-media-classic-scene}

AdobeDynamic Media Classicは、Web、モバイル、Eメールおよびインターネットに接続されたディスプレイと印刷を管理、強化、公開、および配信するためのホストソリューションです。

Dynamic Media Classicを使用するには、Dynamic Media ClassicとAdobe Experience Manager Assetsが相互にやり取りできるようにクラウド設定を行う必要があります。 このドキュメントでは、Dynamic MediaとExperience Managerの設定方法を説明します。

ページ上のすべてのDynamic Media Classicコンポーネントの使用とビデオの操作について詳しくは、[Dynamic Media Classicの使用](../assets/scene7.md)を参照してください。

>[!NOTE]
>
>* Dynamic Media ClassicのDHTMLビューアプラットフォームは、2014年1月31日に正式にサポート終了となりました。 詳しくは、 [DHTMLビューアのサポート終了に関するFAQ](../sites-administering/dhtml-viewer-endoflifefaqs.md)を参照してください。
>* Experience Managerと連携するようにDynamic Media Classicを設定する前に、Dynamic Media ClassicをExperience Managerと統合する際の[ベストプラクティス](#best-practices-for-integrating-scene-with-aem)を参照してください。
>* Dynamic Media Classicをカスタムプロキシ設定で使用する場合、Experience Managerの一部の機能で3.x APIを使用するのと他の機能で4.x APIを使用するので、両方のHTTPクライアントプロキシ設定を指定する必要があります。 3.xは[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)で設定し、4.xは[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)で設定します。

>



## Experience Manager/Dynamic Media ClassicとDynamic Media {#aem-scene-integration-versus-dynamic-media}の統合

Experience Managerユーザーは、Dynamic Mediaを使用する2つのソリューションから選択できます。 次のいずれかを使用できます。

* Dynamic Media ClassicとExperience Managerのインスタンスを統合する。
* Experience Managerに統合されたDynamic Mediaを使用する。

次の条件を使用して、どちらのソリューションを選択するかを決定します。

* 公開および配信のためにDynamic Media Classicにリッチメディアアセットが存在する既存の&#x200B;**Dynamic Media Classicのお客様で、これらのExperience ManagerをSites(WCM)オーサリングやExperience Managerアセットと統合して管理する場合は、このドキュメントで説明する[Asset/Dynamic Media Classicポイントツーポイント統合](#aem-scene-point-to-point-integration)を使用します。**

* リッチメディア配信のニーズを持つ&#x200B;**新しい** Experience Managerのお客様の場合は、[Dynamic Mediaオプション](#aem-dynamic-media)を選択します。 このオプションは、既存の S7 アカウントを持たず、システムに多くのアセットを保存している場合に最も有用です。

* 場合によっては、両方のソリューションを使用します。 [二重使用シナリオ](/help/sites-administering/scene7.md#dual-use-scenario)は、そのシナリオを説明します。

### Experience Manager/Dynamic Media Classicポイントツーポイント統合{#aem-scene-point-to-point-integration}

このソリューションのアセットを使用して作業する場合、次のいずれかの操作をおこないます。

* Dynamic Media Classicに直接アセットをアップロードし、**Dynamic Media Classic**&#x200B;コンテンツブラウザーを介してアクセスして、ページオーサリングまたは
* Experience Managerアセットにアップロードして、Dynamic Media Classicへの自動公開を有効にする。**アセット**&#x200B;コンテンツブラウザーを介してページオーサリング用にアクセス

この統合に使用するコンポーネントは、[デザインモード](/help/sites-authoring/author-environment-tools.md#page-modes)の&#x200B;**Dynamic Media Classic**&#x200B;コンポーネント領域にあります。

### Experience ManagerDynamic Media {#aem-dynamic-media}

Experience ManagerDynamic Mediaは、Dynamic Media Classic機能をExperience Managerプラットフォーム内で直接統合したものです。

このソリューションのアセットを使用して作業する場合、次のワークフローに従います。

1. 単一の画像およびビデオアセットをExperience Managerに直接アップロード。
1. ビデオをExperience Manager内で直接エンコード
1. 画像ベースのセットをExperience Manager内で直接作成する。
1. 必要に応じて、画像やビデオにインタラクティブ機能を追加する。

ダイナミックメディア用に使用するコンポーネントは、**[!UICONTROL デザインモード]**&#x200B;の[ダイナミックメディア](/help/sites-authoring/author-environment-tools.md#page-modes)コンポーネント領域にあります。これらには、次が含まれます。

* **[!UICONTROL ダイナミックメディア]** - **[!UICONTROL ダイナミックメディア]**&#x200B;コンポーネントでは、追加しているアセットが画像であるかビデオであるかに応じて、様々なオプションを使用できます。このコンポーネントは画像プリセット、画像ベースのビューア（画像セット、スピンセット、混在メディアセットなど）およびビデオをサポートします。また、レスポンシブなビューアなので、画面のサイズは画面のサイズに基づいて自動的に変更されます。 すべてのビューアは HTML5 ビューアです。

* **[!UICONTROL インタラクティブメディア]**  — イン **[!UICONTROL タラクティブメ]** ディアコンポーネントは、カルーセルバナー、インタラクティブ画像、インタラクティブビデオなどのアセット用です。このようなアセットには、そのようなホットスポットや画像マップに対するインタラクティビティがあります。 このコンポーネントはスマートです。 つまり、追加する画像とビデオのどちらに応じて、様々なオプションがあります。 また、レスポンシブなビューアなので、画面のサイズは画面のサイズに基づいて自動的に変更されます。 すべてのビューアは HTML5 ビューアです。

### 両方を利用するシナリオ  {#dual-use-scenario}

標準設定では、Dynamic MediaとDynamic Media Classicの両方のExperience Manager統合機能を同時に使用できます。 次の使用例の表で、特定の領域のオン/オフを切り替える場合について説明します。

Dynamic MediaとDynamic Media Classicを同時に使用するには：

1. Cloud Servicesで[Dynamic Media Classic](#creating-a-cloud-configuration-for-scene)を設定します。
1. 次の中からお使いのユースケースに合致する手順を実行します。

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Dynamic Media Classic統合</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>実行する操作...</strong></td>
    <td><strong>ユースケースのワークフロー</strong></td>
    <td><strong>画像／ビデオ</strong></td>
    <td><strong>ダイナミックメディアコンポーネント</strong></td>
    <td><strong>S7 コンテンツブラウザーとコンポーネント</strong></td>
    <td><strong>Assets から S7 への自動アップロード</strong></td>
    </tr>
    <tr>
    <td>Sites とダイナミックメディアを初めて使用する</td>
    <td>Experience Managerへのアセットのアップロードと、Experience ManagerDynamic Mediaコンポーネントを使用したSitesページでのアセットのオーサリング</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td>
    <td>オフ</td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>小売り、およびSitesとDynamic Mediaを初めて使用する場合</td>
    <td>管理および配信のために、製品以外のアセットをExperience Managerにアップロードします。 Dynamic Media ClassicにPRODUCTアセットをアップロードし、Experience ManagerとコンポーネントでDynamic Media Classicコンテンツブラウザーを使用して、Sitesで製品の詳細ページを作成します。</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>Assets とダイナミックメディアを初めて使用する</td>
    <td>Dynamic MediaからExperience ManagerAssetsにアセットをアップロードし、公開済みのURL/埋め込みコードを使用する</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td>オフ</td>
    <td>オフ</td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>ダイナミックメディアを使用して初めてテンプレートを作成する</td>
    <td>Dyamic Media を使用して画像とビデオを作成する。Dynamic Media Classicで画像テンプレートを作成し、Dynamic Media Classicコンテンツファインダーを使用して、Sitesページにテンプレートを含めます。</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>既にDynamic Media Classicをご利用のお客様で、Sitesを初めて使用するお客様</td>
    <td>Dynamic Media Classicにアセットをアップロードし、Experience ManagerDynamic Media Classicコンテンツブラウザーを使用してSitesページでアセットを検索およびオーサリングする</td>
    <td>オフ</td>
    <td>オフ</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>既存のDynamic Media Classicのお客様で、SitesとAssetsを初めて使用する</td>
    <td>アセットをDAMにアップロードし、配信用にDynamic Media Classicに自動的に公開します。 Experience ManagerDynamic Media Classicコンテンツブラウザーを使用して、Sitesページでアセットを検索およびオーサリングします。</td>
    <td>オフ</td>
    <td>オフ</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">オン</a></p> <p>（手順 4 を参照）</p> </td>
    </tr>
    <tr>
    <td>既存のDynamic Media Classicのお客様で、Assetsを初めて使用する方</td>
    <td><p>アセットをExperience Managerにアップロードし、Dynamic Mediaを使用してダウンロード/共有のレンディションを生成します。 Experience ManagerアセットをDynamic Media Classicに自動的に公開して配信します。</p> <p><strong>重要：</strong> 処理の重複が発生し、Experience Managerで生成されたレンディションがDynamic Media Classicに同期されない</p> </td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td>オフ</td>
    <td>オフ</td>
    <td><p><a href="#configuringautouploadingfromaemassets">オン</a></p> <p>（手順 4 を参照）</p> </td>
    </tr>
    </tbody>
    </table>

1. (オプション。使用例の表を参照)- [Dynamic Mediaクラウド設定](/help/assets/config-dynamic.md)と[Dynamic Mediaサーバーを有効にする](/help/assets/config-dynamic.md)を設定します。
1. (オプション。（使用例の表を参照） — 「 AssetsからDynamic Media Classicへの自動アップロード」を有効にする場合は、次を追加する必要があります。

   1. Dynamic Media Classicへの自動アップロードを設定します。
   1. ***Damアセットの更新**ワークフロー( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`*****
   1. （オプション） [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)のMIMEタイプでDynamic Media Classicアセットのアップロードを制限します。 このリストにないアセットのMIMEタイプは、Dynamic Media Classicサーバーにアップロードされません。
   1. （オプション）Dynamic Media Classic設定でビデオをセットアップします。 Dynamic MediaとDynamic Media Classicのどちらかまたは両方に対してビデオエンコーディングを同時に有効にできます。 動的レンディションは、Experience Managerインスタンスでのローカルでのプレビューと再生に使用されるのに対して、Dynamic Media Classicビデオレンディションは、Dynamic Media Classicサーバーで生成され、保存されます。 Dynamic MediaとDynamic Media Classicの両方にビデオエンコーディングサービスを設定する場合は、Dynamic Media Classicアセットフォルダーに[ビデオ処理プロファイル](/help/assets/video-profiles.md)を適用します。
   1. （オプション） [Dynamic Media Classicでセキュアプレビューを設定します](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)。

#### 制限事項 {#limitations}

Dynamic Media ClassicとDynamic Mediaの両方を有効にしている場合、次の制限があります。

* アセットを選択し、Experience Managerページ上のDynamic Media Classicコンポーネントにドラッグして、Dynamic Media Classicに手動でアップロードすることはできません。
* Experience Manager- Dynamic Media Classicの同期済みアセットは、Assetsでアセットが編集されると自動的にDynamic Media Classicに更新されますが、ロールバックアクションでは新しいアップロードがトリガーされません。 したがって、Dynamic Media Classicは、ロールバック後すぐに最新バージョンを取得しません。 回避策は、ロールバックが完了した後に再度編集することです。
* Dynamic Media AssetsがDynamic Media Classicシステムとやり取りしないように、ある使用例でDynamic Mediaを使用し、別の使用例でDynamic Media Classicを統合する必要がある場合は、Dynamic MediaフォルダーにDynamic Media Classic設定を適用しないでください。 また、Dynamic Media設定（処理プロファイル）をDynamic Media Classicフォルダーに適用しないでください。

## Dynamic Media ClassicとExperience Manager{#best-practices-for-integrating-scene-with-aem}の統合のベストプラクティス

Dynamic Media ClassicをExperience Managerと統合する場合、次の点に留意する必要がある重要なベストプラクティスがあります。

* 統合のテストドライブ
* 特定のシナリオで推奨される、Dynamic Media Classicからのアセットの直接アップロード

[既知の制限](#known-limitations-and-design-implications)を参照してください。

### 統合のテストドライブ {#test-driving-your-integration}

Adobeでは、ルートフォルダーが会社全体ではなく、サブフォルダーのみを指すようにして、統合をテストドライブすることをお勧めします。

>[!CAUTION]
>
>既存のDynamic Media Classic会社アカウントからアセットを読み込むと、Experience Managerに表示されるのに長い時間がかかる場合があります。 Dynamic Media Classicで、アセットが多すぎないフォルダーを指定してください（例えば、ルートフォルダーに多くの場合、アセットが多すぎてシステムがクラッシュする可能性があります）。

### Dynamic Media AssetsからのExperience ManagerのアップロードとClassicからのアセットのアップロード{#uploading-assets-from-aem-assets-versus-from-scene}

アセットのアップロードは、 Assets（デジタルアセット管理）機能を使用するか、Dynamic Media Classicコンテンツブラウザーを使用してExperience Managerで直接Dynamic Media Classicにアクセスすることで実行できます。 どちらを選択するかは、次の要素によって異なります。

* Dynamic Media AssetsでまだサポートされていないExperience Managerタイプは、Dynamic Media Classicコンテンツブラウザーを使用して、Dynamic Media Classicから直接Experience ManagerWebサイトに追加する必要があります。 例えば、画像テンプレートなどです。
* Experience ManagerAssetsとDynamic Media Classicの両方でサポートされているアセットタイプの場合、アップロード方法は次のように決まります。

   * アセットが現在ある場所、および
   * 共有リポジトリでのそれらの管理の重要度

アセットが既にDynamic Media Classicに存在し、共通のリポジトリで管理することが重要でない場合は、Experience ManagerAssetsに書き出して配信用にDynamic Media Classicに同期するだけで済むのは、不要なラウンドトリップです。 それ以外の場合は、アセットを単一のリポジトリに保持し、配信用にDynamic Media Classicと同期することをお勧めします。

## Dynamic Media Classic統合の設定{#configuring-scene-integration}

Dynamic Media ClassicにアセットをアップロードするExperience Managerを設定できます。 CQターゲットフォルダーのアセットは、Experience ManagerからDynamic Media Classicの会社アカウントに（自動または手動で）アップロードできます。

>[!NOTE]
>
>Adobeでは、Dynamic Media Classicアセットの読み込みに、指定されたターゲットフォルダーのみを使用することをお勧めします。 ターゲットフォルダーの外部にあるデジタルアセットは、Dynamic Media Classic設定が有効になっているページのDynamic Media Classicコンポーネントでのみ使用できます。 さらに、Dynamic Media Classicのアドホックフォルダーに配置されます。 アドホックフォルダーはExperience Managerと同期されません(ただし、Dynamic Media Classicコンテンツブラウザーでアセットを検出できます)。

Dynamic Media ClassicをExperience Managerと統合するように設定するには、次の手順を実行する必要があります。

1. [クラウド設定の定義](#creating-a-cloud-configuration-for-scene)  - Dynamic Media ClassicフォルダーとAssetsフォルダーの間のマッピングを定義します。一方向(Dynamic Media ClassicへのExperience Managerアセット)の同期のみが必要な場合でも、この手順を実行します。
1. [ **Adobe CQ s7dam Dam Listener**](#enabling-the-adobe-cq-scene-dam-listener)  - OSGiconsoleで実行を有効にし  ます。
1. Experience ManagerアセットをDynamic Media Classicに自動的にアップロードする場合は、そのオプションをオンにし、[!UICONTROL DAMアセットの更新]ワークフローにDynamic Media Classicを追加する必要があります。 また、手動でアセットをアップロードできます。
1. Dynamic Media Classicコンポーネントをサイドキックに追加する。 この機能を使用すると、ユーザーはDynamic Media ClassicコンポーネントをExperience Managerページで使用できます。
1. [設定をExperience Managerのページにマッピング](#enabling-scene-for-wcm)  — この手順は、Dynamic Media Classicで作成したビデオプリセットを表示する場合に必要です。また、CQターゲットフォルダー外からDynamic Media Classicにアセットを公開する必要がある場合にも必要です。

ここでは、これらのすべての手順の実行方法を説明し、重要な制限を示します。

### Dynamic Media ClassicとExperience Managerアセット間の同期の仕組み{#how-synchronization-between-scene-and-aem-assets-works}

AssetsとDynamic Media Classicの同期を設定する場合は、次の点を理解することが重要です。

#### Dynamic Media AssetsからExperience ManagerClassicにアップロード{#uploading-to-scene-from-aem-assets}

* Dynamic Media Classicのアップロード用に、指定された同期Experience Managerーがあります。
* デジタルアセットが指定の同期フォルダーに配置されている場合は、Dynamic Media Classicへのアップロードを自動化できます。
* フォルダー内のフォルダーとサブExperience Managerーの構造がDynamic Media Classicにレプリケートされます。

>[!NOTE]
>
>Experience Managerは、Dynamic Media Classicにアップロードする前に、すべてのメタデータをXMPとして埋め込むので、メタデータノードのすべてのプロパティは、Dynamic Media ClassicでXMPとして使用できます。

#### Known limitations and design implications {#known-limitations-and-design-implications}

Experience ManagerAssetsとDynamic Media Classicの間の同期を使用すると、現在、制限/デザインに関して次のような影響があります。

<table>
 <tbody>
  <tr>
   <td><strong>制限／設計の意味</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>1つの指定された同期（ターゲット）フォルダー</td>
   <td>Dynamic Media Classicのアップロードでは、会社ごとに1つの指定Experience Managerーのみを使用できます。 Dynamic Media Classicの複数の会社アカウントへのアクセス権が必要な場合は、複数の設定を作成できます。</td>
  </tr>
  <tr>
   <td>フォルダー構造</td>
   <td>アセットを含む同期フォルダーを削除すると、Dynamic Media Classicのすべてのリモートアセットは削除されますが、フォルダーは残ります。</td>
  </tr>
  <tr>
   <td>アドホックフォルダー</td>
   <td>WCMでDynamic Media Classicに手動でアップロードしたターゲットフォルダーの外にあるアセットは、Dynamic Media Classicの別のアドホックフォルダーに自動的に配置されます。 このフォルダーは、クラウド設定の「Experience Manager」で設定します。</td>
  </tr>
  <tr>
   <td>混在メディア</td>
   <td>混在メディアセットはExperience Managerではサポートされていませんが、Experience Managerに表示されます。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>Dynamic Media ClassicのeCatalogから生成されたPDFは、CQターゲットフォルダーに読み込まれます。</td>
  </tr>
  <tr>
   <td>UI 更新</td>
   <td>Dynamic MediaとExperience Managerの間で同期を行う場合は、必ずユーザーインターフェイスを更新して変更を表示してください。 </td>
  </tr>
  <tr>
   <td>ビデオサムネール</td>
   <td>Dynamic Media Classicを使用したエンコーディング用にビデオをExperience ManagerAssetsにアップロードする場合、ビデオのサムネールとエンコードされたビデオがExperience ManagerAssetsで使用できるようになるまでに時間がかかることがあります。</td>
  </tr>
  <tr>
   <td>ターゲットサブフォルダー</td>
   <td><p>ターゲットフォルダー内でサブフォルダーを使用する場合は、（場所に関係なく）各アセットに一意の名前を使用するか、（「設定」領域で）Dynamic Media Classicを設定して、場所に関係なくアセットが上書きされないようにします。</p> <p>そうしないと、Dynamic Media Classicのターゲットサブフォルダーにアップロードされたのと同じ名前のアセットがアップロードされますが、ターゲットフォルダー内の同じ名前のアセットは削除されます。 </p> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media Classicサーバーの設定{#configuring-scene-servers}

プロキシの背後でExperience Managerを実行する場合、または特別なファイアウォール設定を持っている場合は、異なる地域のホストを明示的に有効にする必要があります。 サーバーは`/etc/cloudservices/scene7/endpoints`内のコンテンツで管理され、必要に応じてカスタマイズできます。 必要に応じて、URLをタップし、編集してURLを変更します。 以前のバージョンのExperience Managerでは、これらの値はハードコードされていました。

`/etc/cloudservices/scene7/endpoints.html`に移動すると、リストに表示されたサーバーが表示されます（URLをタップして編集できます）。

![chlimage_1-296](assets/chlimage_1-296.png)

### Dynamic Media Classicのクラウド設定の作成{#creating-a-cloud-configuration-for-scene}

クラウド設定では、Dynamic Media ClassicフォルダーとExperience ManagerAssetsフォルダーの間のマッピングを定義します。 Dynamic Media AssetsをExperience Manager Classicと同期するように設定する必要があります。 詳しくは、同期の仕組みを参照してください。

>[!CAUTION]
>
>既存のDynamic Media Classic会社アカウントからアセットを読み込むと、Experience Managerに表示されるのに長い時間がかかる場合があります。 Dynamic Media Classicで、アセットが多すぎないフォルダーを指定してください。 例えば、ルートフォルダーのアセットが多すぎる場合があります。
>
>統合をテストする場合は、ルートフォルダーが会社全体ではなく、サブフォルダーのみを指すようにします。

>[!NOTE]
>
>複数の設定を指定できます。1つのクラウド設定は、Dynamic Media Classicの会社の1人のユーザーを表します。 他のDynamic Media Classicの会社またはユーザーにアクセスする場合は、複数の設定を作成する必要があります。

Experience ManagerがDynamic Media Classicにアセットを公開できるように設定するには：

1. Experience Managerアイコンをタップし、**[!UICONTROL デプロイメント/Cloud Services]**&#x200B;に移動して、AdobeDynamic Media Classicにアクセスします。

1. 「**[!UICONTROL 今すぐ設定]**」をタップします。

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 「**[!UICONTROL タイトル]**」フィールド、およびオプションで「**[!UICONTROL 名前]**」フィールドで、適切な情報を入力します。「**[!UICONTROL 作成]**」をタップします。

   >[!NOTE]
   >
   >さらに多くの設定を作成する場合、**[!UICONTROL 親設定]**&#x200B;フィールドが表示されます。
   >
   >親設定は&#x200B;**変更しない**&#x200B;でください。親設定の変更は、統合を解除する可能性があります。

1. Dynamic Media Classicアカウントの電子メールアドレス、パスワード、地域を入力して、「**[!UICONTROL Dynamic Media Classicに接続]**」をタップします。 Dynamic Media Classicサーバーに接続すると、ダイアログが拡張され、追加のオプションが表示されます。

1. **[!UICONTROL 会社]**&#x200B;名と&#x200B;**[!UICONTROL ルートパス]**&#x200B;を入力します。 この情報は、公開されたサーバー名と、指定する任意のパスです。 公開先のサーバー名が不明な場合は、Dynamic Media Classicで、**[!UICONTROL 設定/アプリケーション設定]**&#x200B;に移動します。

   >[!NOTE]
   >
   >Dynamic Media Classicのルートパスは、Dynamic Media ClassicのフォルダーExperience Managerが接続する場所です。 特定のフォルダーに絞り込むことができます。

   >[!CAUTION]
   >
   >Dynamic Media Classicフォルダーのサイズによっては、ルートフォルダーの読み込みに時間がかかる場合があります。 また、Dynamic Media ClassicのデータがExperience Managerストレージを超える可能性があります。 正しいフォルダーを読み込んでいることを確認してください。読み込むデータが多すぎると、システムが停止する可能性があります。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 「**[!UICONTROL OK]**」をクリックします。Experience Managerは設定を保存します。

>[!NOTE]
>
>再接続する場合：
>
>* 公開時にDynamic Media Classicに再接続する場合、公開時または再接続時にパスワードをリセットしても機能しません（オーサーインスタンスの問題ではありません）。
>* 地域、会社名などの値を変更した場合は、Dynamic Media Classicに再接続する必要があります。 設定オプションが変更されているが保存されていない場合、Experience Managerは誤って設定が有効であることを示します。 必ず再接続するようにします。

>



### Adobe CQ Dynamic Media Classic Damリスナー{#enabling-the-adobe-cq-scene-dam-listener}を有効にする

Adobe CQ Dynamic Media Classic Dam Listenerを有効にします。このリスナーはデフォルトで無効になっています。

Adobe CQ Dynamic Media Classic Damリスナーを有効にするには：

1. [!UICONTROL ツール]アイコンをタップし、**[!UICONTROL 操作/Webコンソール]**&#x200B;に移動します。 Web コンソールが開きます。
1. **[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]**&#x200B;に移動し、「**[!UICONTROL 有効]**」チェックボックスをオンにします。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 「**[!UICONTROL 保存]**」をタップします。

### Dynamic Media Classicアップロードワークフロー{#adding-configurable-timeout-to-scene-upload-workflow}に設定可能なタイムアウトを追加しました

Dynamic Media Classicを使用してビデオエンコーディングを処理するようにExperience Managerインスタンスを設定した場合、デフォルトでは、アップロードジョブに35分のタイムアウトがあります。 長時間実行される可能性のあるビデオエンコーディングジョブに対応するために、次の設定を行うことができます。

1. **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**&#x200B;に移動します。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 「**[!UICONTROL Active job timeout]**」フィールドの数値を目的の値に変更します。負以外の数値であれば、任意の数値を指定できます。単位は秒です。デフォルトでは、この数値は2100に設定されています。

   >[!NOTE]
   >
   >ベストプラクティス：ほとんどのアセットが長くても数分以内に収集されます（画像など）。ただし、大きなビデオなどの場合は、処理時間が長くなるので、タイムアウト値を7200秒（2時間）に増やします。 それ以外の場合、このDynamic Media Classicアップロードジョブは、JCRメタデータで&#x200B;**[!UICONTROL UploadFailed]**&#x200B;とマークされます。

1. 「**[!UICONTROL 保存]**」をタップします。

### Experience Managerアセットからの自動アップロード{#autouploading-from-aem-assets}

Experience Manager6.3.2以降では、Experience ManagerがCQターゲットフォルダー内にある場合に、Asset ManagerにアップロードされたデジタルアセットがDynamic Media Classicに更新されるようにアセットが設定されます。

アセットがExperience Managerアセットに追加されると、Dynamic Media Classicに自動的にアップロードおよび公開されます。

>[!NOTE]
>
>Experience ManagerアセットからDynamic Media Classicに自動アップロードするファイルの最大サイズは500 MBです。

アセットからの自動アップロードをExperience Managerするには：

1. Experience Managerアイコンをタップして&#x200B;**[!UICONTROL デプロイメント/Cloud Services]**&#x200B;に移動し、Dynamic Media見出しの下の「利用可能な設定」で、「**[!UICONTROL dms7(Dynamic Media]**)」をタップします
1. 「**[!UICONTROL 詳細]**」タブをタップし、「**[!UICONTROL 自動アップロードを有効にする]**」チェックボックスを選択して、「**[!UICONTROL OK]**」をタップします。 次に、DAM Assetワークフローを設定して、Dynamic Media Classicへのアップロードを含める必要があります。

   >[!NOTE]
   >
   >非公開状態のDynamic Media Classicにアセットをプッシュする方法については、Dynamic Media Classicにプッシュされたアセットの状態（公開/非公開）の設定[を参照してください。](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Experience Managerのようこそページに戻り、「**[!UICONTROL ワークフロー]**」をタップします。 「**DAM アセットの更新**」ワークフローをダブルクリックして開きます。
1. サイドキックで、**[!UICONTROL Workflow]**&#x200B;コンポーネントに移動し、**[!UICONTROL Dynamic Media Classic]**&#x200B;を選択します。 **[!UICONTROL Dynamic Media Classic]**&#x200B;をワークフローにドラッグし、「**[!UICONTROL 保存]**」をタップします。 ターゲットフォルダー内のExperience Managerアセットに追加されたアセットは、Dynamic Media Classicに自動的にアップロードされます。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 自動化後にアセットを追加する場合、CQのターゲットフォルダーに配置されていない場合、Dynamic Media Classicにはアップロードされません。
   >* Experience Managerは、Dynamic Media Classicにアップロードする前に、すべてのメタデータをXMPとして埋め込むので、メタデータノードのすべてのプロパティは、Dynamic Media ClassicでXMPとして使用できます。


### Dynamic Media Classicにプッシュされたアセットの状態（公開/非公開）の設定{#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Experience ManagerアセットからDynamic Media Classicにアセットをプッシュする場合は、アセットを自動的に公開するか（デフォルトの動作）、非公開状態でDynamic Media Classicにプッシュできます。

運用を開始する前にステージング環境でテストする場合は、Dynamic Media Classicで直ちにアセットを公開しないでください。 Dynamic Media Classicのセキュアテスト環境でExperience Managerを使用して、AssetsからDynamic Media Classicに非公開の状態で直接アセットをプッシュできます。

Dynamic Media Classicアセットは、セキュアプレビューを使用して引き続き使用できます。 Dynamic Media Classicのアセットも実稼動環境でExperience Manager内で公開される場合にのみ有効です。

Dynamic Media Classicにアセットをプッシュする際に、すぐにアセットを公開する場合は、オプションを設定する必要はありません。 この機能はデフォルトの動作です。

ただし、Dynamic Media Classicにプッシュしたアセットを自動的に公開しない場合は、この機能を実行するようにExperience ManagerとDynamic Media Classicを設定する方法について説明します。

#### Dynamic Media Classicを非公開にするための前提条件{#prerequisites-to-push-assets-to-scene-unpublished}

公開せずにDynamic Media Classicにアセットをプッシュするには、次の設定を行う必要があります。

1. [「 」Admin Consoleを使用して、サポートケースを作成します](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)。サポートケースで、Dynamic Media Classicアカウントのセキュアプレビューの有効化をリクエストします。
1. [Dynamic Media Classicアカウントのセキュアプレビューの設定](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)の手順に従います。

これらの手順は、Dynamic Media Classicで安全なテスト設定を作成する場合と同じです。

>[!NOTE]
>
>インストール環境がUNIX® 64ビットオペレーティングシステムの場合、設定する必要がある他の設定オプションについては、 [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)を参照してください。

#### 非公開状態でのアセットのプッシュに関する既知の制限  {#known-limitations-for-pushing-assets-in-unpublished-state}

この機能を使用する場合は、次の制限事項に注意してください。

* バージョン管理のサポートはありません。
* アセットが既にExperience Managerで公開されていて、後続のバージョンが作成された場合は、その新しいバージョンが即座に実稼動環境に公開されます。 アクティベーションに対する公開は、アセットの最初の公開でのみ動作します。

>[!NOTE]
>
>アセットをすぐに公開する場合は、「**[!UICONTROL セキュアプレビューを有効にする]**」を「**[!UICONTROL 即時]**」に設定し、「**[!UICONTROL 自動アップロードを有効にする]**」機能を使用することをお勧めします。

### Dynamic Media Classicに非公開としてプッシュされたアセットの状態の設定{#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>ユーザーがExperience Managerでアセットを公開すると、S7アセットが実稼動/ライブアセットに自動的にトリガーされます（アセットは安全なプレビュー/非公開の状態ではなくなります）。

Dynamic Media Classicに非公開としてプッシュされるアセットの状態を設定するには：

1. Experience Managerアイコンをタップし、**[!UICONTROL デプロイメント/Cloud Services]**&#x200B;に移動し、**[!UICONTROL Dynamic Media Classic]**&#x200B;をタップして、Dynamic Media Classicで設定を選択します。
1. 「**[!UICONTROL 詳細]**」タブをタップします。**[!UICONTROL セキュアビューを有効にする]**&#x200B;ドロップダウンメニューで、「**[!UICONTROL AEM公開のアクティベーション時]**」を選択して、公開せずにDynamic Media Classicにアセットをプッシュします。 (デフォルトでは、この値は&#x200B;**[!UICONTROL 即時]**&#x200B;に設定され、Dynamic Media Classicアセットは直ちに公開されます)。

   アセットを公開する前のテストについて詳しくは、[Dynamic Media Classicのドキュメント](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)を参照してください。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 「**[!UICONTROL OK]**」をタップします。

セキュアプレビューを有効にすると、アセットが非公開のセキュアプレビューサーバーにプッシュされます。

セキュアプレビューが有効かどうかを確認するには、Experience Manager内のページ上のDynamic Media Classicコンポーネントに移動します。 「**[!UICONTROL 編集]**」をタップします。アセットのURLにセキュアプレビューサーバーが表示されます。 Experience Managerで公開すると、ファイル参照内のサーバードメインがプレビューURLから実稼動URLに更新されます。

### WCM用Dynamic Media Classicの有効化{#enabling-scene-for-wcm}

WCMに対するDynamic Media Classicの有効化は、次の2つの理由で必要です。

* これにより、ページオーサリング用のユニバーサルビデオプロファイルのドロップダウンリストが有効になります。 このリストがない場合、「**[!UICONTROL ユニバーサルビデオプリセット]**」ドロップダウンは空で、設定できません。
* デジタルアセットがターゲットフォルダーにない場合は、ページプロパティでそのページのDynamic Media Classicを有効にすると、そのアセットをDynamic Media Classicにアップロードできます。 次に、Dynamic Media Classicコンポーネントにアセットをドラッグ&amp;ドロップします。 通常の継承ルールが適用されます（子ページが親ページから設定を継承することを意味します）。

WCMに対してDynamic Media Classicを有効にする場合は、他の設定と同様に継承ルールが適用されます。 WCM用のDynamic Media Classicは、タッチ操作向けUIまたはクラシックUIで有効にできます。

#### タッチ操作向けUIでのWCM用Dynamic Media Classicの有効化{#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

タッチ操作向けUIでWCM用Dynamic Media Classicを有効にするには：

1. Experience Managerアイコンをタップし、「**[!UICONTROL Sites]**」に移動してから、Webサイトのルートページ（特定言語用ではない）に移動します。

1. ツールバーで[!UICONTROL 設定]アイコンを選択し、**[!UICONTROL プロパティを開く]**&#x200B;をタップします。

1. 「**[!UICONTROL Cloud Services]**」をタップし、「**[!UICONTROL 設定を追加]**」をタップして、「**[!UICONTROL Dynamic Media Classic]**」を選択します。
1. 「**[!UICONTROL Dynamic Media Classic]** Adobe」ドロップダウンリストで、目的の設定を選択して「**[!UICONTROL OK]**」をタップします。

   ![chlimage_1-303](assets/chlimage_1-303.png)

   Dynamic Media ClassicのExperience Managerのビデオプリセットは、そのページと子ページのDynamic Media Classicビデオコンポーネントとの設定で使用できます。

#### クラシックUIでのWCM用Dynamic Media Classicの有効化{#enabling-scene-for-wcm-in-the-classic-user-interface}

クラシックUIでWCM用Dynamic Media Classicを有効にするには：

1. Experience Managerで、「**[!UICONTROL Webサイト]**」をタップし、（特定の言語以外の）Webサイトのルートページに移動します。

1. サイドキックで、**[!UICONTROL ページ]**&#x200B;アイコンをタップし、**[!UICONTROL ページのプロパティ]**&#x200B;をタップします。

1. **[!UICONTROL Cloud Services/サービスを追加/ Dynamic Media Classic]**&#x200B;をタップします。
1. 「**[!UICONTROL Dynamic Media Classic]** Adobe」ドロップダウンリストで、目的の設定を選択して「**[!UICONTROL OK]**」をタップします。

   Dynamic Media ClassicのExperience Managerのビデオプリセットは、そのページと子ページのDynamic Media Classicビデオコンポーネントとの設定で使用できます。

### デフォルト設定の設定 {#configuring-a-default-configuration}

複数のDynamic Media Classic設定がある場合は、そのうちの1つをDynamic Media Classicコンテンツブラウザーのデフォルトとして指定できます。

一度に1つのDynamic Media Classic設定のみをデフォルトとして指定できます。 デフォルト設定は、Dynamic Media Classicコンテンツブラウザーにデフォルトで表示される会社アセットです。

デフォルト設定を設定するには：

1. Experience Managerアイコンをタップし、**[!UICONTROL デプロイメント/Cloud Services]**&#x200B;に移動し、**[!UICONTROL Dynamic Media Classic]**&#x200B;をタップして、Dynamic Media Classicで設定を選択します。
1. 設定を開くには、「**[!UICONTROL 編集]**」をタップします。

1. 「**[!UICONTROL 一般]**」タブで、「**[!UICONTROL デフォルト設定]**」チェックボックスをオンにして、Dynamic Media Classicコンテンツブラウザーに表示されるデフォルトの会社とルートパスにします。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >1 つの設定しかない場合、「**[!UICONTROL デフォルト設定]**」チェックボックスを選択しても、効果はありません。

### アドホックフォルダーの設定  {#configuring-the-ad-hoc-folder}

アセットがCQターゲットフォルダーにない場合に、Dynamic Media Classicでアセットのアップロード先のフォルダーを設定できます。 CQターゲットフォルダー外からのアセットの公開を参照してください。

アドホックフォルダーを設定するには：

1. Experience Managerアイコンをタップし、**[!UICONTROL デプロイメント/Cloud Services]**&#x200B;に移動し、**[!UICONTROL Dynamic Media Classic]**&#x200B;をタップして、Dynamic Media Classicで設定を選択します。
1. 設定を開くには、「**[!UICONTROL 編集]**」をタップします。

1. 「**[!UICONTROL 詳細]**」タブをタップします。「**[!UICONTROL アドホックフォルダー]**」フィールドで、**アドホック**&#x200B;フォルダーを変更できます。デフォルトでは、**name_of_the_company/CQ5_adhoc** です。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### ユニバーサルプリセットの設定 {#configuring-universal-presets}

ビデオコンポーネント用のユニバーサルプリセットを設定するには、[ビデオ](/help/assets/s7-video.md)を参照してください。

## MIMEタイプベースのAssets/Dynamic Media Classicアップロードジョブパラメーターサポートの有効化{#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Digital Asset Manager/Dynamic Media Classicアセットの同期でトリガーされる、設定可能なDynamic Media Classicアップロードジョブパラメーターを有効にできます。

特に、Experience ManagerWebコンソールの設定パネルの「OSGi(Open Service Gateway initiative)」領域で、MIMEタイプ別に受け入れられるファイル形式を設定します。 次に、JCR(Java™ Content Repository)のMIMEタイプごとに使用される個々のアップロードジョブパラメーターをカスタマイズできます。

**MIME タイプベースのアセットを有効にするには：**

1. Experience Managerアイコンをタップし、**[!UICONTROL ツール/運営/Webコンソール]**&#x200B;に移動します。
1. Adobe Experience Manager Webコンソールの設定パネルの&#x200B;**[!UICONTROL OSGi]**&#x200B;メニューで、「**[!UICONTROL 設定]**」をタップします。
1. 「名前」列で、**[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME type Service]**&#x200B;を探してタップし、設定を編集します。
1. 「MIMEタイプマッピング」領域で、任意のプラス記号(+)をタップして、MIMEタイプを追加します。

   [サポートされているMIMEタイプ](/help/assets/assets-formats.md#supported-mime-types)を参照してください。

1. テキストフィールドに、新しいMIMEタイプ名を入力します。

   例えば、`EPS=application/postscript` OR `PSD=image/vnd.adobe.photoshop`のように`<file_extension>=<mime_type>`と入力します。

1. 設定ウィンドウの右下隅の「**[!UICONTROL 保存]**」をタップします。
1. 「Experience Manager」に戻り、左側のレールで「CRXDE Lite」をタップします。
1. CRXDE Liteページの左側のレールで、`/etc/cloudservices/scene7/<environment>`に移動します（実際の名前は`<environment>`に置き換えます）。
1. `<environment>`（`<environment>`は実際の名前に置き換え）を展開して、`mimeTypes`ノードを表示します。
1. 追加したmimeTypeをタップします。

   例えば、`mimeTypes > application_postscript` OR `mimeTypes > image_vnd.adobe.photoshop`のように指定します。

1. CRXDE Lite ページの右側で、「**[!UICONTROL プロパティ]**」タブをタップします。
1. **[!UICONTROL jobParam]**&#x200B;値フィールドにDynamic Media Classicアップロードジョブパラメーターを指定します。

   例： `psprocess="rasterize"&psresolution=120` 。

   使用できるアップロードジョブパラメーターについて詳しくは、[AdobeDynamic Media Classic Image Production System API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html)を参照してください。

   >[!NOTE]
   >
   >PSDファイルをアップロードし、レイヤー抽出を使用してテンプレートとして処理する場合は、**[!UICONTROL jobParam]**&#x200B;値フィールドに次のように入力します。
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >PSDファイルに「レイヤー」が含まれていることを確認します。 厳密に1つの画像またはマスク付きの画像の場合、処理するレイヤーがないので、画像として処理されます。

1. CRXDE Lite ページの左上隅の「**[!UICONTROL すべて保存]**」をタップします。

## Dynamic Media ClassicとExperience Managerの統合のトラブルシューティング{#troubleshooting-scene-and-aem-integration}

Dynamic Media ClassicとのExperience Managerの統合で問題が発生した場合は、次のシナリオを参照してください。

**Dynamic Media Classicへのデジタルアセット公開に失敗する場合：**

* アップロードするアセットが&#x200B;**[!UICONTROL CQ target]**&#x200B;フォルダーにあることを確認します(このフォルダーはDynamic Media Classicクラウド設定で指定します)。
* そうでない場合は、そのページの&#x200B;**[!UICONTROL ページプロパティ]**&#x200B;でクラウド設定を設定し、**[!UICONTROL CQアドホック]**&#x200B;フォルダーへのアップロードを許可する必要があります。

* ログの情報を確認します。

**ビデオプリセットが表示されない場合：**

* **[!UICONTROL ページのプロパティ]**&#x200B;で、そのページのクラウド設定が設定されていることを確認します。ビデオプリセットは、Dynamic Media Classicビデオコンポーネントで使用できます。

**ビデオアセットがExperience Managerで再生されない場合：**

* 正しいビデオコンポーネントを使用していることを確認します。Dynamic Media Classicビデオコンポーネントは、基盤ビデオコンポーネントとは異なります。 [基盤ビデオコンポーネントとDynamic Media Classicビデオコンポーネント](/help/assets/s7-video.md)を参照してください。

**Experience Managerの新しいアセットや変更したアセットがDynamic Media Classicに自動的にアップロードされない場合：**

* アセットが CQ ターゲットフォルダーにあることを確認します。CQターゲットフォルダー内のExperience Managerのみが自動的に更新されます（アセットを自動的にアップロードするように設定されている場合）。
* 「自動アップロードを有効にするCloud Services」設定が完了していることと、DAM Assetワークフローを更新して保存し、Dynamic Media Classicのアップロードを含めていることを確認します。
* 画像をDynamic Media Classicターゲットフォルダーのサブフォルダーにアップロードする場合は、次のいずれかの操作を行ってください。

   * 場所に関係なく、すべてのアセットの名前が一意であることを確認します。そうしないと、メインターゲットフォルダーのアセットが削除され、サブフォルダーのアセットだけが残ります。
   * Dynamic Media Classicアカウントの「設定」領域で、Dynamic Media Classicによるアセットの上書き方法を変更します。 サブフォルダー内で同じ名前のアセットを使用する場合は、場所に関係なく、Dynamic Media Classicを設定してアセットを上書きしないでください。

**削除したアセットまたはフォルダーがDynamic Media ClassicとExperience Managerーの間で同期されない場合：**

* Experience Managerアセットで削除されたアセットとフォルダーは、Dynamic Media Classicの同期済みフォルダーに表示されます。 手動で削除します。

**ビデオのアップロードに失敗した場合**

* ビデオのアップロードに失敗し、Dynamic Media Classic統合を使用してExperience Managerを使用してビデオをエンコードする場合は、[Dynamic Media Classicアップロードワークフローへの設定可能なタイムアウトの追加](#adding-configurable-timeout-to-scene-upload-workflow)を参照してください。

>[!CAUTION]
>
>既存のDynamic Media Classic会社アカウントからアセットを読み込むと、Experience Managerに表示されるのに長い時間がかかる場合があります。 Dynamic Media Classicで、アセットが多すぎないフォルダーを指定してください。 例えば、ルートフォルダーのアセットが多すぎる場合があります。
>
>統合をテストする場合は、ルートフォルダーが会社全体ではなく、サブフォルダーのみを指すようにします。
