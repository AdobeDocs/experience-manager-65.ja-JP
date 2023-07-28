---
title: OAuth 2.0 クライアント資格情報フローを使用したAEM Formsとの Salesforce 統合
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: OAuth 2.0 クライアント資格情報フローを使用して Salesforce とAEM Formsを統合する手順
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
exl-id: 31f2ccf8-1f4f-4d88-8c5f-ef1b7d1bfb4f
source-git-commit: f11bb43d914a43431cab408ca77690b6ba528a06
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 3%

---

# OAuth 2.0 クライアント資格情報フローを使用した Salesforce の統合  {#configure-salesforce-with-ouath-2.0-client-credential}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM 6.5 | この記事 |

OAuth 2.0 クライアント資格情報を使用して、AEM Formsを Salesforce アプリケーションと統合できます。 OAuth 2.0 クライアント資格情報は、ユーザーの関与なしに直接通信するための標準で安全な方法です。

![AEM Formsと Salesforce アプリケーション間の通信を設定する際のワークフロー](/help/forms/using/assets/salesforce-workflow.png)

AEM Formsが、Salesforce 接続アプリケーションで定義されたクライアント資格情報（消費者キーと消費者の秘密鍵）を交換して、アクセストークンを取得します。

認証コードフロー認証を使用した認証に OAuth 2.0 クライアント資格情報を使用すると、次のような複数のメリットがあります。

* OAuth 2.0 クライアント資格情報認証では、1 人のユーザーにつき 5 つ以上の接続を使用できます。
* AEMデータソースの設定は、AEMユーザーの非アクティブ化、アクセスの変更、パスワードの更新に対して引き続き機能します。

## 前提条件 {#prerequisites}

Salesforce アプリケーションとAEM環境間の通信を設定する前に、次の手順を実行します。

* の作成 [OAuth 2.0 クライアント資格情報フローを使用した Salesforce 接続アプリ](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) と組織の API のみのユーザーを含め、アプリの消費者キーと消費者の秘密鍵を取得します。

* Swagger ファイルが組織の API に合わせて適切に設定されていることを確認します。 または、 [Swagger ファイルを作成する](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) 最初から、AEM環境での使用に合わせてカスタマイズされます。
>[!NOTE]
>
> AEM 6.5 では、Swagger 2.0 ファイルの仕様のみがサポートされています。

+++

## クライアント資格情報フローで Salesforce を設定する手順 {#steps-to-create-aem-datasource-configuration}

1. オーサーインスタンスにログインします。
1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL データソース]**.
1. 設定フォルダーを選択します。
1. クリック **[!UICONTROL 作成]** そして **[!UICONTROL データソース設定を作成]** が表示されます。
1. 次を指定します。 **[!UICONTROL タイトル]** をクリックし、 **[!UICONTROL サービスタイプ]** as **[!UICONTROL RESTful サービス]**.
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. を選択します。 **[!UICONTROL Swagger ソース]** as **[!UICONTROL ファイル].**
   >[!NOTE]
   >
   > Swagger ファイルを選択すると、Scheme、Host 名、Base パスが自動的に設定されます。

1. 作成した Swagger ファイルをローカルマシンからアップロードするには、 **[!UICONTROL 参照]**.
1. を選択します。 **[!UICONTROL 認証タイプ]** as **[!UICONTROL OAuth 2.0]** そして **[!UICONTROL 認証設定]** パネルが表示されます。
1. を選択します。 **[!UICONTROL 付与タイプ]** as **[!UICONTROL クライアント資格情報]**.
1. 次を指定します。 **[!UICONTROL クライアント ID]** および **[!UICONTROL クライアントの秘密鍵]** Salesforce 接続アプリから取得しました。
1. 次を指定します。 **[!UICONTROL トークン URL にアクセス]** 形式で
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 各組織には固有のドメイン名があります。

1. クリック **[!UICONTROL 接続をテスト]**.
1. 接続に成功した場合は、 **[!UICONTROL 作成]** 」ボタンをクリックします。

次に、以下を実行できます。 [フォームデータモデルの作成](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) 設定済みのデータソースを Adaptive Formsと統合する場合。
