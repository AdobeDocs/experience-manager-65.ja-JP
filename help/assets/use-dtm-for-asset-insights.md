---
title: DTM での Assets Insights の有効化
description: Adobe Dynamic Tag Management（DTM）を使用して Assets Insights を有効にする方法を学習します。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: afc72fb6b324cf2e0ad8168f783d9c1a6f96c614
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 100%

---

# DTM での Assets Insights の有効化 {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management は、デジタルマーケティングツールをアクティベートするツールです。これは Adobe Analytics のユーザーに無償で提供されます。トラッキングコードをカスタマイズして、サードパーティの CMS ソリューションで Assets Insights を使用できるようにするか、DTM を使用して Assets Insights タグを挿入できます。インサイトのサポートおよび提供が行われるのは、画像に対してのみです。

>[!CAUTION]
>
>Adobe DTM は [!DNL Adobe Experience Platform] に置き換わったことにより非推奨のため、まもなく[提供終了](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f)となります。Adobeでは、 [!DNL Adobe Experience Platform] アセットインサイト](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html?lang=ja) には [ を使用することをお勧めします。

DTM を使用して Assets Insights を有効にするには、次の手順を実行します。

1. Experience Manager のロゴをクリックし、**[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL インサイト設定]**&#x200B;に移動します。
1. [DTM Cloud Service を使用した Experience Manager デプロイメントの設定](/help/sites-administering/dtm.md)

   API トークンは、[https://dtm.adobe.com](https://dtm.adobe.com/) にログオンすると使用できるようになります。ユーザープロファイルから「**[!UICONTROL アカウント設定]**」にアクセスします。Experience Manager Sites と Assets Insights の統合は現在準備中のため、この手順は Assets Insights の観点からは必要ありません。

1. [https://dtm.adobe.com](https://dtm.adobe.com/) にログオンし、必要に応じて会社を選択します。
1. 既存の web プロパティを作成するか、開きます。

   * 「**[!UICONTROL Web プロパティ]**」タブを選択し、「**[!UICONTROL プロパティを追加]**」をクリックします。

   * 必要に応じてフィールドを更新し、「**[!UICONTROL プロパティを作成]**」をクリックします。[ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)を参照してください。

   ![Web プロパティを編集または作成](assets/Create-edit-web-property.png)

1. 「**[!UICONTROL ルール]**」タブで、ナビゲーションパネルの「**[!UICONTROL ページ型ルール]**」を選択し、「**[!UICONTROL 新規ルールを作成]**」をクリックします。

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. 「**[!UICONTROL Javascript／サードパーティタグ]**」を展開します。次に、「**[!UICONTROL 順次 HTML]**」タブの「**[!UICONTROL 新規スクリプトを追加]**」をクリックして、スクリプトダイアログを開きます。

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Experience Manager のロゴをクリックし、**[!UICONTROL ツール]**／**[!UICONTROL Assets]** に移動します。
1. 「**[!UICONTROL Insights ページトラッカー]**」をクリックし、トラッカーコードをコピーして、手順 6 で開いたスクリプトダイアログに貼り付けます。変更内容を保存します。

   >[!NOTE]
   >
   >* `AppMeasurement.js` が削除されました。 これは、DTM の Adobe Analytics ツールで使用できるはずです。
   >* `assetAnalytics.dispatcher.init()` の呼び出しは削除されました。この関数は、DTM の Adobe Analytics ツールの読み込みが完了すると呼び出されるはずです。
   >* Assets Insights ページトラッカーがホストされる場所（例えば、Experience Manager や CDN など）によっては、スクリプトソースのオリジナルを変更する必要があります。
   >* Experience Manager でホストされるページトラッカーの場合、ソースがディスパッチャーインスタンスのホスト名を使用してパブリッシュインスタンスを指す必要があります。


1. `https://dtm.adobe.com` にアクセスします。Web プロパティの「**[!UICONTROL 概要]**」をクリックし、「**[!UICONTROL ツールを追加]**」をクリックするか既存の Adobe Analytics ツールを開きます。ツールを作成する際に、「**[!UICONTROL 設定方法]**」を「**[!UICONTROL 自動]**」に設定できます。

   ![Adobe Analytics ツールを追加します。](assets/Add-Adobe-Analytics-Tool.png)

   必要に応じてステージング／実稼動版レポートスイートを選択します。

1. 「**[!UICONTROL ライブラリ管理]**」を展開し、「**[!UICONTROL ライブラリの読み込み先]**」が「**[!UICONTROL ページの先頭へ移動]**」に設定されていることを確認します。

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. 「**[!UICONTROL ページコードをカスタマイズ]**」を展開し、「**[!UICONTROL エディターを開く]**」をクリックします。

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. 次のコードをウィンドウに貼り付けます。

   ```Java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * DTM のページ読み込みルールには、`pagetracker.js` コードのみが含まれています。`assetAnalytics` のフィールドはすべて、デフォルト値の上書きと見なされます。これらは、デフォルトでは必要ありません。
   * このコードは、`assetAnalytics.dispatcher.init()` を呼び出す前に、`_satellite.getToolsByType('sc')[0].getS()` が初期化され、`assetAnalytics,dispatcher.init` が使用可能であることを確認します。このため、手順 11 ではこのコードの追加をスキップできます。
   * Insights ページトラッカーコード（**[!UICONTROL ツール／Assets／Insights ページトラッカー]**）内のコメントに記述されているように、ページトラッカーが `AppMeasurement` オブジェクトを作成しないとき、最初の 3 つの引数（RSID、トラッキングサーバー、訪問者の名前空間）は関係ありません。これを示すため代わりに空の文字列が渡されます。\
       その他の引数は、インサイト設定ページ（**[!UICONTROL ツール／アセット／インサイト設定]**）で設定された内容に対応しています。
   * AppMeasurement オブジェクトは、すべての使用可能な SiteCatalyst エンジンで `satelliteLib` に対するクエリを実行して取得されます。複数のタグが設定されている場合は、配列セレクターのインデックスをそれに応じて変更します。配列のエントリは、DTM インターフェイスで使用可能な SiteCatalyst ツールの順に並んでいます。

1. 保存して、コードエディターウィンドウを閉じます。その後、変更内容をツール設定で保存します。
1. 「**[!UICONTROL 承認]**」タブで、承認が保留されている両方の項目を承認します。DTM タグを Web ページに挿入する準備ができました。
