---
title: クライアント側のカスタマイズ
seo-title: Client-side Customization
description: AEM Communities でクライアント側の動作や外観をカスタマイズする
seo-description: Customizing behavior or appearance client-side in AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 57%

---

# クライアント側のカスタマイズ  {#client-side-customization}

| **[⇐ 機能の基本事項](essentials.md)** | **[サーバー側のカスタマイズ ⇒](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars ヘルパー ⇒](handlebars-helpers.md)** |

クライアント側の AEM Communities コンポーネントの外観や動作をカスタマイズするには、複数のアプローチがあります。

2 つの主要なアプローチは、コンポーネントのオーバーレイまたは拡張です。

コンポーネントの[オーバーレイ](#overlays)によって、デフォルトのコンポーネントは変更され、コンポーネントのすべての参照が影響を受けます。

コンポーネントの[拡張](#extensions)（一意の名前が付けられる）では、変更の範囲は制限されます。「extend」という用語は、「override」と同じ意味で使用されます。

## オーバーレイ {#overlays}

コンポーネントのオーバーレイは、デフォルトのコンポーネントに変更を加え、デフォルトを使用するすべてのインスタンスに影響を与える方法です。

オーバーレイは、 /内のデフォルトコンポーネントのコピーを変更することで実行されます。**アプリ** ディレクトリ内に配置されます。**libs** ディレクトリ。 コンポーネントは、同じ相対パスを使用して構築されますが、「libs」が「apps」に置き換えられる点が異なります。

/apps ディレクトリは、要求を解決するために最初に検索される場所です。見つからない場合は、/libs ディレクトリにあるデフォルトバージョンが使用されます。

/libs ディレクトリ内のデフォルトコンポーネントは変更しないでください。/libs ディレクトリは、今後のパッチおよびアップグレードによって、公開インターフェイスのメンテナンス中に必要な方法で自由に変更されます。

これは、 [拡張](#extensions) 特定の用途に対して変更を加え、コンポーネントへの一意のパスを作成し、/libs ディレクトリ内の元のデフォルトコンポーネントをスーパーリソースタイプとして参照することを希望するデフォルトコンポーネント。

コメントコンポーネントのオーバーレイの簡単な例については、 [コメントコンポーネントのオーバーレイのチュートリアル](overlay-comments.md).

## 拡張 {#extensions}

コンポーネントの拡張（優先）は、デフォルトを使用するすべてのインスタンスに影響を及ぼさずに、特定の用途のために変更をおこなう方法です。拡張されたコンポーネントは、/apps フォルダー内で一意の名前が付けられ、/libs フォルダー内のデフォルトのコンポーネントを参照します。したがって、コンポーネントのデフォルトのデザインおよび動作は変更されません。

これは、Sling の性質によって libs/ フォルダー内を検索する前に apps/ フォルダーの相対参照を解決し、したがってコンポーネントのデザインまたは動作がグローバルに変更される、デフォルトのコンポーネントの[オーバーレイ](#overlays)とは異なります。

コメントコンポーネントの拡張の簡単な例については、[コメントコンポーネントの拡張チュートリアル](extend-comments.md)を試してください。

## JavaScript バインド {#javascript-binding}

コンポーネントの HBS スクリプトは、この機能を実装する JavaScript オブジェクト、モデルおよびビューにバインドされる必要があります。

の値 `data-scf-component` 属性は、 **`social/tally/components/hbs/rating`**&#x200B;または拡張（カスタマイズ）されたコンポーネント（カスタマイズされた機能）( 例： **weretail/components/hbs/rating**.

コンポーネントをバインドするには、以下の属性を使用してコンポーネントスクリプト全体を &lt;div> 要素で囲む必要があります。

* `data-component-id`=&quot;{{id}}&quot;

   コンテキストから id プロパティに解決されます。

* `data-scf-component`=&quot;*&lt;resourceType>*

例： `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## カスタムプロパティ {#custom-properties}

コンポーネントを拡張またはオーバーレイする場合、変更されたダイアログにプロパティを追加できます。

コンポーネント／リソースに対して設定されるすべてのプロパティには、handlebars テンプレートでプロパティキーを参照することによってアクセスできます。

`{{properties.<property_name>}}`

## CSS のスキンの適用 {#skinning-css}

Web サイトの全体的なテーマに合うようにコンポーネントをカスタマイズすることは、「スキンの適用」によって実現できます。これは、色、フォント、画像、ボタン、リンク、間隔および位置設定を特定の程度まで変更することです。

スキンの適用は、フレームワークスタイルを選択的に上書きすることによって、または完全に新しいスタイルシートを記述することによって実行できます。SCF コンポーネントによって、コンポーネントを構成するさまざまな要素に影響する、名前空間が設定された、モジュール式のセマンティック CSS クラスが定義されます。

コンポーネントにスキンを適用するには、次の手順に従います。

1. 変更する要素を指定します（例：コンポーザー領域、ツールバーボタン、メッセージフォントなど）。
1. これらの要素に影響する CSS クラス／ルールを識別します。
1. スタイルシートファイル（.css）を作成します。
1. クライアントライブラリフォルダー ([clientlibs](#clientlibs-for-scf)) をクリックし、それを [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. スタイルシートで指定した CSS クラスおよびルール (#2) を再定義し、スタイルを追加します。

これで、カスタムスタイルによってデフォルトのフレームワークスタイルは上書きされ、コンポーネントは新しいスキンでレンダリングされます。

>[!CAUTION]
>
>先頭に `scf-js` には、javascript コードで特に使用されます。 これらのクラスは、コンポーネントの状態に影響を与えます（非表示から表示に切り替えるなど）。上書きも削除もできません。
>
>また、 `scf-js` クラスはスタイルに影響を与えません。クラス名は、要素の状態を制御するので、副作用が生じる可能性があるという注意を払って、スタイルシートで使用できます。

## JavaScript の拡張 {#extending-javascript}

JavaScript コンポーネントの実装を拡張するには、次の操作が必要です。

1. jcr:resourceSuperType を拡張コンポーネントの jcr:resourceType の値（例： social/forum/components/hbs/forum）に設定して、アプリのコンポーネントを作成します。
1. デフォルトの SCF コンポーネントの JavaScript を調べて、SCF.registerComponent() を使用して登録する必要があるメソッドを判断します。
1. 拡張コンポーネントの JavaScript をコピーするか、最初から開始します。
1. メソッドを拡張します。
1. SCF.registerComponent() を使用して、すべてのメソッドをデフォルトまたはカスタマイズされたオブジェクトとビューのいずれかに登録します。

### forum.js：フォーラム - HBS のサンプル拡張  {#forum-js-sample-extension-of-forum-hbs}

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

スクリプトタグは、クライアント側フレームワークの固有の部分です。 これらは、サーバー側で生成されたマークアップをクライアント側のモデルおよびビューにバインドするために役立ちます。

コンポーネントをオーバーレイまたは優先するときに SCF スクリプト内のスクリプトタグを削除しないでください。HTMLに JSON を挿入するために自動的に作成された SCF スクリプトタグは、属性で識別されます。 `data-scf-json=true`.

## SCF の clientlib {#clientlibs-for-scf}

[クライアント側ライブラリ](../../help/sites-developing/clientlibs.md)（clientlib）の使用により、クライアント側でコンテンツをレンダリングするために使用される JavaScript および CSS を整理および最適化できます。

SCF の clientlib は、カテゴリ名内の「author」の存在のみが異なる 2 つのバリアントの具体的な命名パターンに従います。

| clientlib のバリアント | カテゴリプロパティのパターン |
|--- |--- |
| 完全 clientlib | cq.social.hbs.&lt;component name> |
| オーサー clientlib | cq.social.author.hbs.&lt;component name> |

### 完全 clientlib {#complete-clientlibs}

完全（オーサー以外）clientlib には依存関係が含まれており、ui:includeClientLib を使用して含める場合に便利です。

これらのバージョンは、次の場所にあります。

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

次に例を示します。

* クライアントフォルダーノード： `/etc/clientlibs/social/hbs/forum`
* Categories プロパティ： `cq.social.hbs.forum`

[コミュニティコンポーネントガイド](components-guide.md)によって、各 SCF コンポーネントに必要なすべての clientlib が一覧表示されます。

[コミュニティコンポーネントの clientlib](clientlibs.md) では、clientlib をページに追加する方法が説明されています。

### オーサー clientlib {#author-clientlibs}

オーサーバージョンの clientlib は、コンポーネントを実装するために必要な最小限の JavaScript に縮小されています。

これらの clientlib を直接含めることはできませんが、代わりに、サイト用に手動で作成された他の clientlib に埋め込むことができます。

これらのバージョンは、SCF libs フォルダー内にあります。

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

次に例を示します。

* クライアントフォルダーノード： `/libs/social/forum/hbs/forum/clientlibs`
* Categories プロパティ： `cq.social.author.hbs.forum`

注意：オーサー clientlib によって他のライブラリは埋め込まれませんが、依存関係は示されます。他のライブラリに埋め込まれる場合、依存関係は自動的に取り込まれず、埋め込む必要があります。

必要なオーサー clientlib は、[コミュニティコンポーネントガイド](components-guide.md)で各 SCF コンポーネントについてリストされた clientlib に「author」を挿入することによって識別できます。

### 使用上の考慮事項 {#usage-considerations}

サイトによってクライアントライブラリの管理方法は異なります。次のような要因が考えられます。

* 全体的な速度：応答の速いサイトが目的ですが、最初のページのロードが少し遅いことは受け入れられる場合があります。多くのページで同じ JavaScript を使用している場合、様々な JavaScript を 1 つの clientlib に埋め込み、最初のページから参照して読み込むことができます。 この単一のダウンロードでの JavaScript はキャッシュされたままになり、後続のページでダウンロードするデータ量が最小限に抑えられます。
* 迅速な最初のページ：最初のページが迅速にロードされることが目的である場合があります。この場合、JavaScript は複数の小さなファイルに含まれ、必要な場所でのみ参照されます。
* 最初のページのロードと後続のダウンロードとの間のバランス。

| **[⇐ 機能の基本事項](essentials.md)** | **[サーバー側のカスタマイズ ⇒](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars ヘルパー ⇒](handlebars-helpers.md)** |
