---
title: ページへの Dynamic Media Classic（Scene7）機能の追加
description: Adobe Dynamic Media Classic（Scene7）は、リッチメディアアセットを管理および拡張したり、web、モバイル、電子メール、インターネットに接続されたディスプレイやプリンターにリッチメディアアセットを公開および提供したりするためのホスト型ソリューションです。
uuid: dc463e2d-a452-490e-88af-f79bdaa3b089
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dc0191d0-f181-4e1e-b3f4-73427aa22073
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: ht
source-wordcount: '3511'
ht-degree: 100%

---

# ページへの Dynamic Media Classic（Scene7）機能の追加{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic（Scene7）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html?lang=ja)は、リッチメディアアセットを管理および拡張したり、web、モバイル、電子メール、インターネットに接続されたディスプレイやプリンターにリッチメディアアセットを公開および提供したりするためのホスト型ソリューションです。

Dynamic Media Classic（Scene7）で公開された Experience Manager Assets を、様々なビューアで表示できます。

* ズーム
* フライアウト
* ビデオ
* 画像テンプレート
* 画像

デジタルアセットを Experience Manager から Dynamic Media Classic（Scene7）に直接公開したり、Dynamic Media Classic（Scene7）から Experience Manager に公開したりできます。

このドキュメントでは、デジタルアセットを Experience Manager から Dynamic Media Classic（Scene7）に公開する方法と、その逆の方法について説明します。また、ビューアについても詳しく説明します。Dynamic Media Classic（Scene7）用の Experience Manager の設定について詳しくは、[Dynamic Media Classic（Scene7）と Experience Manager の統合](/help/sites-administering/scene7.md)を参照してください。

[画像マップの追加](/help/assets/image-maps.md)も参照してください。

Experience Manager でのビデオコンポーネントの使用について詳しくは、以下を参照してください。

* [ビデオ](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Dynamic Media Classic（Scene7）のアセットが適切に表示されない場合は、Dynamic Media が[無効](/help/assets/config-dynamic.md#disabling-dynamic-media)になっていることを確認してからページを更新してください。

## Assets から Dynamic Media Classic（Scene7）への手動による公開 {#manually-publishing-to-scene-from-assets}

クラシック UI のアセットコンソールから、またはアセットから直接 Dynamic Media Classic（Scene7）にデジタルアセットを公開できます。

>[!NOTE]
>
>Experience Manager は、Dynamic Media Classic（Scene7）に非同期で公開します。「**[!UICONTROL 公開]**」をクリックした後、アセットを Dynamic Media Classic（Scene7）に公開するまでに数秒かかる場合があります。

### Assets コンソールからの公開 {#publishing-from-the-assets-console}

アセットが Dynamic Media Classic（Scene7）のターゲットフォルダーにある場合は、Assets コンソールから Dynamic Media Classic（Scene7）に公開できます。

1. Experience Manager のクラシック UI で、「**[!UICONTROL デジタルアセット]**」をクリックして、Digital Asset Manager にアクセスします。

1. Dynamic Media Classic（Scene7）に公開するターゲットフォルダー内からアセットまたはフォルダーを選択して右クリックし、「**[!UICONTROL Dynamic Media Classic（Scene7）に発行]**」を選択します。または、**[!UICONTROL ツール]**&#x200B;メニューの「**[!UICONTROL Dynamic Media Classic（Scene7）に公開]**」を選択できます。

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. Dynamic Media Classic（Scene7）に移動して、アセットが使用可能であることを確認します。

   >[!NOTE]
   >
   >同期された Dynamic Media Classic（Scene7）フォルダーにアセットがない場合、どちらのメニューにも「**[!UICONTROL Dynamic Media Classic（Scene7）に公開]**」と表示されますが、無効になっています。

### アセットからの公開 {#publishing-from-an-asset}

同期された Dynamic Media Classic（Scene7）フォルダー内にアセットがある場合は、そのアセットを手動で公開できます。

>[!NOTE]
>
>アセットが Dynamic Media Classic（Scene7）の同期済みフォルダーにない場合、**[!UICONTROL Dynamic Media Classic（Scene7）に公開]**&#x200B;へのリンクが表示されません。

デジタルアセットから Dynamic Media Classic（Scene7）に直接公開するには：

1. Experience Manager で、「**[!UICONTROL デジタルアセット]**」をクリックして、Digital Asset Manager にアクセスします。

1. アセットをダブルクリックして開きます。

1. アセットの詳細パネルで、「**[!UICONTROL Dynamic Media Classic（Scene7）に公開]**」を選択します。

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. リンクが「**[!UICONTROL 公開中…]**」となった後、「**[!UICONTROL 公開済み]**」に変わります。Dynamic Media Classic（Scene7）に移動し、アセットが使用可能であることを確認します。

   >[!NOTE]
   >
   >アセットが Dynamic Media Classic（Scene7）に適切に公開されない場合は、リンクが「**[!UICONTROL 公開に失敗]**」に変わります。アセットが既に Dynamic Media Classic（Scene7）に公開されている場合は、リンクが「**[!UICONTROL Dynamic Media Classic（Scene7）に再公開]**」に変わります。再公開すると、Experience Manager でアセットを変更し、再公開できます。

### CQ のターゲットフォルダー以外からのアセットの公開 {#publishing-assets-from-outside-the-cq-target-folder}

アドビでは、Dynamic Media Classic（Scene7）のターゲットフォルダー内のアセットからのみ Dynamic Media Classic（Scene7）にアセットを公開することをお勧めします。ただし、ターゲットフォルダー以外のフォルダーからアセットをアップロードする必要がある場合は、Dynamic Media Classic（Scene7）のアドホックフォルダーにアセットをアップロードすると、アセットを公開できます。まず、アセットを表示するページのクラウド設定を指定します。次に、Dynamic Media Classic（Scene7）コンポーネントをページに追加して、そのコンポーネント上にアセットをドラッグ＆ドロップします。そのページのページプロパティの設定が完了した後、Dynamic Media Classic（Scene7）にアップロードするためのトリガーを選択すると、「**[!UICONTROL Dynamic Media Classic（Scene7）に公開]**」リンクが表示されます。

>[!NOTE]
>
>オンデマンドフォルダー内のアセットは、Dynamic Media Classic（Scene7）コンテンツブラウザーには表示されません。

**CQ のターゲットフォルダー以外にあるアセットを公開するには：**

1. Experience Manager のクラシック UI で、「**[!UICONTROL Web サイト]**」を選択して、Dynamic Media Classic（Scene7）にまだ公開されていないデジタルアセットを追加する web ページに移動します。（通常のページ継承ルールが適用されます）。

1. サイドキックで「**[!UICONTROL ページ]**」アイコンを選択し、「**[!UICONTROL ページプロパティ]**」を選択します。

1. 「**[!UICONTROL Cloud Services]**」を選択します。
1. 「**[!UICONTROL サービスを追加]**」を選択します。
1. 「**[!UICONTROL Dynamic Media Classic （Scene7）]**」を選択します。
1. 「**[!UICONTROL Adobe Dynamic Media Classic （Scene7）]**」ドロップダウンリストで目的の設定を選択して、「**[!UICONTROL OK]**」を選択します。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Web ページで、ページの目的の場所に Dynamic Media Classic（Scene7）コンポーネントを追加します。
1. コンテンツファインダーから、デジタルアセットをコンポーネントにドラッグします。**[!UICONTROL Dynamic Media Classic （Scene7） 公開ステータスの確認]**&#x200B;へのリンクが表示されます。

   >[!NOTE]
   >
   >デジタルアセットが CQ ターゲットフォルダー内にある場合、**[!UICONTROL Dynamic Media Classic （Scene7） 公開ステータスの確認]**&#x200B;へのリンクは表示されません。アセットがコンポーネントに配置されます。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. 「**[!UICONTROL Dynamic Media Classic （Scene7） 公開ステータスの確認]**」を選択します。アセットが公開されていない場合、Experience Manager はアセットを Dynamic Media Classic（Scene7）に公開します。アップロードされたアセットは、オンデマンドフォルダーに配置されます。デフォルトでは、オンデマンドフォルダーは **[!UICONTROL name_of_the_company/CQ5_adhoc]** にあります。[必要に応じて、オンデマンドフォルダーを設定](#configuringtheadhocfolder)することができます。

   >[!NOTE]
   >
   >同期された Dynamic Media Classic（Scene7）フォルダーにアセットがなく、Dynamic Media Classic（Scene7）のクラウド設定が現在のページに関連付けられていない場合は、アップロードが失敗します。

## Dynamic Media Classic（Scene7）コンポーネント {#scene-components}

Experience Manager で使用できる Dynamic Media Classic（Scene7）コンポーネントは次のとおりです。

* ズーム
* フライアウト（ズーム）
* 画像テンプレート
* 画像
* ビデオ

>[!NOTE]
>
>これらのコンポーネントはデフォルトでは使用できません。使用する前にデザインモードで選択しておく必要があります。

デザインモードで使用できるようになったら、他の Experience Manager コンポーネントと同様に、コンポーネントをページに追加できます。まだ Dynamic Media Classic（Scene7）に公開されていないアセットは、同期フォルダーやページに配置するか、Dynamic Media Classic（Scene7）クラウド設定を使用することで、Dynamic Media Classic（Scene7）に公開されます。

>[!NOTE]
>
>カスタム S7 ビューアを作成および開発する場合や、コンテンツファインダーを使用する場合は、`allowfullscreen` パラメーターを明示的に追加する必要があります。

### Flash ビューアのサポート終了に関する通知 {#flash-viewers-end-of-life-notice}

2017年1月31日（PT）付けで、Adobe Dynamic Media Classic（Scene7）は Flash ビューアプラットフォームのサポートを正式に終了しました。

### ページへの Dynamic Media Classic（Scene7）コンポーネントの追加 {#adding-a-scene-component-to-a-page}

ページに Dynamic Media Classic（Scene7）コンポーネントを追加する手順は、ページに任意のコンポーネントを追加する手順と同様です。以降のセクションで、Dynamic Media Classic（Scene7）コンポーネントについて詳しく説明します。

クラシック UI を使用して、ページに Dynamic Media Classic（Scene7）コンポーネント／ビューアを追加するには：

1. Dynamic Media Classic（Scene7）コンポーネントを追加するページを Experience Manager で開きます。

1. 使用できる Dynamic Media Classic（Scene7）コンポーネントがない場合は、サイドキックにある定規アイコンを選択して&#x200B;**デザイン**&#x200B;モードに切り替え、parsys の「**[!UICONTROL 編集]**」を選択し、**[!UICONTROL Dynamic Media Classic（Scene7）]** コンポーネントをすべて選択して使用可能にします。

1. サイドキックにある鉛筆を選択して、**編集**&#x200B;モードに戻ります。

1. サイドキックの **[!UICONTROL Dynamic Media Classic（Scene7）]**&#x200B;グループから目的の場所にあるページにコンポーネントをドラッグします。

1. コンポーネントを開くことができるように、「**[!UICONTROL 編集]**」を選択します。

1. 必要に応じてコンポーネントを編集し、「**[!UICONTROL OK]**」を選択して変更内容を保存します。

### レスポンシブ web サイトへのインタラクティブな表示エクスペリエンスの追加 {#adding-interactive-viewing-experiences-to-a-responsive-website}

アセットのレスポンシブデザインとは、表示対象にアセットを適応させることを意味します。レスポンシブデザインを使用すると、同じアセットを複数のデバイスで効果的に表示できます。

クラシック UI を使用して、レスポンシブサイトにインタラクティブな表示エクスペリエンスを追加するには：

1. Experience Manager にログインし、 [Adobe Dynamic Media Classic（Scene7）Cloud Services を設定](/help/sites-administering/scene7.md#configuring-scene-integration)済みであることと、Dynamic Media Classic（Scene7）コンポーネントが使用できることを確認します。

   >[!NOTE]
   >
   >Dynamic Media Classic（Scene7）の WCM コンポーネントが利用できない場合は、必ずデザインモードで有効にしてください。

1. Dynamic Media Classic（Scene7）コンポーネントを有効にした web サイトで、**[!UICONTROL 画像]**&#x200B;ビューアをページにドラッグします。
1. コンポーネントを編集し、「**[!UICONTROL Dynamic Media Classic （Scene7） 設定]**」タブでブレークポイントを調整します。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. ビューアがレスポンシブにサイズ変更され、すべてのインタラクションがデスクトップ、タブレットおよびモバイル用に最適化されていることを確認します。

### すべての Dynamic Media Classic（Scene7）コンポーネントに共通の設定 {#settings-common-to-all-scene-components}

設定オプションはさまざまですが、以下は Dynamic Media Classic（Scene7）の全コンポーネントに共通です。

* **ファイル参照** - 参照するファイルを探します。ファイル参照は、アセット URL を示し、URL コマンドやパラメーターを含んだ完全な Dynamic Media Classic（Scene7）URL であるとは限りません。Dynamic Media Classic（Scene7）の URL コマンドおよびパラメーターをこのフィールドに追加することはできません。代わりに、コンポーネントの対応する機能を通じて追加する必要があります。
* **幅** - 幅を設定できます。
* **高さ** - 高さを設定できます。

これらの設定オプションは、例えば、**ズーム** コンポーネントを開いたときに Dynamic Media Classic（Scene7）コンポーネントを開いて（ダブルクリックして）設定します。

![chlimage_1-52](assets/chlimage_1-52.png)

### ズーム {#zoom}

HTML5 ズームコンポーネントでは、「+」ボタンをクリックすると画像のサイズが拡大されます。

アセットの下部にはズームツールが用意されています。「**[!UICONTROL +]**」を選択すると、拡大します。「**[!UICONTROL -]**」を選択すると、縮小します。「**[!UICONTROL x]**」またはズームのリセット矢印を選択すると、画像が元の（インポート時の）サイズに戻ります。斜めの矢印を選択すると、全画面表示にすることができます。「**[!UICONTROL 編集]**」を選択すると、コンポーネントを設定できます。このコンポーネントでは、[すべての Dynamic Media Classic（Scene7）コンポーネントに共通する設定](#settings-common-to-all-scene-components)を指定できます。

![](do-not-localize/chlimage_1-3.png)

### フライアウト {#flyout}

HTML5 フライアウトコンポーネントでは、アセットが分割画面として表示されます。左側には、アセットが指定されたサイズで表示され、右側には、ズーム部分が表示されます。「**[!UICONTROL 編集]**」を選択すると、コンポーネントを設定できます。このコンポーネントでは、[すべての Dynamic Media Classic（Scene7）コンポーネントに共通する設定](/help/sites-administering/scene7.md#settingscommontoallscene7components)を指定できます。

>[!NOTE]
>
>フライアウトコンポーネントでカスタムサイズを使用する場合は、そのカスタムサイズが使用され、コンポーネントのレスポンシブ設定は無効になります。
>
>フライアウトコンポーネントが、デザインビューで設定されたデフォルトのサイズを使用している場合、デフォルトのサイズが使用されます。コンポーネントのレスポンシブ設定を有効にすると、ページレイアウトのサイズに合わせてコンポーネントが伸縮します。ただし、コンポーネントのレスポンシブ設定には制限があります。フライアウトコンポーネントをレスポンシブ設定で使用する場合は、全ページ拡大で使用しないでください。そうしないと、フライアウトがページの右側のボーダーを超えてしまう可能性があります。

![chlimage_1-53](assets/chlimage_1-53.png)

### 画像 {#image}

Dynamic Media Classic（Scene7）画像コンポーネントでは、Dynamic Media Classic（Scene7）の修飾子、画像またはビューアプリセット、シャープニングなどの機能を画像に追加することが可能です。Dynamic Media Classic（Scene7）画像コンポーネントは、Experience Manager の他のイメージコンポーネントと同様で、Dynamic Media Classic（Scene7）の特別な機能を備えています。この例では、画像に Dynamic Media Classic（Scene7）の URL 修飾子である `&op_invert=1` が適用されています。

![](do-not-localize/chlimage_1-4.png)

**タイトル、代替テキスト** - 「詳細」タブで、画像にタイトルを追加し、グラフィックスをオフにしているユーザーのために代替テキストを追加します。

**URL、次のウィンドウで開く** - リンクを開く元となるアセットを設定することができます。「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-54](assets/chlimage_1-54.png)

**ビューアプリセット** - ドロップダウンメニューから既存のビューアプリセットを選択します。探しているビューアプリセットが表示されない場合は、表示可能に設定する必要があります。詳しくは、ビューアプリセットの管理を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**Dynamic Media Classic （Scene7） 設定** - SPS からアクティブな画像プリセットを取得するための Dynamic Media Classic（Scene7）設定を選択します。

**画像プリセット** - ドロップダウンメニューから既存の画像プリセットを選択します。探している画像プリセットが表示されない場合は、表示できるように設定する必要があります。「画像プリセットの管理」を参照してください。画像プリセットを使用している場合は、ビューアプリセットを選択できません。逆の場合も同様です。

**出力形式** - 画像の出力形式（例：jpeg）を選択します。選択する出力形式によっては、追加の設定オプションが表示される場合があります。画像プリセットのベストプラクティスを参照してください。

 **シャープニング** - 画像のシャープニング方法を選択します。シャープニングについて詳しくは、画像プリセットのベストプラクティスおよびシャープニングのベストプラクティスを参照してください。

**URL 修飾子** - 追加の S7 画像コマンドを指定して、画像エフェクトを変更できます。詳しくは、「画像プリセット」および「コマンドリファレンス」を参照してください。

**ブレークポイント** - レスポンシブ web サイトでは、ブレークポイントの調整が必要な場合があります。ブレークポイントはコンマ（,）で区切って指定してください。

### 画像テンプレート {#image-template}

Dynamic Media Classic（Scene7）画像テンプレートは、Scene7 にインポートされたレイヤー化された Photoshop コンテンツで、可変性を考慮してコンテンツとプロパティがパラメーター化されています。**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを使用すると、Experience Manager に画像をインポートして、テキストを動的に変更できます。また、ClientContext の値を使用するように&#x200B;**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを設定できます。これにより、各ユーザーが個別に画像を活用できます。

コンポーネントを設定するには、「**[!UICONTROL 編集]**」をクリックします。[すべての Dynamic Media Classic（Scene7）コンポーネントに共通の設定](/help/sites-administering/scene7.md#settingscommontoallscene7components)と、この節で説明しているその他の設定を指定できます。

![chlimage_1-55](assets/chlimage_1-55.png)

**ファイル参照、幅、高さ** - [すべての Dynamic Media Classic（Scene7）コンポーネントに共通の設定](/help/sites-administering/scene7.md#settingscommontoallscene7components)を参照してください。

>[!NOTE]
>
>Dynamic Media Classic（Scene7）の URL コマンドおよびパラメーターを「ファイル参照」の URL に直接追加することはできません。これらは、**[!UICONTROL パラメーター]**&#x200B;パネルのコンポーネントの UI でのみ定義できます。

**タイトルと代替テキスト** -「Dynamic Media Classic （Scene7） 画像テンプレート」タブでは、画像のタイトルや、グラフィックの表示をオフにしているユーザー向けの代替テキストを追加できます。

**URL、次のウィンドウで開く** - リンクを開くようにアセットを設定できます。「URL」と「次のウィンドウで開く」で、同じウィンドウで開くか新しいウィンドウで開くかを指定します。

![chlimage_1-56](assets/chlimage_1-56.png)

**パラメーター パネル** - 画像をインポートすると、その画像の情報がパラメーターに設定されます。動的に変更できるコンテンツがない場合、このウィンドウには何も表示されません。

![chlimage_1-57](assets/chlimage_1-57.png)

#### テキストの動的な変更 {#changing-text-dynamically}

テキストを動的に変更するには、フィールドに新しいテキストを入力して、「 **[!UICONTROL OK]**」をクリックします。この例では、「**価格**」が $50 で、送料が 99 セントです。

![chlimage_1-58](assets/chlimage_1-58.png)

画像内のテキストが変更されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-59](assets/chlimage_1-59.png)

#### テキストへの ClientContext 値の反映 {#changing-text-to-reflect-the-value-of-a-client-context-value}

フィールドをクライアントコンテキストの値にリンクするには、「**[!UICONTROL 選択]**」をクリックしてクライアントコンテキストのメニューを開き、クライアントコンテキストを選択して「**[!UICONTROL OK]**」をクリックします。この例では、「名前」フィールドとプロファイル内の書式設定された名前とのリンクに基づいて名前が変わります。

![chlimage_1-60](assets/chlimage_1-60.png)

現在ログインしているユーザーの名前がテキストに反映されます。フィールドの横にある「**[!UICONTROL リセット]**」をクリックすると、テキストを元の値に戻すことができます。

![chlimage_1-61](assets/chlimage_1-61.png)

#### Dynamic Media Classic（Scene7）画像テンプレートのリンク化 {#making-the-scene-image-template-a-link}

Dynamic Media Classic（Scene7）画像テンプレートコンポーネントをクリック可能なリンクにすることができます。

1. Dynamic Media Classic（Scene7）画像テンプレートコンポーネントを含んだページで「**[!UICONTROL 編集]**」を選択します。
1. 「**[!UICONTROL URL]**」フィールドに、ユーザーが画像をクリックしたときに表示される URL を入力します。「**[!UICONTROL 次のウィンドウで開く]**」フィールドで、ターゲットを新しいウィンドウと同じウィンドウのどちらで開くかを選択します。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 「**[!UICONTROL OK]**」を選択します。

### ビデオコンポーネント {#video-component}

Dynamic Media Classic（Scene7）**[!UICONTROL ビデオ]**&#x200B;コンポーネント（サイドキックの「Dynamic Media Classic （Scene7）」セクションから使用可能）では、デバイスと帯域幅の検出機能を使用して、適切な形式のビデオをそれぞれの画面に提供します。このコンポーネントは HTML5 ビデオプレーヤー（チャネルを超えて使用可能な単一のビューア）です。

このコンポーネントはアダプティブビデオセット（単一の MP4 ビデオまたは単一の F4V ビデオ）で使用できます。

ビデオが Dynamic Media Classic（Scene7）統合環境で動作する仕組みについて詳しくは、[ビデオ](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)を参照してください。また、[**Dynamic Media Classic（Scene7）ビデオ**&#x200B;コンポーネントと基盤&#x200B;**ビデオ**&#x200B;コンポーネントとの比較](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)も参照してください。

![chlimage_1-63](assets/chlimage_1-63.png)

### ビデオコンポーネントに関する既知の制限事項 {#known-limitations-for-the-video-component}

プライマリソースビデオがアップロードされると、Adobe DAM および WCM が表示されます。次に示すプロキシアセットは表示されません。

* Dynamic Media Classic（Scene7）のエンコードされたレンディション
* Dynamic Media Classic（Scene7）アダプティブビデオセット

Dynamic Media Classic（Scene7）ビデオコンポーネントでアダプティブビデオセットを使用する場合は、ビデオのサイズに合わせてコンポーネントのサイズを変更する必要があります。

## Dynamic Media Classic（Scene7）コンテンツブラウザー {#scene-content-browser}

Dynamic Media Classic（Scene7）コンテンツブラウザーを使用すると、Dynamic Media Classic（Scene7）のコンテンツを Experience Manager で直接表示できます。コンテンツブラウザーにアクセスするには、コンテンツファインダーで、「**Dynamic Media Classic （Scene7）**」（タッチ操作向け UI の場合）か、「**S7**」アイコン（クラシック UI の場合）を選択します。どちらの UI を使用しても機能は同じです。

設定が複数ある場合、Experience Manager のデフォルトでは[デフォルト設定](/help/sites-administering/scene7.md#configuring-a-default-configuration)が表示されます。Dynamic Media Classic（Scene7）コンテンツブラウザーのドロップダウンメニューで、別の設定を直接選択できます。

>[!NOTE]
>
>* オンデマンドフォルダー内のアセットは、Dynamic Media Classic（Scene7）コンテンツブラウザーには表示されません。
>* [セキュアプレビューが有効](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)なときは、Dynamic Media Classic（Scene7）の公開アセットと非公開アセットの両方が、Dynamic Media Classic（Scene7）コンテンツブラウザーに表示されます。
>* **[!UICONTROL Dynamic Media Classic（Scene7）]**&#x200B;または「**[!UICONTROL S7]**」アイコンがオプションとしてコンテンツブラウザーに表示されない場合は、 [Experience Manager と連携するように Dynamic Media Classic（Scene7）を設定する](/help/sites-administering/scene7.md)必要があります。
>* ビデオの場合、Dynamic Media Classic（Scene7）コンテンツブラウザーは次の項目をサポートしています。
   >   * アダプティブビデオセット：複数の画面でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
   >   * 単一の MP4 ビデオ
   >   * 単一の F4V ビデオ


### コンテンツの参照 {#browsing-content-in-the-classic-ui}

「**[!UICONTROL S7]**」タブを選択して、Dynamic Media Classic（Scene7）のコンテンツを参照します。

設定を選択することで、現在アクセスしている設定を変更することができます。フォルダーは、選択する設定に応じて変わります。

![chlimage_1-64](assets/chlimage_1-64.png)

アセット用のコンテンツファインダーと同様に、アセットを検索して、結果にフィルターを適用できます。ただし、アセットファインダーとは異なり、「**S7**」タブでキーワードを入力すると、そのキーワードが&#x200B;**含まれる**&#x200B;ファイル名ではなく、入力した文字列&#x200B;**で始まる**&#x200B;ファイル名が検索されます。

デフォルトでは、アセットはファイル名で表示されます。ただし、結果をアセットタイプでフィルタリングすることもできます。

>[!NOTE]
>
>ビデオの場合、WCM の Dynamic Media Classic（Scene7）コンテンツブラウザーは次の項目をサポートしています。
>
>* アダプティブビデオセット：複数の画面でシームレスに再生するために必要なすべてのビデオレンディションのコンテナ
>* 単一の MP4 ビデオ
>* 単一の F4V ビデオ
>


### コンテンツブラウザーでの Dynamic Media Classic（Scene7）アセットの検索 {#searching-for-scene-assets-with-the-content-browser}

Dynamic Media Classic（Scene7）アセットの検索は、Experience Manager アセットの検索と似ています。ただし、検索時に、Experience Manager ではアセットを直接インポートするのに対して、Dynamic Media Classic（Scene7）システムでは実際にはアセットのリモートビューが表示されます。

クラシック UI またはタッチ操作向け UI を使用して、アセットを表示および検索できます。インターフェイスによって検索方法は多少異なります。

どちらの UI で検索する場合でも、次の基準でフィルターを適用できます（ここでは、タッチ操作向け UI を示しています）。

**キーワードを入力** - アセットを名前で検索できます。検索時には、入力したキーワードで始まるファイル名が検索されます。例えば、「swimming」という単語を入力すると、入力した順序どおりの文字列で始まるアセットファイルの名前が検索されます。アセットを検索するには、語句を入力した後に Enter キーを押してください。

![chlimage_1-65](assets/chlimage_1-65.png)

**フォルダー／パス** - フォルダーの名前は、選択した設定に基づいています。下位にドリルダウンするには、フォルダーアイコンをクリックしてサブフォルダーを選択し、チェックマークをクリックして選択します。

キーワードを入力してフォルダーを選択すると、Experience Manager でそのフォルダーとすべてのサブフォルダーが検索されます。ただし、検索時にキーワードを入力しない場合は、フォルダーを選択してもそのフォルダー内のアセットしか表示されず、サブフォルダーは含まれません。

デフォルトでは、Experience Manager は、選択されたフォルダーとすべてのサブフォルダーを検索します。

![chlimage_1-66](assets/chlimage_1-66.png)

**アセットのタイプ** - Dynamic Media Classic（Scene7）を選択して、Dynamic Media Classic（Scene7）のコンテンツを参照します。このオプションは、Dynamic Media Classic（Scene7）が設定されている場合にのみ使用できます。

![chlimage_1-67](assets/chlimage_1-67.png)

**設定** - Dynamic Media Classic（Scene7）の設定をクラウドサービスで複数定義してある場合は、ここで選択できます。その結果、選択した設定に応じてフォルダーが変わります。

![chlimage_1-68](assets/chlimage_1-68.png)

**アセットタイプ** - Dynamic Media Classic（Scene7）ブラウザー内では、結果にフィルターを適用して、画像、テンプレート、ビデオ、アダプティブビデオセットのいずれかを抽出することができます。アセットタイプを選択しない場合、Experience Manager ではデフォルトですべてのアセットタイプが検索されます。

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* クラシック UI では、**Flash** と **FXG** も検索できます。タッチ操作向け UI では、これら 2 つの語句のフィルタリングはサポートされていません。
>
>* ビデオを検索するときは、単一のレンディションが検索されています。結果には、元のレンディション（&#42;.mp4 のみ）と、エンコードされたレンディションが返されます。
>* アダプティブビデオセットの検索では、フォルダーとすべてのサブフォルダーが検索されます（検索にキーワードを追加した場合のみ）。キーワードを追加しないと、Experience Manager ではサブフォルダーが検索されません。
>


**公開ステータス** - 公開ステータス（非公開または公開済み）に基づいてアセットをフィルタリングできます。公開ステータスを選択しない場合、Experience Manager ではデフォルトですべての公開ステータスが検索されます。

![chlimage_1-70](assets/chlimage_1-70.png)
