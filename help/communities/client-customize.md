---
title: クライアント側のカスタマイズ
description: AEM Communitiesのクライアントサイドの動作または外観のカスタマイズ
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# クライアント側のカスタマイズ  {#client-side-customization}

| **[⇐機能の基本事項](essentials.md)** | **[サーバーサイドのカスタマイズ ⇒](server-customize.md)** |
|---|---|
|   | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

クライアントサイドでのAEM Communities コンポーネントの外観や動作をカスタマイズする方法はいくつかあります。

コンポーネントをオーバーレイまたは拡張する方法は、主に 2 つあります。

[ オーバーレイ ](#overlays) コンポーネントはデフォルトのコンポーネントを変更し、コンポーネントへのすべての参照に影響します。

[ 拡張 ](#extensions) コンポーネントは一意の名前を持ち、変更の範囲を制限します。 「extend」という用語は、「override」と同じ意味で使用されます。

## オーバーレイ {#overlays}

コンポーネントのオーバーレイとは、デフォルトコンポーネントに変更を加えて、デフォルトを使用するすべてのインスタンスに影響を与える方法です。

オーバーレイを実行するには、/**libs** ディレクトリ内の元のコンポーネントを変更するのではなく、/**apps** ディレクトリ内のデフォルトコンポーネントのコピーを変更します。 コンポーネントは、「libs」が「apps」に置き換えられることを除いて、同一の相対パスで構築されます。

リクエストを解決するために最初に検索されるのは/apps ディレクトリです。見つからない場合は、/libs ディレクトリ内のデフォルトバージョンが使用されます。

今後のパッチおよびアップグレードでは、公開インターフェイスを維持しながら必要な方法で/libs ディレクトリを自由に変更できるので、/libs ディレクトリのデフォルトのコンポーネントは決して変更しないでください。

これは、特定の用途に合わせて変更を加え、コンポーネントへの一意のパスを作成し、/libs ディレクトリ内の元のデフォルトコンポーネントをスーパーリソースタイプとして参照することに依存するデフォルトコンポーネント [ 拡張 ](#extensions) とは異なります。

コメントコンポーネントのオーバーレイの簡単な例については、[ コメントコンポーネントのオーバーレイチュートリアル ](overlay-comments.md) を参照してください。

## 拡張子 {#extensions}

コンポーネントの拡張（上書き）は、デフォルトを使用するすべてのインスタンスに影響を与えずに、特定の用途に合わせて変更を加える方法です。 拡張コンポーネントは、/apps フォルダーで一意の名前を付けられ、/libs フォルダーのデフォルトコンポーネントを参照するので、コンポーネントのデフォルトのデザインと動作は変更されません。

これは、Sling の特性が libs/ フォルダーで検索する前にアプリ/フォルダーへの相対参照を解決するデフォルトのコンポーネント [ オーバーレイ ](#overlays) とは異なります。そのため、コンポーネントのデザインや動作はグローバルに変更されます。

コメントコンポーネントの拡張例については、[ コメントコンポーネントの拡張チュートリアル ](extend-comments.md) を参照してください。

## JavaScript バインディング {#javascript-binding}

コンポーネントの HBS スクリプトは、この機能を実装するJavaScript オブジェクト、モデル、ビューにバインドする必要があります。

`data-scf-component` 属性の値は、**`social/tally/components/hbs/rating`** などのデフォルトの場合もあれば、カスタマイズされた機能の拡張（カスタマイズ）コンポーネントである場合もあります（**weretail/components/hbs/rating**。

コンポーネントをバインドするには、コンポーネントスクリプト全体を次の属性で &lt;div> 要素内に囲む必要があります。

* `data-component-id`=&quot;`{{id}}`&quot;

  コンテキストから「id」プロパティに解決されます

* `data-scf-component`=&quot;*&lt;resourceType>*

例：`/apps/weretail/components/hbs/rating/rating.hbs` から

```xml
<div class="we-Rating" data-component-id="`{{id}}`" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## カスタムプロパティ {#custom-properties}

コンポーネントを拡張またはオーバーレイするときに、変更したダイアログにプロパティを追加することができます。

コンポーネントやリソースに設定されたすべてのプロパティには、handlebars テンプレートのプロパティキーを参照することでアクセスできます。

`{{properties.<property_name>}}`

## CSS のスキニング {#skinning-css}

Web サイトの全体的なテーマに合わせてコンポーネントをカスタマイズするには、「スキニング」を行います。カラー、フォント、画像、ボタン、リンク、間隔を変更し、ある程度配置することもできます。

スキニングを行うには、フレームワークスタイルを選択的に上書きするか、まったく新しいスタイルシートを記述します。 SCF コンポーネントは、コンポーネントを構成する様々な要素に影響を与える、名前空間、モジュール型、セマンティックの CSS クラスを定義します。

コンポーネントをスキニングするには：

1. 変更する要素（コンポーザー領域、ツールバーボタン、メッセージフォントなど）を特定します。
1. これらの要素に影響を与える CSS クラス/ルールを特定します。
1. スタイルシートファイル（.css）を作成します。
1. スタイルシートをサイトのクライアントライブラリフォルダー（[clientlibs](#clientlibs-for-scf)）に含め、[ui:includeClientLib](../../help/sites-developing/clientlibs.md) でテンプレートとページから含まれていることを確認します。

1. スタイルシートで識別（#2）した CSS クラスおよびルールを再定義し、スタイルを追加します。

これで、カスタムスタイルがデフォルトのフレームワークスタイルを上書きし、コンポーネントが新しいスキンでレンダリングされます。

>[!CAUTION]
>
>プレフィックスが `scf-js` の CSS クラス名は、JavaScript コードで固有の用途を持ちます。 これらのクラスは、コンポーネントの状態に影響します（非表示から表示への切り替えなど）。オーバーライドも削除もしないでください。
>
>`scf-js` クラスはスタイルに影響を与えませんが、クラス名はスタイルシートで使用される場合があります。ただし、クラス名は要素の状態を制御するため、副作用が生じる可能性があります。

## JavaScriptの拡張 {#extending-javascript}

コンポーネントのJavaScript実装を拡張するには、次の操作が必要です。

1. jcr:resourceSuperType を拡張されたコンポーネントの jcr:resourceType の値に設定して（例：social/forum/components/hbs/forum）、アプリのコンポーネントを作成します。
1. デフォルトの SCF コンポーネントのJavaScriptを調べて、SCF.registerComponent （）を使用して登録する必要があるメソッドを判断します。
1. 拡張コンポーネントのJavaScriptをコピーするか、最初から開始します。
1. メソッドを拡張します。
1. SCF.registerComponent （）を使用して、すべてのメソッドをデフォルトまたはカスタマイズしたオブジェクトとビューで登録します。

### forum.js:Forum のサンプル拡張機能 – HBS  {#forum-js-sample-extension-of-forum-hbs}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";
    var GMForumView = SCF.ForumView.extend({
        viewName: "GMForum",
        showComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        },
        hideComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        }
    });

    SCF.registerComponent('social/forum/components/hbs/post', SCF.Post, SCF.PostView);
    SCF.registerComponent('social/forum/components/hbs/topic', SCF.Topic, SCF.TopicView);
    SCF.registerComponent('social/forum/components/hbs/forum', SCF.Forum, GMForumView );
})($CQ, _, Backbone, SCF);
```

## スクリプトタグ {#script-tags}

スクリプトタグは、クライアントサイドフレームワークに固有の要素です。 サーバーサイドで生成されたマークアップをクライアントサイドのモデルおよびビューにバインドするのに役立つ接着剤です。

SCF スクリプトのスクリプトタグは、コンポーネントのオーバーレイまたはオーバーライド時には削除しないでください。 HTMLに JSON を挿入するために自動作成された SCF スクリプトタグは、属性 `data-scf-json=true` で識別されます。

## SCF の clientlibs {#clientlibs-for-scf}

[ クライアントサイドライブラリ ](../../help/sites-developing/clientlibs.md) （clientlibs）を使用すると、クライアントでのコンテンツのレンダリングに使用するJavaScriptと CSS を整理および最適化できます。

SCF の clientlib は、2 つのバリアントに対して非常に具体的な命名パターンに従います。これは、カテゴリ名に「author」が含まれているかどうかによってのみ異なります。

| Clientlib バリアント | Categories プロパティのパターン |
|--- |--- |
| clientlib の完了 | cq.social.hbs.&lt; コンポーネント名 > |
| オーサー clientlib | cq.social.author.hbs.&lt; コンポーネント名 > |

### Clientlibs の完了 {#complete-clientlibs}

完全な（作成者以外の） clientlib は依存関係を含むので、ui:includeClientLib を使用してを含めると便利です。

これらのバージョンは次の場所にあります。

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

次に例を示します。

* クライアント フォルダーのノード：`/etc/clientlibs/social/hbs/forum`
* Categories プロパティ：`cq.social.hbs.forum`

[ コミュニティコンポーネントガイド ](components-guide.md) には、各 SCF コンポーネントに必要な完全な clientlib が一覧表示されています。

[ コミュニティコンポーネントの clientlibs](clientlibs.md) で、ページに clientlibs を追加する方法を説明します。

### 作成者 Clientlibs {#author-clientlibs}

オーサーバージョンの clientlib は、コンポーネントの実装に必要な最小限のJavaScriptに分解されます。

これらの clientlibs は直接には含めず、サイト用に手作りされた他の clientlibs に埋め込むことができます。

これらのバージョンは SCF libs フォルダーにあります。

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

次に例を示します。

* クライアント フォルダーのノード：`/libs/social/forum/hbs/forum/clientlibs`
* Categories プロパティ：`cq.social.author.hbs.forum`

メモ：作成者の clientlibs は他のライブラリを埋め込むことはありませんが、依存関係はリスト表示されます。 他のライブラリに埋め込む場合、依存関係は自動的には取り込まれず、埋め込む必要もあります。

必要な作成者 clientlibs は、「コミュニティコンポーネントガイド [ の各 SCF コンポーネントにリストされている clientlibs に「author」を挿入することで識別 ](components-guide.md) きます。

### 使用に関する考慮事項 {#usage-considerations}

クライアントライブラリの管理方法は、サイトによって異なります。 様々な要因として以下のものがあります。

* 全体的な速度：サイトの応答性が望ましいかもしれませんが、最初のページの読み込みが少し遅くなることは許容できます。 多くのページで同じJavaScriptを使用している場合は、1 つの clientlib に様々なJavaScriptを埋め込み、読み込む最初のページから参照することができます。 この 1 回のダウンロードでのJavaScriptはキャッシュされたままなので、後続のページでダウンロードするデータの量を最小限に抑えることができます。
* 最初のページまでの時間が短い：最初のページをすばやく読み込みたいとします。 この場合、JavaScriptは複数の小さなファイルにあり、必要な場合にのみ参照されます。
* 最初のページの読み込みと後続のダウンロードのバランス。

| **[⇐機能の基本事項](essentials.md)** | **[サーバーサイドのカスタマイズ ⇒](server-customize.md)** |
|---|---|
|   | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
