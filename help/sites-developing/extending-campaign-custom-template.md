---
title: Adobe Campaign フォームコンポーネントを使用したカスタム AEM ページテンプレートの作成
seo-title: Adobe Campaign フォームコンポーネントを使用したカスタム AEM ページテンプレートの作成
description: Adobe Campaign フォームコンポーネントを使用するカスタムページテンプレートを作成します
seo-description: Adobe Campaign フォームコンポーネントを使用するカスタムページテンプレートを作成します
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 61%

---

# Adobe Campaign フォームコンポーネントを使用したカスタム AEM ページテンプレートの作成{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

このページでは、[Adobe Campaign Form](/help/sites-authoring/adobe-campaign-components.md)コンポーネントを使用するカスタムページテンプレートの作成方法を説明し、Geometrixxアウトドアテンプレート(`/apps/geometrixx-outdoors/components/page_campaign_profile`)の実装方法と、独自のカスタムテンプレートの作成時に必要となる重要な情報を示します。

>[!NOTE]
>
>[電子メールとフォームのサンプルは、Geometrixx でのみ使用できます](/help/sites-developing/we-retail.md)。パッケージ共有からサンプルGeometrixxコンテンツをダウンロードしてください。

Adobe Campaign フォームコンポーネントを使用してカスタム AEM ページテンプレートを作成するには以下が必要な条件となります。

1. **適切な resourceSuperType**

   ページコンポーネントが`mcm/campaign/components/profile`から継承されていることを確認します。

   これは、サーブレットが情報を取得して保存するために必要です

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext 設定**

   clientcontextの設定(`/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`)を見ると、次の設定が表示されます。

   * ClientContextが`/etc/clientcontext/campaign`を指す
   * 追加の *config* ノードもあります。

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp（/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp）**

   **head.jsp** には、**clientcontext-config** と **cloudservice-hook** を使用する以下の行があります。

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp（/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp）**

   **body.jsp**&#x200B;では、クラウドサービスがページの下部に読み込まれます。

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Campaign のページプロパティ**

   Adobe Campaign テンプレートを選択できるようにするには、「**Campaign**」タブを使用して、ページプロパティを拡張します。

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **テンプレートの設定**

   テンプレート(`/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`)には、次のデフォルト値が表示されます。

   | **acMapping** | mapRecipient（Adobe Campaign 6.1 の場合）、profile（Adobe Campaign Standard の場合） |
   |---|---|
   | **acTemplateId** | mail |

   ![chlimage_1-204](assets/chlimage_1-204.png)
