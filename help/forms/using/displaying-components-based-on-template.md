---
title: 使用するテンプレートに基づいたコンポーネントの表示
seo-title: 使用するテンプレートに基づいたコンポーネントの表示
description: フォームの作成時に、選択したテンプレートに基づいて、サイドバーのコンポーネントを有効にする方法について説明します。
seo-description: フォームの作成時に、選択したテンプレートに基づいて、サイドバーのコンポーネントを有効にする方法について説明します。
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 65%

---


# 使用するテンプレートに基づいたコンポーネントの表示{#displaying-components-based-on-the-template-used}

フォーム作成者は、[テンプレート](../../forms/using/template-editor.md)を使用してアダプティブフォームを作成する際、テンプレートポリシーに基づいて、特定のコンポーネントを表示して使用できます。テンプレートコンテンツポリシーを指定することにより、フォームの作成中にフォーム作成者に表示されるコンポーネントのグループを選択できます。

## テンプレートのコンテンツポリシーの変更  {#changing-the-content-policy-of-a-template}

テンプレートを作成すると、コンテンツリポジトリの`/conf`の下に作成されます。 `/conf`ディレクトリに作成したフォルダーに基づき、テンプレートのパスは次のとおりです。`/conf/<your-folder>/settings/wcm/templates/<your-template>`.

次の手順を実行して、テンプレートのコンテンツポリシーに基づいてサイドバーにコンポーネントを表示します。

1. CRXDE Lite を開きます。\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. CRXDE で、テンプレートを作成したフォルダーに移動します。

   例：`/conf/<your-folder>/`

1. CRXDEで、次の場所に移動します。`/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   コンポーネントのグループを選択するためには、新しいコンテンツポリシーが必要です。新しいポリシーを作成するには、デフォルトのポリシーをコピーして貼り付け、名前を変更します。

   デフォルトコンテンツポリシーのパス：`/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   `gridFluidLayout` フォルダーで、デフォルトのポリシーをコピーして貼り付け、名前を変更します。例： `myPolicy`

   ![デフォルトのポリシーをコピー](assets/crx-default1.png)

1. 作成する新しいポリシーを選択し、右側のパネルでタイプ`string[]`の&#x200B;**components**&#x200B;プロパティを選択します。

   components プロパティを選択して開くと、components を編集ダイアログが表示されます。components を編集ダイアログでは、「**+**」および「**-**」ボタンを使用して、コンポーネントグループを追加または削除できます。作成者が使用するコンポーネントを含むコンポーネントグループを追加できます。

   ![ポリシーのコンポーネントを追加または削除](assets/add-components-list1.png)

   コンポーネントグループを追加した後、「**OK**」をクリックしてリストを更新し、CRXDEアドレスバーの上にある「**すべて保存**」をクリックして更新します。

1. テンプレートで、コンテンツポリシーをデフォルトから、作成した新しいポリシーに変更します。（この例では`myPolicy`）

   ポリシーを変更するには、CRXDEで`/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`に移動します。

   `cq:policy`プロパティで、`default`を新しいポリシー名(`myPolicy`)に変更します。

   ![更新されたテンプレートコンテンツポリシー](assets/updated-policy.png)

   テンプレートを使用して作成したフォームを使用すると、追加したコンポーネントがサイドバーに表示されます。

