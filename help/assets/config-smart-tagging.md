---
title: Smart Content Serviceを使用したアセットのタグ付けの設定
description: Smart Content Serviceを使用して、 [!DNL Adobe Experience Manager]でスマートタグを設定し、高度なスマートタグを設定する方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '2179'
ht-degree: 60%

---


# [!DNL Assets]のスマートタグの準備{#configure-asset-tagging-using-the-smart-content-service}

Smart Content Servicesを使用してアセットのタグ付けを開始できるようにする前に、[!DNL Experience ManageR Assets]をAdobeデベロッパーコンソールに統合し、[!DNL Adobe Sensei]のスマートサービスを活用します。 設定が完了すると、いくつかの画像とタグを使用してサービスのトレーニングを行います。

Smart Content Serviceを使用する前に、次の事項を確認します。

* [Adobe 開発者コンソールとの統合](#integrate-adobe-io).
* [Smart Content Serviceのトレーニング](#training-the-smart-content-service)。

   <!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
  -->

* 最新の[Experience Managerサービスパック](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)をインストールします。

## Adobe 開発者コンソールとの統合 {#integrate-adobe-io}

Adobe開発者コンソールと統合する場合、[!DNL Experience Manager]サーバーは、要求をSmart Content Serviceに転送する前に、Adobe開発者コンソールゲートウェイを使用してサービス資格情報を認証します。 統合するには、組織の管理者権限を持つAdobe IDアカウントと、組織用に購入され有効にされたSmart Content Serviceライセンスが必要です。

Smart Content Serviceを設定するには、次のトップレベルの手順に従います。

1. [ でスマートコンテンツサービス設定を作成して、公開鍵を生成します。](#obtain-public-certificate)[!DNL Experience Manager]OAuth 統合用の[公開証明書を取得します](#obtain-public-certificate)。

1. [Adobe 開発者コンソールで統合を作成](#create-adobe-i-o-integration)し、生成した公開鍵をアップロードします。

1. [AdobeデベロッパーコンソールのAPIキーと他の資格情報を使用して、](#configure-smart-content-service) デプロイを設定します。

1. [設定をテストします](#validate-the-configuration)。

1. 必要に応じて、[アセットのアップロード時に自動タグ付けを有効にする](#enable-smart-tagging-in-the-update-asset-workflow-optional)。

### 公開証明書を取得するためのSmart Content Service設定の作成{#obtain-public-certificate}

公開証明書により、Adobe 開発者コンソールでプロファイルを認証できます。

1. [!DNL Experience Manager]ユーザーインターフェイスで、**[!UICONTROL ツール]**/**[!UICONTROL Cloud Services]**/**[!UICONTROL レガシーCloud Services]**&#x200B;にアクセスします。

1. Cloud Servicesページで、「**[!UICONTROL アセットのスマートタグ]**」の下の「今すぐ設定&#x200B;]**」をクリックします。**[!UICONTROL 

1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、スマートタグ設定のタイトルと名前を指定します。「**[!UICONTROL 作成]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、以下の値を使用します。

   **[!UICONTROL サービス URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 認証サーバー]**: `https://ims-na1.adobelogin.com`

   その他のフィールドは現時点では空白のままにします（後で指定します）。「**[!UICONTROL OK]**」をクリックします。

   ![コンテンツサービスURLを提供するExperience Managerスマートコンテンツサービスダイアログ](assets/aem_scs.png)


   *図：コンテンツサービスURLを提供する「Smart Content Service」ダイアログ*

   >[!NOTE]
   >
   >[!UICONTROL サービスURL]として指定されたURLは、ブラウザーを介してアクセスできず、404エラーが発生します。 この設定は、[!UICONTROL Service URL]パラメーターと同じ値で正常に機能します。 全体的なサービスの状態とメンテナンスのスケジュールについては、[https://status.adobe.com](https://status.adobe.com)を参照してください。

1. 「**[!UICONTROL OAuth統合用の公開証明書をダウンロード]**」をクリックし、公開証明書ファイル`AEM-SmartTags.crt`をダウンロードします。

   ![スマートタグ付けサービス用に作成された設定の表現](assets/smart-tags-download-public-cert.png)


   *図：スマートタグサービスの設定*

#### 証明書の有効期限が切れた場合に再設定{#certrenew}

証明書の有効期限が切れると、信頼されなくなります。 期限切れの証明書は更新できません。新しい証明書を追加するには、以下の手順に従います。

1. [!DNL Experience Manager] デプロイメントに管理者としてログインします。**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;をクリックします。

1. **[!UICONTROL dam-update-service]** ユーザーを見つけてクリックします。「**[!UICONTROL キーストア]**」タブをクリックします。

1. 証明書の有効期限が切れた既存の **[!UICONTROL similaritysearch]** キーストアを削除します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![キーストア内の既存の類似性検索エントリを削除し、新しいセキュリティ証明書を追加します](assets/smarttags_delete_similaritysearch_keystore.png)


   *図：キーストアの既存の `similaritysearch` エントリを削除して新しいセキュリティ証明書を追加.*

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動します。**[!UICONTROL アセットのスマートタグ]**／**[!UICONTROL 設定を表示]**／**[!UICONTROL 利用可能な設定]**&#x200B;をクリックします。必要な設定をクリックします。

1. 公開証明書をダウンロードするには、「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をクリックします。

1. [https://console.adobe.io](https://console.adobe.io) にアクセスし、**[!UICONTROL 統合]**&#x200B;ページで既存のスマートコンテンツサービスに移動します。新しい証明書をアップロードします。詳しくは、[Adobe開発者コンソール統合の作成](#create-adobe-i-o-integration)の手順を参照してください。

### Adobe開発者コンソール統合の作成{#create-adobe-i-o-integration}

Smart Content Service APIを使用するには、Adobe開発者コンソールで統合を作成して、[!UICONTROL APIキー](Adobe開発者コンソール統合の[!UICONTROL CLIENT ID]フィールドで生成)、[!UICONTROL 技術的なアカウントID]、[!UICONTROL ORGANIZATIONを取得します[!UICONTROL アセットのスマートタグサービス設定]のID]と[!UICONTROL CLIENT SECRET]（[!DNL Experience Manager]のクラウド設定）。

1. ブラウザーで [https://console.adobe.io](https://console.adobe.io/) にアクセスします。適切なアカウントを選択し、関連付けられた組織の役割がシステム管理者であることを確認します。

1. 任意の名前でプロジェクトを作成します。「**[!UICONTROL API を追加]**」をクリックします。

1. **[!UICONTROL API を追加]**&#x200B;ページで、「**[!UICONTROL Experience Cloud]**」を選択し、「**[!UICONTROL スマートコンテンツ]**」を選択します。「**[!UICONTROL 次へ]**」をクリックします。

1. 「**[!UICONTROL 公開鍵をアップロード]**」を選択します。[!DNL Experience Manager]からダウンロードした証明書ファイルを指定します。[!UICONTROL 公開鍵が正常にアップロード]されたというメッセージが表示されます。「**[!UICONTROL 次へ]**」をクリックします。

   [!UICONTROL 新しいサービスアカウント（JWT）秘密鍵証明書を作成]ページには、設定したサービスアカウントの公開鍵が表示されます。

1. 「**[!UICONTROL 次へ]**」をクリックします。

1. **[!UICONTROL 製品プロファイルを選択]**&#x200B;ページで、「**[!UICONTROL スマートコンテンツサービス]**」を選択します。「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   設定に関する詳細情報がページに表示されます。このページを開いたままにして、スマートタグを設定するには、[!DNL Experience Manager]のクラウド設定の[!UICONTROL Assets Smart Tagging Service Settings]にこれらの値をコピーして追加します。

   ![「概要」タブで、統合について指定した情報を確認できます。](assets/integration_details.png)


   *図：Adobeデベロッパーコンソールの統合の詳細*

### スマートコンテンツサービスの設定 {#configure-smart-content-service}

統合を設定するには、Adobeデベロッパーコンソール統合の[!UICONTROL TECHNICAL ACCOUNT ID]、[!UICONTROL ORGANIZATION ID]、[!UICONTROL CLIENT SECRET]および[!UICONTROL CLIENT ID]フィールドの値を使用します。 Smart Tagsクラウド設定を作成すると、[!DNL Experience Manager]デプロイメントからAPIリクエストを認証できます。

1. [!DNL Experience Manager]で、**[!UICONTROL ツール]**/**[!UICONTROL Cloud Service]**/**[!UICONTROL レガシーCloud Services]**&#x200B;に移動し、[!UICONTROL Cloud Services]コンソールを開きます。

1. 「**[!UICONTROL アセットのスマートタグ]**」で、上記で作成した設定を開きます。サービスの設定ページで、「**[!UICONTROL 編集]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、「**[!UICONTROL サービス URL]**」および「**[!UICONTROL 認証サーバー]**」フィールドに事前入力された値を使用します。

1. [!UICONTROL Apiキー]、[!UICONTROL テクニカルアカウントID]、[!UICONTROL 組織ID]、[!UICONTROL クライアントシークレット]の各フィールドに対して、[Adobe開発者コンソール](#create-adobe-i-o-integration)で生成された以下の値をコピーして使用します。

   | [!UICONTROL アセットのスマートタグサービス設定] | [!DNL Adobe Developer Console] 統合フィールド |
   |--- |--- |
   | [!UICONTROL API キー] | [!UICONTROL クライアントID] |
   | [!UICONTROL テクニカルアカウント ID] | [!UICONTROL テクニカルアカウントID] |
   | [!UICONTROL 組織 ID] | [!UICONTROL 組織ID] |
   | [!UICONTROL クライアントの秘密鍵] | [!UICONTROL CLIENT SECRET] |

### 設定の検証 {#validate-the-configuration}

設定が完了したら、JMX MBeanを使用して設定を検証できます。 検証するには、次の手順に従います。

1. `https://[aem_server]:[port]`の[!DNL Experience Manager]サーバーにアクセスします。

1. **[!UICONTROL ツール]** > **[!UICONTROL 操作]** > **[!UICONTROL Webコンソール]**&#x200B;に移動して、OSGiコンソールを開きます。 **[!UICONTROL メイン]/[!UICONTROL JMX]**&#x200B;をクリックします。

1. 「`com.day.cq.dam.similaritysearch.internal.impl`」をクリックします。**[!UICONTROL 類似性検索のその他のタスク]**&#x200B;を開きます。

1. 「`validateConfigs()`」をクリックします。**[!UICONTROL 設定を検証]**&#x200B;ダイアログで、**[!UICONTROL 呼び出し]**&#x200B;をクリックします。

検証結果は、同じダイアログに表示されます。

### [!UICONTROL DAMアセットを更新]ワークフローでスマートタグを有効にする（オプション） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. [!DNL Experience Manager]で、**[!UICONTROL ツール]** > **[!UICONTROL ワークフロー]** > **[!UICONTROL モデル]**&#x200B;に移動します。

1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルを選択します。

1. ツールバーの「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルを展開して、ステップを表示します。「DAM ワークフロー」セクションの「**[!UICONTROL スマートタグアセット]**」ステップをドラッグして、「**[!UICONTROL サムネールを処理]**」ステップの後に配置します。

   ![「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加](assets/smart-tag-in-dam-update-asset-workflow.png)

   *図：「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加。*

1. そのステップを編集モードで開きます。「**[!UICONTROL 詳細設定]**」で、「**[!UICONTROL ハンドラー処理の設定]**」オプションが選択されていることを確認します。

   ![DAM更新アセットワークフローの設定とスマートタグ手順の追加](assets/smart-tag-step-properties-workflow1.png)


   *図：DAM更新アセットワークフローの設定とスマートタグ手順の追加*

1. 自動タグ付けのステップに失敗してもワークフローを完了させたい場合は、「**[!UICONTROL 引数]**」タブで「**[!UICONTROL エラーを無視]**」を選択します。

   ![DAMアセットの更新ワークフローを設定し、スマートタグ手順を追加してハンドラーの設定を選択します](assets/smart-tag-step-properties-workflow2.png)


   *図：DAMアセットの更新ワークフローを設定し、スマートタグ手順を追加してハンドラーの設定を選択します*

   フォルダーでスマートタグが有効になっているかに関わらずアップロード時にアセットをタグ付けするには、「**[!UICONTROL スマートタグフラグを無視]**」を選択します。

   ![DAM Update Assetワークフローを設定し、スマートタグ手順を追加して、「スマートタグフラグを無視」を選択します](assets/smart-tag-step-properties-workflow3.png)


   *図：DAM Update Assetワークフローを設定し、スマートタグ手順を追加して、「スマートタグフラグを無視」を選択します*

1. 「**[!UICONTROL OK]**」をクリックして、プロセスステップを閉じ、ワークフローを保存します。

## Smart Content Serviceのトレーニング{#training-the-smart-content-service}

スマートコンテンツサービスでビジネス上の分類を認識できるように、ビジネスに関連するタグが既に含まれているアセットのセットに対してサービスを実行します。ブランド画像に効果的にタグを付けるには、Smart Content Serviceで、トレーニング画像が特定のガイドラインに従っている必要があります。 トレーニングが完了すると、サービスは、類似するアセットのセットに同じ分類を適用できるようになります。

サービスのトレーニングを複数回実施すると、関連性の高いタグを適用する能力が向上します。トレーニングサイクルが終了するたびに、タグ付けワークフローを実行し、アセットが適切にタグ付けされるかどうかを確認します。

スマートコンテンツサービスのトレーニングは、定期的に実施することも、必要に応じて実施することもできます。

>[!NOTE]
>
>トレーニングワークフローは、フォルダーに対してのみ実行されます。

### トレーニングのガイドライン {#guidelines-for-training}

最適な結果を得るには、トレーニングセット内の画像は次のガイドラインに従う必要があります。

**数とサイズ**：タグ 1 つにつき 30 以上の画像が必要です。長辺が 500 ピクセル以上である必要があります。

**一貫性**：タグの各画像は、似たような外観にする必要があります。

例えば、以下の画像は似ていないので、これらの画像すべてを `my-party`（トレーニング用）としてタグ付けするのは適切ではありません。

![トレーニングガイドラインの例を示すイラスト](/help/assets/assets/do-not-localize/coherence.png)

**対象範囲**：トレーニングの画像には十分な多様性が必要です。Experience Managerが適切なものに焦点を合わせるように、いくつかの合理的に多様な例を提供することがアイデアです。 見た目が大きく異なる画像に同じタグを適用する場合は、それぞれの種類に 5 つ以上の例を含めてください。

例えば、*model-down-pose* というタグの場合、タグ付け時、類似する画像をより正確に識別できるよう、以下のハイライト表示された画像に似たトレーニング画像を増やします。

![トレーニングガイドラインの例を示すイラスト](/help/assets/assets/do-not-localize/coverage_1.png)

**妨害物と障害物**：サービスのトレーニングには、障害物（目立つ背景、メインとなる対象と一緒に含まれる物や人物などの関連性のない付随物）が少ない画像のほうが効果的です。

例えば、*casual-shoe* というタグの場合、2 つ目の画像はトレーニングの候補として適切ではありません。

![トレーニングガイドラインの例を示すイラスト](/help/assets/assets/do-not-localize/distraction.png)

**完全性**：画像が複数のタグの対象となる場合は、適用可能なすべてのタグを追加してから、画像をトレーニングに含めます。例えば、`raincoat` と `model-side-view` などのタグの場合、対象となるアセットに両方のタグを追加してから、そのアセットをトレーニングに含めます。

![トレーニングガイドラインの例を示すイラスト](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>スマートコンテンツサービスでタグのトレーニングを実施し、それらのタグを他の画像に適用できるかどうかは、トレーニングで使用する画像の質によって決まります。最適な結果を得るには、視覚的に似ている画像を使用し、それぞれのタグについてサービスのトレーニングを実施することをお勧めします。

### 定期的なトレーニング {#periodic-training}

スマートコンテンツサービスを有効にして、フォルダー内のアセットおよび関連するタグに関する定期的なトレーニングを実施することができます。アセットフォルダーの[!UICONTROL プロパティ]ページを開き、「**[!UICONTROL 詳細]**」タブの「**[!UICONTROL スマートタグを有効にする]**」を選択して、変更を保存します。

![enable_smart_tags](assets/enable_smart_tags.png)

フォルダーに対してこのオプションを選択すると、[!DNL Experience Manager]はトレーニングワークフローを自動的に実行し、フォルダーアセットとそのタグに関するSmart Content Serviceのトレーニングを行います。 デフォルトでは、トレーニングワークフローは週に 1 回、土曜日の午前 0 時 30 分に実行されます。

### オンデマンドのトレーニング  {#on-demand-training}

ワークフローコンソールから、必要に応じていつでもスマートコンテンツサービスのトレーニングをおこなうことができます。

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]** > **[!UICONTROL ワークフロー]** > **[!UICONTROL モデル]**&#x200B;に移動します。
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページから、**[!UICONTROL スマートタグトレーニング]**&#x200B;ワークフローを選択し、ツールバーの&#x200B;**[!UICONTROL 開始ワークフロー]**&#x200B;をクリックします。
1. **[!UICONTROL ワークフローを実行]**&#x200B;ダイアログで、サービスのトレーニングに使用するタグ付けされたアセットが格納されているペイロードフォルダーを参照します。
1. ワークフローのタイトルを指定し、コメントを追加します。次に、「**[!UICONTROL 実行]**」をクリックします。 アセットとタグがトレーニングのために送信されます。

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>フォルダー内のアセットがトレーニング用に処理されると、変更されたアセットのみが後続のトレーニングサイクルで処理されます。

### 表示トレーニングレポート{#viewing-training-reports}

アセットのトレーニングセット内のタグに関するスマートコンテンツサービスのトレーニングが実施されたかどうかを確認するには、レポートコンソールでトレーニングワークフローレポートを調べます。

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]** > **[!UICONTROL アセット]** > **[!UICONTROL レポート]**&#x200B;に移動します。
1. **[!UICONTROL アセットレポート]**&#x200B;ページで、「**[!UICONTROL 作成]**」をクリックします。
1. 「**[!UICONTROL スマートタグトレーニング]**」レポートを選択し、ツールバーで「**[!UICONTROL 次へ]**」をクリックします。
1. レポートのタイトルと説明を指定します。「**[!UICONTROL レポートをスケジュール]**」で、「**[!UICONTROL 今すぐ]**」オプションを選択したままにします。レポートを後で生成するようにスケジュールするには、「**[!UICONTROL 後で]**」を選択し、日時を指定します。次に、ツールバーの「**[!UICONTROL 作成]**」をクリックします。
1. **[!UICONTROL アセットレポート]**&#x200B;ページで、生成したレポートを選択します。レポートを表示するには、ツールバーの「**[!UICONTROL 表示]**」アイコンをクリックします。
1. レポートの詳細をレビューします。

   レポートには、トレーニングしたタグのトレーニングステータスが表示されます。「**[!UICONTROL トレーニングステータス]**」列の緑色は、そのタグについて、スマートコンテンツサービスのトレーニングが実施されたことを示します。黄色は、特定のタグに関するサービスのトレーニングが完全には実施されていないことを示します。この場合、特定のタグを含む画像をさらに追加し、トレーニングワークフローを実行して、そのタグに関するサービスのトレーニングを完全に実施します。

   このレポートにタグが表示されない場合は、それらのタグに関するトレーニングワークフローを再度実行してください。

1. レポートをダウンロードするには、リストから対象のレポートを選択し、ツールバーの「**[!UICONTROL ダウンロード]**」をクリックします。レポートが Microsoft Excel スプレッドシートとしてダウンロードされます。

## 制限事項 {#limitations}

* 強化されたスマートタグは、画像の学習モデルとそのタグに基づいています。 これらのモデルは、タグを識別するうえで常に完璧であるわけではありません。スマートコンテンツサービスの現行バージョンには次の制限事項があります。

   * 画像内の細かい違いを認識することはできません。例えば、シャツのサイズが細身か標準かなどの違いは認識できません。
   * 画像の細かい模様や部分に基づいてタグを識別することはできません。例えば、T シャツのロゴなどです。
   * タグ付けは、[!DNL Experience Manager]がサポートされているロケールでサポートされています。 言語の一覧については、](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html)スマートコンテンツサービスのリリースノート[を参照してください。

* スマートタグ（標準または拡張タグ）を使用してアセットを検索するには、[!DNL Assets] Omnisearch（フルテキスト検索）を使用します。 スマートタグには個別の検索用述語はありません。

>[!MORELIKETHIS]
>
>* [スマートタグの概要とトレーニング方法](enhanced-smart-tags.md)
>* [スマートタグに関するビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

