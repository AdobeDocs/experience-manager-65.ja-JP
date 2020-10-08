---
title: 初期サンドボックスアプリケーション
seo-title: 初期サンドボックスアプリケーション
description: テンプレート、コンポーネントおよびスクリプトの作成
seo-description: テンプレート、コンポーネントおよびスクリプトの作成
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 53%

---


# 初期サンドボックスアプリケーション {#initial-sandbox-application}

ここでは、次のものを作成します。

* サンプル Web サイトのコンテンツページを作成する際に使用する&#x200B;**[テンプレート.](#createthepagetemplate)**
* Web サイトのページをレンダリングする際に使用する&#x200B;**[コンポーネントとスクリプト.](#create-the-template-s-rendering-component)**

## コンテンツテンプレートの作成 {#create-the-content-template}

テンプレートは、新しいページのデフォルトのコンテンツを定義するものです。複雑な Web サイトでは、複数のテンプレートを使用して、サイト内の様々なタイプのページを作成する場合があります。さらに、変更内容をサーバークラスターにロールアウトする際のブループリントとして一連のテンプレートを使用する場合もあります。

この演習では、すべてのページを 1 つの単純なテンプレートに基づいて作成します。

1. CRXDE Lite のエクスプローラーペインで、次の手順を実行します。：

   *  `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 作成]** /テンプレート **[!UICONTROL を作成]**

1. テンプレートを作成ダイアログで、次の値を入力し、「**[!UICONTROL 次へ]**」をクリックします。

   * ラベル: `playpage`
   * タイトル: `An SCF Sandbox Play Template`
   * 説明: `An SCF Sandbox template for play pages`
   * リソースタイプ: `an-scf-sandbox/components/playpage`
   * ランキング：&lt;デフォルトのまま>

   「ラベル」は、ノード名に使用されます。

   「リソースタイプ」は、`playpage` の jcr:content ノードにプロパティ `sling:resourceType` として表示されます。ブラウザーから要求されたときにコンテンツをレンダリングするコンポーネント（リソース）を識別します。

   In this case, all pages created using the `playpage` template are rendered by the `an-scf-sandbox/components/playpage` component. By convention, the path to the component is relative, allowing Sling to search for the resource first in the `/apps` folder and, if not found, in the `/libs` folder.

   ![create-content-template](assets/create-content-template-1.png)

1. コピー／貼り付けを使用する場合は、「リソースタイプ」の値の先頭や末尾にスペースがないことを確認します。

   「**[!UICONTROL 次へ]**」をクリックします。

1. 「許可されているパス」は、**[!UICONTROL 新しいページ]**&#x200B;ダイアログにテンプレートが表示されるように、このテンプレートを使用するページのパスを参照します。

   To add a path, click the plus button `+` and type `/content(/.&ast;)?` in the text box that appears. コピー&amp;ペーストを使用する場合は、先頭または末尾に空白文字がないことを確認します。

   Note: The value of the allowed path property is a *regular expression*. この表現と一致するパスを持つコンテンツページでテンプレートを使用できます。In this case, the regular expression matches the path of the **/content** folder and all its subpages.

   When an author creates a page below `/content`, the `playpage` template titled &quot;An SCF Sandbox Page Template&quot; appears in a list of available templates to use.

   テンプレートからルートページを作成した後、通常の式にルートパスを含めるようにプロパティを変更することで、テンプレートへのアクセスをこのWebサイトに制限できます。

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   **[!UICONTROL 許可されている親]** パネルで「次へ **** 」をクリックします。

   Click **[!UICONTROL Next]** in the **[!UICONTROL Allowed Children]** panels.

   「**[!UICONTROL OK]**」をクリックします。

1. 「OK」をクリックし、テンプレートの作成を終了すると、新しい `playpage` テンプレートについて、「プロパティ」タブの値の隅に赤い三角形が表示されていることがわかります。これらの赤い三角形は、編集内容が保存されていないことを示します。

   Click **[!UICONTROL Save All]** to save the new template to the repository.

   ![verify-content-template](assets/verify-content-template.png)

### テンプレートのレンダリングコンポーネントの作成 {#create-the-template-s-rendering-component}

コンテンツを定義し、[playpage テンプレート](#createthepagetemplate)に基づいて作成されたページをレンダリングするコンポーネントを作成します。**

1. In CRXDE Lite, right-click **`/apps/an-scf-sandbox/components`** and click **[!UICONTROL Create > Component]**.
1. ノードの名前（ラベル）を *playpageに設定すると*、コンポーネントのパスは

   `/apps/an-scf-sandbox/components/playpage`

   これは、再生ページテンプレートの「リソースタイプ」に対応します(オプションで、パスの最初の **`/apps/`** 部分を除いた値)。

   **[!UICONTROL コンポーネントを作成]**&#x200B;ダイアログで、以下のプロパティ値を入力します。

   * ラベル：**playpage**
   * タイトル：**An SCF Sandbox Play Component**
   * 説明：**This is the component which renders content for An SCF Sandbox page.**
   * Super Type: *&lt;leave blank>*
   * Group: *&lt;leave blank>*

   ![create-template-component](assets/create-template-component.png)

1. Click **[!UICONTROL Next]** until the **[!UICONTROL Allowed Children]** panel of the dialog appears:

   * 「**[!UICONTROL OK]**」をクリックします。
   * 「**[!UICONTROL すべて保存]**」をクリックします。

1. コンポーネントのパスとテンプレートの resourceType が一致していることを確認します。

   >[!CAUTION]
   >
   >playpageコンポーネントへのパスとplaypageテンプレートのsling:resourceTypeプロパティとの対応は、Webサイトを正しく機能させるために重要です。

   ![verify-template-component](assets/verify-template-component.png)