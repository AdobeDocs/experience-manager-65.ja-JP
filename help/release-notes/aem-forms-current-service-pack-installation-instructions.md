---
title: AEM Forms の AEM Forms パッチのインストール手順
description: OSGi および JEE 環境に対する AEM Forms サービスパックのインストール手順
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 95%

---

# AEM 6.5 Forms サービスパックのインストール手順 {#aem-form-patch-installation-instructions}

## リリース情報

| 製品 | Adobe Experience Manager 6.5 Forms |
|---|---|
| バージョン | 6.5.23.0 |
| タイプ | サービスパックのリリース |
| 日付 | 2025年6月6日（PT） |
| ダウンロード URL | [AEM Forms の最新リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) |

>[!NOTE]
>
>修正された問題の一覧については、最新の[AEM サービスパックリリースノート](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=ja)を参照してください。

## Experience Manager Forms 6.5 に含まれる内容

Adobe Experience Manager（AEM）Forms サービスパックには、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善など、新機能およびアップグレードされた機能が含まれています。 最新の機能と改善を提供するために、AEM Forms リリースのサービスパックを定期的に用意しています。 テクノロジースタックに応じて次のいずれかのパスを選択し、お使いの環境にサービスパックをダウンロードしてインストールします。

* [JEE 環境の AEM Forms へのサービスパックのダウンロードおよびインストール](#download-and-install-for-jee-service-pack)
* [OSGi 環境の AEM Forms へのサービスパックのダウンロードおよびインストール](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * アドビは、6 回目のサービスパックごとに完全なインストーラーをリリースしています。 AEM 6.5 Forms サービスパック 18（6.5.18.0）は、最新の JEE の完全なインストーラーです。完全なインストーラーが新しいプラットフォームをサポートするのに対して、通常のサービスパックインストーラーには新機能、バグ修正、一般的な改善のみが含まれます。新規インストールを実行する場合や、JEE 環境上の AEM 6.5 Forms の最新ソフトウェアを使用することを計画している場合は、AEM 6.5 Forms インストーラー（2019年4月8日（PT）にリリース）または AEM 6.5.12.0 Forms インストーラー（2022年3月3日（PT）にリリース）ではなく、JEE 上のAEM 6.5.18.0 Forms の完全なインストーラー（2023年8月31日（PT）にリリース）を使用することをお勧めします。完全なインストーラーを使用した後、最新のサービスパックをインストールします。
> * [AEM 6.5 クイックスタート](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=ja)で使用できるアダプティブフォームなどの AEM Forms 機能は、探索と評価のみを目的としています。 実稼動環境で使用する場合は、AEM Forms の有効なライセンスを取得することが不可欠です。

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## JEE 環境の AEM Forms へのサービスパックのダウンロードおよびインストール {#download-and-install-for-jee-service-pack}

<!--
![JEE Installation](/help/forms/using/assets/jeeinstallation.png) -->

+++1.既存の環境のバックアップを取る

1. [CRX リポジトリ、データベーススキーマ、GDS（グローバルドキュメントストレージ）](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=ja)をバックアップします。
1. &lt;*AEM_forms_root*>/deploy フォルダーをバックアップします。

>[!NOTE]
>
> AEM サービスパックインストーラーを実行する前に、AEM のインストールディレクトリに対する書き込みアクセス権があることを確認します。

+++

+++2.必要なソフトウェアをダウンロードする

* [AEM Forms on JEE サービスパック](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)

* [フラグメントサーブレット](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

* [AEM サービスパック](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=ja)
* [Forms アドオンパッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)


+++

+++&#x200B;3. Microsoft Visual C++ 再頒布可能パッケージのインストール

* AEM 6.5 Forms がインストールされているコンピューターに、[Visual Studio 2015、2017、2019、2022 用の 64 ビット版の Microsoft Visual C++ 再頒布可能パッケージ](https://learn.microsoft.com/ja-jp/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)をダウンロードしてインストールします。

>[!NOTE]
>
> 最新バージョンの可用性を保証するには、前のバージョンがインストールされている場合でも、再頒布可能パッケージをインストールします。

+++

+++&#x200B;4. AEM Forms on JEE サービスパックをインストールします。

1. アプリケーションサーバーを停止します。
1. **AEM Forms on JEE サービスパックのインストーラーアーカイブ**&#x200B;をハードドライブに抽出します。

   * **Windows**
インストールメディアまたはハードディスク上にあるインストーラーのコピー先フォルダー内の適切なディレクトリに移動して、`aemforms65_cfp_install.exe` ファイルをダブルクリックします。

      * （Windows 32 ビット） `Windows\Disk1\InstData\VM`
      * （Windows 64 ビット） `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
適切なディレクトリに移動し、シェルから `./aem65_cfp_install.bin` と入力します。

      * （Linux®）`Linux/Disk1/InstData/NoVM`

   これにより、インストール手順を示すインストールウィザードが起動します。

1. 最初のパネルで&#x200B;**[!UICONTROL 次へ]**&#x200B;をクリックします。
1. **インストールフォルダーを選択**&#x200B;画面で、表示されるデフォルトの場所が既存のインストール場所であることを確認するか、または&#x200B;**[!UICONTROL 参照]**&#x200B;をクリックして AEM Forms がインストールされている別のフォルダーを選択してから、**[!UICONTROL 次へ]**&#x200B;をクリックします。
1. サービスパックの概要情報を読み、**[!UICONTROL 次へ]**&#x200B;をクリックします。
1. プリインストールの概要情報を読み、**[!UICONTROL インストール]**&#x200B;をクリックします。
1. インストールが完了したら、**[!UICONTROL 次へ]**&#x200B;をクリックして、インストールされたファイルに対して Quick Fix アップデートを適用します。
1. **[Windows のみ]：** 次のいずれかのステップを実行します。

   * **Configuration Manager を起動**&#x200B;オプションの選択を解除し、**[!UICONTROL 完了]**&#x200B;をクリックします。 `[aem-forms root]\configurationManager\bin` にある **ConfigurationManager.bat** ファイルを使用して **Configuration Manager** を実行します。

   * または、**Configuration Manager を起動**&#x200B;オプションの選択を解除し、**[!UICONTROL 完了]**&#x200B;をクリックします。 **ConfigurationManager.exe** または **ConfigurationManager_IPv6.exe** を使用して **Configuration Manager** を実行する前に、*`<AEMForms_Install_Dir>\configurationManager\bin`* ディレクトリに移動し、**ConfigurationManager.lax** と **ConfigurationManager_IPV6.lax** を最新の [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) ファイルと [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) ファイルに置き換えて、これら 2 つのファイル内で **axis-1.4.1.1.jar** を検索し、**axis-1.4.1.2.jar** に置き換えます。

     >[!NOTE]
     >
     >* **ConfigurationManager.bat** ファイルの更新または置き換えを行うと、.lax ファイルを手動で更新する必要がなくなります。

1. **[UNIX ベース専用]：**&#x200B;**Configuration Manager を起動**&#x200B;チェックボックスは、デフォルトで選択されています。 **[!UICONTROL 完了]**&#x200B;をクリックして Configuration Manager をすぐに実行するか、**Configuration Manager** を後で実行するには、**Configuration Manager を起動**&#x200B;オプションの選択を解除してから、**[!UICONTROL 完了]**&#x200B;をクリックします。 `[AEM_forms_root]/configurationManager/bin` ディレクトリ内の適切なスクリプトを使用して、後で **Configuration Manager** を起動することができます。

1. アプリケーションサーバーに応じて、以下のいずれかのドキュメントを選択し、*AEM Forms の設定とデプロイ*&#x200B;節の指示に従ってください。

   * [AEM Forms for JBoss® のインストールおよびデプロイ](https://www.adobe.com/go/learn_aemforms_installJBoss_65_jp)
   * [AEM Forms for WebSphere® のインストールおよびデプロイ](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_jp)
   * [&#x200B; AEM Forms for WebLogic のインストールおよびデプロイ](https://www.adobe.com/go/learn_aemforms_installWebLogic_65_jp)
   * [AEM forms for JBoss® Cluste のインストールおよびデプロイ](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [AEM forms for WebSphere® Cluste のインストールおよびデプロイ](https://helpx.adobe.com/content/dam/help/ja/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [AEM Forms for WebLogic Cluster のインストールおよびデプロイ](https://helpx.adobe.com/content/dam/help/ja/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
>* JEE 上に AEM Forms サービスパックをインストールした後、appserver を再起動する前に、`crx-repository\install` フォルダーから Forms アドオンパッケージを削除する必要があります。 [ソフトウェア配布ポータル](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)から、最新の Forms アドオンパッケージをダウンロードします。
>* 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。 Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。
>* [JEE 上の AEM Forms の Spring Framework の脆弱性を軽減するためのホットフィックス](/help/release-notes/aem-forms-hotfix.md)の場合、クラスター環境にデプロイする際に、ロケーターが JDK 17 を使用して起動されていることを確認する必要があります。

+++

+++&#x200B;5. インストールされていない場合は、サーブレットフラグメントをインストールする（**必須の手順**）

<!-- >[!NOTE] > > * If you are upgrading from **AEM Service Pack 6.5.15.0**, the installation of the **servlet fragment** is not required. For versions **AEM Service Pack 6.5.14.0** or earlier, it is **mandatory to install** the servlet fragment. -->

サーブレットフラグメントのダウンロードとインストール

1. フラグメントをダウンロードしていない場合は、[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)からダウンロードします。

2. アプリケーションサーバーを起動し、ログが安定するのを待ってから、バンドルの状態を確認します。

3. Web コンソールのバンドルを開きます。 デフォルトの URL は `http://[Server]:[Port]/system/console/bundles` です。

4. 「インストール／更新」をクリックします。 ダウンロードしたフラグメント`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`を選択します。 **インストール**&#x200B;または&#x200B;**更新**&#x200B;をクリックします。 アプリケーションサーバーが安定するまで待つ

5. アプリケーションサーバーを停止します。

+++

+++&#x200B;6. AEM サービスパックをインストールする

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。
1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。
1. [ソフトウェア配布](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)からサービスパックをダウンロードします。 <!-- UPDATE FOR EACH NEW RELEASE -->
1. パッケージマネージャーを開き、**[!UICONTROL パッケージをアップロード]**&#x200B;を選択して、パッケージをアップロードします。 詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。
1. パッケージを選択して、**[!UICONTROL インストール]**&#x200B;を選択します。

**自動インストール**

[!DNL ExperienceManager] サービスパックの自動インストールに使用できる方法は 2 つあります。<!--       UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。 パッケージが自動的にインストールされます。

* [パッケージマネージャーの HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja) を使用します。 ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

  >[!NOTE]
  >
  >Experience Manager サービスパックでは、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

  **インストールの検証**

  このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

   1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (spversion)` が表示されます。<!-- UPDATE FOR EACH NEW RELEASE -->
   1. すべての OSGi バンドルは、OSGi コンソールで&#x200B;**[!UICONTROL アクティブ]**&#x200B;または&#x200B;**[!UICONTROL フラグメント]**&#x200B;のいずれかになっています（web コンソールを使用：`/system/console/bundles`）。
   1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.14 以降です（web コンソールを使用：`/system/console/bundles`）。

+++

+++&#x200B;7. AEM Experience Manager Forms アドオンパッケージのインストール

1. [!DNL Experience Manager] サービスパックがインストールされていることを確認してください。
1. [AEM Forms リリース](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. [AEM Forms アドオンパッケージのインストール](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)の記載どおりに Forms アドオンパッケージをインストールします。
1. Experience Manager 6.5 Forms でレターを使用する場合は、[最新の AEMFD 互換性パッケージ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)をインストールします。

+++

## OSGi 環境の AEM Forms へのサービスパックのダウンロードおよびインストール {#download-and-install-for-osgi-service-pack}


<!-- ![OSGi Installation Steps](/help/forms/using/assets/osgiinstallation.png)
-->

+++1.既存の環境のバックアップを取る

1. [CRX リポジトリとデータベーススキーマ](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=ja)をバックアップします。

>[!NOTE]
>
> リレーショナルデータベース用の AEM Forms サービスパックをインストールする場合は、DB_schema のバックアップを作成する必要があります。

+++

+++2.必要なソフトウェアをダウンロードする

* [AEM サービスパック](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=ja)
* [Forms アドオンパッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)

+++

+++ &#x200B;3. Microsoft Visual C++ 再頒布可能パッケージのインストール

* AEM 6.5 Forms がインストールされているコンピューターに、[Visual Studio 2015、2017、2019、2022 用の 64 ビット版の Microsoft Visual C++ 再頒布可能パッケージ](https://learn.microsoft.com/ja-jp/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)をダウンロードしてインストールします。

>[!NOTE]
>
>
> 最新バージョンの可用性を保証するには、前のバージョンがインストールされている場合でも、再頒布可能パッケージをインストールします。

+++

+++&#x200B;4. AEM サービスパックをインストールする

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。
1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。
1. [ソフトウェア配布](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)からサービスパックをダウンロードします。 <!-- UPDATE FOR EACH NEW RELEASE -->
1. パッケージマネージャーを開き、**[!UICONTROL パッケージをアップロード]**&#x200B;を選択して、パッケージをアップロードします。 詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。
1. パッケージを選択して、**[!UICONTROL インストール]**&#x200B;を選択します。

**自動インストール**

[!DNL Experience Manager] サービスパックの自動インストールに使用できる方法は 2 つあります。<!--  UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。 パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja) を使用します。 ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

  >[!NOTE]
  >
  >Experience Manager サービスパックは Bootstrap のインストールをサポートしていません。 <!-- UPDATE FOR EACH NEW RELEASE -->

  **インストールの検証**

  このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

   1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (spversion)` が表示されます。 <!-- UPDATE FOR EACH NEW RELEASE -->

   1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

      1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.14 以降です（web コンソールを使用：`/system/console/bundles`）。

+++

+++&#x200B;5. Adobe Experience Manager Forms（AEM）アドオンパッケージのインストール

1. [!DNL Experience Manager] サービスパックがインストールされていることを確認してください。
1. [AEM Forms リリース](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. [AEM Forms アドオンパッケージのインストール](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)の記載どおりに Forms アドオンパッケージをインストールします。
1. Experience Manager 6.5 Forms でレターを使用する場合は、[最新の AEMFD 互換性パッケージ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)をインストールします。

+++

## トラブルシューティング

* サービスパックのインストール中に&#x200B;**パッケージマネージャー UI のダイアログ**&#x200B;が終了した場合は、エラーログが安定するまで待ってからデプロイメントにアクセスしてください。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 この問題は、通常 Safari ブラウザーで発生しますが、どのブラウザーでもときどき発生する場合があります。

* インストールが完了したら、アクティビティの監視ログ（error.log）を確認します。 ログにアクティビティが表示されなくなるまで、数分お待ちください。 AEM インスタンスを再起動します。

* AEM Forms 6.5.15.0 以降のサービスパックをインストール後、**サービスを利用できないエラー**&#x200B;が発生した場合は、[サーブレットフラグメントとバンドルをインストール](/help/forms/using/aem-service-pack-installation-solution.md)してエラーを修正します。
