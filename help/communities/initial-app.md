---
title: 初期サンドボックスアプリケーション
description: コンテンツページの作成に使用するコンテンツテンプレートと、web サイトページのレンダリングに使用するコンポーネントおよびスクリプトの使用方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 14%

---

# 初期サンドボックスアプリケーション {#initial-sandbox-application}

この節では、次を作成します。

* サンプル web サイトのコンテンツページの作成に使用される **[テンプレート](#createthepagetemplate)**。
* Web サイトのページのレンダリングに使用する **[コンポーネントとスクリプト](#create-the-template-s-rendering-component)**。

## コンテンツテンプレートの作成 {#create-the-content-template}

テンプレートは、新しいページのデフォルトコンテンツを定義します。複雑な web サイトでは、サイト内の様々なタイプのページを作成するために、複数のテンプレートを使用する場合があります。さらに、一連のテンプレートは、サーバーのクラスターに対する変更のロールアウトに使用されるブループリントになる場合があります。

この演習では、すべてのページを 1 つのシンプルなテンプレートに基づいて作成します。

1. CRXDE Liteのエクスプローラーパネルで、次の操作を行います。

   * `/apps/an-scf-sandbox/templates` を選択します。
   * **[!UICONTROL 作成]**/**[!UICONTROL テンプレートを作成]**

1. テンプレートを作成ダイアログで、次の値を入力して「**[!UICONTROL 次へ]**」をクリックします。

   * ラベル：`playpage`
   * タイトル：`An SCF Sandbox Play Template`
   * 説明：`An SCF Sandbox template for play pages`
   * リソースの種類：`an-scf-sandbox/components/playpage`
   * ランキング：&lt; デフォルトのままにする >

   ラベルはノード名に使用されます。

   リソースタイプは、`playpage` の `jcr:content` ノードにプロパティ `sling:resourceType` として表示されます。 ブラウザーから要求されたときに、コンテンツをレンダリングするコンポーネント（リソース）を識別します。

   この場合、`playpage` テンプレートを使用して作成されたページはすべて `an-scf-sandbox/components/playpage` コンポーネントによってレンダリングされます。 慣例により、コンポーネントへのパスは相対パスとなり、Sling は最初に `/apps` フォルダーでリソースを検索し、見つからない場合は `/libs` フォルダーでリソースを検索できます。

   ![create-content-template](assets/create-content-template-1.png)

1. コピー/貼り付けを使用する場合は、「リソースタイプ」の値の先頭または末尾にスペースが含まれていないことを確認します。

   「**[!UICONTROL 次へ]**」をクリックします。

1. 「許可されるパス」とは、このテンプレートを使用するページのパスを指し、例えば、このテンプレートは **[!UICONTROL 新規ページ]** ダイアログに表示されます。

   パスを追加するには、`+` のプラスボタンをクリックし、表示されるテキストボックスに `/content(/.&ast;)?` と入力します。 コピー/貼り付けを使用する場合は、先頭または末尾にスペースがないことを確認します。

   メモ：許可されているパスプロパティの値は *正規表現* です。 式に一致するパスを持つコンテンツページは、テンプレートを使用できます。 この場合、正規表現は、**/content** フォルダーとそのすべてのサブページのパスに一致します。

   作成者が `/content` の下にページを作成すると、使用可能なテンプレートのリストに「SCF サンドボックスページテンプレート」というタイトルの `playpage` テンプレートが表示されます。

   テンプレートからルートページを作成した後に、プロパティを編集して正規表現にルートパスを含めると、テンプレートへのアクセスをこの web サイトに制限できます。

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   **[!UICONTROL 許可された親]** パネルの **[!UICONTROL 次へ]** をクリックします。

   **[!UICONTROL 許可された子]** パネルの **[!UICONTROL 次へ]** をクリックします。

   「**[!UICONTROL OK]**」をクリックします。

1. [OK] をクリックしてテンプレートの作成が完了したら、新しい `playpage` テンプレートの [ プロパティ ] タブの値の隅に表示される赤い三角形に注目してください。 これらの赤い三角形は、保存されていない編集を示します。

   **[!UICONTROL すべて保存]** をクリックして、新しいテンプレートをリポジトリに保存します。

   ![verify-content-template](assets/verify-content-template.png)

### テンプレートのレンダリングコンポーネントの作成 {#create-the-template-s-rendering-component}

コンテンツを定義し、*playpage テンプレート* に基づいて作成されたすべてのページをレンダリングする [ コンポーネント ](#createthepagetemplate) を作成します。

1. CRXDE Liteで、**`/apps/an-scf-sandbox/components`** を右クリックして、**[!UICONTROL 作成/コンポーネント]** をクリックします。
1. ノードの名前（ラベル）を *playpage* に設定すると、コンポーネントへのパスはになります。

   `/apps/an-scf-sandbox/components/playpage`

   これは、再生ページテンプレートのリソースタイプ（オプションでパスの最初の **`/apps/`** 部分を除く）に対応します。

   **[!UICONTROL コンポーネントを作成]**&#x200B;ダイアログで、以下のプロパティ値を入力します。

   * ラベル：**playpage**
   * タイトル：**SCF サンドボックス再生コンポーネント**
   * 説明：**これは、SCF サンドボックスページのコンテンツをレンダリングするコンポーネントです。**
   * スーパータイプ：*&lt;leave blank>*
   * グループ：*&lt;leave blank>*

   ![create-template-component](assets/create-template-component.png)

1. **[!UICONTROL 次へ]** をクリックして、ダイアログの **[!UICONTROL 許可されている子]** パネルを表示します。

   * 「**[!UICONTROL OK]**」をクリックします。
   * 「**[!UICONTROL すべて保存]**」をクリックします。

1. コンポーネントへのパスとテンプレートの resourceType が一致することを確認します。

   >[!CAUTION]
   >
   >Web サイトを正しく機能させるには、再生ページコンポーネントへのパスと再生ページテンプレートの `sling:resourceType` プロパティとの対応が重要です。

   ![verify-template-component](assets/verify-template-component.png)
