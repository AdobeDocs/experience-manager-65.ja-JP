---
title: AEM Form Service Pack のホットフィックス
description: AEM Forms Service Pack のホットフィックスをダウンロードしてインストールする方法に関する情報を提供します。
source-git-commit: 169d407835098add0312b0d12c2c80035b525762
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 17%

---


# Adobe Experience Manager Hotfixes{#aem-form-hotfix}

最新の [AEM Service Pack](/help/release-notes/release-notes.md) は、セキュリティ、パフォーマンス、安定性、お客様向けの主な修正および機能強化を含むを、Adobe Experience Manager 6.5 の一般リリース以降にリリースされたお勧めです。

## アダプティブFormsのホットフィックス {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日付</strong></td>
    <td><strong>ホットフィックス名</strong></td>
    <td><strong>修正</strong></td>
   </tr>
   <tr>
    <td>2023年11月20日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Linux 用AEM Service Pack 6.5.18.0のホットフィックス</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Windows 向けAEM Service Pack 6.5.18.0のホットフィックス</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Mac OS 用AEM Service Pack 6.5.18.0のホットフィックス</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>アダプティブフォームのガイドコンテナにリダイレクト URL が設定されていると、インライン署名が機能しなくなります。 （FORMS-10493）</li>
    <li>ローカライズされたアダプティブFormsで、レコードのドキュメント (DoR) テンプレートが公開されない。 （FORMS-10535）</li>
    <li>大きなインライン画像を含むインタラクティブ通信が、編集モードで開けません。 （FORMS-10578）</li>
    </ul>
    </td>    
    </tr>
    <tbody>
     </table>

## ホットフィックスのダウンロードとインストール {#download-install-hotfix}

ホットフィックスをダウンロードしてインストールするには、次の手順を実行します。

1. ダウンロード [ホットフィックス](#hotfix-for-adaptive-forms) SD リンクから。
1. ホットフィックスアーカイブファイルを抽出して、Experience Manager パッケージ（.zip）とバンドル（.jar）ファイルを取得できるようにします。
1. パッケージマネージャーを通じてパッケージ（.zip）をアップロードしてインストールします。
1. 設定マネージャーのバンドル `https://server:host/system/console/bundles` を開き、バンドル（.jar）をアップロードしてインストールします。
