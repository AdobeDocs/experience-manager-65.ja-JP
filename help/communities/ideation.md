---
title: アイディエーションの基本事項
description: コミュニティのアイデア出し機能を操作する際の基本について説明します。これはフォーラムに似ていますが、より協力的に操作できます。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ad3592b-f8b5-45c0-97bc-15f781d7b811
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
source-wordcount: '129'
ht-degree: 6%
---
# アイディエーションの基本事項 {#ideation-essentials}

このページでは、フォーラムに似ていますが、ドラフトとして保存でき、より協力的な感覚を持つアイデア出し機能を操作するための重要な情報を提供します。

## クライアントサイドの基本 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/アイデア創出/コンポーネント/hbs/アイデア創出</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.voting<br /> cq.social.hbs.liking<br /> cq.social.hbs.ideation</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/ideation.hbs<br /> /libs/social/ideation/components/hbs/ideation/ideationlists.hbs<br /> /libs/social/ideation/components/hbs/ideation/composer.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/clientlibs/ideation.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td><a href="ideation-feature.md"> アイデア出し機能</a>を参照</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

### アイディエーション機能 {#ideation-function}

[ アイデア出し関数](functions.md#ideation-function)を含むコミュニティサイト構造には、設定済みの`ideation` コンポーネントが含まれています。
