---
title: カレンダーの基本事項
seo-title: Calendar Essentials
description: カレンダー機能の概要
seo-description: Calendar feature overview
uuid: 14ff7a83-b2a7-4f7e-8ee7-88f336329a1a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 88932a3c-ba7f-47ba-9e0b-206755c2d42e
exl-id: 069e379d-c6fd-49ca-b337-df6fd466e023
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 66%

---

# カレンダーの基本事項 {#calendar-essentials}

このページでは、カレンダー機能の操作に関する基本情報をまとめています。

## クライアント側の基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendar/components/hbs/calendar</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td><a href="calendar.md">カレンダーの使用</a>を参照</td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [カレンダー API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [カレンダーエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### カレンダー機能 {#calendar-function}

を含むコミュニティサイト構造 [カレンダー関数](functions.md#calendar-function) 設定済み `calendar` コンポーネント。 カレンダー関数は、 [権限を持つメンバーユーザーグループ](users.md#privileged-members-group).

### カレンダー投稿（UGC）へのアクセス {#accessing-calendar-posts-ugc}

AEM 6.1 Communities 以降では、UGC の[共通ストア](working-with-srp.md)を使用する際に、選択されたストレージオプション（ASRP、MSRP、JSRP など）に関係なく、プログラムによって UGC にアクセスする必要があります。

**リポジトリ内の UGC の場所と形式は予告なく変更されることがあります**。

以下を参照してください。

* [ストレージリソースプロバイダーの概要](srp.md) - 序論とリポジトリの使用方法の概要
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングガイドライン
* [SocialUtils のリファクタリング](socialutils.md) - 廃止されたユーティリティメソッドと現在の SRP ユーティリティメソッドの対応関係
