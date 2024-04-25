---
title: アイディエーションの基本事項
description: Communities のアイディエーション機能を使用する際の基本を説明します。これは、フォーラムに似ていますが、より協調的な雰囲気があります。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ad3592b-f8b5-45c0-97bc-15f781d7b811
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 7%

---

# アイディエーションの基本事項 {#ideation-essentials}

このページでは、アイディエーション機能の操作に必要な情報を提供します。この機能はフォーラムに似ていますが、ドラフトとして保存でき、共同作業がしやすくなります。

## クライアントサイドの基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/ideation/components/hbs/ideation</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.voting<br /> cq.social.hbs.liking<br /> cq.social.hbs.ideation</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/ideation.hbs<br /> /libs/social/ideation/components/hbs/ideation/ideationlists.hbs<br /> /libs/social/ideation/components/hbs/ideation/composer.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/clientlibs/ideation.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>参照： <a href="ideation-feature.md">アイディエーション機能</a></td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

### アイディエーション機能 {#ideation-function}

を含むコミュニティサイト構造 [Ideation 関数](functions.md#ideation-function)、設定済みのを含む `ideation` コンポーネント。
