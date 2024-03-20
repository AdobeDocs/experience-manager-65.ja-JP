---
title: フォームポータルのコンポーネントの有効化
description: 出荷時の設定では、フォームポータルコンポーネントは無効になっています。Document Services グループと Document Services Predicates グループを有効にして、フォームポータルコンポーネントを有効にします。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 100%

---

# フォームポータルのコンポーネントの有効化 {#enabling-forms-portal-components}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html?lang=ja) |
| AEM 6.5 | この記事 |

フォームポータルコンポーネントは、出荷時の設定では使用できません。AEM サイドキックで使用可能なコンポーネントのリストにコンポーネントを表示するには、次の手順を実行します。

1. Web サイトのオーサーインスタンスにログインし、AEM Sites ページを開きます。

1. 静的テンプレートを使用するページでは、次の手順を実行します。

   1. ページのヘッダーで、![canvas-drop-down](assets/canvas-drop-down.png)／**Design** を選択すると、デザインモードでページが表示されます。
   1. 任意の（青色の境界線の付いている）コンポーネントを選択してから ![field-level](assets/field-level.png) を選択し、現在のコンポーネントが含まれている段落システムを選択します。
   1. 段落システムで ![settings_icon](assets/settings_icon.png) を選択して段落システムの編集ダイアログを開きます。
   1. **[!UICONTROL 許可されたコンポーネント]**&#x200B;のリストから、**[!UICONTROL Document Services]** コンポーネントと **[!UICONTROL Document Services Predicates]** コンポーネントのチェックボックスをオンにします。「**[!UICONTROL OK]**」を選択します。

1. 動的テンプレートを使用するページでは、次の手順を実行します。

   1. ページのヘッダーで、![プロパティ](assets/properties.png)／**テンプレートの編集**&#x200B;を選択してページのテンプレートを開きます。
   1. 「**レイアウトコンテナ**」を選択し、「![FeedManagement](/help/forms/using/assets/feedmanagement.png)」を選択します。「**許可されたコンポーネント**」タブで「**Document Services」オプションと「Document Service Predicates**」オプションを有効にして「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」を選択します。

>[!NOTE]
>
>また、コンポーネントを選択して、これらのカテゴリから特定のコンポーネントを有効にすることもできます。コンポーネントとその使用方法について詳しくは、[フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)と[ページでのリンクコンポーネントの埋め込み](/help/forms/using/embedding-link-component-page.md)を参照してください。

これで、コンポーネントブラウザーで Document Services コンポーネントカテゴリと Document Services Predicates コンポーネントカテゴリを使用できるようになります。コンポーネントは、同じテンプレートを使用するすべてのページで有効になります。

## 関連記事

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成 ](/help/forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](/help/forms/using/integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](/help/forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム公開の概要](/help/forms/using/introduction-publishing-forms.md)
