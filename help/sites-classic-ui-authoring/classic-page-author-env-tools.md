---
title: オーサリング - 環境とツール
description: Web サイトコンソールを使用すると、Web サイトを管理し、移動できます。 2 つのパネルを使用して、Web サイトの構造を展開し、必要な要素に対して実行するアクションを設定できます。
uuid: 0a9ce725-042a-4697-81fe-ac86cbab0398
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 67625e62-7035-4eb5-8dd5-6840d775a547
docset: aem65
exl-id: 5d7b6b2e-d1d8-4efe-b9ff-c9542b4e67d7
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 45%

---

# オーサリング - 環境とツール  {#authoring-the-environment-and-tools}

AEM のオーサリング環境は、コンテンツを編成および編集するための様々なメカニズムを提供しています. 提供されるツールには、様々なコンソールおよびページエディターからアクセスします。

## サイト管理 {#site-administration}

この **Web サイト** コンソールを使用すると、Web サイトを管理および移動できます。 2 つのパネルを使用して、Web サイトの構造を展開し、必要な要素に対して実行するアクションを指定できます。

![chlimage_1-108](assets/chlimage_1-108.png)

## ページコンテンツの編集 {#editing-your-page-content}

クラシック UI には、コンテンツファインダーとサイドキックを利用する個別のページエディターがあります。

`https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

![chlimage_1-109](assets/chlimage_1-109.png)

## ヘルプへのアクセス {#accessing-help}

各種 **ヘルプ** リソースには、AEM内から直接アクセスできます。

アクセス [コンソールツールバーからのヘルプ](/help/sites-classic-ui-authoring/author-env-basic-handling.md#accessing-help)を使用すると、サイドキックからヘルプにアクセスすることもできます ( アイコン ) を使用して、以下の操作を実行できます。

![](do-not-localize/sidekick-collapsed-2.png)

または、 **ヘルプ** 特定のコンポーネントの編集ダイアログのボタンコンテキスト依存のヘルプが表示されます。

## サイドキック {#sidekick}

この **コンポーネント** サイドキックの「 」タブでは、現在のページに追加できるコンポーネントを参照できます。 必要なグループを展開し、コンポーネントをページ上の必要な場所にドラッグできます。

![chlimage_1-110](assets/chlimage_1-110.png)

## コンテンツファインダー {#the-content-finder}

コンテンツファインダーを使用すると、ページ編集時にリポジトリ内のアセットやコンテンツをすばやく簡単に見つけることができます。

コンテンツファインダーを使用して、様々なリソースを検索できます。 必要に応じて、項目をドラッグしてページ上の段落にドロップできます。

* [画像](#finding-images)
* [ドキュメント](#finding-documents)
* [ムービー](#finding-movies)
* [Dynamic Media ブラウザー](/help/sites-administering/scene7.md#scene7contentbrowser)
* [ページ](#finding-pages)

* [段落](#referencing-paragraphs-from-other-pages)
* [製品](#products)
* または、[リポジトリ構造から web サイトを参照](#the-content-finder)できます

すべてのオプションを使用して、次の操作を実行できます。 [特定の項目を検索](#the-content-finder).

### 画像の検索 {#finding-images}

このタブには、リポジトリ内の画像が一覧表示されます。

ページ上に画像段落を作成した後、項目をドラッグして段落にドロップできます。

![chlimage_1-111](assets/chlimage_1-111.png)

### ドキュメントの検索 {#finding-documents}

このタブには、リポジトリ内のドキュメントが一覧表示されます。

ページ上にダウンロード段落を作成したら、項目をドラッグして段落にドロップできます。

![chlimage_1-112](assets/chlimage_1-112.png)

### 映画の検索 {#finding-movies}

このタブには、リポジトリ内のムービー (Flash項目など ) が一覧表示されます。

ページ上に適切な段落 (Flashなど ) を作成したら、項目をドラッグして段落にドロップできます。

![chlimage_1-113](assets/chlimage_1-113.png)

### 製品 {#products}

このタブには、すべての製品が一覧表示されます。 ページ上に適切な段落（「製品」など）を作成したら、項目をドラッグして段落にドロップできます。

![chlimage_1-114](assets/chlimage_1-114.png)

### ページの検索 {#finding-pages}

このタブには、すべてのページが表示されます。任意のページをダブルクリックし、編集用に開きます。

![chlimage_1-115](assets/chlimage_1-115.png)

### 他のページから段落を参照する {#referencing-paragraphs-from-other-pages}

このタブでは、別のページを検索できます。 そのページのすべての段落がリスト表示されます。 段落を現在のページにドラッグすると、元の段落への参照が作成されます。

![chlimage_1-116](assets/chlimage_1-116.png)

### フルリポジトリ表示の使用 {#using-the-full-repository-view}

このタブには、リポジトリ内のすべてのリソースが表示されます。

![chlimage_1-117](assets/chlimage_1-117.png)

### コンテンツブラウザーでの検索の使用 {#using-search-with-the-content-browser}

すべてのオプションで、特定の項目を検索できます。 検索パターンに一致するタグとリソースが一覧表示されます。

![screen_shot_2012-02-08at100746am](assets/screen_shot_2012-02-08at100746am.png)

検索にワイルドカードを使用することもできます。 次のワイルドカードがサポートされます。

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

AEMを使用すると、現在作業中のページにリンクされているページを表示できます。

直接ページ参照を表示するには：

1. サイドキックで、 **ページ** タブアイコン

   ![screen_shot_2012-02-16at83127pm](assets/screen_shot_2012-02-16at83127pm.png)

1. AEM で「**参照を表示**」を選択すると、参照ウィンドウが開き、選択したページを参照するページとそのパスが表示されます。

   ![screen_shot_2012-02-16at83311pm](assets/screen_shot_2012-02-16at83311pm.png)

状況によっては、サイドキックから次のようなアクションを追加で実行できます。

* [ローンチ](/help/sites-classic-ui-authoring/classic-launches.md)
* [ライブコピー](/help/sites-administering/msm.md)

* [ブループリント](/help/sites-administering/msm-best-practices.md)

その他 [ページ間の関係は、Web サイトコンソールで確認できます。](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console).

## 監査ログ {#audit-log}

**監査ログ**&#x200B;には、サイドキックの「**情報**」タブからアクセスできます。ここには、現在のページで実行された最近のアクションが一覧表示されます。次に例を示します。

![chlimage_1-118](assets/chlimage_1-118.png)

## ページ情報 {#page-information}

Web サイトコンソールには、[ページの現在のステータスに関する情報も表示されます](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console)（公開、変更、ロック、ライブコピーなど）。

## ページモード {#page-modes}

クラシック UI でページを編集中に、サイドキックの下部のアイコンを使用して次のモードにアクセスできます。

![](do-not-localize/chlimage_1-12.png)

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
