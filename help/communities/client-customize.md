---
title: クライアント側のカスタマイズ
description: AEM Communitiesのクライアントサイドでのビヘイビアーまたはアピアランスのカスタマイズ
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 1%
---
# クライアント側のカスタマイズ  {#client-side-customization}

| **[⇐機能エッセンシャル](essentials.md)** | **[サーバーサイドのカスタマイズ ⇒](server-customize.md)** |
|---|---|
|   | **[SCF ハンドルバーのヘルパー⇒](handlebars-helpers.md)** |

クライアントサイドのAEM Communities コンポーネントの外観や動作をカスタマイズするには、いくつかの方法があります。

コンポーネントをオーバーレイまたは拡張するには、主にふたつの方法があります。

[&#x200B; コンポーネントをオーバーレイ &#x200B;](#overlays)すると、デフォルトコンポーネントが変更され、コンポーネントへのすべての参照に影響します。

一意の名前を持つコンポーネントを[拡張](#extensions)すると、変更の範囲が制限されます。 「extend」という用語は、「override」と同じ意味で使用されます。

## オーバーレイ {#overlays}

コンポーネントのオーバーレイは、デフォルトコンポーネントを変更し、デフォルトを使用するすべてのインスタンスに影響を与える方法です。

オーバーレイは、/**libs** ディレクトリの元のコンポーネントを変更するのではなく、/**apps** ディレクトリのデフォルトコンポーネントのコピーを変更することで実現します。 コンポーネントは同一の相対パスで構築されますが、「libs」は「apps」に置き換えられます。

/apps ディレクトリは、リクエストを解決するために最初に検索される場所です。見つからない場合は、/libs ディレクトリのデフォルトバージョンが使用されます。

/libs ディレクトリ内のデフォルトコンポーネントは、今後のパッチやアップグレードで、パブリックインターフェイスを維持しながら必要な方法で/libs ディレクトリを変更できるため、変更しないでください。

これは、特定の使用に対して変更を行い、コンポーネントに対して一意のパスを作成し、/libs ディレクトリ内の元のデフォルトコンポーネントをスーパーリソースタイプとして参照することに依存するデフォルトコンポーネントの[拡張](#extensions)とは異なります。

コメントコンポーネントのオーバーレイの簡単な例として、[&#x200B; コメントコンポーネントのオーバーレイチュートリアル &#x200B;](overlay-comments.md)を試してください。

## 拡張子 {#extensions}

コンポーネントの拡張（オーバーライド）は、デフォルトを使用するすべてのインスタンスに影響を与えることなく、特定の使用に対して変更を加える方法です。 拡張コンポーネントは/apps フォルダー内で一意に名前が付けられ、/libs フォルダー内のデフォルトコンポーネントを参照するため、コンポーネントのデフォルトデザインと動作は変更されません。

これは、libs/ フォルダー内で検索する前にSlingの性質がapps/ フォルダーへの相対参照を解決するデフォルトのコンポーネントである[&#x200B; オーバーレイ &#x200B;](#overlays)とは異なるため、コンポーネントのデザインや動作はグローバルに変更されます。

コメントコンポーネントの拡張の簡単な例については、[&#x200B; コメントコンポーネントの拡張チュートリアル &#x200B;](extend-comments.md)を参照してください。

## JavaScript バインディング {#javascript-binding}

コンポーネントのHBS スクリプトは、この機能を実装するJavaScript オブジェクト、モデル、ビューにバインドする必要があります。

`data-scf-component`属性の値は、**`social/tally/components/hbs/rating`**&#x200B;などの既定値、または&#x200B;**weretail/components/hbs/rating**&#x200B;などのカスタマイズされた機能の拡張（カスタマイズ）コンポーネントである場合があります。

コンポーネントをバインドするには、コンポーネントスクリプト全体を、次の属性を持つ&lt;div>要素の中に囲む必要があります。

* `data-component-id`=&quot;`{{id}}`&quot;

  コンテキストからid プロパティに解決します

* `data-scf-component`=&quot;*&lt;resourceType>*

例えば、`/apps/weretail/components/hbs/rating/rating.hbs`から：

```xml
<div class="we-Rating" data-component-id="`{{id}}`" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## カスタムプロパティ {#custom-properties}

コンポーネントを拡張またはオーバーレイする場合、変更したダイアログにプロパティを追加できます。

コンポーネント/リソースに設定されているすべてのプロパティには、ハンドルバーテンプレートのプロパティキーを参照してアクセスできます。

`{{properties.<property_name>}}`

## スキニング CSS {#skinning-css}

web サイト全体のテーマに合わせてコンポーネントをカスタマイズするには、色、フォント、画像、ボタン、リンク、間隔、さらには特定の範囲で配置を変更する「スキニング」を実行します。

スキニングは、フレームワークスタイルを選択して上書きするか、まったく新しいスタイルシートを作成することで実現できます。 SCF コンポーネントは、コンポーネントを構成する様々な要素に影響を与える名前空間、モジュール式、セマンティック CSS クラスを定義します。

コンポーネントのスキンを作成するには：

1. 変更する要素を特定します（例：コンポーザー領域、ツールバーボタン、メッセージフォントなど）。
1. これらの要素に影響を与えるCSS クラス/ルールを特定します。
1. スタイルシートファイル（.css）を作成します。
1. サイトのクライアントライブラリフォルダー（[clientlibs](#clientlibs-for-scf)）にスタイルシートを含め、[ui:includeClientLib](../../help/sites-developing/clientlibs.md)を含むテンプレートとページからスタイルシートが含まれていることを確認します。

1. スタイルシートで特定（#2）したCSS クラスとルールを再定義し、スタイルを追加します。

カスタムスタイルはデフォルトのフレームワークスタイルを上書きし、コンポーネントは新しいスキンでレンダリングされます。

>[!CAUTION]
>
>先頭に`scf-js`が付いたCSS クラス名は、JavaScript コードで特定の用途を持ちます。 これらのクラスは、コンポーネントの状態（非表示から表示への切り替えなど）に影響を与えるので、オーバーライドも削除もできません。
>
>`scf-js` クラスはスタイルに影響を与えませんが、クラス名は要素の状態を制御するため、副作用が発生する可能性があることを警告するスタイルシートで使用できます。

## JavaScriptの拡張 {#extending-javascript}

コンポーネントのJavaScript実装を拡張するには、次のことが必要です。

1. 拡張コンポーネントのjcr:resourceTypeの値に設定されたjcr:resourceSuperTypeを使用して、アプリのコンポーネント（social/forum/components/hbs/forumなど）を作成します。
1. デフォルトのSCF コンポーネントのJavaScriptを調べて、SCF.registerComponent （）を使用して登録する必要があるメソッドを判断します。
1. 拡張コンポーネントのJavaScriptをコピーするか、最初から開始します。
1. メソッドを拡張します。
1. SCF.registerComponent （）を使用して、すべてのメソッドをデフォルトまたはカスタマイズされたオブジェクトとビューに登録します。

### forum.js: フォーラムのサンプル拡張機能 – HBS  {#forum-js-sample-extension-of-forum-hbs}

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

スクリプトタグは、クライアントサイドフレームワークに固有の要素です。 これは、サーバーサイドで生成されたマークアップを、クライアントサイドのモデルやビューとバインドするのに役立つ接着剤です。

SCF スクリプトのスクリプトタグは、コンポーネントをオーバーレイまたはオーバーライドする際に削除しないでください。 HTMLでJSONを挿入するために自動的に作成されたSCF スクリプトタグは、属性`data-scf-json=true`で識別されます。

## SCFのClientlibs {#clientlibs-for-scf}

[&#x200B; クライアントサイドライブラリ &#x200B;](../../help/sites-developing/clientlibs.md) （clientlibs）を使用すると、クライアント上でコンテンツをレンダリングするために使用されるJavaScriptとCSSを整理および最適化する方法が提供されます。

SCFのclientlibsは、2つのバリエーションに対して非常に特殊な命名パターンに従っており、カテゴリ名に「author」が含まれているかどうかによって異なります。

| Clientlib バリアント | カテゴリープロパティのパターン |
|--- |--- |
| 完全clientlib | cq.social.hbs.&lt; コンポーネント名> |
| clientlibの作成 | cq.social.author.hbs.&lt; コンポーネント名> |

### 完全なClientlibs {#complete-clientlibs}

完全な（オーサー以外の） clientlibには依存関係が含まれており、ui:includeClientLibを使用して含めるのに便利です。

これらのバージョンは、次の場所にあります。

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

例：

* クライアント フォルダーのノード：`/etc/clientlibs/social/hbs/forum`
* Categories プロパティ：`cq.social.hbs.forum`

[&#x200B; コミュニティコンポーネントガイド &#x200B;](components-guide.md)には、各SCF コンポーネントに必要な完全なクライアントライブラリが一覧表示されています。

[Clientlibs for Communities Components](clientlibs.md)は、ページにclientlibsを追加する方法について説明します。

### オーサーClientlibs {#author-clientlibs}

オーサー版のclientlibは、コンポーネントの実装に必要な最小限のJavaScriptまで削除されます。

これらのclientlibを直接含めるのではなく、サイト用に手作業で作成した他のclientlibに埋め込むことができます。

これらのバージョンは、SCF libs フォルダーにあります。

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

例：

* クライアント フォルダーのノード：`/libs/social/forum/hbs/forum/clientlibs`
* Categories プロパティ：`cq.social.author.hbs.forum`

注意：オーサー側のクライアントライブラリは他のライブラリを埋め込むことはありませんが、依存関係はリスト化されています。 他のライブラリに埋め込まれた場合、依存関係は自動的に取り込まれることはなく、同様に埋め込む必要があります。

必要なオーサーclientlibは、[&#x200B; コミュニティコンポーネントガイド &#x200B;](components-guide.md)の各SCF コンポーネントにリストされているclientlibsに「author」を挿入することで特定できます。

### 使用上の考慮事項 {#usage-considerations}

クライアントライブラリの管理方法は、サイトごとに異なります。 要因には、次のようなものがあります。

* 全体的な速度：サイトの応答性が向上することを望んでいますが、最初のページの読み込みが少し遅くても問題ありません。 多くのページで同じJavaScriptを使用している場合、様々なJavaScriptを1つのclientlibに埋め込み、最初のページから参照して読み込むことができます。 この1回のダウンロードのJavaScriptはキャッシュされたままになり、後続のページでダウンロードするデータの量が最小限に抑えられます。
* 最初のページまでの時間が短い：最初のページの読み込みが速くなることを望んでいるのかもしれません。 この場合、JavaScriptは複数の小さなファイルに含まれており、必要な場合にのみ参照されます。
* 最初のページ読み込みとその後のダウンロードのバランス。

| **[⇐機能エッセンシャル](essentials.md)** | **[サーバーサイドのカスタマイズ ⇒](server-customize.md)** |
|---|---|
|   | **[SCF ハンドルバーのヘルパー⇒](handlebars-helpers.md)** |
