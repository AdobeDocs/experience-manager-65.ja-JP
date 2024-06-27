---
title: JEE 版 Experience Manager Forms の Struts 2 脆弱性の緩和
description: JEE 版 Experience Manager Forms の Struts 2 脆弱性の緩和
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 73b5aff2-1320-4d9a-8972-54c4fdd3a2c2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: ht
source-wordcount: '593'
ht-degree: 100%

---

# Experience Manager Forms の Struts 2 脆弱性の緩和 {#mitigatin-struts2-rce-vulnerabilities-for-aem-forms}

## 問題

Java EE web アプリケーションを開発するための一般的なオープンソース web アプリケーションフレームワークである Struts 2 について、重大なセキュリティ脆弱性が報告されています。分析された脆弱性は次のとおりです。

| 脆弱性 | 影響を受けるもの | 影響を受けないもの |
|---|---|---|
| [CVE-2023-50164](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-50164) | JEE 版 Experience Manager 6.5 Forms（6.5 GA から 6.5.19.0 までのすべてのバージョン） | <ul><li> Experience Manager Forms Workbench（すべてのバージョン）</li> <li> OSGi 版 Experience Manager Forms（すべてのバージョン） </li> <li> Experience Manager Forms as a Cloud Service </li> <ul> |

## 解決策

影響を受けるすべてのバージョンの解決策を次の表に示します。

| リリース | 現在のバージョン | ユーザーアクション |
|---|---|---|
| JEE 版 Experience Manager 6.5 Forms | 6.5.19.0 | [最新のサービスパックのインストール](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=ja) |
| JEE 版 Experience Manager 6.5 Forms | 6.5.13.0 - 6.5.18.0 | 次のいずれかの方法を使用します。 <ul><li>  <a href="https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=ja"> 最新のサービスパックのインストール </a> </li> <li> <a href ="#use-manual-mitigation-steps"> 手動の緩和手順の使用 </a> |
| JEE 版 Experience Manager 6.5 Forms | 6.5 - 6.5.12.0 | [最新のサービスパックのインストール](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=ja)  </br> </br> **メモ**：AEM Forms は現在、バージョン 6.5.13.0 から 6.5.19.0 までをサポートしています。古いバージョンを使用している場合は、6.5.13.0 以降のリリースにアップグレードすることをお勧めします。AEM 6.5.13.0 以降のリリースのインストール手順については、リリースノートを参照してください。 |

### 手動の緩和手順の使用 {#use-manual-mitigation-steps}

手動の緩和手順を使用して、サービスパック 13 を適用した AEM 6.5 Forms サーバーから、サービスパック 18 を適用した AEM 6.5 Forms サーバーまで（6.5.13.0 から 6.5.18.0 まで）の問題を解決できます。

1. [struts-core 2.5.33 jar](https://repo1.maven.org/maven2/org/apache/struts/struts2-core/2.5.33/struts2-core-2.5.33.jar) をローカルフォルダーにをダウンロードします。例：C:\Users\labuser\Desktop\struts2-core-2.5.33.jar。
1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/patch_utility/archive-patcher-1.0.0.zip)から JEE 版 AEM Forms の手動パッチ適用ツールをダウンロードします。
1. この手動パッチ適用ツールアーカイブを解凍します。例えば、`/Users/labuser/Desktop/archive-patcher-1.0.0 folder` に解凍します。次のファイルが解凍されます。
   * archive-patcher-1.0.0.jar
   * patch-archive.bat
   * patch-archive.sh

>[!BEGINTABS]

>[!TAB Windows]

1. すべてのサーバーインスタンスとロケーターをシャットダウンします。

1. ターミナルウィンドウを開き、JEE 版 AEM Forms 手動パッチ適用ツール（解凍したファイル）を含んだフォルダーに移動します。

1. 次のコマンドを実行して、古い struts2 ライブラリを含むすべてのファイルを検索します。コマンドを実行する前に、コマンド内のパスを AEM Forms サーバーのパスに置き換えます。


   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >このツールは、実行時に依存関係をダウンロードするので、使用するにはインターネット接続が必要です。したがって、ツールを実行する前に、インターネットに接続していることを確認します。

1. 再帰的なインプレース置換を行うには、次のコマンドを列挙した順に実行します。コマンドを実行する前に、コマンド内のパスを AEM Forms サーバーのパスと `struts2-core-2.5.33.jar` ファイルに置き換えます。



   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$ -action=replace C:\Users\labuser\Desktop\struts2-core-2.5.33.jar
   ```

   上記の手順では、古い struts2 ライブラリを含むすべての EAR ファイルにパッチを適用します。

1. 古い EAR をデプロイ解除し、（エクスポートフォルダーにある）パッチ適用済みの EAR ファイルをアプリケーションサーバーにデプロイします。

1. AEM Forms サーバーを起動します。

>[!TAB Linux]

1. すべてのサーバーインスタンスとロケーターをシャットダウンします。

1. ターミナルウィンドウを開き、JEE 版 AEM Forms 手動パッチ適用ツール（解凍したファイル）を含んだフォルダーに移動します。

1. 次のコマンドを実行して、古い struts2 ライブラリを含むすべてのファイルを検索します。コマンドを実行する前に、コマンド内のパスを AEM Forms サーバーのパスに置き換えます。


   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >このツールは、実行時に依存関係をダウンロードするので、使用するにはインターネット接続が必要です。したがって、ツールを実行する前に、インターネットに接続していることを確認します。

1. 再帰的なインプレース置換を行うには、次のコマンドを列挙した順に実行します。コマンドを実行する前に、コマンド内のパスを AEM Forms サーバーのパスと `struts2-core-2.5.33.jar` ファイルに置き換えます。



   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$ -action=replace /opt/struts2-core-2.5.33.jar
   ```

   上記の手順では、古い struts2 ライブラリを含むすべての EAR ファイルにパッチを適用します。

1. 古い EAR をデプロイ解除し、（エクスポートフォルダーにある）パッチ適用済みの EAR ファイルをアプリケーションサーバーにデプロイします。

1. AEM Forms サーバーを起動します。

>[!ENDTABS]




<!-- 
### Manual patching tool 


>[!BEGINTABS]

>[!TAB Windows]

    ```
    
    patch-archive.bat [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.

>[!TAB macOS]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  

>[!TAB Linux]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  



>[!ENDTABS]









-->
