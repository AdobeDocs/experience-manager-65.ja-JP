---
title: Q&A の基本事項
description: Adobe Experience Manager Communities の質問と回答（QnA）フォーラム機能を使用するための基本について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# Q&amp;A の基本事項 {#qna-essentials}

このページでは、QnA （Questions and Answers）フォーラム機能の操作に関する基本的な情報を提供します。

## クライアントサイドの基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>ソーシャル/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"> 次を含む </a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientlibs</a></td>
   <td>cq.ckeditor<br />cq.social.hbs.voting<br />cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> templates</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> properties</td>
   <td><a href="working-with-qna.md">Q&amp;A フォーラム機能 </a> 参照</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [QnA API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [QnA エンドポイント &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### Q&amp;A 機能 {#qna-function}

[QnA 関数 &#x200B;](functions.md#qna-function) を含むコミュニティサイト構造は、設定済みの `QnA` コンポーネントと、モデレートおよびタグ付けに影響する設定を持ちます。 QnA 関数は、[&#x200B; 特権メンバーユーザーグループ &#x200B;](users.md#privileged-members-group) の識別をサポートします。

### QnA フォーラム投稿へのアクセス （UGC） {#accessing-qna-forum-posts-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
[&#x200B; ユーザー作成コンテンツのモデレート &#x200B;](moderate-ugc.md) を参照してください。

AEM 6.1 Communities の時点では、UGC の [&#x200B; 共通ストア &#x200B;](working-with-srp.md) の使用には、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます。

**リポジトリ内の UGC の場所と形式は、警告なく変更される場合があります**。

以下を参照してください。

* [&#x200B; ストレージリソースプロバイダーの概要 &#x200B;](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRP と UGC の基本事項 &#x200B;](srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP による UGC へのアクセス &#x200B;](accessing-ugc-with-srp.md) - コーディングガイドライン。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
