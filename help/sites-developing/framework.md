---
title: AEM タグ付けフレームワーク
seo-title: AEM Tagging Framework
description: コンテンツへのタグ付けと AEM タグ付けインフラストラクチャの利用
seo-description: Tag content and leverage the AEM Tagging infrastructure
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 4db9279f2d15f2e08939ba453ae8ddbbc3c3d69f
workflow-type: ht
source-wordcount: '1883'
ht-degree: 100%

---

# AEM タグ付けフレームワーク {#aem-tagging-framework}

コンテンツにタグ付けし、AEM タグ付けインフラストラクチャを利用するには：

* タグは、` [cq:Tag](#tags-cq-tag-node-type)` タイプのノードとして、[分類のルートノード](#taxonomy-root-node)の下に存在する必要があります。

* タグ付けされたコンテンツノードのノードタイプには、[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin が含まれている必要があります。
* [タグ ID](#tagid) がコンテンツノードの [ `cq:tags`](#tagged-content-cq-tags-property) プロパティに追加され、` [cq:Tag](#tags-cq-tag-node-type)` タイプのノードに解決されます。

## タグ：cq:Tag ノードタイプ  {#tags-cq-tag-node-type}

タグの宣言は、リポジトリーにおける `cq:Tag.` タイプのノードにキャプチャされます。

タグは、単純な単語（sky など）にしたり、階層分類（包括的な fruit と具体的な apple の両方を意味する fruit/apple など）を表したりすることができます。

タグは一意のタグ ID によって識別されます。

タグには、タイトル、ローカライズされたタイトル、説明など、任意のメタ情報があります。ユーザーインターフェイスには、タグ ID ではなくタイトル（存在する場合）が表示されます。

タグ付けフレームワークでは、作成者やサイト訪問者に、特定の事前定義されたタグだけを使用するよう制限を設けることもできます。

### タグの特徴 {#tag-characteristics}

* ノードタイプは `cq:Tag`
* ノード名は ` [TagID](#tagid)` のコンポーネント
* ` [TagID](#tagid)` には常に[名前空間](#tag-namespace)が含まれている

* オプションの `jcr:title` プロパティ（UI に表示されるタイトル）

* `jcr:description` プロパティ（オプション）

* 子ノードが含まれている場合、[コンテナタグ](#container-tags)と呼ばれます。
* [分類のルートノード](#taxonomy-root-node)と呼ばれる基本パスの下のリポジトリに保存されます。

### タグ ID {#tagid}

タグ ID は、リポジトリ内のタグノードに解決されるパスを識別します。

通常、タグ ID は名前空間で始まる短縮形のタグ ID ですが、[分類のルートノード](#taxonomy-root-node)から始まる絶対タグ ID にすることもできます。

コンテンツにタグ付けするときに、コンテンツがまだ存在しない場合は、` [cq:tags](#tagged-content-cq-tags-property)` プロパティがコンテンツノードに追加され、タグ ID がこのプロパティの文字列配列値に追加されます。

タグ ID は、[名前空間](#tag-namespace)とそれに続くローカルタグ ID で構成されます。[コンテナタグ](#container-tags)にはサブタグがあり、これは分類における階層順序を表します。サブタグは、任意のローカルタグ ID と同じタグを参照するのに使用できます。 例えば、「fruit」というタグが「fruit/apple」、「fruit/banana」などのサブタグを含むコンテナタグであっても、コンテンツにこのタグを付けることができます。

### 分類のルートノード {#taxonomy-root-node}

分類のルートノードは、リポジトリー内にあるすべてのタグの基本パスです。分類のルートノードは、`  cq   :Tag` タイプのノードにすることが&#x200B;*できません*。

AEM の基本パスは `/content/  cq   :tags` であり、ルートノードのタイプは `  cq   :Folder` です。

### タグの名前空間 {#tag-namespace}

名前空間を使用するとグループ化を行うことができます。（Web）サイトごと（例：公開、社内またはポータル）や大規模なアプリケーションごと（例：WCM、アセット、Communities）に名前空間を設けることが最も典型的なユースケースですが、その他の様々なニーズに名前空間を使用できます。 名前空間は、現在のコンテンツに適用されるタグのサブセット（つまり特定の名前空間のタグ）のみを表示するためにユーザーインターフェイスで使用されます。

タグの名前空間は、分類サブツリーの最初のレベルです。これは、[分類のルートノード](#taxonomy-root-node)の直下のノードです。名前空間は `cq:Tag` タイプのノードで、その親は `cq:Tag` ノードタイプではありません。

すべてのタグには名前空間があります。名前空間を指定しない場合、タグはデフォルトの名前空間であるタグ ID `default` に割り当てられます（タイトルは`Standard Tags),`つまり`/content/cq:tags/default.`

### コンテナタグ {#container-tags}

コンテナタグは、任意の数およびタイプの子ノードを含む、`cq:Tag` タイプのノードです。これにより、カスタムメタデータを使用してタグモデルを強化できます。

さらに、コンテナタグ（またはスーパータグ）は分類において、すべてのサブタグの小計としての機能を果たします。例えば fruit/apple でタグ付けされたコンテンツは、fruit でタグ付けされたとも見なされます。つまり、fruit でタグ付けされたコンテンツを検索すると、fruit/apple でタグ付けされたコンテンツも検索されます。

### タグ ID の解決 {#resolving-tagids}

タグ ID にコロン「:」が含まれている場合、そのコロンによってタグやサブ分類から名前空間が区別され、その後、タグやサブ分類は通常のスラッシュ「/」で区別されます。タグ ID にコロンが含まれていない場合は、デフォルトの名前空間が暗示されます。

タグの標準の場所は /content/cq:tags の下のみです。

存在しないパスまたは cq:Tag ノードを示していないパスを参照するタグは、無効と見なされて無視されます。

次の表に、タグ ID の例とその要素、リポジトリでそのタグ ID がどのように絶対パスに解決されるかを示します。

次の表に、タグ ID の例とその要素、リポジトリでそのタグ ID がどのように絶対パスに解決されるかを示します。

<table>
 <tbody>
  <tr>
   <td><strong>タグ ID<br /> </strong></td>
   <td><strong>名前空間</strong></td>
   <td><strong>ローカル ID</strong></td>
   <td><strong>コンテナタグ</strong></td>
   <td><strong>リーフタグ</strong></td>
   <td><strong>リポジトリ <br /> 絶対タグパス</strong></td>
  </tr>
  <tr>
   <td>dam:fruit/apple/braeburn</td>
   <td>DAM</td>
   <td>fruit/apple/braeburn</td>
   <td>fruit、apple</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>color/red</td>
   <td>default</td>
   <td>color/red</td>
   <td>color</td>
   <td>red</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>sky</td>
   <td>default</td>
   <td>sky</td>
   <td>（なし）</td>
   <td>sky</td>
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
   <td>category</td>
   <td>car</td>
   <td>car</td>
   <td>car</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### タグタイトルのローカリゼーション {#localization-of-tag-title}

タグにオプションのタイトル文字列（`jcr:title`）が含まれている場合は、プロパティ `jcr:title.<locale>` を追加することにより、表示するタイトルをローカライズすることができます。

詳しくは、以下を参照してください。

* [他の言語でのタグ](/help/sites-developing/building.md#tags-in-different-languages) - API の使用について説明しています。
* [他の言語でのタグの管理](/help/sites-administering/tags.md#managing-tags-in-different-languages) - タグ付けコンソールの使用について説明しています。

### アクセス制御 {#access-control}

タグは、リポジトリ内で[分類のルートノード](#taxonomy-root-node)の下にノードとして存在します。作成者やサイト訪問者に対し、特定の名前空間内でのタグの作成を許可または禁止するには、リポジトリに適切な ACL を設定してください。

また、特定のタグまたは名前空間に対する読み取り権限を拒否することで、特定のコンテンツへのタグの適用を制御できます。

一般的な方法には次のものがあります。

* すべての名前空間への書き込みアクセス（`/content/cq:tags` 下への add／modify）を`tag-administrators` グループ／役割に許可する。このグループは、追加設定なしで使用できる AEM に付属しています。

* 読み取り可能にする必要があるすべての名前空間への読み取りアクセスをユーザー／作成者に許可する。
* ユーザー／作成者がタグを自由に定義できる名前空間への書き込みアクセス（`/content/cq:tags/some_namespace` の下の add_node）をユーザー／作成者に許可する

## タグ付け可能なコンテンツ：cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

アプリケーション開発者がコンテンツタイプにタグ付けを付加するには、ノードの登録（[CND](https://jackrabbit.apache.org/node-type-notation.html)）に `cq:Taggable` Mixin または `cq:OwnerTaggable` Mixin を含める必要があります。

`cq:OwnerTaggable` Mixin は `cq:Taggable` から継承されており、その目的は、所有者または作成者がコンテンツを分類できることを示すことです。AEM では、`cq:PageContent` ノードの属性にすぎません。`cq:OwnerTaggable` Mixin は、タグ付けフレームワークには必要ありません。

>[!NOTE]
>
>集約されたコンテンツアイテムの最上位ノード（またはその jcr:content ノード）では、タグの有効化だけをおこなうことをお勧めします。以下に例を示します。
>
>* `jcr:content` ノードのタイプが `cq:PageContent` であるページ（`cq:Page`）。`cq:Taggable` Mixin が含まれています。
>
>* `jcr:content/metadata` ノードに常に `cq:Taggable` Mixin を持つアセット（`cq:Asset`）。
>


### ノードタイプの表記（CND） {#node-type-notation-cnd}

ノードタイプの定義は、リポジトリー内に CND ファイルとして存在します。CND 表記は、[こちら](https://jackrabbit.apache.org/node-type-notation.html)の JCR ドキュメントの一部として定義されています。

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

* タグ A を `/content/cq:tags` の下のタグ B に移動または統合した場合：

   * タグ A は削除されず、`cq:movedTo` プロパティを取得します。
   * タグ B が作成され（移動の場合）、`cq:backlinks` プロパティを取得します。

* `cq:movedTo` はタグ B を指します。
このプロパティは、タグ A がタグ B に移動または統合されたことを示します。タグ B を移動すると、このプロパティはそれに応じて更新されます。タグ A は非表示になり、タグ A を示すコンテンツノード内のタグ ID を解決するリポジトリに保持されるだけになります。タグガベージコレクターは、タグ A のように、コンテンツノードで指定されなくなったタグを削除します。
`cq:movedTo` プロパティの特殊な値に `nirvana` があります。この値は、タグが削除されたにもかかわらず、保持する必要のある `cq:movedTo` が含まれるサブタブが存在することが原因でそのタグをリポジトリから削除できない場合に適用されます。

   >[!NOTE]
   >
   >`cq:movedTo` プロパティは、次のいずれかの条件を満たす場合にのみ、移動または統合されたタグに追加されます。
   > 1. タグがコンテンツで使用されている（参照があることを意味します）または
   > 1. タグが、既に移動した子を持っています。


* `cq:backlinks` は他の方向への参照を保持します。つまり、タグ B に移動または統合されたすべてのタグのリストを保持します。これは主に、タグ B が移動、統合、削除された場合や、タグ B がアクティブになった場合に、`cq:movedTo` プロパティを最新の状態で保持するために必要です。この場合、すべてのバックリンクタグもアクティブにする必要があります。

   >[!NOTE]
   >
   >`cq:backlinks` プロパティは、次のいずれかの条件を満たす場合にのみ、移動または統合されたタグに追加されます。
   >
   > 1. タグがコンテンツで使用されている（参照があることを意味します）または >
   > 1. タグが、既に移動した子を持っています。


* コンテンツノードの `cq:tags` プロパティを読み取ると、以下のように解決されます。

   1. `/content/cq:tags` 下で一致するものが見つからない場合、タグは返されません。
   1. タグに `cq:movedTo` プロパティが設定されている場合は、参照先のタグ ID が使用されます。
これは、その次のタグに `cq:movedTo` プロパティがある限り繰り返されます。

   1. 次のタグに `cq:movedTo` プロパティがない場合は、そのタグが読み取られます。

* タグが移動または統合されたときにその変更を発行するには、`cq:Tag` ノードとそのすべてのバックリンクを複製する必要があります。この処理は、タグ管理コンソールでタグがアクティベートされたときに自動的に実行されます。

* 後でページの `cq:tags` プロパティに対して更新がおこなわれると、「以前の」参照が自動的にクリーンアップされます。移動したタグを API で解決すると移動先のタグが戻され、移動先のタグ ID が提供されることから、この処理がトリガーされます。

>[!NOTE]
>
>タグの移動は、タグの移行とは異なります。

## タグの移行 {#tags-migration}

Experience Manager 6.4 以降のタグは `/content/cq:tags` に格納されますが、以前は `/etc/tags` に格納されていました。ただし、Adobe Experience Manager が以前のバージョンからアップグレードされたシナリオでは、タグは古い場所 `/etc/tags` に引き続き存在します。アップグレードされたシステムでは、タグを `/content/cq:tags` の下に移行する必要があります。

>[!NOTE]
>
>タグページのページプロパティでは、タグのベースパス（例えば `/etc/tags/geometrixx-outdoors/activity/biking`）をハードコーディングする代わりに、タグ ID（`geometrixx-outdoors:activity/biking`）を使用することをお勧めします。
>
>タグを一覧表示するには、`com.day.cq.tagging.servlets.TagListServlet` を使用できます。

>[!NOTE]
>
>タグマネージャー API をリソースとして使用することをお勧めします。

### アップグレードされた AEM インスタンスが TagManager API をサポートしている場合 {#upgraded-instance-support-tagmanager-api}

1. コンポーネントの開始時に、TagManager API はアップグレードされた AEM インスタンスであるかどうかを検出します。アップグレードされたシステムでは、タグは `/etc/tags` 下に格納されます。

1. その後、TagManager API は後方互換モードで動作します。つまり、API はベースパスとして `/etc/tags` を使用します。そうでない場合は、新しい場所 `/content/cq:tags` を使用します。

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

スクリプトは、`cq:movedTo/cq:backLinks` プロパティの値に `/etc/tags` が含まれているタグをすべて取得します。その後、取得した結果セットを反復し、 `cq:movedTo` および `cq:backlinks` プロパティ値を `/content/cq:tags` パスに解決します（値に `/etc/tags` が検出された場合 ）。

### アップグレードされた AEM インスタンスがクラシック UI で動作する場合 {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>クラシック UI は、ダウンタイムなしに準拠しておらず、新しいタグのベースパスをサポートしていません。クラシック UI を使用する場合は、`/etc/tags` を作成し、その後に `cq-tagging` コンポーネントを再起動する必要があります。

TagManager API でサポートされ、クラシック UI で実行されているアップグレードされた AEM インスタンスの場合：

1. 古いタグのベースパス `/etc/tags` への参照が、タグ ID または新しいタグの場所 `/content/cq:tags` を使用して置き換えられると、CRX で新しい場所 `/content/cq:tags` にタグを移行し、その後にコンポーネントを再起動できます。

1. 新しい場所にタグを移行した後、上記のスクリプトを実行します。
