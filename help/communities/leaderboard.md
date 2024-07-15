---
title: リーダーボードの基本事項
description: Adobe Experience Manager Communities でリーダーボードコンポーネントを操作できるように、コミュニティのスコアとバッジを設定する方法について説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 8%

---

# リーダーボードの基本事項 {#leaderboard-essentials}

このページでは、リーダーボード機能の操作に関する重要な情報を提供します。

リーダーボードコンポーネントをページに含める前に、[ コミュニティのスコアとバッジ ](implementing-scoring.md) を設定する必要があります。

詳しくは [ スコアおよびバッジの基本事項 ](configure-scoring.md) を参照してください。

## クライアントサイドの基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/ゲーミフィケーション/コンポーネント/hbs/リーダーボード</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong> 含む </strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.gamification.hbs.leaderboard</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/leaderboard.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td><a href="enabling-leaderboard.md"> リーダーボード機能 </a> を参照してください。</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

### ファイルライブラリ機能 {#file-library-function}

[ リーダーボード関数 ](functions.md#leaderboard-function) を含むコミュニティサイト構造は、設定済みの `leaderboard` コンポーネントを含む。
