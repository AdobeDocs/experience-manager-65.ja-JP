---
title: Visual Studio プロジェクトの設定と Windows アプリケーションの構築
seo-title: Visual Studio プロジェクトの設定と Windows アプリケーションの構築
description: Visual Studio プロジェクトを設定し、AEM Forms Windows モバイルデバイスアプリを構築する方法について学びます。
seo-description: Visual Studio プロジェクトを設定し、AEM Forms Windows モバイルデバイスアプリを構築する方法について学びます。
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 63%

---


# Visual Studio プロジェクトの設定と Windows アプリケーションの構築{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムワークスペースアプリケーションを構築するためのすべてのコンポーネントが含まれています。ソースコードアーカイブ `adobe-lc-mobileworkspace-src-<version>.zip`は、ソフトウェア配布 `adobe-aemfd-forms-app-src-pkg-<version>.zip` パッケージの一部です。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. Open [Software Distribution](https://experience.adobe.com/downloads)（ソフトウェア配布）。 Adobe IDがソフトウェア配布物にログインする必要があります。
1. ヘッダーメニューで **[!UICONTROL Adobe Experience Manager]** をタップします。
1. In the **[!UICONTROL Filters]** section:
   1. 「 **[!UICONTROL ソリューション]** 」ドロップダウンリストから「 **[!UICONTROL フォーム]** 」を選択します。
   2. パッケージのバージョンと種類を選択します。 また、「 **[!UICONTROL 検索のダウンロード数]** 」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに対応するパッケージ名をタップし、「EULA条項に **[!UICONTROL 同意します]**」を選択して、「 **[!UICONTROL ダウンロード]**」をタップします。
1. パッ [ケージマネージャーを開き](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/contentmanagement/package-manager.html) 、「パッケージを **[!UICONTROL アップロード]** 」をクリックしてパッケージをアップロードします。
1. Select the package and click **[!UICONTROL Install]**.

1. ソースコードアーカイブをダウンロードするには、ブラウザ `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` ーで開きます。\
   ソースパッケージがデバイスにダウンロードされます。

The following image displays the extracted contents of the `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-1](assets/mws-content-1.png)

The following image displays the directory structure of the `windows` folder in the `src` folder.

![win-dir](assets/win-dir.png)

## 環境の設定 {#setting-up-the-environment}

Windows デバイスの場合、以下の環境が必要です。

* Microsoft Windows 8.1 または Windows 10
* Microsoft Visual Studio 2015
* Apache Cordova 向け Microsoft Visual Studio Tools

## AEM Forms アプリケーション向けの Visual Studio プロジェクトの設定 {#setting-up-visual-studio-project-for-aem-forms-app}

Visual Studio で AEM Forms アプリケーションのプロジェクトを設定するには、以下の手順を実行します。

1. Copy the `adobe-lc-mobileworkspace-src-<version>.zip` archive to `%HOMEPATH%\Projects` folder in the Windows 8.1 or Windows 10 device with Visual Studio 2015 installed and configured.
1. Extract the archive in the `%HOMEPATH%\Projects\MobileWorkspace` directory.
1. Navigate to the `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` directory.
1. Open the `CordovaApp.sln` file using Visual Studio 2015 and proceed to building the AEM Forms app.

## AEM Forms アプリケーションの構築 {#build-aem-forms-app}

AEM Forms アプリケーションを構築しデプロイするには、次の手順を実行します。

>[!NOTE]
>
>AEM Forms アプリケーション向けに Windows ファイルシステムに保存されるデータは、暗号化されていません。Windows BitLocker Drive Encryptionなどのサードパーティ製ツールを使用して、ディスクデータを暗号化することをお勧めします。

1. In the Visual Studio Standard Toolbar, select **Release** from the drop-down for build mode.

1. 使用しているプラットフォームに応じて Windows-AnyCPU、Windows-x64、または Windows-x86 を選択します。Windows-AnyCPU を選択することをお勧めします。
1. In the Visual Studio Solution Explorer, right-click the project **CordovaApp.Windows** and select **Store > Create AppPackages**.

   ![createapppackages](assets/createapppackages.png)

   アプリケーションパッケージの作成ウィザードが表示されます。

   CordovaApp.Windows_3.0.2.0_anycpu.appx インストーラーファイルが platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test ディレクトリに作成されます。

   If you encounter the error `Retarget to windows 8.1 required`, right-click the error and in the pop-up menu, select **Retarget To Windows 8.1**.

   ![リターゲット解](assets/retarget-solution.png)

1. アプリパッケージの作成ウィザードで、アプリを Windows ストアにアップロードするかどうか選択し、「**次へ**」をクリックします。

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 必要に応じて、バージョンやアプリのビルドの出力場所などのパラメーターを変更します。

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. プロジェクトのビルド後に、以下のプログラムを使用してアプリをインストールすることができます。

   * Windows PowerShell
   * Visual Studio

   The `.appx` package requires the following items to install successfully:

   1. WinJS ライブラリ
   1. WinJS のパッケージに、自己署名証明書または VeriSign などの信頼できる機関によって署名された公開証明書が付帯していることを確認してください。
   1. 開発者用のライセンス

   Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Testディレクトリには、4つの主要なコンポーネントが含まれています。

   1. `.appx` file
   1. 証明書（現在、Apache Cordovaによる自己署名証明書です）
   1. Dependency フォルダー
   1. PowerShell ファイル（.ps1 の拡張子）



## Windows PowerShell によるアプリのデプロイ {#deploying-an-app-using-windows-powershell}

Windows デバイスにアプリケーションをインストールするには、以下の 2 つの方法があります。

### 開発者用のライセンスを取得する方法 {#by-acquiring-the-developer-license}

1. Right-click on the PowerShell file ( `Add-AppDevPackage.ps1)`, and choose **Run with PowerShell**.

1. 開発者用のライセンスを取得するように求めるセットアップ画面が表示されます。Microsoft アカウントの資格情報を使用して、開発者用のライセンスを取得します。\
   このライセンスは 30 日間有効です。無料で更新することができます。
1. 開発者用のライセンスを取得すると、セットアップでシステムに自己署名証明書がインストールされ、アプリケーションが正常にインストールされます。

### 企業の所有するデバイスを使用する方法 {#by-using-enterprise-owned-devices}

企業のエンタープライズドメインに加入している企業の所有するデバイスの場合は、開発者用のライセンスを取得する必要はありません。

企業の所有するデバイスでは、Professional Edition または Enterprise Edition の Windows が使用されています。

Microsoft では VeriSign などの信頼できる機関が発行した公開証明書をインストールすることを推奨しています。

アプリをデプロイするには：

* デバイスがエンタープライズのドメインに参加していることを確認します。
* グループポリシー設定を有効にします。

**グループポリシー設定を有効にするには：**

1. In your device, run `gpedit.msc`.
1. **コンピューターの構成／管理用テンプレート／Windows コンポーネント／アプリケーションパッケージの展開**&#x200B;に移動します。
1. 「**信頼できるすべてのアプリケーションのインストールを許可する**」を右クリックします。
1. 「**編集**」をクリックし、「**有効**」を選択します。

1. 「**OK**」をクリックします。

次の手順で Visual Studio によって生成された PowerShell スクリプトを編集し、開発者用のライセンスを取得しないように設定します。

In the PowerShell script, set the variable: `$NeedDeveloperLicense = $false`.

ドメインに加入していないデバイスの場合は、製品のアクティベーションキーのサイドローディングが必要です。アクティベーションキーは Windows 販売店で購入することができます。

グループポリシーが存在せず、エンタープライズのサイドローディングが許可されていない Windows 8.1 Home Edition の場合は、エンタープライズドメインに加入することはできません。Windows 8.1 Home Edition にアプリケーションリをデプロイするには、開発者用のライセンスを使用してください。

詳しくは、[こちら](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)をクリックしてください。

## Visual Studio によるアプリのデプロイ {#deploying-an-app-using-visual-studio}

Visual Studio を使用して Windows にアプリをインストールするには：

1. リモートデバッガーを使用してデバイスに接続します。\
   For more information, see [Run Windows Store apps on a remote machine](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine).

1. Visual Studio でアプリケーションを開き、ソリューションプラットフォームリストで Windows-x64、Windows-x86、または Windows-AnyCPU を選択して「**リモートマシン**」を選択します。
1. リモートマシンにアプリケーションがデプロイされます。

