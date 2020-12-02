---
title: ダイナミックMedia Classic機能のページへの追加
description: AEMページにDynamic Media Classicの機能とコンポーネントを追加する方法を説明します。
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '2862'
ht-degree: 31%

---


# ページへのDynamic Media Classic機能の追加{#adding-scene-features-to-your-page}

[Adobeダイナミックメディア](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) クラシックは、リッチメディアアセットを管理、強化、公開、およびWeb、モバイル、電子メール、インターネットに接続されたディスプレイや印刷に配信するためのホストソリューションです。

Dynamic Media Classicで公開したAEMアセットは、様々なビューアに表示できます。

* ズーム
* フライアウト
* ビデオ
* 画像テンプレート
* 画像

デジタルアセットはAEMからDynamic Media Classicに直接公開でき、デジタルアセットはDynamic Media ClassicからAEMに公開できます。

このドキュメントでは、デジタルアセットをAEMからDynamic Media Classicに公開する方法と、デジタルアセットをからDynamic Media Classicに公開する方法を説明します。 また、ビューアについても詳しく説明します。Dynamic Media Classic用のAEMの設定について詳しくは、[Dynamic Media ClassicとAEM](/help/sites-administering/scene7.md)の統合を参照してください。

[画像マップの追加](image-maps.md)も参照してください。

AEM でのビデオコンポーネントの使用について詳しくは、[ビデオ](video.md)を参照してください。

>[!NOTE]
>
>Dynamic Media Classicアセットが正しく表示されない場合は、ダイナミックメディアが[無効](config-dynamic.md#disabling-dynamic-media)であることを確認し、ページを更新します。

## アセット{#manually-publishing-to-scene-from-assets}からDynamic Media Classicへの手動公開

デジタルアセットは、次の方法でDynamic Media Classicに公開できます。

* [クラシック UI を使用して Assets コンソールから](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [クラシック UI を使用してアセットから](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [CQターゲットフォルダーの外側からの従来のユーザーインターフェイス](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>AEMは、Dynamic Media Classicに非同期で公開します。 「**[!UICONTROL 公開]**」をクリックした後、アセットがDynamic Media Classicに公開されるまでに数秒かかる場合があります。


## Dynamic Media Classicコンポーネント{#scene-components}

AEMでは、次のDynamic Media Classicコンポーネントを使用できます。

* ズーム
* フライアウト（ズーム）
* 画像テンプレート
* 画像
* ビデオ

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できないので、を使用する前に&#x200B;**[!UICONTROL デザイン]**&#x200B;モードで選択する必要があります。

これらのコンポーネントを&#x200B;**[!UICONTROL デザイン]**&#x200B;モードで使用できるようになったら、他のAEMコンポーネントと同様に、ページに追加できます。 まだDynamic Media Classicに公開されていないアセットは、同期フォルダー内、ページ上、またはDynamic Media Classicクラウド設定と共に公開される場合、Dynamic Media Classicに公開されます。

>[!NOTE]
>
>カスタムビューアを作成して開発する場合は、コンテンツファインダーを使用して、**[!UICONTROL allowfullscreen]**&#x200B;パラメーターを明示的に追加する必要があります。

### Flash ビューアのサポート終了に関する通知 {#flash-viewers-end-of-life-notice}

2017年1月31日、AdobeダイナミックメディアクラシックはFlashビューアプラットフォームのサポートを終了しました。

この重要な変更について詳しくは、[Flash ビューアのサポート終了に関する FAQ](https://docs.adobe.com/content/docs/jp/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html) を参照してください。

### ページ{#adding-a-scene-component-to-a-page}へのDynamic Media Classicコンポーネント(Scene7)の追加

ダイナミックメディアクラシック(Scene7)コンポーネントをページに追加するのと、コンポーネントをページに追加するのと同じです。 Dynamic Media Classicコンポーネントについては、以下の各節で詳しく説明します。

**ダイナミックメディアクラシック(Scene7)コンポーネントをページに追加するには**

1. AEMで、ダイナミックメディアクラシック(Scene7)コンポーネントを追加するページを開きます。

1. 使用可能なDynamic Media Classicコンポーネントがない場合は、「**[!UICONTROL デザイン]**&#x200B;モード」をクリックし、青い境界線の付いた任意のコンポーネントをタップします。次に、**[!UICONTROL 親]**&#x200B;アイコンをタップし、**[!UICONTROL 設定]**&#x200B;アイコンをタップします。 **[!UICONTROL Parsys (Design)]**&#x200B;で、使用可能にするすべてのDynamic Media Classicコンポーネントを選択し、「**[!UICONTROL OK.]**」をクリックします。

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. 「**[!UICONTROL 編集]**」をクリックして&#x200B;**[!UICONTROL 編集]**&#x200B;モードに戻ります。

1. サイドキックのDynamic Media Classicグループから、目的の場所のページにコンポーネントをドラッグします。

1. **[!UICONTROL 設定]**&#x200B;アイコンをクリックして、コンポーネントを開きます。

1. コンポーネントの編集を必要に応じておこない、「**[!UICONTROL OK]**」をクリックして変更内容を保存します。
1. 画像またはビデオをコンテンツブラウザーから、ページに追加したDynamic Media Classicコンポーネントにドラッグします。

   >[!NOTE]
   >
   >タッチ操作対応UIのみ、画像またはビデオをページに配置したDynamic Media Classicコンポーネントにドラッグ&amp;ドロップする必要があります。 Dynamic Media Classicコンポーネントの選択と編集、およびアセットの選択はサポートされていません。

### レスポンシブサイトへのインタラクティブな表示エクスペリエンスの追加{#adding-interactive-viewing-experiences-to-a-responsive-website}

アセットのレスポンシブデザインとは、アセットが表示される場所に適応することを意味します。レスポンシブデザインを使用すると、同じアセットを複数のデバイスで効果的に表示できます。

[Web ページのレスポンシブデザイン](/help/sites-developing/responsive.md)も参照してください。

**インタラクティブな表示エクスペリエンスをレスポンシブサイトに追加するには**

1. AEMにログインし、[AdobeのダイナミックメディアクラシックCloud Services](/help/sites-administering/scene7.md#configuring-scene-integration)を設定済みで、Dynamic Media Classicコンポーネントが使用可能であることを確認します。

   >[!NOTE]
   >
   >Dynamic Media Classicコンポーネントが使用できない場合は、[デザインモード](/help/sites-authoring/default-components-designmode.md)を使用してコンポーネントを有効にする必要があります。

1. **[!UICONTROL ダイナミックメディアクラシック]**&#x200B;コンポーネントが有効なWebサイトで、**[!UICONTROL 画像]**&#x200B;コンポーネントをページにドラッグします。
1. コンポーネントを選択し、設定アイコンをタップします。
1. 「**[!UICONTROL ダイナミックメディアクラシック設定]**」タブで、ブレークポイントを調整します。

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. ビューアがレスポンシブにサイズ変更され、すべてのインタラクションがデスクトップ、タブレットおよびモバイル用に最適化されていることを確認します。

### すべてのDynamic Media Classicコンポーネントに共通の設定{#settings-common-to-all-scene-components}

設定オプションは異なりますが、以下はすべての[!UICONTROL Dynamic Media Classic]コンポーネントに共通です。

* **[!UICONTROL ファイル参照]**  — 参照するファイルを参照します。ファイル参照にはアセットのURLが表示されます。このURLは、URLコマンドとパラメーターを含む完全なDynamic Media Classic URLとは限りません。 このフィールドには、Dynamic Media Classic URLのコマンドおよびパラメーターを追加できません。 それらは、コンポーネントの対応する機能を使用して追加する必要があります。
* **[!UICONTROL 幅]**  — 幅を設定します。
* **[!UICONTROL 高さ]**  — 高さを設定します。

これらの設定オプションを設定するには、例えば&#x200B;**[!UICONTROL ズーム]**&#x200B;コンポーネントを開いたときに、Dynamic Media Classicコンポーネントを開く(重複をクリックする)ことで行います。

![chlimage_1-226](assets/chlimage_1-226.png)

### ズーム {#zoom}

**[!UICONTROL +]**&#x200B;ボタンを押すと、HTML5ズームコンポーネントで大きい画像が表示されます。

アセットの下部にはズームツールが用意されています。**[!UICONTROL +]**&#x200B;をタップして拡大します。 **[!UICONTROL -]**&#x200B;をタップして減らします。 **[!UICONTROL x]**&#x200B;またはズームリセットの矢印をタップすると、画像が読み込み元のサイズに戻ります。 斜めの矢印をタップして、画面全体を表示します。 「**[!UICONTROL 編集]**」をタップして、コンポーネントを設定します。 このコンポーネントでは、[!UICONTROL ダイナミックメディアクラシック]コンポーネント](#settings-common-to-all-scene-components)に共通の[設定を構成できます。

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### Flyout {#flyout}

HTML5 **[!UICONTROL フライアウト]**&#x200B;コンポーネントでは、アセットは分割画面で表示されます。アセットを指定されたサイズで残し、右にズーム部分が表示されます。 「**[!UICONTROL 編集]**」をタップして、コンポーネントを設定します。 このコンポーネントでは、すべてのダイナミックMedia Classicコンポーネント](#settings-common-to-all-scene-components)に共通の[設定を構成できます。

>[!NOTE]
>
>**[!UICONTROL フライアウト]**&#x200B;コンポーネントでカスタムサイズを使用する場合、そのカスタムサイズが使用され、コンポーネントのレスポンシブセットアップが無効になります。
>
>**[!UICONTROL フライアウト]**&#x200B;コンポーネントで、**[!UICONTROL デザイン表示]**&#x200B;の設定に従って初期設定のサイズが使用される場合は、初期設定のサイズが使用され、コンポーネントが伸張して、コンポーネントのレスポンシブ設定にページレイアウトサイズが調整されます。ただし、コンポーネントのレスポンシブセットアップには制限があることに注意してください。レスポンシブ設定で&#x200B;**[!UICONTROL フライアウト]**&#x200B;コンポーネントを使用する場合は、フルページで使用しないでください。そうでないと、**[!UICONTROL フライアウト]**&#x200B;がページの右の境界線を越える場合があります。

![chlimage_1-228](assets/chlimage_1-228.png)

### 画像 {#image}

Dynamic Media Classic **[!UICONTROL 画像]**&#x200B;コンポーネントを使用すると、Dynamic Media Classic修飾子、画像またはビューアプリセット、シャープなどのダイナミックメディアクラシック機能を画像に追加できます。 ダイナミックメディアクラシック&#x200B;**[!UICONTROL 画像]**&#x200B;コンポーネントは、AEMの特別なダイナミックメディアクラシック機能を持つ他の画像コンポーネントと似ています。 この例では、画像にダイナミックメディアクラシックURL修飾子`&op_invert=1`が適用されています。

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL タイトル、代替テキスト]** - 「 **** 詳細」タブで、画像にタイトルを追加し、グラフィックをオフにしているユーザー用の代替テキストを追加します。

**[!UICONTROL URL、開く場所]**  — リンクを開くアセットを設定できます。「**[!UICONTROL URL]**」と「**[!UICONTROL 次のウィンドウで開く]**」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL ビューアプリセット]**  — ドロップダウンメニューから既存のビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL ダイナミックメディアクラシック設定]**  — アクティブな画像プリセットをSPSから取得する際に使用するダイナミックメディアクラシック設定を選択します。

**[!UICONTROL 画像プリセット]**  — ドロップダウンメニューから既存の画像プリセットを選択します。探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL 出力形式]**  — 画像の出力形式（jpegなど）を選択します。選択する出力形式によっては、追加の設定オプションが表示される場合があります。[画像プリセットのベストプラクティス](/help/assets/managing-image-presets.md#image-preset-options)を参照してください。

**[!UICONTROL シャープ]**  — 画像にシャープを適用する方法を選択します。シャープニングについて詳しくは、[画像プリセットのベストプラクティス](/help/assets/managing-image-presets.md#image-preset-options)および[シャープニングのベストプラクティス](/help/assets/assets/s7_sharpening_images.pdf)を参照してください。

**[!UICONTROL URL修飾子]**  — ダイナミックメディアクラシック画像のコマンドを追加することで、画像効果を変更できます。詳しくは、[画像プリセット](/help/assets/managing-image-presets.md)および「[コマンドリファレンス](https://docs.adobe.com/content/help/ja-JP/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)」を参照してください。

**[!UICONTROL ブレークポイント]** - Webサイトがレスポンシブである場合は、ブレークポイントを調整します。ブレークポイントはコンマ（,）で区切って指定してください。

### 画像テンプレート {#image-template}

[Dynamic Media Classic画像テンプレートは、Dynamic Media Classicに読み込まれたレイヤーPhotoshopコンテンツです。コンテンツとプロパティは可変性を考慮してパラメータ化されていました。](https://docs.adobe.com/help/en/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) **[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを使用すると、画像を読み込んで、テキストを AEM で動的に変更できます。また、ClientContext の値を使用するように&#x200B;**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを設定できます。これにより、各ユーザーが個別に画像を活用できます。

「**[!UICONTROL 編集]**」をタップして、コンポーネントを設定します。 すべてのDynamic Media Classicコンポーネント](#settings-common-to-all-scene-components)に共通の[設定と、この節で説明する他の設定を構成できます。

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL ファイル参照、幅、高さ]** - ScDynamic Media Classicene7のすべてのコンポーネントに共通の設定を参照してください。

>[!NOTE]
>
>Dynamic Media ClassicのURLコマンドとパラメーターは、ファイル参照URLに直接追加できません。 これらは、**[!UICONTROL パラメーター]**&#x200B;パネルのコンポーネントの UI でのみ定義できます。

**[!UICONTROL タイトル、代替テキスト]** - 「ダイナミックメディアクラシック画像テンプレート」タブで、画像にタイトルを追加し、グラフィックをオフにしているユーザー用の代替テキストを追加します。

**[!UICONTROL URL、開く場所]**  — リンクを開くアセットを設定できます。「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL パラメータパネル]**  — 画像を読み込むと、パラメーターに画像の情報が事前に入力されます。動的に変更できるコンテンツがない場合、このウィンドウは空になります。

![chlimage_1-233](assets/chlimage_1-233.png)

#### テキストの動的な変更 {#changing-text-dynamically}

テキストを動的に変更するには、フィールドに新しいテキストを入力し、「**[!UICONTROL OK」をクリックします。]**&#x200B;この例では、**[!UICONTROL Price]**&#x200B;は$50になり、配送料は$99セントになります。

![chlimage_1-234](assets/chlimage_1-234.png)

画像内のテキストが変更されます。フィールドの横の「**[!UICONTROL リセット]**」をタップすると、テキストを元の値に戻すことができます。

![chlimage_1-235](assets/chlimage_1-235.png)

#### ClientContext の値を反映したテキストの変更 {#changing-text-to-reflect-the-value-of-a-client-context-value}

フィールドをクライアントコンテキスト値にリンクするには、「**[!UICONTROL 選択]**」をタップしてクライアントコンテキストメニューを開き、クライアントコンテキストを選択して「**[!UICONTROL OK」をタップします。]**&#x200B;この例では、「名前」フィールドとプロファイル内の書式設定された名前とのリンクに基づいて名前が変わります。

![chlimage_1-236](assets/chlimage_1-236.png)

現在ログインしているユーザーの名前がテキストに反映されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-237](assets/chlimage_1-237.png)

#### ダイナミックメディアクラシック画像テンプレートをリンク{#making-the-scene-image-template-a-link}にする

1. Dynamic Media Classic **[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを含むページで、「**[!UICONTROL 編集]**」をタップします。
1. 「**[!UICONTROL URL]**」フィールドに、画像をタップしたときにユーザーが移動するURLを入力します。 「**[!UICONTROL 次のウィンドウで開く]**」フィールドで、ターゲットを新しいウィンドウと同じウィンドウのどちらで開くかを選択します。

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 「**[!UICONTROL OK]**」をタップします。

### ビデオコンポーネント {#video-component}

ダイナミックメディアクラシック&#x200B;**[!UICONTROL ビデオ]**&#x200B;コンポーネント（サイドキックのダイナミックメディアクラシックセクションから利用可能）は、デバイスと帯域幅検出を使用して、各画面に適切なビデオを提供します。 このコンポーネントは HTML5 ビデオプレーヤー（チャネルを超えて使用可能な単一のビューア）です。

このコンポーネントはアダプティブビデオセット（単一の MP4 ビデオまたは単一の F4V ビデオ）で使用できます。

Dynamic Media Classic統合でのビデオの動作について詳しくは、[ビデオ](s7-video.md)を参照してください。 また、[Dynamic Media Classic VideoコンポーネントとFoundation Videoコンポーネント](s7-video.md)を参照してください。

![chlimage_1-239](assets/chlimage_1-239.png)

### ビデオコンポーネントに関する既知の制限事項 {#known-limitations-for-the-video-component}

AdobeDAMとWCMは、プライマリソースビデオがアップロードされたかどうかを表示します。 次に示すプロキシアセットは表示されません。

* Dynamic Media Classicのエンコードされたレンディション
* ダイナミックMedia Classicアダプティブビデオセット

Dynamic Media Classicビデオコンポーネントでアダプティブビデオセットを使用する場合、ビデオのサイズに合わせてコンポーネントのサイズを変更する必要があります。

## Dynamic Media Classicコンテンツブラウザー{#scene-content-browser}

Dynamic Media Classicコンテンツブラウザーを使用すると、Dynamic Media ClassicのコンテンツをAEMで直接表示できます。 コンテンツブラウザーにアクセスするには、**[!UICONTROL コンテンツファインダー]**&#x200B;で、タッチ操作向けユーザーインターフェイスの&#x200B;**[!UICONTROL ダイナミックメディアクラシック]**&#x200B;またはクラシックユーザーインターフェイスの&#x200B;**[!UICONTROL S7]**&#x200B;アイコンを選択します。 どちらの UI を使用しても機能は同じです。

設定が複数ある場合、AEM では既定で[デフォルト設定](/help/sites-administering/scene7.md#configuring-a-default-configuration)が表示されます。ドロップダウンメニューのDynamic Media Classicコンテンツブラウザーで、異なる設定を直接選択できます。

>[!NOTE]
>
>* アドホックフォルダーにあるアセットは、Dynamic Media Classicコンテンツブラウザーには表示されません。
>* [セキュアプレビューを有効にする](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)と、Dynamic Media Classicの公開済みアセットと未公開アセットの両方が、Dynamic Media Classicコンテンツブラウザーに表示されます。
>* コンテンツブラウザーに&#x200B;**[!UICONTROL ダイナミックメディアクラシック]**&#x200B;または&#x200B;**[!UICONTROL S7]**&#x200B;アイコンが表示されない場合は、AEM](/help/sites-administering/scene7.md)で動作するように[ダイナミックメディアクラシックを設定する必要があります。
>* ビデオの場合、Dynamic Media Classicコンテンツブラウザーは次の機能をサポートします。

   >
   >   
   * アダプティブビデオセット：複数の画面でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
   >   * 単一の MP4 ビデオ
   >   * 単一の F4V ビデオ


### タッチ操作向けUIでのコンテンツの参照{#browsing-content-in-the-touch-optimized-ui}

タッチ対応 UI またはクラシック UI を使用してコンテンツブラウザーにアクセスできます。現時点では、タッチ対応 UI には次の制限事項があります。

* FXGおよびDynamic Media ClassicのFlashアセットはサポートされていません。

3つ目のドロップダウンメニューから「**[!UICONTROL ダイナミックメディアクラシック]**」を選択して、ダイナミックメディアクラシックアセットを参照します。 Dynamic Media Classic/AEM統合を設定していない場合、Dynamic Media Classicはリストに表示されません。

>[!NOTE]
>
>* Dynamic Media Classicコンテンツブラウザーでは、約100個のアセットが読み込まれ、名前順に並べ替えられます。
>* セキュリティで保護されたプレビューサーバーが設定されている場合、ブラウザーはそのプレビューサーバーを使用してサムネールとアセットをレンダリングします。

>



![chlimage_1-240](assets/chlimage_1-240.png)

また、ブラウザー内でアセットの上にマウスポインターを置くと、解像度の情報、サイズ、変更後の日数およびファイル名を参照できます。

![chlimage_1-241](assets/chlimage_1-241.png)

* アダプティブビデオセットとテンプレートの場合は、サムネール用のサイズ情報が生成されません。
* アダプティブビデオセットの場合は、サムネール用の解像度が生成されません。

### コンテンツブラウザー{#searching-for-scene-assets-with-the-content-browser}でのDynamic Media Classicアセットの検索

ダイナミックメディアクラシックアセットの検索は、AEMアセットの検索と似ていますが、検索時に、実際にはアセットをAEMに直接読み込むのではなく、リモート表示のアセットが表示される点が異なります。

クラシック UI またはタッチ操作向け UI を使用して、アセットを表示および検索できます。インターフェイスによって検索方法は多少異なります。

どちらの UI で検索する場合でも、次の基準でフィルターを適用できます（ここでは、タッチ操作向け UI を示しています）。

**[!UICONTROL キーワードの入力]**  — アセットを名前で検索できます。検索時には、入力したキーワードで始まるファイル名が検索されます。例えば、「swimming」という単語を入力すると、入力した順序どおりの文字列で始まるアセットファイルの名前が検索されます。キーワードを入力した後は、必ずenterをタップしてアセットを検索してください。

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Folder/path]**  — 表示されるフォルダーの名前は、選択した設定に基づいています。フォルダーのアイコンをタップし、サブフォルダーを選択し、チェックマークをタップしてレベルを下げることができます。

キーワードを入力してフォルダーを選択すると、AEM ではそのフォルダーがとすべてのサブフォルダーが検索されます。ただし、検索時にキーワードを入力しない場合は、フォルダーを選択してもそのフォルダー内のアセットしか表示されず、サブフォルダーは含まれません。

デフォルトでは、AEM は、選択したフォルダーとすべてのサブフォルダーを検索します。

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL アセットのタイプ]** - 「 **** ダイナミックメディアクラシック」を選択して、ダイナミックメディアクラシックのコンテンツを参照します。このオプションは、Dynamic Media Classicが設定されている場合にのみ使用できます。

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 設定]** - [!UICONTROL Cloud Servicesで複数のDynamic Media Classic設定が定義されている場合]、ここで選択できます。そのため、選択した設定に基づいてフォルダーが変わります。

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL アセットタイプ]** - Dynamic Media Classicブラウザー内で、結果をフィルタリングして次のいずれかを含めることができます。画像、テンプレート、ビデオおよびアダプティブビデオセットを参照してください。アセットタイプを選択しない場合、AEM ではデフォルトですべてのアセットタイプが検索されます。

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* クラシック UI では、**Flash** と **FXG** も検索できます。現時点では、タッチ対応 UI でのこれらのフィルタリングはサポートされていません。
   >
   >
* ビデオを検索するときは、単一のレンディションが検索されています。結果は、元のレンディション（&amp;ast;.mp4のみ）とエンコードされたレンディションを返します。
>* アダプティブビデオセットを検索すると、フォルダとすべてのサブフォルダが検索されますが、検索にキーワードを追加した場合にのみ検索されます。 キーワードを追加しない場合、AEM はサブフォルダーを検索しません。

>



**[!UICONTROL 公開ステータス]**  — 公開ステータスに基づいてアセットをフィルタリングできます。 **[!UICONTROL 非公開または]**  **[!UICONTROL 公開済み。]** 「 **[!UICONTROL 公開ステータス」を選択しない場合、AEMでは、デフォルトですべての]**&#x200B;公開ステータスが検索されます。

![chlimage_1-247](assets/chlimage_1-247.png)

