---
title: ブログの基本事項
seo-title: Blog Essentials
description: ブログの概要
seo-description: Blog overview
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 61%

---

# ブログの基本事項 {#blog-essentials}

AEM 6.1 Communities 以降、ブログはコミュニティアクティビティとなります。 ブログ記事は、パブリッシュ環境から投稿されるようになりました。以前は、ブログ記事はオーサー環境でのみ作成し、公開できました。

権限を持つメンバーに制限されない限り、すべてのコミュニティメンバーがブログ記事を作成できるようになりました。

このページでは、ブログ機能の操作に関する基本情報をまとめています。

>[!NOTE]
>
>ブログ機能の基礎となるインフラストラクチャはジャーナル機能です。

## クライアント側の基本事項 {#essentials-for-client-side}

ブログ機能は 2 つの主要コンポーネントで構成されます。これらのコンポーネントは、[ブログ機能](/help/communities/functions.md#blog-function)を追加するか、オーサーインスタンスの編集モードでページに追加することによって使用可能になります。

### ブログ {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
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
| [**インクルード可能**](/help/communities/scf.md#add-or-include-a-communities-component) | いいえ |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **テンプレート** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **プロパティ** | 参照 [ブログ機能](/help/communities/blog-feature.md) |

* [クライアント側のカスタマイズ](/help/communities/client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [ブログ API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [ブログエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](/help/communities/server-customize.md)

### ブログ機能 {#blog-function}

を含むコミュニティサイト構造 [ブログ機能](/help/communities/functions.md#blog-function) は設定されます `Blog` および `Blog Sidebar` コンポーネント。 ブログ機能は、 [権限を持つメンバーユーザーグループ](/help/communities/users.md#privileged-members-group).

### ブログエントリ（UGC）へのアクセス {#accessing-blog-entries-ugc}

UGC は、標準モデレート方法のいずれかを使用してモデレートする必要があります。[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)を参照してください。

AEM 6.1 Communities 以降では、UGC の[共通ストア](/help/communities/working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

次のページを参照してください。

* [ストレージリソースプロバイダーの概要](/help/communities/srp.md) - 序論とリポジトリの使用方法の概要.
* [SRP と UGC の基本事項](/help/communities/srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP を使用した UGC へのアクセス](/help/communities/accessing-ugc-with-srp.md)  — コーディングのガイドライン。
* [SocialUtils のリファクタリング](/help/communities/socialutils.md) - 廃止されたユーティリティメソッドと現在の SRP ユーティリティメソッドの対応関係.

## プライマリパブリッシャー {#primary-publisher}

デプロイメントがパブリッシュファームである場合、公開予定の記事をポーリングするプライマリパブリッシャーを識別する必要があります。

詳しくは、[プライマリパブリッシャー](/help/communities/deploy-communities.md#primary-publisher)を参照してください。

## リッチメディアの許可 {#allowing-rich-media}

AEM プラットフォームでは、次に説明するように、XSS 攻撃を防止する目的でその他の Web サイトからのリンクがブロックされます。

* [クロスサイトスクリプティング（XSS）に対する保護](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

AEM 6.2 以降では、手動で行う必要があった変更がデフォルトの AntiSamy 設定ファイルに含まれています。

リッチメディアは、 `Embed Media from External Sites` アイコン：

![media](assets/media-icon.png)
