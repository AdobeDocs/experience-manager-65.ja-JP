---
title: AEM Forms のホットフィックス
description: AEM Forms のホットフィックスをダウンロードしてインストールする方法について説明します。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: 0f718a65a5aa0257a1507f3c9541dba84d861ea3
workflow-type: tm+mt
source-wordcount: '3491'
ht-degree: 85%

---

# Adobe Experience Manager Forms のホットフィックス{#aem-form-hotfix}

この記事では、既知の問題に対処し、システムの安定性を改善して、AEM Forms の全体的なパフォーマンスを向上させるために実装された重要な修正について説明します。

>[!NOTE]
>
> ホットフィックスは累積的に設計されており、以前のすべての修正が含まれます。 最新のホットフィックスをリリースに適用すると、最新の問題に対処するだけでなく、以前のすべてのバグ修正と機能強化も組み込まれます。

## AEM Forms のホットフィックス {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日付</strong></td>
    <td><strong>ホットフィックスのダウンロードリンク（AEM ソフトウェア配布リンク）</strong></td>
    <td><strong>修正された問題</strong></td>
  </tr>
  <tr>
    <td>
      <strong>2026年6月8日</strong><br>
      <em>適用対象：</em> AEM 6.5.25.0 WAR/JEE デプロイメント （JEE上のAEM Formsを含む） <br>
    </td>
    <td>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-service-pkg-6.5.25-NPR-44100-B0002.zip">AEM サービスパック 6.5.25.0のホットフィックス （NPR-44100）</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>NPR-44100</b> WAR/JEE デプロイメントにAEM 6.5 Service Pack 25.0をインストールした後、<code>com.adobe.cq.screens.sessions</code> バンドルはインストール済み状態のままになり、アクティブになりません。</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>2025年10月14日</strong><br>
      <em>適用先：</em> ImgToPdfがAEM Forms SP23 Jboss<br>で失敗する
    </td>
    <td>
    <ul> 解決策については、<a href="https://business.adobe.com/in/support/main.html">Adobe Experience Manager Forms サポート </a>にお問い合わせください
    </ul>
    </td>
    <td>
    <ul>
    <li> <b> （FORMS-22029）:</b> SP23にアップグレードした後にPDF Generator （PDFG）で画像ファイルをPDFに変換できない問題が発生し、予期しない後処理エラーが発生するため、PDFの変換の信頼性が向上します。</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>2025年9月23日</strong><br>
    </td>
    <td>
    <ul>
    <strong>Jboss:</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-jboss.zip">JBoss JEE サーバー用の Windows 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-jboss.tar.gz">JBoss JEE サーバー用の Linux 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <strong>Weblogic:</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-weblogic.zip">WebLogic JEE サーバー用の Windows 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-weblogic.tar.gz">WebLogic JEE サーバー用の Linux 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <strong>Websphere:</strong>
    <li>Windows for Websphere JEE サーバー</a>のWindowsでのAEM Service Pack 6.5.23.0のホットフィックス<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-websphere.zip"></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-websphere.tar.gz">Websphere JEE サーバー向けLinux上のAEM Service Pack 6.5.23.0のホットフィックス </a></li>
    </ul>
    </td>
    <td>
    <ul>
    <strong>このホットフィックスでは、次の問題が修正されます。</strong> 
   <li> <b> （FORMS-21721）:</b> 6.5.23.0のホットフィックス （2025年8月5日（PT）にリリース）をデプロイした後、PSからPDFへのコンバージョンとHTMLからPDFへのコンバージョン （WebKit）のコンバージョンが失敗する問題を改善しました。 
    <b></b></li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>
      <strong>2025年8月5日（PT）</strong><br>
      <em>対象：</em>AEM 6.5 Forms サービスパック 23<br>
      <em>設定手順：</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-1-for-users-on-version-65230-install-latest-hotfix">
        AEM Forms on JEE での XXE、設定、リモートコード実行（CVE-2025-49533）の脆弱性の軽減
      </a>
    </td>
    <td>
    <ul>
    <li><strong>Jboss：</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-jboss.zip">JBoss JEE サーバー用の Windows 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-jboss.tar.gz">JBoss JEE サーバー用の Linux 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li><strong>WebLogic：</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-weblogic.zip">WebLogic JEE サーバー用の Windows 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-weblogic.tar.gz">WebLogic JEE サーバー用の Linux 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li><strong>WebSphere：</strong></li>
    <li>Windows for Websphere JEE サーバー</a>のWindowsでのAEM Service Pack 6.5.23.0のホットフィックス<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-websphere.zip"></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-websphere.zip">Websphere JEE サーバー向けLinux上のAEM Service Pack 6.5.23.0のホットフィックス </a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Adobe Experience Manager（AEM）Forms のリモートコード実行（RCE）の脆弱性に対処することで、セキュリティを強化しました。 この問題は、管理ユーザー インターフェイス（UI）の Struts 開発モードに関連し、デバッグ機能を通じて任意のオブジェクトグラフナビゲーション言語（OGNL）評価が可能でした。 この修正により、Struts 開発モードが無効になり、適切なセキュリティフィルターが適用され、不正アクセスが防止されます。</li>
    <li>Adobe Experience Manager（AEM）FormsのEDC （Electronic Document Component）モジュールにおけるXML （External Entity） XXE （Extensible Markup Language）の脆弱性に対する保護を改善しました。この脆弱性は、XXE保護のないXML ドキュメントの不適切な処理が原因で、ローカルのファイル読み取りにつながる可能性がありました。修正には次のものが含まれます。
      <ul>
        <li>SecurityCheckHandler クラスで使用される DocumentBuilderFactory が XXE 攻撃を防ぐように設定されていることを確認します。</li>
        <li>EDC web サービスを更新して XML ドキュメントを安全に処理し、ローカルファイルへの不正アクセスを防ぎます。</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>
      <strong>2025年8月5日（PT）</strong><br>
      <em>適用先：</em>AEM 6.5 Forms サービスパック 18 ～ 22<br>
      <em>設定手順：</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-2-for-users-on-65180---65220-manual-hotfix-installation">
        サービスパック18～22 のホットフィックスの手動インストール
      </a>
    </td>
    <td>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-xxe-configuration-hotfix.zip">AEM 6.5 Forms サービスパック 18 のパッチ - AEM 6.5 Forms サービスパック 22 </a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Adobe Experience Manager（AEM）Forms のリモートコード実行（RCE）の脆弱性に対処することで、セキュリティを強化しました。 この問題は、管理ユーザー インターフェイス（UI）の Struts 開発モードに関連し、デバッグ機能を通じて任意のオブジェクトグラフナビゲーション言語（OGNL）評価が可能でした。 この修正により、Struts 開発モードが無効になり、適切なセキュリティフィルターが適用され、不正アクセスが防止されます。</li>
    <li>Adobe Experience Manager（AEM）FormsのDocument Security モジュールにおける、XML （Extensible Markup Language） External Entity （XXE）の脆弱性に対する保護の強化。この脆弱性は、XXE保護のないXML ドキュメントの不適切な処理が原因で、ローカルのファイル読み取りにつながる可能性がありました。修正には次のものが含まれます。
      <ul>
        <li>SecurityCheckHandler クラスで使用される DocumentBuilderFactory が XXE 攻撃を防ぐように設定されていることを確認します。</li>
        <li>Document Security web サービスを更新して XML ドキュメントを安全に処理し、ローカルファイルへの不正アクセスを防ぎます。</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2025年7月10日（PT）-</td>
    <td>
    <ul>
    <li><strong>Jboss：</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-win-jboss.zip">JBoss JEE サーバー用の Windows 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-jboss.tar.gz">JBoss JEE サーバー用の Linux 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li><strong>WebLogic：</strong></li>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-win-weblogic.zip">WebLogic JEE サーバー用の Windows 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-weblogic.tar.gz">WebLogic JEE サーバー用の Linux 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li><strong>WebSphere：</strong></li>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-win-websphere.zip">WebShpere JEE サーバー用の Windows 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-websphere.tar.gz">WebShpere JEE サーバー用の Linux 上の AEM サービスパック 6.5.23.0 のホットフィックス</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><strong>このホットフィックスでは、次の問題が修正されます。</strong>
      <ul>
        <li><strong>FORMS-20533：</strong>AEM Forms には、フォームコンポーネントの Struts バージョンが 2.5.33 から 6.x へのアップグレードが含まれるようになりました。 これにより、SP23 には含まれていなかった Struts の変更が反映されます。 このサポートは、ダウンロードしてインストールすることで最新バージョンの Struts のサポートを追加できる、ホットフィックスを介して追加されました。</li>
        <li><strong>FORMS-20532：</strong>AEM Forms には、出力コンポーネントの Struts バージョンが 2.5.33 から 6.x へのアップグレードが含まれるようになりました。 これにより、SP23 には含まれていなかった Struts の変更が反映されます。 このサポートは、ダウンロードしてインストールすることで最新バージョンの Struts のサポートを追加できる、ホットフィックスを介して追加されました。</li>
        <li><strong>FORMS-20203：</strong>Struts を AEM サービスパック 2.5.x から AEM Forms サービスパック 6.x にアップグレードすると、ポリシー UI に透かしを追加するオプションなどのすべての設定が表示されなくなります。 問題を解決するには、ホットフィックスをダウンロードしてインストールしてください。</li>
        <li><strong>FORMS-20360：</strong>AEM Forms サービスパック 6.5.23.0 にアップグレードすると、ImageToPDF 変換サービスが次のエラーで失敗します。<br>
        <code>17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp</code><br>
        問題を解決するには、ホットフィックスをダウンロードしてインストールしてください。</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2025年3月26日（PT） </br> </br>この修正をインストールするには、<a href="/help/forms/using/mitigating-spring-framework-vulnerabilities-for-aem-forms-on-jee.md">JEE 上のAEM Forms の Spring Framework の脆弱性の軽減</a>の手順に従ってください。</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-win-jboss.tar.gz">JBoss JEE サーバー用の Windows 上の AEM サービスパック 6.5.22.0 のホットフィックス</a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-jboss.tar.gz">JBoss JEE サーバー用の Linux 上の AEM サービスパック 6.5.22.0 のホットフィックス</a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-win-weblogic.tar.gz">Weblogic JEE サーバー用の Windows 上の AEM サービスパック 6.5.22.0 のホットフィックス</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-weblogic.tar.gz">Weblogic JEE サーバー用の Linux 上の AEM サービスパック 6.5.22.0 のホットフィックス</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-win-websphere.tar.gz">Webshpere JEE サーバー用の Windows 上の AEM サービスパック 6.5.22.0 のホットフィックス</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-websphere.tar.gz">Webshpere JEE サーバー用の Linux 上の AEM サービスパック 6.5.22.0 のホットフィックス</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>JEE 上の AEM Forms の Spring Framework の脆弱性の軽減</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年7月10日（PT）</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">JBoss JEE サーバー用の Windows 上の AEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
      <li>Linux for JBoss JEE サーバー</a>のAEM Service Pack 6.5.21.0のホットフィックス <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz"></li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">Webshpere JEE サーバー用の Windows 上の AEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">Webshpere JEE サーバー用の Linux 上の AEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">Weblogic JEE サーバー用の Windows 上の AEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Weblogic JEE サーバー用の Linux 上の AEM サービスパック 6.5.21.0 のホットフィックス</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>ユーザーが JEE サーバー上で AEM Forms サービスパック 20（6.5.20.0）に更新し、Output サービスを使用して PDF を生成すると、PDF がアクセシビリティに関する問題を伴ってレンダリングされます。 （LC-3922112）</li><li>AEM Forms JEE の Output サービスを使用して生成されたタグ付き PDF に「不適切な構造の警告」が表示されます。 （LC-3922038）</li><li>AEM Forms JEE でフォームを送信すると、繰り返し XML 要素のインスタンスがデータから削除されます。 （LC-3922017）</li><li>Linux 環境のユーザーがアダプティブフォーム（JEE 上）を HTML でレンダリングすると、正しくレンダリングされません。 （LC-3921957）</li><li>ユーザーが AEM Forms JEE 上の Output サービスを使用して XTG ファイルを PostScript 形式に変換すると、エラー：AEM_OUT_001_003：予期しない例外：PAExecute 失敗：XFA_RENDER_FAILURE が発生して失敗します。 （LC-3921720）</li><li>JEE サーバー上のAEM Forms サービスパック 18 （6.5.18.0）にアップグレードした後、ユーザーがフォームを送信すると、HTML5またはPDF formsとXMLFMがクラッシュします。（LC-3921718）
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年6月21日（PT）</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">JBoss JEE サーバー上の AEM サービスパック 6.5.21.0 または AEM Forms サービスパック 6.5.22.0 のホットフィックス</a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">Weblogic JEE サーバー上の AEM サービスパック 6.5.21.0 または AEM Forms サービスパック 6.5.22.0 のホットフィックス</a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">Webshpere JEE サーバー上の AEM サービスパック 6.5.21.0 または AEM Forms サービスパック 6.5.22.0 のホットフィックス</a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">OSGi JEE サーバー上の AEM サービスパック 6.5.21.0 または AEM Forms サービスパック 6.5.22.0 のホットフィックス</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> AEM Forms サービスパック 6.5.21.0 または AEM Forms サービスパック 6.5.22.0 にアップグレードすると、PaperCapture サービスが PDF に対して OCR（光学式文字認識）操作を実行できなくなります。 インストール手順については、<a href="/help/forms/using/papercapture-service-resolution.md"> トラブルシューティング </a>の記事を参照してください。（CQDOC-21680） </li>
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
    <li>チェックボックスにスクリプトが埋め込まれた XDP に基づくアダプティブフォームでは、このようなチェックボックスの後の要素に対してスクリプトは実行されません。 この問題のホットフィックスが入手可能です。 （FORMS-14244） </li>
     <li> 編集／表示パターンを持つフィールドのポップアップウィジェットで月をトラバースすると、日付選択ウィジェットの行が切り捨てられます。 この問題のホットフィックスが入手可能です。 （FORMS-13620） </li>
     <li>バックエンドで DOR（レコードのドキュメント）サービスを使用しようとすると、フォームの送信が失敗します。 「フォームリソースが正しく割り当てられていないので、送信アクションを完了できませんでした」というエラーメッセージが表示されます。 （FORMS-13798） </li>
     <li>アダプティブフォームを Adobe Experience Manager パブリッシュインスタンスから Adobe Experience Manager ワークフローに送信すると、ワークフローでは添付ファイルの保存に失敗します。  （FORMS-14209） </li>
     <li> AEM 6.5 Forms サービスパック 20 パッケージ（SP20 用の AEM Forms アドオンパッケージ）をインストールすると、AEM Sites ユーザーインターフェイス（UI）のパフォーマンスが大幅に低下します。  （FORMS-13791） </li>
     <li>インタラクティブなコミュニケーションで null ポインターの例外が発生して、事前入力サービスが失敗します。 （CQDOC-21355）</li>
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
    <li>JEE サーバー上の AEM Forms では、コンテキストパスを使用する HTML5 フォームのレンダリングに失敗します。 （FORMS-12485、FORMS-12691）。</li>
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
    <li> 標準の手書き署名コンポーネントでは、アダプティブフォームでのプレビューのレンダリングに失敗します。 （FORMS-12073）。</li>
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
    <li>アダプティブフォームのガイドコンテナにリダイレクト URL が設定されると、インライン署名が機能しなくなります。 （FORMS-10493）</li>
    <li>レコードのドキュメント（DoR）テンプレートでは、ローカライズされたアダプティブフォームに対して公開に失敗します。 （FORMS-10535）</li>
    <li>大きなインライン画像を使用したインタラクティブなコミュニケーションでは、編集モードで開くのに失敗します。 （FORMS-10578）</li>
    </ul>
    </td>    
  </tr>
  </tbody>
</table>

## OSGi ホットフィックスのダウンロードとインストール {#download-install-hotfix}

ホットフィックスをダウンロードしてインストールするには、次の手順を実行します。

1. ソフトウェア配布リンクから[ホットフィックス](#hotfix-for-adaptive-forms)をダウンロードします。
1. ホットフィックスアーカイブファイルを抽出して、Experience Manager パッケージ（.zip）とバンドル（.jar）ファイルを取得できるようにします。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=ja#accessing)を通じてパッケージ（.zip）をアップロードしてインストールします。
1. 設定マネージャーのバンドル `https://server:host/system/console/bundles` を開き、バンドル（.jar）をアップロードしてインストールします。 ホットフィックスがインストールされます。

## JEE パッチのインストール {#download-install-jee-patch}

JEE パッチのインストール手順について詳しくは、[AEM Forms JEE パッチインストーラードキュメント](/help/release-notes/jee-patch-installer-65.md)を参照してください。

<!--
Retained for retrieval: hotfix entries hidden because issues are fixed in AEM Forms 6.5.25.0 or earlier.
Issues: FORMS-14521, FORMS-15428, FORMS-21378, FORMS-23789, FORMS-23802, FORMS-23875, GRANITE-63681

  <tr>
    <td>
      <strong>Feb 18, 2026</strong><br>
      <em>Applies to:</em> AEM Forms on JEE Service Pack 6.5.24.0<br>
    </td>
    <td>
    <ul>
    <strong>Jboss:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/jboss/adobe-aem-forms-jee-hotfix-6.5.24.0-win-jboss.zip">Hotfix for AEM Service Pack 6.5.24.0 on Windows for JBoss JEE server</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/jboss/adobe-aem-forms-jee-hotfix-6.5.24.0-linux-jboss.zip">Hotfix for AEM Service Pack 6.5.24.0 on Linux for JBoss JEE server</a></li>
    <strong>Weblogic:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/weblogic/adobe-aem-forms-jee-hotfix-6.5.24.0-win-weblogic.zip">Hotfix for AEM Service Pack 6.5.24.0 on Windows for Weblogic JEE server</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/weblogic/adobe-aem-forms-jee-hotfix-6.5.24.0-linux-weblogic.tar.gz">Hotfix for AEM Service Pack 6.5.24.0 on Linux for Weblogic JEE server</a></li>
    <strong>Websphere:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/websphere/adobe-aem-forms-jee-hotfix-6.5.24.0-win-websphere.zip">Hotfix for AEM Service Pack 6.5.24.0 on Windows for Websphere JEE server</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/websphere/adobe-aem-forms-jee-hotfix-6.5.24.0-linux-websphere.zip">Hotfix for AEM Service Pack 6.5.24.0 on Linux for Websphere JEE server</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>FORMS-23789</b> Addresses Log4j-related issues in AEM Forms on JEE SP24 that caused disruptions in logging and monitoring for enterprise customers.</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>Feb 17, 2026</strong><br>
      <em>Applies to:</em> AEM Forms SP24<br>
    </td>
    <td>
    <ul> <a href = "https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-GRANITE-64751-SP24-1.0.zip"> AEM 6.5 Forms Hotfix</a>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>GRANITE-63681</b> Form Data Model connectors may fail to authenticate because the required keywords and regex pattern are not allowed by default.</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>Feb 17, 2026</strong><br>
      <em>Applies to:</em> AEM Forms SP24<br>
    </td>
    <td>
    <ul>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-on-add-on/adobe-aemfd-win-pkg-6.0.1454.zip">Hotfix for AEM Forms AddOn 6.0.1454 on Windows</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-on-add-on/adobe-aemfd-linux-pkg-6.0.1454.zip">Hotfix for AEM Forms AddOn 6.0.1454 on Linux</a></li>
    <li>OSX: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.0.1454.zip">Hotfix for AEM Forms AddOn 6.0.1454 on macOS</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>FORMS-23802</b> Custom functions do not work in preview or publish when the Adaptive Form is embedded in a Sites page and the aem-forms-core-component version is less than 1.1.76. This hotfix restores backward compatibility with older aem-forms-core-component versions.</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>Feb 10, 2026</strong><br>
      <em>Applies to:</em>  AEM Forms SP24<br>
    </td>
    <td>
    <ul> <a href = "https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip"> AEM 6.5 Forms AddOn Hotfix</a>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>FORMS-23875</b> In Form Data Model search, an HTML tag is displayed in the UI even when a relevant entity is not present.</li>
    </ul>
    </td>
  </tr>

  Sept 23, 2025 — FORMS-21378 list item:
  <li> <b>(FORMS-21378):</b> Improved form submission reliability by addressing an issue where submissions fail when Server-Side Validation (SSV) is enabled and computed Meta Info is empty.</li>

  June 21, 2024 — FORMS-14521 row:
  <tr>
    <td>June 21, 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">Hotfix for AEM Service Pack 6.5.21.0 </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Draft letters with XML data are getting stuck in the loading state during preview. (FORMS-14521)</li>
    </ul>
    </td>
  </tr>

  May 16, 2024 — FORMS-15428 list item:
  <li>Configurations using the legacy cloud service for Adobe Analytics with user credential-based authentication, fail to function correctly, causing the failure of analytics rules to execute. (FORMS-15428)</li>

  ## Download and install hotfix for draft letter issue {#install-hotfix}
  To resolve FORMS-14521, perform the following steps:
  1. Download the hotfix from the Software Distribution portal.
  2. Upload and install the package (.zip) using the CRX Package Manager.
-->
