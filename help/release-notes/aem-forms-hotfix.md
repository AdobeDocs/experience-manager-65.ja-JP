---
title: AEM Formsのホットフィックス
description: AEM Formsのホットフィックスをダウンロードしてインストールする方法に関する情報を提供します。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
source-git-commit: 4685a4babbec07dc09fe19c9264b4141b9989fbb
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 9%

---

# Adobe Experience Manager Forms Hotfixes{#aem-form-hotfix}

この記事では、既知の問題に対処し、システムの安定性を向上し、AEM Formsの全体的なパフォーマンスを向上させるために実装された重要な修正について説明します。

>[!NOTE]
>
> ホットフィックスは、以前のすべての修正を含む累積的な修正になるように設計されています。 最新のホットフィックスをリリースに適用すると、最新の問題に対処するだけでなく、以前のバグ修正および機能強化もすべて含まれます。

## アダプティブFormsのホットフィックス {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日付</strong></td>
    <td><strong>修正プログラムのダウンロードリンク (AEM Software Distribution リンク )</strong></td>
    <td><strong>修正された問題</strong></td>
  </tr>
  <tr>
    <td>2024年1月29日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">JEE サーバー上の Windows 用AEM Service Pack 6.5.19.0のホットフィックス</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>JEE サーバー上のAEM Formsで、コンテキストパスを利用するHTML5 Formsがレンダリングに失敗します。 (FORMS-12485)。</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年1月29日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Microsoft Windows 向けAEM Service Pack 6.5.18.0のホットフィックス</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Linux 用AEM Service Pack 6.5.18.0のホットフィックス</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Apple macOSのAEM Service Pack 6.5.18.0のホットフィックス</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> OOTB の手書き署名コンポーネントは、アダプティブフォームのプレビュー用にレンダリングできません。 (FORMS-12073)。</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>2023年11月20日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Linux 用AEM Service Pack 6.5.18.0のホットフィックス</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Microsoft Windows 向けAEM Service Pack 6.5.18.0のホットフィックス</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Apple macOSのAEM Service Pack 6.5.18.0のホットフィックス</a></li>
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

1. ダウンロード [ホットフィックス](#hotfix-for-adaptive-forms) を「ソフトウェア配布」リンクからクリックします。
1. ホットフィックスアーカイブファイルを抽出して、Experience Manager パッケージ（.zip）とバンドル（.jar）ファイルを取得できるようにします。
1. を使用してパッケージ (.zip) をアップロードしインストールします。 [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Configuration Manager バンドルを開きます。 `https://server:host/system/console/bundles`バンドル (.jar) をアップロードし、インストールします。 ホットフィックスがインストールされている。
