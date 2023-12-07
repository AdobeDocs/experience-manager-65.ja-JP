---
title: Visual Studio プロジェクトの設定と Windows アプリケーションの構築
description: Visual Studio プロジェクトを設定してAEM Forms Windows モバイルデバイスアプリを構築する方法を説明します。
topic-tags: forms-app
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 51%

---

# Visual Studio プロジェクトの設定と Windows アプリケーションの構築{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムワークスペースアプリケーションを構築するためのすべてのコンポーネントが含まれています。ソースコードアーカイブ `adobe-lc-mobileworkspace-src-<version>.zip` は、ソフトウェアディストリビューションの `adobe-aemfd-forms-app-src-pkg-<version>.zip` パッケージの一部です。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. 選択 **[!UICONTROL Adobe Experience Manager]** は、ヘッダーメニューで使用できます。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージ名を選択し、「 」を選択します。 **[!UICONTROL 使用許諾契約書に同意する]**&#x200B;をクリックし、次を選択します。 **[!UICONTROL ダウンロード]**.
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

1. ソースコードアーカイブをダウンロードするには、ブラウザーで `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` を開きます。\
   ソースパッケージがデバイスにダウンロードされます。

以下の画像は、`adobe-lc-mobileworkspace-src-<version>.zip` から抽出した内容を示しています。

![mws-content-1](assets/mws-content-1.png)

以下の画像は、`src` フォルダー内の `windows` フォルダーのディレクトリ構造を示しています。

![win-dir](assets/win-dir.png)

## 環境の設定 {#setting-up-the-environment}

Windows デバイスの場合は、次が必要です。

* Microsoft Windows 8.1 または Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools for Apache Cordova

## AEM Formsアプリ用の Visual Studio プロジェクトの設定 {#setting-up-visual-studio-project-for-aem-forms-app}

次の手順を実行して、Visual Studio でAEM Formsアプリケーションプロジェクトを設定します。

1. Visual Studio 2015 がインストールおよび設定済みの Windows 8.1 または Windows 10 デバイスの `%HOMEPATH%\Projects` フォルダーに、`adobe-lc-mobileworkspace-src-<version>.zip` アーカイブをコピーします。
1. `%HOMEPATH%\Projects\MobileWorkspace` ディレクトリにアーカイブを抽出します。
1. `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` ディレクトリに移動します。
1. Visual Studio 2015 を使用して `CordovaApp.sln` ファイルを開き、AEM Forms アプリケーションの構築に進みます。

## AEM Formsアプリの作成 {#build-aem-forms-app}

次の手順を実行して、AEM Formsアプリをビルドおよびデプロイします。

>[!NOTE]
>
>AEM Formsアプリ用に Windows ファイルシステムに保存されたデータは、暗号化されません。 Windows BitLocker Drive Encryption などのサードパーティのツールを使用して、ディスクのデータを暗号化することをお勧めします。

1. Visual Studio の標準ツールバーで、「ビルドモード」のドロップダウンリストから「**リリース**」を選択します。

1. ご使用のプラットフォームに応じて、Windows-AnyCPU、Windows-x64、または Windows-x86 を選択します。 Windows-AnyCPU を推奨します。
1. Visual Studio Solution Explorer で「**CordovaApp.Windows**」プロジェクトを右クリックし、**ストア／アプリパッケージを作成**&#x200B;を選択します。

   ![createapppackages](assets/createapppackages.png)

   「アプリパッケージの作成」ウィザードが表示されます。

   CordovaApp.Windows_3.0.2.0_anycpu.appx インストーラーファイルが platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test ディレクトリに作成されます。

   `Retarget to windows 8.1 required` というエラーが発生した場合は、そのエラーを右クリックし、ポップアップメニューで **Windows 8.1 に再ターゲット**&#x200B;を選択します。

   ![retarget-solution](assets/retarget-solution.png)

1. 「アプリパッケージの作成」ウィザードで、Windows ストアにアプリケーションをアップロードするかどうかを選択し、「**次へ**」をクリックします。

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 必要に応じて、バージョンやアプリケーションのビルドの出力場所などのパラメーターを変更します。

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. プロジェクトが構築されたら、以下を使用してアプリをインストールできます。

   * Windows PowerShell
   * Visual Studio

   `.appx` パッケージのインストールには、以下の項目が必要です。

   1. WinJS ライブラリ
   1. パッケージに、自己署名済みの証明書、または VeriSign などの信頼できる機関が署名した公開証明書が付属していることを確認します。
   1. 開発者用ライセンス

   4 つの主要なコンポーネントが、Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test ディレクトリに格納されています。

   1. `.appx` ファイル
   1. 証明書（現在 Apache Cordova の自己署名証明書が使用されています）
   1. 依存フォルダー
   1. PowerShell ファイル（.ps1 拡張子）

## Windows PowerShell を使用したアプリのデプロイ {#deploying-an-app-using-windows-powershell}

Windows デバイスにアプリケーションをインストールする方法は 2 つあります。

### 開発者用ライセンスを取得する方法 {#by-acquiring-the-developer-license}

1. PowerShell ファイル ( `Add-AppDevPackage.ps1)`を選択します。 **PowerShell で実行**.

1. 設定により、開発者用ライセンスを取得するよう求められます。 Microsoftアカウントの資格情報を使用して、開発者用ライセンスを取得します。\
   このライセンスは 30 日間有効です。無料で更新することができます。
1. 開発者用ライセンスを取得すると、セットアップによって自己署名証明書がシステムにインストールされ、アプリケーションが正常にインストールされます。

### 企業が所有するデバイスを使用する {#by-using-enterprise-owned-devices}

企業が所有するデバイスが企業のドメインに加入している場合、開発者用ライセンスを取得する必要はありません。

企業が所有するデバイスは、Windows の Professional エディションと Enterprise エディションを使用します。

Microsoftでは、VeriSign などの信頼できる機関が発行した公開証明書をインストールすることをお勧めします。

アプリケーションをデプロイするには：

* デバイスがエンタープライズドメインに加入していることを確認します。
* グループポリシー設定を有効にします。

**グループポリシー設定を有効にするには：**

1. デバイス上で `gpedit.msc` を実行します。
1. に移動します。 **コンピューターの構成/管理テンプレート/ Windows コンポーネント/アプリパッケージの展開**.
1. 右クリック **信頼できるすべてのアプリのインストールを許可**.
1. クリック **編集** を選択し、 **有効**.

1. 「**OK**」をクリックします。

Visual Studio で生成された PowerShell スクリプトを編集して、開発者用ライセンスの取得を停止します。

PowerShell スクリプトで、`$NeedDeveloperLicense = $false` の変数を設定します。

ドメインに参加していないデバイスの場合は、製品のアクティベーションキーのサイドロードが必要です。 Windows の販売店から購入できます。

Windows 8.1 Home Edition の場合、グループポリシーがなく、エンタープライズサイドロードが許可されておらず、エンタープライズドメインとの参加はできません。 開発者用ライセンスを使用して、Windows 8.1 Home Edition デバイスにアプリをデプロイします。

詳しくは、 [ここ](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx).

## Visual Studio を使用したアプリのデプロイ {#deploying-an-app-using-visual-studio}

Visual Studio を使用して Windows にアプリケーションをインストールするには：

1. リモートデバッガーを使用してデバイスに接続します。\
   詳しくは、[リモートマシン上での Windows ストアアプリケーションの実行](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)を参照してください。

1. Visual Studio でアプリを開き、「ソリューションプラットフォーム」リストから Windows-x64、Windows-x86、または Windows-AnyCPU を選択し、「 」を選択します。 **リモートマシン**.
1. アプリがリモートマシンにデプロイされます。
