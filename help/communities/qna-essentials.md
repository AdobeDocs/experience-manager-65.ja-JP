---
title: Q&A の基本事項
description: Adobe Experience Manager Communitiesの質疑応答（QnA）フォーラム機能の操作の基本について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 3%
---
# Q&amp;A の基本事項 {#qna-essentials}

このページでは、質疑応答（QnA）フォーラム機能を操作するための重要な情報を提供します。

## クライアントサイドの基本 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">include</a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> テンプレート</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> properties</td>
   <td><a href="working-with-qna.md">Q&amp;A フォーラム機能</a>を参照してください</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの基本 {#essentials-for-server-side}

* [QnA API](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [QnA エンドポイント](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### Q&amp;A 機能 {#qna-function}

[QnA関数](functions.md#qna-function)を含むコミュニティサイト構造には、設定済みの`QnA` コンポーネントと、モデレーションとタグ付けに影響する設定が含まれています。 QnA関数は、[特権メンバーユーザーグループ &#x200B;](users.md#privileged-members-group)の識別をサポートしています。

### QnA フォーラム投稿へのアクセス（UGC） {#accessing-qna-forum-posts-ugc}

UGCは、モデレーションの標準的な方法のひとつを使用してモデレーションする必要があります。
[&#x200B; ユーザー生成コンテンツの管理](moderate-ugc.md)を参照してください。

AEM 6.1 Communitiesでは、UGC用の[common store](working-with-srp.md)を使用すると、選択したストレージオプション（ASRP、MSRP、JSRPなど）に関係なく、UGCにプログラムでアクセスできます。

**リポジトリ内のUGCの場所と形式は、警告なしで変更される可能性があります**。

以下を参照してください。

* [&#x200B; ストレージリソースプロバイダーの概要](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRPおよびUGC Essentials](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP](accessing-ugc-with-srp.md)を使用したUGCへのアクセス – コーディング ガイドライン。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) – 非推奨のユーティリティメソッドを現在のSRP ユーティリティメソッドにマッピングします。
