---
title: リーダーボードの基本事項
seo-title: Leaderboard Essentials
description: リーダーボード機能の概要
seo-description: Leaderboard feature overview
uuid: 815a6928-b147-496d-9751-13159ad1304d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7449f99e-77d7-4c0f-96d5-b67d5e1f124a
exl-id: fd1b1749-13f9-4079-ae39-348676105852
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 77%

---

# リーダーボードの基本事項 {#leaderboard-essentials}

このページでは、リーダーボード機能の操作に関する基本情報をまとめています。

ページにリーダーボードコンポーネントを含める前に、[コミュニティのスコアとバッジ](implementing-scoring.md)を設定する必要があります。

詳しくは、 [スコアとバッジの基本事項](configure-scoring.md).

## クライアント側の基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gamification/components/hbs/leaderboard</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.gamification.hbs.leaderboard</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/leaderboard.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>詳しくは、 <a href="enabling-leaderboard.md">リーダーボード機能</a></td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

### ファイルライブラリ機能 {#file-library-function}

を含むコミュニティサイト構造 [リーダーボード機能](functions.md#leaderboard-function)（設定済みを含む） `leaderboard` コンポーネント。
