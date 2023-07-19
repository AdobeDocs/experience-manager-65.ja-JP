---
title: AEM タグ付けフレームワーク
description: コンテンツのタグ付けとAEM Tagging インフラストラクチャの使用
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 47%

---


# AEM タグ付けフレームワーク {#aem-tagging-framework}

タグ付けにより、コンテンツを分類および整理できますタグの分類には、名前空間と分類を使用できます。タグの使用について詳しくは、以下を参照してください。

* ドキュメントを参照 [タグの使用](/help/sites-authoring/tags.md) コンテンツ作成者としてのコンテンツのタグ付けについて説明します。
* ドキュメントを参照 [タグの管理](/help/sites-administering/tags.md) タグの作成と管理、およびタグが適用されるコンテンツに関する管理者の視点。

この記事では、AEMでタグ付けをサポートする基盤となるフレームワークと、それを開発者として使用する方法に焦点を当てます。

## はじめに {#introduction}

コンテンツにタグを付けてAEM Tagging インフラストラクチャを使用するには：

* タグは、`[cq:Tag](#tags-cq-tag-node-type)` タイプのノードとして[分類階層のルートノード](#taxonomy-root-node)の下に存在する必要があります。

* タグ付けされたコンテンツノードの`NodeType`には、[`cq:Taggable`](#taggable-content-cq-taggable-mixin) Mixin が含まれている必要があります。
* [`TagID`](#tagid) がコンテンツノードの [`cq:tags`](#tagged-content-cq-tags-property) プロパティに追加され、` [cq:Tag](#tags-cq-tag-node-type)` タイプのノードに解決されます。

## タグ：cq:Tag ノードタイプ  {#tags-cq-tag-node-type}

タグの宣言は、リポジトリーにおける `cq:Tag` タイプのノードにキャプチャされます。。

タグは、単純な単語にすることができます ( 例： `sky`) または階層的な分類 ( 例： `fruit/apple`（両方の汎用を意味する） `fruit` そしてより具体的に `apple`) をクリックします。

タグは一意のタグ ID で識別されます。

タグには、タイトル、ローカライズされたタイトル、説明など、オプションのメタ情報が含まれます。 ユーザーインターフェイスには、タグ ID ではなくタイトル（存在する場合）が表示されます。

タグ付けフレームワークでは、作成者やサイト訪問者に、特定の事前定義されたタグだけを使用するよう制限を設けることもできます。

### タグの特徴 {#tag-characteristics}

* ノードタイプは `cq:Tag`n
* ノード名は [タグ ID](#tagid).
* この [タグ ID](#tagid) 常にを含む [名前空間。](#tag-namespace)
* この `jcr:title` プロパティ（UI に表示するタイトル）はオプションです。
* `jcr:description` プロパティは省略可能です。
* 子ノードを含む場合、タグは [コンテナタグで使用できます。](#container-tags)
* リポジトリーにおいて、[分類のルートノード](#taxonomy-root-node)と呼ばれる基本パスの下に保存されます。

タグは単に JCR ノードなので、ノード名はもちろん [JCR 命名規則。](naming-conventions.md)

### タグ ID {#tagid}

タグ ID は、リポジトリ内のタグノードに解決されるパスを識別します。

通常、タグ ID は名前空間で始まる短縮形のタグ ID です。または、 [分類のルートノード。](#taxonomy-root-node)

コンテンツがタグ付けされているときに、コンテンツがまだ存在しない場合は、 `[cq:tags](#tagged-content-cq-tags-property)` プロパティが content ノードに追加され、タグ ID がプロパティの `String` 配列の値。

タグ ID は、[名前空間](#tag-namespace)とそれに続くローカルタグ ID で構成されます。[コンテナタグ](#container-tags) には、分類の階層順を表すサブタグがあります。 サブタグは、任意のローカルタグ ID と同じタグを参照するために使用できます。 例えば、コンテンツのタグ付けには `fruit` サブタグを含むコンテナタグ ( `fruit/apple` および `fruit/banana`.

### 分類のルートノード {#taxonomy-root-node}

分類のルートノードは、リポジトリー内にあるすべてのタグの基本パスです。分類のルートノードは、`cq:Tag` タイプのノードにすることができません。

AEM の基本パスは `/content/cq:tags` であり、ルートノードのタイプは `cq:Folder` です。

### タグの名前空間 {#tag-namespace}

名前空間を使用してグループ化できます。 最も一般的な使用例は、サイトごと（例：公開、内部、ポータル）または大規模なアプリケーションごと（例：WCM、Assets、Communities）の名前空間です。 ただし、名前空間は他の様々なニーズに使用できます。 名前空間は、現在のコンテンツに適用できるタグのサブセット（特定の名前空間のタグなど）のみを表示するために、ユーザーインターフェイスで使用されます。

タグの名前空間は、分類サブツリーの最初のレベルです。これは、[分類のルートノード](#taxonomy-root-node)の直下のノードです。名前空間は `cq:Tag` タイプのノードで、その親は `cq:Tag` ノードタイプではありません。

すべてのタグには名前空間があります。名前空間が指定されていない場合、タグはデフォルトの名前空間 (TagID) に割り当てられます `default` タイトルを持つ `Standard Tags`例： `/content/cq:tags/default`.

### コンテナタグ {#container-tags}

コンテナタグは、任意の数およびタイプの子ノードを含む、`cq:Tag` タイプのノードです。これにより、カスタムメタデータを使用してタグモデルを強化できます。

さらに、分類のコンテナタグ（スーパータグ）は、すべてのサブタグの購読として機能します。 例えば、 `fruit/apple` は、 `fruit` 同様に。 つまり、でタグ付けされたコンテンツを検索します。 `fruit` また、次のタグが付いたコンテンツも見つかります： `fruit/apple`.

### タグ ID の解決 {#resolving-tagids}

タグ ID にコロン (`:`) を呼び出すと、コロンでタグやサブ分類から名前空間が区切られます。このタグはスラッシュ (`/`) をクリックします。 TagID にコロンが含まれない場合、デフォルトの名前空間が暗黙化されます。

タグの標準の場所は `/content/cq:tags` の下のみです。

存在しないパスまたはを指さないパスを参照するタグ `cq:Tag` ノードは無効と見なされ、無視されます。

次の表に、タグ ID の例とその要素、リポジトリでそのタグ ID がどのように絶対パスに解決されるかを示します。

| タグ ID | 名前空間 | ローカル ID | コンテナタグ | リーフタグ | リポジトリー内の絶対パス |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`、`apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | なし | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | なし | なし | なし、名前空間 | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### タグタイトルのローカリゼーション {#localization-of-tag-title}

タグにオプションのタイトル文字列 ( `jcr:title`) の代わりに使用する場合、プロパティ `jcr:title.<locale>`.

詳しくは、次のドキュメントを参照してください。

* [異なる言語のタグ](/help/sites-developing/building.md#tags-in-different-languages)（API の使用を説明します）
* [異なる言語でのタグの管理](/help/sites-administering/tags.md#managing-tags-in-different-languages)（タグ付けコンソールの使用を説明します）

### アクセス制御 {#access-control}

タグは、リポジトリ内で[分類のルートノード](#taxonomy-root-node)の下にノードとして存在します。の下にノードとして存在します。作成者やサイト訪問者に対し、特定の名前空間内でのタグの作成を許可または禁止するには、リポジトリーに適切な ACL を設定します。

また、特定のタグや名前空間に対する読み取り権限を拒否することで、特定のコンテンツにタグを適用する機能を制御できます。

一般的な方法には次のものがあります。

* すべての名前空間への書き込みアクセス（`/content/cq:tags` 下への add／modify）を`tag-administrators` グループ／役割に許可する。このグループは、追加設定なしで使用できる AEM に付属しています。
* 読み取り可能にする必要があるすべての名前空間への読み取りアクセスをユーザー／作成者に許可する。
* ユーザーや作成者がタグを自由に定義できる名前空間への書き込みアクセスを許可する（以下にノードを追加） `/content/cq:tags/some_namespace`)

## タグ付け可能なコンテンツ：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

アプリケーション開発者がコンテンツタイプにタグを付けるために、ノードの登録 ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) は、 `cq:Taggable` mixin または `cq:OwnerTaggable` mixin.

`cq:OwnerTaggable` Mixin は `cq:Taggable` から継承されており、その目的は、所有者または作成者がコンテンツを分類できることを示すことです。AEM では、`cq:PageContent` ノードの属性にすぎません。`cq:OwnerTaggable` Mixin は、タグ付けフレームワークには必要ありません。

>[!NOTE]
>
>集約されたコンテンツアイテムの最上位ノード（またはその `jcr:content` ノード）では、タグの有効化だけを行うことをお勧めします。以下に例を示します。
>
>* ページ (`cq:Page`) で、 `jcr:content`ノードのタイプは `cq:PageContent` これには `cq:Taggable` mixin
>* アセット ( `cq:Asset`) で、 `jcr:content/metadata` ノードは常に `cq:Taggable` mixin
>

### ノードタイプの表記（CND） {#node-type-notation-cnd}

ノードタイプの定義は、リポジトリに CND ファイルとして存在します。 CND 表記は、[こちら](https://jackrabbit.apache.org/jcr/node-type-notation.html)の JCR ドキュメントの一部として定義されています。

AEM に含まれるノードタイプの基本的な定義は、次のようになります。

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## タグ付けされたコンテンツ：cq:tags プロパティ {#tagged-content-cq-tags-property}

この `cq:tags` プロパティは `String` 作成者またはサイト訪問者がコンテンツに適用した 1 つ以上のタグ ID を保存するために使用する配列。 このプロパティは、`[cq:Taggable](#taggable-content-cq-taggable-mixin)` Mixin で定義されているノードに追加した場合にのみ意味があります。

>[!NOTE]
>
>AEMのタグ付け機能を使用するには、カスタムで開発されたアプリケーションは、 `cq:tags`.

## タグの移動と統合 {#moving-and-merging-tags}

以下に、 [タグ付けコンソール](/help/sites-administering/tags.md):

* タグ A を `/content/cq:tags` の下のタグ B に移動または統合した場合：

   * タグ A は削除されず、 `cq:movedTo` プロパティ。
   * タグ B が作成され（移動があった場合）、 `cq:backlinks` プロパティ。

* `cq:movedTo` はタグ B を指します。

   * このプロパティは、タグ A がタグ B に移動または結合されたことを意味します。 タグ B を移動すると、それに応じてこのプロパティが更新されます。 タグ A は非表示になり、タグ A を示すコンテンツノード内のタグ ID を解決するリポジトリに保持されるだけになります。タグガベージコレクターは、タグ A のように、コンテンツノードで指定されなくなったタグを削除します。


   * の特別な値 `cq:movedTo` プロパティは `nirvana`.タグが削除された場合に適用されますが、リポジトリからは削除できません。これは、 `cq:movedTo` それは守るべきだ

  >[!NOTE]
  >
  >`cq:movedTo` プロパティは、次のいずれかの条件を満たす場合にのみ、移動または統合されたタグに追加されます。
  >
  >1. タグは、コンテンツ（参照が含まれている）で使用されます。または
  >1. タグが、既に移動した子を持っています。

* `cq:backlinks` は、参照を他の方向に保持します。 つまり、タグ B に移動または結合されたすべてのタグのリストを保持します。これは、主にタグ B の保持に必要です `cq:movedTo` タグ B が移動、結合、削除されたとき、またはタグ B がアクティブになったときに、それまでのプロパティ。この場合、すべての逆リンクタグもアクティブにする必要があります。

  >[!NOTE]
  >
  >`cq:backlinks` プロパティは、次のいずれかの条件を満たす場合にのみ、移動または統合されたタグに追加されます。
  >
  >1. タグがコンテンツ（参照を持つ）で使用されている OR
  >1. タグが、既に移動した子を持っています。

* コンテンツノードの `cq:tags` プロパティを読み取る場合は、次のように解決されます。

   1. `/content/cq:tags` 下で一致するものが見つからない場合、タグは返されません。

   1. タグに `cq:movedTo` プロパティが設定されている場合は、参照先のタグ ID が使用されます。

      * これは、その次のタグに `cq:movedTo` プロパティがある限り繰り返されます。

   1. 次のタグに `cq:movedTo` プロパティがない場合は、そのタグが読み取られます。

* タグを移動または結合したときに変更を発行するには、`cq:Tag` ノードとそのすべてのバックリンクを複製する必要があります。これは、タグ管理コンソールでタグがアクティブにされたときに自動的に行われます。

* 後でページの `cq:tags` プロパティは、古い参照を自動的にクリーンアップします。 移動したタグを API で解決すると移動先のタグが戻され、移動先のタグ ID が提供されることから、この処理がトリガーされます。

>[!NOTE]
>
>タグの移動は、タグの移行とは異なります。

## タグの移行 {#tags-migration}

Adobe Experience Manager 6.4 以降、タグは `/content/cq:tags` 以前のバージョンではタグは次の場所に保存されていました： `/etc/tags`.

6.4 より前のバージョンからAEMシステムをアップグレードする場合は、タグをに移行する必要があります。 `/content/cq:tags`. ドキュメントを参照してください [AEM 6.5 における一般的なリポジトリの再構築](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags) を参照してください。
