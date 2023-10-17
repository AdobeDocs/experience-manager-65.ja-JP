---
title: PhoneGap CLI によるアプリの開発
description: ブートストラップを設定した開発環境を使用して、PhoneGap CLI でモバイル用のアプリを開発する方法を説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 4%

---

# PhoneGap CLI によるアプリの開発{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

開発環境を設定している場合は、開発者として、いつでもデバイス上またはエミュレーター内でアプリを実行できます。

次の例を実行するには、Xcode でmacOS X を実行するシステムか、Android™ SDK をインストールしたMac/Win/Linux システムが必要です。

## 開発環境のBootstrap {#bootstrap-your-development-environment}

PhoneGap CLI の設定 (`https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface`)

iOSの場合： iPhone および iPad 向けの開発を行うには、Appleで Xcode IDE を使用する必要があります。

* 無料でダウンロードできます [ここ](https://idmsa.apple.com/IDMSWebAuth/signin?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&amp;path=%2Fdownload%2F&amp;rv=1).
* PhoneGap iOSプラットフォームガイド (`https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide`)

Android™の場合： iPhone および iPad 向けの開発を行うには、Googleの Android™ Stuido IDE が必要です。

* 無料でダウンロードできます [ここ](https://developer.android.com/studio).
* PhoneGap Android™プラットフォームガイド (`https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide`)

## ソースのダウンロード {#download-the-source}

開発環境を正常にブートストラップしたら、 AEM App Build タイルからソースをダウンロードします。

* 「PhoneGap Buildタイル」ドロップダウンの山形をクリックします。

![chlimage_1-45](assets/chlimage_1-45.png)

* 「ソースをダウンロード」をクリックします。
* 「ソースをダウンロード」モーダルから目的のソースを選択します。

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>開発ソースには、未ステージの変更も含め、アプリの最新の状態が含まれています。 アプリストアベンダーに送信するリリース候補を構築するには、ステージングソースを使用します。
>
>アプリをステージングしない場合、ステージングトリガーを選択してステージングワークフローを実行します ( ヒント：は、AppStore およびGoogle PlayStore で利用可能な PhoneGap Enterprise Viewer App にステージング済みアプリとして表示されます )。

* 「ダウンロード」をクリックし、ZIP をコンピューターに保存します。
* ダウンロードした zip ファイルをワークスペースに展開します。

## （ソースから）アプリをビルドして読み込む {#build-and-load-the-app-from-source}

PhoneGap CLI は、プラットフォームプロジェクトの作成、ソースのコンパイル、1 つのコマンドでのアプリのデプロイを行うことができます。

>[!NOTE]
>
>これらの手順はすべて個別に実行できます。 PhoneGap CLI のドキュメント (`https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/`) をクリックします。

1. PhoneGap CLI をインストール済みであることを確認します。上記を参照してください。
1. コンソール（またはターミナル）ウィンドウで、抽出したソースのルートディレクトリに移動します。
1. 以下のコマンドを入力します。

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>この時点で問題が発生した場合は、基本事項に戻ってトラブルシューティングしてください。
>
>1. フォルダーの作成（mkdir テスト）
>1. この新しいフォルダーに移動します（cd テスト）
>1. 実行 `phonegap create helloWorld`
>1. helloWorld(cd helloWorld) に移動します。
>1. 実行 `phonegap run android` ( または、上記のように Android™をiOSに置き換えます )。
1. 新しく作成した PhoneGap アプリを実行するエミュレーターが開き、ネイティブへの JavaScript ブリッジが動作している場合は「Device Ready」と表示されます。
>
このトラブルシューティングは、PhoneGap CLI 開発環境が正しく実行されていることを確認します。

## Safari およびIOSデバッグでの JavaScript のデバッグ {#debug-javascripts-with-safari-and-ios-debug}

Web アプリケーションの場合と同様に、Safari の開発者ツールを使用して、アプリの JavaScript をデバッグできます。

## Safari 開発者ツールの有効化 {#enable-safari-developer-tools}

開発者ツールを有効にするには：

* Safari の環境設定を開きます。

   * メニューバーで Safari をクリックします。
   * 「環境設定」をクリックします

* 「プリファレンス」ウィンドウで「詳細」をクリックします。

![chlimage_1-47](assets/chlimage_1-47.png)

* 「メニューバーに開発メニューを表示」をオンにします。
* 「プリファレンス」ウィンドウを閉じます。

## Safari をiOSに接続 {#connect-safari-to-ios}

Safari は、iOSデバイスまたはエミュレーターに接続できます。

* コンソールウィンドウで、抽出したソースのルートディレクトリに移動します。
* 次のコマンドを入力して、デバイスまたはエミュレーターでアプリを起動できるようにします。

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Safari を開く
* メニューバーの「開発」をクリックします。
* 「 iOS Simulator 」サブメニューを選択します。
* home.html をクリックします。

![chlimage_1-48](assets/chlimage_1-48.png)

## Safari の Web インスペクタでの JavaScript のデバッグ {#debug-javascript-with-safari-s-web-inspector}

ソースの任意の場所にブレークポイントを設定できます。 エミュレーターまたはデバイスとやり取りすると、アプリの実行がこれらのブレークポイントで停止します。 実行を順を追って進め、変数の値を調べることができます。

* 「Web インスペクタ」ウィンドウで「リソース」をクリックします。
* ソースツリーに移動し、目的のソースファイルをクリックします。
* 隣の行番号をクリックして、ブレークポイントを追加します。
* デバイスまたはエミュレーターとやり取りする

![chlimage_1-49](assets/chlimage_1-49.png)

* コントロールボタンを使用して、メソッドの実行、上へ、下へ、および下へのステップアウトを続行します。

![横の行に配置された、5 つの異なる機能するコントロールボタン。](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
現在のメソッドの変数の値を確認するには、マウスポインターを置きます。

## 次の手順 {#the-next-steps}

PhoneGap CLI を使用したアプリの開発について学んだ後は、 [デバイスの機能へのアクセス](/help/mobile/phonegap-access-device-features.md).
