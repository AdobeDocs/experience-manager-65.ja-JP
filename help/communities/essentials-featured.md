---
title: おすすめコンテンツの基本事項
description: コミュニティサイト内の任意の場所でハイライト表示したい注目コンテンツを操作する基本について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 70b0ad6a-c891-4588-8515-449aed206805
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
source-wordcount: '122'
ht-degree: 10%
---
# おすすめコンテンツの基本事項  {#featured-content-essentials}

このページでは、おすすめコンテンツを操作するための重要な情報を提供します。

フォーラムの上部に投稿をピン留めするのとは対照的に、この機能を使用すると、コミュニティサイト内のどこでもコンテンツを強調表示できます。


## クライアントサイドの基本 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/コモンズ/コンポーネント/hbs/featuredcontent</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td> <i>default</i></td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/commons/components/hbs/featuredcontent/featuredcontent.hbs<br /> /libs/social/commons/components/hbs/featuredtopic/featuredtopic.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/featuredcontent/clientlibs/featuredcontent.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td><a href="featured.md">注目のコンテンツ </a>を参照</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

### ファイルライブラリ機能 {#file-library-function}

[おすすめコンテンツ関数](functions.md#featured-content-function)を含むコミュニティサイト構造には、設定済みの`featured content` コンポーネントが含まれています。
