---
title: AEM Forms Android アプリケーションの構築
description: Android Studio プロジェクトを設定し、Android 向け AEM Forms アプリケーションの .apk ファイルを構築するための手順
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 100%

---

# AEM Forms Android アプリケーションの構築 {#build-the-aem-forms-android-app}

AEM Forms 用の Android アプリを構築するには、次の手順を推奨される順序で実行します。

1. [AEM Forms アプリケーションのソースコードパッケージのダウンロード](#download-android-zip)
1. [環境変数の設定](#set-environment-variable-android)
1. [標準的な AEM Forms アプリケーションの構築](#set-up-the-xcode-project)

## AEM Forms アプリケーションのソースコードパッケージのダウンロード {#download-android-zip}

AEM Forms アプリケーションのソースコードパッケージは `adobe-lc-mobileworkspace-src-<version>.zip` アーカイブを参照します。このアーカイブにはカスタムの AEM Forms アプリケーションを構築するために必要なソースコードが含まれています。アーカイブは、「ソフトウェア配布」で入手できる `adobe-aemfd-forms-app-src-pkg-<version>.zip` パッケージに含まれています。

`adobe-aemfd-forms-app-src-pkg-<version>.zip` ファイルをダウンロードするには、次の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」を選択します。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適した Forms アドオンパッケージの名前を選択し、「**[!UICONTROL EULA 利用条件に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」を選択します。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。
1. ソースコードアーカイブをダウンロードするには、ブラウザーで **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zipp** を開きます。Android アプリケーションの .zip ファイルがお使いのデバイスにダウンロードされます。
1. ローカルファイルシステム上のフォルダーに .zip ファイルの内容を解凍します。例：*C:\&lt;Folder Structure>\adobe-lc-mobileworkspace-src-2.4.20*

次の画像は、`adobe-lc-mobileworkspace-src-<version>.zip\android` フォルダーの構造を示しています。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 環境変数の設定 {#set-environment-variable-android}

AEM Forms アプリケーションの構築プロセスを開始する前に、次の環境変数を設定します。

* JAVA_HOME 環境変数を、ローカルファイルシステム上の JDK ソフトウェアの場所に設定します（C:\Program Files\Java\jdk1.8.0_181 など）。
* `ANDROID_SDK_ROOT` システム環境変数を、Android の SDK の場所に設定します。例：C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* `Path` システム環境変数を、Android の platform-tools フォルダーおよび tools フォルダーに含めるように設定します。例：C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools および C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

adobe-lc-mobileworkspace-src-&lt;version>.zip ファイルをローカルファイルシステムに保存し、環境変数を設定した後、次のいずれかのオプションを使用して、標準的な AEM Forms Android アプリケーションを構築します。

* [Android Studio を使用した AEM Forms アプリケーションの構築](#using-android-studio)
* [Android Studio を使用した .apk ファイルの生成](#generate-apk-android-studio)

### Android Studio を使用した AEM Forms アプリケーションの構築 {#using-android-studio}

Android Studio を使用して AEM Forms アプリを構築するには、次の手順を実行します。

1. お使いのマシンで Android Studio アプリケーションを起動します。
1. 「**Open an existing Android Studio project**」をクリックします。既存のプロジェクトを開くダイアログボックスが自動的に表示されない場合は、**File**／**Open** を選択します。
1. ローカルファイルシステム上の *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* に移動し、「**OK**」をクリックします。

    「**android**」オプションが左側のペインに表示されます。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 左側のペインで「**android**」を選択し、**Run**／**Run &#39;android&#39;** をクリックします。
1. Select Deployment Target ダイアログボックスの「Connected Devices」セクションで Android デバイスを選択し、「OK」をクリックします。

   開発環境を正しく構築すると、アプリケーションをカスタマイズできるようになります。アプリケーションをカスタマイズする場合は、次の記事を参照してください。

   * [ブランディングのカスタマイズ](/help/forms/using/branding-customization.md)
   * [テーマのカスタマイズ](/help/forms/using/theme-customization.md)
   * [ジェスチャのカスタマイズ](/help/forms/using/gesture-customization.md)

   アプリケーションを適切にカスタマイズした後、.apk ファイルを生成して配布できます。

### Android Studio を使用した .apk ファイルの生成 {#generate-apk-android-studio}

Android Studio を使用して.apk ファイルを生成するには、以下の手順を実行します。

1. お使いのマシンで Android Studio アプリケーションを起動します。
1. 「**Open an existing Android Studio project**」を選択します。既存のプロジェクトを開くダイアログボックスが自動的に表示されない場合は、**File**／**Open** を選択します。
1. ローカルファイルシステム上の *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* に移動し、「**OK**」をクリックします。

    「android」オプションが左側のペインに表示されます。

1. .apk ファイルを生成するには、**ビルド**／**APK の構築**&#x200B;を選択します。

   オプションで、**Build**／**Generate Signed APK** を選択し、.apk ファイルの[署名バージョン](https://developer.android.com/studio/publish/app-signing)を生成することもできます。

## Android Debug Bridge の使用 {#build-android-debug-bridge}

.apk ファイルの生成後、次のコマンドを実行して、[Android Debug Bridge](https://developer.android.com/tools/adb) を使用して Android デバイスにアプリケーションをインストールします。

**Windows ユーザー：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Mac ユーザー：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
