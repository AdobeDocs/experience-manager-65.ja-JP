---
title: 初期サンドボックスアプリケーション
description: コンテンツページの作成に使用されるコンテンツテンプレートと、Web サイトページのレンダリングに使用されるコンポーネントおよびスクリプトの使用方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 14%

---

# 初期サンドボックスアプリケーション {#initial-sandbox-application}

この節では、次を作成します。

* The **[テンプレート](#createthepagetemplate)** を使用して、サンプル web サイト内にコンテンツページを作成します。
* The **[コンポーネントとスクリプト](#create-the-template-s-rendering-component)** Web サイトページのレンダリングに使用される。

## コンテンツテンプレートの作成 {#create-the-content-template}

テンプレートは、新しいページのデフォルトコンテンツを定義します。複雑な web サイトでは、サイト内の様々なタイプのページを作成するために、複数のテンプレートを使用する場合があります。また、一連のテンプレートは、サーバーのクラスターに対する変更をロールアウトするためのブループリントになる場合があります。

この演習では、すべてのページを 1 つのシンプルなテンプレートに基づいて作成します。

1. CRXDE Liteのエクスプローラペイン：

   * `/apps/an-scf-sandbox/templates` を選択します。
   * **[!UICONTROL 作成]** > **[!UICONTROL テンプレートを作成]**

1. テンプレートを作成ダイアログで、次の値を入力して「**[!UICONTROL 次へ]**」をクリックします。

   * ラベル：`playpage`
   * タイトル：`An SCF Sandbox Play Template`
   * 説明：`An SCF Sandbox template for play pages`
   * リソースタイプ： `an-scf-sandbox/components/playpage`
   * ランキング： &lt;leave as=&quot;&quot; default=&quot;&quot;>

   ラベルは、ノード名に使用されます。

   「リソースタイプ」が `playpage`&#39;s `jcr:content` ノードをプロパティとして `sling:resourceType`. ブラウザーから要求された場合に、コンテンツをレンダリングするコンポーネント（リソース）を識別します。

   この場合、 `playpage` テンプレートは、 `an-scf-sandbox/components/playpage` コンポーネント。 慣例により、コンポーネントのパスは相対パスなので、Sling は、 `/apps` フォルダーおよび（見つからない場合） `/libs` フォルダー。

   ![create-content-template](assets/create-content-template-1.png)

1. コピー/貼り付けを使用する場合は、「リソースタイプ」の値の先頭または末尾にスペースがないことを確認します。

   「**[!UICONTROL 次へ]**」をクリックします。

1. 「許可されたパス」は、このテンプレートを使用するページのパスを指し、そのテンプレートが **[!UICONTROL 新しいページ]** ダイアログ。

   パスを追加するには、プラスボタンをクリックします。 `+` と入力します。 `/content(/.&ast;)?` をクリックします。 コピー/貼り付けを使用する場合は、先頭または末尾にスペースがないことを確認します。

   注意：許可されるパスプロパティの値は、 *正規表現*. 式と一致するパスを持つコンテンツページは、このテンプレートを使用できます。 この場合、正規表現は **/content** フォルダーおよびそのすべてのサブページ。

   作成者が以下のページを作成したとき `/content`、 `playpage` 使用可能なテンプレートのリストに、「SCF サンドボックスページテンプレート」というタイトルのテンプレートが表示されます。

   テンプレートからルートページを作成した後は、プロパティを編集して正規表現にルートパスを含めることで、このテンプレートへのアクセスをこの Web サイトに制限できます。

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   クリック **[!UICONTROL 次へ]** （内） **[!UICONTROL 許可された親]** パネル。

   クリック **[!UICONTROL 次へ]** （内） **[!UICONTROL 許可されている子]** パネル。

   「**[!UICONTROL OK]**」をクリックします。

1. [OK] をクリックしてテンプレートの作成を終了した後、新しいの [ プロパティ ] タブの値の隅に赤い三角形が表示されることに注意してください。 `playpage` テンプレート。 これらの赤い三角形は、編集内容が保存されていないことを示します。

   クリック **[!UICONTROL すべて保存]** をクリックして、新しいテンプレートをリポジトリに保存します。

   ![verify-content-template](assets/verify-content-template.png)

### テンプレートのレンダリングコンポーネントの作成 {#create-the-template-s-rendering-component}

を作成します。 *コンポーネント* コンテンツを定義し、 [playpage テンプレート](#createthepagetemplate).

1. CRXDE Liteで右クリック **`/apps/an-scf-sandbox/components`** をクリックします。 **[!UICONTROL 作成/コンポーネント]**.
1. ノードの名前（ラベル）を *playpage*&#x200B;の場合、コンポーネントへのパスは

   `/apps/an-scf-sandbox/components/playpage`

   再生ページテンプレートのリソースタイプに対応する ( オプションで、最初の **`/apps/`** パスの一部 )。

   **[!UICONTROL コンポーネントを作成]**&#x200B;ダイアログで、以下のプロパティ値を入力します。

   * ラベル： **playpage**
   * タイトル： **SCF Sandbox Play コンポーネント**
   * 説明： **これは、SCF サンドボックスページのコンテンツをレンダリングするコンポーネントです。**
   * スーパータイプ： *&lt;leave blank=&quot;&quot;>*
   * グループ： *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. クリック **[!UICONTROL 次へ]** まで **[!UICONTROL 許可されている子]** ダイアログのパネルが表示されます。

   * 「**[!UICONTROL OK]**」をクリックします。
   * 「**[!UICONTROL すべて保存]**」をクリックします。

1. テンプレートのコンポーネントへのパスと resourceType が一致していることを確認します。

   >[!CAUTION]
   >
   >再生ページコンポーネントのパスと `sling:resourceType` 再生ページテンプレートのプロパティは、Web サイトが正しく機能するには非常に重要です。

   ![verify-template-component](assets/verify-template-component.png)
