---
title: OAuth 2.0 クライアント資格情報フローを使用したAEM Formsとの Salesforce 統合
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: OAuth 2.0 クライアント資格情報フローを使用して Salesforce とAEM Formsを統合する手順
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
exl-id: 31f2ccf8-1f4f-4d88-8c5f-ef1b7d1bfb4f
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 3%

---

# OAuth 2.0 クライアント資格情報フローを使用した Salesforce の統合  {#configure-salesforce-with-ouath-2.0-client-credential}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html) |
| AEM 6.5 | この記事 |


AEM Formsを Salesforce アプリケーションと統合するには、OAuth 2.0 クライアント資格情報フローが使用されます。 これは、ユーザーの関与なしに直接通信を行うための、標準化され、安全な方法です。 このフローでは、クライアントアプリケーション (AEM Form) は、Salesforce 接続アプリケーションで定義されたクライアント資格情報を交換して、アクセストークンを取得します。 必要なクライアント資格情報には、消費者キーと消費者秘密鍵が含まれます。

## OAuth 2.0 クライアント資格情報フローを使用して Salesforce をAEM Formsと統合するメリット {#advantages-of-integrating-saleforce-aemforms}

AEM Formsは、OAuth 2.0 クライアント資格情報フローに加えて、認証コードフローと Salesforce の統合をサポートしています。 OAuth 2.0 認証コードフローでは、クライアントアプリケーション (AEM Forms) は Salesforce ユーザーに代わってリソースアクセスを取得しますが、いくつかの制限があります。

* 1 人のユーザーにつき最大 5 つの接続が許可されます。 それ以降の接続では、古い接続が自動的に取り消されます。
* ユーザーがアクティベートを解除されたり、アクセス権が失われたり、パスワードが更新されたりすると、AEMデータソース設定は機能しなくなります。

## 前提条件 {#prerequisites}

Salesforce とAEM環境間でデータを取得して取得するには、次の手順に進む前に、特定の前提条件が必要です。

+++ **クライアント資格情報フローと API 専用ユーザーを使用して Saleforce 接続アプリケーションを設定する**

OAuth 2.0 クライアント資格情報フローと組織の API 専用ユーザーを含む Salesforce 接続アプリを作成する必要があります。 詳細な手順については、この記事を参照してください。 [サーバー間統合用の OAuth 2.0 クライアント資格情報フロー](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5). これらの手順は、消費者キーと消費者の秘密鍵を取得するのに役立ちます。

>[!NOTE]
>
> AEMデータソース設定を作成する際には、必要に応じて、消費者キーと消費者秘密鍵をメモしておきます。

+++

+++ **Swagger ファイルの作成**

Swagger は、RESTful API を開発および説明するためのオープンソースのルール、仕様、ツールのセットです。 [Swagger ファイルの作成](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) Salesforce とAEM Formsを統合する前に

>[!NOTE]
>
> AEM 6.5 では、Swagger 2.0 ファイルの仕様のみがサポートされています。

+++

## クライアント資格情報フローで Salesforce を設定する手順 {#steps-to-create-aem-datasource-configuration}

1. オーサーインスタンスにログインします。
1. に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL データソース]**.
1. 設定フォルダーを選択します。
1. クリック **[!UICONTROL 作成]** そして **[!UICONTROL データソース設定を作成]** が表示されます。
1. 次を指定： **[!UICONTROL タイトル]** をクリックし、 **[!UICONTROL サービスタイプ]** as **[!UICONTROL RESTful サービス]**.
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. を選択します。 **[!UICONTROL Swagger ソース]** as **[!UICONTROL ファイル].**
   >[!NOTE]
   >
   > Swagger ファイルを選択すると、Scheme、Host 名、Base パスが自動的に設定されます。

1. 作成した Swagger ファイルをローカルマシンから、 **[!UICONTROL 参照]**.
1. を選択します。 **[!UICONTROL 認証タイプ]** as **[!UICONTROL OAuth 2.0]** そして **[!UICONTROL 認証設定]** パネルが表示されます。
1. を選択します。 **[!UICONTROL 付与タイプ]** as **[!UICONTROL クライアント資格情報]**.
1. 次を指定： **[!UICONTROL クライアント ID]** および **[!UICONTROL クライアント秘密鍵]** Salesforce 接続アプリから取得しました。
1. 次を指定： **[!UICONTROL トークン URL にアクセス]** 形式
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 各組織には固有のドメイン名があります。

1. クリック **[!UICONTROL 接続をテスト]**.
1. 接続に成功した場合は、 **[!UICONTROL 作成]** 」ボタンをクリックします。

次に、以下を実行できます。 [フォームデータモデルの作成](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) 設定済みのデータソースをアダプティブフォームに統合する場合。
