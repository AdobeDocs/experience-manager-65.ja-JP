---
title: コンテンツのアーキテクチャ
seo-title: Content Architecture
description: コンテンツをアーカイブするためのヒント（ヒント：すべてがコンテンツ）
seo-description: Tips for architecting your content in Adobe Experience Manager (AEM). (hint - everything is content)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 100%

---

# コンテンツのアーキテクチャ{#content-architecture}

## David&#39;s Model に準拠 {#follow-david-s-model}

David&#39;s Model は何年も前に David Nuescheler によって作成されたものですが、その考え方は今でも当てはまります。David モデルの主な考えは次のとおりです。

* データが第一、構造は二の次（おそらくですが）。
* コンテンツ階層は手動で設計し、成り行き任せにしない。
* ワークスペース は `clone()`、`merge()`、`update()` のためのもの。
* 同じ名前の兄弟に注意する。
* 参照は害が多いと考えられる。
* ファイルはあくまでもファイル。
* ID は有害。

David モデルについては、Jackrabbit wiki（[https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)）に詳しい解説があります。

### すべてがコンテンツである {#everything-is-content}

あらゆるデータの格納には、データベースなど別個のサードパーティデータソースを利用するのではなく、リポジトリを使用する必要があります。このことは、作成済みコンテンツ、バイナリデータ（画像など）、コード、設定などに当てはまります。このようにすると、1 つの API セットを使用してすべてのコンテンツを管理でき、レプリケーションによってこのコンテンツのプロモーションを管理できます。また、バックアップやログの単一ソースを得ることができます。

### 「コンテンツモデルが第一」というデザインの原則の使用 {#use-the-content-model-first-design-principle}

新機能をビルドするときには、常に JCR コンテンツ構造の設計から始め、次にデフォルトの Sling サーブレットを使用したコンテンツの読み込みおよび書き込みに進みます。これにより、初期設定済みのアクセス制御メカニズムで実装が正常に機能できることを確認したり、CRUD 形式の不要なサーブレットの生成を回避したりできます。

### RESTful に準拠 {#be-restful}

サーブレットをパスではなく resourceType に基づいて定義する必要があります。このようにすると、JCR アクセス制御を使用し、REST 原則に準拠し、要求で提供されるリソースおよびリソースリゾルバーを使用できます。また、これにより、サーバーサイドで URL をレンダリングするスクリプトを変更でき（クライアントサイドから URL を変更する必要がありません）、サーバーサイドの実装をクライアントに対して非表示にすることでセキュリティを強化します。

### 新しいノードタイプの定義を回避 {#avoid-defining-new-node-types}

ノードタイプはインフラストラクチャレイヤー内の下位レベルで機能し、ほとんどの要件は nt:unstructured、oak:Unstructured、sling:Folder または cq:Page のノードタイプに割り当てられた sling:resourceType を使用することで満たすことができます。ノードタイプはリポジトリではスキーマと同等で、ノードタイプを変更すると後で非常に高コストになる可能性があります。

### JCR の命名規則に準拠 {#adhere-to-naming-conventions-in-the-jcr}

命名規則に準拠することにより、コードベースの一貫性が高まるので、不具合の発生率を低下させ、システムで作業する開発者の生産性を高めることができます。AEM の開発においてアドビが使用した規則は次のとおりです。

* ノード名

   * すべて小文字
   * 単語間の区切りにハイフンを使用

* プロパティ名

   * キャメルケース、小文字で開始

* コンポーネント（JSP/HTML）

   * すべて小文字
   * 単語間の区切りにハイフンを使用
