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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 61%

---


# Xcode プロジェクトの設定と iOS アプリケーションの構築{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムの AEM Forms アプリケーションを構築するためのすべてのコンポーネントが含まれています。ソースコードアーカイブ`adobe-lc-mobileworkspace-src-<version>.zip`は、ソフトウェア配布の`adobe-aemfd-forms-app-src-pkg-<version>.zip`パッケージの一部です。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。 ソフトウェアディストリビューションにログインするには、Adobe ID が必要です。
1. ヘッダーメニューにある&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して、結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに対応するパッケージ名をタップし、「**[!UICONTROL EULA条項に同意]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [Package Manager](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/contentmanagement/package-manager.html)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックして、パッケージをアップロードします。
1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

1. ソースコードアーカイブをダウンロードするには、ブラウザで`https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip`を開きます。
ソースパッケージがデバイスにダウンロードされます。

次の画像は、`adobe-lc-mobileworkspace-src-<version>.zip`の抽出された内容を示しています。

![mws-content](assets/mws-content.png)

次の表に、`adobe-lc-mobileworkspace-src-[version]/ios`フォルダーの内容を示します。

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

1. `adobe-lc-mobileworkspace-src-<version>.zip`アーカイブをダウンロードフォルダーから`[User_Home]/Projects/`にコピーします。
1. アーカイブを`[User_Home]/Projects/[your-project]`ディレクトリに展開します。
1. ` [User_Home]/Projects/ `[your-project]`/adobe-lc-mobileworkspace-src-[version]/ios`ディレクトリに移動します。
1. Xcode で `AEM Forms.xcodeproj` プロジェクトを開きます。
1. 「**TARGETS**」の「**AEM Forms**」をクリックし、**AEM Forms**」を選択します。「**ビルド設定**」タブを選択し、「**コード署名のエンタイトルメント**」セクションを探します。デバッグフィールドとリリースフィールドでは、次のいずれかを実行します。

   * 標準 Mobile Workspace アプリケーションを作成するための各フィールドを未指定のままにする。
   * [セキュアAEM Formsアプリを作成するためのセキュアAEM Formsアプリの作成](/help/forms/using/building-secure-mobile-workspace-app.md)の説明に従い、に対するフィールドを指定します。

1. 「**Build Settings**」タブで、「**All**」をクリックし、「**Combined**」をクリックします。
1. 「**Settings**」リストで、「**Code Signing**」を展開します。
1. 「**Code Signing Identity**」から、適切な署名を選択します。新しい署名の作成について詳しくは、「[開発版プロビジョニングプロファイルの作成とダウンロード](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)」を参照してください。
1. 「**Debug**」、「**Release**」、「**Any iOS SDK**」に同じ署名が選択されていることを確認します。
1. `AEM Forms-info.plist`ファイル内の次のコードを置き換えます。

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   `yourserver.com` をサーバーの適切なホスト名で置き換える際に、上記のコードを以下のコードに置き換えます。

   ```xml
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
   >この手順は、AEM Formsアプリがアプリ転送セキュリティの要件に従っていないサーバーに接続する必要がある場合にのみ必要です。

1. 「**PROJECT**」で「**AEM Forms**」を選択し、「**コード署名ID**」、「**デバッグ**」、「**リリース**」、「**任意のiOS SDK」が選択されていることを確認します。11/>.**
1. プロビジョニング済み iPad を Mac マシンに接続します。
1. **AEM Forms**&#x200B;プロジェクト用にプロビジョニングされたデバイスを選択します。

   ![ipad](assets/ipad.png)

   プロビジョニング済みデバイスの iPad Air 2 が選択されます。

1. 「**Product**」／「**Clean**」を選択します。
1. 「**Product**」／「**Build**」を選択します。

## AEM Forms アプリケーション用インストーラーの構築 {#build-the-installer-for-the-mobile-workspace-app}

 Xcode プロジェクトをアーカイブして、インストーラー（.ipa ファイル）とプロパティリストファイル（.plist ファイル）を構築する必要があります。プロパティリストファイルには、アプリケーションの名前やホストしているロケーションなど、ホストされているインハウスアプリケーションの設定情報が含まれます。 プロパティリストファイルについての詳細は、「[情報プロパティリストファイルについて](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)」を参照してください。

1. プロビジョニングされた iPad の Mac マシンへの接続iPadのプロビジョニングについて詳しくは、[開発版プロビジョニングプロファイルの作成とダウンロード](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)を参照してください。
1. **AEM Forms**&#x200B;プロジェクト用にプロビジョニングされたデバイスを選択します。

   ![ipad-1](assets/ipad-1.png)

   プロビジョニング済みデバイスの iPad Air 2 が選択されます。

1. 「**Product**」／「**Clean**」を選択します。
1. 「**Product**」／「**Build**」を選択します。
1. 「**Product**」／「**Archive**」を選択します。
1. Organizer - Archives で、プロジェクトの最新のアーカイブを選択し、「**Distribute**」をクリックします。
1. 「**Save for Enterprise or Ad-Hoc Deployment**」を配布手段として選択し、「**Next**」をクリックします。
1. 適切な「**Code Signing Identity**」を選択し、「**Next**」をクリックします。「**Allow**」をクリックして署名を適用します。
1. アプリケーションに名前をつけて、「**Save for Enterprise Distribution**」を選択します。
1. アプリケーションに&#x200B;**アプリケーション URL** を指定します。 例えば、CRXサーバー上でアプリをホストするには、URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`を指定します。
1. 「**タイトル**」フィールドで、AEM Forms を指定します。
1. 「**保存**」をクリックして Xcode を閉じます。

   インストーラーファイル `AEM Forms.ipa`、プロパティリストファイル `AEM Forms-info.plist` が指定された場所に作成されます。

1. `AEM Forms-info.plist`ファイルをエディターで開きます。
1. .ipa ファイルの URL のスペースをすべて %20 に置き換えます。
1. `AEM Forms-info.plist`ファイルを保存して閉じます。