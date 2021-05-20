---
title: ページへのDynamic Media Classic機能の追加
description: AEMページにDynamic Media Classicの機能とコンポーネントを追加する方法を説明します。
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: Business Practitioner, Administrator
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2863'
ht-degree: 31%

---

# ページ{#adding-scene-features-to-your-page}へのDynamic Media Classic機能の追加

[AdobeDynamic Media ](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) Classicは、Web、モバイル、電子メールおよびインターネットに接続されたディスプレイと印刷でリッチメディアアセットを管理、強化、公開、および配信するためのホストソリューションです。

Dynamic Media Classicで公開されたAEMアセットは、様々なビューアで表示できます。

* ズーム
* フライアウト
* ビデオ
* 画像テンプレート
* 画像

デジタルアセットをAEMからDynamic Media Classicに直接公開したり、Dynamic Media ClassicからAEMに公開したりできます。

このドキュメントでは、AEMからDynamic Media Classicにデジタルアセットを公開する方法と、その逆の方法について説明します。 また、ビューアについても詳しく説明します。AEM for Dynamic Media Classicの設定について詳しくは、[Dynamic Media ClassicとAEM](/help/sites-administering/scene7.md)の統合を参照してください。

[画像マップの追加](image-maps.md)も参照してください。

AEM でのビデオコンポーネントの使用について詳しくは、[ビデオ](video.md)を参照してください。

>[!NOTE]
>
>Dynamic Media Classicのアセットが正しく表示されない場合は、Dynamic Mediaが[無効](config-dynamic.md#disabling-dynamic-media)であることを確認してから、ページを更新します。

## アセット{#manually-publishing-to-scene-from-assets}からDynamic Media Classicへの手動公開

次の手順で、デジタルアセットをDynamic Media Classicに公開できます。

* [クラシック UI を使用して Assets コンソールから](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [クラシック UI を使用してアセットから](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [クラシックUIでのCQ Targetフォルダーの外側からの操作](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>AEMはDynamic Media Classicに非同期で公開します。 「**[!UICONTROL 公開]**」をクリックした後、アセットがDynamic Media Classicに公開されるまでに数秒かかる場合があります。


## Dynamic Media Classicコンポーネント{#scene-components}

AEMでは、次のDynamic Media Classicコンポーネントを使用できます。

* ズーム
* フライアウト（ズーム）
* 画像テンプレート
* 画像
* ビデオ

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できないので、使用する前に&#x200B;**[!UICONTROL デザイン]**&#x200B;モードで選択する必要があります。

**[!UICONTROL デザイン]**&#x200B;モードで使用可能になったら、他のAEMコンポーネントと同様に、コンポーネントをページに追加できます。 まだDynamic Media Classicに公開されていないアセットは、同期されたフォルダー内、ページ上、またはDynamic Media Classicクラウド設定を使用している場合、Dynamic Media Classicに公開されます。

>[!NOTE]
>
>カスタムビューアを作成および開発し、コンテンツファインダーを使用する場合は、**[!UICONTROL allowfullscreen]**&#x200B;パラメーターを明示的に追加する必要があります。

### Flash ビューアのサポート終了に関する通知 {#flash-viewers-end-of-life-notice}

2017年1月31日に、AdobeDynamic Media ClassicはFlashビューアプラットフォームのサポートを終了しました。

この重要な変更について詳しくは、[Flash ビューアのサポート終了に関する FAQ](https://docs.adobe.com/content/docs/jp/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html) を参照してください。

### Dynamic Media Classicコンポーネント(Scene7)のページへの追加{#adding-a-scene-component-to-a-page}

Dynamic Media Classic(Scene7)コンポーネントをページに追加する方法は、任意のページにコンポーネントを追加する方法と同じです。 Dynamic Media Classicコンポーネントについて、以降の節で詳しく説明します。

**Dynamic Media Classic(Scene7)コンポーネントをページに追加するには**

1. AEMで、Dynamic Media Classic(Scene7)コンポーネントを追加するページを開きます。

1. Dynamic Media Classicコンポーネントが使用できない場合は、「**[!UICONTROL デザイン]**」モードをクリックし、青い境界線の付いた任意のコンポーネントをタップし、**[!UICONTROL 親]**&#x200B;アイコンをタップして、**[!UICONTROL 設定]**&#x200B;アイコンをタップします。 **[!UICONTROL Parsys(Design)]**&#x200B;で、すべてのDynamic Media Classicコンポーネントを選択して使用可能にし、「**[!UICONTROL OK]**」をクリックします。

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. 「**[!UICONTROL 編集]**」をクリックして、「**[!UICONTROL 編集]**」モードに戻ります。

1. サイドキックのDynamic Media Classicグループからページの目的の場所にコンポーネントをドラッグします。

1. **[!UICONTROL 設定]**&#x200B;アイコンをクリックして、コンポーネントを開きます。

1. コンポーネントの編集を必要に応じておこない、「**[!UICONTROL OK]**」をクリックして変更内容を保存します。
1. 画像またはビデオをコンテンツブラウザーからページに追加したDynamic Media Classicコンポーネントにドラッグします。

   >[!NOTE]
   >
   >タッチUIの場合のみ、画像またはビデオをページに配置したDynamic Media Classicコンポーネントにドラッグ&amp;ドロップする必要があります。 Dynamic Media Classicコンポーネントの選択と編集の後でのアセットの選択はサポートされていません。

### レスポンシブサイトへのインタラクティブな表示エクスペリエンスの追加{#adding-interactive-viewing-experiences-to-a-responsive-website}

アセットのレスポンシブデザインとは、アセットが表示される場所に適応することを意味します。レスポンシブデザインを使用すると、同じアセットを複数のデバイスで効果的に表示できます。

[Web ページのレスポンシブデザイン](/help/sites-developing/responsive.md)も参照してください。

**レスポンシブサイトにインタラクティブな表示エクスペリエンスを追加するには**

1. AEMにログインし、[AdobeDynamic Media ClassicCloud Services](/help/sites-administering/scene7.md#configuring-scene-integration)が設定され、Dynamic Media Classicコンポーネントが使用可能であることを確認します。

   >[!NOTE]
   >
   >Dynamic Media Classicコンポーネントを使用できない場合は、デザインモード](/help/sites-authoring/default-components-designmode.md)を使用して有効にするように[してください。

1. **[!UICONTROL Dynamic Media Classic]**&#x200B;コンポーネントが有効なWebサイトで、**[!UICONTROL 画像]**&#x200B;コンポーネントをページにドラッグします。
1. コンポーネントを選択し、設定アイコンをタップします。
1. 「**[!UICONTROL Dynamic Media Classic設定]**」タブで、ブレークポイントを調整します。

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. ビューアがレスポンシブにサイズ変更され、すべてのインタラクションがデスクトップ、タブレットおよびモバイル用に最適化されていることを確認します。

### すべてのDynamic Media Classicコンポーネントに共通の設定{#settings-common-to-all-scene-components}

設定オプションは異なりますが、次の操作はすべての[!UICONTROL Dynamic Media Classic]コンポーネントに共通です。

* **[!UICONTROL ファイル参照]**  — 参照するファイルを参照します。ファイル参照は、アセットのURLを表示しますが、必ずしもURLコマンドやパラメーターを含む完全なDynamic Media Classic URLとは限りません。 このフィールドにDynamic Media Classic URLコマンドおよびパラメーターを追加することはできません。 それらは、コンポーネントの対応する機能を使用して追加する必要があります。
* **[!UICONTROL 幅]**  — 幅を設定できます。
* **[!UICONTROL 高さ]**  — 高さを設定できます。

これらの設定オプションを設定するには、例えば&#x200B;**[!UICONTROL ズーム]**&#x200B;コンポーネントを開く際に、Dynamic Media Classicコンポーネントを開く（ダブルクリックする）必要があります。

![chlimage_1-226](assets/chlimage_1-226.png)

### ズーム {#zoom}

**[!UICONTROL +]**&#x200B;ボタンを押すと、HTML5ズームコンポーネントで大きな画像が表示されます。

アセットの下部にはズームツールが用意されています。**[!UICONTROL +]**&#x200B;をタップして拡大します。 **[!UICONTROL -]**&#x200B;をタップして減らします。 **[!UICONTROL x]**&#x200B;をタップするか、ズームのリセット矢印をタップすると、画像が元のサイズに戻ります。 斜めの矢印をタップして、全画面表示にします。 「**[!UICONTROL 編集]**」をタップして、コンポーネントを設定します。 このコンポーネントを使用すると、すべての[!UICONTROL Dynamic Media Classic]コンポーネント](#settings-common-to-all-scene-components)に共通の[設定を構成できます。

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### フライアウト {#flyout}

HTML5の&#x200B;**[!UICONTROL フライアウト]**&#x200B;コンポーネントでは、アセットは分割画面で表示されます。アセットを指定されたサイズのままにした。ズーム部分の右側が表示されます。 「**[!UICONTROL 編集]**」をタップして、コンポーネントを設定します。 このコンポーネントを使用すると、すべてのDynamic Media Classicコンポーネント](#settings-common-to-all-scene-components)に共通の[設定を構成できます。

>[!NOTE]
>
>**[!UICONTROL フライアウト]**&#x200B;コンポーネントでカスタムサイズを使用する場合は、そのカスタムサイズが使用され、コンポーネントのレスポンシブ設定が無効になります。
>
>**[!UICONTROL フライアウト]**&#x200B;コンポーネントで、**[!UICONTROL デザインビュー]**&#x200B;で設定したデフォルトのサイズを使用する場合は、デフォルトのサイズが使用され、コンポーネントが拡大されて、レスポンシブなコンポーネント設定に合わせます。ただし、コンポーネントのレスポンシブ設定には制限があることに注意してください。**[!UICONTROL フライアウト]**&#x200B;コンポーネントをレスポンシブに設定して使用する場合は、ページ全体を拡大して使用しないでください。そうしないと、**[!UICONTROL フライアウト]**&#x200B;がページの右の境界線を越えて伸びる場合があります。

![chlimage_1-228](assets/chlimage_1-228.png)

### 画像 {#image}

Dynamic Media Classicの&#x200B;**[!UICONTROL 画像]**&#x200B;コンポーネントを使用すると、Dynamic Media Classicの修飾子、画像またはビューアプリセット、シャープニングなど、Dynamic Media Classicの機能を画像に追加できます。 Dynamic Media Classicの&#x200B;**[!UICONTROL 画像]**&#x200B;コンポーネントは、AEMの特別なDynamic Media Classic機能を持つ他の画像コンポーネントと似ています。 この例では、画像にDynamic Media Classic URL修飾子`&op_invert=1`が適用されています。

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL タイトル、代替テキスト]**  - 「詳細設 **** 定」タブで、グラフィックの表示をオフにしているユーザー向けのタイトルと代替テキストを画像に追加します。

**[!UICONTROL URL、次のウィンドウで開く]**  — からアセットを設定して、リンクを開くことができます。「**[!UICONTROL URL]**」と「**[!UICONTROL 次のウィンドウで開く]**」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL ビューアプリセット]**  — ドロップダウンメニューから既存のビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL Dynamic Media Classic設定]**  - SPSからアクティブな画像プリセットを取得するために使用するDynamic Media Classic設定を選択します。

**[!UICONTROL 画像プリセット]**  — ドロップダウンメニューから既存の画像プリセットを選択します。探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL 出力形式]**  — 画像の出力形式（例：jpeg）を選択します。選択する出力形式によっては、追加の設定オプションが表示される場合があります。[画像プリセットのベストプラクティス](/help/assets/managing-image-presets.md#image-preset-options)を参照してください。

**[!UICONTROL シャープ]**  — 画像にシャープを適用する方法を選択します。シャープニングについて詳しくは、[画像プリセットのベストプラクティス](/help/assets/managing-image-presets.md#image-preset-options)および[シャープニングのベストプラクティス](/help/assets/assets/sharpening_images.pdf)を参照してください。

**[!UICONTROL URL修飾子]**  — 追加のDynamic Media Classic画像コマンドを指定して、画像効果を変更できます。詳しくは、[画像プリセット](/help/assets/managing-image-presets.md)および「[コマンドリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)」を参照してください。

**[!UICONTROL ブレークポイント]**  - Webサイトがレスポンシブな場合は、ブレークポイントを調整する必要があります。ブレークポイントはコンマ（,）で区切って指定してください。

### 画像テンプレート {#image-template}

[Dynamic Media Classic Image Templates](https://docs.adobe.com/help/en/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) は、Dynamic Media Classicに読み込まれたPhotoshopコンテンツのレイヤーです。コンテンツとプロパティは、可変性を考慮してパラメーター化されています。**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを使用すると、画像を読み込んで、テキストを AEM で動的に変更できます。また、ClientContext の値を使用するように&#x200B;**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを設定できます。これにより、各ユーザーが個別に画像を活用できます。

「**[!UICONTROL 編集]**」をタップして、コンポーネントを設定します。 すべてのDynamic Media Classicコンポーネント](#settings-common-to-all-scene-components)に共通の[設定や、この節で説明するその他の設定を構成できます。

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL ファイル参照、幅、高さ]**  — すべてのScDynamic Media Classicene7コンポーネントに共通の設定を参照してください。

>[!NOTE]
>
>Dynamic Media Classic URLのコマンドとパラメーターは、ファイル参照URLに直接追加できません。 これらは、**[!UICONTROL パラメーター]**&#x200B;パネルのコンポーネントの UI でのみ定義できます。

**[!UICONTROL タイトル、代替テキスト]**  - 「 Dynamic Media Classic画像テンプレート」タブで、グラフィックの表示をオフにしているユーザー向けのタイトルと代替テキストを画像に追加します。

**[!UICONTROL URL、次のウィンドウで開く]**  — からアセットを設定して、リンクを開くことができます。「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL パラメーターパネル]**  — 画像を読み込む際に、画像の情報がパラメーターに事前に設定されます。動的に変更できるコンテンツがない場合、このウィンドウは空になります。

![chlimage_1-233](assets/chlimage_1-233.png)

#### テキストの動的な変更 {#changing-text-dynamically}

テキストを動的に変更するには、フィールドに新しいテキストを入力し、「**[!UICONTROL OK]**」をクリックします。この例では、**[!UICONTROL Price]**&#x200B;が$50になり、出荷は99セントになります。

![chlimage_1-234](assets/chlimage_1-234.png)

画像内のテキストが変更されます。フィールドの横にある「**[!UICONTROL リセット]**」をタップして、テキストを元の値に戻すことができます。

![chlimage_1-235](assets/chlimage_1-235.png)

#### ClientContext の値を反映したテキストの変更 {#changing-text-to-reflect-the-value-of-a-client-context-value}

フィールドをClientContext値にリンクするには、**[!UICONTROL 「]**&#x200B;を選択」をタップしてClientContextメニューを開き、ClientContextを選択して「**[!UICONTROL OK」をタップします。]**&#x200B;この例では、「名前」フィールドとプロファイル内の書式設定された名前とのリンクに基づいて名前が変わります。

![chlimage_1-236](assets/chlimage_1-236.png)

現在ログインしているユーザーの名前がテキストに反映されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-237](assets/chlimage_1-237.png)

#### Dynamic Mediaクラシック画像テンプレートをリンクにする{#making-the-scene-image-template-a-link}

1. Dynamic Media Classicの&#x200B;**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを含むページで、「**[!UICONTROL 編集]**」をタップします。
1. 「**[!UICONTROL URL]**」フィールドに、画像をタップしたときに表示されるURLを入力します。 「**[!UICONTROL 次のウィンドウで開く]**」フィールドで、ターゲットを新しいウィンドウと同じウィンドウのどちらで開くかを選択します。

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 「**[!UICONTROL OK]**」をタップします。

### ビデオコンポーネント {#video-component}

Dynamic Media Classicの&#x200B;**[!UICONTROL ビデオ]**&#x200B;コンポーネント(サイドキックのDynamic Media Classicセクションから利用可能)は、デバイスと帯域幅の検出を使用して、適切なビデオを各画面に提供します。 このコンポーネントは HTML5 ビデオプレーヤー（チャネルを超えて使用可能な単一のビューア）です。

このコンポーネントはアダプティブビデオセット（単一の MP4 ビデオまたは単一の F4V ビデオ）で使用できます。

ビデオとDynamic Media Classicの統合の連携について詳しくは、[ビデオ](s7-video.md)を参照してください。 また、[Dynamic Media Classicビデオコンポーネントと基盤ビデオコンポーネント](s7-video.md)を参照してください。

![chlimage_1-239](assets/chlimage_1-239.png)

### ビデオコンポーネントに関する既知の制限事項 {#known-limitations-for-the-video-component}

AdobeDAMとWCMに、プライマリソースビデオがアップロードされたかどうかが表示されます。 次に示すプロキシアセットは表示されません。

* Dynamic Media Classicのエンコードされたレンディション
* Dynamic Media Classicアダプティブビデオセット

Dynamic Media Classicビデオコンポーネントでアダプティブビデオセットを使用する場合は、ビデオのサイズに合わせてコンポーネントのサイズを変更する必要があります。

## Dynamic Media Classicコンテンツブラウザー{#scene-content-browser}

Dynamic Media Classicコンテンツブラウザーを使用すると、Dynamic Media ClassicのコンテンツをAEMで直接表示できます。 コンテンツブラウザーにアクセスするには、**[!UICONTROL コンテンツファインダー]**&#x200B;で、タッチ操作向けUIの&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;またはクラシックUIの&#x200B;**[!UICONTROL S7]**&#x200B;アイコンを選択します。 どちらの UI を使用しても機能は同じです。

設定が複数ある場合、AEM では既定で[デフォルト設定](/help/sites-administering/scene7.md#configuring-a-default-configuration)が表示されます。Dynamic Media Classicのコンテンツブラウザーのドロップダウンメニューで、様々な設定を直接選択できます。

>[!NOTE]
>
>* アドホックフォルダー内のアセットは、Dynamic Media Classicコンテンツブラウザーには表示されません。
>* [セキュアプレビューを有効にすると](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)、Dynamic Media Classicで公開済みと非公開の両方のアセットがDynamic Media Classicコンテンツブラウザーに表示されます。
>* コンテンツブラウザーで&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;や&#x200B;**[!UICONTROL S7]**&#x200B;アイコンがオプションとして表示されない場合は、AEM](/help/sites-administering/scene7.md)と連携するように[Dynamic Media Classicを設定する必要があります。
>* ビデオの場合、Dynamic Media Classicコンテンツブラウザーは次の機能をサポートしています。

   >
   >   
   * アダプティブビデオセット：複数の画面でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
   >   * 単一の MP4 ビデオ
   >   * 単一の F4V ビデオ


### タッチ操作向けUIでのコンテンツの参照{#browsing-content-in-the-touch-optimized-ui}

タッチ対応 UI またはクラシック UI を使用してコンテンツブラウザーにアクセスできます。現時点では、タッチ対応 UI には次の制限事項があります。

* Dynamic Media ClassicのFXGおよびFlashアセットはサポートされていません。

3番目のドロップダウンメニューから「**[!UICONTROL Dynamic Media Classic]**」を選択して、Dynamic Media Classicアセットを参照します。 Dynamic Media Classic/AEMの統合を設定していない場合、Dynamic Media Classicはリストに表示されません。

>[!NOTE]
>
>* Dynamic Media Classicコンテンツブラウザーは、約100個のアセットを読み込んで名前順に並べ替えます。
>* セキュリティで保護されたプレビューサーバーが設定されている場合、ブラウザーはそのプレビューサーバーを使用してサムネールとアセットをレンダリングします。

>



![chlimage_1-240](assets/chlimage_1-240.png)

また、ブラウザー内でアセットの上にマウスポインターを置くと、解像度の情報、サイズ、変更後の日数およびファイル名を参照できます。

![chlimage_1-241](assets/chlimage_1-241.png)

* アダプティブビデオセットとテンプレートの場合は、サムネール用のサイズ情報が生成されません。
* アダプティブビデオセットの場合は、サムネール用の解像度が生成されません。

### コンテンツブラウザー{#searching-for-scene-assets-with-the-content-browser}でのDynamic Media Classicアセットの検索

Dynamic Media Classicアセットの検索は、AEMアセットの検索と似ていますが、検索時に、実際にはAEMに直接読み込むのではなく、Dynamic Media Classicシステムにアセットのリモート表示が表示される点が異なります。

クラシック UI またはタッチ操作向け UI を使用して、アセットを表示および検索できます。インターフェイスによって検索方法は多少異なります。

どちらの UI で検索する場合でも、次の基準でフィルターを適用できます（ここでは、タッチ操作向け UI を示しています）。

**[!UICONTROL キーワードを入力]**  — アセットを名前で検索できます。検索時には、入力したキーワードで始まるファイル名が検索されます。例えば、「swimming」という単語を入力すると、入力した順序どおりの文字列で始まるアセットファイルの名前が検索されます。アセットを検索するキーワードを入力した後、必ずEnterキーを押してください。

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL フォルダー/パス]**  — 表示されるフォルダーの名前は、選択した設定に基づきます。フォルダーアイコンをタップしてサブフォルダーを選択し、チェックマークをタップして下位レベルまでドリルダウンできます。

キーワードを入力してフォルダーを選択すると、AEM ではそのフォルダーがとすべてのサブフォルダーが検索されます。ただし、検索時にキーワードを入力しない場合は、フォルダーを選択してもそのフォルダー内のアセットしか表示されず、サブフォルダーは含まれません。

デフォルトでは、AEM は、選択したフォルダーとすべてのサブフォルダーを検索します。

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL アセットのタイプ]**  -  **[!UICONTROL Dynamic Media Classicを選択]** してDynamic Media Classicコンテンツを参照します。このオプションは、Dynamic Media Classicが設定されている場合にのみ使用できます。

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 設定]**  -  [!UICONTROL Cloud Services]で複数のDynamic Media Classic設定を定義している場合は、ここで選択できます。そのため、選択した設定に基づいてフォルダーが変わります。

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL アセットタイプ]**  - Dynamic Media Classicブラウザーでは、結果をフィルタリングして次のいずれかを含めることができます。画像、テンプレート、ビデオおよびアダプティブビデオセットを参照してください。アセットタイプを選択しない場合、AEM ではデフォルトですべてのアセットタイプが検索されます。

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* クラシック UI では、**Flash** と **FXG** も検索できます。現時点では、タッチ対応 UI でのこれらのフィルタリングはサポートされていません。
   >
   >
* ビデオを検索するときは、単一のレンディションが検索されています。結果は、元のレンディション（&amp;ast;.mp4のみ）とエンコードされたレンディションを返します。
>* アダプティブビデオセットを検索する場合、検索対象は、検索にキーワードを追加した場合のみ、フォルダーとすべてのサブフォルダーです。 キーワードを追加しない場合、AEM はサブフォルダーを検索しません。

>



**[!UICONTROL 公開ステータス]**  — 公開ステータスに基づいてアセットをフィルタリングできます。 **** 非公開または **[!UICONTROL 公開済み。]** 「公開ステータス」を選択しない **[!UICONTROL 場合]**、AEMはデフォルトですべての公開ステータスを検索します。

![chlimage_1-247](assets/chlimage_1-247.png)
