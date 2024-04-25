---
title: ブログの基本事項
description: ログインしたコミュニティメンバーがブログ記事を投稿できるように、ページにブログ機能を追加する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 4%

---

# ブログの基本事項 {#blog-essentials}

AEM 6.1 Communities の時点では、ブログはコミュニティアクティビティです。 ブログ記事はパブリッシュ環境から投稿されるようになりました。以前は、ブログ記事をオーサー環境で作成して公開することしかできませんでした。

ブログ記事は、権限のあるメンバーに制限されていない限り、任意のコミュニティメンバーが作成できるようになりました。

このページでは、ブログ機能を使用する際に必要な情報を提供します。

>[!NOTE]
>
>ブログ機能の基盤となるインフラストラクチャは、ジャーナル機能です。

## クライアントサイドの基本事項 {#essentials-for-client-side}

ブログ機能は、を追加することで利用できる 2 つの主要なコンポーネントで構成されています。 [ブログ関数](/help/communities/functions.md#blog-function) または、オーサー編集モードでページにコンポーネントを追加します。

### ブログ {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/ジャーナル/コンポーネント/hbs/ジャーナル</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>参照： <a href="/help/communities/blog-feature.md">ブログ機能</a></td>
  </tr>
 </tbody>
</table>

### ブログのサイドバー {#blog-sidebar}

| **resourceType** | ソーシャル/ジャーナル/コンポーネント/hbs/サイドバー |
|---|---|
| [**includable**](/help/communities/scf.md#add-or-include-a-communities-component) | いいえ |
| [**clientlibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **templates** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **プロパティ** | 参照： [ブログ機能](/help/communities/blog-feature.md) |

* [クライアントサイドのカスタマイズ](/help/communities/client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [ブログ API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [ブログエンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](/help/communities/server-customize.md)

### ブログ機能 {#blog-function}

を含むコミュニティサイト構造 [ブログ関数](/help/communities/functions.md#blog-function) が `Blog` および `Blog Sidebar` コンポーネントが設定されました。 ブログ関数は、 [特権メンバーユーザーグループ](/help/communities/users.md#privileged-members-group).

### ブログエントリへのアクセス（UGC） {#accessing-blog-entries-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
参照： [ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md).

AEM 6.1 Communities 現在、の使用 [共通店舗](/help/communities/working-with-srp.md) （UGC の場合、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます）。

**リポジトリ内の UGC の場所と形式は、警告なしに変更される場合があります**.

参照：

* [ストレージリソースプロバイダーの概要](/help/communities/srp.md)  – 概要とリポジトリ使用状況の概要。
* [SRP と UGC の基本事項](/help/communities/srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP による UGC へのアクセス](/help/communities/accessing-ugc-with-srp.md) - コーディングのガイドライン
* [SocialUtils のリファクタリング](/help/communities/socialutils.md)  – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする。

## プライマリ発行者 {#primary-publisher}

デプロイメントがパブリッシュファームであるとき、公開スケジュールされた記事をポーリングするプライマリ公開者を識別する必要があります。

参照： [プライマリ発行者](/help/communities/deploy-communities.md#primary-publisher) を参照してください。

## リッチメディアの許可 {#allowing-rich-media}

AEM プラットフォームでは、に示すように、XSS 攻撃を防ぐために他の web サイトからのリンクがブロックされます。

* [クロスサイトスクリプティング（XSS）に対する保護](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

AEM 6.2 では、以前に手動で行う必要があった変更が、デフォルトの AntiSamy 設定ファイルに含まれています。

リッチメディアをブログ記事に埋め込むには、 `Embed Media from External Sites` アイコン :

![media](assets/media-icon.png)
