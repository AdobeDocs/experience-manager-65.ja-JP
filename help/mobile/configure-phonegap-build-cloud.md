---
title: Adobe PhoneGap Build の設定
seo-title: Configure your Adobe PhoneGap Build Cloud Service
description: このページでは、クラウドサービスの設定と、PhoneGap Build を使用したアプリケーションのビルドについて説明します。
seo-description: Follow this page for configuring the cloud services and building your application with PhoneGap build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 77%

---

# Adobe PhoneGap Build の設定 {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

この **PhoneGap Buildタイル** 「アプリケーション」ダッシュボードでは、Adobe PhoneGap Build Service を通じて PhoneGap モバイルアプリケーションを構築し、配布する機能を提供します。

内で定義されたすべてのサポート対象プラットフォーム **アプリを管理** タイルは、 **PhoneGap Build** タイル。

リモートビルドを [https://build.phonegap.com](https://build.phonegap.com) にプッシュしたり、ソースをダウンロードして [PhoneGap CLI](https://docs.phonegap.com/references/phonegap-cli/) でローカルにビルドしたりできます。

![PhoneGap Build タイル](assets/chlimage_1-60.png)

## クラウドサービスの設定 {#configuring-the-cloud-service}

PhoneGap Build を利用するには、PhoneGap Build アカウント情報を使用して AEM PhoneGap Build クラウドサービスを設定する必要があります。

現在アカウントをお持ちでない場合は、に移動します。 [https://build.phonegap.com](https://build.phonegap.com) 登録してください。 Adobe Creative Cloudメンバーシップをお持ちの場合、最大 25 個のプライベートアプリ（オープンソース以外のアプリ）をサポートしている可能性があります。

PhoneGap Buildアカウントがアクティブであることを確認したら、AEM Cloud Management コンソール ( 特に [PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)。

以下を使用： **Cloud Services** タイルを使用して、新しいクラウドサービス設定を構成します。

### クラウドサービスを管理タイルの使用 {#using-manage-cloud-services-tile}

**PhoneGap Build** タイルを使用してアプリをビルドする前に、AEM Mobile ダッシュボードの&#x200B;**クラウドサービスを管理**&#x200B;タイルを使用して、クラウドサービスを設定する必要があります。

アプリのクラウドサービスを設定するには、以下の手順に従います。

1. **クラウドサービスを管理**&#x200B;タイルの右上隅をクリックします。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. **クラウドサービスを追加または編集**&#x200B;画面で「**PhoneGap Build**」オプションを選択します。

   「**次へ**」をクリックします。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 資格情報を入力して、新しいクラウド設定を作成します。

   確認が終わったら、「**送信**」をクリックします。この設定したクラウド設定が、**クラウドサービスを管理**&#x200B;タイルに表示されます。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### PhoneGap Build でのアプリケーションのビルド {#building-your-application-with-phonegap-build}

クラウドサービスを設定したら、**PhoneGap Build** タイルを使用してアプリケーションをビルドできます。右上隅をクリックして、「**リモートビルド**」または「**ソースをダウンロード**」オプションを選択します。

![chlimage_1-64](assets/chlimage_1-64.png)

Adobe PhoneGap Build を使用してリモートビルドを呼び出す場合は、「**リモートビルド**」をクリックします。

>[!NOTE]
>
>何らかの理由でビルドが失敗した場合は（下の赤い iOS アイコンはプラットフォームの障害を示しています）、アイコンにマウスポインターを合わせると、エラーメッセージが表示されます。または、タイルの下部にある 3 つのドット「...」（省略記号）をクリックして、https://build.phonegap.com に直接移動し（認証が必要です）、ビルドを直接監視および管理できます。

### PhoneGap CLI によるアプリケーションのビルド {#building-your-application-with-phonegap-cli}

PhoneGap には、アプリケーションをローカルでビルドするためのコマンドラインインターフェイスが用意されています。

PhoneGap コマンドラインインターフェイス（CLI）を使用して、コンピューター上で PhoneGap アプリケーションをコンパイルします。AEM コンテンツをアプリケーションに含めるには、モバイルアプリケーションのコンテンツ、コンテンツ同期設定およびその他の必要なアセットを含む ZIP ファイルを作成します。ZIP ファイルをダウンロードしてビルドに含めます。

PhoneGap のコマンドラインインターフェイスを利用するには、ローカル環境に以下のものを設定する必要があります。

1. プラットフォーム SDK（iOS、Android、WindowsPhone、...）および
1. PhoneGap CLI

詳しくは、[こちら](https://docs.phonegap.com/references/phonegap-cli/)をお読みください。

前提条件となる上記のものをインストールしたら、簡単なアプリを作成し、シミュレーターまたはできればデバイス上で実行して簡単なテストを実施し、ターミナルから次を試します。

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>接続しているデバイス上で実行しない場合は、この行の末尾に --emulate を追加してください。

上記の機能を確認したら、 **PhoneGap Build** 並べ替え先 **ソースをダウンロード**. ファイルを保存して、ローカルシステム上に解凍します。この作業が完了したら、以下をおこないます。

* 保存されたファイル（フォルダー）に移動します。
* 「phonegap run ios」（または android など）を実行します。

### その他のリソース {#additional-resources}

作成者および開発者の役割と責任について詳しくは、以下のリソースを参照してください。

* [AEM と Adobe PhoneGap Enterprise での開発](/help/mobile/developing-in-phonegap.md)
* [AEM での Adobe PhoneGap Enterprise 向けオーサリング](/help/mobile/phonegap.md)
