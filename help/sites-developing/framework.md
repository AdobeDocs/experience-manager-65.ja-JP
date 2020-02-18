---
title: AEM タグ付けフレームワーク
seo-title: AEM タグ付けフレームワーク
description: コンテンツへのタグ付けと AEM タグ付けインフラストラクチャの利用
seo-description: コンテンツへのタグ付けと AEM タグ付けインフラストラクチャの利用
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# AEM タグ付けフレームワーク{#aem-tagging-framework}

コンテンツにタグ付けし、AEM タグ付けインフラストラクチャを利用するには：

* タグは、` [cq:Tag](#tags-cq-tag-node-type)` タイプのノードとして、[分類のルートノード](#taxonomy-root-node)の下に存在する必要があります。

* タグ付けされたコンテンツノードのノードタイプには、[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin が含まれている必要があります。
* The [TagID](#tagid) is added to the content node&#39;s [ `cq:tags`](#tagged-content-cq-tags-property) property and resolves to a node of type ` [cq:Tag](#tags-cq-tag-node-type)`

## タグ：cq:Tag ノードタイプ  {#tags-cq-tag-node-type}

The declaration of a tag is captured in the repository in a node of type `cq:Tag.`

タグは、単純な単語（sky など）にしたり、階層分類（包括的な fruit と具体的な apple の両方を意味する fruit/apple など）を表したりすることができます。

タグは一意のタグ ID によって識別されます。

タグには、タイトル、ローカライズされたタイトル、説明など、任意のメタ情報があります。タイトルは、TagIDが存在する場合は、ユーザーインターフェイスで表示する必要があります。

タグ付けフレームワークでは、作成者やサイト訪問者に、特定の事前定義されたタグだけを使用するよう制限を設けることもできます。

### タグの特徴 {#tag-characteristics}

* node type is `cq:Tag`
* node name is a component of the ` [TagID](#tagid)`
* the ` [TagID](#tagid)` always includes a [namespace](#tag-namespace)

* optional `jcr:title` property (the Title to display in the UI)

* optional `jcr:description` property

* 子ノードが含まれている場合、[コンテナタグ](#container-tags)と呼ばれます。
* [分類のルートノード](#taxonomy-root-node)と呼ばれる基本パスの下のリポジトリに保存されます。

### タグ ID {#tagid}

タグ ID は、リポジトリ内のタグノードに解決されるパスを識別します。

Typically, the TagID is a shorthand TagID starting with the namespace or it can be an absolute TagID starting from the [taxonomy root node](#taxonomy-root-node).

コンテンツにタグ付けするときに、コンテンツがまだ存在しない場合は、` [cq:tags](#tagged-content-cq-tags-property)` プロパティがコンテンツノードに追加され、タグ ID がこのプロパティの String 配列値に追加されます。

タグ ID は、[名前空間](#tag-namespace)とそれに続くローカルタグ ID で構成されます。[コンテナタグ](#container-tags) には、分類内の階層順序を表すサブタグが含まれます。 サブタグは、ローカルのTagIDと同じタグを参照するために使用できます。 例えば、コンテンツが「fruit/apple」や「fruit/banana」などのサブタグを含むコンテナタグであっても、コンテンツに「fruit」とタグ付けすることができます。

### 分類のルートノード {#taxonomy-root-node}

分類のルートノードは、リポジトリ内にあるすべてのタグの基本パスです。The taxonomy root node must *not* be a node of type `  cq   :Tag`.

In AEM, the base path is `/content/  cq   :tags` and the root node is of type `  cq   :Folder`.

### タグの名前空間 {#tag-namespace}

名前空間を使用するとグループ化をおこなうことができます。最も一般的な使用例は、(Web)サイトごとに名前空間（例えば、パブリック、内部、ポータル）を持つか、大規模なアプリケーションごとに名前空間（例えば、WCM、アセット、コミュニティ）を持つことですが、その他の様々なニーズに対して名前空間を使用できます。 名前空間は、現在のコンテンツに適用されるタグ（特定の名前空間のタグ）のサブセットのみを表示するために、ユーザーインターフェイスで使用されます。

タグの名前空間は、分類サブツリーの最初のレベルです。これは、[分類のルートノード](#taxonomy-root-node)の直下のノードです。A namespace is a node of type `cq:Tag` whose parent is not a `cq:Tag`node type.

すべてのタグには名前空間があります。名前空間が指定されていない場合、タグはデフォルトの名前空間であるTagIDに割り当て `default` られます(タ `Standard Tags),`イトルは `/content/cq:tags/default.`

### コンテナタグ {#container-tags}

コンテナタグは、任意の数およびタイプの子ノードを含む、`cq:Tag` タイプのノードです。これにより、カスタムメタデータを使用してタグモデルを強化できます。

さらに、コンテナタグ（またはスーパータグ）は分類において、すべてのサブタグの小計としての機能を果たします。例えば fruit/apple でタグ付けされたコンテンツは、fruit でタグ付けされたとも見なされます。つまり、fruit でタグ付けされたコンテンツを検索すると、fruit/apple でタグ付けされたコンテンツも検索されます。

### タグ ID の解決 {#resolving-tagids}

タグ ID にコロン「:」が含まれている場合、そのコロンによってタグやサブ分類から名前空間が区別され、その後、タグやサブ分類は通常のスラッシュ「/」で区別されます。タグ ID にコロンが含まれていない場合は、デフォルトの名前空間が暗示されます。

タグの標準的で唯一の場所は/content/cq:tagsの下です。

cq:Tagノードを指していない、既存でないパスまたはパスを参照するタグは無効と見なされ、無視されます。

次の表に、タグ ID の例とその要素、リポジトリでそのタグ ID がどのように絶対パスに解決されるかを示します。

次の表に、サンプルのTagIDとその要素、およびTagIDがリポジトリ内の絶対パスに解決される方法を示します。次の表に、サンプルのTagIDとその要素、およびTagIDがリポジトリ内の絶対パスに解決される方法を示します。

<table>
 <tbody>
  <tr>
   <td><strong>タグ ID<br /> </strong></td>
   <td><strong>名前空間</strong></td>
   <td><strong>ローカルID</strong></td>
   <td><strong>コンテナタグ</strong></td>
   <td><strong>リーフタグ</strong></td>
   <td><strong>Repository<br /> Absoluteタグのパス</strong></td>
  </tr>
  <tr>
   <td>dam:fruit/apple/braeburn</td>
   <td>dam</td>
   <td>fruit/apple/braeburn</td>
   <td>果物，リンゴ</td>
   <td>焼き網</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>カラー/赤</td>
   <td>default</td>
   <td>カラー/赤</td>
   <td>カラー</td>
   <td>red</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>空</td>
   <td>default</td>
   <td>空</td>
   <td>(なし)</td>
   <td>空</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>dam</td>
   <td>(なし)</td>
   <td>(なし)</td>
   <td>（なし、名前空間）</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>カテゴリ</td>
   <td>車</td>
   <td>車</td>
   <td>車</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### タグタイトルのローカリゼーション {#localization-of-tag-title}

When the tag includes the optional title string ( `jcr:title`) it is possible to localize the title for display by adding the property `jcr:title.<locale>`.

詳しくは、以下を参照してください。

* [他の言語でのタグ](/help/sites-developing/building.md#tags-in-different-languages) - API の使用について説明しています。
* [他の言語でのタグの管理](/help/sites-administering/tags.md#managing-tags-in-different-languages) - タグ付けコンソールの使用について説明しています。

### アクセス制御 {#access-control}

タグは、リポジトリ内で[分類のルートノード](#taxonomy-root-node)の下にノードとして存在します。特定の名前空間で作成者とサイト訪問者がタグを作成できるようにするか、または拒否するには、リポジトリで適切なACLを設定します。

また、特定のタグまたは名前空間に対する読み取り権限を拒否することで、特定のコンテンツへのタグの適用を制御できます。

一般的な方法には以下のものがあります。

* Allowing the `tag-administrators` group/role write access to all namespaces (add/modify under `/content/cq:tags`). このグループは、追加設定なしで使用できる AEM に付属しています。

* 読み取り可能なすべての名前空間（ほとんどすべて）に対する読み取りアクセスをユーザー/作成者に許可します。
* ユーザー/作成者がタグを自由に定義できる名前空間への書き込みアクセスをユーザー/作成者に許可する(下のadd_node `/content/cq:tags/some_namespace`)

## タグ付け可能なコンテンツ：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

In order for application developers to attach tagging to a content type, the node&#39;s registration ([CND](https://jackrabbit.apache.org/node-type-notation.html)) must include the `cq:Taggable` mixin or the `cq:OwnerTaggable` mixin.

`cq:OwnerTaggable` mixin は `cq:Taggable` から継承されており、その目的は、所有者または作成者がコンテンツを分類できることを示すことです。In AEM, it is only an attribute of the `cq:PageContent` node. The `cq:OwnerTaggable` mixin is not required by the tagging framework.

>[!NOTE]
>
>集約されたコンテンツアイテムの最上位ノード（またはその jcr:content ノード）では、タグの有効化だけをおこなうことをお勧めします。次のような例があります。
>
>* ページ( `cq:Page`)です。ノ `jcr:content`ードのタイプはミ `cq:PageContent` ックスインが含ま `cq:Taggable` れます。
   >
   >
* アセット( `cq:Asset`)です。この場 `jcr:content/metadata` 合、ノードには常にミックスインが `cq:Taggable` あります。
>



### Node Type Notation (CND) {#node-type-notation-cnd}

ノードタイプの定義は、リポジトリ内に CND ファイルとして存在します。The CND notation is defined as part of the JCR documentation [here](https://jackrabbit.apache.org/node-type-notation.html).

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

`cq:tags` プロパティは、作成者またはサイト訪問者によってコンテンツに 1 つ以上のタグ ID が割り当てられたときにその ID を格納するための文字列配列です。The property only has meaning when added to a node which is defined with the ` [cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>To leverage AEM tagging functionality, custom developed applications should not define tag properties other than `cq:tags`.

## タグの移動と統合 {#moving-and-merging-tags}

次に、[タグ付けコンソール](/help/sites-administering/tags.md)を使用してタグの移動または統合を実行した場合のリポジトリ内での影響について説明します。

* When a tag A is moved or merged into tag B under `/content/cq:tags`:

   * tag A is not deleted and gets a `cq:movedTo` property.
   * タグBが作成され（移動の場合）、プロパティが取得され `cq:backlinks` ます。

* `cq:movedTo` は、タグBを指します。このプロパティは、タグAがタグBに移動または結合されたことを意味します。タグBを移動すると、それに応じてこのプロパティが更新されます。 タグ A は非表示になり、タグ A を示すコンテンツノード内のタグ ID を解決するリポジトリに保持されるだけになります。タグガベージコレクターは、タグ A のように、コンテンツノードで指定されなくなったタグを削除します。A special value for the `cq:movedTo` property is `nirvana`: it is applied when the tag is deleted but cannot be removed from the repository because there are subtags with a `cq:movedTo` that must be kept.

   >[!NOTE]
   >
   >次のい `cq:movedTo` ずれかの条件を満たしている場合にのみ、プロパティが移動されたタグまたは結合されたタグに追加されます。
   > 1. タグがコンテンツで使用されている（参照が含まれている）。OR
   > 1. タグには既に移動された子が含まれています。


* `cq:backlinks` は、参照を別の方向に保持します。つまり、タグBに移動または結合されたすべてのタグのリストを保持します。これは、タグBが移動、結合、 `cq:movedTo`削除されたとき、またはタグBがアクティブなときに、プロパティを最新の状態に保つために必要な場合に、そのすべてのバックリンクタグもアクティブにする必要があります。

   >[!NOTE]
   >
   >次のい `cq:backlinks` ずれかの条件を満たしている場合にのみ、プロパティが移動されたタグまたは結合されたタグに追加されます。
   > 1. タグがコンテンツで使用されている（参照が含まれている）。OR
   > 1. タグには既に移動された子が含まれています。


* コンテンツノードの `cq:tags` プロパティを読み取ると、以下のように解決されます。

   1. の下に一致がない場合、タ `/content/cq:tags`グは返されません。
   1. タグにプロパティが設定さ `cq:movedTo` れている場合は、参照先のタグIDが使用されます。
これは、その次のタグに `cq:movedTo` プロパティがある限り繰り返されます。

   1. 次のタグに `cq:movedTo` プロパティがない場合は、そのタグが読み取られます。

* タグが移動またはマージされたときにその変更を発行するには、`cq:Tag` ノードとそのすべてのバックリンクを複製する必要があります。この処理は、タグ管理コンソールでタグがアクティベートされたときに自動的に実行されます。

* 後でページの `cq:tags` プロパティに対して更新がおこなわれると、「以前の」参照が自動的にクリーンアップされます。移動したタグを API で解決すると移動先のタグが戻され、移動先のタグ ID が提供されることから、この処理がトリガーされます。
