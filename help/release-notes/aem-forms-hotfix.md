---
title: AEM Forms のホットフィックス
description: AEM Forms のホットフィックスをダウンロードしてインストールする方法について説明します。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 100%

---

# Adobe Experience Manager Forms のホットフィックス{#aem-form-hotfix}

この記事では、既知の問題に対処し、システムの安定性を改善して、AEM Forms の全体的なパフォーマンスを向上させるために実装された重要な修正について説明します。

>[!NOTE]
>
> ホットフィックスは累積的に設計されており、以前のすべての修正が含まれます。最新のホットフィックスをリリースに適用すると、最新の問題に対処するだけでなく、以前のすべてのバグ修正と機能強化も組み込まれます。

## アダプティブフォームのホットフィックス {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日付</strong></td>
    <td><strong>ホットフィックスのダウンロードリンク（AEM ソフトウェア配布リンク）</strong></td>
    <td><strong>修正された問題</strong></td>
  </tr>
  <tr>
    <td>2024年1月29日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">JEE サーバー上の Windows 用 AEM サービスパック 6.5.19.0 のホットフィックス</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>JEE サーバー上の AEM Forms では、コンテキストパスを使用する HTML5 フォームのレンダリングに失敗します。（FORMS-12485、FORMS-12691）。</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年1月29日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Microsoft Windows 用 AEM サービスパック 6.5.18.0 のホットフィックス</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Linux 用 AEM サービスパック 6.5.18.0 のホットフィックス</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Apple macOS 用 AEM サービスパック 6.5.18.0 のホットフィックス</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> 標準の手書き署名コンポーネントでは、アダプティブフォームでのプレビューのレンダリングに失敗します。（FORMS-12073）。</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>2023年11月20日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Linux 用 AEM サービスパック 6.5.18.0 のホットフィックス</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Microsoft Windows 用 AEM サービスパック 6.5.18.0 のホットフィックス</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Apple macOS 用 AEM サービスパック 6.5.18.0 のホットフィックス</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>アダプティブフォームのガイドコンテナにリダイレクト URL が設定されると、インライン署名が機能しなくなります。（FORMS-10493）</li>
    <li>レコードのドキュメント（DoR）テンプレートでは、ローカライズされたアダプティブフォームに対して公開に失敗します。（FORMS-10535）</li>
    <li>大きなインライン画像を使用したインタラクティブ通信では、編集モードで開くのに失敗します。（FORMS-10578）</li>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## ホットフィックスのダウンロードとインストール {#download-install-hotfix}

ホットフィックスをダウンロードしてインストールするには、次の手順を実行します。

1. ソフトウェア配布リンクから[ホットフィックス](#hotfix-for-adaptive-forms)をダウンロードします。
1. ホットフィックスアーカイブファイルを抽出して、Experience Manager パッケージ（.zip）とバンドル（.jar）ファイルを取得できるようにします。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=ja#accessing)を通じてパッケージ（.zip）をアップロードしてインストールします。
1. 設定マネージャーのバンドル `https://server:host/system/console/bundles` を開き、バンドル（.jar）をアップロードしてインストールします。ホットフィックスがインストールされます。
