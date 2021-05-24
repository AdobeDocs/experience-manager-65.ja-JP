---
title: コンテンツのアーキテクチャ
seo-title: コンテンツのアーキテクチャ
description: コンテンツのアーキテクチャに関するヒント（ヒント — すべてがコンテンツ）
seo-description: Adobe Experience Manager(AEM)でのコンテンツのアーキテクチャに関するヒントです。 （ヒント — すべてがコンテンツ）
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 58%

---

# コンテンツのアーキテクチャ{#content-architecture}

## David&#39;s Model に準拠 {#follow-david-s-model}

David&#39;s Model は何年も前に David Nuescheler によって作成されたものですが、その考え方は今でも当てはまります。David&#39;s Modelの主な定義は次のとおりです。

* データが最初に、構造が後になります。 多分。
* コンテンツ階層は手動で設計し、成り行き任せにしない。
* ワークスペースは`clone()`、`merge()`、`update()`用です。
* 同じ名前の兄弟に注意する。
* 参照は害が多いと考えられる。
* ファイルはあくまでもファイル。
* IDは悪い。

DavidのモデルはJackrabbit Wikiの[https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)にあります。

### すべてがコンテンツである {#everything-is-content}

あらゆるデータの格納には、データベースなど別個のサードパーティデータソースを利用するのではなく、リポジトリを使用する必要があります。このことは、作成済みコンテンツ、バイナリデータ（画像など）、コード、設定などに当てはまります。このようにすると、1 つの API セットを使用してすべてのコンテンツを管理でき、レプリケーションによってこのコンテンツのプロモーションを管理できます。また、バックアップやログの単一ソースを得ることができます。

### 「コンテンツモデルが第一」というデザインの原則の使用  {#use-the-content-model-first-design-principle}

新機能をビルドするときには、常に JCR コンテンツ構造の設計から始め、次にデフォルトの Sling サーブレットを使用したコンテンツの読み込みおよび書き込みに進みます。これにより、実装が標準のアクセス制御メカニズムで正常に動作し、不要なCRUDスタイルのサーブレットを生成するのを防ぐことができます。

### RESTful に準拠 {#be-restful}

サーブレットをパスではなく resourceType に基づいて定義する必要があります。これにより、JCRアクセス制御を使用し、REST原則に準拠し、リクエストでアドビに提供されるリソースおよびリソースリゾルバーを使用できます。 また、クライアント側からURLを変更する必要なく、サーバー側でURLをレンダリングするスクリプトを変更できます。また、セキュリティを強化するために、クライアント側の実装の詳細をクライアントから非表示にできます。

### 新しいノードタイプの定義を回避 {#avoid-defining-new-node-types}

ノードタイプはインフラストラクチャレイヤー内の下位レベルで機能し、ほとんどの要件は nt:unstructured、oak:Unstructured、sling:Folder または cq:Page のノードタイプに割り当てられた sling:resourceType を使用することで満たすことができます。ノードタイプはリポジトリ内のスキーマと同じで、ノードタイプの変更は最後に非常に高価になる場合があります。

### JCR の命名規則に準拠 {#adhere-to-naming-conventions-in-the-jcr}

命名規則に準拠することにより、コードベースの一貫性が高まるので、不具合の発生率を低下させ、システムで作業する開発者の生産性を高めることができます。AEMの開発では、次の規則をAdobeが使用します。

* ノード名

   * すべて小文字
   * 単語間の区切りにハイフンを使用

* プロパティ名

   * キャメルケース、小文字で開始

* コンポーネント（JSP/HTML）

   * すべて小文字
   * 単語間の区切りにハイフンを使用
