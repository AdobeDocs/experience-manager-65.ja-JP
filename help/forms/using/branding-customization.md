---
title: ブランディングのカスタマイズ
seo-title: ブランディングのカスタマイズ
description: AEM Forms アプリケーションに対して組織固有の明確な外観と操作性を提供するために、アプリケーションアイコン、アプリケーション名、起動画像、ログインページをカスタマイズできます。
seo-description: AEM Forms アプリケーションに対して組織固有の明確な外観と操作性を提供するために、アプリケーションアイコン、アプリケーション名、起動画像、ログインページをカスタマイズできます。
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# ブランディングのカスタマイズ {#branding-customization}

アプリケーションアイコン、アプリケーション名、起動画像、ログインページをカスタマイズすることで、AEM Forms アプリケーションに組織固有のユニークな外観を与えることができます。例えば、組織のロゴを使用するために画像を変更できます。AEM Formsアプリケーションは、次のカスタマイズをサポートしています。

* アプリケーションアイコンと起動画像のカスタマイズ
* アプリケーション名のカスタマイズ
* ログインページの画像のカスタマイズ
* アプリケーションメニューのロゴのカスタマイズ

## アイコンと起動画像のカスタマイズ {#customizing-icon-and-launch-images}

次の手順を実行して、AEM Forms アプリケーションのデフォルトのアプリケーションアイコンと起動画像をカスタマイズします。

>[!NOTE]
>
>すべてのアイコンと起動画像で、ノンインターレースの PNG 形式を使用します。

### アイコンと起動画像をカスタマイズするには {#to-customize-icon-and-launch-images}

#### iOS の場合 {#for-ios}

1. Xcode で `Capture.xcodeproj` プロジェクトを開きます。
1. （***アイコンのカスタマイズの場合***）キャプチャのナビゲータービューで、**[!UICONTROL キャプチャ／キャプチャ／サポートするファイル／Capture-info.plist]** に移動します。アイコンファイルの横にあるドロップダウンをクリックします。 アイコンファイル（.png）の名前を指定し、**[!UICONTROL キャプチャ／キャプチャ／リソース／アイコン]**&#x200B;でファイルをアップロードします。現在サポートされているディメンションは次のとおりです。29x29、50x50、58x58、72x72、100x100、144x144。
1. （***起動画像のカスタマイズの場合***）画像のファイル名が次のいずれかであることを確認します。

   * 縦向きの場合： `Default-Portrait~ipad.png` および `Default-Portrait@2x~ipad.png`
   * 横置きの場合： `Default-Landscape~ipad.png` および `Default-Landscape@2x~ipad.png`
   これらのファイルをキャプチャプロジェクトにアップロードして、プロジェクトの既存のファイルと置き換えます。

   >[!NOTE]
   >
   >画像の名前と解像度が、プロジェクト内の置き換える画像と一致していることを確認します。

1. iOS デバイスまたは iOS シミュレーター上で AEM Forms アプリケーションを構築して実行します。

#### Android の場合 {#for-android}

1. アプリケーションのアイコンファイルに次の名前を付けます。

   `ic_launcher.png`

1. 対応するアイコンファイルを次のディレクトリに配置します。

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`
   >[!NOTE]
   >
   >画像の名前と解像度が、プロジェクト内の置き換える画像と一致していることを確認します。

1. AEM Forms アプリケーションを再構築します。

### Windows の場合 {#for-windows}

1. 次のパスにあるアイコンを置き換えます。

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. 次のパスにある起動画像を置き換えます。

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >画像の名前と解像度が、プロジェクト内の置き換える画像と一致していることを確認します。

1. AEM Forms アプリケーションを再構築します。

## アプリケーション名のカスタマイズ {#customize-the-app-name}

### iOS の場合 {#for-ios-1}

1. Xcode で `Capture.xcodeproj` プロジェクトを開きます。
1. Captureのナビゲータ表示で、Capture/Capture/ **[!UICONTROL Supporting Files/InfoPlist.stringsに移動します]**。

   属性の値を、アプリ `CFBundleDisplayName` に表示する名前に更新します。

1. iOS デバイスまたは iOS シミュレーター上で AEM Forms アプリケーションを構築して実行します。

   For details on building the app for iOS, see [Set up the Xcode project and build the iOS app](/help/forms/using/setup-xcode-project-build-installer.md).

### Android の場合 {#for-android-1}

1. テキストエディターまたは XML エディターで次の Xml ファイルを開きます。

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Update the value for the key `app_name`.
1. AEM Forms アプリケーションを再構築します。

   Andriod のアプリケーション構築について詳しくは、「[Eclipse プロジェクトの設定と Android アプリケーションの構築](/help/forms/using/setup-eclipse-project-build-installer.md)」を参照してください。

### Windows の場合 {#for-windows-1}

1. テキストエディターで次の Xml ファイルを開きます。

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Update the value in the `<name>...</name>` tag.
1. AEM Forms アプリケーションを再構築します。

   Windows 上でのアプリケーションの構築について詳しくは、「[Visual Studio プロジェクトの設定と Windows アプリケーションの構築](/help/forms/using/setup-visual-studio-project-build-installer.md)」を参照してください。

## ログインページの画像のカスタマイズ {#customizing-images-on-the-login-page}

AEM Formsアプリケーションのログインページには、ロゴと背景の画像が表示されます。 ロゴはログインダイアログボックスの上に配置されており、背景の画像はログインダイアログボックスの下に配置されています。次の手順を実行してログインページのデフォルトの画像をカスタマイズします。

**事前準備**

次の画像があることを確認します。

<table>
 <tbody>
  <tr>
   <th><p>説明</p> </th>
   <th><p>サイズ</p> </th>
   <th><p>ファイル名</p> </th>
  </tr>
  <tr>
   <td><p>Logo（ロゴ）</p> </td>
   <td><p>72 x 72 ピクセル</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>背景画像（縦長）</p> </td>
   <td><p>1280 x 989 ピクセル</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**Xcode を使用してログインページの画像をカスタマイズするには**

1. Xcode で `Capture.xcodeproj` プロジェクトを開きます。

1. `www/wsmobile/images` フォルダーに移動し、
1. ロゴを変更するには、デフォルトの `LC-logo.png` ファイルをカスタムの `LC-logo.png` ファイルに置き換えます。
1. To change background, replace the default `Landing_bg.jpeg` file with the custom `Landing_bg.jpeg`file.
1. iOS デバイスまたは iOS シミュレーター上で AEM Forms アプリケーションを構築して実行します。

### Eclipse を使用してログインページの画像をカスタマイズするには {#to-customize-images-on-the-login-pages-using-eclipse}

1. EclipseでAndroidプロジェクトを開きます。

1. `assets/www/wsmobile/images` フォルダーに移動し、
1. ロゴを変更するには、デフォルトの `LC-logo.png` ファイルをカスタムの `LC-logo.png` ファイルに置き換えます。
1. To change background, replace the default `Landing_bg.jpeg` file with the custom `Landing_bg.jpeg`file.
1. Android デバイス上で AEM Forms アプリケーションを構築して実行します。

### Visual Studio を使用してログインページの画像をカスタマイズするには {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Open the `MWSWindows.sln` project in Visual Studio.

1. `MWSWindows\www\wsmobile\images` フォルダーに移動し、
1. ロゴを変更するには、デフォルトの `LC-logo.png` ファイルをカスタムの `LC-logo.png` ファイルに置き換えます。
1. To change background, replace the default `Landing_bg.jpeg` file with the custom `Landing_bg.jpeg`file.
1. Windows デバイス上で AEM Forms アプリケーションを構築して実行します。

## アプリケーションメニューのロゴのカスタマイズ {#customizing_images_on_the_login_page-1}

AEM Forms アプリケーションにログインしてメニューボタンをタップすると、メニュー上にロゴが表示されます。次の手順を実行してデフォルトのロゴをカスタマイズします。

**事前準備**

次の画像があることを確認します。

<table>
 <tbody>
  <tr>
   <th><p>説明</p> </th>
   <th><p>サイズ</p> </th>
   <th><p>ファイル名</p> </th>
  </tr>
  <tr>
   <td><p>Logo（ロゴ）</p> </td>
   <td><p>72 x 72 ピクセル</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**Xcode を使用してログインページの画像をカスタマイズするには**

1. Xcode で `Capture.xcodeproj` プロジェクトを開きます。

1. `www/wsmobile/images` フォルダーに移動し、
1. To change the logo, replace the default `aem_icon.png` file with the custom `aem_icon.png` file.
1. iOS デバイスまたは iOS シミュレーター上で AEM Forms アプリケーションを構築して実行します。

### Eclipse を使用してログインページの画像をカスタマイズするには {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. EclipseでAndroidプロジェクトを開きます。

1. `assets/www/wsmobile/images` フォルダーに移動し、
1. To change the logo, replace the default `aem_icon.png` file with the custom `aem_icon.png` file.
1. Android デバイス上で AEM Forms アプリケーションを構築して実行します。

### Visual Studio を使用してログインページの画像をカスタマイズするには {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Open the `MWSWindows.sln` project in Visual Studio.

1. `MWSWindows\www\wsmobile\images` フォルダーに移動し、
1. To change the logo, replace the default `aem_icon.png` file with the custom `aem_icon.png` file.
1. Windows デバイス上で AEM Forms アプリケーションを構築して実行します。
