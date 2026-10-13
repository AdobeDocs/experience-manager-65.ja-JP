---
title: OAuth 2.0 クライアント資格情報フローを使用した Salesforce と AEM Forms の統合
description: OAuth 2.0 クライアント資格情報フローを使用した Salesforce と AEM Forms の統合手順
exl-id: 4c356aa6-ebd4-40b9-89e3-bc4519e4a7c5
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 4876a742-a341-5402-aba7-e749c45e777c
    internal-label: Form Data Model
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 98%
---
# OAuth 2.0 クライアント資格情報フローを使用したSalesforceの統合  {#configure-salesforce-with-ouath-2.0-client-credential}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=ja) |
| AEM 6.5 | この記事 |

OAuth 2.0 クライアント資格情報を使用して、AEM Forms を Salesforce アプリケーションと統合できます。 OAuth 2.0 クライアント資格情報は、ユーザーの関与なしに直接通信するための標準で安全な方法です。

![AEM Forms と Salesforce アプリケーション間の通信を設定する際のワークフロー](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms が、Salesforce 接続アプリケーションで定義されたクライアント資格情報（Consumer key と Consumer secret）を交換して、アクセストークンを取得します。

認証コードフロー認証を使用した認証に OAuth 2.0 クライアント資格情報を使用すると、次のような複数のメリットがあります。

* OAuth 2.0 クライアント資格情報認証では、1 人のユーザーにつき 5 つ以上の接続を使用できます。
* AEM データソースの設定は、AEM ユーザーの非アクティブ化、アクセスの変更、パスワードの更新に対して引き続き機能します。

## 前提条件 {#prerequisites}

Salesforce アプリケーションと AEM 環境間の通信を設定する前に、次の手順を実行します。

* [OAuth 2.0 クライアント資格情報フローを使用した Salesforce 接続アプリ](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&type=5)および組織の API のみのユーザーを作成し、アプリの Consumer key と Consumer secret を取得します。

* Swagger ファイルが組織の API に合わせて適切に設定されていることを確認します。 または、AEM 環境での利用に合わせて、最初から [Swagger ファイルを作成](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=ja)することもできます。

>[!NOTE]
>
> AEM 6.5 では、Swagger 2.0 ファイル仕様のみをサポートします。

## クライアント資格情報フローで Salesforce を設定する手順 {#steps-to-create-aem-datasource-configuration}

1. オーサーインスタンスにログインします。
1. **[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL データソース]**&#x200B;に移動します。
1. 設定フォルダーを選択します。
1. 「**[!UICONTROL 作成]**」をクリックします。**[!UICONTROL データソース設定を作成]**&#x200B;が表示されます。
1. **[!UICONTROL タイトル]**&#x200B;を指定し、**[!UICONTROL サービスタイプ]**&#x200B;に「**[!UICONTROL RESTful サービス]**」を選択します。
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. **[!UICONTROL Swagger ソース]**&#x200B;に「**[!UICONTROL ファイル]」を選択します。**
   >[!NOTE]
   >
   > Swagger ファイルを選択するとすぐに、スキーム、ホスト名、ベースパスが自動的に設定されます。

1. 「**[!UICONTROL 参照]**」をクリックして、作成した Swagger ファイルをローカルマシンからアップロードします。
1. **[!UICONTROL 認証タイプ]**&#x200B;に「**[!UICONTROL OAuth 2.0]**」を選択します。**[!UICONTROL 認証設定]**&#x200B;パネルが表示されます。
1. **[!UICONTROL 付与タイプ]**&#x200B;に「**[!UICONTROL クライアント資格情報]**」を選択します。
1. Salesforce 接続アプリから取得した&#x200B;**[!UICONTROL クライアント ID]** と&#x200B;**[!UICONTROL クライアント秘密鍵]**&#x200B;を指定します。
1. **[!UICONTROL アクセストークンの URL]** を次の形式で指定します
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`。

   >[!NOTE]
   >
   > 各組織には独自のドメイン名があります。

1. 「**[!UICONTROL 接続をテスト]**」をクリックします。
1. 接続に成功した場合は、「**[!UICONTROL 作成]**」ボタンをクリックします。

これで、[フォームデータモデルを作成](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=ja)して、設定したデータソースをアダプティブフォームと統合できます。
