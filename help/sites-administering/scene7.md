---
title: Dynamic Media Classic（Scene7）との統合
seo-title: Dynamic Media Classic（Scene7）との統合
description: AEMをダイナミックメディアクラシックと統合する方法を説明します。
seo-description: AEMをダイナミックメディアクラシックと統合する方法を説明します。
uuid: b014d643-1cc1-47f3-a79c-7f6f9e45637a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: f55e68c3-3309-4400-bef9-fd3afa6e2b5f
translation-type: tm+mt
source-git-commit: e9c64d214456eed8e0adb29edd60c2350b852a67

---


# Dynamic Media Classic（Scene7）との統合{#integrating-with-dynamic-media-classic-scene}

[Adobe Dynamic Media Classicは](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) 、Web、モバイル、電子メールおよびインターネットに接続されたディスプレイや印刷でリッチメディアアセットを管理、拡張、公開、配信するためのホストソリューションです。

Dynamic Media Classicを使用するには、Dynamic Media ClassicとAEM Assetsが相互にやり取りできるようにクラウド設定を行う必要があります。 このドキュメントでは、AEMおよびダイナミックメディアクラシックの設定方法を説明します。

すべてのダイナミックメディアクラシックコンポーネントのページでの使用およびビデオの操作について詳しくは、ダイナミックメディアクラ [シックの使用を参照してくださ](../assets/scene7.md)い。

>[!NOTE]
>
>* Dynamic Media ClassicのDHTMLビューアプラットフォームは、2014年1月31日に正式に提供終了となりました。 詳しくは、[DHTML ビューアのサポート終了 FAQ](../sites-administering/dhtml-viewer-endoflifefaqs.md) を参照してください。
>* AEMで動作するようにDynamic Media Classicを設定する前に、「Dynamic Media ClassicとAEMを統 [合するためのベストプラクティス](#best-practices-for-integrating-scene-with-aem) 」を参照してください。
>* Dynamic Media Classicをカスタムプロキシ設定で使用する場合は、AEMの一部の機能で3.x APIを使用し、その他の機能で4.x APIを使用するので、両方のHTTPクライアントプロキシ設定を設定する必要があります。 3.x is configured with [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) and 4.x is configured with [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).
>



## AEM/Dynamic Media Classicの統合とダイナミックメディアの統合 {#aem-scene-integration-versus-dynamic-media}

AEMユーザーは、ダイナミックメディアを操作するための2つのソリューションの中から選択できます。AEMのインスタンスをDynamic Media Classicと統合するか、AEMに統合されたダイナミックメディアソリューションを使用します。

次の条件を使用して、どちらのソリューションを選択するかを決定します。

* If you are an **existing** Dynamic Media Classic customer whose rich media assets reside in Dynamic Media Classic for publishing and delivery, but you want to integrate those assets with Sites (WCM) authoring and/or AEM Assets for management, then use the [AEM/Dynamic Media Classic point-to-point integration](#aem-scene-point-to-point-integration) described in this document.

* リッチメディア配信を必要とする&#x200B;**新しい** AEM のお客様の場合、[ダイナミックメディアオプション](#aem-dynamic-media)を選択します。このオプションは、既存の S7 アカウントを持たず、システムに多くのアセットを保存している場合に最も有用です。

* 両方のソリューションを使用する必要がある場合もあります。The [dual-use scenario](/help/sites-administering/scene7.md#dual-use-scenario) describes that scenario.

### AEM/Dynamic Media Classicのポイントツーポイント統合 {#aem-scene-point-to-point-integration}

このソリューションのアセットを使用して作業する場合、次のいずれかの操作をおこないます。

* アセットを直接Dynamic Media Classicにアップロードし、 **Dynamic Media Classicコンテンツブラウザーを使用してアクセスして** 、ページオーサリングまたは
* Upload to AEM Assets and then enable automatic publishing to Dynamic Media Classic; you access via **Assets** content browser for page authoring

The components you use for this integration are found in the **Dynamic Media Classic** component area in [Design mode.](/help/sites-authoring/author-environment-tools.md#page-modes)

### AEM Dynamic Media {#aem-dynamic-media}

AEMダイナミックメディアは、AEMプラットフォーム内で直接Dynamic Media Classic機能を統合したものです。

このソリューションのアセットを使用して作業する場合、次のワークフローに従います。

1. 1 つの画像およびビデオアセットを直接 AEM にアップロードする。
1. AEM 内で直接ビデオをエンコードする。
1. AEM 内で画像ベースのセットを直接構築する。
1. 必要に応じて、画像やビデオにインタラクティブ機能を追加する。

ダイナミックメディア用に使用するコンポーネントは、**[!UICONTROL デザインモード]**&#x200B;の[ダイナミックメディア](/help/sites-authoring/author-environment-tools.md#page-modes)コンポーネント領域にあります。これらには、次が含まれます。

* **[!UICONTROL ダイナミックメディア]** - **[!UICONTROL ダイナミックメディア]**&#x200B;コンポーネントでは、追加しているアセットが画像であるかビデオであるかに応じて、様々なオプションを使用できます。このコンポーネントは画像プリセット、画像ベースのビューア（画像セット、スピンセット、混在メディアセットなど）およびビデオをサポートします。さらに、レスポンシブビューアであるので、ビューアのサイズは画面サイズに合わせて自動的に変化します。すべてのビューアは HTML5 ビューアです。

* **[!UICONTROL インタラクティブなメディア]** - **[!UICONTROL インタラクティブなメディア]**&#x200B;コンポーネントは、ホットスポットや画像マップなどのインタラクティブ機能が備わったカルーセルバナー、インタラクティブな画像、インタラクティブなビデオなどのアセットで使用します。このコンポーネントはスマートであり、追加しているアセットが画像であるかビデオであるかに応じて、様々なオプションを使用できます。さらに、レスポンシブビューアであるので、ビューアのサイズは画面サイズに合わせて自動的に変化します。すべてのビューアは HTML5 ビューアです。

### 両方を利用するシナリオ {#dual-use-scenario}

AEMのダイナミックメディアとダイナミックメディアクラシックの統合機能を同時に使用できます。 次の使用例の表で、特定の領域のオン/オフを切り替える場合について説明します。

ダイナミックメディアとダイナミックメディアクラシックを同時に使用するには：

1. クラウド [サービスで](#creating-a-cloud-configuration-for-scene) Dynamic Media Classicを設定します。
1. 次の中からお使いのユースケースに合致する手順を実行します。

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Dynamic Media Classicの統合</strong></td>
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
    <td>アセットを AEM にアップロードし、AEM ダイナミックメディアコンポーネントを使用して Sites ページにアセットを作成する</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td>
    <td>オフ</td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>小売業界で Sites とダイナミックメディアを初めて使用する</td>
    <td>商品以外のアセットは AEM にアップロードして管理および配信する。PRODUCTアセットをDynamic Media Classicにアップロードし、AEMおよびコンポーネントでDynamic Media Classicコンテンツブラウザーを使用して、サイトに製品の詳細ページをオーサリングします。</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>Assets とダイナミックメディアを初めて使用する</td>
    <td>アセットを AEM Assets にアップロードし、ダイナミックメディアで公開済み URL を使用またはコードを埋め込む</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td>オフ</td>
    <td>オフ</td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>ダイナミックメディアを使用して初めてテンプレートを作成する</td>
    <td>Dyamic Media を使用して画像とビデオを作成する。ダイナミックメディアクラシックで画像テンプレートを作成し、ダイナミックメディアクラシックコンテンツファインダーを使用して、サイトページにテンプレートを含めます。</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>既存のDynamic Media Classicのお客様で、Sitesを初めて使用する場合</td>
    <td>アセットをDynamic Media Classicにアップロードし、AEM Dynamic Media Classicコンテンツブラウザーを使用して、サイトページでアセットを検索およびオーサリングします</td>
    <td>オフ</td>
    <td>オフ</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>既存のDynamic Media Classicをご利用のお客様で、サイトとアセットを初めてお使いになる方</td>
    <td>DAMにアセットをアップロードし、自動的にDynamic Media Classicに公開して配信します。 AEM Dynamic Media Classicコンテンツブラウザーを使用して、サイトページ上のアセットを検索し、オーサリングします。</td>
    <td>オフ</td>
    <td>オフ</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">オン</a></p> <p>（手順 4 を参照）</p> </td>
    </tr>
    <tr>
    <td>既存のDynamic Media Classicをお使いの、アセットを初めて使用する場合</td>
    <td><p>アセットを AEM にアップロードし、ダイナミックメディアを使用してダウンロードや共有のレンディションを生成する。AEMアセットを自動的にダイナミックメディアクラシックに公開して配信します。</p> <p><strong></strong> 重要：AEMで生成された処理とレンディションの重複は、Dynamic Media Classicと同期されません</p> </td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td>オフ</td>
    <td>オフ</td>
    <td><p><a href="#configuringautouploadingfromaemassets">オン</a></p> <p>（手順 4 を参照）</p> </td>
    </tr>
    </tbody>
    </table>

1. (Optional; see use case table) - Set up the [Dynamic Media cloud configuration](/help/assets/config-dynamic.md) and [enable the Dynamic Media server](/help/assets/config-dynamic.md).
1. (オプション、使用例の表を参照)- 「アセットからダイナミックメディアクラシックへの自動アップロード」を有効にする場合は、次を追加する必要があります。

   1. Dynamic Media Classicへの自動アップロードの設定
   1. Dynamic Media Classicのアップロ **ード手順を******** Dam Update Assetワークフロー( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. (Optional) Restrict Dynamic Media Classic asset upload by MIME type in [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). このリストにないアセットのMIMEタイプは、Dynamic Media Classicサーバーにアップロードされません。
   1. （オプション）ビデオをダイナミックメディアクラシック設定で設定します。 ビデオエンコーディングは、ダイナミックメディアとダイナミックメディアクラシックのどちらかまたは両方に対して同時に有効にすることができます。 ダイナミックレンディションは、AEMインスタンスでのローカルでのプレビューと再生に使用されますが、ダイナミックメディアクラシックビデオレンディションは、Dynamic Media Classicサーバーで生成および保存されます。 When setting up video encoding services for both Dynamic Media and Dynamic Media Classic, apply a [video processing profile](/help/assets/video-profiles.md) to the Dynamic Media Classic asset folder.
   1. （オプション）ダ [イナミックメディアクラシックでセキュアプレビューを設定](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)。

#### 制限事項 {#limitations}

ダイナミックメディアクラシックとダイナミックメディアの両方を有効にしている場合、次の制限があります。

* AEMページ上でアセットを選択してDynamic Media Classicコンポーネントにドラッグして、手動でDynamic Media Classicにアップロードしても、機能しません。
* AEM-Dynamic Media Classicの同期アセットは、アセットでアセットを編集すると自動的にDynamic Media Classicに更新されますが、ロールバック操作では新しいアップロードがトリガーされないので、ロールバックの直後に最新バージョンを取得できません。 ロールバック完了後に再度編集する必要があります。
* ある使用例にダイナミックメディアを、別の使用例にダイナミックメディアクラシック統合を使用する必要がある場合、ダイナミックメディアクラシック設定をダイナミックメディアフォルダーに、またはダイナミックメディアクラシックフォルダーに適用しないでください。

## Dynamic Media ClassicとAEMの統合のベストプラクティス {#best-practices-for-integrating-scene-with-aem}

Dynamic Media ClassicをAEMと統合する場合、次の領域で確認する必要がある重要なベストプラクティスがいくつかあります。

* 統合のテストドライブ
* 特定のシナリオで推奨される、Dynamic Media Classicからアセットを直接アップロードする方法

既知の制 [限を参照](#known-limitations-and-design-implications)。

### 統合のテストドライブ {#test-driving-your-integration}

アドビでは、ルートフォルダーが会社全体ではなくサブフォルダーのみを参照するようにして、統合をテストドライブすることをお勧めします。

>[!CAUTION]
>
>既存のDynamic Media Classicの会社アカウントからアセットを読み込むと、AEMで表示されるまでに時間がかかる場合があります。 アセット数が多すぎない（例えば、ルートフォルダーのアセット数が多すぎる場合が多く、システムがクラッシュする場合がある）フォルダーをダイナミックメディアクラシックで指定します。

### AEM AssetsからのアセットのアップロードとDynamic Media Classicからのアセットのアップロード {#uploading-assets-from-aem-assets-versus-from-scene}

アセットは、アセット（デジタルアセット管理）機能を使用するか、Dynamic Media Classicコンテンツブラウザーを使用してAEMから直接Dynamic Media Classicにアクセスしてアップロードできます。 どちらを選択するかは、次の要素によって異なります。

* AEM AssetsでまだサポートされていないDynamic Media Classicアセットタイプは、Dynamic Media Classicから直接、例えば画像テンプレートを使用して、AEM webサイトに追加する必要があります。
* AEM AssetsとDynamic Media Classicの両方でサポートされるアセットタイプの場合、アセットタイプのアップロード方法は次のように決定します。

   * アセットが現在ある場所、および
   * 共有リポジトリでのそれらの管理の重要度

アセットが既にダイナミックメディアクラシックに存在し、共通リポジトリで管理することがそれほど重要でない場合は、アセットをAEM Assetsに書き出してDynamic Media Classicに同期して配信するだけで、不要なラウンドトリップが発生します。 それ以外の場合は、アセットを単一のリポジトリに保持し、配信目的でのみDynamic Media Classicと同期する方が望ましい場合があります。

## Configuring Dynamic Media Classic integration {#configuring-scene-integration}

AEMを設定して、Dynamic Media Classicにアセットをアップロードできます。 CQターゲットフォルダーのアセットは、AEMからDynamic Media Classicの会社アカウントに（自動または手動で）アップロードできます。

>[!NOTE]
>
>Dynamic Media Classicアセットの読み込みには、指定したターゲットフォルダーのみを使用することをお勧めします。 ターゲットフォルダーの外部にあるデジタルアセットは、ダイナミックメディアクラシック設定が有効になっているページのダイナミックメディアクラシックコンポーネントでのみ使用できます。 また、これらはDynamic Media Classicのアドホックフォルダーに配置されます。 アドホックフォルダーはAEMと同期されません（ただし、アセットはDynamic Media Classicコンテンツブラウザーで検出可能です）。

AEMと統合するようにDynamic Media Classicを設定するには、次の手順を実行する必要があります。

1. [クラウド設定の定義](#creating-a-cloud-configuration-for-scene) - Dynamic Media ClassicフォルダーとAssetsフォルダーの間のマッピングを定義します。 一方向（AEM Assetsからダイナミックメディアクラシック）同期のみが必要な場合でも、この手順を実行する必要があります。
1. [OSGiコンソ **ールでAdobe CQ s7dam Dam Listener **](#enabling-the-adobe-cq-scene-dam-listener)- Doneを有効に[!UICONTROL します]。
1. AEMアセットを自動的にダイナミックメディアクラシックにアップロードする場合は、このオプションをオンにして、DAMアセット更新ワークフローにダイナミックメディアクラシックを追加する必要があります。 また、手動でアセットをアップロードできます。
1. サイドキックへのDynamic Media Classicコンポーネントの追加 これにより、ユーザーはAEMページでダイナミックメディアクラシックコンポーネントを使用できます。
1. [AEMのページへの設定のマッピング](#enabling-scene-for-wcm) — この手順は、Dynamic Media Classicで作成したビデオプリセットを表示する場合に必要です。 また、CQターゲットフォルダー外からDynamic Media Classicにアセットを公開する必要がある場合にも必要です。

ここでは、これらのすべての手順の実行方法を説明し、重要な制限を示します。

### ダイナミックメディアクラシックとAEMアセット間の同期の仕組み {#how-synchronization-between-scene-and-aem-assets-works}

AEM Assetsとダイナミックメディアクラシック同期を設定する場合は、次の点を理解することが重要です。

#### AEM AssetsからDynamic Media Classicへのアップロード {#uploading-to-scene-from-aem-assets}

* AEMには、Dynamic Media Classicのアップロード用に指定された同期フォルダーがあります。
* デジタルアセットが指定された同期フォルダーに配置されている場合は、Dynamic Media Classicへのアップロードを自動化できます。
* AEMのフォルダーとサブフォルダーの構造は、Dynamic Media Classicで複製されます。

>[!NOTE]
>
>AEMは、すべてのメタデータをXMPとして埋め込んでからDynamic Media Classicにアップロードするので、メタデータノード上のすべてのプロパティは、Dynamic Media ClassicでXMPとして使用できます。

#### Known limitations and design implications {#known-limitations-and-design-implications}

AEM AssetsとDynamic Media Classicの間の同期では、現在、次の制限事項/デザイン上の影響があります。

<table>
 <tbody>
  <tr>
   <td><strong>制限／設計の意味</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>1つの指定された同期（ターゲット）フォルダ</td>
   <td>AEMでは、Dynamic Media Classicのアップロード用に会社ごとに1つのフォルダーのみを指定できます。 Dynamic Media Classicで複数の会社アカウントにアクセスする必要がある場合は、複数の設定を作成できます。</td>
  </tr>
  <tr>
   <td>フォルダー構造</td>
   <td>アセットを含む同期済みフォルダーを削除すると、すべてのDynamic Media Classicリモートアセットが削除されますが、フォルダーは残ります。</td>
  </tr>
  <tr>
   <td>アドホックフォルダー</td>
   <td>WCMのDynamic Media Classicに手動でアップロードしたターゲットフォルダー外のアセットは、Dynamic Media Classicの別のアドホックフォルダーに自動的に配置されます。 AEM のクラウド設定でこれを設定します。</td>
  </tr>
  <tr>
   <td>混在メディア</td>
   <td>混在メディアセットは、AEM ではサポートされませんが、AEM に表示されます。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>ダイナミックメディアクラシックのeCatalogから生成されたPDFは、CQターゲットフォルダーに読み込まれます。</td>
  </tr>
  <tr>
   <td>UI 更新</td>
   <td>AEMとDynamic Media Classicの間で同期を行う場合は、変更を表示するには、必ずユーザーインターフェイスを更新してください。 </td>
  </tr>
  <tr>
   <td>ビデオサムネール</td>
   <td>ビデオをAEM AssetsにアップロードしてDynamic Media Classic経由でエンコードする場合、ビデオの処理時間に応じて、ビデオサムネールとエンコードされたビデオがAEM Assetsで使用できるようになるまでに時間がかかる場合があります。</td>
  </tr>
  <tr>
   <td>ターゲットサブフォルダー</td>
   <td><p>ターゲットフォルダー内のサブフォルダーを使用する場合は、場所に関係なく、各アセットに一意の名前を使用するか、設定領域でDynamic Media Classicを設定して、場所に関係なくアセットが上書きされないようにします。</p> <p>それ以外の場合は、Dynamic Media Classicのターゲットサブフォルダーにアップロードされる同じ名前のアセットがアップロードされますが、ターゲットフォルダー内の同じ名前のアセットは削除されます。 </p> </td>
  </tr>
 </tbody>
</table>

### Configuring Dynamic Media Classic servers {#configuring-scene-servers}

プロキシの背後でAEMを実行する場合、または特別なファイアウォール設定を使用する場合は、異なる地域のホストを明示的に有効にする必要がある場合があります。 Servers are managed in content in `/etc/cloudservices/scene7/endpoints` and can be customized as required. 必要に応じて、URLをタップし、編集してURLを変更します。 AEM の以前のバージョンでは、これらの値はハードコードされていました。

If you navigate to `/etc/cloudservices/scene7/endpoints.html`, you see the servers listed (and can edit them by clicking on the URL):

![chlimage_1-296](assets/chlimage_1-296.png)

### Dynamic Media Classicのクラウド設定の作成 {#creating-a-cloud-configuration-for-scene}

クラウド設定は、ダイナミックメディアクラシックフォルダーとAEMアセットフォルダーの間のマッピングを定義します。 AEM AssetsをDynamic Media Classicと同期するように設定する必要があります。 詳しくは、同期の仕組みを参照してください。

>[!CAUTION]
>
>既存のDynamic Media Classicの会社アカウントからアセットを読み込むと、AEMで表示されるまでに時間がかかる場合があります。 アセット数が多すぎない（例えば、ルートフォルダーに含まれるアセット数が多すぎる）フォルダーをダイナミックメディアクラシックで指定します。
>
>統合をテストドライブしたい場合、会社全体ではなく、サブフォルダーのみを指すルートフォルダーを用意してもよいでしょう。

>[!NOTE]
>
>複数の設定を指定できます。クラウド設定の1つは、Dynamic Media Classicの会社の1人のユーザーを表します。 他のダイナミックメディアクラシックの会社またはユーザーにアクセスする場合は、複数の設定を作成する必要があります。

AEMがダイナミックメディアクラシックにアセットを公開できるように設定するには：

1. AEMアイコンをタップし、デプロイメ **[!UICONTROL ント/クラウドサービスに移動して]** 、Adobe Dynamic Media Classicにアクセスします。

1. 「今すぐ設 **[!UICONTROL 定」をタップしま]**&#x200B;す。

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 「**[!UICONTROL タイトル]**」フィールド、およびオプションで「**[!UICONTROL 名前]**」フィールドで、適切な情報を入力します。「**[!UICONTROL 作成]**」をタップします。

   >[!NOTE]
   >
   >追加の設定を作成する場合は、「**[!UICONTROL 親設定]**」フィールドが表示されます。
   >
   >親設定は&#x200B;**変更しない**&#x200B;でください。親設定の変更は、統合を解除する可能性があります。

1. Dynamic Media Classicアカウントの電子メールアドレス、パスワードおよび地域を入力し、「Dynamic Media Classic **[!UICONTROL に接続」をタップします]**。 Dynamic Media Classicサーバーに接続している場合は、ダイアログが展開され、その他のオプションが表示されます。

1. Enter the **[!UICONTROL Company]** name and **[!UICONTROL Root Path]** (this is the published server name together with any path you want to specify; if you do not know the published server name, in Dynamic Media Classic, go to **[!UICONTROL Setup > Application Setup]**.)

   >[!NOTE]
   >
   >ダイナミックメディアクラシックのルートパスは、AEMが接続するダイナミックメディアクラシックフォルダーです。 特定のフォルダーに絞り込むことができます。

   >[!CAUTION]
   >
   >ダイナミックメディアクラシックフォルダーのサイズによっては、ルートフォルダーの読み込みに時間がかかる場合があります。 また、ダイナミックメディアクラシックデータはAEMストレージを超える可能性があります。 正しいフォルダーを読み込んでいることを確認してください。読み込むデータが多すぎると、システムが停止する可能性があります。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 「**[!UICONTROL OK]**」をクリックします。AEM で設定が保存されます。

>[!NOTE]
>
>再接続する場合：
>
>* 公開時にDynamic Media Classicに再接続する場合、公開時にパスワードのリセットが必要になる場合や、再接続が機能しない場合があります。 これは、オーサーインスタンスの問題ではありません。
>* 地域や会社名などの値を変更した場合は、Dynamic Media Classicに再接続する必要があります。 設定オプションが変更されているが保存されていない場合、AEM は、設定が有効であると誤って示し続けます。必ず再接続するようにします。
>



### Adobe CQ Dynamic Media Classic Damリスナーの有効化 {#enabling-the-adobe-cq-scene-dam-listener}

Adobe CQ Dynamic Media Classic Dam Listenerを有効にする必要があります。この機能は、デフォルトで無効になっています。

有効にするには：

1. Tap the [!UICONTROL Tools] icon, then navigate to **[!UICONTROL Operations > Web Console]**. Web コンソールが開きます。
1. Navigate to **[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]** and select the **[!UICONTROL Enabled]** check box.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 「**[!UICONTROL 保存]**」をタップします。

### Dynamic Media Classicアップロードワークフローへの設定可能なタイムアウトの追加 {#adding-configurable-timeout-to-scene-upload-workflow}

Dynamic Media Classic（Scene7）を使用してビデオエンコーディングを処理するように AEM インスタンスが設定されている場合、アップロードジョブのタイムアウトはデフォルトで 35 分になります。ビデオエンコーディングジョブの実行時間がこれよりも長くなる可能性を考慮して、この設定を変更できます。

1. Navigate to **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 「**[!UICONTROL Active job timeout]**」フィールドの数値を目的の値に変更します。負以外の数値であれば、任意の数値を指定できます。単位は秒です。デフォルトでは 2100 に設定されています。

   >[!NOTE]
   >
   >ベストプラクティス：ほとんどのアセットが長くても数分以内に収集されます（画像など）。ただし、長編ビデオを扱う場合など、状況によっては、タイムアウト値を 7200 秒（2 時間）まで増やし、長い処理時間にも対応できるようにする必要があります。Otherwise, this Dynamic Media Classic upload job is marked as **[!UICONTROL UploadFailed]** in the JCR metadata.

1. 「**[!UICONTROL 保存]**」をタップします。

### AEM Assets からの自動アップロード {#autouploading-from-aem-assets}

AEM 6.3.2以降では、AEM Assetsが設定され、デジタルアセットマネージャーにアップロードするデジタルアセットがCQターゲットフォルダーにある場合は、自動的にDynamic Media Classicに更新されるようになりました。

アセットは、AEM Assetsに追加されると、自動的にアップロードされ、Dynamic Media Classicに公開されます。

>[!NOTE]
>
>AEM Assetsからダイナミックメディアクラシックに自動アップロードする場合の最大ファイルサイズは500 MBです。

AEM Assets からの自動アップロードを設定するには：

1. Tap the AEM icon and navigate to **[!UICONTROL Deployment > Cloud Services]** then, under the Dynamic Media heading, under Available Configurations, tap **[!UICONTROL dms7 (Dynamic Media]**)
1. Tap the **[!UICONTROL Advanced]** tab, select the **[!UICONTROL Enable Automatic Upload]** check box, then tap **[!UICONTROL OK]**. 次に、DAM Assetワークフローを設定して、Dynamic Media Classicへのアップロードを含める必要があります。

   >[!NOTE]
   >
   >See [Configuring the state (published/unpublished) of assets pushed to Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) for information on pushing assets to Dynamic Media Classic in an unpublished state.

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Navigate back to the AEM welcome page and tap **[!UICONTROL Workflows]**. 「**DAM アセットの更新**」ワークフローをダブルクリックして開きます。
1. In the sidekick, navigate to the **[!UICONTROL Workflow]** components, and select **[!UICONTROL Dynamic Media Classic]**. Dynamic Media Classicをワ **[!UICONTROL ークフローにドラッグし]** 、「保存」をタッ **[!UICONTROL プします]**。 ターゲットフォルダー内のAEMアセットに追加されたアセットは、自動的にDynamic Media Classicにアップロードされます。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 自動化後にアセットを追加する場合、アセットがCQターゲットフォルダーに配置されていないと、Dynamic Media Classicにアップロードされません。
   >* AEMは、すべてのメタデータをXMPとして埋め込んでからDynamic Media Classicにアップロードするので、メタデータノード上のすべてのプロパティは、Dynamic Media ClassicでXMPとして使用できます。


### Dynamic Media Classicにプッシュされるアセットの状態（公開済み/未公開）の設定 {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

AEM Assetsからダイナミックメディアクラシックにアセットをプッシュする場合は、アセットを自動的に公開するか（デフォルトの動作）、非公開状態のDynamic Media Classicにプッシュすることができます。

実稼働前にステージング環境でアセットをテストする場合は、アセットを直ちにダイナミックメディアクラシックに公開しないでください。 AEMをDynamic Media Classicのセキュアテスト環境と共に使用して、アセットを非公開状態で直接Dynamic Media Classicにプッシュすることができます。

ダイナミックMedia Classicアセットは、セキュアプレビューで引き続き使用できます。 AEM内でアセットが公開された場合にのみ、ダイナミックメディアクラシックアセットも実稼働環境に移行します。

アセットをダイナミックメディアクラシックにプッシュしたときにすぐに公開する場合は、オプションを設定する必要はありません。 これはデフォルトの動作です。

ただし、Dynamic Media Classicにプッシュされたアセットを自動的に公開しないようにする場合は、AEMおよびDynamic Media Classicで自動公開を設定する方法について説明します。

#### 非公開のDynamic Media Classicにアセットをプッシュするための前提条件 {#prerequisites-to-push-assets-to-scene-unpublished}

アセットを公開せずにダイナミックメディアクラシックにプッシュするには、次の設定を行う必要があります。

1. Dynamic Media Classicアカウントのセキュアプレビューを有効にするには、Dynamic Media Classicカスタマーケア(s7support@adobe.com)にお問い合わせください。
1. Follow directions to [setup secure preview for your Dynamic Media Classic account.](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

以下の手順は、Dynamic Media Classicで安全なテスト設定を作成する場合と同じです。

>[!NOTE]
>
>If your installation environment is a Unix 64-bit operating system, see [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) regarding additional configuration options you need to set.

#### 非公開状態でのアセットのプッシュに関する既知の制限  {#known-limitations-for-pushing-assets-in-unpublished-state}

この機能を使用する場合、次の制限に注意してください。

* バージョン管理のサポートはありません。
* アセットが既に AEM で公開されていて、後続バージョンが作成されている場合、その新しいバージョンは、即座に実稼動環境に公開されます。アクティベーションに対する公開は、アセットの最初の公開でのみ動作します。

>[!NOTE]
>
>If you want to publish assets instantly, best practice is to keep **[!UICONTROL Enable Secure Preview]** set to **[!UICONTROL Immediately]** and use the **[!UICONTROL Enable Automatic Upload]** feature.

### Dynamic Media Classicにプッシュされたアセットの状態を非公開に設定 {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>ユーザーが AEM でアセットを公開する場合、S7 アセットが実稼動／ライブアセットに自動的にトリガーされます（そのアセットは、セキュアプレビュー／非公開ではなくなります）。

Dynamic Media Classicにプッシュされるアセットの状態を非公開に設定するには：

1. AEMアイコンをタップし、デプロイメ **[!UICONTROL ント/クラウドサービスに移動し、]**「ダイナミックメディアクラシ **[!UICONTROL ック]**」をタップし、Dynamic Media Classicで設定を選択します。
1. 「**[!UICONTROL 詳細]**」タブをタップします。In the **[!UICONTROL Enable Secure View]** drop-down menu, select **[!UICONTROL Upon AEM Publish Activation]** to push assets to Dynamic Media Classic without publishing. (By default, this value is set to **[!UICONTROL Immediately]**, where Dynamic Media Classic assets are published immediately.)

   See [Dynamic Media Classic documentation](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html) for more information on testing assets before making them public.

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 「**[!UICONTROL OK]**」をタップします。

「セキュアビューを有効にする」は、アセットが非公開のセキュアプレビューサーバーにプッシュされることを意味します。

You can check this by navigating to a Dynamic Media Classic component on a page in AEM and tapping **[!UICONTROL Edit]**. アセットには、セキュアプレビューサーバーが URL にリストされます。AEM で公開したら、ファイル参照のサーバードメインは、プレビュー URL から実稼動 URL にアップロードされます。

### WCM用のDynamic Media Classicの有効化 {#enabling-scene-for-wcm}

WCMに対してDynamic Media Classicを有効にする必要があるのは、次の2つの理由によります。

* ページオーサリング用のユニバーサルビデオプロファイルのドロップダウンリストを有効にするため。Without this, the **[!UICONTROL Universal Video Preset]** drop-down is empty and cannot be set.
* デジタルアセットがターゲットフォルダーにない場合は、ページプロパティでそのページに対してダイナミックメディアクラシックを有効にし、そのアセットをダイナミックメディアクラシックコンポーネントにドラッグ&amp;ドロップすると、そのアセットをダイナミックメディアクラシックにアップロードできます。 通常の継承ルールが適用されます（つまり、子ページがその親ページから設定を継承します）。

WCMに対してDynamic Media Classicを有効にする場合、他の設定と同様に継承ルールが適用されます。 WCM用のダイナミックメディアクラシックは、タッチ操作向けまたはクラシックユーザーインターフェイスで有効にできます。

#### タッチ操作向けユーザーインターフェイスでのWCM用のDynamic Media Classicの有効化 {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

タッチ操作向けUIでWCMに対してDynamic Media Classicを有効にするには：

1. Tap the AEM icon and navigate to **[!UICONTROL Sites]** and then the root page of your web site (not language specific).

1. In the toolbar, select the [!UICONTROL settings] icon and tap **[!UICONTROL Open Properties]**.

1. 「クラウ **[!UICONTROL ドサービス]** 」をタップ **[!UICONTROL し、「設定を追加]** 」をタップし **[!UICONTROL て、「Dynamic Media Classic」を選択します]**。
1. 「 **[!UICONTROL Adobe Dynamic Media Classic]** 」ドロップダウンリストで、必要な設定を選択し、「 **[!UICONTROL OK」をタップします]**。

   ![chlimage_1-303](assets/chlimage_1-303.png)

   その設定のDynamic Media Classicのビデオプリセットは、そのページと子ページにあるDynamic Media Classicビデオコンポーネントを含むAEMで使用できます。

#### クラシックユーザーインターフェイスでのWCM用のDynamic Media Classicの有効化 {#enabling-scene-for-wcm-in-the-classic-user-interface}

クラシックUIでWCMに対してダイナミックメディアクラシックを有効にするには：

1. In AEM, tap **[!UICONTROL Websites]** and navigate to the root page of your web site (not language specific).

1. In the sidekick, tap the **[!UICONTROL Page]** icon and tap **[!UICONTROL Page Properties]**.

1. クラウ **[!UICONTROL ドサービス/サービスを追加/Dynamic Media Classicをタップします]**。
1. 「 **[!UICONTROL Adobe Dynamic Media Classic]** 」ドロップダウンリストで、必要な設定を選択し、「 **[!UICONTROL OK」をタップします]**。

   その設定のDynamic Media Classicのビデオプリセットは、そのページと子ページにあるDynamic Media Classicビデオコンポーネントを含むAEMで使用できます。

### デフォルト設定の設定 {#configuring-a-default-configuration}

複数のダイナミックメディアクラシック設定がある場合は、いずれかの設定をダイナミックメディアクラシックコンテンツブラウザーのデフォルトとして指定できます。

特定の時点で、デフォルトとしてマークできるDynamic Media Classic設定は1つだけです。 デフォルト設定は、ダイナミックメディアクラシックコンテンツブラウザーにデフォルトで表示される会社アセットです。

デフォルト設定を設定するには：

1. AEMアイコンをタップし、デプロイメ **[!UICONTROL ント/クラウドサービスに移動し、]**「ダイナミックメディアクラシ **[!UICONTROL ック]**」をタップし、Dynamic Media Classicで設定を選択します。
1. Tap **[!UICONTROL Edit]** to open the configuration.

1. In the **[!UICONTROL General]** tab, select the **[!UICONTROL Default Configuration]** check box to make this the default company and root path that appears in the Dynamic Media Classic content browser.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >1 つの設定しかない場合、「**[!UICONTROL デフォルト設定]**」チェックボックスを選択しても、効果はありません。

### アドホックフォルダーの設定 {#configuring-the-ad-hoc-folder}

アセットがCQターゲットフォルダーにない場合に、アセットのアップロード先フォルダーをDynamic Media Classicで設定できます。 詳しくは、CQターゲットフォルダー外からのアセットの公開を参照してください。

アドホックフォルダーを設定するには：

1. AEMアイコンをタップし、デプロイメ **[!UICONTROL ント/クラウドサービスに移動し、]**「ダイナミックメディアクラシ **[!UICONTROL ック]**」をタップし、Dynamic Media Classicで設定を選択します。
1. Tap **[!UICONTROL Edit]** to open the configuration.

1. 「**[!UICONTROL 詳細]**」タブをタップします。「**[!UICONTROL アドホックフォルダー]**」フィールドで、**アドホック**&#x200B;フォルダーを変更できます。デフォルトでは、**name_of_the_company/CQ5_adhoc** です。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### ユニバーサルプリセットの設定 {#configuring-universal-presets}

ビデオコンポーネント用のユニバーサルプリセットを設定するには、[ビデオ](/help/assets/s7-video.md)を参照してください。

## MIMEタイプベースのAssets/Dynamic Media Classicアップロードジョブパラメーターのサポートの有効化 {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Digital Asset Manager/Dynamic Media Classicアセットの同期によってトリガーされる、設定可能なDynamic Media Classicアップロードジョブのパラメーターを有効にすることができます。

特に、AEM Web コンソール設定パネルの OSGi（Open Service Gateway initiative）領域にある MIME タイプで、受け入れられるファイル形式を設定します。次に、JCR(Java Content Repository)の各MIMEタイプに使用する個々のアップロードジョブのパラメータをカスタマイズできます。

**MIME タイプベースのアセットを有効にするには：**

1. Tap the AEM icon and navigate to **[!UICONTROL Tools > Operations > Web Console]**.
1. In the Adobe Experience Manager Web Console Configuration panel, on the **[!UICONTROL OSGi]** menu, tap **[!UICONTROL Configuration]**.
1. Under the Name column, find and tap **[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME type Service]** to edit the configuration.
1. 「MIMEタイプのマッピング」領域で、任意のプラス記号(+)をタップしてMIMEタイプを追加します。

   See [Supported MIME types](/help/assets/assets-formats.md#supported-mime-types).

1. テキストフィールドに、新しいMIMEタイプ名を入力します。

   例えば、ORで「a」と入 `<file_extension>=<mime_type>` 力し `EPS=application/postscript` ます `PSD=image/vnd.adobe.photoshop`。

1. 設定ウィンドウの右下隅の「**[!UICONTROL 保存]**」をタップします。
1. AEM に戻り、左側のレールで、CRXDE Lite をタップします。
1. On the CRXDE Lite page, in the left rail, navigate to `/etc/cloudservices/scene7/<environment>` (substitute `<environment>` for the actual name).
1. Expand `<environment>` (substitute `<environment>` for the actual name) to reveal the `mimeTypes` node.
1. 先ほど追加したmimeTypeをタップします。

   For example, `mimeTypes > application_postscript` OR `mimeTypes > image_vnd.adobe.photoshop`.

1. CRXDE Lite ページの右側で、「**[!UICONTROL プロパティ]**」タブをタップします。
1. Specify a Dynamic Media Classic upload job parameter in the **[!UICONTROL jobParam]** value field.

   For example, `psprocess="rasterize"&psresolution=120` .

   See the [Adobe Dynamic Media Classic Image Production System API](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/) for additional upload job parameters you can use.

   >[!NOTE]
   >
   >PSDファイルをアップロードし、レイヤー抽出を使用してテンプレートとして処理する場合は、jobParam **** valueフィールドに次のように入力します。
   >
   >`process=MaintainLayers&createTemplate=true`
   >
   >PSDファイルに「レイヤー」が含まれていることを確認します。厳密に1つの画像、またはマスクを含む画像の場合、処理するレイヤーがないので、画像として処理されます。

1. CRXDE Lite ページの左上隅の「**[!UICONTROL すべて保存]**」をタップします。

## Dynamic Media ClassicとAEMの統合のトラブルシューティング {#troubleshooting-scene-and-aem-integration}

AEMとDynamic Media Classicの統合で問題が発生する場合は、次の解決策のシナリオを参照してください。

**Dynamic Media Classicへのデジタルアセットの公開に失敗した場合：**

* アップロードしようとしているアセットが **[!UICONTROL CQターゲットフォルダー内にあることを確認します]** （このフォルダーは、Dynamic Media Classicクラウド設定で指定します）。
* ない場合、**[!UICONTROL CQ アドホックフォルダー]**&#x200B;にアップロードできるように、そのページの&#x200B;**[!UICONTROL ページプロパティ]**&#x200B;でクラウド設定を設定する必要があります。

* ログの情報を確認します。

**ビデオプリセットが表示されない場合：**

* **[!UICONTROL ページのプロパティ]**&#x200B;で、そのページのクラウド設定が設定されていることを確認します。ビデオプリセットは、Dynamic Media Classicビデオコンポーネントで使用できます。

**AEM でビデオアセットが再生されない場合：**

* 正しいビデオコンポーネントを使用していることを確認します。ダイナミックMedia Classicビデオコンポーネントは、基礎ビデオコンポーネントとは異なります。 Foundationビデオコン [ポーネントとDynamic Media Classicビデオコンポーネントを参照してください](/help/assets/s7-video.md)。

**AEMで新規または変更されたアセットがDynamic Media Classicに自動的にアップロードされない場合：**

* アセットが CQ ターゲットフォルダーにあることを確認します。CQ ターゲットフォルダーにあるアセットだけが自動的に更新されます（アセットを自動的にアップロードするように AEM Assets を設定した場合）。
* 「自動アップロードを有効にする」にクラウドサービスの設定が完了していること、およびDAM Assetワークフローが更新され、保存されていることを確認してください。
* 画像をDynamic Media Classicのターゲットフォルダーのサブフォルダーにアップロードする場合は、次のいずれかの操作を行います。

   * 場所に関係なく、すべてのアセットの名前が一意であることを確認します。そうしないと、メインターゲットフォルダーのアセットが削除され、サブフォルダーのアセットだけが残ります。
   * Dynamic Media Classicアカウントの「設定」領域で、Dynamic Media Classicがアセットを上書きする方法を変更します。 サブフォルダー内で同じ名前のアセットを使用する場合、場所に関係なくアセットを上書きするようにDynamic Media Classicを設定しないでください。

**削除したアセットまたはフォルダーがDynamic Media ClassicとAEMの間で同期されない場合：**

* AEM Assetsで削除されたアセットとフォルダーは、Dynamic Media Classicの同期フォルダーに引き続き表示されます。 それらを手動で削除する必要があります。

**ビデオのアップロードに失敗した場合**

* If your video upload fails and you are using AEM to encode video through the Dynamic Media Classic integration, see [Adding configurable timeout to Dynamic Media Classic Upload workflow](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>既存のDynamic Media Classicの会社アカウントからアセットを読み込むと、AEMで表示されるまでに時間がかかる場合があります。 アセット数が多すぎない（例えば、ルートフォルダーに含まれるアセット数が多すぎる）フォルダーをダイナミックメディアクラシックで指定します。
>
>統合をテストドライブしたい場合、会社全体ではなく、サブフォルダーのみを指すルートフォルダーを用意してもよいでしょう。

