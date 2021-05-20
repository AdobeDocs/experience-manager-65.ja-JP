---
title: AEM Forms Android アプリケーションの構築
seo-title: AEM Forms Android アプリケーションの構築
description: Android Studio プロジェクトを設定し、Android 向け AEM Forms アプリケーションの .apk ファイルを構築するための手順
seo-description: Android Studio プロジェクトを設定し、Android 向け AEM Forms アプリケーションの .apk ファイルを構築するための手順
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 62%

---

# AEM Forms Android アプリケーションの構築 {#build-the-aem-forms-android-app}

AEM Forms Android アプリケーションを構築するには、以下の手順を、記載されている順序で実行します。

1. [AEM Forms アプリケーションのソースコードパッケージのダウンロード](#download-android-zip)
1. [環境変数の設定](#set-environment-variable-android)
1. [標準的な AEM Forms アプリケーションの構築](#set-up-the-xcode-project)

## AEM Forms アプリケーションのソースコードパッケージのダウンロード {#download-android-zip}

AEM Forms App Source Code Packageは`adobe-lc-mobileworkspace-src-<version>.zip`アーカイブを参照します。 このアーカイブにはカスタムの AEM Forms アプリケーションを構築するために必要なソースコードが含まれています。アーカイブは、ソフトウェアディストリビューションで入手可能な`adobe-aemfd-forms-app-src-pkg-<version>.zip`パッケージに含まれます。

`adobe-aemfd-forms-app-src-pkg-<version>.zip`ファイルをダウンロードするには、次の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 **[!UICONTROL ダウンロードの検索]**&#x200B;オプションを使用して、結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージ名をタップし、「**[!UICONTROL EULA利用条件]**&#x200B;に同意し、**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。
1. ソースコードアーカイブをダウンロードするには、ブラウザーで&#x200B;**https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip**&#x200B;を開きます。 Androidアプリの.zipファイルがデバイスにダウンロードされます。
1. ローカルファイルシステム上のフォルダーに .zip ファイルの内容を解凍します。例えば、*C:\&lt;Folder Structure>\adobe-lc-mobileworkspace-src-2.4.20*&#x200B;のようになります。

次の画像は、`adobe-lc-mobileworkspace-src-<version>.zip\android`フォルダーの構造を示しています。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 環境変数の設定 {#set-environment-variable-android}

AEM Forms アプリケーションの構築プロセスを開始する前に、次の環境変数を設定します。

* JAVA_HOME 環境変数を、ローカルファイルシステム上の JDK ソフトウェアの場所に設定します。例：C:\Program Files\Java\jdk1.8.0_181
* `ANDROID_SDK_ROOT`システム環境変数を、AndroidのSDKの場所に設定します。 例： C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* `Path` システム環境変数を、Android の platform-tools フォルダーおよび tools フォルダーに含めるように設定します。例： C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

adobe-lc-mobileworkspace-src-&lt;version>.zipファイルをローカルファイルシステムに保存し、環境変数を設定したら、次のいずれかのオプションを使用して、標準のAEM Forms Androidアプリを構築します。

* [Android Studio を使用した AEM Forms アプリケーションの構築](#using-android-studio)
* [Android Studio を使用した .apk ファイルの生成](#generate-apk-android-studio)

### Android Studio を使用した AEM Forms アプリケーションの構築 {#using-android-studio}

Android Studio を使用して AEM Forms アプリケーションを構築するには、次の手順を実行します。

1. お使いのマシンで Android Studio アプリケーションを起動します。
1. 「**Open an existing Android Studio project**」をクリックします。既存のプロジェクトを開くダイアログボックスが自動的に表示されない場合は、**File**／**Open** を選択します。
1. ローカルファイルシステム上の *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* に移動し、「**OK**」をクリックします。

    「**android**」オプションが左側のペインに表示されます。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 左側のウィンドウから&#x200B;**android**&#x200B;を選択し、****&#x200B;を実行/**「android」**&#x200B;を実行をクリックします。
1. Select Deployment Targetダイアログボックスの「Connected Devices」セクションからAndroidデバイスを選択し、「OK」をクリックします。

    開発環境を正しく構築すると、アプリケーションをカスタマイズできるようになります。アプリケーションをカスタマイズする場合は、次の記事を参照してください。

   * [ブランディングのカスタマイズ](/help/forms/using/branding-customization.md)
   * [テーマのカスタマイズ](/help/forms/using/theme-customization.md)
   * [ジェスチャーのカスタマイズ](/help/forms/using/gesture-customization.md)

   アプリケーションを適切にカスタマイズした後、.apk ファイルを生成して配布できます。

### Android Studio を使用した .apk ファイルの生成  {#generate-apk-android-studio}

Android Studio を使用して .apk ファイルを生成するには、次の手順を実行します。

1. お使いのマシンで Android Studio アプリケーションを起動します。
1. 「**既存のAndroid Studioプロジェクトを開く**」を選択します。 既存のプロジェクトを開くダイアログボックスが自動的に表示されない場合は、**File**／**Open** を選択します。
1. ローカルファイルシステム上の *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* に移動し、「**OK**」をクリックします。

    「android」オプションが左側のペインに表示されます。

1. **Build**／**Build APK**&#x200B;を選択し、.apk ファイルを生成します。

   必要に応じて、「**ビルド** / **署名済みAPKを生成**」を選択して、.apkファイルの[署名済みバージョン](https://developer.android.com/studio/publish/app-signing)を生成します。

## Android Debug Bridge の使用 {#build-android-debug-bridge}

.apkファイルが生成されたら、次のコマンドを実行して、[Android Debug Bridge](https://developer.android.com/tools/help/adb.html)を使用してAndroidデバイスにアプリケーションをインストールします。

**Windowsユーザー：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**MACユーザー：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
