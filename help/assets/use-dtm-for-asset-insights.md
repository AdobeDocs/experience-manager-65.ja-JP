---
title: DTM でのアセットインサイトの有効化
description: Adobe Dynamic Tag Management（DTM）を使用してアセットインサイトを有効にする方法を学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 34%

---


# DTM でのアセットインサイトの有効化  {#enable-asset-insights-through-dtm}

Adobe Dynamic Tag Management は、デジタルマーケティングツールをアクティベートするツールです。これは Adobe Analytics のユーザーに無償で提供されます。トラッキングコードをカスタマイズしてサードパーティのCMSソリューションでアセットインサイトを使用できるようにするか、DTMを使用してアセットインサイトタグを挿入できます。 インサイトのサポートおよび提供がおこなわれるのは、画像に対してのみです。

>[!CAUTION]
>
>AdobeDTMは[!DNL Adobe Experience Platform Launch]の利用を推奨する形で廃止され、間もなく[提供終了](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f)に達する予定です。 Adobeでは、アセットのインサイト](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)に対して[ [!DNL Launch] を使用することを推奨します。

DTM を使用してアセットインサイトを有効にするには、次の手順を実行します。

1. Experience Managerのロゴをクリックし、**[!UICONTROL ツール]**/**[!UICONTROL アセット]**/**[!UICONTROL インサイトの設定]**&#x200B;に移動します。
1. [DTMCloud Serviceを使用したExperience Managerデプロイメントの設定](/help/sites-administering/dtm.md)

   APIトークンは、[https://dtm.adobe.com](https://dtm.adobe.com/)にログオンして、ユーザープロファイルの&#x200B;**[!UICONTROL アカウント設定]**&#x200B;にアクセスしたら、使用できるはずです。 Experience Managerサイトとアセットインサイトの統合はまだ機能しているので、アセットインサイトの観点からは、この手順は必要ありません。

1. [https://dtm.adobe.com](https://dtm.adobe.com/)にログオンし、必要に応じて会社を選択します。
1. 既存のWebプロパティを作成または開く

   * 「**[!UICONTROL Webプロパティ]**」タブを選択し、「**[!UICONTROL 追加プロパティ]**」をクリックします。

   * 必要に応じてフィールドを更新し、「**[!UICONTROL プロパティを作成]**」をクリックします。 [ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)を参照してください。

   ![Webプロパティの編集を作成する](assets/Create-edit-web-property.png)

1. 「**[!UICONTROL ルール]**」タブで、ナビゲーションウィンドウから「**[!UICONTROL ページ型ルール]**」を選択し、「**[!UICONTROL 新しいルールを作成]**」をクリックします。

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. **[!UICONTROL JavaScript /サードパーティタグ]**&#x200B;を展開します。 次に、「**[!UICONTROL 順次HTML]**」タブの追加「**[!UICONTROL 新しいスクリプト]**」をクリックして、スクリプトダイアログを開きます。

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Experience Managerのロゴをクリックし、**[!UICONTROL ツール]**/**[!UICONTROL アセット]**&#x200B;に移動します。
1. 「**[!UICONTROL インサイトページトラッカー]**」をクリックし、トラッカーコードをコピーして、手順6で開いたスクリプトダイアログに貼り付けます。 変更内容を保存します。

   >[!NOTE]
   >
   >* `AppMeasurement.js` が削除されます。これは、DTM の Adobe Analytics ツールで使用できるはずです。
   >* `assetAnalytics.dispatcher.init()`への呼び出しは削除されます。 この関数は、DTM の Adobe Analytics ツールの読み込みが完了すると呼び出されるはずです。
   >* アセットインサイトページトラッカーがホストされている場所(Experience Manager、CDNなど)に応じて、スクリプトソースの接触チャネルに変更が必要な場合があります。
   >* Experience Managerがホストするページトラッカーの場合、ソースは、ディスパッチャーインスタンスのホスト名を使用して発行インスタンスを指し示す必要があります。


1. `https://dtm.adobe.com` にアクセスします。Web プロパティの「**[!UICONTROL 概要]**」をクリックし、「**[!UICONTROL ツールを追加]**」をクリックするか既存の Adobe Analytics ツールを開きます。ツールの作成時に、**[!UICONTROL 設定方法]**&#x200B;を&#x200B;**[!UICONTROL 自動]**&#x200B;に設定できます。

   ![追加Adobe Analyticsツール](assets/Add-Adobe-Analytics-Tool.png)

   必要に応じてステージング／実稼動版レポートスイートを選択します。

1. **[!UICONTROL ライブラリ管理]**&#x200B;を展開し、****&#x200B;のライブラリを読み込みが&#x200B;**[!UICONTROL ページのトップ]**&#x200B;に設定されていることを確認します。

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

   * DTMのページ型ルールには、`pagetracker.js`コードのみが含まれます。 `assetAnalytics` のフィールドはすべて、デフォルト値の上書きと見なされます。これらは、デフォルトでは必要ありません。
   * コードは、`_satellite.getToolsByType('sc')[0].getS()`が初期化され、`assetAnalytics,dispatcher.init`が使用可能であることを確認した後、`assetAnalytics.dispatcher.init()`を呼び出します。 このため、手順 11 ではこのコードの追加をスキップできます。
   * インサイトページトラッカーコード（**[!UICONTROL ツール/アセット/インサイトページトラッカー]**）内のコメントに示されているように、ページトラッカーが`AppMeasurement`オブジェクトを作成しない場合、最初の3つの引数(RSID、トラッキングサーバー、訪問者名前空間)は無関係です。 これを示すため代わりに空の文字列が渡されます。\
       その他の引数は、インサイト設定ページ（**[!UICONTROL ツール／アセット／インサイト設定]**）で設定された内容に対応しています。
   * AppMeasurement オブジェクトは、すべての使用可能な SiteCatalyst エンジンで `satelliteLib` に対するクエリを実行して取得されます。複数のタグが設定されている場合は、配列セレクターのインデックスをそれに応じて変更します。配列のエントリは、DTM インターフェイスで使用可能な SiteCatalyst ツールの順に並んでいます。

1. コードエディターウィンドウを保存して閉じ、変更をツール設定に保存します。
1. 「**[!UICONTROL 承認]**」タブで、承認待ちの両方を承認します。 DTM タグを Web ページに挿入する準備ができました。WebページにDTMタグを挿入する方法について詳しくは、「[DTMをカスタムページテンプレートに統合する](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/)」を参照してください。
