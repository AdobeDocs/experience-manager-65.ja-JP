---
title: リーダーボードの基本事項
description: Adobe Experience Manager Communitiesでリーダーボードコンポーネントを操作できるように、Communities スコアリングとバッジを設定する方法について説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 8%
---
# リーダーボードの基本事項 {#leaderboard-essentials}

このページでは、リーダーボード機能を操作するための重要な情報を提供します。

ページにリーダーボードコンポーネントを含める前に、[&#x200B; コミュニティのスコアリングとバッジ &#x200B;](implementing-scoring.md)を設定する必要があります。

[&#x200B; スコアリングとバッジの基本](configure-scoring.md)を参照してください。

## クライアントサイドの基本 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/gamification/コンポーネント/hbs/リーダーボード</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.gamification.hbs.leaderboard</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/leaderboard.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td><a href="enabling-leaderboard.md"> リーダーボード機能</a>を参照</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

### ファイルライブラリ機能 {#file-library-function}

[&#x200B; リーダーボード関数](functions.md#leaderboard-function)を含むコミュニティサイト構造には、設定済みの`leaderboard` コンポーネントが含まれています。
