---
title: ページへのDynamic Media Classic機能の追加
description: Adobe Experience ManagerのページにDynamic Media Classicの機能とコンポーネントを追加する方法。
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: User, Admin
mini-toc-levels: 3
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: d947bd98b3a0f6fd79cde5b5b2fca23487077da3
workflow-type: tm+mt
source-wordcount: '2845'
ht-degree: 22%

---

# ページへのDynamic Media Classic機能の追加 {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) は、リッチメディアアセットを管理、強化、公開、および Web、モバイル、電子メール、インターネットに接続されたディスプレイと印刷できるようにする、ホストソリューションです。

Dynamic Media Classicで公開されたExperience Managerアセットは、様々なビューアで表示できます。

* ズーム
* フライアウト
* ビデオ
* 画像テンプレート
* 画像

デジタルアセットをExperience ManagerからDynamic Media Classicに直接公開したり、Dynamic Media ClassicからExperience Managerに公開したりできます。

このドキュメントでは、デジタルアセットをExperience ManagerからDynamic Media Classicに公開する方法と、その逆の方法について説明します。 また、ビューアについても詳しく説明します。Dynamic Media Classic用のExperience Managerの設定について詳しくは、 [Dynamic Media ClassicとExperience Managerの統合](/help/sites-administering/scene7.md).

関連トピック [画像マップを追加](image-maps.md).

ビデオコンポーネントをExperience Managerで使用する方法について詳しくは、 [ビデオ](video.md).

>[!NOTE]
>
>Dynamic Media Classicのアセットが正しく表示されない場合は、Dynamic Mediaが [無効](config-dynamic.md#disabling-dynamic-media) ページを更新します。

## アセットからDynamic Media Classicへの手動公開 {#manually-publishing-to-scene-from-assets}

デジタルアセットは、次の手順でDynamic Media Classicに公開できます。

* [クラシック UI を使用して Assets コンソールから](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [クラシック UI を使用してアセットから](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [CQ Target フォルダーの外側からクラシックユーザーインターフェイスを表示する場合](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>Experience ManagerはDynamic Media Classicに非同期で公開します。 次を選択した後： **[!UICONTROL 公開]**( アセットがDynamic Media Classicに公開されるまで数秒かかります )。

## Dynamic Media Classicコンポーネント {#scene-components}

次のDynamic Media ClassicコンポーネントをExperience Managerで使用できます。

* ズーム
* フライアウト（ズーム）
* 画像テンプレート
* 画像
* ビデオ

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できないので、で選択する必要があります。 **[!UICONTROL デザイン]** モードを使用してください。

これらが **[!UICONTROL デザイン]** モードでは、他のExperience Managerコンポーネントと同様に、コンポーネントをページに追加できます。 まだDynamic Media Classicに公開されていないアセットは、同期済みフォルダー内、ページ上、またはDynamic Media Classicクラウド設定を使用している場合、Dynamic Media Classicに公開されます。

>[!NOTE]
>
>カスタムビューアを作成および開発し、コンテンツファインダーを使用する場合は、 `allowfullscreen` パラメーター。

### Flash ビューアのサポート終了に関する通知 {#flash-viewers-end-of-life-notice}

Adobe Dynamic Media Classicは、2017 年 1 月 31 日にFlashビューアプラットフォームのサポートを終了しました。

### ページへのDynamic Media Classic(Scene7) コンポーネントの追加 {#adding-a-scene-component-to-a-page}

Dynamic Media Classic(Scene7) コンポーネントをページに追加する操作は、任意のページにコンポーネントを追加する操作と同じです。 Dynamic Media Classicコンポーネントについて、以降の節で詳しく説明します。

**Dynamic Media Classic(Scene7) コンポーネントをページに追加するには：**

1. Experience Managerで、 **[!UICONTROL Dynamic Media Classic(Scene7)]** コンポーネント。

1. 使用できるDynamic Media Classicコンポーネントがない場合は、「 **[!UICONTROL デザイン]** モードで、青い境界線の付いた任意のコンポーネントを選択し、 **[!UICONTROL 親]** アイコン、 **[!UICONTROL 設定]** アイコン In **[!UICONTROL Parsys （デザイン）]**&#x200B;をクリックし、すべてのDynamic Media Classicコンポーネントを選択して使用可能にし、「 」を選択します。 **[!UICONTROL OK]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. 選択 **[!UICONTROL 編集]** 次に戻る **[!UICONTROL 編集]** モード。

1. サイドキックのDynamic Media Classicグループからページの目的の場所にコンポーネントをドラッグします。

1. を選択します。 **[!UICONTROL 設定]** アイコンをクリックして、コンポーネントを開くことができます。

1. 必要に応じてコンポーネントを編集し、「 」を選択します。 **[!UICONTROL OK]** 変更を保存します。
1. 画像またはビデオをコンテンツブラウザーからページに追加したDynamic Media Classicコンポーネントにドラッグします。

   >[!NOTE]
   >
   >タッチ UI のみで、画像またはビデオをページに配置したDynamic Media Classicコンポーネントにドラッグ&amp;ドロップする必要があります。 Dynamic Media Classicコンポーネントの選択と編集の後でのアセットの選択はサポートされていません。

### レスポンシブサイトにインタラクティブな表示エクスペリエンスを追加する {#adding-interactive-viewing-experiences-to-a-responsive-website}

アセットのレスポンシブデザインとは、アセットが表示される場所に応じて適応することを意味します。 レスポンシブデザインを使用すると、同じアセットを複数のデバイスで効果的に表示できます。

関連トピック [Web ページのレスポンシブデザイン](/help/sites-developing/responsive.md).

**レスポンシブサイトにインタラクティブな表示エクスペリエンスを追加するには：**

1. Experience Managerにログインし、 [設定済みのAdobe Dynamic Media ClassicCloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) Dynamic Media Classicコンポーネントを使用できます。

   >[!NOTE]
   >
   >Dynamic Media Classicコンポーネントを使用できない場合は、 [デザインモードで有効にするには](/help/sites-authoring/default-components-designmode.md).

1. Web サイト内の **[!UICONTROL Dynamic Media Classic]** 有効なコンポーネント、ドラッグ **[!UICONTROL 画像]** コンポーネントをページに追加します。
1. コンポーネントを選択し、設定アイコンを選択します。
1. 内 **[!UICONTROL Dynamic Media Classic Settings]** タブで、ブレークポイントを調整します。

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. ビューアがレスポンシブにサイズ変更され、すべてのインタラクションがデスクトップ、タブレットおよびモバイル用に最適化されていることを確認します。

### すべてのDynamic Media Classicコンポーネントに共通の設定 {#settings-common-to-all-scene-components}

設定オプションは異なりますが、次の操作はすべての [!UICONTROL Dynamic Media Classic] コンポーネント：

* **[!UICONTROL ファイル参照]**- 参照するファイルを探します。ファイル参照は、アセット URL を表示しますが、必ずしも URL コマンドやパラメーターを含む完全なDynamic Media Classic URL ではありません。 このフィールドにDynamic Media Classic URL のコマンドとパラメーターを追加することはできません。 代わりに、コンポーネントの対応する機能を使用して追加します。
* **[!UICONTROL 幅]** - 幅を設定できます。
* **[!UICONTROL 高さ]** - 高さを設定できます。

これらの設定オプションを設定するには、例えば、Dynamic Media Classicコンポーネントを開く（ダブルクリックする）と、 **[!UICONTROL ズーム]** コンポーネント：

![chlimage_1-226](assets/chlimage_1-226.png)

### ズーム {#zoom}

HTML5 ズームコンポーネントで、 **[!UICONTROL +]** 」ボタンをクリックします。

アセットの下部にはズームツールが用意されています。選択 **[!UICONTROL +]** もし拡大したければ選択 **[!UICONTROL -]** を減らしたい場合は、をクリックします。 次をタップ **[!UICONTROL x]** または「ズームをリセット」矢印を使用すると、画像は読み込み時の元のサイズに戻ります。 斜めの矢印を選択して、全画面表示にします。 選択 **[!UICONTROL 編集]** コンポーネントを設定できます。 このコンポーネントを使用すると、 [すべての [!UICONTROL Dynamic Media Classic] コンポーネント](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### フライアウト {#flyout}

HTML5 **[!UICONTROL フライアウト]** コンポーネントの場合、アセットは分割画面で表示されます。アセットを指定されたサイズで残し、ズーム部分の右側が表示されます。 選択 **[!UICONTROL 編集]** コンポーネントを設定できます。 このコンポーネントを使用すると、 [すべてのDynamic Media Classicコンポーネントに共通の設定](#settings-common-to-all-scene-components).

>[!NOTE]
>
>次に、 **[!UICONTROL フライアウト]** コンポーネントでカスタムサイズが使用され、そのカスタムサイズが使用されて、コンポーネントのレスポンシブ設定が無効になります。
>
>次に、 **[!UICONTROL フライアウト]** コンポーネントは、で設定されたデフォルトのサイズを使用します **[!UICONTROL デザインビュー]**&#x200B;を指定した場合は、デフォルトのサイズが使用され、コンポーネントが拡大され、コンポーネントのレスポンシブ設定が有効なページレイアウトサイズに合わせて調整されます。 コンポーネントのレスポンシブ設定には制限があります。 を使用する場合、 **[!UICONTROL フライアウト]** レスポンシブ設定のコンポーネント。フルページで拡大して使用しないでください。 それ以外の場合は、 **[!UICONTROL フライアウト]** は、ページの右の境界線を越えて拡張されています。

![chlimage_1-228](assets/chlimage_1-228.png)

### 画像 {#image}

ザDynamic Media Classic **[!UICONTROL 画像]** コンポーネントを使用すると、Dynamic Media Classicの修飾子、画像またはビューアプリセット、シャープニングなどのDynamic Media Classic機能を画像に追加できます。 ザDynamic Media Classic **[!UICONTROL 画像]** コンポーネントは、Dynamic Media Classicの特別な機能を備えた、Experience Manager内の他の画像コンポーネントと似ています。 この例では、画像にDynamic Media Classic URL 修飾子が含まれています。 `&op_invert=1` 適用済み

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL タイトル、代替テキスト]**  — 内 **[!UICONTROL 詳細]** 「 」タブで、グラフィックの表示をオフにしているユーザー向けのタイトルと代替テキストを画像に追加します。

**[!UICONTROL URL、で開く]**  — からアセットを設定して、リンクを開くことができます。 「**[!UICONTROL URL]**」と「**[!UICONTROL 次のウィンドウで開く]**」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL ビューアプリセット]**  — ドロップダウンメニューから既存のビューアプリセットを選択します。 探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットを管理する](/help/assets/managing-viewer-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL Dynamic Media Classic Configuration]** - SPS からアクティブな画像プリセットを取得するために使用するDynamic Media Classic設定を選択します。

**[!UICONTROL 画像プリセット]**  — ドロップダウンメニューから既存の画像プリセットを選択します。 探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、 [画像プリセットを管理](/help/assets/managing-image-presets.md). 画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL 出力形式]**  — 画像の出力形式（例：jpeg）を選択します。 選択した出力形式に応じて、追加の設定オプションがあります。 [画像プリセットのベストプラクティス](/help/assets/managing-image-presets.md#image-preset-options)を参照してください。

**[!UICONTROL シャープ]**  — 画像にシャープを適用する方法を選択します。 シャープニングについて詳しくは、[画像プリセットのベストプラクティス](/help/assets/managing-image-presets.md#image-preset-options)および[シャープニングのベストプラクティス](/help/assets/assets/sharpening_images.pdf)を参照してください。

**[!UICONTROL URL 修飾子]**  — 追加のDynamic Media Classic画像コマンドを指定して、画像エフェクトを変更できます。 これらのコマンドについては、 [画像プリセット](/help/assets/managing-image-presets.md) そして [コマンドリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL ブレークポイント]** - Web サイトがレスポンシブな場合は、ブレークポイントを調整する必要があります。 ブレークポイントはコンマ（,）で区切って指定してください。

### 画像テンプレート {#image-template}

[Dynamic Media Classic画像テンプレート](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) は、Dynamic Media Classicに読み込まれたPhotoshopコンテンツに重ね合わされ、可変性を考慮してコンテンツとプロパティがパラメーター化されました。 この **[!UICONTROL 画像テンプレート]** コンポーネントを使用すると、画像を読み込み、Experience Managerでテキストを動的に変更できます。 また、ClientContext の値を使用するように&#x200B;**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを設定できます。これにより、各ユーザーが個別に画像を活用できます。

選択 **[!UICONTROL 編集]** コンポーネントを設定する場合。 次の項目を設定できます。 [すべてのDynamic Media Classicコンポーネントに共通の設定](#settings-common-to-all-scene-components) およびこの節で説明するその他の設定

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL ファイル参照、幅、高さ]**  — すべての ScDynamic Media Classicene7 コンポーネントに共通の設定を参照してください。

>[!NOTE]
>
>Dynamic Media Classic URL のコマンドとパラメーターをファイル参照 URL に直接追加することはできません。 これらは、**[!UICONTROL パラメーター]**&#x200B;パネルのコンポーネントの UI でのみ定義できます。

**[!UICONTROL タイトル、代替テキスト]** - 「 Dynamic Media Classic画像テンプレート」タブで、グラフィックの表示をオフにしているユーザー向けのタイトルと代替テキストを画像に追加します。

**[!UICONTROL URL、で開く]**  — からアセットを設定して、リンクを開くことができます。 「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL パラメータパネル]**  — 画像をインポートする際に、パラメーターには画像からの情報が事前に入力されます。 動的に変更できるコンテンツがない場合、このウィンドウは空になります。

![chlimage_1-233](assets/chlimage_1-233.png)

#### テキストを動的に変更 {#changing-text-dynamically}

テキストを動的に変更するには、フィールドに新しいテキストを入力し、「 」を選択します。 **[!UICONTROL OK]**. この例では、「**[!UICONTROL 価格]**」が $50 で、送料が 99 セントです。

![chlimage_1-234](assets/chlimage_1-234.png)

画像内のテキストが変更されます。をタップして、テキストを元の値に戻すことができます。 **[!UICONTROL リセット]** をクリックします。

![chlimage_1-235](assets/chlimage_1-235.png)

#### ClientContext 値の値を反映するようにテキストを変更 {#changing-text-to-reflect-the-value-of-a-client-context-value}

フィールドを ClientContext の値にリンクするには、 **[!UICONTROL 選択]** client-context メニューを開くには、clientcontext を選択し、「 **[!UICONTROL OK]**. この例では、「名前」フィールドとプロファイル内の書式設定された名前とのリンクに基づいて名前が変わります。

![chlimage_1-236](assets/chlimage_1-236.png)

現在ログインしているユーザーの名前がテキストに反映されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-237](assets/chlimage_1-237.png)

#### Dynamic Media Classic画像テンプレートをリンクにする {#making-the-scene-image-template-a-link}

1. Dynamic Media Classicを含むページ上 **[!UICONTROL 画像テンプレート]** コンポーネント、選択 **[!UICONTROL 編集]**.
1. 内 **[!UICONTROL URL]** 「 」フィールドに、画像がタップされたときの移動先 URL を入力します。 「**[!UICONTROL 次のウィンドウで開く]**」フィールドで、ターゲットを新しいウィンドウと同じウィンドウのどちらで開くかを選択します。

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 「**[!UICONTROL OK]**」を選択します。

### ビデオコンポーネント {#video-component}

ザDynamic Media Classic **[!UICONTROL ビデオ]** ( サイドキックの「Dynamic Media Classic」セクションから利用可能な ) コンポーネントは、デバイスと帯域幅の検出を使用して、適切なビデオを各画面に表示します。 このコンポーネントは HTML5 ビデオプレーヤー（チャネルを超えて使用可能な単一のビューア）です。

このコンポーネントはアダプティブビデオセット（単一の MP4 ビデオまたは単一の F4V ビデオ）で使用できます。

詳しくは、 [ビデオ](s7-video.md) ビデオとDynamic Media Classicの統合の連携について詳しくは、こちらを参照してください。 また、 [Dynamic Media Classicビデオコンポーネントと基盤ビデオコンポーネントの比較](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### ビデオコンポーネントの既知の制限事項 {#known-limitations-for-the-video-component}

AdobeDAM と WCM に、プライマリソースビデオがアップロードされたかどうかを示します。 次に示すプロキシアセットは表示されません。

* Dynamic Media Classicエンコードされたレンディション
* Dynamic Media Classicアダプティブビデオセット

Dynamic Media Classicビデオコンポーネントでアダプティブビデオセットを使用する場合、ビデオのサイズに合うようにコンポーネントのサイズを変更する必要があります。

## Dynamic Media Classic Content Browser {#scene-content-browser}

Dynamic Media Classicのコンテンツブラウザーを使用すると、Dynamic Media Classicのコンテンツを直接Experience Managerで表示できます。 コンテンツブラウザーにアクセスするには、 **[!UICONTROL コンテンツファインダー]**&#x200B;を選択します。 **[!UICONTROL Dynamic Media Classic]** （タッチ操作向け UI）または **[!UICONTROL S7]** アイコンをクリックします。 どちらの UI を使用しても機能は同じです。

複数の設定がある場合、Experience Managerにはデフォルトで「 [デフォルト設定](/help/sites-administering/scene7.md#configuring-a-default-configuration). 様々な設定を、Dynamic Media Classicコンテンツブラウザーのドロップダウンメニューで直接選択できます。

>[!NOTE]
>
>* オンデマンドフォルダー内のアセットは、Dynamic Media Classicコンテンツブラウザーに表示されません。
>* 条件 [プレビューの保護が有効になっています](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)に設定されている場合、Dynamic Media Classic上の公開済みアセットと未公開アセットの両方がDynamic Media Classicコンテンツブラウザーに表示されます。
>* 表示されない **[!UICONTROL Dynamic Media Classic]** または **[!UICONTROL S7]** アイコンをコンテンツブラウザーのオプションとして使用する場合は、 [Dynamic Media ClassicをExperience Managerと連携するように設定](/help/sites-administering/scene7.md).
>* ビデオの場合、Dynamic Media Classicコンテンツブラウザーは次の機能をサポートしています。
   >
   >   * アダプティブビデオセット：複数の画面でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
   >   * 単一の MP4 ビデオ
   >   * 単一の F4V ビデオ


### タッチ操作向け UI でコンテンツを参照する {#browsing-content-in-the-touch-optimized-ui}

タッチ対応 UI またはクラシック UI を使用してコンテンツブラウザーにアクセスできます。現時点では、タッチ対応 UI には次の制限事項があります。

* Dynamic Media Classicの FXG およびFlashアセットはサポートされていません。

選択によるDynamic Media Classicアセットの参照 **[!UICONTROL Dynamic Media Classic]** 3 番目のドロップダウンメニューから。 Dynamic Media Classic/Experience Managerの統合を設定していない場合、Dynamic Media Classicはリストに表示されません。

>[!NOTE]
>
>* Dynamic Media Classicコンテンツブラウザーは、約 100 個のアセットを読み込み、名前順に並べ替えます。
>* セキュアなプレビューサーバーが設定されている場合、ブラウザーはそのプレビューサーバーを使用してサムネールとアセットをレンダリングします。

>


![chlimage_1-240](assets/chlimage_1-240.png)

また、ブラウザー内でアセットの上にマウスポインターを置くと、解像度の情報、サイズ、変更後の日数およびファイル名を参照できます。

![chlimage_1-241](assets/chlimage_1-241.png)

* アダプティブビデオセットとテンプレートの場合は、サムネール用のサイズ情報が生成されません。
* アダプティブビデオセットの場合は、サムネール用の解像度が生成されません。

### コンテンツブラウザーでのDynamic Media Classicアセットの検索 {#searching-for-scene-assets-with-the-content-browser}

Dynamic Media Classicでのアセットの検索は、Experience Manager Assetsでのアセットの検索と似ています。 ただし、検索時に、実際にはDynamic Media Classicシステム内のアセットのリモート表示が表示されます。アセットを直接Experience Managerに読み込むのではありません。

クラシック UI またはタッチ操作向け UI を使用して、アセットを表示および検索できます。インターフェイスによって検索方法は多少異なります。

どちらの UI で検索する場合でも、次の基準でフィルターを適用できます（ここでは、タッチ操作向け UI を示しています）。

**[!UICONTROL キーワードを入力]** ：アセットを名前で検索できます。 検索時に入力したキーワードが、ファイル名の先頭になります。 例えば、「swimming」という単語を入力すると、入力した順序どおりの文字列で始まるアセットファイルの名前が検索されます。アセットを検索するには、キーワードを入力した後、必ず Enter キーを押します。

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL フォルダー/パス]**  — 表示されるフォルダーの名前は、選択した設定に基づいています。 フォルダーアイコンをタップしてサブフォルダーを選択し、チェックマークをタップして選択すると、下位のレベルまでドリルダウンできます。

キーワードを入力してフォルダーを選択すると、そのExperience Managerーとサブフォルダーが検索されます。 ただし、検索時にキーワードを入力しない場合、フォルダーを選択すると、そのフォルダー内のアセットのみが表示され、サブフォルダーは含まれません。

デフォルトでは、Experience Managerは、選択されたフォルダーとすべてのサブフォルダーを検索します。

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL アセットのタイプ]**  — 選択 **[!UICONTROL Dynamic Media Classic]** Dynamic Media Classicコンテンツを参照します。 このオプションは、Dynamic Media Classicが設定されている場合にのみ使用できます。

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 設定]**  — で複数のDynamic Media Classic設定が定義されている場合 [!UICONTROL Cloud Services]を選択する場合は、ここで選択できます。 その結果、選択した設定に応じてフォルダーが変わります。

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL アセットタイプ]** - Dynamic Media Classicブラウザー内で、結果をフィルタリングして、次のいずれかを含めることができます。画像、テンプレート、ビデオおよびアダプティブビデオセットを参照してください。 どのアセットタイプも選択しない場合、デフォルトでは、「Experience Manager」はすべてのアセットタイプを検索します。

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* クラシック UI では、**Flash** と **FXG** も検索できます。タッチ操作向け UI でのこれらのタイプのフィルタリングはサポートされていません。
>
>* ビデオを検索するときは、単一のレンディションが検索されています。結果は、元のレンディション（&amp;ast;.mp4 のみ）とエンコードされたレンディションを返します。
>* アダプティブビデオセットを検索する場合は、フォルダーとすべてのサブフォルダーが検索されますが、検索にキーワードを追加した場合にのみ検索されます。 キーワードを追加していない場合、Experience Managerはサブフォルダーを検索しません。

>


**[!UICONTROL 公開ステータス]**  — 公開ステータスに基づいてアセットをフィルタリングできます。 **[!UICONTROL 非公開]** または **[!UICONTROL 公開済み]**. 選択しない場合は、 **[!UICONTROL 公開ステータス]**:Experience Managerは、デフォルトで、すべての公開ステータスを検索します。

![chlimage_1-247](assets/chlimage_1-247.png)
