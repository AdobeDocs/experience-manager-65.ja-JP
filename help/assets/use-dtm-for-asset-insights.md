---
title: DTMを使用したアセットインサイトの有効化
description: Assets Insightsを有効にするために、AdobeのDynamic Tag Management(DTM)を使用する方法について説明します。
contentOwner: AG
role: User, Admin
feature: アセットインサイト、アセットレポート
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: b3acfdba41e1bd94c65bb7a87f63b9c326a80dd2
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 30%

---

# DTMを使用したアセットインサイトの有効化 {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management は、デジタルマーケティングツールをアクティベートするツールです。これは Adobe Analytics のユーザーに無償で提供されます。トラッキングコードをカスタマイズして、サードパーティのCMSソリューションでAssets Insightsを使用できるようにするか、DTMを使用してAssets Insightsタグを挿入することができます。 インサイトのサポートおよび提供がおこなわれるのは、画像に対してのみです。

>[!CAUTION]
>
>AdobeDTMは[!DNL Adobe Experience Platform Launch]のために廃止され、まもなく[提供終了](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f)に達します。 Adobeでは、アセットのインサイト](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)に[ [!DNL Launch] を使用することをお勧めします。

DTMを使用してアセットインサイトを有効にするには、次の手順を実行します。

1. Experience Managerのロゴをクリックし、**[!UICONTROL ツール]** / **[!UICONTROL アセット]** / **[!UICONTROL インサイト設定]**&#x200B;に移動します。
1. [DTMを使用したExperience ManagerデプロイメントのCloud Service](/help/sites-administering/dtm.md)

   APIトークンは、[https://dtm.adobe.com](https://dtm.adobe.com/)にログオンし、ユーザープロファイルの&#x200B;**[!UICONTROL アカウント設定]**&#x200B;にアクセスすると使用できます。 Experience Managerサイトとアセットインサイトの統合は、引き続き機能するので、アセットインサイトの観点からは、この手順は必要ありません。

1. [https://dtm.adobe.com](https://dtm.adobe.com/)にログオンし、必要に応じて会社を選択します。
1. 既存のWebプロパティを作成するか、開きます

   * 「**[!UICONTROL Webプロパティ]**」タブを選択し、「**[!UICONTROL プロパティを追加]**」をクリックします。

   * 必要に応じてフィールドを更新し、「**[!UICONTROL プロパティを作成]**」をクリックします。 [ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)を参照してください。

   ![Webプロパティの編集の作成](assets/Create-edit-web-property.png)

1. 「**[!UICONTROL ルール]**」タブで、ナビゲーションウィンドウから「**[!UICONTROL ページ型ルール]**」を選択し、「**[!UICONTROL 新しいルールを作成]**」をクリックします。

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. **[!UICONTROL JavaScript /サードパーティタグ]**&#x200B;を展開します。 次に、「**[!UICONTROL 順次HTML]**」タブで「**[!UICONTROL 新しいスクリプトを追加]**」をクリックして、スクリプトダイアログを開きます。

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Experience Managerのロゴをクリックし、**[!UICONTROL ツール]** / **[!UICONTROL アセット]**&#x200B;に移動します。
1. 「**[!UICONTROL インサイトページトラッカー]**」をクリックし、トラッカーコードをコピーして、手順6で開いたスクリプトダイアログに貼り付けます。 変更内容を保存します。

   >[!NOTE]
   >
   >* `AppMeasurement.js` が削除されました。これは、DTM の Adobe Analytics ツールで使用できるはずです。
   >* `assetAnalytics.dispatcher.init()`への呼び出しは削除されます。 この関数は、DTM の Adobe Analytics ツールの読み込みが完了すると呼び出されるはずです。
   >* アセットインサイトページトラッカーがホストされている場所(Experience Manager、CDNなど)によっては、スクリプトソースの出所を変更する必要が生じる場合があります。
   >* Experience Managerでホストされるページトラッカーの場合、ソースは、Dispatcherインスタンスのホスト名を使用してパブリッシュインスタンスを指す必要があります。


1. `https://dtm.adobe.com` にアクセスします。Web プロパティの「**[!UICONTROL 概要]**」をクリックし、「**[!UICONTROL ツールを追加]**」をクリックするか既存の Adobe Analytics ツールを開きます。ツールの作成時に、**[!UICONTROL 設定方法]**&#x200B;を&#x200B;**[!UICONTROL 自動]**&#x200B;に設定できます。

   ![Adobe Analyticsツールの追加](assets/Add-Adobe-Analytics-Tool.png)

   必要に応じてステージング／実稼動版レポートスイートを選択します。

1. **[!UICONTROL 「ライブラリ管理」]**&#x200B;を展開し、**[!UICONTROL 「]**&#x200B;でのライブラリの読み込み」が&#x200B;**[!UICONTROL 「ページ上部]**」に設定されていることを確認します。

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. **[!UICONTROL ページコードをカスタマイズ]**&#x200B;を展開し、**[!UICONTROL エディターを開く]**&#x200B;をクリックします。

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

   * DTMのページ型ルールには、`pagetracker.js`コードのみが含まれます。 `assetAnalytics` のフィールドはすべて、デフォルト値の上書きと見なされます。これらは、デフォルトでは必要ありません。
   * `_satellite.getToolsByType('sc')[0].getS()`が初期化され、`assetAnalytics,dispatcher.init`が使用可能になっていることを確認した後、コードは`assetAnalytics.dispatcher.init()`を呼び出します。 このため、手順 11 ではこのコードの追加をスキップできます。
   * インサイトページトラッカーコード（**[!UICONTROL ツール/アセット/インサイトページトラッカー]**）内のコメントで示したように、ページトラッカーが`AppMeasurement`オブジェクトを作成しない場合、最初の3つの引数（RSID、トラッキングサーバー、訪問者名前空間）は無関係です。 これを示すため代わりに空の文字列が渡されます。\
       その他の引数は、インサイト設定ページ（**[!UICONTROL ツール／アセット／インサイト設定]**）で設定された内容に対応しています。
   * AppMeasurement オブジェクトは、すべての使用可能な SiteCatalyst エンジンで `satelliteLib` に対するクエリを実行して取得されます。複数のタグが設定されている場合は、配列セレクターのインデックスをそれに応じて変更します。配列のエントリは、DTM インターフェイスで使用可能な SiteCatalyst ツールの順に並んでいます。

1. 保存してコードエディターウィンドウを閉じ、変更をツール設定に保存します。
1. 「**[!UICONTROL 承認]**」タブで、承認待ちの両方を承認します。 DTM タグを Web ページに挿入する準備ができました。
