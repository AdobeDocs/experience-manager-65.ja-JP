---
title: アイディエーションの基本事項
seo-title: アイディエーションの基本事項
description: アイディエーション機能の概要
seo-description: アイディエーション機能の概要
uuid: abaf03ee-8bf4-4241-96c3-474c95a30a88
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9e4f2f0-d1ff-40c0-abcf-645e40586a84
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 66%

---


# アイディエーションの基本事項 {#ideation-essentials}

このページでは、アイディエーション機能の操作に関する基本情報をまとめています。この機能は、フォーラムに似ていますが、ドラフトとして保存する機能があるほか、共同作業しやすくなります。

## クライアント側の基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/ideation/components/hbs/ideation</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>不可</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.voting<br /> cq.social.hbs.liking<br /> cq.social.hbs.ideation</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/ideation.hbs<br /> /libs/social/ideation/components/hbs/ideation/ideationlists.hbs<br /> /libs/social/ideation/components/hbs/ideation/composer.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/ideation/components/hbs/ideation/clientlibs/ideation.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>See <a href="ideation-feature.md">Ideation Feature</a></td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

### アイディエーション機能 {#ideation-function}

A community site structure that includes the [Ideation function](functions.md#ideation-function), includes a configured `ideation` component.
