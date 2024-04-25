---
title: PhoneGap CLI によるアプリの開発
description: ブートストラップされた開発環境を使用して、PhoneGap CLI でモバイル用アプリを開発する方法を説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 7%

---

# PhoneGap CLI によるアプリの開発{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

開発環境を設定した場合、開発者は任意の時点でアプリをデバイス上またはエミュレーター内で実行できます。

次の例を実行するには、Xcode を使用してmacOS X を実行するシステム、または Android™ SDK がインストールされたMac/Win/Linux システムが必要です。

## 開発環境のBootstrap {#bootstrap-your-development-environment}

PhoneGap CLI の設定（`https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface`）

iOSの場合：iPhone および iPad 用に開発するには、Appleの Xcode IDE が必要です。

* 無料でダウンロード [こちら](https://idmsa.apple.com/IDMSWebAuth/signin?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&amp;path=%2Fdownload%2F&amp;rv=1).
* PhoneGap iOS プラットフォームガイド （`https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide`）

Android™ の場合：iPhone および iPad 用に開発するには、Googleの Android™ Stuido IDE が必要です。

* 無料でダウンロード [こちら](https://developer.android.com/studio).
* PhoneGap Android™ プラットフォームガイド （`https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide`）

## ソースをダウンロード {#download-the-source}

開発環境のブートストラップが正常に完了したら、AEM アプリケーションのビルドタイルからソースをダウンロードします。

* PhoneGap Buildタイル ドロップダウンの山形アイコンをクリックします。

![chlimage_1-45](assets/chlimage_1-45.png)

* 「ソースをダウンロード」をクリックします。
* ソースをダウンロード モーダルから目的のソースを選択します。

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>開発ソースには、ステージングされていない変更を含めて、アプリの最新の状態が含まれています。 アプリストアのベンダーに送信するリリース候補を作成するには、ステージングソースを使用します。
>
>アプリをステージングしない場合、「ステージングトリガー」を選択すると、ステージングワークフローが表示されます（ヒント：は、AppStore およびGoogle PlayStore で利用可能な PhoneGap Enterprise ビューアアプリでステージング済みアプリとして表示されます）。

* 「ダウンロード」をクリックして、ZIP をコンピューターに保存します。
* ダウンロードした zip ファイルをワークスペースに抽出します。

## アプリケーションのビルドと読み込み（ソースから） {#build-and-load-the-app-from-source}

PhoneGap CLI では、プラットフォームプロジェクトの作成、ソースのコンパイル、および 1 つのコマンドでのアプリのデプロイが可能です。

>[!NOTE]
>
>これらの手順はすべて個別に実行できます。PhoneGap CLI ドキュメント （`https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/`）に設定します。

1. 上記を参照して、PhoneGap CLI がインストールされていることを確認します。
1. コンソール（またはターミナル）ウィンドウで、抽出したソースのルートディレクトリに移動します。
1. 以下のコマンドを入力します。

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>この時点で問題が発生した場合は、基本に戻ってトラブルシューティングをおこないます。
>
>1. フォルダーの作成（mkdir テスト）
>1. この新しいフォルダーに移動（cd テスト）
>1. 実行 `phonegap create helloWorld`
>1. helloWorld （cd helloWorld）に移動します
>1. 実行 `phonegap run android` （または、上記のように Android™ をiOSに置き換えます）。
>1. 新しく作成した PhoneGap アプリを実行しているエミュレーターが開き、ネイティブへの JavaScript ブリッジが動作している場合は「デバイス準備完了」と表示されます。
>
>このトラブルシューティングでは、PhoneGap CLI 開発環境が正しく動作していることを確認します。

## Safari およびIOSでの JavaScript のデバッグ デバッグ {#debug-javascripts-with-safari-and-ios-debug}

Web アプリケーションを使用する場合と同じように、Safari の開発者ツールを使用してアプリの JavaScript をデバッグできます。

## Safari 開発者ツールの有効化 {#enable-safari-developer-tools}

デベロッパーツールを有効にするには：

* Safari の環境設定を開く

   * メニューバーで Safari をクリックします
   * 「環境設定」をクリックします

* 環境設定ウィンドウで「詳細」をクリックします

![chlimage_1-47](assets/chlimage_1-47.png)

* 「メニューバーに「開発」メニューを表示」をオンにします
* 環境設定ウィンドウを閉じる

## Safari をiOSに接続 {#connect-safari-to-ios}

Safari は、iOS デバイスまたはエミュレーターのいずれかに接続できます。

* コンソールウィンドウで、抽出したソースのルートディレクトリに移動します。
* 次のコマンドを入力して、デバイスまたはエミュレーターでアプリを起動します。

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Safari を開きます。
* メニューバーの「開発」をクリックします
* 「iOSシミュレータ」サブメニューを選択します
* home.html をクリックします

![chlimage_1-48](assets/chlimage_1-48.png)

## Safari の Web Inspector を使用した JavaScript のデバッグ {#debug-javascript-with-safari-s-web-inspector}

ブレークポイントは、ソースの任意の場所で設定できます。 エミュレーターやデバイスとやり取りする場合、アプリの実行はこれらのブレークポイントで停止します。 実行を段階的に実行し、変数の値を調べることができます。

* 「Web インスペクタ」ウィンドウで「リソース」をクリックします
* ソースツリーに移動し、目的のソースファイルをクリックします
* ブレークポイントを追加するには、行番号をクリックします
* デバイスまたはエミュレーターとのインタラクション

![chlimage_1-49](assets/chlimage_1-49.png)

* コントロールボタンを使用して、実行の続行、ステップオーバー、ステップイン、ステップアウトの各メソッドを実行します。

![5 つの異なる機能コントロールボタンが水平方向に並んでいます。](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>現在のメソッドの変数の値を確認するには、マウスを合わせます。

## 次の手順 {#the-next-steps}

PhoneGap CLI を使用したアプリの開発については、次を参照してください。 [デバイス機能へのアクセス](/help/mobile/phonegap-access-device-features.md).
