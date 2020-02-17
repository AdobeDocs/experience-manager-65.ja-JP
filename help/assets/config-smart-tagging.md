---
title: スマートコンテンツサービスを使用したアセットのタグ付けの設定
description: スマートコンテンツサービスを使用して、AEM でスマートタグと拡張スマートタグを設定する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Configure asset tagging using the Smart Content Service {#configure-asset-tagging-using-the-smart-content-service}

Adobe I/O を使用して、Adobe Experience Manager（AEM）とスマートコンテンツサービスを統合できます。この設定を使用すると、AEM 内からスマートコンテンツサービスにアクセスできます。

この記事では、スマートコンテンツサービスの設定に必要となる以下の主要なタスクについて詳しく説明します。バックエンドでは、スマートコンテンツサービスに要求を転送する前に、AEM サーバーが Adobe IO ゲートウェイでサービスの資格情報を認証します。

* AEM でスマートコンテンツサービス設定を作成して、公開鍵を生成します。OAuth 統合用の公開証明書を取得します。
* Adobe I/O で統合を作成し、生成した公開鍵をアップロードします。
* API キーやその他の Adobe I/O の資格情報を使用して AEM インスタンスを設定します。
* （オプション）アセットアップロード時の自動タグ付けを有効化します。

## 前提条件 {#prerequisites}

Adobe I/O で統合を作成してスマートコンテンツサービスを使用する前に、以下の事項を確認します。

* 組織の管理者権限を持つ Adobe ID アカウントがあること。
* 組織でスマートコンテンツサービスが有効化されていること。

## 公開証明書の取得 {#obtain-public-certificate}

公開証明書により、Adobe I/O でプロファイルを認証できます。

1. AEM ユーザーインターフェイスで、AEM のロゴをタップし、**[!UICONTROL ツール／クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動します。

1. クラウドサービスページで、「**[!UICONTROL アセットのスマートタグ]**」の「**[!UICONTROL 今すぐ設定]**」をタップまたはクリックします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、スマートタグ設定のタイトルと名前を指定します。「**[!UICONTROL 作成]**」をタップまたはクリックします。
1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、以下の値を使用します。

   **[!UICONTROL サービス URL]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 認証サーバー]**: `https://ims-na1.adobelogin.com`

   その他のフィールドは現時点では空白のままにします（後で指定します）。「**[!UICONTROL OK]**」をタップまたはクリックします。

   ![コンテンツサービスの URL を指定するための AEM スマートコンテンツサービスダイアログ](assets/aem_scs.png)

1. 「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をタップまたはクリックし、公開証明書ファイル `AEM-SmartTags.crt` をダウンロードします。

   ![スマートタグ付けサービス用に作成された設定の表現](assets/download_link.png)

### Reconfigure when a certificate expires {#certrenew}

証明書の有効期限が切れると、証明書は信頼されなくなります。新しい証明書を追加するには、以下の手順に従います。期限切れの証明書は更新できません。

1. AEM デプロイメントに管理者としてログインします。**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL ユーザー]**&#x200B;をクリックします。

1. **[!UICONTROL dam-update-service]** ユーザーを見つけてクリックします。「**[!UICONTROL キーストア]**」タブをクリックします。
1. 証明書の有効期限が切れた既存の **[!UICONTROL similaritysearch]** キーストアを削除します。「**[!UICONTROL 保存して閉じる]**」をクリックします。

   ![キーストアの既存の similaritysearch エントリを削除して新しいセキュリティ証明書を追加](assets/smarttags_delete_similaritysearch_keystore.png)

   キーストアの既存の similaritysearch エントリを削除して新しいセキュリティ証明書を追加

1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動します。**[!UICONTROL アセットのスマートタグ]**／**[!UICONTROL 設定を表示]**／**[!UICONTROL 利用可能な設定]**&#x200B;をクリックします。必要な設定をクリックします。

1. 公開証明書をダウンロードするには、「**[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**」をクリックします。
1. [https://console.adobe.io](https://console.adobe.io) にアクセスし、**[!UICONTROL 統合]**&#x200B;ページで既存のスマートコンテンツサービスに移動します。新しい証明書をアップロードします。詳細については、[Adobe I/O 統合の作成](#create-adobe-i-o-integration)の手順を参照してください。

## Adobe I/O 統合の作成 {#create-adobe-i-o-integration}

スマートコンテンツサービス API を使用するには、Adobe I/O で統合を作成して、API キー、テクニカルアカウント ID、組織 ID およびクライアントの秘密鍵を生成します。

1. [https://console.adobe.io](https://console.adobe.io/) にアクセスします。
1. 「統合」ペ **[!UICONTROL ージで]** 、適切なアカウントを選択し、関連する組織の役割がシステム管理者であることを確認します。
1. Tap **[!UICONTROL New integration]**.
1. **[!UICONTROL Create a new integration]** ページで、「**[!UICONTROL Access an API]**」を選択します。「続行」を **[!UICONTROL タップしま]**&#x200B;す。
1. 「 **[!UICONTROL Experience Cloud]**」で「スマートコン **[!UICONTROL テンツ」を選択します]**。 「続行」を **[!UICONTROL タップしま]**&#x200B;す。

   ![新しい統合を作成する場合は、使用可能なオプションから「Experience Cloud」の「Smart Content」を選択します。](assets/smart_content.png)

1. 次のページで、「**[!UICONTROL New integration]**」を選択します。「**[!UICONTROL Continue]**」をタップまたはクリックします。
1. **[!UICONTROL Integration Details]** ページで、統合ゲートウェイの名前を指定し、説明を追加します。
1. 「**[!UICONTROL Public keys certificates]**」で、上記でダウンロードした `AEM-SmartTags.crt` ファイルをアップロードします。
1. 「**[!UICONTROL Create Integration]**」をタップまたはクリックします。
1. 統合の情報を表示するには、「**[!UICONTROL Continue to integration details]**」をタップまたはクリックします。

   ![「Overview」タブで、統合について指定した情報を確認できます。](assets/integration_details.png)

## スマートコンテンツサービスの設定 {#configure-smart-content-service}

統合を設定するには、Adobe I/O 統合のテクニカルアカウント ID、組織 ID、クライアントの秘密鍵、認証サーバーおよび API キーのフィールドの値を使用します。スマートタグクラウド設定を作成すると、AEM インスタンスからの API 要求を認証できるようになります。

1. AEM ユーザーインターフェイスで、AEM のロゴをタップまたはクリックします。**[!UICONTROL ツール／クラウドサービス／従来のクラウドサービス]**&#x200B;に移動して、クラウドサービスコンソールを開きます。
1. 「**[!UICONTROL アセットのスマートタグ]**」で、上記で作成した設定を開きます。サービスの設定ページで、「**[!UICONTROL 編集]**」をクリックします。
1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、「**[!UICONTROL サービス URL]**」および「**[!UICONTROL 認証サーバー]**」フィールドに事前入力された値を使用します。
1. 「**[!UICONTROL API キー]**」、「**[!UICONTROL テクニカルアカウント ID]**」、「**[!UICONTROL 組織 ID]**」、「**[!UICONTROL クライアントの秘密鍵]**」の各フィールドでは、上記で生成された値を使用します。

## 設定の検証 {#validate-the-configuration}

設定を完了したら、JMX MBean を使用して設定を検証できます。検証するには、次の手順に従います。

1. Access your AEM server at `https://[server]:[port]`.

1. **[!UICONTROL ツール／操作／Web コンソール]**&#x200B;に移動して、OSGi コンソールを開きます。**[!UICONTROL メイン／JMX]** を選択します。
1. 「**[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**」をクリックします。**[!UICONTROL SimilaritySearch Miscellaneous Tasks]** が開きます。
1. 「**[!UICONTROL validateConfigs()]**」をクリックします。In the **[!UICONTROL Validate Configurations]** dialog, click **[!UICONTROL Invoke]**.

   同じダイアログに検証結果が表示されます。

## アセットの更新ワークフローでのスマートタグの有効化（オプション） {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. AEM ユーザーインターフェイスで、AEM のロゴをタップまたはクリックし、**[!UICONTROL ツール／ワークフロー／モデル]**&#x200B;に移動します。
1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、「**[!UICONTROL DAM アセットの更新]**」ワークフローモデルを選択します。
1. ツールバーの「**[!UICONTROL 編集]**」をタップまたはクリックします。
1. サイドパネルを展開して、ステップを表示します。「DAM ワークフロー」セクションの「**[!UICONTROL スマートタグアセット]**」ステップをドラッグして、「**[!UICONTROL サムネールを処理]**」ステップの後に配置します。

   ![「DAM アセットの更新」ワークフローで「サムネールを処理」ステップの後に「スマートタグアセット」ステップを追加](assets/chlimage_1-105.png)

1. そのステップを編集モードで開きます。Under **[!UICONTROL Advanced Settings]**, ensure that the **[!UICONTROL Handler Advance]** option is selected.

   ![chlimage_1-3](assets/chlimage_1-106.png)

1. 自動タグ付けのステップに失敗してもワークフローを完了させたい場合は、「**[!UICONTROL 引数]**」タブで「**[!UICONTROL エラーを無視]**」を選択します。

   ![chlimage_1-4](assets/chlimage_1-107.png)

   フォルダーでスマートタグが有効になっているかに関わらずアップロード時にアセットをタグ付けするには、「**[!UICONTROL スマートタグフラグを無視]**」を選択します。

   ![chlimage_1-5](assets/chlimage_1-108.png)

1. Tap **[!UICONTROL OK]** to close the process step, and then save the workflow.

>[!MORELIKETHIS]
>
>* [スマートタグの管理](managing-smart-tags.md)
>* [スマートタグの概要とトレーニング方法](enhanced-smart-tags.md)
>* [Smart Content Serviceをトレーニングするためのガイドラインとルール](smart-tags-training-guidelines.md)
>* [スマートタグの設定方法に関するビデオチュートリアル](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

