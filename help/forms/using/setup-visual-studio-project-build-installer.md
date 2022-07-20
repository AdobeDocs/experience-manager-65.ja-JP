---
title: Visual Studio プロジェクトの設定と Windows アプリケーションの構築
seo-title: Set up the Visual Studio project and build the Windows app
description: Visual Studio プロジェクトを設定し、AEM Forms Windows モバイルデバイスアプリを構築する方法について学びます。
seo-description: Learn how to set up a Visual Studio project to build the AEM Forms Windows mobile device app.
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '911'
ht-degree: 100%

---

# Visual Studio プロジェクトの設定と Windows アプリケーションの構築{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムワークスペースアプリケーションを構築するためのすべてのコンポーネントが含まれています。ソースコードアーカイブ `adobe-lc-mobileworkspace-src-<version>.zip` は、ソフトウェアディストリビューションの `adobe-aemfd-forms-app-src-pkg-<version>.zip` パッケージの一部です。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージの名前をタップし、「**[!UICONTROL EULA 利用規約に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

1. ソースコードアーカイブをダウンロードするには、ブラウザーで `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` を開きます。\
   ソースパッケージがデバイスにダウンロードされます。

以下の画像は、`adobe-lc-mobileworkspace-src-<version>.zip` から抽出した内容を示しています。

![mws-content-1](assets/mws-content-1.png)

以下の画像は、`src` フォルダー内の `windows` フォルダーのディレクトリ構造を示しています。

![win-dir](assets/win-dir.png)

## 環境の設定 {#setting-up-the-environment}

Windows デバイスの場合、以下の環境が必要です。

* Microsoft Windows 8.1 または Windows 10
* Microsoft Visual Studio 2015
* Apache Cordova 向け Microsoft Visual Studio Tools

## AEM Forms アプリケーション向けの Visual Studio プロジェクトの設定 {#setting-up-visual-studio-project-for-aem-forms-app}

Visual Studio で AEM Forms アプリケーションのプロジェクトを設定するには、以下の手順を実行します。

1. Visual Studio 2015 がインストールおよび設定済みの Windows 8.1 または Windows 10 デバイスの `%HOMEPATH%\Projects` フォルダーに、`adobe-lc-mobileworkspace-src-<version>.zip` アーカイブをコピーします。
1. `%HOMEPATH%\Projects\MobileWorkspace` ディレクトリにアーカイブを抽出します。
1. `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` ディレクトリに移動します。
1. Visual Studio 2015 を使用して `CordovaApp.sln` ファイルを開き、AEM Forms アプリケーションの構築に進みます。

## AEM Forms アプリケーションの構築 {#build-aem-forms-app}

AEM Forms アプリケーションを構築しデプロイするには、次の手順を実行します。

>[!NOTE]
>
>AEM Forms アプリケーション向けに Windows ファイルシステムに保存されるデータは、暗号化されていません。Windows BitLocker Drive Encryption などのサードパーティのツールを使用して、ディスクのデータを暗号化することをお勧めします。

1. Visual Studio の標準ツールバーで、「ビルドモード」のドロップダウンリストから「**リリース**」を選択します。

1. 使用しているプラットフォームに応じて Windows-AnyCPU、Windows-x64、または Windows-x86 を選択します。Windows-AnyCPU を選択することをお勧めします。
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

1. プロジェクトのビルド後に、以下のプログラムを使用してアプリをインストールすることができます。

   * Windows PowerShell
   * Visual Studio

   `.appx` パッケージのインストールには、以下の項目が必要です。

   1. WinJS ライブラリ
   1. WinJS のパッケージに、自己署名証明書または VeriSign などの信頼できる機関によって署名された公開証明書が付帯していることを確認してください。
   1. 開発者用のライセンス

   4 つの主要なコンポーネントが、Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test ディレクトリに格納されています。

   1. `.appx` ファイル
   1. 証明書（現在 Apache Cordova の自己署名証明書が使用されています）
   1. Dependency フォルダー
   1. PowerShell ファイル（.ps1 の拡張子）



## Windows PowerShell によるアプリのデプロイ {#deploying-an-app-using-windows-powershell}

Windows デバイスにアプリケーションをインストールするには、以下の 2 つの方法があります。

### 開発者用ライセンスを取得する方法 {#by-acquiring-the-developer-license}

1. PowerShell ファイル（`Add-AppDevPackage.ps1)`）を右クリックして、「**PowerShell で実行**」を選択します。

1. 開発者用のライセンスを取得するように求めるセットアップ画面が表示されます。Microsoft アカウントの資格情報を使用して、開発者用のライセンスを取得します。\
   このライセンスは 30 日間有効です。無料で更新することができます。
1. 開発者用のライセンスを取得すると、セットアップでシステムに自己署名証明書がインストールされ、アプリケーションが正常にインストールされます。

### 企業の所有するデバイスを使用する方法 {#by-using-enterprise-owned-devices}

企業のエンタープライズドメインに加入している企業の所有するデバイスの場合は、開発者用のライセンスを取得する必要はありません。

企業の所有するデバイスでは、Professional Edition または Enterprise Edition の Windows が使用されています。

Microsoft では VeriSign などの信頼できる機関が発行した公開証明書をインストールすることを推奨しています。

アプリケーションをデプロイするには：

* デバイスがエンタープライズドメインに加入していることを確認します。
* グループポリシー設定を有効にします。

**グループポリシー設定を有効にするには：**

1. デバイス上で `gpedit.msc` を実行します。
1. **コンピューターの構成／管理用テンプレート／Windows コンポーネント／アプリケーションパッケージの展開**&#x200B;に移動します。
1. 「**信頼できるすべてのアプリケーションのインストールを許可する**」を右クリックします。
1. 「**編集**」をクリックし、「**有効**」を選択します。

1. 「**OK**」をクリックします。

次の手順で Visual Studio によって生成された PowerShell スクリプトを編集し、開発者用のライセンスを取得しないように設定します。

PowerShell スクリプトで、`$NeedDeveloperLicense = $false` の変数を設定します。

ドメインに加入していないデバイスの場合は、製品のアクティベーションキーのサイドローディングが必要です。アクティベーションキーは Windows 販売店で購入することができます。

グループポリシーが存在せず、エンタープライズのサイドローディングが許可されていない Windows 8.1 Home Edition の場合は、エンタープライズドメインに加入することはできません。Windows 8.1 Home Edition にアプリケーションリをデプロイするには、開発者用のライセンスを使用してください。

詳しくは、[こちら](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)をクリックしてください。

## Visual Studio によるアプリのデプロイ {#deploying-an-app-using-visual-studio}

Visual Studio を使用して Windows にアプリをインストールするには：

1. リモートデバッガーを使用してデバイスに接続します。\
   詳しくは、[リモートマシン上での Windows ストアアプリケーションの実行](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)を参照してください。

1. Visual Studio でアプリケーションを開き、ソリューションプラットフォームリストで Windows-x64、Windows-x86、または Windows-AnyCPU を選択して「**リモートマシン**」を選択します。
1. リモートマシンにアプリケーションがデプロイされます。
