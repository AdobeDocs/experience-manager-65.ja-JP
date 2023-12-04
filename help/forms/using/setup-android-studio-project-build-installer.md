---
title: Android&trade; studio プロジェクトを設定し、Android&trade；アプリを構築します。
description: Android&trade; Studio プロジェクトを設定し、Adobe Experience Manager (AEM) Formsアプリ用のインストーラーを構築する手順
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 58%

---

# Android™ Studio プロジェクトを設定し、Android™アプリを構築します。 {#set-up-the-android-studio-project-and-build-the-android-app}

ここでは、バージョン 6.3.1.1 移行の AEM Forms アプリケーションを作成する手順について説明します。AEM Forms App 6.3 のソースコードからアプリを構築する場合は、 [Eclipse プロジェクトの設定と Android™アプリの構築](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Formsは、AEM Formsアプリの完全なソースコードを提供します。 このソースには、カスタムの AEM Forms アプリケーションを構築するためのすべてのコンポーネントが含まれています。ソースコードアーカイブ `adobe-lc-mobileworkspace-src-<version>.zip` は、ソフトウェア配布の `adobe-aemfd-forms-app-src-pkg-<version>.zip` パッケージの一部です。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行してください。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. 選択 **[!UICONTROL Adobe Experience Manager]** は、ヘッダーメニューで使用できます。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージ名を選択し、「 」を選択します。 **[!UICONTROL 使用許諾契約書に同意する]**&#x200B;をクリックし、次を選択します。 **[!UICONTROL ダウンロード]**.
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して、**[!UICONTROL インストール]**&#x200B;をクリックします。

次の画像は、`adobe-lc-mobileworkspace-src-<version>.zip` から抽出した内容を示しています。

![ZIP 形式に圧縮された Android™ ソースの抽出されたコンテンツ](assets/mws-content-1.png)

次の画像は、`src`フォルダー内の `android`フォルダーのディレクトリ構造を示しています。

![src 内の Android フォルダーのディレクトリ構造](assets/android-folder.png)

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

1. 次の手順を実行して、Android™ Studio でプロジェクトを設定し、署名 ID を指定します。

   Android™ Studio がインストールおよび設定されているマシンにログインします。

1. ダウンロードした `adobe-lc-mobileworkspace-src-<version>.zip` アーカイブを次の場所にコピーします。

   **Macユーザー向け**: `[User_Home]/Projects`

   **Windows®ユーザーの場合**：`%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Windows®の場合は、Android™プロジェクトをシステムドライブに保持することをお勧めします。

1. アーカイブを次のディレクトリに展開します。

   **Macユーザー向け**: `[User_Home]/Projects/[your-project]`

   **Windows®ユーザーの場合**：`%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   プロジェクトを Android™ Studio に読み込む前に、抽出した Android プロジェクトをシステムドライブに保持することをお勧めします。

1. Android™ Studio を起動します。

   **Macユーザー向け**：を更新します。 `local.properties` ファイルが `[User_Home]/Projects/[your-project]/android` フォルダーとポイント `sdk.dir` 変数を `SDK` の場所を指定します。

   **Windows® ユーザーの場合**：`%HOMEPATH%\Projects\[your-project]\android` フォルダー内の `local.properties` ファイルを更新用に開き、デスクトップ上の `SDK` の場所を指すように `sdk.dir` 変数を編集します。

1. プロジェクトをビルドするには、**[!UICONTROL 完了]**&#x200B;をクリックします。

   プロジェクトが ADT Project Explorer で使用できるようになります。 

   ![アプリケーション構築後の Eclipse プロジェクト](assets/eclipsebuildmws.png)

1. Android™ Studio で、**[!UICONTROL Import Project (Eclipse ADT, Gradle, Etc.)]** を選択します。
1. プロジェクトエクスプローラーの「**Root Directory**」テキストボックスで、作成するプロジェクトのルートディレクトリを選択します。

   **Mac ユーザーの場合：** [User_Home]/Projects/MobileWorkspace/src/android

   **Windows® ユーザーの場合：** %HOMEPATH%¥Projects¥MobileWorkspace¥src¥android

1. プロジェクトが読み込まれると、Android™プラグイン Gradle を更新するためのオプションがポップアップ表示されます。 必要に応じて、適切なボタンをクリックします。

   ![dontremindmeagainforthisproject](assets/dontremindmeagainforthisproject.png)

1. Gradle が正しく作成されると、以下の画面が表示されます。適切なデバイスまたはエミュレーターをシステムに接続し、「**[!UICONTROL Android™ を実行]**」をクリックします。

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio に、接続デバイスと使用可能なエミュレーターが表示されます。アプリケーションを実行するデバイスを選択して **OK** をクリックします。

   ![connecteddevice](assets/connecteddevice.png)

プロジェクトの作成が完了したら、Android™ Debug Bridge または Android™ Studio を使用して、アプリケーションをインストールすることができます。

### Android™ Debug Bridge を使用する {#andriod-debug-bridge}

Android™デバイスにアプリケーションをインストールするには、 [Android™ Debug Bridge](https://developer.android.com/tools/adb) 次のコマンドを使用します。

**Macユーザー向け**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Windows®ユーザーの場合**：`adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
