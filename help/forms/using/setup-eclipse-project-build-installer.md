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
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 55%

---


# AEM Forms Android アプリケーションの構築 {#build-the-aem-forms-android-app}

AEM Forms Android アプリケーションを構築するには、以下の手順を、記載されている順序で実行します。

1. [AEM Forms アプリケーションのソースコードパッケージのダウンロード](#download-android-zip)
1. [環境変数の設定](#set-environment-variable-android)
1. [標準的な AEM Forms アプリケーションの構築](#set-up-the-xcode-project)

## AEM Forms アプリケーションのソースコードパッケージのダウンロード {#download-android-zip}

AEM Forms App Source Code Package refers to the `adobe-lc-mobileworkspace-src-<version>.zip` archive. このアーカイブにはカスタムの AEM Forms アプリケーションを構築するために必要なソースコードが含まれています。アーカイブは、ソフトウェア配布(Software Distribution)で使用可能な `adobe-aemfd-forms-app-src-pkg-<version>.zip`パッケージに含まれます。

Perform the following steps to download the `adobe-aemfd-forms-app-src-pkg-<version>.zip` file:

1. Open [Software Distribution](https://experience.adobe.com/downloads)（ソフトウェア配布）。 Adobe IDがソフトウェア配布物にログインする必要があります。
1. ヘッダーメニューで **[!UICONTROL Adobe Experience Manager]** をタップします。
1. In the **[!UICONTROL Filters]** section:
   1. 「 **[!UICONTROL ソリューション]** 」ドロップダウンリストから「 **[!UICONTROL フォーム]** 」を選択します。
   2. パッケージのバージョンと種類を選択します。 また、「 **[!UICONTROL 検索のダウンロード数]** 」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに対応するパッケージ名をタップし、「EULA条項に **[!UICONTROL 同意します]**」を選択して、「 **[!UICONTROL ダウンロード]**」をタップします。
1. パッ [ケージマネージャーを開き](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/contentmanagement/package-manager.html) 、「パッケージを **[!UICONTROL アップロード]** 」をクリックしてパッケージをアップロードします。
1. Select the package and click **[!UICONTROL Install]**.
1. To download the source-code archive, open **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** in your browser. Androidアプリの.zipファイルがデバイスにダウンロードされます。
1. ローカルファイルシステム上のフォルダーに .zip ファイルの内容を解凍します。For example, *C:\&lt;Folder Structure>\adobe-lc-mobileworkspace-src-2.4.20*

The following image displays the structure of the `adobe-lc-mobileworkspace-src-<version>.zip\android`folder.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 環境変数の設定 {#set-environment-variable-android}

AEM Forms アプリケーションの構築プロセスを開始する前に、次の環境変数を設定します。

* JAVA_HOME 環境変数を、ローカルファイルシステム上の JDK ソフトウェアの場所に設定します。例：C:\Program Files\Java\jdk1.8.0_181
* Set the `ANDROID_SDK_ROOT` system environment variable to the SDK location for Android. 例：C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* `Path` システム環境変数を、Android の platform-tools フォルダーおよび tools フォルダーに含めるように設定します。例えば、C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\toolsのように指定します。

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

adobe-lc-mobileworkspace-src-&lt;version>.zipファイルをローカルファイルシステムに保存し、環境変数を設定したら、次のいずれかのオプションを使用して、標準AEM FormsのAndroidアプリを作成します。

* [Android Studio を使用した AEM Forms アプリケーションの構築](#using-android-studio)
* [Android Studio を使用した .apk ファイルの生成](#generate-apk-android-studio)

### Android Studio を使用した AEM Forms アプリケーションの構築 {#using-android-studio}

Android Studio を使用して AEM Forms アプリケーションを構築するには、次の手順を実行します。

1. お使いのマシンで Android Studio アプリケーションを起動します。
1. 「**Open an existing Android Studio project**」をクリックします。既存のプロジェクトを開くダイアログボックスが自動的に表示されない場合は、**File**／**Open** を選択します。
1. ローカルファイルシステム上の *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* に移動し、「**OK**」をクリックします。

    「**android**」オプションが左側のペインに表示されます。

   ![android_folder_studio](assets/android_folder_studio.png)

1. Select **android** from the left pane and click **Run** > **Run &#39;android&#39;**.
1. デプロイメントTargetを選択ダイアログボックスの「接続されているデバイス」セクションでAndroidデバイスを選択し、「OK」をクリックします。

    開発環境を正しく構築すると、アプリケーションをカスタマイズできるようになります。アプリケーションをカスタマイズする場合は、次の記事を参照してください。

   * [ブランディングのカスタマイズ](/help/forms/using/branding-customization.md)
   * [テーマのカスタマイズ](/help/forms/using/theme-customization.md)
   * [ジェスチャーのカスタマイズ](/help/forms/using/gesture-customization.md)

   アプリケーションを適切にカスタマイズした後、.apk ファイルを生成して配布できます。

### Android Studio を使用した .apk ファイルの生成 {#generate-apk-android-studio}

Android Studio を使用して .apk ファイルを生成するには、次の手順を実行します。

1. お使いのマシンで Android Studio アプリケーションを起動します。
1. Select **Open an existing Android Studio project**. 既存のプロジェクトを開くダイアログボックスが自動的に表示されない場合は、**File**／**Open** を選択します。
1. ローカルファイルシステム上の *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* に移動し、「**OK**」をクリックします。

    「android」オプションが左側のペインに表示されます。

1. **Build**／**Build APK**&#x200B;を選択し、.apk ファイルを生成します。

   Optionally, Select **Build** > **Generate Signed APK** to generate a [signed version](https://developer.android.com/studio/publish/app-signing) of the .apk file.

## Android Debug Bridge の使用 {#build-android-debug-bridge}

Once the .apk file has been generated, execute the following command to install the application on an Android device using the [Android Debug Bridge](https://developer.android.com/tools/help/adb.html).

**Windowsユーザー：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**MACユーザー：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
