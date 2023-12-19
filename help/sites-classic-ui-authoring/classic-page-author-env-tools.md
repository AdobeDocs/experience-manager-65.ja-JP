---
title: オーサリング - 環境とツール
description: Web サイトコンソールを使用すると、web サイトを管理したり、web サイト内を移動したりできます。2 つのパネルを使用して、web サイトの構造を展開し、必要な要素に対してアクションを実行できます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 5d7b6b2e-d1d8-4efe-b9ff-c9542b4e67d7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 96%

---

# オーサリング - 環境とツール {#authoring-the-environment-and-tools}

AEM のオーサリング環境は、コンテンツを編成および編集するための様々なメカニズムを提供しています. 提供されるツールには、様々なコンソールおよびページエディターからアクセスします。

## サイト管理 {#site-administration}

**Web サイト**&#x200B;コンソールを使用すると、web サイトを管理したり、web サイト内を移動したりできます。2 つのパネルを使用して、web サイトの構造を展開し、必要な要素に対してアクションを実行できます。

![chlimage_1-108](assets/chlimage_1-108.png)

## ページコンテンツの編集 {#editing-your-page-content}

クラシック UI には、コンテンツファインダーとサイドキックを利用する個別のページエディターがあります。

`https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

![chlimage_1-109](assets/chlimage_1-109.png)

## ヘルプへのアクセス {#accessing-help}

様々な&#x200B;**ヘルプ**&#x200B;リソースには、AEM 内から直接アクセスできます。

[コンソールツールバーからのヘルプ](/help/sites-classic-ui-authoring/author-env-basic-handling.md#accessing-help)をアクセスすると、ページ編集時にサイドキックからヘルプに（？アイコンを使用して）アクセスできます。

![折りたたまれた Sidekick](do-not-localize/sidekick-collapsed-2.png)

または、特定のコンポーネントの編集ダイアログで「**ヘルプ**」ボタンを使用することで、コンテキスト依存のヘルプが表示されます。

## サイドキック {#sidekick}

サイドキックの「**コンポーネント**」タブでは、現在のページに追加できるコンポーネントを参照できます。必要なグループを展開し、コンポーネントをページ上の必要な場所にドラッグできます。

![chlimage_1-110](assets/chlimage_1-110.png)

## コンテンツファインダー {#the-content-finder}

コンテンツファインダーは、ページ編集時にリポジトリ内のアセットやコンテンツを素早く簡単に見つけることができます。

コンテンツファインダーを使用して、幅広いリソースを検索できます。必要に応じて、項目をページ上の段落にドラッグ＆ドロップできます。

* [画像](#finding-images)
* [ドキュメント](#finding-documents)
* [ムービー](#finding-movies)
* [Dynamic Media ブラウザー](/help/sites-administering/scene7.md#scene7contentbrowser)
* [ページ](#finding-pages)

* [段落](#referencing-paragraphs-from-other-pages)
* [製品](#products)
* または、[リポジトリ構造から web サイトを参照](#the-content-finder)できます

すべてのオプションを使用して、[特定の項目を検索](#the-content-finder)できます。

### 画像の検索 {#finding-images}

このタブには、リポジトリ内の画像が一覧表示されます。

ページ上に画像段落を作成した後、項目を段落にドラッグ＆ドロップできます。

![chlimage_1-111](assets/chlimage_1-111.png)

### ドキュメントの検索 {#finding-documents}

このタブには、リポジトリ内のドキュメントが一覧表示されます。

ページ上にダウンロード段落を作成したら、項目を段落にドラッグ＆ドロップできます。

![chlimage_1-112](assets/chlimage_1-112.png)

### ムービーの検索 {#finding-movies}

このタブには、リポジトリ内のムービー（Flash アイテムなど）が一覧表示されます。

ページ上に適切な段落（Flashなど）を作成したら、項目を段落にドラッグ＆ドロップできます。

![chlimage_1-113](assets/chlimage_1-113.png)

### 製品 {#products}

このタブには、製品が一覧表示されます。ページ上に適切な段落（製品など）を作成したら、その段落に項目をドラッグ＆ドロップできます。

![chlimage_1-114](assets/chlimage_1-114.png)

### ページの検索 {#finding-pages}

このタブには、すべてのページが表示されます。任意のページをダブルクリックし、編集用に開きます。

![chlimage_1-115](assets/chlimage_1-115.png)

### 他のページからの段落の参照 {#referencing-paragraphs-from-other-pages}

このタブを使用すると、他のページを検索できます。そのページのすべての段落が一覧表示されます。段落を現在のページにドラッグすると、元の段落への参照が作成されます。

![chlimage_1-116](assets/chlimage_1-116.png)

### リポジトリの一覧表示の使用 {#using-the-full-repository-view}

このタブには、リポジトリ内のすべてのリソースが表示されます。

![chlimage_1-117](assets/chlimage_1-117.png)

### コンテンツブラウザーでの検索の使用 {#using-search-with-the-content-browser}

すべてのオプションについて、特定の項目を検索できます。検索パターンに一致するタグとリソースが一覧表示されます。

![screen_shot_2012-02-08at100746am](assets/screen_shot_2012-02-08at100746am.png)

検索にワイルドカードを使用することもできます。サポートされているワイルドカードは、次のとおりです。

* `*`
0 個以上の連続した文字に一致します。

* `?`
1 個の文字に一致します。

>[!NOTE]
>
>ワイルドカード検索を実行するには、擬似プロパティの「name」を使用する必要があります。

例えば、次の名前でアクセス可能な画像があるとします。

`ad-nmvtis.jpg`

以下の検索パターンで、この画像（およびこのパターンに一致するそれ以外の画像）が見つかります。

* `name:*nmv*`
* `name:AD*`
文字の一致では、大文字と小文字は区別され*ません*。

* `name:ad?nm??is.*`
1 つのクエリ内で任意の数のワイルドカードを使用できます。

>[!NOTE]
>
>[SQL2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/commons/query/sql2/package-summary.html) 検索を使用することもできます。

## 参照の表示 {#showing-references}

AEM を使用すると、現在作業中のページにリンクされているページを表示できます。

直接ページ参照を表示するには：

1. サイドキックで、「**ページ**」タブアイコンを選択します。

   ![screen_shot_2012-02-16at83127pm](assets/screen_shot_2012-02-16at83127pm.png)

1. AEM で「**参照を表示**」を選択すると、参照ウィンドウが開き、選択したページを参照するページとそのパスが表示されます。

   ![screen_shot_2012-02-16at83311pm](assets/screen_shot_2012-02-16at83311pm.png)

状況によっては、サイドキックから次のようなアクションを追加で実行できます。

* [ローンチ](/help/sites-classic-ui-authoring/classic-launches.md)
* [ライブコピー](/help/sites-administering/msm.md)

* [ブループリント](/help/sites-administering/msm-best-practices.md)

その他の[ページ間の関係は、web サイトコンソールで確認できます](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)。

## 監査ログ {#audit-log}

**監査ログ**&#x200B;には、サイドキックの「**情報**」タブからアクセスできます。ここには、現在のページで実行された最近のアクションが一覧表示されます。次に例を示します。

![chlimage_1-118](assets/chlimage_1-118.png)

## ページ情報 {#page-information}

Web サイトコンソールも [ページの現在のステータスに関する情報を提供します](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) パブリッシュ、変更、ロック、ライブコピーなど。

## ページモード {#page-modes}

クラシック UI でページを編集中に、サイドキックの下部のアイコンを使用して次のモードにアクセスできます。

![ページモード](do-not-localize/chlimage_1-12.png)

サイドキックの下部に並ぶ 1 行のアイコンは、ページを操作するモードの切り替えに使用します。

* [編集](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)
デフォルトのモードであり、ページの編集、コンポーネントの追加または削除、およびそれ以外の変更を行うことができます。

* [プレビュー](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#previewing-pages)
このモードを使用すると、ページが web サイトで最終的にどのように表示されるかをプレビューできます。

* [デザイン](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md#main-pars-procedure-0)
このモードでは、アクセス可能なコンポーネントを設定して、ページのデザインを編集できます。

>[!NOTE]
>
>それ以外に次のオプションも利用できます。
>
>* [基礎モード](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md)
>* [ClientContext](/help/sites-administering/client-context.md)
>* Web サイト — Web サイトコンソールを開きます。
>* 再読み込み - ページを更新します。

## キーボードショートカット {#keyboard-shortcuts}

様々な[キーボードショートカット](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)を利用できます。
