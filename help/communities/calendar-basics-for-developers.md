---
title: カレンダーの基本事項
description: Experience Managerコミュニティでカレンダー機能を使用する方法を説明します。 カレンダーでは、権限を持つメンバーユーザーグループの識別がサポートされています。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 069e379d-c6fd-49ca-b337-df6fd466e023
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 4%

---

# カレンダーの基本事項 {#calendar-essentials}

このページでは、カレンダー機能の操作に関する重要な情報を提供します。

## クライアントサイドの基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/カレンダー/コンポーネント/hbs/カレンダー</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong> 含む </strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td><a href="calendar.md"> カレンダーの使用 </a> を参照してください。</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [ カレンダー API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [ カレンダーエンドポイント ](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### カレンダー機能 {#calendar-function}

[ カレンダー関数 ](functions.md#calendar-function) を含むコミュニティサイト構造には、`calendar` コンポーネントが設定されています。 カレンダー関数は、[ 特権メンバーユーザーグループ ](users.md#privileged-members-group) の識別をサポートしています。

### カレンダー投稿へのアクセス（UGC） {#accessing-calendar-posts-ugc}

AEM 6.1 Communities の時点では、UGC の [ 共通ストア ](working-with-srp.md) の使用には、選択したストレージオプション（ASRP、MSRP、JSRP など）に関係なく、UGC へのプログラムによるアクセスが含まれます。

**リポジトリ内の UGC の場所と形式は、警告なく変更される場合があります**。

以下を参照してください。

* [ ストレージリソースプロバイダーの概要 ](srp.md) – 概要とリポジトリの使用状況の概要
* [SRP と UGC の基本事項 ](srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [SRP による UGC へのアクセス ](accessing-ugc-with-srp.md) - コーディングガイドライン
* [SocialUtils リファクタリング ](socialutils.md) – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
