---
title: ブログの基本事項
description: ログインしたコミュニティメンバーがブログ記事を投稿できるように、ブログ機能をページに追加する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# ブログの基本事項 {#blog-essentials}

AEM 6.1 Communities 以降、ブログはコミュニティアクティビティとなります。 ブログ記事は、パブリッシュ環境から投稿されるようになりました。以前は、ブログ記事はオーサー環境でのみ作成し、公開できました。

権限を持つメンバーに制限されない限り、すべてのコミュニティメンバーがブログ記事を作成できるようになりました。

このページでは、ブログ機能の操作に関する基本情報を提供します。

>[!NOTE]
>
>ブログ機能の基盤となるインフラストラクチャは、ジャーナル機能です。

## クライアント側の基本事項 {#essentials-for-client-side}

ブログ機能は、 [ブログ機能](/help/communities/functions.md#blog-function) または、オーサリング編集モードでコンポーネントをページに追加します。

### ブログ {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>参照 <a href="/help/communities/blog-feature.md">ブログ機能</a></td>
  </tr>
 </tbody>
</table>

### ブログのサイドバー {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**包含可能な**](/help/communities/scf.md#add-or-include-a-communities-component) | いいえ |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **テンプレート** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **プロパティ** | 参照 [ブログ機能](/help/communities/blog-feature.md) |

* [クライアント側のカスタマイズ](/help/communities/client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [ブログ API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [ブログエンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](/help/communities/server-customize.md)

### ブログ機能 {#blog-function}

を含むコミュニティサイト構造 [ブログ機能](/help/communities/functions.md#blog-function) 次に該当 `Blog` および `Blog Sidebar` 設定されたコンポーネント ブログ機能は、 [権限を持つメンバーユーザーグループ](/help/communities/users.md#privileged-members-group).

### ブログエントリ (UGC) へのアクセス {#accessing-blog-entries-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
詳しくは、 [ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md).

AEM 6.1 Communities 以降では、 [共通店](/help/communities/working-with-srp.md) UGC の場合は、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムで UGC にアクセスできます。

**リポジトリ内の UGC の場所と形式は、警告なしで変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダの概要](/help/communities/srp.md)  — の概要とリポジトリの使用の概要。
* [SRP と UGC の基本事項](/help/communities/srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP を使用した UGC へのアクセス](/help/communities/accessing-ugc-with-srp.md)  — コーディングのガイドライン。
* [SocialUtils のリファクタリング](/help/communities/socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします。

## プライマリ発行者 {#primary-publisher}

デプロイメントがパブリッシュファームの場合は、公開予定の記事をポーリングするプライマリパブリッシャーを特定する必要があります。

詳しくは、 [プライマリ発行者](/help/communities/deploy-communities.md#primary-publisher) を参照してください。

## リッチメディアの許可 {#allowing-rich-media}

AEMプラットフォームは、XSS 攻撃を防ぐために、他の Web サイトからのリンクをブロックします。詳しくは、

* [クロスサイトスクリプティング (XSS) に対するProtect](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

AEM 6.2 以降では、手動で行う必要があった変更がデフォルトの AntiSamy 設定ファイルに含まれています。

ブログ記事にリッチメディアを埋め込むには、 `Embed Media from External Sites` アイコン：

![media](assets/media-icon.png)
