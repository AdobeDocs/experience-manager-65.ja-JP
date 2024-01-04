---
title: AEM Formsのホットフィックス
description: AEM Formsのホットフィックスをダウンロードしてインストールする方法に関する情報を提供します。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
source-git-commit: 276b0122fb3d88c584dd6b2b4c2c6f6eda9d0537
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 14%

---

# Adobe Experience Manager Forms Hotfixes{#aem-form-hotfix}

この記事では、既知の問題に対処し、システムの安定性を向上し、AEM Formsの全体的なパフォーマンスを向上させるために実装された重要な修正について説明します。

## アダプティブFormsのホットフィックス {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日付</strong></td>
    <td><strong>修正プログラムのダウンロードリンク (AEM Software Distribution リンク )</strong></td>
    <td><strong>修正された問題</strong></td>
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

1. ダウンロード [ホットフィックス](#hotfix-for-adaptive-forms) を「Software Distribution」リンクからダウンロードします。
1. ホットフィックスアーカイブファイルを抽出して、Experience Manager パッケージ（.zip）とバンドル（.jar）ファイルを取得できるようにします。
1. を使用してパッケージ (.zip) をアップロードしインストールします。 [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Configuration Manager バンドルを開きます。 `https://server:host/system/console/bundles`バンドル (.jar) をアップロードし、インストールします。 ホットフィックスがインストールされている。
