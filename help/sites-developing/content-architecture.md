---
title: コンテンツのアーキテクチャ
seo-title: コンテンツのアーキテクチャ
description: コンテンツの設計に関するヒント（ヒント — すべてがコンテンツ）
seo-description: Adobe Experience Manager(AEM)でのコンテンツの設計に関するヒントです。 （ヒント — すべてがコンテンツ）
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# コンテンツのアーキテクチャ{#content-architecture}

## David&#39;s Model に準拠 {#follow-david-s-model}

David&#39;s Model は何年も前に David Nuescheler によって作成されたものですが、その考え方は今でも当てはまります。Davidのモデルの主な特徴は次のとおりです。

* データが最初に来て、後で構造が始まります。 多分。
* コンテンツ階層は手動で設計し、成り行き任せにしない。
* ワークスペースは、、 `clone()`および `merge()`用で `update()`す。
* 同じ名前の兄弟に注意する。
* 参照は害が多いと考えられる。
* ファイルはあくまでもファイル。
* 身分証明書は悪い。

David’s Model can be found on the Jackrabbit wiki at [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### すべてがコンテンツである {#everything-is-content}

あらゆるデータの格納には、データベースなど別個のサードパーティデータソースを利用するのではなく、リポジトリを使用する必要があります。このことは、作成済みコンテンツ、バイナリデータ（画像など）、コード、設定などに当てはまります。このようにすると、1 つの API セットを使用してすべてのコンテンツを管理でき、レプリケーションによってこのコンテンツのプロモーションを管理できます。また、バックアップやログの単一ソースを得ることができます。

### 「コンテンツモデルが第一」というデザインの原則の使用 {#use-the-content-model-first-design-principle}

新機能をビルドするときには、常に JCR コンテンツ構造の設計から始め、次にデフォルトの Sling サーブレットを使用したコンテンツの読み込みおよび書き込みに進みます。これにより、お使いの実装が初期設定のアクセス制御メカニズムと適切に機能し、不要なCRUDスタイルのサーブレットを生成しないようにすることができます。

### RESTful に準拠 {#be-restful}

サーブレットをパスではなく resourceType に基づいて定義する必要があります。これにより、JCRアクセス制御を使用し、REST原則に従い、リクエストで提供されるリソースとリソースリゾルバーを使用することが可能になります。 また、クライアント側からURLを変更する必要なく、サーバー側でURLをレンダリングするスクリプトを変更できます。また、セキュリティを強化するために、クライアント側からサーバー側の実装の詳細を非表示にできます。

### 新しいノードタイプの定義を回避 {#avoid-defining-new-node-types}

ノードタイプはインフラストラクチャレイヤー内の下位レベルで機能し、ほとんどの要件は nt:unstructured、oak:Unstructured、sling:Folder または cq:Page のノードタイプに割り当てられた sling:resourceType を使用することで満たすことができます。ノードタイプはリポジトリ内のスキーマと同じで、ノードタイプの変更は将来的に非常に高コストになる可能性があります。

### JCR の命名規則に準拠 {#adhere-to-naming-conventions-in-the-jcr}

命名規則に準拠することにより、コードベースの一貫性が高まるので、不具合の発生率を低下させ、システムで作業する開発者の生産性を高めることができます。AEMの開発では、次の規則を使用します。

* ノード名

   * すべて小文字
   * 単語間の区切りにハイフンを使用

* プロパティ名

   * キャメルケース、小文字で開始

* コンポーネント（JSP/HTML）

   * すべて小文字
   * 単語間の区切りにハイフンを使用

