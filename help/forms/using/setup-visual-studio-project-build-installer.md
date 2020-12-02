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
ht-degree: 67%

---


# Visual Studio プロジェクトの設定と Windows アプリケーションの構築{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムワークスペースアプリケーションを構築するためのすべてのコンポーネントが含まれています。ソースコードアーカイブ`adobe-lc-mobileworkspace-src-<version>.zip`は、ソフトウェア配布の`adobe-aemfd-forms-app-src-pkg-<version>.zip`パッケージの一部です。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。 ソフトウェアディストリビューションにログインするには、Adobe ID が必要です。
1. ヘッダーメニューにある&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して、結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに対応するパッケージ名をタップし、「**[!UICONTROL EULA条項に同意]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [Package Manager](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/contentmanagement/package-manager.html)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックして、パッケージをアップロードします。
1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

1. ソースコードアーカイブをダウンロードするには、ブラウザで`https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip`を開きます。\
   ソースパッケージがデバイスにダウンロードされます。

次の画像は、`adobe-lc-mobileworkspace-src-<version>.zip`の抽出された内容を示しています。

![mws-content-1](assets/mws-content-1.png)

次の図は、`src`フォルダー内の`windows`フォルダーのディレクトリ構造を示しています。

![win-dir](assets/win-dir.png)

## 環境の設定 {#setting-up-the-environment}

Windows デバイスの場合、以下の環境が必要です。

* Microsoft Windows 8.1 または Windows 10
* Microsoft Visual Studio 2015
* Apache Cordova 向け Microsoft Visual Studio Tools

## AEM Forms アプリケーション向けの Visual Studio プロジェクトの設定  {#setting-up-visual-studio-project-for-aem-forms-app}

Visual Studio で AEM Forms アプリケーションのプロジェクトを設定するには、以下の手順を実行します。

1. Visual Studio 2015がインストールおよび構成されているWindows 8.1またはWindows 10デバイスの`adobe-lc-mobileworkspace-src-<version>.zip`フォルダーに`%HOMEPATH%\Projects`アーカイブをコピーします。
1. アーカイブを`%HOMEPATH%\Projects\MobileWorkspace`ディレクトリに展開します。
1. `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows`ディレクトリに移動します。
1. Visual Studio 2015を使用して`CordovaApp.sln`ファイルを開き、AEM Formsアプリの作成に進みます。

## AEM Forms アプリケーションの構築 {#build-aem-forms-app}

AEM Forms アプリケーションを構築しデプロイするには、次の手順を実行します。

>[!NOTE]
>
>AEM Forms アプリケーション向けに Windows ファイルシステムに保存されるデータは、暗号化されていません。Windows BitLocker Drive Encryptionなどのサードパーティ製ツールを使用して、ディスクデータを暗号化することをお勧めします。

1. Visual Studioの標準ツールバーで、ビルドモードのドロップダウンから「**リリース**」を選択します。

1. 使用しているプラットフォームに応じて Windows-AnyCPU、Windows-x64、または Windows-x86 を選択します。Windows-AnyCPU を選択することをお勧めします。
1. Visual Studio Solution Explorerで、プロジェクト&#x200B;**CordovaApp.Windows**&#x200B;を右クリックし、**ストア/AppPackagesを作成**&#x200B;を選択します。

   ![createapppackages](assets/createapppackages.png)

   アプリケーションパッケージの作成ウィザードが表示されます。

   CordovaApp.Windows_3.0.2.0_anycpu.appx インストーラーファイルが platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test ディレクトリに作成されます。

   エラー`Retarget to windows 8.1 required`が発生した場合は、エラーを右クリックし、ポップアップメニューで[**Windows 8.1にリターゲットする**]を選択します。

   ![リターゲット解](assets/retarget-solution.png)

1. アプリパッケージの作成ウィザードで、アプリを Windows ストアにアップロードするかどうか選択し、「**次へ**」をクリックします。

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 必要に応じて、バージョンやアプリのビルドの出力場所などのパラメーターを変更します。

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. プロジェクトのビルド後に、以下のプログラムを使用してアプリをインストールすることができます。

   * Windows PowerShell
   * Visual Studio

   `.appx`パッケージを正常にインストールするには、次のアイテムが必要です。

   1. WinJS ライブラリ
   1. WinJS のパッケージに、自己署名証明書または VeriSign などの信頼できる機関によって署名された公開証明書が付帯していることを確認してください。
   1. 開発者用のライセンス

   Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Testディレクトリには、4つの主要なコンポーネントが含まれています。

   1. `.appx` file
   1. 証明書（現在、Apache Cordovaによる自己署名証明書です）
   1. Dependency フォルダー
   1. PowerShell ファイル（.ps1 の拡張子）



## Windows PowerShell によるアプリのデプロイ  {#deploying-an-app-using-windows-powershell}

Windows デバイスにアプリケーションをインストールするには、以下の 2 つの方法があります。

### 開発者用のライセンスを取得する方法 {#by-acquiring-the-developer-license}

1. PowerShellファイル(`Add-AppDevPackage.ps1)`)を右クリックし、「**PowerShellで実行**」を選択します。

1. 開発者用のライセンスを取得するように求めるセットアップ画面が表示されます。Microsoft アカウントの資格情報を使用して、開発者用のライセンスを取得します。\
   このライセンスは 30 日間有効です。無料で更新することができます。
1. 開発者用のライセンスを取得すると、セットアップでシステムに自己署名証明書がインストールされ、アプリケーションが正常にインストールされます。

### 企業の所有するデバイスを使用する方法  {#by-using-enterprise-owned-devices}

企業のエンタープライズドメインに加入している企業の所有するデバイスの場合は、開発者用のライセンスを取得する必要はありません。

企業の所有するデバイスでは、Professional Edition または Enterprise Edition の Windows が使用されています。

Microsoft では VeriSign などの信頼できる機関が発行した公開証明書をインストールすることを推奨しています。

アプリをデプロイするには：

* デバイスがエンタープライズのドメインに参加していることを確認します。
* グループポリシー設定を有効にします。

**グループポリシー設定を有効にするには：**

1. デバイスで、`gpedit.msc`を実行します。
1. **コンピューターの構成／管理用テンプレート／Windows コンポーネント／アプリケーションパッケージの展開**&#x200B;に移動します。
1. 「**信頼できるすべてのアプリケーションのインストールを許可する**」を右クリックします。
1. 「**編集**」をクリックし、「**有効**」を選択します。

1. 「**OK**」をクリックします。

次の手順で Visual Studio によって生成された PowerShell スクリプトを編集し、開発者用のライセンスを取得しないように設定します。

PowerShellスクリプトで、次の変数を設定します。`$NeedDeveloperLicense = $false`.

ドメインに加入していないデバイスの場合は、製品のアクティベーションキーのサイドローディングが必要です。アクティベーションキーは Windows 販売店で購入することができます。

グループポリシーが存在せず、エンタープライズのサイドローディングが許可されていない Windows 8.1 Home Edition の場合は、エンタープライズドメインに加入することはできません。Windows 8.1 Home Edition にアプリケーションリをデプロイするには、開発者用のライセンスを使用してください。

詳しくは、[こちら](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)をクリックしてください。

## Visual Studio によるアプリのデプロイ  {#deploying-an-app-using-visual-studio}

Visual Studio を使用して Windows にアプリをインストールするには：

1. リモートデバッガーを使用してデバイスに接続します。\
   詳しくは、「[リモートマシンでWindowsストアアプリケーションを実行する](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)」を参照してください。

1. Visual Studio でアプリケーションを開き、ソリューションプラットフォームリストで Windows-x64、Windows-x86、または Windows-AnyCPU を選択して「**リモートマシン**」を選択します。
1. リモートマシンにアプリケーションがデプロイされます。

