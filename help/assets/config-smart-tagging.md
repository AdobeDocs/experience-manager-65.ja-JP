---
title: スマートコンテンツサービスを使用したアセットのタグ付けの設定
description: スマートコンテンツサービスを使用して、 [!DNL Adobe Experience Manager] でスマートタグと拡張スマートタグを設定する方法について説明します。
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
source-git-commit: 83e9ab570fac686fd53c9c2594cbfb2c05a89a0c
workflow-type: tm+mt
source-wordcount: '2262'
ht-degree: 96%

---

# スマートタグ付けのために [!DNL Assets] を準備 {#configure-asset-tagging-using-the-smart-content-service}

スマートコンテンツサービスを使用してアセットのタグ付けを開始する前に、[!DNL Experience Manager Assets] と Adobe Developer Console を統合して、[!DNL Adobe Sensei] スマートコンテンツサービスを活用します。設定が完了したら、いくつかの画像とタグを使用してサービスのトレーニングを行います。

>[!NOTE]
>
>* スマートコンテンツサービスは、新しく使用できなくなりました [!DNL Experience Manager Assets] オンプレミス型の顧客。 既にこの機能を有効にしているオンプレミス版のお客様は、引き続きスマートコンテンツサービスを使用できます。
>* スマートコンテンツサービスは既存のユーザーが利用できます [!DNL Experience Manager Assets] Managed Servicesをご利用のお客様（この機能を既に有効にしています）。
>* 新規 [!DNL Experience Manager Assets] Managed Servicesのお客様は、この記事に記載されている手順に従ってスマートコンテンツサービスを設定できます。


スマートコンテンツサービスを使用する前に、次を確認します。

* [Adobe 開発者コンソールとの統合](#integrate-adobe-io)。
* [スマートコンテンツサービスのトレーニング](#training-the-smart-content-service)

* 最新の[[!DNL Experience Manager] サービスパック](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=ja)をインストールします。

## と Adobe 開発者コンソールの統合 {#integrate-adobe-io}

Adobe Developer Console と統合する場合、[!DNL Experience Manager] サーバーはリクエストをスマートコンテンツサービスに転送する前に、Adobe Developer Console ゲートウェイを使用してサービス資格情報を認証します。統合するには、組織の管理者権限と、組織で購入して有効化されたスマートコンテンツサービスライセンスを持つ Adobe ID アカウントが必要です。

スマートコンテンツサービスを設定するには、次のトップレベルの手順に従います。

1. 公開鍵を生成するには、[!DNL Experience Manager] に[スマートコンテンツサービス](#obtain-public-certificate)の設定を作成します。OAuth 統合用の[公開証明書を取得します](#obtain-public-certificate)。

1. [Adobe 開発者コンソールで統合を作成](#create-adobe-i-o-integration)し、生成した公開鍵をアップロードします。

1. Adobe Developer Console の API キーおよびその他の資格情報を使用して、[デプロイメントを設定します](#configure-smart-content-service)。

1. [設定をテストします](#validate-the-configuration)。

1. オプションで、[アセットアップロード時の自動タグ付けを有効化します](#enable-smart-tagging-in-the-update-asset-workflow-optional)。

### スマートコンテンツサービス設定を作成して公開証明書を取得 {#obtain-public-certificate}

公開証明書により、Adobe 開発者コンソールでプロファイルを認証できます。

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL Cloud Services]**／**[!UICONTROL 従来の Cloud Services]** にアクセスします。

1. クラウドサービスページで、「**[!UICONTROL アセットのスマートタグ]**」の「**[!UICONTROL 今すぐ設定]**」をクリックします。

1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、スマートタグ設定のタイトルと名前を指定します。「**[!UICONTROL 作成]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、以下の値を使用します。

   **[!UICONTROL サービス URL]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   （例：`https://smartcontent.adobe.io/apac`）。次を指定できます。 `na`, `emea`、または `apac` :Experience Managerオーサーインスタンスがホストされる地域。

   >[!NOTE]
   >
   >2022 年 9 月 1 日より前にExperience Manager管理サービスがプロビジョニングされている場合は、次のサービス URL を使用します。
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 認証サーバー]**: `https://ims-na1.adobelogin.com`

   その他のフィールドは現時点では空白のままにします（後で指定します）。「**[!UICONTROL OK]**」をクリックします。

   ![コンテンツサービスの URL を指定するための Experience Manager スマートコンテンツサービスダイアログ](assets/aem_scs.png)


   *図：コンテンツサービスの URL を指定するためのスマートコンテンツサービスダイアログ*

   >[!NOTE]
   >
   >[!UICONTROL サービス URL] として提供された URL は、ブラウザーからアクセスできず、404 エラーが発生します。設定は、[!UICONTROL サービス URL] パラメーターの同じ値で正常に動作します。サービスの全体的なステータスとメンテナンススケジュールについては、[https://status.adobe.com](https://status.adobe.com) を参照してください。

1. 「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をクリックし、公開証明書ファイル `AEM-SmartTags.crt` をダウンロードします。

   ![スマートタグ付けサービス用に作成された設定の表現](assets/smart-tags-download-public-cert.png)


   *図：スマートタグサービスの設定。*

#### 証明書の有効期限が切れた場合の再設定 {#certrenew}

証明書の有効期限が切れると、証明書は信頼されなくなります。期限切れの証明書は更新できません。証明書を追加するには、以下の手順に従います。

1. [!DNL Experience Manager] デプロイメントに管理者としてログインします。**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;をクリックします。

1. **[!UICONTROL dam-update-service]** ユーザーを見つけてクリックします。「**[!UICONTROL キーストア]**」タブをクリックします。

1. 証明書の有効期限が切れた既存の **[!UICONTROL similaritysearch]** キーストアを削除します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![キーストアで既存の類似検索エントリを削除して、新しいセキュリティ証明書を追加する](assets/smarttags_delete_similaritysearch_keystore.png)


   *図：キーストアで既存の `similaritysearch` エントリを削除してセキュリティ証明書を追加します。*

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動します。**[!UICONTROL アセットのスマートタグ]**／**[!UICONTROL 設定を表示]**／**[!UICONTROL 利用可能な設定]**&#x200B;をクリックします。必要な設定をクリックします。

1. 公開証明書をダウンロードするには、「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をクリックします。

1. [https://console.adobe.io](https://console.adobe.io) にアクセスし、**[!UICONTROL 統合]**&#x200B;ページで既存のスマートコンテンツサービスに移動します。新しい証明書をアップロードします。詳しくは、[Adobe 開発者コンソール統合の作成](#create-adobe-i-o-integration)の手順を参照してください。

### Adobe 開発者コンソール統合の作成 {#create-adobe-i-o-integration}

スマートコンテンツサービス API を使用するには、Adobe 開発者コンソールで統合を作成して、[!UICONTROL API キー]（Adobe 開発者コンソール統合の[!UICONTROL クライアント ID] フィールドで生成）、[!UICONTROL テクニカルアカウント ID]、[!UICONTROL 組織 ID]、および[!UICONTROL クライアント秘密鍵]を、[!DNL Experience Manager] のクラウド設定の [!UICONTROL Assets スマートタグサービス設定]用に取得します。

1. ブラウザーで [https://console.adobe.io](https://console.adobe.io/) にアクセスします。適切なアカウントを選択し、関連付けられた組織の役割がシステム管理者であることを確認します。

1. 任意の名前でプロジェクトを作成します。「**[!UICONTROL API を追加]**」をクリックします。

1. **[!UICONTROL API を追加]**&#x200B;ページで、「**[!UICONTROL Experience Cloud]**」を選択し、「**[!UICONTROL スマートコンテンツ]**」を選択します。「**[!UICONTROL 次へ]**」をクリックします。

1. 「**[!UICONTROL 公開鍵をアップロード]**」を選択します。[!DNL Experience Manager]からダウンロードした証明書ファイルを指定します。[!UICONTROL 公開鍵が正常にアップロード]されたというメッセージが表示されます。「**[!UICONTROL 次へ]**」をクリックします。

   [!UICONTROL 新しいサービスアカウント（JWT）秘密鍵証明書を作成]ページにはサービスアカウントの公開鍵が表示されます。

1. 「**[!UICONTROL 次へ]**」をクリックします。

1. **[!UICONTROL 製品プロファイルを選択]**&#x200B;ページで、「**[!UICONTROL スマートコンテンツサービス]**」を選択します。「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   設定に関する詳細情報がページに表示されます。このページを開いたままにしてこれらの値をコピーし、[!DNL Experience Manager] のクラウド設定の「[!UICONTROL Assets スマートタグサービス設定]」に追加して、スマートタグを設定します。

   ![「概要」タブで、統合について指定した情報を確認できます。](assets/integration_details.png)


   *図：Adobe 開発者コンソールの統合の詳細*

### スマートコンテンツサービスの設定 {#configure-smart-content-service}

統合を設定するには、Adobe 開発者コンソール統合から、[!UICONTROL テクニカルアカウント ID]、[!UICONTROL 組織 ID]、[!UICONTROL クライアント秘密鍵]、および[!UICONTROL クライアント ID] の各フィールドの値を使用します。スマートタグのクラウド設定を作成すると、[!DNL Experience Manager] デプロイメントからの API 要求を認証できるようになります。

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動して、[!UICONTROL クラウドサービス]コンソールを開きます。

1. 「**[!UICONTROL アセットのスマートタグ]**」で、上記で作成した設定を開きます。サービスの設定ページで、「**[!UICONTROL 編集]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、「**[!UICONTROL サービス URL]**」および「**[!UICONTROL 認証サーバー]**」フィールドに事前入力された値を使用します。

1. [Adobe 開発者コンソールの統合](#create-adobe-i-o-integration)で生成した次の値を使用して、[!UICONTROL API キー]、[!UICONTROL テクニカルアカウント ID]、[!UICONTROL 組織 ID]、および[!UICONTROL クライアント秘密鍵]の各フィールドにコピーします。

   | [!UICONTROL アセットのスマートタグサービス設定] | [!DNL Adobe Developer Console] 統合フィールド |
   |--- |--- |
   | [!UICONTROL API キー] | [!UICONTROL クライアント ID] |
   | [!UICONTROL テクニカルアカウント ID] | [!UICONTROL テクニカルアカウント ID] |
   | [!UICONTROL 組織 ID] | [!UICONTROL 組織 ID] |
   | [!UICONTROL クライアントの秘密鍵] | [!UICONTROL クライアント秘密鍵] |

### 設定の検証 {#validate-the-configuration}

設定を完了したら、JMX MBean を使用して設定を検証できます。検証するには、次の手順に従います。

1. [!DNL Experience Manager] サーバー （`https://[aem_server]:[port]`）にアクセスします。

1. **[!UICONTROL ツール]**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;に移動して、OSGi コンソールを開きます。**[!UICONTROL メイン]／[!UICONTROL JMX]** をクリックします。

1. 「`com.day.cq.dam.similaritysearch.internal.impl`」をクリックします。**[!UICONTROL SimilaritySearch Miscellaneous Tasks]** が開きます。

1. 「`validateConfigs()`」をクリックします。**[!UICONTROL 設定を検証]**&#x200B;ダイアログで、「**[!UICONTROL 起動]**」をクリックします。

同じダイアログに検証結果が表示されます。

### [!UICONTROL DAM アセットの更新]ワークフローでのスマートタグの有効化（オプション） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動します。

1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルを選択します。

1. ツールバーの「**[!UICONTROL 編集]**」をクリックします。

1. サイドパネルを展開して、ステップを表示します。「DAM ワークフロー」セクションの「**[!UICONTROL スマートタグアセット]**」ステップをドラッグして、「**[!UICONTROL サムネールを処理]**」ステップの後に配置します。

   ![「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加](assets/smart-tag-in-dam-update-asset-workflow.png)

   *図：「[!UICONTROL DAM アセットの更新]」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加。*

1. そのステップを編集モードで開きます。「**[!UICONTROL 詳細設定]**」で、「**[!UICONTROL ハンドラー処理の設定]**」オプションが選択されていることを確認します。

   ![DAM アセットの更新ワークフローを設定して、スマートタグステップを追加する](assets/smart-tag-step-properties-workflow1.png)


   *図：DAM アセットの更新ワークフローを設定して、スマートタグステップを追加する*

1. 自動タグ付けのステップに失敗してもワークフローを完了させたい場合は、「**[!UICONTROL 引数]**」タブで「**[!UICONTROL エラーを無視]**」を選択します。

   ![DAM アセットの更新ワークフローを設定してスマートタグステップを追加し、ハンドラー処理の設定を選択する](assets/smart-tag-step-properties-workflow2.png)


   *図：DAM アセットの更新ワークフローを設定してスマートタグステップを追加し、ハンドラー処理の設定を選択する*

   フォルダーでスマートタグが有効になっているかに関わらずアップロード時にアセットをタグ付けするには、「**[!UICONTROL スマートタグフラグを無視]**」を選択します。

   ![DAM アセットの更新ワークフローを設定してスマートタグステップを追加し、「スマートタグフラグを無視」を選択する](assets/smart-tag-step-properties-workflow3.png)


   *図：DAM アセットの更新ワークフローを設定してスマートタグステップを追加し、「スマートタグフラグを無視」を選択する*

1. 「**[!UICONTROL OK]**」をクリックして、プロセスステップを閉じ、ワークフローを保存します。

## スマートコンテンツサービスのトレーニング {#training-the-smart-content-service}

スマートコンテンツサービスでビジネス上の分類を認識できるように、ビジネスに関連するタグが既に含まれているアセットのセットに対してサービスを実行します。スマートコンテンツサービスでブランド画像を効果的にタグ付けできるようにするには、トレーニング画像が一定のガイドラインに従っている必要があります。トレーニングが完了すると、サービスは、類似するアセットのセットに同じ分類を適用できるようになります。

サービスのトレーニングを複数回実施すると、関連性の高いタグを適用する能力が向上します。トレーニングサイクルが終了するたびに、タグ付けワークフローを実行し、アセットが適切にタグ付けされるかどうかを確認します。

スマートコンテンツサービスのトレーニングは、定期的に実施することも、必要に応じて実施することもできます。

>[!NOTE]
>
>トレーニングワークフローは、フォルダーに対してのみ実行されます。

### トレーニングのガイドライン {#guidelines-for-training}

最適な結果を得るには、トレーニングセット内の画像が以下のガイドラインに準拠している必要があります。

**数とサイズ**：タグ 1 つにつき 30 以上の画像が必要です。長辺が 500 ピクセル以上である必要があります。

**一貫性**：特定のタグに使用する画像は、視覚的に似ています。

例えば、以下の画像は似ていないので、これらの画像すべてを `my-party`（トレーニング用）としてタグ付けするのは適切ではありません。

![トレーニングガイドラインの例を示すイラスト](/help/assets/assets/do-not-localize/coherence.png)

**対象範囲**：多様性に富んだトレーニング画像を使用します。その目的は、数は少なくても多様性の高い例を提供することで、Experience Manager が適切なものに焦点を絞れるようにすることです。見た目が大きく異なる画像に同じタグを適用する場合は、それぞれの種類に 5 つ以上の例を含めてください。

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

スマートコンテンツサービスを有効にして、フォルダー内のアセットおよび関連するタグに関する定期的なトレーニングを実施することができます。アセットフォルダーの[!UICONTROL プロパティ]ページを開き、「**[!UICONTROL 詳細]**」タブで「**[!UICONTROL スマートタグを有効にする]**」を選択し、変更内容を保存します。

![enable_smart_tags](assets/enable_smart_tags.png)

フォルダーに対してこのオプションを選択すると、[!DNL Experience Manager] によりレーニングワークフローが自動的に実行され、フォルダーのアセットおよびそのタグに関するスマートコンテンツサービスのトレーニングが実施されます。デフォルトでは、トレーニングワークフローは週に 1 回、土曜日の午前 0 時 30 分に実行されます。

### オンデマンドのトレーニング {#on-demand-training}

ワークフローコンソールから、必要に応じていつでもスマートコンテンツサービスのトレーニングをおこなうことができます。

1. [!DNL Experience Manager] インターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動します。
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL スマートタグトレーニング]**」ワークフローを選択し、ツールバーの「**[!UICONTROL ワークフローを開始]**」をクリックします。
1. **[!UICONTROL ワークフローを実行]**&#x200B;ダイアログで、サービスのトレーニングに使用するタグ付けされたアセットが格納されているペイロードフォルダーを参照します。
1. ワークフローのタイトルを指定し、コメントを追加します。次に、「**[!UICONTROL 実行]**」をクリックします。アセットとタグがトレーニングのために送信されます。

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>フォルダー内のアセットがトレーニング用に処理されると、後続のトレーニングサイクルでは、変更されたアセットのみが処理されます。

### トレーニングレポートの表示 {#viewing-training-reports}

アセットのトレーニングセット内のタグに関するスマートコンテンツサービスのトレーニングが実施されたかどうかを確認するには、レポートコンソールでトレーニングワークフローレポートを調べます。

1. [!DNL Experience Manager] インターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL レポート]**&#x200B;に移動します。
1. **[!UICONTROL アセットレポート]**&#x200B;ページで、「**[!UICONTROL 作成]**」をクリックします。
1. 「**[!UICONTROL スマートタグトレーニング]**」レポートを選択し、ツールバーで「**[!UICONTROL 次へ]**」をクリックします。
1. レポートのタイトルと説明を指定します。「**[!UICONTROL レポートをスケジュール]**」で、「**[!UICONTROL 今すぐ]**」オプションを選択したままにします。レポートを後で生成するようにスケジュールするには、「**[!UICONTROL 後で]**」を選択し、日時を指定します。次に、ツールバーの「**[!UICONTROL 作成]**」をクリックします。
1. **[!UICONTROL アセットレポート]**&#x200B;ページで、生成したレポートを選択します。レポートを表示するには、ツールバーの「**[!UICONTROL 表示]**」アイコンをクリックします。
1. レポートの詳細をレビューします。

   レポートには、トレーニングしたタグのトレーニングステータスが表示されます。「**[!UICONTROL トレーニングステータス]**」列の緑色は、そのタグについて、スマートコンテンツサービスのトレーニングが実施されたことを示します。黄色は、特定のタグに関するサービスのトレーニングが完全には実施されていないことを示します。この場合、特定のタグを含む画像をさらに追加し、トレーニングワークフローを実行して、そのタグに関するサービスのトレーニングを完全に実施します。

   このレポートにタグが表示されない場合は、それらのタグに関するトレーニングワークフローを再度実行してください。

1. レポートをダウンロードするには、リストから対象のレポートを選択し、ツールバーの「**[!UICONTROL ダウンロード]**」をクリックします。レポートが Microsoft Excel スプレッドシートとしてダウンロードされます。

## 制限事項 {#limitations}

* 拡張スマートタグは、画像とそのタグの学習モデルにもとづいています。これらのモデルは、タグを識別するうえで常に完璧であるわけではありません。スマートコンテンツサービスの現行バージョンには次の制限事項があります。

   * 画像内の細かい違いを認識することはできません。例えば、シャツのサイズが細身か標準かなどの違いは認識できません。
   * 画像の細かい模様や部分に基づいてタグを識別することはできません。例えば、T シャツのロゴなどです。
   * タグ付けは、[!DNL Experience Manager] がサポートされているロケールでサポートされています。言語の一覧については、](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html?lang=ja)スマートコンテンツサービスのリリースノート[を参照してください。

* スマートタグ（通常または拡張）付きのアセットを検索するには、[!DNL Assets] のオムニサーチ（全文検索）を使用します。スマートタグには個別の検索用述語はありません。

>[!MORELIKETHIS]
>
>* [スマートタグの概要とスマートタグのトレーニング方法](enhanced-smart-tags.md)
>* [スマートタグに関するビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html?lang=ja)

