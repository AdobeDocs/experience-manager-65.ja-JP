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
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 65%

---

# Android Studio プロジェクトのセットアップと Android アプリの作成 {#set-up-the-android-studio-project-and-build-the-android-app}

ここでは、バージョン 6.3.1.1 移行の AEM Forms アプリケーションを作成する手順について説明します。AEM Forms App 6.3のソースコードからアプリを構築する場合は、「 [Eclipseプロジェクトの設定とAndroid™アプリの構築](/help/forms/using/setup-eclipse-project-build-installer.md) 」を参照してください。

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムの AEM Forms アプリケーションを構築するためのすべてのコンポーネントが含まれています。ソースコードアーカイブ`adobe-lc-mobileworkspace-src-<version>.zip`は、ソフトウェア配布の`adobe-aemfd-forms-app-src-pkg-<version>.zip`パッケージの一部です。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 **[!UICONTROL ダウンロードの検索]**&#x200B;オプションを使用して、結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージ名をタップし、「**[!UICONTROL EULA利用条件]**&#x200B;に同意し、**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

次の画像は、`adobe-lc-mobileworkspace-src-<version>.zip`の抽出されたコンテンツを示しています。

![Zip 形式に圧縮された Android™ ソースの抽出されたコンテンツ](assets/mws-content-1.png)

次の画像は、`src`フォルダー内の`android`フォルダーのディレクトリ構造を示しています。

![src 内の android フォルダーのディレクトリ構造](assets/android-folder.png)

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

1. Android™ Studio でプロジェクトを設定し、署名 ID を指定するには、以下の手順を実行します。

   設定済みの Android™ Studio がインストールされているマシンにログインします。

1. ダウンロードした`adobe-lc-mobileworkspace-src-<version>.zip`アーカイブを次の場所にコピーします。

   **MACユーザーの場合**:  `[User_Home]/Projects`

   **Windows®ユーザーの場合**:  `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Windows® の場合は、Android プロジェクトをシステムドライブに保存することをお勧めします。

1. アーカイブを次のディレクトリに展開します。

   **MACユーザーの場合**:  `[User_Home]/Projects/[your-project]`

   **Windows®ユーザーの場合**:  `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >抽出した Android プロジェクトを Android Studio に読み込む前に、そのプロジェクトをシステムドライブに保存することをお勧めします。

1. Android™ Studio を起動します。

   **MACユーザーの場合**:フォルダー `local.properties` 内のファイルを更新 `[User_Home]/Projects/[your-project]/android` し、デスクトップ上の場 `sdk.dir` 所を指 `SDK` 定します。

   **Windows®ユーザーの場合**:フォルダー `local.properties` 内のファイルを更新 `%HOMEPATH%\Projects\[your-project]\android` し、デスクトップ上の場 `sdk.dir` 所を指 `SDK` 定します。

1. プロジェクトをビルドするには、「**[!UICONTROL 完了]**」をクリックします。

    プロジェクトが ADT Project Explorer で使用できるようになります。 

   ![アプリケーション構築後の eclipse プロジェクト](assets/eclipsebuildmws.png)

1. Android™ Studio で、「**[!UICONTROL Import Project (Eclipse ADT, Gradle, Etc.)]**」を選択します。
1. プロジェクトエクスプローラーで、「**ルートディレクトリ**」テキストボックスで、ビルドするプロジェクトのルートディレクトリを選択します。

   **Macユーザーの場合：** [User_Home]/Projects/MobileWorkspace/src/android

   **Windows®ユーザーの場合：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. プロジェクトの読み込みが完了すると、ポップアップが表示されます。このポップアップには、Android™ プラグインの Gradle を更新するためのオプションが表示されます。要件に応じて、適切なボタンをクリックします。

   ![このプロジェクトに対する動き](assets/dontremindmeagainforthisproject.png)

1. Gradle が正しく作成されると、以下の画面が表示されます。適切なデバイスまたはエミュレーターをシステムに接続し、「**[!UICONTROL Android™]**&#x200B;を実行」をクリックします。

   ![格子底](assets/gradleconsole.png)

1. Android™ Studio に、接続デバイスと使用可能なエミュレーターが表示されます。アプリケーションを実行するデバイスを選択して「**OK**」をクリックします。

   ![connecteddevice](assets/connecteddevice.png)

プロジェクトの作成が完了したら、Android™ Debug Bridge または Android™ Studio を使用して、アプリケーションをインストールすることができます。

### Android™ Debug Bridge を使用する {#andriod-debug-bridge}

[Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) で以下のコマンドを使用して、アプリケーションを Android™ デバイスにインストールすることができます。

**MACユーザーの場合**:  `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Windows®ユーザーの場合**:  `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
