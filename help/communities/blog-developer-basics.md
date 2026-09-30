---
title: ブログの基本事項
description: ログインしているコミュニティ メンバーがブログ記事を投稿できるように、ブログ機能をページに追加する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 4%
---
# ブログの基本事項 {#blog-essentials}

AEM 6.1 Communitiesでは、ブログはコミュニティアクティビティです。 ブログ記事はパブリッシュ環境から投稿されるようになりました。以前は、ブログ記事はオーサー環境でのみ作成して公開していました。

特権付きメンバーに限定されない限り、コミュニティのメンバーがブログ記事を作成できるようになりました。

このページでは、ブログ機能を操作するための重要な情報を提供します。

>[!NOTE]
>
>ブログ機能の基盤となるインフラストラクチャは、ジャーナル機能です。

## クライアントサイドの基本 {#essentials-for-client-side}

ブログ機能は、[ ブログ関数](/help/communities/functions.md#blog-function)を追加するか、作成者編集モードでページにコンポーネントを追加することで使用できる2つの主要コンポーネントで構成されています。

### ブログ {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/ジャーナル/コンポーネント/hbs/ジャーナル</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包含可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td><a href="/help/communities/blog-feature.md"> ブログ機能</a>を参照</td>
  </tr>
 </tbody>
</table>

### ブログのサイドバー {#blog-sidebar}

| **resourceType** | ソーシャル/ジャーナル/コンポーネント/hbs/サイドバー |
|---|---|
| [**包含可能**](/help/communities/scf.md#add-or-include-a-communities-component) | いいえ |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **テンプレート** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **プロパティ** | [ ブログ機能](/help/communities/blog-feature.md)を参照 |

* [クライアントサイドのカスタマイズ](/help/communities/client-customize.md)

## サーバーサイドの基本 {#essentials-for-server-side}

* [ブログ API](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [ブログエンドポイント](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](/help/communities/server-customize.md)

### ブログ機能 {#blog-function}

[ ブログ関数](/help/communities/functions.md#blog-function)を含むコミュニティサイト構造には、`Blog`および`Blog Sidebar`個のコンポーネントが設定されています。 ブログ関数は、[特権メンバーユーザーグループ ](/help/communities/users.md#privileged-members-group)の識別をサポートしています。

### ブログエントリ（UGC）へのアクセス {#accessing-blog-entries-ugc}

UGCは、モデレーションの標準的な方法のひとつを使用してモデレーションする必要があります。
[ ユーザー生成コンテンツの管理](/help/communities/moderate-ugc.md)を参照してください。

AEM 6.1 Communitiesでは、UGC用の[common store](/help/communities/working-with-srp.md)を使用すると、選択したストレージオプション（ASRP、MSRP、JSRPなど）に関係なく、UGCにプログラムでアクセスできます。

**リポジトリ内のUGCの場所と形式は、警告なしで変更される可能性があります**。

を参照：

* [ ストレージリソースプロバイダーの概要](/help/communities/srp.md) – 概要とリポジトリの使用状況の概要。
* [SRPおよびUGC Essentials](/help/communities/srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP](/help/communities/accessing-ugc-with-srp.md)を使用したUGCへのアクセス – コーディング ガイドライン。
* [SocialUtils リファクタリング ](/help/communities/socialutils.md) – 非推奨のユーティリティメソッドを現在のSRP ユーティリティメソッドにマッピングします。

## プライマリ発行者 {#primary-publisher}

デプロイメントがパブリッシュファームの場合、パブリッシュがスケジュールされている記事をポーリングするプライマリパブリッシャーを特定する必要があります。

詳しくは、[プライマリパブリッシャー](/help/communities/deploy-communities.md#primary-publisher)を参照してください。

## リッチメディアの許可 {#allowing-rich-media}

AEM プラットフォームは、他のWeb サイトからのリンクをブロックして、の説明に従ってXSS攻撃を防ぎます

* [クロスサイトスクリプティング（XSS）に対する保護](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

AEM 6.2以降、以前は手動で行う必要があった変更は、デフォルトのAntiSamy設定ファイルに含まれています。

リッチメディアは、`Embed Media from External Sites` アイコンを選択してブログ記事に埋め込まれます。

![ メディア ](assets/media-icon.png)
