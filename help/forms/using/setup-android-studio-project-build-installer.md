---
title: Android Studio プロジェクトのセットアップと Android アプリの作成
seo-title: Android Studio プロジェクトのセットアップと Android アプリの作成
description: Android Studio プロジェクトのセットアップ手順と AEM Forms アプリケーションのインストーラーの作成手順
seo-description: Android Studio プロジェクトのセットアップ手順と AEM Forms アプリケーションのインストーラーの作成手順
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Android Studio プロジェクトのセットアップと Android アプリの作成 {#set-up-the-android-studio-project-and-build-the-android-app}

ここでは、バージョン 6.3.1.1 移行の AEM Forms アプリケーションを作成する手順について説明します。For building an app from source code of source code of the AEM Forms App 6.3, see [Set up the Eclipse project and build the Android™ app](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムの AEM Forms アプリケーションを構築するためのすべてのコンポーネントが含まれています。The source code archive, `adobe-lc-mobileworkspace-src-<version>.zip` is a part of the `adobe-aemfd-forms-app-src-pkg-<version>.zip` package on package share.

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. パッケージ共有に移動

   URL: `https://<server>:<port>/crx/packageshare`.

1. ソースパッケージをダウンロードします。パッケージをダウンロードすると、AEM Forms パッケージマネージャーに追加されます。
1. ダウンロード後、次の場所に移動します。をクリ `https://<server>:<port>/crx/packmgr/index.jsp`ックし、をインストールし `adobe-aemfd-forms-app-src-pkg-<version>.zip`ます。

1. ソースコードアーカイブをダウンロードするには、ブラウザ `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` ーで開いてください。

   ソースパッケージがデバイスにダウンロードされます。

The following image displays the extracted contents of the `adobe-lc-mobileworkspace-src-<version>.zip`.

![Zip 形式に圧縮された Android™ ソースの抽出されたコンテンツ](assets/mws-content-1.png)

The following image displays the directory structure of the `android`folder in the `src`folder.

![src 内の android フォルダーのディレクトリ構造](assets/android-folder.png)

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

1. Android™ Studio でプロジェクトを設定し、署名 ID を指定するには、以下の手順を実行します。

   設定済みの Android™ Studio がインストールされているマシンにログインします。

1. Copy the downloaded `adobe-lc-mobileworkspace-src-<version>.zip` archive to:

   **MACユーザーの場合**: `[User_Home]/Projects`

   **Windows®ユーザーの場合**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Windows® の場合は、Android プロジェクトをシステムドライブに保存することをお勧めします。

1. アーカイブを次のディレクトリに展開します。

   **MACユーザーの場合**: `[User_Home]/Projects/[your-project]`

   **Windows®ユーザーの場合**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >抽出した Android プロジェクトを Android Studio に読み込む前に、そのプロジェクトをシステムドライブに保存することをお勧めします。

1. Android™ Studio を起動します。

   **MACユーザーの場合**:フォルダー `local.properties` 内のファイルを更 `[User_Home]/Projects/[your-project]/android` 新し、デスクトップ上 `sdk.dir` の場所を変 `SDK` 数で指定してください。

   **Windows®ユーザーの場合**:フォルダー `local.properties` 内のファイルを更 `%HOMEPATH%\Projects\[your-project]\android` 新し、デスクトップ上 `sdk.dir` の場所を変 `SDK` 数で指定してください。

1. プロジェクトをビルドするには、「**[!UICONTROL 完了]**」をクリックします。

    プロジェクトが ADT Project Explorer で使用できるようになります。 

   ![アプリケーション構築後の eclipse プロジェクト](assets/eclipsebuildmws.png)

1. Android™ Studio で、「**[!UICONTROL Import Project (Eclipse ADT, Gradle, Etc.)]**」を選択します。
1. In the project explorer, select the root directory of the project that you want to build in the **Root Directory** text box:

   **Macユーザーの場合：**[User_Home]/Projects/MobileWorkspace/src/android

   **Windows®ユーザーの場合：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. プロジェクトの読み込みが完了すると、ポップアップが表示されます。このポップアップには、Android™ プラグインの Gradle を更新するためのオプションが表示されます。要件に応じて、適切なボタンをクリックします。

   ![このプロジェクトに対する](assets/dontremindmeagainforthisproject.png)

1. Gradle が正しく作成されると、以下の画面が表示されます。Connect the appropriate device or emulator with the system and click **[!UICONTROL Run Android™]**.

   ![格子底](assets/gradleconsole.png)

1. Android™ Studio に、接続デバイスと使用可能なエミュレーターが表示されます。アプリケーションを実行するデバイスを選択して「**OK**」をクリックします。

   ![connecteddevice](assets/connecteddevice.png)

プロジェクトの作成が完了したら、Android™ Debug Bridge または Android™ Studio を使用して、アプリケーションをインストールすることができます。

### Android™ Debug Bridge を使用する {#andriod-debug-bridge}

[Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) で以下のコマンドを使用して、アプリケーションを Android™ デバイスにインストールすることができます。

**MACユーザーの場合**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Windows®ユーザーの場合**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
