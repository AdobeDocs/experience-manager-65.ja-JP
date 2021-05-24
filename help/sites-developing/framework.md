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
feature: タグ付け
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 51%

---

# AEM タグ付けフレームワーク {#aem-tagging-framework}

コンテンツにタグ付けし、AEM タグ付けインフラストラクチャを利用するには：

* タグは、` [cq:Tag](#tags-cq-tag-node-type)` タイプのノードとして、[分類のルートノード](#taxonomy-root-node)の下に存在する必要があります。

* タグ付けされたコンテンツノードのノードタイプには、[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin が含まれている必要があります。
* [TagID](#tagid)がコンテンツノードの[ `cq:tags`](#tagged-content-cq-tags-property)プロパティに追加され、タイプ` [cq:Tag](#tags-cq-tag-node-type)`のノードに解決されます。

## タグ：cq:Tag ノードタイプ  {#tags-cq-tag-node-type}

タグの宣言は、リポジトリーにおける `cq:Tag.` タイプのノードにキャプチャされます。

タグは、単純な単語（sky など）にしたり、階層分類（包括的な fruit と具体的な apple の両方を意味する fruit/apple など）を表したりすることができます。

タグは一意のタグ ID によって識別されます。

タグには、タイトル、ローカライズされたタイトル、説明など、任意のメタ情報があります。タイトルは、TagIDではなく、ユーザーインターフェイスに表示されます。

タグ付けフレームワークでは、作成者やサイト訪問者に、特定の事前定義されたタグだけを使用するよう制限を設けることもできます。

### タグの特徴 {#tag-characteristics}

* ノードタイプは`cq:Tag`です。
* ノード名は、` [TagID](#tagid)`
* ` [TagID](#tagid)`には常に[名前空間](#tag-namespace)が含まれます

* オプションの`jcr:title`プロパティ（UIに表示するタイトル）

* オプションの`jcr:description`プロパティ

* 子ノードが含まれている場合、[コンテナタグ](#container-tags)と呼ばれます。
* [分類のルートノード](#taxonomy-root-node)と呼ばれる基本パスの下のリポジトリに保存されます。

### タグ ID {#tagid}

タグ ID は、リポジトリ内のタグノードに解決されるパスを識別します。

通常、タグIDは名前空間で始まる短縮形のタグIDです。または、[分類のルートノード](#taxonomy-root-node)から始まる絶対タグIDを使用できます。

コンテンツにタグ付けするときに、コンテンツがまだ存在しない場合は、` [cq:tags](#tagged-content-cq-tags-property)` プロパティがコンテンツノードに追加され、タグ ID がこのプロパティの String 配列値に追加されます。

タグ ID は、[名前空間](#tag-namespace)とそれに続くローカルタグ ID で構成されます。[コンテナタグ](#container-tags)にはサブタグがあり、これは分類における階層順序を表します。サブタグは、任意のローカルのTagIDと同じタグを参照するために使用できます。 例えば、「fruit/apple」や「fruit/banana」などのサブタグを含むコンテナタグであっても、「fruit」を含むコンテンツのタグ付けは許可されます。

### 分類のルートノード {#taxonomy-root-node}

分類のルートノードは、リポジトリー内にあるすべてのタグの基本パスです。分類のルートノードは、`  cq   :Tag` タイプのノードにすることが&#x200B;*できません*。

AEM の基本パスは `/content/  cq   :tags` であり、ルートノードのタイプは `  cq   :Folder` です。

### タグの名前空間 {#tag-namespace}

名前空間を使用するとグループ化をおこなうことができます。最も一般的な使用例は、(Web)サイトごと（公開、内部、ポータルなど）または大規模なアプリケーションごと（WCM、アセット、コミュニティなど）に名前空間を持つことですが、他の様々なニーズに使用できます。 名前空間は、現在のコンテンツに適用できるタグのサブセット（特定の名前空間のタグなど）のみを表示するために、ユーザーインターフェイスで使用されます。

タグの名前空間は、分類サブツリーの最初のレベルです。これは、[分類のルートノード](#taxonomy-root-node)の直下のノードです。の直下のノードです。名前空間は `cq:Tag` タイプのノードで、その親は `cq:Tag` ノードタイプではありません。

すべてのタグには名前空間があります。名前空間が指定されていない場合、タグはデフォルトの名前空間(タグID `default` （タイトルは`Standard Tags),`、`/content/cq:tags/default.`）に割り当てられます

### コンテナタグ {#container-tags}

コンテナタグは、任意の数およびタイプの子ノードを含む、`cq:Tag` タイプのノードです。これにより、カスタムメタデータを使用してタグモデルを強化できます。

さらに、コンテナタグ（またはスーパータグ）は分類において、すべてのサブタグの小計としての機能を果たします。例えば fruit/apple でタグ付けされたコンテンツは、fruit でタグ付けされたとも見なされます。つまり、fruit でタグ付けされたコンテンツを検索すると、fruit/apple でタグ付けされたコンテンツも検索されます。

### タグ ID の解決 {#resolving-tagids}

タグ ID にコロン「:」が含まれている場合、そのコロンによってタグやサブ分類から名前空間が区別され、その後、タグやサブ分類は通常のスラッシュ「/」で区別されます。タグ ID にコロンが含まれていない場合は、デフォルトの名前空間が暗示されます。

タグの標準の場所は/content/cq:tagsの下のみです。

存在しないパスまたはcq:Tagノードを指さないパスを参照するタグは、無効と見なされ、無視されます。

次の表に、タグ ID の例とその要素、リポジトリでそのタグ ID がどのように絶対パスに解決されるかを示します。

次の表に、タグIDの例とその要素、およびリポジトリ内の絶対パスに解決されるタグIDの例を示します。
次の表に、タグIDの例とその要素、およびリポジトリ内の絶対パスに解決されるタグIDの例を示します。

<table>
 <tbody>
  <tr>
   <td><strong>タグ ID<br /> </strong></td>
   <td><strong>名前空間</strong></td>
   <td><strong>ローカル ID</strong></td>
   <td><strong>コンテナタグ</strong></td>
   <td><strong>リーフタグ</strong></td>
   <td><strong>リポジトリ<br />タグの絶対パス</strong></td>
  </tr>
  <tr>
   <td>dam:fruit/apple/braeburn</td>
   <td>dam</td>
   <td>fruit/apple/braeburn</td>
   <td>果物、リンゴ</td>
   <td>脳火傷</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>色/赤</td>
   <td>default</td>
   <td>色/赤</td>
   <td>カラー</td>
   <td>red</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>空</td>
   <td>default</td>
   <td>空</td>
   <td>（なし）</td>
   <td>空</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>dam</td>
   <td>（なし）</td>
   <td>（なし）</td>
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

タグにオプションのタイトル文字列( `jcr:title` )が含まれている場合は、プロパティ`jcr:title.<locale>`を追加することで、表示するタイトルをローカライズできます。

詳しくは、以下を参照してください。

* [他の言語でのタグ](/help/sites-developing/building.md#tags-in-different-languages) - API の使用について説明しています。
* [他の言語でのタグの管理](/help/sites-administering/tags.md#managing-tags-in-different-languages) - タグ付けコンソールの使用について説明しています。

### アクセス制御 {#access-control}

タグは、リポジトリ内で[分類のルートノード](#taxonomy-root-node)の下にノードとして存在します。作成者やサイト訪問者が特定の名前空間でタグを作成するのを許可または拒否するには、リポジトリで適切なACLを設定します。

また、特定のタグまたは名前空間に対する読み取り権限を拒否することで、特定のコンテンツへのタグの適用を制御できます。

一般的な方法には次のものがあります。

* すべての名前空間への書き込みアクセス（`/content/cq:tags` 下への add／modify）を`tag-administrators` グループ／役割に許可する。このグループは、追加設定なしで使用できる AEM に付属しています。

* 読み取り可能にする必要があるすべての名前空間への読み取りアクセスをユーザー／作成者に許可する。
* ユーザー/作成者が、タグを自由に定義できる名前空間（`/content/cq:tags/some_namespace`の下のadd_node）への書き込みアクセスを許可する

## タグ付け可能なコンテンツ：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

アプリケーション開発者がコンテンツタイプにタグ付けを付加するには、ノードの登録（[CND](https://jackrabbit.apache.org/node-type-notation.html)）に `cq:Taggable` Mixin または `cq:OwnerTaggable` Mixin を含める必要があります。

`cq:OwnerTaggable` Mixin は `cq:Taggable` から継承されており、その目的は、所有者または作成者がコンテンツを分類できることを示すことです。AEM では、`cq:PageContent` ノードの属性にすぎません。`cq:OwnerTaggable` Mixin は、タグ付けフレームワークには必要ありません。

>[!NOTE]
>
>集約されたコンテンツアイテムの最上位ノード（またはその jcr:content ノード）では、タグの有効化だけをおこなうことをお勧めします。以下に例を示します。
>
>* ページ( `cq:Page` )。`jcr:content`ノードのタイプは`cq:PageContent`で、`cq:Taggable` mixinが含まれます。
   >
   >
* アセット( `cq:Asset` )で、`jcr:content/metadata`ノードには常に`cq:Taggable` mixinが含まれます。

>



### ノードタイプの表記（CND） {#node-type-notation-cnd}

ノードタイプの定義は、リポジトリー内に CND ファイルとして存在します。CND表記は、JCRドキュメント[ここ](https://jackrabbit.apache.org/node-type-notation.html)の一部として定義されます。

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

`cq:tags` プロパティは、作成者またはサイト訪問者によってコンテンツに 1 つ以上のタグ ID が割り当てられたときにその ID を格納するための文字列配列です。このプロパティは、`[cq:Taggable](#taggable-content-cq-taggable-mixin)` Mixin で定義されているノードに追加した場合にのみ意味があります。

>[!NOTE]
>
>AEM のタグ付け機能を使用するには、カスタムで開発されたアプリケーションで `cq:tags` 以外のタグプロパティを定義しないでください。

## タグの移動と統合 {#moving-and-merging-tags}

次に、[タグ付けコンソール](/help/sites-administering/tags.md)を使用してタグの移動または統合を実行した場合のリポジトリ内での影響について説明します。

* タグAが`/content/cq:tags`の下のタグBに移動または結合されたとき：

   * タグAは削除されず、`cq:movedTo`プロパティを取得します。
   * タグBが作成され（移動の場合）、`cq:backlinks`プロパティが取得されます。

* `cq:movedTo` がタグBを指している。このプロパティは、タグAがタグBに移動または結合されたことを意味する。タグBを移動すると、それに応じてこのプロパティが更新される。タグ A は非表示になり、タグ A を示すコンテンツノード内のタグ ID を解決するリポジトリに保持されるだけになります。タグガベージコレクターは、タグ A のように、コンテンツノードで指定されなくなったタグを削除します。`cq:movedTo`プロパティの特別な値は`nirvana`です。タグが削除された場合に適用されますが、保持する必要がある`cq:movedTo`を含むサブタグがあるので、リポジトリから削除できません。

   >[!NOTE]
   >
   >`cq:movedTo` プロパティは、次のいずれかの条件を満たす場合にのみ、移動または結合されたタグに追加されます。
   > 1. タグは、コンテンツ（参照を含む）で使用されます。または
   > 1. タグに、既に移動済みの子が含まれています。


* `cq:backlinks` は、他の方向への参照を保持します。つまり、タグBに移動またはタグBと結合されたすべてのタグのリストを保持します。これは、タグBの移動/結合/削除時やタグBの有効化時に、プロパティを最新に保つためにほとんど必要で `cq:movedTo`す。

   >[!NOTE]
   >
   >`cq:backlinks` プロパティは、次のいずれかの条件を満たす場合にのみ、移動または結合されたタグに追加されます。
   >
   > 1. タグは、コンテンツ（参照を含む）で使用されます。または    >
   > 1. タグに、既に移動済みの子が含まれています。


* コンテンツノードの `cq:tags` プロパティを読み取ると、以下のように解決されます。

   1. `/content/cq:tags` 下で一致するものが見つからない場合、タグは返されません。
   1. タグに `cq:movedTo` プロパティが設定されている場合は、参照先のタグ ID が使用されます。これは、その次のタグに `cq:movedTo` プロパティがある限り繰り返されます。

   1. 次のタグに `cq:movedTo` プロパティがない場合は、そのタグが読み取られます。

* タグが移動またはマージされたときにその変更を発行するには、`cq:Tag` ノードとそのすべてのバックリンクを複製する必要があります。この処理は、タグ管理コンソールでタグがアクティベートされたときに自動的に実行されます。

* 後でページの `cq:tags` プロパティに対して更新がおこなわれると、「以前の」参照が自動的にクリーンアップされます。移動したタグを API で解決すると移動先のタグが戻され、移動先のタグ ID が提供されることから、この処理がトリガーされます。

>[!NOTE]
>
>タグの移動は、タグの移行とは異なります。

## タグの移行{#tags-migration}

Experience Manager6.4以降のタグは`/content/cq:tags`に格納され、以前は`/etc/tags`に格納されていました。 ただし、Adobe Experience Managerが以前のバージョンからアップグレードされた場合、タグは古い場所`/etc/tags`の下に残ります。 アップグレードしたシステムでは、タグは`/content/cq:tags`の下に移行する必要があります。

>[!NOTE]
>
>タグのページプロパティページでは、タグのベースパス（例：`/etc/tags/geometrixx-outdoors/activity/biking`）をハードコーディングする代わりに、タグID(`geometrixx-outdoors:activity/biking`)を使用することをお勧めします。
>
>タグのリストを表示するには、`com.day.cq.tagging.servlets.TagListServlet`を使用できます。

>[!NOTE]
>
>タグマネージャーAPIをリソースとして使用することをお勧めします。

### アップグレードされたAEMインスタンスがTagManager API {#upgraded-instance-support-tagmanager-api}をサポートしている場合

1. コンポーネントの開始時に、TagManager APIは、コンポーネントがアップグレードされたAEMインスタンスであるかどうかを検出します。 アップグレードされたシステムでは、タグは`/etc/tags`に保存されます。

1. 次に、TagManager APIは下位互換モードで実行されます。つまり、APIはベースパスとして`/etc/tags`を使用します。 そうでない場合は、新しい場所`/content/cq:tags`を使用します。

1. タグの場所を更新します。

1. 新しい場所にタグを移行した後、次のスクリプトを実行します。

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
  def tagPath = node.path;
  println "tag = ${tagPath}";

  if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags"))
    {
     def movedTo = node.getProperty("cq:movedTo").getValue().toString();

     println "cq:movedTo = ${movedTo} \n";

     movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
     node.setProperty("cq:movedTo",movedTo);
     } else if(node.hasProperty("cq:backlinks")){

     String[] backLinks = node.getProperty("cq:backlinks").getValues();
     int count = 0;

     backLinks.each { value ->
             if(value.startsWith("/etc/tags")){
                     println "cq:backlinks = ${value}\n";
                     backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
             count++;
     }

    node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

スクリプトは、`cq:movedTo/cq:backLinks`プロパティの値に`/etc/tags`が含まれるすべてのタグを取得します。 次に、取得された結果セットを繰り返し処理し、`cq:movedTo`と`cq:backlinks`のプロパティ値を`/content/cq:tags`パスに解決します（値で`/etc/tags`が検出された場合）。

### アップグレードされたAEMインスタンスがクラシックUIで動作する場合{#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>クラシックUIは、ダウンタイムなしに準拠しておらず、新しいタグベースパスをサポートしていません。 `/etc/tags`よりもクラシックUIを使用する場合は、`cq-tagging`コンポーネントを作成した後で再起動する必要があります。

TagManager APIでサポートされ、クラシックUIで実行されるアップグレード済みAEMインスタンスの場合：

1. 古いタグのベースパス`/etc/tags`への参照をtagIdまたは新しいタグの場所`/content/cq:tags`を使用して置き換えたら、CRXの新しい場所`/content/cq:tags`にタグを移行し、次にコンポーネントを再起動できます。

1. タグを新しい場所に移行した後、上記のスクリプトを実行します。
