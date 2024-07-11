---
title: AEM Forms のホットフィックス
description: AEM Forms のホットフィックスをダウンロードしてインストールする方法について説明します。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: fb689e86deaabcc4033ed75f615086b630a9a525
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 75%

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
    <td>2024年7月10日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">Windows 上のAEM サービスパック 6.5.21.0 のホットフィックス（JBoss JEE サーバー用） </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">JBoss JEE サーバー用 Linux 上のAEM サービスパック 6.5.21.0 のホットフィックス </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">Windows 上のAEM サービスパック 6.5.21.0 の Webshpere JEE サーバー用ホットフィックス </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">Webshpere JEE サーバー用 Linux 上のAEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">Windows for Weblogic JEE サーバーのAEM サービスパック 6.5.21.0 のホットフィックス </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Weblogic JEE サーバー用 Linux 上のAEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>JEE サーバー上でAEM Forms サービスパック 20 （6.5.20.0）に更新し、出力サービスを使用してPDFを生成すると、PDFがレンダリングされてアクセシビリティの問題が発生します。 （LC-3922112）</li><li>AEM Forms JEE の出力サービスを使用して生成されたタグ付きPDFに、「不適切な構造の警告」と表示される。 （LC-3922038）</li><li>フォームがAEM Forms JEE で送信されると、繰り返し XML 要素のインスタンスがデータから削除されます。 （LC-3922017）</li><li>Linux 環境で（JEE 上の）アダプティブフォームをHTMLーでレンダリングすると、が正しくレンダリングされません。 （LC-3921957）</li><li>AEM Forms JEE でユーザーが Output サービスを使用して XTG ファイルをPostScript形式に変換すると、次のエラーで失敗します。AEM_OUT_001_003：予期しない例外：PAExecute エラー：XFA_RENDER_FAILURE。 （LC-3921720）</li><li>JEE サーバー上のAEM Forms サービスパック 18 （6.5.18.0）にアップグレードした後、フォームを送信すると、HTML5 またはPDF formsのレンダリングに失敗し、XMLFM がクラッシュします。 （LC-3921718）
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年6月21日（PT）</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">JBoss JEE サーバー上の AEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Weblogic JEE サーバー上の AEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Webshpere JEE サーバー上のAEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">OSGi サーバー上の AEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> AEM Forms サービスパック 6.5.21.0 にアップグレードすると、PaperCapture サービスが PDF に対して OCR（光学式文字認識）操作を実行できなくなります。インストール手順については、<a href="/help/forms/using/papercapture-service-resolution.md">トラブルシューティング</a>の記事を参照してください。（CQDOC-21680） </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年6月21日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">AEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>XML データを含むドラフトレターがプレビュー中に読み込み状態で停止します。ホットフィックスのダウンロードとインストールの手順については、<a href="#install-hotfix">ドラフトレターの問題に対するホットフィックスのダウンロードとインストール</a>の節を参照してください。（FORMS-14521）</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年5月16日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=/content/software-distribution/ja/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">Microsoft Windows 用 AEM サービスパック 6.5.20.0 のホットフィックス</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=/content/software-distribution/ja/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">Linux 用 AEM サービスパック 6.5.20.0 のホットフィックス</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html?package=/content/software-distribution/ja/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">Apple macOS 用 AEM サービスパック 6.5.20.0 のホットフィックス</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>チェックボックスにスクリプトが埋め込まれた XDP に基づくアダプティブフォームでは、このようなチェックボックスの後の要素に対してスクリプトは実行されません。この問題のホットフィックスが入手可能です。（FORMS-14244） </li>
     <li> 編集／表示パターンを持つフィールドのポップアップウィジェットで月をトラバースすると、日付選択ウィジェットの行が切り捨てられます。この問題のホットフィックスが入手可能です。（FORMS-13620） </li>
     <li>バックエンドで DOR（レコードのドキュメント）サービスを使用しようとすると、フォームの送信が失敗します。「フォームリソースが正しく割り当てられていないので、送信アクションを完了できませんでした」というエラーメッセージが表示されます。（FORMS-13798） </li>
     <li>アダプティブフォームを Adobe Experience Manager パブリッシュインスタンスから Adobe Experience Manager ワークフローに送信すると、ワークフローでは添付ファイルの保存に失敗します。（FORMS-14209） </li>
     <li> AEM 6.5 Forms サービスパック 20 パッケージ（SP20 用の AEM Forms アドオンパッケージ）をインストールすると、AEM Sites ユーザーインターフェイス（UI）のパフォーマンスが大幅に低下します。（FORMS-13791） </li>
     <li>インタラクティブ通信で null ポインターの例外が発生して、事前入力サービスが失敗します。（CQDOC-21355）</li>
    </ul>
    </td>    
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


## ドラフトレターの問題に対するホットフィックスのダウンロードとインストール {#install-hotfix}

問題を解決するには、次の手順に従います。

1. ソフトウェア配布リンクから[ホットフィックス](#hotfix-for-adaptive-forms)をダウンロードします。
2. [CRX パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=ja#accessing)を使用してパッケージ（.zip）をアップロードしてインストールします。