---
title: Dynamic Mediaの制限
description: 画像セットやスピンセットを作成したり、画像をアップロードしたりする際の、ベストプラクティスと適用される制限について説明します。PDF また、Dynamic Media Viewers でサポートされていない Web ブラウザーとオペレーティングシステムの組み合わせについても説明します。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
exl-id: e4d4059e-ac0b-42e7-910c-001310796574
source-git-commit: 098c52720d08ad294a745addb8bd3ca3f1c63b5c
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 4%

---

# Dynamic Mediaの制限

次の節では、Dynamic Mediaの制限について説明します。

このトピックには、次の節が含まれます。

* [アセットタイプに関するDynamic Mediaのベストプラクティスと適用される制限](#best-practice-enforced-limits)
* [Dynamic Media Viewers でサポートされていない Web ブラウザーとオペレーティングシステムの組み合わせ](#unsupported-browser-os)

## アセットタイプに関するDynamic Mediaのベストプラクティスと適用される制限 {#best-practice-enforced-limits}

Adobeでは、ページ抽出用にスピンセットや画像セットを作成したり、PDFをアップロードしたりする際に、次のベストプラクティスを推奨し、次の制限を適用します。

| アセット — 制限タイプ | ベストプラクティス | 制限が適用されました | 2022 年 12 月 31 日の制限に変更 |
| --- | --- | --- | --- |
| **画像**  — 画像あたりのスマート切り抜き数 | 5 | 100 | 20 |
| **すべてのセット**  — セットあたりの重複アセット数 | 重複なし | 20 | 適用なし |
| **すべてのセット**  — セットあたりの最大アセット数 | 1 セットあたり 5～10 個の画像 | 1000 | 適用なし |
| **スピンセット** - 2D セットあたりの最大行数/列数 | 1 セットあたり 12～18 個の画像 | 1000 | 適用なし |
| **PDF**  — 抽出対象となるPDFの最大ページ数 |  | 5000（新しいアップロード用） | 100( すべてのPDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Dynamic Media Viewers でサポートされていない Web ブラウザーとオペレーティングシステムの組み合わせ {#unsupported-browser-os}

Dynamic Mediaビューアでは、次の Web ブラウザーとオペレーティングシステムの組み合わせはサポートされていません。

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 の更新
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 ヨセミテ

## TLS 1.0 および 1.1 のサポート終了 {#tls}

<!-- CQDOC-19433 -->

2022 年 9 月 30 日に、AdobeDynamic Mediaビューアは次のサポートを終了します。

* TLS(Transport Layer Security)1.0 および 1.1
* TLS 1.2 での以下の脆弱な暗号：
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_RSA_WITH_AES_256_GCM_SHA384`
   * `TLS_RSA_WITH_AES_256_CBC_SHA256`
   * `TLS_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_AES_128_GCM_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
   * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

