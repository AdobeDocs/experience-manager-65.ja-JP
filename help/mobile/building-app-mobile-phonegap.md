---
title: モバイルアプリケーションのビルド
seo-title: Building Mobile Applications
description: このページでは、GitHub から入手可能なコードを使用してモバイルアプリケーションを構築する方法に関する詳細な手順を説明します。アプリケーションを構築して、デバイスやシミュレーターにインストールし、テストやアプリストアに公開します。 PhoneGap コマンドラインインターフェイスを使用して、またはPhoneGap Buildを使用してクラウド内で、アプリケーションをローカルに構築できます。
seo-description: This page provides a complete step-by-step article on how to build a mobile application using code available from GitHub is available here.Build your application to install to a device or simulator for testing or for publishing to app stores. You can build applications locally using the PhoneGap Command Line Interface, or in the cloud using PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 3%

---

# モバイルアプリケーションのビルド{#building-mobile-applications}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

アプリケーションをビルドして、テスト用またはアプリストアに公開用に、デバイスまたはシミュレーターにインストールします。 PhoneGap コマンドラインインターフェイスを使用して、またはPhoneGap Buildを使用してクラウド内で、アプリケーションをローカルに構築できます。

GitHub から入手可能なコードを使用してモバイルアプリケーションを構築する方法に関する詳細な手順記事を利用できます [ここ](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## パブリッシュインスタンスへのアプリの移動 {#moving-the-application-to-the-publish-instance}

アプリケーションファイルをパブリッシュインスタンスに移動して、インストールされているモバイルアプリケーションのインスタンスにコンテンツの更新を提供し、公開されたコンテンツを使用してアプリを構築できるようにします。 アプリケーションは、リポジトリ内の 2 つのノードブランチで構成されます。

* `/content/phonegap/apps/<application name>`:作成者が作成およびアクティブ化する Web ページ。
* `/content/phonegap/content/<application name>`:アプリケーション設定ファイルとコンテンツ同期設定。

>[!NOTE]
>
>アプリケーションファイルをパブリッシュインスタンスに移動しないと、コンテンツ作成者はコンテンツ同期キャッシュを更新できません。

必要なのは、 `/content/phonegap/content/<application name>` パブリッシュインスタンスにブランチします。 のファイル `/content/phonegap/apps/<application name>` ブランチは、作成者がページをアクティベートすると移動されます。

AEMには、コンテンツを一括でパブリッシュインスタンスに移動する方法が 2 つ用意されています。

* [「ツリーをアクティベート」コマンドを使用する](/help/sites-authoring/publishing-pages.md) レプリケーションコンソールの
* [パッケージの作成](/help/sites-administering/package-manager.md) コンテンツを格納し、パッケージをレプリケートします。

例えば、phonegapapp という名前のモバイルアプリケーションが作成されます。 次のノードをパブリッシュインスタンスに移動する必要があります。/content/phonegap/content/phonegapapp.

**ヒント：** パッケージをオーサーインスタンスからパブリッシュインスタンスに移動するには、パッケージで「レプリケート」コマンドを使用します。

![chlimage_1-16](assets/chlimage_1-16.png)

## PhoneGap コマンドラインインターフェイスを使用した構築 {#building-using-the-phonegap-command-line-interface}

PhoneGap コマンドラインインターフェイス (CLI) を使用して、コンピューター上で PhoneGap アプリケーションをコンパイルします。 AEMコンテンツをアプリケーションに含めるために、AEMは、モバイルアプリケーションのコンテンツ、コンテンツ同期設定、その他の必要なアセットを含む ZIP ファイルを作成します。 ZIP ファイルをダウンロードして、ビルドに含めます。

### ビルド環境の準備 {#preparing-your-build-environment}

PhoneGap CLI を使用してビルドするには、Node.js と PhoneGap クライアントユーティリティをインストールする必要があります。 次の手順を実行するには、インターネット接続が必要です。

1. ダウンロードとインストール [Node.js](https://nodejs.org/).
1. ターミナルまたはコマンドプロンプトを開き、次のノードコマンドを入力して PhoneGap ユーティリティをインストールします。

   ```shell
   npm install -g phonegap
   ```

   UNIX または Linux システムでは、コマンドの先頭にを付ける必要がある場合があります。 `sudo`.

   端末は、一連の HTTPGETコマンドの結果を示します。 インストールが正常に完了すると、次の例のように、ターミナルはライブラリのインストール先を示します。

   ```xml
   /usr/local/bin/phonegap -> /usr/local/lib/node_modules/phonegap/bin/phonegap.js
   phonegap@3.3.0-0.19.6 /usr/local/lib/node_modules/phonegap
   ├── pluralize@0.0.4
   ├── colors@0.6.0-1
   ├── semver@1.1.0
   ├── qrcode-terminal@0.9.4
   ├── shelljs@0.1.4
   ├── optimist@0.6.0 (...)
   ├── prompt@0.2.11 (...)
   ├── phonegap-build@0.8.4 (...)
   ├── connect-phonegap@0.8.1 (...)
   └── cordova@3.3.0-0.1.1 (...)
   ```

1. （オプション）ターゲットとするモバイルプラットフォーム用の SDK を取得します。

   * iOSプラットフォーム用のアプリを作成するには、最新バージョンのをインストールしてください [Xcode](https://developer.apple.com/xcode/).
   * Android アプリを作成するには、 [Android SDK](https://developer.android.com/).

### コンテンツ ZIP ファイルのダウンロード {#downloading-the-content-zip-file}

モバイルアプリケーションのコンテンツをファイルシステムに移動します。

1. モバイルアプリケーションページで、アプリケーションを選択します。
1. （オプション）完全なインストール用のアプリケーションを構築するには、ツールバーで、「キャッシュをクリア」アイコンをクリックまたはタップします。

   ![](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >キャッシュには、インストールされたアプリケーションのコンテンツの更新が格納されます。 キャッシュをクリアすると、キャッシュされたすべての更新が無効になります。

1. ツールバーの「 CLI Assets をダウンロード」アイコンをクリックまたはタップします。

   ![](do-not-localize/chlimage_1-1.png)

1. ZIP ファイルを保存したら、成功ダイアログの「閉じる」をクリックします。
1. ZIP ファイルの内容を抽出します。

### PhoneGap CLI を使用したビルド {#using-the-phonegap-cli-to-build}

PhoneGap CLI を使用して、アプリケーションをコンパイルしてインストールします。 PhoneGap CLI の使用方法について詳しくは、 PhoneGap [コマンドラインインターフェイス](https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html) ドキュメント。

1. ターミナルまたはコマンドプロンプトを開き、現在のディレクトリをダウンロードしたアプリケーションの ZIP ファイルに変更します。 例えば、次の例では、ディレクトリが ng-app-cli.1392137825303.zip ファイルに変更されます。

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. ターゲットとするプラットフォームの phonegap コマンドを入力します。 例えば、次のコマンドを実行すると、Android 用のアプリが構築されます。

   ```shell
   phonegap build android
   ```

## PhoneGap Buildを使用したビルド {#building-using-phonegap-build}

PhoneGap クラウドサービスを使用してアプリを構築します。 この手順を実行するには、まずPhoneGap Build設定を作成する必要があります。

### PhoneGap Build に接続しています {#connecting-to-phonegap-build}

AEM内でPhoneGap Buildサービスを使用できるようにPhoneGap Build設定を作成します。 モバイルアプリケーションの構築に使用するPhoneGap Buildアカウントのユーザー名とパスワードを指定します。

1. ツールページを開きます。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. 「CQ Operations」領域で、「Cloud Services」をクリックします。
1. 「今すぐ設定」リンクをクリックして、PhoneGap Buildを表示します。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 設定を作成ダイアログで、Title プロパティの値を入力します。 既定では、Name プロパティの値はタイトルから派生しますが、名前を入力することもできます。 「作成」をクリックします。
1. [PhoneGap Buildの設定 ] ダイアログで、PhoneGap Buildのユーザ名とパスワードを入力し、[OK] をクリックします。

### PhoneGap Buildの使用 {#using-phonegap-build}

様々なモバイルプラットフォーム向けにをコンパイルするために、アプリケーションリソースをPhoneGap Buildに送信します。

1. モバイルアプリケーションページで、モバイルアプリケーションを開きます。 ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. （オプション）完全なインストール用のアプリケーションを構築するには、アプリケーションを選択し、キャッシュをクリアアイコンをクリックします。

   ![](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >キャッシュには、インストールされたアプリケーションのコンテンツの更新が格納されます。 キャッシュをクリアすると、キャッシュされたすべての更新が無効になります。

1. スプラッシュページを選択し、「リモートビルド」アイコンをクリックします。

   ![](do-not-localize/chlimage_1-3.png)

   **注意：** ビルドが正常に完了した場合、AEM Beta バージョンではインボックス通知が作成されません。

1. 成功ダイアログボックスで、「PhoneGap Build」をクリックしてAdobe PhoneGap Buildページを開きます。 [https://build.phonegap.com/apps](https://build.phonegap.com/apps). アプリが表示されるのを待っている場合は、 [PhoneGap Buildステータス](https://status.build.phonegap.com/) ページ。

   ビルドのインストールについて詳しくは、 [PhoneGap Build文書](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build).

   >[!NOTE]
   >
   >無料のPhoneGap Buildアカウントは、1 つのプライベートアプリケーションで使用できます。 追加のプライベートアプリケーションを作成する場合、PhoneGap ビルドは失敗します。

### 次の手順 {#the-next-steps}

構築プロセスの次の手順は、 [アプリの構造](/help/mobile/phonegap-structure-an-app.md).
