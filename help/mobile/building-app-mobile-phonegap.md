---
title: モバイルアプリケーションのビルド
description: このページでは、GitHub から入手できるコードを使用してモバイルアプリケーションを構築する方法を、順を追って詳しく説明します。この記事はここから入手できます。 テスト用またはアプリストアへの公開用にデバイスまたはシミュレーターにインストールするアプリケーションを作成します。 PhoneGap コマンドラインインターフェイスを使用してローカルで、またはPhoneGap Buildを使用してクラウドでアプリケーションを構築できます。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 1%

---

# モバイルアプリケーションのビルド{#building-mobile-applications}

{{ue-over-mobile}}

テスト用またはアプリストアへの公開用にデバイスまたはシミュレーターにインストールするアプリケーションを作成します。 PhoneGap コマンドラインインターフェイスを使用してローカルで、またはPhoneGap Buildを使用してクラウドでアプリケーションを構築できます。

GitHub から入手できるコードを使用してモバイルアプリケーションを構築する方法を説明する詳細な手順の記事は、[&#x200B; こちら &#x200B;](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html) から入手できます。

## アプリケーションのPublish インスタンスへの移動 {#moving-the-application-to-the-publish-instance}

モバイルアプリケーションのインストール済みインスタンスにコンテンツの更新を提供したり、公開済みコンテンツを使用してアプリケーションを構築したりできるように、アプリケーションファイルをパブリッシュインスタンスに移動します。 アプリケーションは、リポジトリ内の次の 2 つのノードブランチで構成されます。

* `/content/phonegap/apps/<application name>`：作成者が作成およびアクティブ化する web ページ。
* `/content/phonegap/content/<application name>`：アプリケーション設定ファイルとコンテンツ同期設定。

>[!NOTE]
>
>アプリケーションファイルをパブリッシュインスタンスに移動しない場合、コンテンツ作成者はコンテンツ同期のキャッシュを更新できません。

`/content/phonegap/content/<application name>` ブランチのファイルをパブリッシュインスタンスに移動するだけです。 `/content/phonegap/apps/<application name>` ブランチ内のファイルは、作成者がページをアクティベートすると移動されます。

AEMには、一括コンテンツをパブリッシュインスタンスに移動するための 2 つの方法が用意されています。

* レプリケーションコンソールで [&#x200B; 「ツリーをアクティベート」コマンドを使用 &#x200B;](/help/sites-authoring/publishing-pages.md) します。
* コンテンツを含む [&#x200B; パッケージを作成 &#x200B;](/help/sites-administering/package-manager.md) し、パッケージをレプリケートします。

例えば、phonegapapp という名前のモバイルアプリケーションが作成されます。 次のノードをパブリッシュインスタンスに移動する必要があります：/content/phonegap/content/phonegapapp。

**ヒント：** パッケージをオーサーインスタンスからパブリッシュインスタンスに移動するには、パッケージに対して「レプリケート」コマンドを使用します。

![chlimage_1-16](assets/chlimage_1-16.png)

## PhoneGap コマンドラインインターフェイスを使用した構築 {#building-using-the-phonegap-command-line-interface}

PhoneGap Command-Line Interface （CLI）を使用して、コンピュータ上で PhoneGap アプリケーションをコンパイルします。 AEM コンテンツをアプリケーションに含めるには、AEMがモバイルアプリケーションのコンテンツ、コンテンツ同期設定、その他の必要なアセットを含む ZIP ファイルを作成します。 ZIP ファイルをダウンロードし、ビルドに含めます。

### ビルド環境の準備 {#preparing-your-build-environment}

PhoneGap CLI を使用してビルドするには、Node.js と PhoneGap クライアントユーティリティをインストールする必要があります。 次の手順を実行するには、インターネット接続が必要です。

1. [Node.js](https://nodejs.org/ja) をダウンロードしてインストールします。
1. ターミナルまたはコマンドプロンプトを開き、次のノードコマンドを入力して PhoneGap ユーティリティをインストールします。

   ```shell
   npm install -g phonegap
   ```

   UNIX® または Linux® システムでは、コマンドの前に `sudo` を付ける必要がある場合があります。

   端末には、一連の HTTP GETコマンドの結果が表示されます。 インストールに成功すると、次の例のように、ターミナルにライブラリのインストール先が表示されます。

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

1. （オプション）ターゲットとするモバイルプラットフォームのSDKを取得します。

   * iOS プラットフォーム用のアプリを作成するには、最新バージョンの [Xcode](https://developer.apple.com/xcode/) をインストールします。
   * Android™ アプリを作成するには、[Android™ SDK](https://developer.android.com/) をインストールします。

### コンテンツ ZIP ファイルのダウンロード {#downloading-the-content-zip-file}

モバイルアプリケーションのコンテンツをファイルシステムに移動します。

1. モバイルアプリケーションページで、アプリケーションを選択します。
1. （オプション）完全インストール用のアプリケーションを構築するには、ツールバーの [ キャッシュのクリア ] アイコンをクリックします。

   ![&#x200B; 壊れたリンク記号で示されるキャッシュ アイコンをクリアします。](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >キャッシュには、インストールされたアプリケーションのコンテンツのアップデートが保持されます。 キャッシュをクリアすると、キャッシュされた更新がすべて無効になります。

1. ツールバーの「CLI Assetsをダウンロード」アイコンをクリックします。

   ![CLI Assetsのアイコンをダウンロードします。このアイコンは、タブレットのアイコンが重なっていることを示しています &#x200B;](do-not-localize/chlimage_1-1.png)。

1. ZIP ファイルを保存したら、成功ダイアログで「閉じる」をクリックします。
1. ZIP ファイルの内容を解凍します。

### PhoneGap CLI を使用したビルド {#using-the-phonegap-cli-to-build}

PhoneGap CLI を使用してアプリケーションをコンパイルし、インストールします。 PhoneGap CLI の使用方法については、PhoneGap Command-line Interface （`https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html`）のマニュアルを参照してください。

1. ターミナルまたはコマンドプロンプトを開き、現在のディレクトリをダウンロードしたアプリケーションの ZIP ファイルに変更します。 例えば、次のように指定すると、ディレクトリが ng-app-cli.1392137825303.zip ファイルに変更されます。

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. ターゲットとするプラットフォームの phonegap コマンドを入力します。 例えば、次のコマンドは、Android用のアプリをビルドし™ す。

   ```shell
   phonegap build android
   ```

## PhoneGap Buildを使用した構築 {#building-using-phonegap-build}

PhoneGap クラウドサービスを使用してアプリを作成します。 この手順を実行するには、まずPhoneGap Build設定を作成する必要があります。

### PhoneGap Buildへの接続 {#connecting-to-phonegap-build}

PhoneGap Build設定を作成して、AEM内からPhoneGap Buildサービスを使用できるようにします。 モバイルアプリケーションの構築に使用するPhoneGap Buildアカウントのユーザー名とパスワードを指定します。

1. ツール ページを開きます。 （[http://localhost:4502/tools.html](http://localhost:4502/tools.html)）。
1. CQ Operations 領域で、「Cloud Service」をクリックします。
1. PhoneGap Buildの「今すぐ設定」リンクをクリックします。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 設定を作成ダイアログボックスで、タイトル プロパティの値を入力します。 既定では、Name プロパティの値はタイトルから派生しますが、名前を入力することもできます。 「作成」をクリックします。
1. PhoneGap Build設定ダイアログで、PhoneGap Buildのユーザー名とパスワードを入力し、「OK」をクリックします。

### PhoneGap Buildの使用 {#using-phonegap-build}

アプリケーションリソースをPhoneGap Buildに送信し、様々なモバイルプラットフォーム用にコンパイルします。

1. モバイルアプリケーションページで、モバイルアプリケーションを開きます。 （[http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap)）
1. （オプション）完全インストール用のアプリケーションを構築するには、アプリケーションを選択して「キャッシュの消去」アイコンをクリックします。

   ![&#x200B; 壊れたリンク記号で示されるキャッシュ アイコンをクリアします。](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >キャッシュには、インストールされたアプリケーションのコンテンツのアップデートが保持されます。 キャッシュをクリアすると、キャッシュされた更新がすべて無効になります。

1. スプラッシュページを選択し、「リモートを構築」アイコンをクリックします。

   ![2 つの丸歯車で示されるリモートアイコンを作成します &#x200B;](do-not-localize/chlimage_1-3.png)。

   **注意：** AEM BetaのBeta バージョンでは、ビルドが正常に完了してもインボックス通知は作成されません。

1. 成功ダイアログボックスで、「PhoneGap Build」をクリックしてAdobe PhoneGap Buildページ（`https://build.phonegap.com/apps`）を開きます。 アプリが表示されるのを待っている場合は、`https://status.build.phonegap.com/` でPhoneGap Buildステータスを確認できます。

   ビルドのインストールについて詳しくは、[PhoneGap Buildのドキュメント &#x200B;](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build) を参照してください。

   >[!NOTE]
   >
   >無料のPhoneGap Buildアカウントは、1 つのプライベートアプリケーションで使用できます。 追加のプライベートアプリケーションを作成している場合、PhoneGap ビルドが失敗します。

### 次の手順 {#the-next-steps}

構築プロセスの次のステップは、[&#x200B; アプリの構造 &#x200B;](/help/mobile/phonegap-structure-an-app.md) について学ぶことです。
