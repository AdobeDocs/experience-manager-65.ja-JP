---
title: Q&A の基本事項
seo-title: Q&A の基本事項
description: フォーラム機能の質問および回答
seo-description: フォーラム機能の質問および回答
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
translation-type: tm+mt
source-git-commit: ca15258a5dc7ca99b6c9d6ae85e42c77a3802c87
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 56%

---


# Q&amp;A の基本事項 {#qna-essentials}

このページでは、Q&amp;A（質問および回答）フォーラム機能の操作に関する基本情報をまとめています。

## クライアント側の基本事項  {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">インクルード可能</a></td>
   <td>不可</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.qna</td>
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
   <td><a href="working-with-qna.md">Q&amp;Aフォーラム機能</a>を参照</td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項  {#essentials-for-server-side}

* [Q&amp;A API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [Q&amp;A エンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### Q&amp;A 機能  {#qna-function}

[QnA関数](functions.md#qna-function)を含むコミュニティサイト構造には、設定済みの`QnA`コンポーネントと、モデレートとタグに影響する設定が含まれます。 QnA関数は、[特権メンバー・ユーザー・グループ](users.md#privileged-members-group)の識別をサポートします。

### QnAフォーラム投稿(UGC)へのアクセス{#accessing-qna-forum-posts-ugc}

UGC は、標準モデレート方法のいずれかを使用してモデレートする必要があります。[ユーザー生成コンテンツのモデレート](moderate-ugc.md)を参照してください。

AEM 6.1 Communities 以降では、UGC の[共通ストア](working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

次のページを参照してください。

* [ストレージリソースプロバイダーの概要](srp.md) - 序論とリポジトリの使用方法の概要.
* [SRPとUGC Essentials](srp-and-ugc.md)  - SRPユーティリティのメソッドと例。
* [SRP](accessing-ugc-with-srp.md)  — コーディングガイドラインを使用したUGCへのアクセス
* [SocialUtils のリファクタリング](socialutils.md) - 廃止されたユーティリティメソッドと現在の SRP ユーティリティメソッドの対応関係.

