---
title: リーダーボードの基本事項
seo-title: リーダーボードの基本事項
description: リーダーボード機能の概要
seo-description: リーダーボード機能の概要
uuid: 815a6928-b147-496d-9751-13159ad1304d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7449f99e-77d7-4c0f-96d5-b67d5e1f124a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# リーダーボードの基本事項 {#leaderboard-essentials}

このページでは、リーダーボード機能の操作に関する基本情報をまとめています。

リーダーボードコンポーネントをページに追加する前に、[コミュニティのスコアとバッジ](implementing-scoring.md)を設定する必要があります。See also [Scoring and Badges Essentials](configure-scoring.md).

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
   <td>See <a href="enabling-leaderboard.md">Leaderboard Feature</a></td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

### ファイルライブラリ機能 {#file-library-function}

A community site structure that includes the [Leaderboard function](functions.md#leaderboard-function), includes a configured `leaderboard` component.
