---
title: フォームポータルのコンポーネントの有効化
seo-title: Enabling forms portal components
description: デフォルトでは、Forms Portal コンポーネントは無効になっています。 Document Services グループと Document Services Predicates グループを有効にして、Forms Portal コンポーネントを有効にします。
seo-description: Out of the box, Forms Portal components are disabled. Enable Document Services and Document Services Predicates groups to enable Forms Portal components.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 53%

---

# フォームポータルのコンポーネントの有効化 {#enabling-forms-portal-components}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html?lang=ja) |
| AEM 6.5 | この記事 |

フォームポータルのコンポーネントは、デフォルトでは使用できません。 AEM サイドキックで使用可能なコンポーネントのリストにコンポーネントを表示するには、次の手順を実行します。

1. Web サイトのオーサーインスタンスにログインし、AEM Sites ページを開きます。

1. 静的テンプレートを使用するページでは、次の手順を実行します。

   1. ページヘッダーで、「 」を選択します。 ![キャンバスドロップダウン](assets/canvas-drop-down.png) > **デザイン** をクリックして、デザインモードでページを開きます。
   1. 任意のコンポーネント（青い境界線付き）を選択し、「 」を選択します。 ![フィールドレベル](assets/field-level.png) 現在のコンポーネントを含む段落システムを選択します。
   1. 段落システムで、 ![settings_icon](assets/settings_icon.png) をクリックして、段落システムの編集ダイアログを開きます。
   1. **[!UICONTROL 許可されたコンポーネント]**&#x200B;のリストから、**[!UICONTROL Document Services]** コンポーネントと **[!UICONTROL Document Services Predicates]** コンポーネントのチェックボックスをオンにします。「**[!UICONTROL OK]**」を選択します。

1. 動的テンプレートを使用するページでは、次の手順を実行します。

   1. ページヘッダーで、「 」を選択します。 ![プロパティ](assets/properties.png) > **テンプレートを編集** をクリックして、ページのテンプレートを開きます。
   1. 選択 **レイアウトコンテナ** を選択し、 ![FeedManagement](/help/forms/using/assets/feedmanagement.png). Adobe Analytics の **許可されたコンポーネント** タブ、有効 **Document Services と Document Services の述語** オプション、および選択 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>また、コンポーネントを選択することで、これらのカテゴリから特定のコンポーネントを有効にすることもできます。 コンポーネントとその使用方法について詳しくは、 [フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md) および [ページへのリンクコンポーネントの埋め込み](/help/forms/using/embedding-link-component-page.md).

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
