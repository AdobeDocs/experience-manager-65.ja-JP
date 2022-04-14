---
title: インタラクティブ画像
description: Dynamic Media でのインタラクティブ画像の使用方法について説明します。
uuid: 0bdb73f7-6ce9-4cdf-b6b5-a4d3d4e19a23
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: a6f58f6a-015a-4ced-941c-ef1b6d3e1d6f
docset: aem65
feature: Interactive Images
role: User, Admin
exl-id: 8a609024-e9e6-4805-8306-48d095110eb6
source-git-commit: 4b8369de9e6a10b73115d53358ce98729d92ed44
workflow-type: ht
source-wordcount: '4275'
ht-degree: 100%

---

# インタラクティブ画像{#interactive-images}

「ショッパブル」ホットスポットを画像にドラッグドロップすることで、静的な画像を、顧客にとってリッチで魅力的なエクスペリエンスに簡単に変えることができます。ショッパブルホットスポットは、製品やサービスに関する追加情報と、販売に直結する「買い物かごに追加」機能や「購入」機能を組み合わせています。ホットスポットを選択すると、製品またはサービスに直接リンクされ、その製品またはサービスが買い物かごに追加されるか、web ページにリンクされます。こうしたダイレクトなエクスペリエンスによって顧客のエンゲージメントが向上し、web サイトでのコンバージョン率が向上します。

次に、クイックビューポップアップを含むショッパブルバナーを示します。モデルの上の円（「ホットスポット」）を選択すると、クイックビューがアクティブになります。

![chlimage_1-152](assets/chlimage_1-368.png)

この web ページの実際のインタラクティブ画像は、次の URL から参照してください。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html?lang=ja)

## インタラクティブ画像バナーの作成方法をご覧ください。 {#watch-how-interactive-image-banners-are-created}

[インタラクティブ画像バナーの作成方法](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner)に関する説明を視聴します（10 分 33 秒）。このガイドでは、インタラクティブ画像バナーのプレビュー、編集、配信方法も説明します。

## クイックスタート：インタラクティブ画像 {#quick-start-interactive-images}

次のワークフローの手順説明は、Adobe Experience Manager Assets 内のインタラクティブ画像をすぐに使い始めることを目的としたものです。

一部のクイックスタートタスク内には「**例**」という見出しがあります。これには、まだインタラクティブ画像が追加されていない次のサンプル Web ページに基づく簡単なチュートリアルが含まれています。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=ja)

このチュートリアルでは、Web サイトにインタラクティブ画像を統合する手順が説明されています。

インタラクティブ画像の手順：

1. **（任意）ホットスポットの変数の識別** - Experience Manager Assets と Dynamic Media をスタンドアロンで使用している場合は、まず、既存のクイックビュー実装で使用されている動的変数を識別します。次に、インタラクティブ画像の作成時にホットスポットデータを入力します。[（任意）ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。
ただし、Adobe Experience Manager Sites もしくは Adobe Experience Manager eCommerce（またはその両方）を使用している場合、この手順は必要ありません。
[Experience Manager Assets の e コマースの概念](/help/commerce/cif-classic/administering/concepts.md)を参照してください。

1. **（任意）インタラクティブ画像ビューアープリセットの作成** - ホットスポットを表すために使用するグラフィック画像をカスタマイズします。独自のインタラクティブ画像ビューアプリセットの作成は、標準提供のインタラクティブ画像ビューアプリセット `Shoppable_Banner` を使用する場合には必要ありません。[（任意）インタラクティブ画像ビューアープリセットの作成](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset)を参照してください。

1. **画像バナーのアップロード** - インタラクティブにする画像バナーをアップロードします。
[画像バナーのアップロード](#uploading-an-image-banner)を参照してください。

1. **画像バナーへのホットスポットの追加** - 1 つ以上のホットスポットを画像バナーに追加し、それぞれにアクション（ハイパーリンク、クイックビュー、エクスペリエンスフラグメントなど）を関連付けます。ホットスポットを追加した後は、インタラクティブ画像を公開するとタスクが終了します。

   * [画像バナーへのホットスポットの追加](#adding-hotspots-to-an-image-banner)を参照してください。
   * [インタラクティブ画像のプレビュー](#optional-previewing-interactive-images)（任意）を参照してください。必要に応じて、ショッパブルバナーの表示を確認して、インタラクティビティをテストすることができます。
   * インタラクティブ画像アセットの公開方法について詳しくは、[アセットの公開](/help/assets/publishing-dynamicmedia-assets.md)を参照してください。

1. **Web サイトへのインタラクティブ画像の追加** - Experience Manager Sites、Experience Manager eCommerce、またはその両方を使用している場合は、Experience Managerで web ページにインタラクティブ画像を追加できます。インタラクティブメディアのコンポーネントを web ページにドラッグします。[ページへの Dynamic Media アセットの追加](/help/assets/adding-dynamic-media-assets-to-pages.md)を参照してください。

   Experience Manager Assets と Dynamic Media をスタンドアロンで使用している場合は、埋め込みコードを web サイトにコピーしてから、既存のクイックビューに統合する必要があります。[インタラクティブ画像の web サイトへの統合](#integrating-an-interactive-image-with-your-website)を参照してください。

   サードパーティの WCM（Web Content Manager）を使用している場合は、新しいインタラクティブビデオを、Web サイトで使用されている既存のクイックビュー実装に統合する必要があります。[インタラクティブ画像の既存のクイックビューへの統合](#integrating-an-interactive-image-with-an-existing-quickview)を参照してください。

## （オプション）ホットスポットの変数の識別 {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>このタスクが必要になるのは次に該当する場合のみです。
>
>* クイックビューをトリガーして、画像にインタラクティブ機能を追加する。
>* e コマースソリューション（IBM WebSphere® Commerce、Elastic Path、hybris、Intershop など）から Adobe Experience Manager に製品データを取り出すために、Adobe Experience Manager の実装が e コマース統合フレームワークを使用して&#x200B;*いない*。[Experience Manager Assetsの e コマースの概念](/help/commerce/cif-classic/administering/concepts.md)を参照してください。

>
>Experience Manager の実装で eCommerce を使用している場合は、このタスクをスキップして次のタスクに進みます。

まず、既存のクイックビュー実装で使用されている動的変数を識別します。こうすることで、ホットスポットデータを入力してインタラクティブ画像を作成できます。

Experience Manager Assets でバナー画像にホットスポットを追加する場合は、各ホットスポットに SKU（Stock Keeping Unit）と任意の追加変数を割り当てる必要があります。そのようなホットスポットの変数は、後でホットスポットとクイックビューコンテンツを対応付けるために使用されます。

重要なのは、ホットスポットデータに関連付けられる変数の数とタイプを正しく識別することです。バナー画像に追加するそれぞれのホットスポットに、既存のバックエンドシステム内で製品を一意に識別するための十分な情報がある必要があります。

ホットスポットデータに使用する一連の変数を識別するには、様々な方法があります。

既存のクイックビュー実装を担当している IT 担当者に問い合わせれば済む場合もあります。IT 担当者であれば、システムのクイックビューを識別するために必要な最小限のデータセットを把握している可能性が高いからです。ただし、フロントエンドコードの既存の動作を分析するだけでもかまいません。

ほとんどのクイックビュー実装では、次のような枠組みが使用されています。

* ユーザーは Web サイト上の特定のユーザーインターフェイス要素をアクティベートします。例えば、「クイックビュー」ボタンを選択します。
* Web サイトでは、必要に応じて、クイックビューのデータまたはコンテンツを読み込むための Ajax リクエストをバックエンドに送信します。
* クイックビューのデータは、Web ページでのレンダリングに備えて、コンテンツに変換されます。
* 最後に、フロントエンドコードによってそのコンテンツが画面上に視覚的にレンダリングされます。

次に、クイックビュー機能が実装されている既存の Web サイトの様々な領域を参照します。次に、クイックビューをトリガーし、web ページから送信された Ajax URL を取得して、クイックビューのデータまたはコンテンツを読み込みます。

通常、専門のデバッグツールを使用する必要はありません。最新の Web ブラウザーには、十分なタスクを実行できる Web インスペクターが備わっています。Web インスペクターが搭載されている Web ブラウザーの例を次に示します。

* Google Chrome で、ブラウザーから送信されるすべての HTTP リクエストを参照するには、F12 キーを押してデベロッパーツールパネルを開き、「Network」タブを選択します。Mac の場合、Command + Option + I キーを押してデベロッパーツールパネルを開き、「Network」タブを選択します。

* Firefox では、F12 キーを押して Firebug プラグインを有効にして「Net」タブを使用するか、組み込みの Inspector ツールとその「Network」タブを使用します。Mac の場合、Command + Option + I キーを押してデベロッパーツールパネルを開き、「Inspector」タブを選択します。

ブラウザーでネットワーク監視をオンにして、ページ上でクイックビューをトリガーします。

次に、ネットワークログ内でクイックビューの Ajax URL を見つけ、記録された URL を今後の分析のためにコピーします。通常、クイックビューをトリガーすると、多数のリクエストがサーバーに送信されます。クイックビューの Ajax URL は通常、そのリスト内の最初のほうにあります。この URL には複雑なクエリ文字列部分またはパスが含まれ、その応答の MIME タイプは `text/html`、`text/xml`、`text/javascript` のいずれかになります。

このプロセスの実行中は、製品カテゴリや製品タイプが異なる、Web サイトの様々な領域にアクセスすることが重要です。クイックビューの URL には、特定の web サイトカテゴリに共通するものの、web サイトの異なる領域にアクセスした場合にのみ変化する部分が存在するからです。

最も単純なケースでは、クイックビュー URL 内で変化する唯一の部分が製品 SKU となります。その場合、SKU の値が、ホットスポットをバナー画像に追加するために必要になる唯一のデータです。

一方、複雑なケースでは、クイックビューの URL に SKU 以外の様々な要素が含まれます（カテゴリ ID、カラーコード、サイズコードなど）。その場合、各要素は Experience Manager Assets のショッパブルインタラクティブ画像機能において、ホットスポットデータ定義内の個別の変数になります。

次のクイックビュー URL の例と、その結果となるホットスポットの変数について見てみましょう。

<table>
  <tbody>
  <tr>
    <td><p>単一の SKU（クエリ文字列内）</p> </td>
    <td><p>記録されたクイックビューの URL：</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>この URL で変化する唯一の部分は productId= というクエリ文字列パラメーターの値であり、これが SKU 値であることは明白です。したがって、ホットスポットでは、<strong><code>866558</code></strong>、<strong><code>1196184</code></strong>、<strong><code>1081492</code></strong>、<strong><code>1898294</code></strong> などの値が設定された SKU フィールドのみが必要になります。</p> </td>
  </tr>
  <tr>
    <td><p>単一の SKU（URL パス内）</p> </td>
    <td><p>記録されたクイックビューの URL：</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>パスの最後の要素が変化する部分であり、これがホットスポットの SKU 値（<strong><code>6422350843</code></strong>、<strong><code>1607745002</code></strong>、<strong><code>0086724882</code></strong>）になります。</p> </td>
  </tr>
  <tr>
    <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td>
    <td><p>記録されたクイックビューの URL：</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>この場合、URL には変化する部分が 2 つあります。SKU が <code>prodId</code> パラメーターに、カテゴリ ID<code></code> が <code>category=</code> パラメーターに格納されています。</p> <p>そのため、ホットスポット定義はペアになります。つまり、SKU 値と、<code>categoryId</code> という追加の変数です。結果のペアは次のようになります。</p>
    <ul>
      <li><p>SKU が <strong><code>305466</code></strong>、<code>categoryId</code> が <code>1100004</code>。</p> </li>
      <li><p>SKU が <strong><code>310181</code></strong>、<code>categoryId</code> が <strong><code>1100004</code></strong>。</p> </li>
      <li><p>SKU が <strong><code>308706</code></strong>、<code>categoryId</code> が <strong><code>1740148</code></strong>。</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**例**

この 3 つの例で使用されているものと同じアプローチを次のデモ Web ページに適用できます。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=ja)

このデモ Web ページにはいくつかの製品サムネールがあり、それぞれのサムネールには、「See More」というラベルの付いたクイックビューボタンが用意されています。Web ブラウザーのデバッグツールをアクティブにしたまま各ボタンを選択し、記録されたクイックビュー URL に注目してください。そのページの 4 つの製品クイックビューをすべてアクティベートすると、バックエンドに対して以下のリストのクイックビューリクエストが作成されます。

* `/datafeed/Male-Windbreaker.json`
* `/datafeed/Male-SimpleHenley.json`
* `/datafeed/Male-CamoPullover.json`
* `/datafeed/Female-QuiltedDownJacket.json`

これらのサーバーコールを見ると、製品固有の情報はリクエストパスにしか存在しないことがわかります。また、クエリ文字列がまったく使用されていないこと、2 つの異なるタイプのデータが含まれることもわかります。

* 最初のタイプは Male または Female です。これは「製品カテゴリ」と呼ばれます。
* 2 つ目のタイプは製品名（CamoPullover など）です。この情報は製品 SKU と考えることができます。

この情報に基づいて、全体的なクイックビュー URL は次のようなパターンであることがわかります。

`/datafeed/$categoryId$-$SKU$.json`

このような分析に基づいて、ホットスポットに対して `categoryId` と `SKU` を使用することになります。

これで、画像バナーをアップロードし、Experience Manager Assets のショッパブルインタラクティブ画像機能を使用して画像バナーにホットスポットを追加する準備ができました。

## （オプション）インタラクティブ画像ビューアプリセットの作成 {#optional-creating-an-interactive-image-viewer-preset}

Experience Manager Assets に含まれる、デフォルトの標準提供インタラクティブ画像ビューアプリセット（`Shoppable_Banner`）を使用するように選択できます。または、インタラクティブ画像で使用するために独自のカスタムビューアプリセットを作成できます。

カスタムインタラクティブ画像ビューアプリセットを作成する場合は、画像バナーのホットスポットの外観を決定できます。ビューアプリセットの作成中に、事前定義済みの画像ギャラリーからホットスポットのグラフィックを選択して使用できます。

ビューアプリセットを保存すると、Experience Manager Assets のビューアプリセットリストページで自動的にアクティベートされます（有効になります）。つまり、そのビューアプリセットは、インタラクティブメディアコンポーネントで、アセットを表示するときに常に表示されます。ただし、このビューアープリセットが設定されているインタラクティブバナーを&#x200B;*配信*&#x200B;するには、ビューアープリセットも&#x200B;*公開*&#x200B;する必要があります。このルールは、カスタムまたは初期設定のビューアプリセットに対して適用されます。

**インタラクティブ画像ビューアプリセットを作成するには：:**

1. 左パネルで、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL ビューアープリセット]**&#x200B;に移動します。
1. ページの右上隅付近にある「**[!UICONTROL 作成]**」を選択します。
1. 新規ビューアプリセットダイアログボックスで、インタラクティブバナービューアプリセットを表す名前を入力します。

   このタイトルは、保存後、ビューアープリセットリストページに表示されます。

1. 「リッチメディアタイプ」プルダウンメニューで、「**[!UICONTROL インタラクティブ画像]**」を選択します。
1. 「**[!UICONTROL 作成]**」を選択します。
1. ビューアープリセットを編集ページで、「**[!UICONTROL アピアランス]**」タブを選択します。
1. 次のいずれかの操作をおこないます。

   * 画像上で使用する独自のホットスポット画像をアップロードするには、アセットピッカーアイコンを選択します。コンテンツを選択ページで、使用するホットスポット画像の場所に移動して画像を選択し、右上隅のチェックマークアイコンを選択します。
   * 事前定義済みのホットスポット画像を選択するには、ホットスポットギャラリーアイコンを選択します。ホットスポットギャラリーパレットで、使用するホットスポット画像を選択します。

1. ページの右上隅にある「**[!UICONTROL 保存]**」を選択します。

   新しいビューアプリセットを忘れずに公開してください。

   [追加したビューアプリセットの公開](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)を参照してください。

   これで、画像バナーをアップロードできるようになりました。

## 画像バナーのアップロード {#uploading-an-image-banner}

使用する画像を既にアップロードしている場合は、次の手順（[画像バナーへのホットスポットの追加](#adding-hotspots-to-an-image-banner)）に進んでください。

**画像バナーをアップロードするには：:**

1. インタラクティブにする画像バナーをアップロードします。

   [アセットのアップロード](/help/assets/manage-assets.md#uploading-assets)を参照してください。

   これで、画像バナーにホットスポットを追加する準備が整いました。この後のタスクを参照してください。

## 画像バナーへのホットスポットの追加 {#adding-hotspots-to-an-image-banner}

ホットスポット管理ページのエディターを使用して、画像バナーにホットスポットを追加できます。

ホットスポットを追加する際に、クイックビューポップアップ表示、ハイパーリンクまたはエクスペリエンスフラグメントとして定義することができます。

[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)を参照してください。

>[!NOTE]
>
>ビューアをエクスペリエンスフラグメントに埋め込んだ場合、インタラクティブ画像のソーシャルメディア共有ツールはサポートされません。この問題を回避するには、ソーシャルメディアでの共有ツールを持たないビューアプリセットを使用または作成します。このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。

ページの右上隅にある「取り消し」および「やり直し」オプションは、現在の作成／編集セッションの間で有効です。

インタラクティブ画像の作成が完了したら、プレビューを使用して、インタラクティブ画像が顧客にどのように表示されるかを確認できます。

[（オプション）インタラクティブ画像のプレビュー](#optional-previewing-interactive-images)を参照してください。

>[!NOTE]
>
>インタラクティブ画像またはカルーセルバナー内の画像にホットスポットを追加すると、ホットスポット情報は同じメタデータの場所に保存されます。この場所は、インタラクティブ画像かカルーセルバナーかに関わらず、画像の場所に対して相対的な場所になります。つまり、どちらのビューアでも、同じ画像を、定義済みのホットスポットデータとともに簡単に再使用することができます。
カルーセルバナーは、画像上の画像マップ（ホットスポットを含むことができる）をサポートします。インタラクティブ画像はサポートしません。同じ画像を使用するインタラクティブ画像またはカルーセルバナーを作成する場合には、この点に注意してください。同じ画像の別々のコピーを使用してインタラクティブ画像とカルーセルバナーを作成することもできます。
[カルーセルバナー](/help/assets/carousel-banners.md)も参照してください。

>[!NOTE]
ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

**画像バナーにホットスポットを追加するには：:**

1. Assets ビューで、インタラクティブにする画像バナーに移動します。
1. 次のいずれかの操作を行います。

   * 画像の上にマウスポインターを置き、**[!UICONTROL 選択]**（チェックマークアイコン）を選択します。ツールバーの「**[!UICONTROL 編集]**」を選択します。

   * 画像の上にマウスポインターを置き、**[!UICONTROL その他のアクション]**（3 つのドットのアイコン）／**[!UICONTROL 編集]**&#x200B;を選択します。

   * 画像を選択して、詳細ビューページで開きます。 ツールバーの「**[!UICONTROL 編集]**」を選択します。

1. ページの左上隅にある「**[!UICONTROL ホットスポットを追加]**」（指先アイコン）を選択して、ホットスポット管理ページを開きます。
1. ページの左上隅にある「**[!UICONTROL ホットスポット]**」を選択します。

   1. ホットスポット管理ページの左上隅にある「**[!UICONTROL ホットスポット]**」を選択します。
   1. 画像上で、ホットスポットを表示する場所を選択します。必要に応じて、ホットスポットをドラッグして場所を調整します。
   1. 必要に応じて手順 a と b を繰り返し、他のホットスポットを追加します。
   1. （オプション）ホットスポットを削除するには、そのホットスポットを画像上で選択した後、「**[!UICONTROL ホットスポット]**」見出しの下にある&#x200B;**[!UICONTROL 削除]**（ごみ箱アイコン）を選択します。

1. 「名前」テキストフィールドにホットスポットの名前を入力します。この名前は、選択したホットスポットドロップダウンリストにも表示されます。
1. 次のいずれかの操作を行います。

   * 「**[!UICONTROL クイックビュー]**」を選択します。

      * Experience Manager Sites または AEM eCommerce のユーザーである場合は、製品ピッカーアイコン（虫眼鏡）を選択して、製品を選択ページを開きます。使用する製品を選択し、ページの右上隅にある「**[!UICONTROL 選択]**」を選択して、ホットスポット管理ページに戻ります。
      * Experience Manager Sites または e コマースのユーザー&#x200B;*ではない*&#x200B;場合は次のようにします。

         * [ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。これらの変数を定義する必要があります。
         * 次に、SKU 値を手動で入力します。「SKU 値」テキストフィールドに、製品の SKU（Stock Keeping Unit）を入力します。SKU は、提供している製品またはサービスごとの一意の識別子です。入力した SKU 値によってクイックビューテンプレートの変数部分が自動的に入力され、選択されたホットスポットが特定の SKU のクイックビューに関連付けられます。
         * （オプション）クイックビュー内で製品をさらに識別するために必要な他の変数がある場合は、「**[!UICONTROL 汎用変数を追加]**」を選択します。テキストフィールドに追加の変数を指定します。例えば、追加の変数として `category=Males` などと指定します。
   * 「**[!UICONTROL ハイパーリンク]**」を選択します。

      * Experience Manager Sites のユーザーである場合は、サイトセレクターアイコン（フォルダー）を選択して URL に移動します。インタラクティブコンテンツに相対 URL のリンク（特に Experience Manager Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。
      * スタンドアロンユーザーである場合は、「HREF」テキストフィールドに、リンクされる Web ページへの完全な URL パスを指定します。

   このリンクを新しいブラウザータブで開く（推奨のデフォルト）か同じタブで開くかを指定してください。

   詳しくは、[セレクターの操作](/help/assets/working-with-selectors.md)を参照してください。

   * 「**[!UICONTROL エクスペリエンスフラグメント]**」を選択します。

      * Adobe Experience Manager Sites のユーザーである場合は、検索アイコン（虫眼鏡）を選択してエクスペリエンスフラグメントページを開きます。使用するエクスペリエンスフラグメントを選択してからページ右上隅の「 **[!UICONTROL 選択]** 」を選択して、ホットスポット管理ページに戻ることができます。
[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)を参照してください。

      * エクスペリエンスフラグメントがバナーに表示されるときの幅と高さを指定します。

         >[!NOTE]
         ビューアをエクスペリエンスフラグメントに埋め込んだ場合、インタラクティブ画像のソーシャルメディア共有ツールはサポートされません。この問題を回避するには、ソーシャルメディアでの共有ツールを持たないビューアプリセットを使用または作成します。このようなビューアプリセットを使用すると、ビューアをエクスペリエンスフラグメントに正常に埋め込むことができます。



1. 「**[!UICONTROL 保存]**」を選択して作業内容を保存し、参照ページに戻ります。
1. インタラクティブ画像を公開します。公開すると、バナーをクラウドで配信できるようになり、サードパーティの web サイトに統合する必要がある場合は埋め込みコードが生成されます。

   [アセットの公開](/help/assets/manage-assets.md#publishing-assets)を参照してください。

   ホットスポットを追加してインタラクティブ画像を公開したら、次に既存の Web サイトにその画像を追加できます。

   [インタラクティブ画像の Web サイトへの統合](#integrating-an-interactive-image-with-your-website)を参照してください。

   >[!NOTE]
   ホットスポットを含むインタラクティブ画像を編集しているときに、画像を切り取ると、ホットスポットは削除されます。

### （オプション）インタラクティブ画像のプレビュー {#optional-previewing-interactive-images}

プレビューを使用して、顧客に対して示されるインタラクティブ画像の表示方法を確認し、画像のホットスポットをテストして動作が期待どおりであるかを確認することができます。

インタラクティブ画像の設定が完了したら、この画像を公開できます。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/embed-code.md)を参照してください。[Web アプリケーションへの URL のリンク](/help/assets/linking-urls-to-yourwebapplication.md)を参照してください。インタラクティブコンテンツに相対 URL のリンク（特に Experience Manager Sites ページへのリンク）がある場合、URL ベースのリンク方法は使用できません。[ページへの Dynamic Media アセットの追加](/help/assets/adding-dynamic-media-assets-to-pages.md)を参照してください。

**インタラクティブ画像をプレビューするには：:**

1. Assets ビューで、作成した既存のインタラクティブ画像の場所に移動し、選択してプレビューで表示します。
1. プレビューページの左上隅付近にある「コンテンツ」ドロップダウンリストで「**[!UICONTROL ビューアー]**」を選択します。
1. ビューアーリストで「**[!UICONTROL Shoppable_Banner]**」または作成したインタラクティブ画像ビューアープリセットの名前を選択します。
1. 画像上のホットスポットを選択します（関連するアクションをテストする場合）。

## インタラクティブ画像アセットの公開 {#publishing-interactive-image-assets}

インタラクティブ画像アセットの公開方法について詳しくは、[アセットの公開](/help/assets/publishing-dynamicmedia-assets.md)を参照してください。

## インタラクティブ画像の web サイトへの統合 {#integrating-an-interactive-image-with-your-website}

バナー画像をアップロードし、ホットスポットを画像に追加してインタラクティブ画像を公開したら、次に web サイトページにその画像を追加できます。

Experience Manager Sites の顧客である場合は、インタラクティブメディアコンポーネントをページにドラッグしてインタラクティブ画像を追加できます。[ページへの Dynamic Media アセットの追加](/help/assets/adding-dynamic-media-assets-to-pages.md)を参照してください。

スタンドアロンの Adobe Experience Manager Assets のユーザーは、この節で説明するようにインタラクティブ画像を手動で Web サイトに追加できます。

1. 公開済みのインタラクティブ画像の埋め込みコードをコピーします。[Web ページへのビデオビューアまたは画像ビューアの埋め込み](/help/assets/embed-code.md)を参照してください。

1. コピーした埋め込みコードを、Web ページ内の必要な場所に追加します。コピーされた埋め込みコードはレスポンシブ環境向けに設定されているので、追加された場所に自動的に適応します。

**例**

次のデモ Web サイトを例として使用します。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-0.html?lang=ja)

3 人の男性の写真には、以下のような静的 `IMG` タグが使用されています。

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

統合は、`IMG` タグを削除して Experience Manager Assets からコピーした埋め込みコードに置き換えるだけで簡単にできます。以下の URL を確認すると、ページ上に 3 つの円のホットスポットを伴うショッパブルインタラクティブ画像が表示されています。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-1.html?lang=ja)

>[!NOTE]
この時点では、デモ eb サイトのショッパブルインタラクティブ画像上のホットスポットは表示用のみで、まだ既存のクイックビューと統合されていません。

レスポンシブ環境用のショッパブルインタラクティブ画像に「crop（切り抜き）」を適用するには、パスにインタラクティブ画像設定属性 `ZoomView.iscommand` を含めます。コンポーネント `ZoomView` が呼び出され、`iscommand` は適用する「切り抜き」画像提供コマンドです。

[ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html?lang=ja) 設定属性を参照してください。

[crop](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html?lang=ja) 画像サービングコマンドを参照してください。

これで、インタラクティブ画像を Web サイト上の既存のクイックビューに統合できるようになりました。

## インタラクティブ画像の既存のクイックビューへの統合 {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
このタスクはスタンドアロン Adobe Experience Manager Assets のユーザーにのみ当てはまります。

このプロセスの最後の手順は、インタラクティブ画像を Web サイトの既存のクイックビュー実装に統合することです。すべてのケースで機能する統合のソリューションはありません。クイックビューの実装はそれぞれがユニークで、特定のアプローチが必要となります。フロントエンド IT 担当者の支援が必要になる可能性が高いです。

既存のクイックビュー実装は一般的に、Web ページ上で以下の順に発生する、相互に関連するアクションの連鎖となっています。

1. ユーザーは、Web サイトのユーザーインターフェイス内で、特定の要素を起動します。
1. フロントエンドコードは、手順 1 で起動されたユーザーインターフェイス要素に基づいてクイックビュー URL を取得します。
1. フロントエンドコードは、手順 2 で取得した URL を使用して Ajax リクエストを送信します。
1. バックエンドロジックは、対応するクイックビューのデータまたはコンテンツをフロントコードに送り返します。
1. フロントエンドコードは、そのクイックビューのデータまたはコンテンツを読み込みます。
1. （オプション）フロントエンドコードは、読み込んだクイックビューのデータを HTML 表現に変換します。
1. フロントエンドコードは、モーダルダイアログボックスまたはパネルを表示し、エンドユーザー向けに、画面上に HTML コンテンツをレンダリングします。

これらの呼び出しは、必ずしもそれぞれ独立した、Web ページのロジックから任意の手順で呼び出すことができるパブリックな API 呼び出しを表すわけではありません。むしろ、次の手順が前の手順の最後のフェーズ（コールバック）に隠されているような連鎖的な呼び出しになっています。

ショッパブルインタラクティブ画像が手順 1 と（部分的に）手順 2 を置き換えるのと同時に、ユーザーがショッパブル画像内のホットスポットを選択したときに、そのユーザー操作がビューアーによって処理されます。ビューアは、Adobe Experience Manager Assets に以前に追加されたすべてのサムネールデータを含む Web ページに、イベントを返します。

そのようなイベントハンドラーでは、フロントエンドコードは次の処理を実行します。

* ショッパブルインタラクティブ画像から送出されるイベントをリッスンします。
* ホットスポットデータに基づいてクイックビュー URL を作成します。
* バックエンドからクイックビューを読み込み、画面上の表示用にレンダリングするプロセスを起動します。

Experience Manager Assets によって返される埋め込みコードには、以下のハイライトされたコードのように、すぐに使用可能なイベントハンドラーがコメントアウトされた状態で既に含まれています。

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

従って必要な処理は、このコードのコメントアウトを解除し、ダミーのハンドラー本体を、特定の Web ページ専用のコードに置き換えることだけです。

クイックビュー URL の作成プロセスは、先ほど説明したホットスポットの変数を識別するためのプロセスとは逆のプロセスになります。

[ホットスポットの変数の識別](#optional-identifying-hotspot-variables)を参照してください。

以前のクイックビュー URL の例を使用した場合、クイックビュー URL の各ケースでの作成方法は次の例のようになります。

<table>
 <tbody>
  <tr>
   <td><p>単一の SKU（クエリ文字列内）</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>単一の SKU（URL パス内）</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU とカテゴリ ID（クエリ文字列内）</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

クイックビュー URL をトリガーしてクイックビューパネルをアクティベートするための最後の手順では、おそらく IT 部門のフロントエンド IT 担当者の支援が必要になります。フロントエンド IT 担当者は、すぐに使用できるクイックビュー URL を含め、クイックビュー実装を適切な手順から正しくトリガーするための最適な方法について理解しています。

これらの手順をデモ Web サイトに適用してショッパブルインタラクティブ画像をクイックビューのコードに統合する方法を確認できます。先ほど、クイックビュー URL の構造を次のように識別しました。

```xml
/datafeed/$categoryId$-$SKU$.json
```

この URL を `quickViewActivate` ハンドラー内で再構成するために、ビューアのコードからハンドラーに渡される `inData` オブジェクト内の `categoryId` フィールドと `SKU` フィールドを使用できます。

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

このデモ Web サイトは、単純な `loadQuickView()` 関数呼び出しを使用してクイックビューダイアログボックスを起動しています。この関数は、1 つの引数（クイックビューデータの URL）のみを受け取ります。したがって、ショッパブルインタラクティブ画像を統合するために必要な最後の手順は、`quickViewActivate` ハンドラーに次のコード行を追加することです。

```xml
loadQuickView(quickViewUrl);
```

次に、ソースコード全体を示します。

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

インタラクティブ画像が完全に統合された最終的なデモ Web サイトは次のようになります。

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html?lang=ja](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-banner/we-fashion/landing-3.html?lang=ja)

## クイックビューを使用したカスタムポップアップの作成 {#using-quickviews-to-create-custom-pop-ups}

[クイックビューを使用したカスタムポップアップの作成](/help/assets/custom-pop-ups.md)を参照してください。
