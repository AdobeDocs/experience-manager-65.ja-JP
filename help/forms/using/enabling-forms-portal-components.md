---
title: フォームポータルコンポーネントの有効化
seo-title: フォームポータルコンポーネントの有効化
description: デフォルトでは、フォームポータルコンポーネントは無効になっています。フォームポータルコンポーネントを有効にするには、Document Services と Document Services Predicates グループを有効にします。
seo-description: デフォルトでは、フォームポータルコンポーネントは無効になっています。フォームポータルコンポーネントを有効にするには、Document Services と Document Services Predicates グループを有効にします。
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
translation-type: tm+mt
source-git-commit: a209b2dda04985a3f2d7c6838f11f0b5dc62d520
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 48%

---


# フォームポータルコンポーネントの有効化  {#enabling-forms-portal-components}

フォームポータルコンポーネントは、デフォルトで使用できません。コンポーネントをAEMサイドキックで使用可能なコンポーネントのリストに表示するには、次の手順を実行します。

1. Webサイトの作成者インスタンスにログインし、AEM Sitesページを開きます。

1. 静的テンプレートを使用するページに対して、次の手順を実行します。

   1. ページヘッダーで、![canvas-drop-down](assets/canvas-drop-down.png) > **Design**&#x200B;をタップし、デザインモードでページを開きます。
   1. 任意の（青い境界線の付いた）コンポーネントをタップし、![field-level](assets/field-level.png)をタップして、現在のコンポーネントを含む段落システムを選択します。
   1. 段落システムで![settings_icon](assets/settings_icon.png)をタップし、段落システムの編集ダイアログを開きます。
   1. 「**[!UICONTROL 許可されているコンポーネント]**」のリストから、**[!UICONTROL Document Services]** コンポーネントと **[!UICONTROL Document Services Predicates]** コンポーネントのチェックボックスをオンにします。「**[!UICONTROL OK]**」をタップします。

1. 動的テンプレートを使用するページに対して、次の手順を実行します。

   1. ページヘッダーで、![プロパティ](assets/properties.png)/**テンプレートを編集**&#x200B;をタップして、ページのテンプレートを開きます。
   1. **レイアウトコンテナ**&#x200B;をタップし、![FeedManagement](/help/forms/using/assets/feedmanagement.png)をタップします。 「**許可されているコンポーネント**」タブで、「**ドキュメントサービスとドキュメントサービスの述部**」オプションを有効にし、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。

>[!NOTE]
>
>また、コンポーネントを選択して、これらのカテゴリから特定のコンポーネントを有効にすることもできます。コンポーネントとその使用方法について詳しくは、「[フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)」と「[ページでのリンクコンポーネントの埋め込み](/help/forms/using/embedding-link-component-page.md)」を参照してください。

これで、コンポーネントブラウザーで Document Services コンポーネントカテゴリと Document Services Predicates コンポーネントカテゴリを使用できるようになります。コンポーネントは、同じテンプレートを使用するすべてのページで有効になります。

## 関連記事

* [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)
* [フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)
* [API を使用した Web ページ上のフォームの一覧表示](/help/forms/using/listing-forms-webpage-using-apis.md)
* [ドラフトと送信コンポーネントの使用](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信済みフォームのストレージのカスタマイズ](/help/forms/using/draft-submission-component.md)
* [ドラフトと送信コンポーネントとデータベースの統合のサンプル](/help/forms/using/integrate-draft-submission-database.md)
* [フォームポータルコンポーネントのテンプレートをカスタマイズする](/help/forms/using/customizing-templates-forms-portal-components.md)
* [ポータル上のフォーム発行の概要](/help/forms/using/introduction-publishing-forms.md)
