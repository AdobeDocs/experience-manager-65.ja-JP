---
title: Smart Content Serviceを使用してアセットのタグ付けを設定します。
description: Learn how to configure smart tagging and enhanced smart tagging in [!DNL Adobe Experience Manager], using the Smart Content Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 55%

---


# Configure asset tagging using the Smart Content Service {#configure-asset-tagging-using-the-smart-content-service}

You can integrate [!DNL Adobe Experience Manager] with the Smart Content Service using Adobe Developer Console. Use this configuration to access the Smart Content Service from within [!DNL Experience Manager].

この記事では、スマートコンテンツサービスの設定に必要となる以下の主要なタスクについて詳しく説明します。At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Content Service.

1. Create a Smart Content Service configuration in [!DNL Experience Manager] to generate a public key. [OAuth 統合用の公開証明書を取得します。](#obtain-public-certificate)
1. [Adobe 開発者コンソールで統合を作成し、生成した公開鍵をアップロードします。](#create-adobe-i-o-integration)
1. [Adobe Developer ConsoleのAPIキーと他の資格情報を使用して](#configure-smart-content-service) 、デプロイメントを設定します。
1. [設定をテストします](#validate-the-configuration)。
1. Optionally, [enable auto-tagging on asset upload](#enable-smart-tagging-in-the-update-asset-workflow-optional).

## 前提条件 {#prerequisites}

Smart Content Serviceを使用する前に、次の手順を実行してAdobe Developer Consoleで統合を作成します。

* 組織の管理者権限を持つ Adobe ID アカウントがあること。
* 組織でスマートコンテンツサービスが有効化されていること。

To enable Enhanced Smart Tags, in addition to the above, also install the latest [AEM service pack](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html).

## 公開証明書の取得 {#obtain-public-certificate}

公開証明書により、Adobe 開発者コンソールでプロファイルを認証できます。

1. ユーザーインターフェイスで、 [!DNL Experience Manager] ツール **[!UICONTROL /]** Cloud Service **[!UICONTROL /]** レガシCloud Serviceにアクセスします ****。

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、スマートタグ設定のタイトルと名前を指定します。「**[!UICONTROL 作成]**」をクリックします。
1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、以下の値を使用します。

   **[!UICONTROL サービス URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 認証サーバー]**: `https://ims-na1.adobelogin.com`

   その他のフィールドは現時点では空白のままにします（後で指定します）。「**[!UICONTROL OK]**」をクリックします。

   ![コンテンツサービスURLを提供するExperience Managerスマートコンテンツサービスダイアログ](assets/aem_scs.png)

   >[!NOTE]
   >
   >The URL provided as [!UICONTROL Service URL] is not accessible via browser and generates a 404 error. この設定は、 [!UICONTROL サービスURL] パラメーターと同じ値で正常に機能します。 For the overall service status and maintenance schedule, see [https://status.adobe.com](https://status.adobe.com).

1. Click **[!UICONTROL Download Public Certificate for OAuth Integration]**, and download the public certificate file `AEM-SmartTags.crt`.

   ![スマートタグ付けサービス用に作成された設定の表現](assets/smart-tags-download-public-cert.png)

### Reconfigure when a certificate expires {#certrenew}

証明書の有効期限が切れると、信頼されなくなります。 期限切れの証明書は更新できません。新しい証明書を追加するには、以下の手順に従います。

1. [!DNL Experience Manager] デプロイメントに管理者としてログインします。**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;をクリックします。

1. **[!UICONTROL dam-update-service]** ユーザーを見つけてクリックします。「**[!UICONTROL キーストア]**」タブをクリックします。
1. 証明書の有効期限が切れた既存の **[!UICONTROL similaritysearch]** キーストアを削除します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![キーストア内の既存の類似性検索エントリを削除し、新しいセキュリティ証明書を追加します](assets/smarttags_delete_similaritysearch_keystore.png)

   *図：キーストアの既存の`similaritysearch`エントリを削除して新しいセキュリティ証明書を追加.*

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動します。**[!UICONTROL アセットのスマートタグ]**／**[!UICONTROL 設定を表示]**／**[!UICONTROL 利用可能な設定]**&#x200B;をクリックします。必要な設定をクリックします。

1. 公開証明書をダウンロードするには、「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をクリックします。
1. [https://console.adobe.io](https://console.adobe.io) にアクセスし、**[!UICONTROL 統合]**&#x200B;ページで既存のスマートコンテンツサービスに移動します。新しい証明書をアップロードします。For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

## Adobe Developer Console統合の作成 {#create-adobe-i-o-integration}

Smart Content Service APIを使用するには、Adobe Developer ConsoleでAPIキー、テクニカルアカウントID、組織IDおよびクライアントシークレットを生成するための統合を作成します。

1. ブラウザーで [https://console.adobe.io](https://console.adobe.io/) にアクセスします。適切なアカウントを選択し、関連付けられた組織の役割がシステム管理者であることを確認します。
1. 任意の名前でプロジェクトを作成します。「**[!UICONTROL API を追加]**」をクリックします。
1. **[!UICONTROL API を追加]**&#x200B;ページで、「**[!UICONTROL Experience Cloud]**」を選択し、「**[!UICONTROL スマートコンテンツ]**」を選択します。「**[!UICONTROL 次へ]**」をクリックします。
1. 「**[!UICONTROL 公開鍵をアップロード]**」を選択します。[!DNL Experience Manager]からダウンロードした証明書ファイルを指定します。[!UICONTROL 公開鍵が正常にアップロード]されたというメッセージが表示されます。「**[!UICONTROL 次へ]**」をクリックします。
1. [!UICONTROL 新しいサービスアカウント（JWT）秘密鍵証明書を作成]ページには、設定したサービスアカウントの公開鍵が表示されます。「**[!UICONTROL 次へ]**」をクリックします。
1. **[!UICONTROL 製品プロファイルを選択]**&#x200B;ページで、「**[!UICONTROL スマートコンテンツサービス]**」を選択します。「**[!UICONTROL 設定済み API を保存]**」をクリックします。設定に関する詳細情報がページに表示されます。[!DNL Experience Manager] でスマートタグをさらに設定する場合は、このページを開いたままにして、これらの値をコピーし、Experience Manager に追加します。

   ![「概要」タブで、統合について指定した情報を確認できます。](assets/integration_details.png)

## スマートコンテンツサービスの設定 {#configure-smart-content-service}

統合を設定するには、Adobe Developer Console統合の「テクニカルアカウントID」、「組織ID」、「クライアントシークレット」、「認証サーバー」および「APIキー」フィールドの値を使用します。 Creating a Smart Tags cloud configuration allows authentication of API requests from the [!DNL Experience Manager] deployment.

1. In [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Legacy Cloud Services]** to open the [!UICONTROL Cloud Services] console.
1. 「**[!UICONTROL アセットのスマートタグ]**」で、上記で作成した設定を開きます。サービスの設定ページで、「**[!UICONTROL 編集]**」をクリックします。
1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、「**[!UICONTROL サービス URL]**」および「**[!UICONTROL 認証サーバー]**」フィールドに事前入力された値を使用します。
1. 「**[!UICONTROL API キー]**」、「**[!UICONTROL テクニカルアカウント ID]**」、「**[!UICONTROL 組織 ID]**」、「**[!UICONTROL クライアントの秘密鍵]**」の各フィールドでは、上記で生成された値を使用します。

## 設定の検証 {#validate-the-configuration}

設定を完了したら、JMX MBean を使用して設定を検証できます。検証するには、次の手順に従います。

1. で [!DNL Experience Manager] サーバーにアクセスし `https://[aem_server]:[port]`ます。
1. **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **** Webコンソールに移動し、OSGiコンソールを開きます。 **[!UICONTROL メイン]/[!UICONTROL JMXをクリックします]**。
1. 「`com.day.cq.dam.similaritysearch.internal.impl`」をクリックします。It opens **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.
1. 「`validateConfigs()`」をクリックします。In the **[!UICONTROL Validate Configurations]** dialog, click **[!UICONTROL Invoke]**. 検証結果は、同じダイアログに表示されます。

## Enable smart tagging in the [!UICONTROL DAM Update Asset] workflow (Optional) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルを選択します。
1. ツールバーの「**[!UICONTROL 編集]**」をクリックします。
1. サイドパネルを展開して、ステップを表示します。「DAM ワークフロー」セクションの「**[!UICONTROL スマートタグアセット]**」ステップをドラッグして、「**[!UICONTROL サムネールを処理]**」ステップの後に配置します。

   ![「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加](assets/smart-tag-in-dam-update-asset-workflow.png)

   *図：「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加。*

1. そのステップを編集モードで開きます。「**[!UICONTROL 詳細設定]**」で、「**[!UICONTROL ハンドラー処理の設定]**」オプションが選択されていることを確認します。

   ![DAM更新アセットワークフローの設定とスマートタグ手順の追加](assets/smart-tag-step-properties-workflow1.png)

1. 自動タグ付けのステップに失敗してもワークフローを完了させたい場合は、「**[!UICONTROL 引数]**」タブで「**[!UICONTROL エラーを無視]**」を選択します。

   ![DAMアセットの更新ワークフローを設定し、スマートタグ手順を追加してハンドラーの設定を選択します](assets/smart-tag-step-properties-workflow2.png)

   フォルダーでスマートタグが有効になっているかに関わらずアップロード時にアセットをタグ付けするには、「**[!UICONTROL スマートタグフラグを無視]**」を選択します。

   ![DAM Update Assetワークフローを設定し、スマートタグ手順を追加して、「スマートタグフラグを無視」を選択します](assets/smart-tag-step-properties-workflow3.png)

1. 「**[!UICONTROL OK]**」をクリックして、プロセスステップを閉じ、ワークフローを保存します。

>[!MORELIKETHIS]
>
>* [スマートタグの管理](managing-smart-tags.md)
>* [スマートタグの概要とトレーニング方法](enhanced-smart-tags.md)
>* [Smart Content Serviceをトレーニングするためのガイドラインとルール](smart-tags-training-guidelines.md)
>* [スマートタグの設定方法に関するビデオチュートリアル](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

