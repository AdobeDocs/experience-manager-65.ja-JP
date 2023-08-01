---
title: クライアント側のカスタマイズ
seo-title: Client-side Customization
description: AEM Communitiesでのクライアント側での動作や外観のカスタマイズ
seo-description: Customizing behavior or appearance client-side in AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: c667a1658e43bb5b61daede5f94256dae582a4fc
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# クライアント側のカスタマイズ  {#client-side-customization}

| **[⇐機能の基本事項](essentials.md)** | **[サーバー側のカスタマイズ ⇒](server-customize.md)** |
|---|---|
|   | **[SCF Handlebars ヘルパー ⇒](handlebars-helpers.md)** |

クライアント側でAEM Communitiesコンポーネントの外観や動作をカスタマイズするには、いくつかの方法があります。

主にコンポーネントをオーバーレイまたは拡張する方法が 2 つあります。

[オーバーレイ](#overlays) コンポーネントは、デフォルトのコンポーネントを変更し、コンポーネントへのすべての参照に影響を与えます。

[拡張ガイド](#extensions) コンポーネントは一意の名前を付け、変更の範囲を制限します。 「extend」という用語は、「override」と同じ意味で使用されます。

## オーバーレイ {#overlays}

コンポーネントのオーバーレイは、デフォルトのコンポーネントに変更を加え、デフォルトを使用するすべてのインスタンスに影響を与える方法です。

オーバーレイは、 /内のデフォルトコンポーネントのコピーを変更することで実行されます。**アプリ** ディレクトリ内に配置されます。**libs** ディレクトリ。 コンポーネントは、同じ相対パスを使用して構築されますが、「libs」が「apps」に置き換えられる点が異なります。

/apps ディレクトリは、要求を解決するために最初に検索される場所です。見つからない場合は、/libs ディレクトリにあるデフォルトバージョンが使用されます。

/libs ディレクトリ内のデフォルトコンポーネントは、今後のパッチやアップグレードでは、パブリックインターフェイスを維持しながら必要な方法で/libs ディレクトリを自由に変更できるので、変更しないでください。

これは、次とは異なります： [拡張](#extensions) 特定の用途に対して変更を加え、コンポーネントへの一意のパスを作成し、/libs ディレクトリ内の元のデフォルトコンポーネントをスーパーリソースタイプとして参照することを希望するデフォルトコンポーネント。

コメントコンポーネントのオーバーレイの簡単な例については、 [コメントコンポーネントのオーバーレイのチュートリアル](overlay-comments.md).

## 拡張子 {#extensions}

コンポーネントの拡張（上書き）は、デフォルトを使用するすべてのインスタンスに影響を与えることなく、特定の使用に対して変更を加える方法です。 拡張されたコンポーネントは、/apps フォルダー内で一意の名前を付け、/libs フォルダー内のデフォルトコンポーネントを参照するので、コンポーネントのデフォルトのデザインと動作は変更されません。

これは、次とは異なります： [重ね合わせ](#overlays) Sling の特性が解決されるデフォルトコンポーネントは、libs/フォルダー内で検索する前に apps/フォルダーへの相対参照を解決するので、コンポーネントのデザインや動作はグローバルに変更されます。

コメントコンポーネントの拡張の簡単な例については、 [コメントコンポーネントの拡張チュートリアル](extend-comments.md).

## JavaScript バインディング {#javascript-binding}

コンポーネントの HBS スクリプトは、この機能を実装する JavaScript オブジェクト、モデル、ビューにバインドする必要があります。

の値 `data-scf-component` 属性は、次のようなデフォルト値に設定できます。 **`social/tally/components/hbs/rating`**&#x200B;または拡張（カスタマイズ）されたコンポーネント（カスタマイズされた機能）( 例： **weretail/components/hbs/rating**.

コンポーネントをバインドするには、コンポーネントスクリプト全体を &lt;div> 要素に次の属性を追加します。

* `data-component-id`=&quot;`{{id}}`&quot;

  コンテキストから id プロパティに解決されます。

* `data-scf-component`=&quot;*&lt;resourcetype>*

例： `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="`{{id}}`" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## カスタムプロパティ {#custom-properties}

コンポーネントを拡張またはオーバーレイする場合、変更したダイアログにプロパティを追加できます。

コンポーネントやリソースに設定されたすべてのプロパティにアクセスするには、handlebars テンプレート内のプロパティキーを参照します。

`{{properties.<property_name>}}`

## CSS のスキニング {#skinning-css}

Web サイトの全体的なテーマに合わせたコンポーネントのカスタマイズは、色、フォント、画像、ボタン、リンク、間隔、特定の程度の位置の変更など、「スキン表示」によって実現できます。

スキニングは、フレームワークスタイルを選択的に上書きするか、まったく新しいスタイルシートを書き込むことで実現できます。 SCF コンポーネントは、コンポーネントを構成する様々な要素に影響を与える名前空間、モジュラー、セマンティック CSS クラスを定義します。

コンポーネントをスキンにするには：

1. 変更する要素を指定します（例：コンポーザー領域、ツールバーボタン、メッセージフォントなど）。
1. これらの要素に影響する CSS クラス/ルールを特定します。
1. スタイルシートファイル (.css) を作成します。
1. クライアントライブラリフォルダーにスタイルシートを含める ([clientlibs](#clientlibs-for-scf)) をクリックし、を使用してテンプレートまたはページから含める必要があります。 [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. スタイルシートで指定した CSS クラスおよびルール (#2) を再定義し、スタイルを追加します。

カスタムスタイルがデフォルトのフレームワークスタイルを上書きし、新しいスキンでコンポーネントがレンダリングされるようになりました。

>[!CAUTION]
>
>先頭に `scf-js` は、JavaScript コードで特定の用途を持ちます。 これらのクラスは、コンポーネントの状態に影響を与えます（非表示から表示に切り替えるなど）。また、上書きも削除もできません。
>
>また、 `scf-js` クラスはスタイルに影響を与えません。クラス名は、要素の状態を制御するので、副作用が生じる可能性があるという注意を払って、スタイルシートで使用できます。

## JavaScript の拡張 {#extending-javascript}

JavaScript コンポーネントの実装を拡張するには、次の操作が必要です。

1. jcr:resourceSuperType を拡張コンポーネントの jcr:resourceType の値に設定して、アプリのコンポーネントを作成します（例：social/forum/components/hbs/forum）。
1. デフォルトの SCF コンポーネントの JavaScript を調べて、SCF.registerComponent() を使用して登録する必要があるメソッドを判断します。
1. 拡張コンポーネントの JavaScript をコピーするか、最初から開始します。
1. メソッドを拡張します。
1. SCF.registerComponent() を使用して、すべてのメソッドをデフォルトまたはカスタマイズされたオブジェクトとビューのいずれかに登録します。

### forum.js：フォーラムのサンプル拡張 — HBS  {#forum-js-sample-extension-of-forum-hbs}

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

スクリプトタグは、クライアント側フレームワークに固有の部分です。 これは、サーバー側で生成されたマークアップを、クライアント側のモデルやビューと結び付けるのに役立つ接着剤です。

コンポーネントをオーバーレイまたは上書きする際に、SCF スクリプト内のスクリプトタグを削除しないでください。 HTMLに JSON を挿入するために自動的に作成された SCF スクリプトタグは、属性で識別されます。 `data-scf-json=true`.

## SCF の clientlibs {#clientlibs-for-scf}

の使用 [クライアントサイドライブラリ](../../help/sites-developing/clientlibs.md) (clientlibs) は、クライアントでコンテンツをレンダリングするために使用する JavaScript と CSS を整理および最適化する手段を提供します。

SCF の clientlib は、2 つのバリアントに対して非常に具体的な命名パターンに従います。これは、カテゴリ名に「author」が存在する場合にのみ異なります。

| Clientlib のバリアント | カテゴリプロパティのパターン |
|--- |--- |
| complete clientlib | cq.social.hbs.&lt;component name> |
| オーサー clientlib | cq.social.author.hbs.&lt;component name> |

### 完全な clientlibs {#complete-clientlibs}

完全な（作成者以外の）clientlib は依存関係を含み、ui:includeClientLib を含めるのに便利です。

これらのバージョンは、次の場所にあります。

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

例：

* クライアントフォルダーノード： `/etc/clientlibs/social/hbs/forum`
* Categories プロパティ： `cq.social.hbs.forum`

The [コミュニティコンポーネントガイド](components-guide.md) 各 SCF コンポーネントに必要な完全な clientlib を示します。

[コミュニティコンポーネントの clientlib](clientlibs.md) を使用して、ページに clientlibs を追加する方法を説明します。

### オーサー Clientlibs {#author-clientlibs}

オーサーバージョンの clientlib は、コンポーネントの実装に必要な最小限の JavaScript まで削除されます。

これらの clientlib は直接含めるべきではなく、サイト用に手作りされた他の clientlib に埋め込むことができます。

これらのバージョンは、SCF libs フォルダーにあります。

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

例：

* クライアントフォルダーノード： `/libs/social/forum/hbs/forum/clientlibs`
* Categories プロパティ： `cq.social.author.hbs.forum`

注意：オーサークライアントライブラリは他のライブラリを埋め込みませんが、依存関係をリストします。 他のライブラリに埋め込まれる場合、依存関係は自動的に取り込まれず、埋め込む必要があります。

必要なオーサー clientlib は、 [コミュニティコンポーネントガイド](components-guide.md).

### 使用に関する考慮事項 {#usage-considerations}

クライアントライブラリの管理方法は、サイトごとに異なります。 次のような要因が考えられます。

* 全体的な速度：サイトがレスポンシブであることが望ましいのかもしれませんが、最初のページの読み込みが少し遅い場合でも問題ありません。 多くのページで同じ JavaScript を使用している場合、様々な JavaScript を 1 つの clientlib に埋め込み、最初のページから参照して読み込みます。 この単一のダウンロードの JavaScript はキャッシュされたままになり、後続のページでダウンロードするデータ量が最小限に抑えられます。
* 最初のページへの短い時間：最初のページがすばやく読み込まれるようにしたい場合があります。 この場合、JavaScript は複数の小さなファイルに含まれ、必要な場所でのみ参照されます。
* 最初のページ読み込みとそれ以降のダウンロードの間のバランス。

| **[⇐機能の基本事項](essentials.md)** | **[サーバー側のカスタマイズ ⇒](server-customize.md)** |
|---|---|
|   | **[SCF Handlebars ヘルパー ⇒](handlebars-helpers.md)** |
