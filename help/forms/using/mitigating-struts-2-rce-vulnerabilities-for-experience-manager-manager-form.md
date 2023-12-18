---
title: JEE 上のExperience Manager Formsの Struts 2 脆弱性の緩和
description: JEE 上のExperience Manager Formsの Struts 2 脆弱性の緩和
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
source-git-commit: e42d01f1e5e44b12b755c20f826331ddbad8ab58
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 1%

---


# Experience Manager Formsの Struts 2 脆弱性の緩和 {#mitigatin-struts2-rce-vulnerabilities-for-aem-forms}

## イシュー

Java EE Web アプリケーションを開発するための一般的でオープンソースな Web アプリケーションフレームワークである Struts 2 に対して、重要なセキュリティ脆弱性が報告されています。 次の脆弱性が分析されました。

| 脆弱性 | 影響 | 影響のないもの |
|---|---|---|
| [CVE-2023-50164](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-50164) | JEE 上のFormsExperience Manager6.5 (6.5 GA から 6.5.19.0までのすべてのバージョン ) | <ul><li> Experience Manager Forms Workbench（すべてのバージョン）</li> <li> OSGi 上のExperience Manager Forms（すべてのバージョン） </li> <li> Experience Manager Formsas a Cloud Service </li> <ul> |

## 解決策

次の表に、影響を受けるすべてのバージョンの解決方法を示します。

| リリース | 現在のバージョン | ユーザーアクション |
|---|---|---|
| JEE 上のExperience Manager6.5 Forms | 6.5.19.0 | [最新のサービスパックをインストールする](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en) |
| JEE 上のExperience Manager6.5 Forms | 6.5.13.0 - 6.5.18.0 | 次のいずれかの方法を使用します。 <ul><li>  <a href="https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en"> 最新のサービスパックをインストールする </a> </li> <li> <a href ="#use-manual-mitigation-steps"> 手動の緩和手順の使用 </a> |
| JEE 上のExperience Manager6.5 Forms | 6.5 - 6.5.12.0 | [最新のサービスパックをインストールする](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en)  </br> </br> **注意：** AEM Formsは現在、バージョン 6.5.13.0 ～ 6.5.19.0をサポートしています。古いバージョンを使用している場合は、6.5.13.0以降のリリースにアップグレードすることをお勧めします。 AEM 6.5.13.0以降のリリースのインストール手順については、リリースノートを参照してください。 |

### 手動の緩和手順の使用 {#use-manual-mitigation-steps}

手動の緩和手順を使用して、Service Pack 13 を実行しているAEM 6.5 Form Server からAEM 6.5 Form Server Running Service Pack 18 (6.5.13.0 - 6.5.18.0) の問題を解決できます。

1. すべてのサーバーインスタンスとロケーターをシャットダウンします。
1. をダウンロードします。 [struts-core 2.5.33 jar](https://repo1.maven.org/maven2/org/apache/struts/struts2-core/2.5.33/struts2-core-2.5.33.jar).
1. JEE 上のAEM Formsの手動パッチ適用ツールのダウンロード先 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/patch_utility/archive-patcher-1.0.0.zip).
1. 手動パッチツールアーカイブを解凍します。 次のファイルが抽出されます。
   * archive-patcher-1.0.0.jar
   * patch-archive.bat
   * patch-archive.sh
1. ターミナルウィンドウを開き、抽出したファイルを含むフォルダーに移動します。
1. 手動パッチ適用ツールを使用して、すべての struts2 jar ファイルを検索、リスト、および置換します。 このツールは、実行時に依存関係をダウンロードするので、インターネット接続が必要です。 したがって、ツールを実行する前に、インターネットに接続していることを確認します。

検索と置換を行うには `struts2-core-2.5.30.jar` および `struts2-core.jar` ファイル：



>[!BEGINTABS]

>[!TAB Windows]

1. 次のコマンドを実行して、すべての struts2 jar ファイルを一覧表示します。 コマンドを実行する前に、コマンドのパスをAEM Forms Server のパスに置き換えます。


   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$
   ```

1. 再帰的なインプレース置換を行うには、次のコマンドをリストの順序で実行します。 コマンドを実行する前に、コマンドのパスをAEM Forms Server のパスに置き換え、 `struts2-core-2.5.33.jar` ファイル。



   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$ -action=replace C:\temp\struts2-core-2.5.33.jar
   
   
   patch-archive.bat -root=C:\Users\labuser\Desktop\check -pattern=.*struts2-core.jar$ -action=replace C:\Users\labuser\Desktop\struts2-core.jar        
   ```

   上記の手順では、 `struts2-core-2.5.30.jar` および `struts2-core.jar` ファイル。

1. 古い EAR をデプロイ解除し、パッチを適用した EAR ファイルをアプリケーションサーバーにデプロイします。


1. AEM Forms Server を起動します。


>[!TAB Linux]

1. 次のコマンドを実行して、すべての struts2 jar ファイルを一覧表示します。 コマンドを実行する前に、コマンドのパスをAEM Forms Server のパスに置き換えます。


   ```
   patch-archive.sh -root=/Users/labuser/Adobe.Adobe_Experience_Manager_Forms/.../export -pattern=.*struts2-core-2.5.30.jar$
   ```

1. 再帰的なインプレース置換を行うには、次のコマンドをリストの順序で実行します。 コマンドを実行する前に、コマンドのパスをAEM Forms Server のパスに置き換え、 `struts2-core-2.5.33.jar` ファイル。


   ```
   patch-archive.sh -root=/Users/labuser/Adobe/Adobe_Experience_Manager_Forms/.../export -pattern=.*struts2-core-2.5.30.jar$ -action=replace /temp/struts2-core-2.5.33.jar
   
   
   patch-archive.sh -root=/Users/labuser/Desktop/check -pattern=.*struts2-core.jar$ -action=replace /Users/labuser/Desktop/struts2-core.jar
   ```

   上記の手順では、 `struts2-core-2.5.30.jar` および `struts2-core.jar` ファイル。

1. 古い EAR をデプロイ解除し、パッチを適用した EAR ファイルをアプリケーションサーバーにデプロイします。

1. AEM Forms Server を起動します。

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