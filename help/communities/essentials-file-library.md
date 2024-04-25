---
title: ファイルライブラリの基本事項
description: Adobe Experience Manager Communities のファイルライブラリ機能の操作の基本について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6d653331-c1ce-4ccb-bb45-656b6413ac3e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 5%

---

# ファイルライブラリの基本事項 {#file-library-essentials}

このページでは、ファイル ライブラリ機能を使用するための基本的な情報を提供します。

## クライアントサイドの基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/filelibrary/components/hbs/filelibrary</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.filelibrary</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/filelibrary.hbs<br /> /libs/social/filelibrary/components/hbs/folder/folder.hbs<br /> /libs/social/filelibrary/components/hbs/folder/item.hbs<br /> /libs/social/filelibrary/components/hbs/document/document.hbs<br /> /libs/social/filelibrary/components/hbs/document/item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/clientlibs/filelibrary.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>参照： <a href="file-library.md">ファイルライブラリ機能</a></td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [ファイルライブラリ API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/filelibrary/client/api/package-summary.html)

* [ファイル ライブラリ エンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/filelibrary/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### ファイルライブラリ機能 {#file-library-function}

を含むコミュニティサイト構造 [ファイルライブラリ関数](functions.md#file-library-function)、設定済みのを含む `file library` コンポーネント。

### ファイルライブラリに投稿されたコメントへのアクセス （UGC） {#accessing-comments-posted-for-file-libraries-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
参照： [ユーザー生成コンテンツのモデレート](moderate-ugc.md).

AEM 6.1 Communities 現在、の使用 [共通店舗](working-with-srp.md) （UGC の場合、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます）。

**リポジトリ内の UGC の場所と形式は、警告なしに変更される場合があります**.

以下を参照してください。

* [ストレージリソースプロバイダーの概要](srp.md)  – 概要とリポジトリ使用状況の概要。
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRP による UGC へのアクセス](accessing-ugc-with-srp.md) - コーディングのガイドライン
* [SocialUtils のリファクタリング](socialutils.md)  – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする。
