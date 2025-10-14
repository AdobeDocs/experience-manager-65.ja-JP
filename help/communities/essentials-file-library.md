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
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong> 含む </strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br />cq.social.hbs.voting<br />cq.social.hbs.filelibrary</td>
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
   <td><a href="file-library.md"> ファイルライブラリ機能 </a> を参照してください。</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [&#x200B; ファイルライブラリ API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/filelibrary/client/api/package-summary.html)

* [&#x200B; ファイル ライブラリ エンドポイント &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/filelibrary/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### ファイルライブラリ機能 {#file-library-function}

[&#x200B; ファイルライブラリ関数 &#x200B;](functions.md#file-library-function) を含むコミュニティサイト構造には、設定済みの `file library` コンポーネントが含まれています。

### ファイルライブラリに投稿されたコメントへのアクセス （UGC） {#accessing-comments-posted-for-file-libraries-ugc}

UGC は、モデレートの標準的な方法の 1 つを使用してモデレートする必要があります。
[&#x200B; ユーザー生成コンテンツのモデレート &#x200B;](moderate-ugc.md) を参照してください。

AEM 6.1 Communities の時点では、UGC の [&#x200B; 共通ストア &#x200B;](working-with-srp.md) の使用には、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます。

**リポジトリ内の UGC の場所と形式は、警告なく変更される場合があります**。

以下を参照してください。

* [&#x200B; ストレージリソースプロバイダーの概要 &#x200B;](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRP と UGC の基本事項 &#x200B;](srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP による UGC へのアクセス &#x200B;](accessing-ugc-with-srp.md) - コーディングガイドライン。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
