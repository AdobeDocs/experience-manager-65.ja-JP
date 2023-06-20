---
title: Adobe PhoneGap Build の設定
seo-title: Configure your Adobe PhoneGap Build Cloud Service
description: このページでは、クラウドサービスの設定と PhoneGap Build を使用したアプリケーションの構築について説明します。
seo-description: Follow this page for configuring the cloud services and building your application with PhoneGap build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: 17d13e9b201629d9d1519fde4740cf651fe89d2c
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 3%

---

# Adobe PhoneGap Build の設定 {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

この **PhoneGap Buildタイル** 「アプリケーション」ダッシュボードでは、Adobe PhoneGap Build Service を通じて PhoneGap モバイルアプリケーションを構築し、配布する機能を提供します。

内で定義されたすべてのサポート対象プラットフォーム **アプリを管理** タイルは、 **PhoneGap Build** タイル。

リモートビルドを次にプッシュできます： `https://build.phonegap.com` PhoneGap CLI を使用してローカルにビルドするには、次の場所にソースをダウンロードします。 `https://docs.phonegap.com/references/phonegap-cli/`.

![PhoneGap Buildタイル](assets/chlimage_1-60.png)

## Cloud Service {#configuring-the-cloud-service}

PhoneGap Buildを活用するには、PhoneGap Buildアカウント情報を使用してAEMPhoneGap BuildCloud Serviceを設定する必要があります。

現在アカウントをお持ちでない場合は、に移動します。 `https://build.phonegap.com` 登録してください。 Adobe Creative Cloudメンバーシップをお持ちの場合、最大 25 個のプライベートアプリ（オープンソース以外のアプリ）をサポートしている可能性があります。

PhoneGap Buildアカウントがアクティブであることを確認したら、AEM Cloud Management コンソール ( 特に [PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)。

以下を使用： **Cloud Services** タイルを使用して、新しいクラウドサービス設定を構成します。

### Cloud Servicesを管理タイルを使用 {#using-manage-cloud-services-tile}

を使用してアプリのビルドを開始する前に **PhoneGap Build** タイルでは、 **Cloud Services** タイルをAEM Mobileダッシュボードから表示します。

アプリにクラウドサービスを設定するには、次の手順に従います。

1. の右上隅をクリックします。 **Cloud Services** タイル。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 選択 **PhoneGap Build** オプションを **「追加」または「編集」Cloud Service** 画面

   「**次へ**」をクリックします。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 資格情報を入力して、新しいクラウド設定を作成します。

   検証が完了したら、「 **送信**. この設定済みのクラウド設定が、 **Cloud Services** タイル。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### PhoneGap Buildを使用したアプリケーションの構築 {#building-your-application-with-phonegap-build}

クラウドサービスを設定したら、を使用してアプリケーションを構築できます。 **PhoneGap Build** タイル。 右上隅をクリックして、 **リモートビルド** または **ソースをダウンロード** オプション。

![chlimage_1-64](assets/chlimage_1-64.png)

Adobe PhoneGap Buildでリモートビルドを呼び出すには、 **リモートビルド**.

>[!NOTE]
>
>何らかの理由でビルドが失敗した場合 ( 下の赤いiOSのアイコンはプラットフォームが失敗したことを示しています )、アイコンの上にマウスポインターを置くと、エラーメッセージが表示されます。 または、3 つのドット (「。..」) をクリックすることもできます。 タイルの下部で、に直接移動します。 `https://build.phonegap.com` （認証が必要です）。ビルドを直接監視および管理します。

### PhoneGap CLI を使用したアプリケーションの構築 {#building-your-application-with-phonegap-cli}

PhoneGap は、アプリケーションをローカルにビルドするためのコマンドラインインターフェイスを提供します。

PhoneGap コマンドラインインターフェイス (CLI) を使用して、コンピューター上で PhoneGap アプリケーションをコンパイルします。 AEMコンテンツをアプリケーションに含めるために、AEMは、モバイルアプリケーションのコンテンツ、コンテンツ同期設定、その他の必要なアセットを含む ZIP ファイルを作成します。 ZIP ファイルをダウンロードして、ビルドに含めます。

PhoneGap のコマンドラインインターフェイスを活用するには、次を含むようにローカル環境を設定する必要があります。

1. Platform SDK(iOS、Android、WindowsPhone など ) および
1. PhoneGap CLI

詳しくは、こちらを参照してください。 `https://docs.phonegap.com/references/phonegap-cli/`.

前提条件をインストールしたら、単純なアプリを作成し、シミュレーター内またはデバイス上でより高い方法で実行し、ターミナルから次の操作を試すことで、簡単なテストを行います。

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>接続されたデバイスで実行したくない場合は、—emulate をこの行の末尾に追加します。

上記の機能を確認したら、 **PhoneGap Build** 並べ替え先 **ソースをダウンロード**. ファイルを保存し、ローカルシステムに解凍します。 完了したら、次の手順に従います。

* 保存されたファイル（フォルダー）に移動します。
* 「phonegap run ios」（または android など）を実行

### その他のリソース {#additional-resources}

作成者と開発者の役割と責任について詳しくは、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向け開発](/help/mobile/developing-in-phonegap.md)
* [AEMでのAdobe PhoneGap Enterprise 向けのオーサリング](/help/mobile/phonegap.md)
