---
title: Q&A の基本事項
description: 質問と回答フォーラムの機能
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 4%

---

# Q&amp;A の基本事項 {#qna-essentials}

このページでは、質問と回答 (Q&amp;A) フォーラム機能を使用する際の基本情報を提供します。

## クライアント側の基本事項 {#essentials-for-client-side}

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
   <td>詳しくは、 <a href="working-with-qna.md">Q&amp;A フォーラム機能</a></td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [Q&amp;A API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [Q&amp;A エンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### Q&amp;A 機能 {#qna-function}

を含むコミュニティサイト構造 [Q&amp;A 機能](functions.md#qna-function) が設定されている `QnA` モデレートとタグ付けに影響するコンポーネントおよび設定です。 Q&amp;A 機能は、 [権限を持つメンバーユーザーグループ](users.md#privileged-members-group).

### Q&amp;A フォーラム投稿 (UGC) へのアクセス {#accessing-qna-forum-posts-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
詳しくは、 [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

AEM 6.1 Communities 以降では、 [共通店](working-with-srp.md) UGC の場合は、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムで UGC にアクセスできます。

**リポジトリ内の UGC の場所と形式は、警告なしで変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダの概要](srp.md)  — の概要とリポジトリの使用の概要。
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン。
* [SocialUtils リファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします。
