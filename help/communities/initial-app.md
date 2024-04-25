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

* この **[template](#createthepagetemplate)** これは、サンプル web サイトのコンテンツページの作成に使用されます。
* この **[コンポーネントとスクリプト](#create-the-template-s-rendering-component)** これは、web サイトページのレンダリングに使用されます。

## コンテンツテンプレートの作成 {#create-the-content-template}

テンプレートは、新しいページのデフォルトコンテンツを定義します。複雑な web サイトでは、サイト内の様々なタイプのページを作成するために、複数のテンプレートを使用する場合があります。さらに、一連のテンプレートは、サーバーのクラスターに対する変更のロールアウトに使用されるブループリントになる場合があります。

この演習では、すべてのページを 1 つのシンプルなテンプレートに基づいて作成します。

1. CRXDE Liteのエクスプローラーパネルで、次の操作を行います。

   * `/apps/an-scf-sandbox/templates` を選択します。
   * **[!UICONTROL 作成]** > **[!UICONTROL テンプレートを作成]**

1. テンプレートを作成ダイアログで、次の値を入力して「**[!UICONTROL 次へ]**」をクリックします。

   * ラベル：`playpage`
   * タイトル：`An SCF Sandbox Play Template`
   * 説明：`An SCF Sandbox template for play pages`
   * リソースタイプ： `an-scf-sandbox/components/playpage`
   * ランキング : &lt;leave as=&quot;&quot; default=&quot;&quot;>

   ラベルはノード名に使用されます。

   リソースタイプがに表示されます。 `playpage`の `jcr:content` プロパティとしてのノード `sling:resourceType`. ブラウザーから要求されたときに、コンテンツをレンダリングするコンポーネント（リソース）を識別します。

   この場合、を使用して作成されたすべてのページ `playpage` テンプレートは、 `an-scf-sandbox/components/playpage` コンポーネント。 慣例により、コンポーネントへのパスは相対パスとなり、Sling は最初にでリソースを検索できます。 `/apps` フォルダーが見つからない場合は、フォルダー内の `/libs` フォルダー。

   ![create-content-template](assets/create-content-template-1.png)

1. コピー/貼り付けを使用する場合は、「リソースタイプ」の値の先頭または末尾にスペースが含まれていないことを確認します。

   「**[!UICONTROL 次へ]**」をクリックします。

1. 「許可されているパス」とは、このテンプレートを使用するページのパスを指し、このテンプレートは **[!UICONTROL 新しいページ]** ダイアログ。

   パスを追加するには、「+」ボタンをクリックします `+` およびタイプ `/content(/.&ast;)?` 表示されるテキストボックス内。 コピー/貼り付けを使用する場合は、先頭または末尾にスペースがないことを確認します。

   メモ：許可されているパスプロパティの値は *正規表現*. 式に一致するパスを持つコンテンツページは、テンプレートを使用できます。 この場合、正規表現はのパスと一致します **/content** フォルダーとそのすべてのサブページ。

   作成者が以下にページを作成した場合 `/content`, `playpage` 使用可能なテンプレートのリストに、「SCF サンドボックスページテンプレート」というタイトルのテンプレートが表示されます。

   テンプレートからルートページを作成した後に、プロパティを編集して正規表現にルートパスを含めると、テンプレートへのアクセスをこの web サイトに制限できます。

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   クリック **[!UICONTROL 次]** が含まれる **[!UICONTROL 許可された親]** パネル。

   クリック **[!UICONTROL 次]** が含まれる **[!UICONTROL 許可された子]** パネル。

   「**[!UICONTROL OK]**」をクリックします。

1. [OK] をクリックしてテンプレートの作成が完了したら、新しいの [ プロパティ ] タブの値の隅に表示される赤い三角形に注目してください `playpage` テンプレート。 これらの赤い三角形は、保存されていない編集を示します。

   クリック **[!UICONTROL すべて保存]** をクリックして、新しいテンプレートをリポジトリに保存します。

   ![verify-content-template](assets/verify-content-template.png)

### テンプレートのレンダリングコンポーネントの作成 {#create-the-template-s-rendering-component}

を作成 *component* コンテンツを定義し、に基づいて作成されたページをレンダリングします。 [再生ページテンプレート](#createthepagetemplate).

1. CRXDE Liteーで、右クリックします **`/apps/an-scf-sandbox/components`** をクリックして、 **[!UICONTROL 作成/ コンポーネント]**.
1. ノードの名前（ラベル）をに設定する *playpage*、コンポーネントへのパスはです。

   `/apps/an-scf-sandbox/components/playpage`

   これは、再生ページテンプレートのリソースタイプ （オプションでイニシャルを除く）に対応します **`/apps/`** パスの一部）。

   **[!UICONTROL コンポーネントを作成]**&#x200B;ダイアログで、以下のプロパティ値を入力します。

   * ラベル： **playpage**
   * タイトル： **SCF サンドボックス再生コンポーネント**
   * 説明： **これは、SCF サンドボックスページのコンテンツをレンダリングするコンポーネントです。**
   * スーパータイプ： *&lt;leave blank=&quot;&quot;>*
   * グループ： *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. クリック **[!UICONTROL 次]** まで **[!UICONTROL 許可された子]** ダイアログのパネルが表示されます。

   * 「**[!UICONTROL OK]**」をクリックします。
   * 「**[!UICONTROL すべて保存]**」をクリックします。

1. コンポーネントへのパスとテンプレートの resourceType が一致することを確認します。

   >[!CAUTION]
   >
   >再生ページコンポーネントへのパスと `sling:resourceType` playpage テンプレートのプロパティは、web サイトが正しく機能するためにはきわめて重要です。

   ![verify-template-component](assets/verify-template-component.png)
