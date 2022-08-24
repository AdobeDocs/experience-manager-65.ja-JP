---
title: ページに Dynamic Media Classic 機能を追加
description: Adobe Experience Manager で Dynamic Media Classic 機能およびコンポーネントをページに追加する方法。
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
ht-degree: 100%

---

# ページに Dynamic Media Classic 機能を追加 {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html?lang=ja) は、リッチメディアアセットを管理および拡張したり、web、モバイル、電子メール、インターネットに接続されたディスプレイやプリンターにリッチメディアアセットを公開および提供したりするためのホスト型ソリューションです。

Dynamic Media Classic で公開された Experience Manager アセットは、様々なビューアで表示できます。

* ズーム
* フライアウト
* ビデオ
* 画像テンプレート
* 画像

デジタルアセットを Experience Manager から Dynamic Media Classic に直接公開したり、Dynamic Media Classic から Experience Manager に公開したりできます。

このドキュメントでは、デジタルアセットを Experience Manager から Dynamic Media Classic に公開する方法と、その逆の方法について説明します。また、ビューアについても詳しく説明します。Dynamic Media Classic 用の Experience Manager の設定について詳しくは、 [Dynamic Media Classic と Experience Manager を統合](/help/sites-administering/scene7.md)を参照してください。

[画像マップを追加](image-maps.md)も参照してください。

Experience Manager でのビデオコンポーネントの使用について詳しくは、[ビデオ](video.md)を参照してください。

>[!NOTE]
>
>Dynamic Media Classic のアセットが適切に表示されない場合は、Dynamic Media が[無効](config-dynamic.md#disabling-dynamic-media)になっていることを確認してからページを更新してください。

## アセットから Dynamic Media Classic への手動公開 {#manually-publishing-to-scene-from-assets}

デジタルアセットは、次の手順で Dynamic Media Classic に公開できます。

* [クラシックユーザーインターフェイスを使用して Assets コンソールから](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [クラシックユーザーインターフェイスを使用してアセットから](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [クラシックユーザーインターフェイスを使用して CQ Target フォルダーの外側から](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>Experience Manager は Dynamic Media Classic に非同期で公開します。**[!UICONTROL 公開]**&#x200B;を選択した後、アセットが Dynamic Media Classic に公開されるまでに数秒かかります。

## Dynamic Media Classic コンポーネント {#scene-components}

次の Dynamic Media Classic コンポーネントを Experience Manager で使用できます。

* ズーム
* フライアウト (ズーム)
* 画像テンプレート
* 画像
* ビデオ

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できません。使用する前に **[!UICONTROL デザイン]** モードで選択しておく必要があります。

**[!UICONTROL デザイン]**&#x200B;モードで使用できるようになったら、他の Experience Manager コンポーネントと同様に、コンポーネントをページに追加できます。同期済みフォルダー内、ページ上、または Dynamic Media Classic クラウド設定を使用している場合、まだ Dynamic Media Classic に公開されていないアセットは Dynamic Media Classic に公開されます。

>[!NOTE]
>
>カスタムビューアを作成および開発する場合や、コンテンツファインダーを使用する場合は、`allowfullscreen` パラメーターを明示的に追加する必要があります。

### Flash ビューアのサポート終了に関するお知らせ {#flash-viewers-end-of-life-notice}

2017年1月31日（PT）をもって、Adobe Dynamic Media Classic は Flash ビューアプラットフォームのサポートを終了しました。

### ページに Dynamic Media Classic（Scene7）コンポーネントを追加 {#adding-a-scene-component-to-a-page}

ページに Dynamic Media Classic（Scene7）コンポーネントを追加する手順は、任意のページにコンポーネントを追加する手順と同様です。Dynamic Media Classic コンポーネントについて、以降の節で詳しく説明します。

**ページに Dynamic Media Classic（Scene7）コンポーネントを追加するには：**

1. **[!UICONTROL Dynamic Media Classic（Scene7）]**&#x200B;コンポーネントを追加するページを Experience Manager で開きます。

1. 使用できる Dynamic Media Classic コンポーネントがない場合は、**[!UICONTROL デザイン]**&#x200B;モードで、青い境界線の付いた任意のコンポーネントを選択し、**[!UICONTROL 親]**&#x200B;アイコン、 **[!UICONTROL 設定]**&#x200B;アイコンの順に選択します。「**[!UICONTROL ParSys（デザイン）]**」で、Dynamic Media Classic コンポーネントをすべて選択して使用可能にし、「**[!UICONTROL OK]**」を選択します。

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. 「**[!UICONTROL 編集]**」を選択すると、**[!UICONTROL 編集]**&#x200B;モードに戻ります。

1. コンポーネントをサイドキックの Dynamic Media Classic グループから目的の場所のページにドラッグします。

1. 「**[!UICONTROL 設定]**」アイコンを選択して、コンポーネントを開きます。

1. 必要に応じてコンポーネントを編集し、「**[!UICONTROL OK]**」を選択して変更内容を保存します。
1. コンテンツブラウザーから画像やビデオを、ページに追加した Dynamic Media Classic コンポーネントにドラッグします。

   >[!NOTE]
   >
   >タッチ UI に限り、画像やビデオを、ページに配置した Dynamic Media Classic コンポーネントにドラッグ＆ドロップする必要があります。Dynamic Media Classic コンポーネントを選択して編集した後にアセットを選択する操作はサポートされていません。

### レスポンシブサイトにインタラクティブな表示エクスペリエンスを追加 {#adding-interactive-viewing-experiences-to-a-responsive-website}

アセットのレスポンシブデザインとは、表示先に合わせてアセットが調整されることを意味します。レスポンシブデザインを使用すると、同じアセットを複数のデバイスで効果的に表示できます。

[Web ページのレスポンシブデザイン](/help/sites-developing/responsive.md)も参照してください。

**レスポンシブサイトにインタラクティブな表示エクスペリエンスを追加するには：**

1. Experience Manager にログインし、[Adobe Dynamic Media Classic Cloud Services を設定済み](/help/sites-administering/scene7.md#configuring-scene-integration)であることと、Dynamic Media Classic コンポーネントが使用可能であることを確認します。

   >[!NOTE]
   >
   >Dynamic Media Classic コンポーネントが使用可能になっていない場合は、[デザインモードで有効に](/help/sites-authoring/default-components-designmode.md)してください。

1. **[!UICONTROL Dynamic Media Classic]** コンポーネントが有効になっている web サイトで、**[!UICONTROL 画像]**&#x200B;コンポーネントをページにドラッグします。
1. コンポーネントを選択し、設定アイコンを選択します。
1. 「**[!UICONTROL Dynamic Media Classic の設定]**」タブで、ブレークポイントを調整します。

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. ビューアがレスポンシブにサイズ変更され、すべてのインタラクションがデスクトップ、タブレットおよびモバイル用に最適化されていることを確認します。

### すべての Dynamic Media Classic コンポーネントに共通の設定 {#settings-common-to-all-scene-components}

様々な設定オプションがありますが、次のオプションはすべての [!UICONTROL Dynamic Media Classic] コンポーネントに共通です。

* **[!UICONTROL ファイル参照]** - 参照するファイルを探します。ファイル参照には、アセットの URL が表示されます。これは必ずしも、URL コマンドおよびパラメーターを含む Dynamic Media Classic の完全な URL ではありません。このフィールドに Dynamic Media Classic の URL コマンドおよびパラメーターを追加することはできません。代わりに、コンポーネントの対応する機能を使用して追加します。
* **[!UICONTROL 幅]** - 幅を設定できます。
* **[!UICONTROL 高さ]** - 高さを設定できます。

これらの設定オプションは、Dynamic Media Classic コンポーネントを開く（ダブルクリックする）ことで設定できます。例えば、**[!UICONTROL ズーム]**&#x200B;コンポーネントを開いた場合は、次のようになります。

![chlimage_1-226](assets/chlimage_1-226.png)

### ズーム {#zoom}

HTML5 ズームコンポーネントでは、「**[!UICONTROL +]**」ボタンをクリックすると画像のサイズが拡大されます。

アセットの下部にはズームツールが用意されています。拡大する場合は「**[!UICONTROL +]**」を選択し、縮小する場合は「**[!UICONTROL -]**」を選択します。「**[!UICONTROL x]**」またはズームのリセット矢印をタップすると、画像が元の（読み込み時の）サイズに戻ります。斜めの矢印を選択すると、フルスクリーンモードになります。「**[!UICONTROL 編集]**」を選択すると、コンポーネントを設定できます。このコンポーネントを使用すると、[[!UICONTROL Dynamic Media Classic] のすべてのコンポーネントに共通の設定](#settings-common-to-all-scene-components)を指定できます。

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### フライアウト {#flyout}

HTML5 **[!UICONTROL フライアウト]**&#x200B;コンポーネントでは、アセットが分割画面として表示されます。左側にはアセットが指定されたサイズで表示され、右側にはズーム部分が表示されます。「**[!UICONTROL 編集]**」を選択して、コンポーネントを設定します。このコンポーネントを使用すると、[Dynamic Media Classic のすべてのコンポーネントに共通の設定](#settings-common-to-all-scene-components)を指定できます。

>[!NOTE]
>
>**[!UICONTROL フライアウト]**&#x200B;コンポーネントでカスタムサイズを使用している場合は、そのカスタムサイズが使用され、コンポーネントのレスポンシブ設定は無効になります。
>
>**[!UICONTROL フライアウト]**&#x200B;コンポーネントでデフォルトサイズ（**[!UICONTROL デザインビュー]**&#x200B;で設定されたもの）を使用している場合は、そのデフォルトサイズが使用され、コンポーネントのレスポンシブ設定を有効にしていれば、ページレイアウトサイズに合わせてコンポーネントが拡大されます。コンポーネントのレスポンシブ設定には制限があります。レスポンシブ設定と&#x200B;**[!UICONTROL フライアウト]**&#x200B;コンポーネントを使用する場合は、全ページ拡大で使用しないでください。そうしないと、**[!UICONTROL フライアウト]**&#x200B;がページの右端からはみ出してしまう可能性があります。

![chlimage_1-228](assets/chlimage_1-228.png)

### 画像 {#image}

Dynamic Media Classic の&#x200B;**[!UICONTROL 画像]**&#x200B;コンポーネントを使用すると、Dynamic Media Classic の修飾子、画像またはビューアのプリセット、シャープニングなどといった Dynamic Media Classic 機能を画像に追加できます。Dynamic Media Classic の&#x200B;**[!UICONTROL 画像]**&#x200B;コンポーネントは、Experience Manager の他の画像コンポーネントと似ていますが、Dynamic Media Classic 専用の機能も備えています。この例では、画像に Dynamic Media Classic の URL 修飾子である `&op_invert=1` が適用されています。

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL タイトル、代替テキスト]** - 「**[!UICONTROL 詳細]**」タブでは画像にタイトルを追加し、グラフィックの表示をオフにしているユーザー向けに代替テキストを追加します。

**[!UICONTROL URL、次のウィンドウで開く]** - アセットを設定してリンクを開くことができます。「**[!UICONTROL URL]**」と「**[!UICONTROL 次のウィンドウで開く]**」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL ビューアプリセット]** - ドロップダウンメニューから既存のビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示できるように設定する必要があります。詳しくは、[ビューアプリセットの管理](/help/assets/managing-viewer-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL Dynamic Media Classic Configuration]** - SPS からアクティブな画像プリセットを取得するために使用する Dynamic Media Classic 設定を選択します。

**[!UICONTROL 画像プリセット]** - ドロップダウンメニューから既存の画像プリセットを選択します。探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。[画像プリセットの管理](/help/assets/managing-image-presets.md)を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**[!UICONTROL 出力形式]** - 画像の出力形式（例：jpeg）を選択します。選択する出力形式によっては、追加の設定オプションがあります。[画像プリセットのベストプラクティス](/help/assets/managing-image-presets.md#image-preset-options)を参照してください。

**[!UICONTROL シャープニング]** - 画像にシャープニングを適用する方法を選択します。シャープニングについて詳しくは、[画像プリセットのベストプラクティス](/help/assets/managing-image-presets.md#image-preset-options)および[シャープニングのベストプラクティス](/help/assets/assets/sharpening_images.pdf)を参照してください。

**[!UICONTROL URL 修飾子]** — 追加の Dynamic Media Classic 画像コマンドを指定して、画像エフェクトを変更できます。これらのコマンドは[画像プリセット](/help/assets/managing-image-presets.md)および[コマンドリファレンス](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=ja)で説明されています。

**[!UICONTROL ブレークポイント]** - レスポンシブ web サイトでは、ブレークポイントの調整が必要な場合があります。ブレークポイントはコンマ（,）で区切る必要があります。

### 画像テンプレート {#image-template}

[Dynamic Media Classic 画像テンプレート](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html?lang=ja) は、Dynamic Media Classic にインポートされたレイヤー化された Photoshop コンテンツで、可変性を考慮してコンテンツとプロパティがパラメーター化されています。**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを使用すると、Experience Manager で画像をインポートしてテキストを動的に変更できます。また、ClientContext の値を使用するように&#x200B;**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを設定できます。これにより、各ユーザーが個別に画像を活用できます。

コンポーネントを設定する場合は「**[!UICONTROL 編集]**」を選択します。[すべての Dynamic Media Classic コンポーネントに共通の設定](#settings-common-to-all-scene-components)およびこの節で説明するその他の設定を指定できます。

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL ファイル参照、幅、高さ]** - すべての ScDynamic Media Classicene7 コンポーネントに共通の設定を参照してください。

>[!NOTE]
>
>Dynamic Media Classic の URL コマンドおよびパラメーターを「ファイル参照」の URL に直接追加することはできません。これらは、**[!UICONTROL パラメーター]**&#x200B;パネルのコンポーネントの UI でのみ定義できます。

**[!UICONTROL タイトル、代替テキスト]** - 「Dynamic Media Classic 画像テンプレート」タブでは、グラフィックの表示をオフにしているユーザー向けの画像と代替テキストにタイトルを追加します。

**[!UICONTROL URL、次のウィンドウで開く]** - リンクを開くようにアセットを設定できます。「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL パラメーターパネル]** - 画像をインポートすると、その画像の情報がパラメーターに設定されます。動的に変更できるコンテンツがない場合、このウィンドウは空になります。

![chlimage_1-233](assets/chlimage_1-233.png)

#### テキストを動的に変更 {#changing-text-dynamically}

テキストを動的に変更するには、フィールドに新しいテキストを入力して、「**[!UICONTROL OK]**」をクリックします。この例では、「**[!UICONTROL 価格]**」が 50 ドルで、送料が 99 セントです。

![chlimage_1-234](assets/chlimage_1-234.png)

画像内のテキストが変更されます。フィールドの横にある「**[!UICONTROL リセット]**」をタップすると、テキストを元の値に戻すことができます。

![chlimage_1-235](assets/chlimage_1-235.png)

#### クライアントコンテキストの値を反映してテキストを変更 {#changing-text-to-reflect-the-value-of-a-client-context-value}

フィールドをクライアントコンテキストの値にリンクするには、「**[!UICONTROL 選択]**」をクリックしてクライアントコンテキストのメニューを開き、クライアントコンテキストを選択して「**[!UICONTROL OK]**」をクリックします。この例では、「名前」フィールドとプロファイル内の書式設定された名前とのリンクに基づいて名前が変わります。

![chlimage_1-236](assets/chlimage_1-236.png)

現在ログインしているユーザーの名前がテキストに反映されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-237](assets/chlimage_1-237.png)

#### Dynamic Media Classic 画像テンプレートをリンクにする {#making-the-scene-image-template-a-link}

1. Dynamic Media Classic **[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを含むページ上で、**[!UICONTROL 編集]**&#x200B;を選択します。
1. 「**[!UICONTROL URL]**」フィールドに、ユーザーが画像をタップしたときに表示される URL を入力します。「**[!UICONTROL 次のウィンドウで開く]**」フィールドで、ターゲットを新しいウィンドウと同じウィンドウのどちらで開くかを選択します。

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 「**[!UICONTROL OK]**」を選択します。

### ビデオコンポーネント {#video-component}

Dynamic Media Classic **[!UICONTROL ビデオ]**&#x200B;コンポーネント（サイドキックの「Dynamic Media Classic」セクションから使用可能）では、デバイスと帯域幅の検出を使用して、適切なビデオをそれぞれの画面に提供します。このコンポーネントは HTML5 ビデオプレーヤー（チャネルを超えて使用可能な単一のビューア）です。

このコンポーネントはアダプティブビデオセット（単一の MP4 ビデオまたは単一の F4V ビデオ）で使用できます。

ビデオが Dynamic Media Classic 統合でどのように機能するかに関する詳細は、[ビデオ](s7-video.md)を参照してください。また、 [Dynamic Media Classicビデオコンポーネントと基盤ビデオコンポーネントの比較](s7-video.md)も参照してください。

![chlimage_1-239](assets/chlimage_1-239.png)

### ビデオコンポーネントに関する既知の制限事項 {#known-limitations-for-the-video-component}

Adobe DAM および WCM が、プライマリソースビデオがアップロードされたかどうかを示します。次に示すプロキシアセットは表示されません。

* Dynamic Media Classic のエンコードされたレンディション
* Dynamic Media Classic アダプティブビデオセット

Dynamic Media Classic ビデオコンポーネントでアダプティブビデオセットを使用する場合、ビデオのサイズに合わせてコンポーネントのサイズを変更する必要があります。

## Dynamic Media Classic コンテンツブラウザー {#scene-content-browser}

Dynamic Media Classic のコンテンツブラウザーを使用すると、Dynamic Media Classic のコンテンツを直接 Experience Manager で表示できます。コンテンツブラウザーにアクセスするには、**[!UICONTROL コンテンツファインダー]**&#x200B;で、タッチ操作向けユーザーインターフェイスの「**[!UICONTROL Dynamic Media Classic]**」またはクラシックインターフェイスの&#x200B;**[!UICONTROL S7]**&#x200B;アイコンを選択します。どちらのユーザーインターフェイスを使用しても、機能は同じです。

設定が複数ある場合、Experience Manager ではデフォルトで[デフォルト設定](/help/sites-administering/scene7.md#configuring-a-default-configuration)が表示されます。Dynamic Media Classic コンテンツブラウザーのドロップダウンメニューで、別の設定を直接選択できます。

>[!NOTE]
>
>* オンデマンドフォルダー内のアセットは、Dynamic Media Classic コンテンツブラウザーに表示されません。
>* [セキュアプレビューが有効](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)に設定されている場合、Dynamic Media Classic 上の公開済みアセットと未公開アセットの両方が Dynamic Media Classic コンテンツブラウザーに表示されます。
>* コンテンツブラウザーに&#x200B;**[!UICONTROL Dynamic Media Classic]** または **[!UICONTROL S7]**&#x200B;アイコンがオプションとして表示されない場合は、 [Dynamic Media Classic が Experience Manager と連携するように設定](/help/sites-administering/scene7.md)しなければなりません。
>* ビデオの場合、Dynamic Media Classic コンテンツブラウザーは次の項目をサポートしています。
   >
   >   * アダプティブビデオセット：複数の Screens でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
   >   * 単一の MP4 ビデオ
   >   * 単一の F4V ビデオ


### タッチ操作向け UI でのコンテンツを参照 {#browsing-content-in-the-touch-optimized-ui}

タッチ対応 UI またはクラシック UI を使用してコンテンツブラウザーにアクセスできます。現時点では、タッチ対応 UI には次の制限事項があります。

* Dynamic Media Classic の FXG および Flash のアセットはサポートされていません。

3 番目のドロップダウンメニューから「**[!UICONTROL Dynamic Media Classic]**」を選択して、Dynamic Media Classic アセットを参照します。Dynamic Media Classic/Experience Manager の統合を設定していない場合、Dynamic Media Classic はリストに表示されません。

>[!NOTE]
>
>* Dynamic Media Classic コンテンツブラウザーは、約 100 個のアセットを読み込んで、名前順に並べ替えます。
>* セキュリティで保護されたプレビューサーバーが設定されている場合、ブラウザーはそのプレビューサーバーを使用してサムネールとアセットをレンダリングします。
>


![chlimage_1-240](assets/chlimage_1-240.png)

また、ブラウザー内でアセットの上にマウスポインターを置くと、解像度の情報、サイズ、変更後の日数およびファイル名を参照できます。

![chlimage_1-241](assets/chlimage_1-241.png)

* アダプティブビデオセットとテンプレートの場合は、サムネール用のサイズ情報が生成されません。
* アダプティブビデオセットの場合は、サムネール用の解像度が生成されません。

### コンテンツブラウザーでの Dynamic Media Classic アセットの検索 {#searching-for-scene-assets-with-the-content-browser}

Dynamic Media Classic でのアセットの検索は、Experience Manager Assets でのアセットの検索と類似しています。ただし、検索時に、Experience Manager にアセットを直接インポートするのではなく、実際には Dynamic Media Classic システム内のアセットのリモートビューが表示されます。

クラシック UI またはタッチ操作向け UI を使用して、アセットを表示および検索できます。インターフェイスによって検索方法は多少異なります。

どちらの UI で検索する場合でも、次の基準でフィルターを適用できます（ここでは、タッチ操作向け UI を示しています）。

**[!UICONTROL キーワードを入力]** - アセットを名前で検索できます。検索時には、入力したキーワードで始まるファイル名が検索されます。例えば、「swimming」という単語を入力すると、入力した順序どおりの文字列で始まるアセットファイルの名前が検索されます。アセットを検索するには、語句を入力した後に Enter キーを押してください。

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL フォルダー／パス]** - 表示されるフォルダーの名前は、選択した設定に基づいています。下位にドリルダウンするには、フォルダーアイコンをタップしてサブフォルダーを選択し、チェックマークをタップして選択します。

キーワードを入力してフォルダーを選択すると、Experience Manager でそのフォルダーとすべてのサブフォルダーが検索されます。ただし、検索時にキーワードを入力しない場合は、フォルダーを選択してもそのフォルダー内のアセットしか表示されず、サブフォルダーは含まれません。

デフォルトでは、Experience Manager は選択されたフォルダーとすべてのサブフォルダーを検索します。

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL アセットのタイプ]** - **[!UICONTROL Dynamic Media Classic]** を選択して、Dynamic Media Classic のコンテンツを参照します。このオプションは、Dynamic Media Classic が設定されている場合にのみ使用できます。

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 設定]** - Dynamic Media Classic の設定が[!UICONTROL クラウドサービス]で複数定義されている場合は、ここで選択できます。その結果、選択した設定に応じてフォルダーが変わります。

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL アセットタイプ]** - Dynamic Media Classic ブラウザー内では、結果にフィルターを適用して、画像、テンプレート、ビデオ、アダプティブビデオセットのいずれかを抽出することができます。アセットタイプを選択しない場合、Experience Manager ではデフォルトですべてのアセットタイプが検索されます。

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* クラシック UI では、**Flash** と **FXG** も検索できます。タッチ操作向け UI では、これらのタイプのフィルタリングはサポートされていません。
>
>* ビデオを検索するときは、単一のレンディションが検索されています。結果には、元のレンディション（&amp;ast;.mp4 のみ）と、エンコードされたレンディションが返されます。
>* アダプティブビデオセットを検索する場合は、フォルダーとすべてのサブフォルダーが検索されます（検索にキーワードを追加した場合のみ）。キーワードを追加しないと、Experience Manager ではサブフォルダーが検索されません。
>


**[!UICONTROL 公開ステータス]** - 公開ステータス（**[!UICONTROL 非公開]**&#x200B;または&#x200B;**[!UICONTROL 公開済み]**）に基づいてアセットをフィルタリングできます。**[!UICONTROL 公開ステータス]**&#x200B;を選択しない場合、Experience Manager ではデフォルトですべての公開ステータスが検索されます。

![chlimage_1-247](assets/chlimage_1-247.png)
