---
title: コンテンツのアーキテクチャ
description: コンテンツをアーカイブするためのヒント（ヒント：すべてがコンテンツ）
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: bcebbdb4-20b9-4c2d-8a87-013549d686c1
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 45%

---

# コンテンツのアーキテクチャ{#content-architecture}

## David のモデルに従う {#follow-david-s-model}

David&#39;s Model は、数年前に David Nuescheler が書いたものですが、今日ではその考えが正しいと考えています。 David&#39;s Model の主な定義は次のとおりです。

* データが第一、構造は二の次（おそらくですが）。
* コンテンツ階層を推進し、実現させないでください。
* ワークスペース は `clone()`、`merge()`、`update()` のためのもの。
* 同じ名前の兄弟には注意が必要です。
* 参照は有害と見なされます。
* ファイルはファイルです。
* ID は有害。

David&#39;s Model は、Jackrabbit Wiki の [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### すべてがコンテンツです {#everything-is-content}

データベースなどの別々のサードパーティデータソースに依存するのではなく、すべてをリポジトリに保存する必要があります。 これは、作成したコンテンツ、画像、コード、設定などのバイナリデータに当てはまります。 これにより、1 つの API セットを使用してすべてのコンテンツを管理し、レプリケーションを通じてこのコンテンツのプロモーションを管理できます。 また、バックアップ、ログなどの単一のソースも得られます。

### 「コンテンツモデルが最初」のデザイン原則を使用 {#use-the-content-model-first-design-principle}

新機能をビルドするときには、常に JCR コンテンツ構造の設計から始め、次にデフォルトの Sling サーブレットを使用したコンテンツの読み込みおよび書き込みに進みます。これにより、標準のアクセス制御メカニズムで実装が適切に動作し、不要な CRUD スタイルのサーブレットが生成されるのを防ぐことができます。

### RESTful に準拠 {#be-restful}

サーブレットをパスではなく resourceType に基づいて定義する必要があります。このようにすると、JCR アクセス制御を使用し、REST 原則に準拠し、要求で提供されるリソースおよびリソースリゾルバーを使用できます。また、これにより、サーバーサイドで URL をレンダリングするスクリプトを変更でき（クライアントサイドから URL を変更する必要がありません）、サーバーサイドの実装をクライアントに対して非表示にすることでセキュリティを強化します。

### 新しいノードタイプの定義を回避 {#avoid-defining-new-node-types}

ノードタイプはインフラストラクチャレイヤー内の下位レベルで機能し、ほとんどの要件は nt:unstructured、oak:Unstructured、sling:Folder または cq:Page のノードタイプに割り当てられた sling:resourceType を使用することで満たすことができます。ノードタイプはリポジトリ内のスキーマと同じで、ノードタイプの変更は将来的に高価になる場合があります。

### JCR の命名規則に準拠 {#adhere-to-naming-conventions-in-the-jcr}

命名規則に従うと、コードベースの一貫性が向上し、不具合の発生率が低下し、システムで作業する開発者の速度が向上します。 AEM の開発においてアドビが使用した規則は次のとおりです。

* ノード名

   * すべて小文字
   * ハイフンを使用した単語の分離

* プロパティ名

   * キャメルケース（小文字で開始）

* コンポーネント (JSP/HTML)

   * すべて小文字
   * ハイフンを使用した単語の分離
