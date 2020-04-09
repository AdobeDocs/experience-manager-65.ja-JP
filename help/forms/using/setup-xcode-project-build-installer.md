---
title: Xcode プロジェクトの設定と iOS アプリケーションの構築
seo-title: Xcode プロジェクトの設定と iOS アプリケーションの構築
description: 標準的な AEM Forms アプリケーション（iOS 用）の構築方法を説明します。
seo-description: 標準的な AEM Forms アプリケーション（iOS 用）の構築方法を説明します。
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
translation-type: tm+mt
source-git-commit: 72a582b7ac19322b81fd1a92de8fce34e55b9db1

---


# Xcode プロジェクトの設定と iOS アプリケーションの構築{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムの AEM Forms アプリケーションを構築するためのすべてのコンポーネントが含まれています。The source code archive, `adobe-lc-mobileworkspace-src-<version>.zip` is a part of the `adobe-aemfd-forms-app-src-pkg-<version>.zip` package on package share.

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. パッケージshareURLに移動： `https://<server>:<port>/crx/packageshare`.

1. ソースパッケージをダウンロードします。パッケージをダウンロードすると、AEM Forms パッケージマネージャーに追加されます。
1. ダウンロード後、次の場所に移動します。をクリ `https://<server>:<port>/crx/packmgr/index.jsp`ックし、をインストールし `adobe-aemfd-forms-app-src-pkg-<version>.zip`ます。

1. ソースコードアーカイブをダウンロードするには、ブラウザ `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` ーで開いてください。
ソースパッケージがデバイスにダウンロードされます。

The following image displays the extracted contents of the `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

The following table details contents of the `adobe-lc-mobileworkspace-src-[version]/ios` folder.

<table>
 <tbody>
  <tr>
   <th><p>ディレクトリ</p> </th>
   <th><p>コンテンツ</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>PhoneGap SDK 6.4.0</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>リソース、PhoneGap プラグイン、およびアプリケーションのメインモジュール</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>AEM Forms アプリケーション用 Xcode プロジェクト</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>AEM Forms アプリケーション プロジェクト用 HTML、CSS、画像、および JavaScript ファイル</p> </td>
  </tr>
 </tbody>
</table>

コード署名と iOS プロビジョニングポータルへのデバイスの追加について詳しくは、[iOS コード署名の設定、処理、トラブルシューティング](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)を参照してください。

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

1. 以下の手順を実行して、Xcode でプロジェクトを設定し、署名 ID を決定します。

   XcodeとiOS SDKがインストールおよび設定されているMacマシンにログインします。

1. Copy the `adobe-lc-mobileworkspace-src-<version>.zip` archive from the downloads folder to `[User_Home]/Projects/`.
1. Extract the archive in the `[User_Home]/Projects/[your-project]`directory.
1. プロジェクトデ ` [User_Home]/Projects/ `[ィレクトリに移動]`/adobe-lc-mobileworkspace-src-[version]/ios` します。
1. Xcode で `AEM Forms.xcodeproj` プロジェクトを開きます。
1. 「**TARGETS**」の「**AEM Forms**」をクリックし、**AEM Forms**」を選択します。Select the **Build Settings** tab, locate the **Code Signing Entitlement** section, and in Debug and Release fields do one of the following:

   * 標準 Mobile Workspace アプリケーションを作成するための各フィールドを未指定のままにする。
   * Specify the fields to as explained in [Building a Secure AEM Forms app for iOS](/help/forms/using/building-secure-mobile-workspace-app.md) to build a secure AEM Forms app.

1. 「**Build Settings**」タブで、「**All**」をクリックし、「**Combined**」をクリックします。
1. 「**Settings**」リストで、「**Code Signing**」を展開します。
1. 「**Code Signing Identity**」から、適切な署名を選択します。For detailed information about, creating new signatures, see [Creating and Downloading Development Provisioning Profiles](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. 「**Debug**」、「**Release**」、「**Any iOS SDK**」に同じ署名が選択されていることを確認します。
1. Replace the following code in the `AEM Forms-info.plist` file:

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   `yourserver.com` をサーバーの適切なホスト名で置き換える際に、上記のコードを以下のコードに置き換えます。

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >この手順は、AEM Formsアプリケーションが、アプリケーション転送セキュリティの要件に従わないサーバーに接続する必要がある場合にのみ必要です。

1. Under **PROJECT**, select **AEM Forms** and ensure that the appropriate signature is selected for **Code Signing Identity**, **Debug**, **Release** and **Any iOS SDK**.
1. プロビジョニング済み iPad を Mac マシンに接続します。
1. **AEM Formsプロジェクトのプロビジョニングされたデバイスを選択します** 。

   ![ipad](assets/ipad.png)

   プロビジョニング済みデバイスの iPad Air 2 が選択されます。

1. 「**Product**」／「**Clean**」を選択します。
1. 「**Product**」／「**Build**」を選択します。

## AEM Forms アプリケーション用インストーラーの構築 {#build-the-installer-for-the-mobile-workspace-app}

 Xcode プロジェクトをアーカイブして、インストーラー（.ipa ファイル）とプロパティリストファイル（.plist ファイル）を構築する必要があります。プロパティリストファイルには、アプリケーションの名前やホストしているロケーションなど、ホストされているインハウスアプリケーションの設定情報が含まれます。 プロパティリストファイルについての詳細は、「[情報プロパティリストファイルについて](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)」を参照してください。

1. プロビジョニングされた iPad の Mac マシンへの接続For detailed information about provisioning an iPad, see [Creating and Downloading Development Provisioning Profiles](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. **AEM Formsプロジェクトのプロビジョニングされたデバイスを選択します** 。

   ![ipad-1](assets/ipad-1.png)

   プロビジョニング済みデバイスの iPad Air 2 が選択されます。

1. 「**Product**」／「**Clean**」を選択します。
1. 「**Product**」／「**Build**」を選択します。
1. 「**Product**」／「**Archive**」を選択します。
1. Organizer - Archives で、プロジェクトの最新のアーカイブを選択し、「**Distribute**」をクリックします。
1. 「**Save for Enterprise or Ad-Hoc Deployment**」を配布手段として選択し、「**Next**」をクリックします。
1. 適切な「**Code Signing Identity**」を選択し、「**Next**」をクリックします。「**Allow**」をクリックして署名を適用します。
1. アプリケーションに名前をつけて、「**Save for Enterprise Distribution**」を選択します。
1. アプリケーションに&#x200B;**アプリケーション URL** を指定します。 For example, to host the app on a CRX server, provide URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. 「**タイトル**」フィールドで、AEM Forms を指定します。
1. 「**保存**」をクリックして Xcode を閉じます。

   インストーラーファイル `AEM Forms.ipa`、プロパティリストファイル `AEM Forms-info.plist` が指定された場所に作成されます。

1. Open the `AEM Forms-info.plist` file in an editor.
1. .ipa ファイルの URL のスペースをすべて %20 に置き換えます。
1. Save and close the `AEM Forms-info.plist` file.