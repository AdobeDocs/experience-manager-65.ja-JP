---
title: Adobe PhoneGap Build の設定
description: クラウドサービスの設定とPhoneGap Buildを使用したアプリケーションの構築については、このページに従ってください。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 7%

---

# Adobe PhoneGap Build の設定 {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

この **PhoneGap Buildタイル** アプリケーションダッシュボードのを使用すると、Adobe PhoneGap Build サービスを通じて PhoneGap モバイルアプリケーションを作成および配布できます。

内で定義されている、サポートされるすべてのプラットフォーム **アプリの管理** を使用してリモートビルドをプッシュする際、タイルはPhoneGap Buildを使用してビルドされます。 **PhoneGap Build** タイル。

リモートビルドをプッシュして、 `https://build.phonegap.com` または、PhoneGap CLI を使用してローカルにビルドするソースを `https://docs.phonegap.com/references/phonegap-cli/`.

![PhoneGap Buildタイル](assets/chlimage_1-60.png)

## Cloud Serviceの設定 {#configuring-the-cloud-service}

PhoneGap Buildを利用するには、PhoneGap Buildアカウント情報を使用してAEM PhoneGap BuildCloud Serviceを設定する必要があります。

現在アカウントをお持ちでない場合は、に移動します `https://build.phonegap.com` そして、サインアップ！ Adobe Creative Cloud メンバーシップをお持ちの場合、最大 25 個のプライベートアプリ（非オープンソースアプリ）をサポートしている場合があります。

PhoneGap Buildアカウントがアクティブであることを確認したら、AEM Cloud Management コンソール（特に）に移動します [PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) （http://localhost:4502/etc/cloudservices/phonegap-build.html）。

の使用 **Cloud Serviceの管理** 新しいクラウドサービス設定を設定するためのタイル。

### Cloud Serviceを管理タイルの使用 {#using-manage-cloud-services-tile}

を使用してアプリのビルドを開始する前に **PhoneGap Build** タイルの場合、 **Cloud Serviceの管理** AEM Mobile ダッシュボードからタイル表示します。

アプリにクラウドサービスを設定するには、次の手順に従います。

1. の右上隅をクリックします **Cloud Serviceの管理** タイル。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. を選択 **PhoneGap Build** からのオプション **Cloud Serviceを追加または編集** 画面。

   「**次へ**」をクリックします。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. クラウド設定を作成できるように、資格情報を入力します。

   確認が完了したら、 **Submit**. この設定されたクラウド設定はに表示されます。 **Cloud Serviceの管理** タイル。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### PhoneGap Buildを使用したアプリケーションの構築 {#building-your-application-with-phonegap-build}

クラウドサービスを設定したら、を使用してアプリケーションを構築できます **PhoneGap Build** タイル。 右上隅をクリックして、 **リモートのビルド** または **ソースをダウンロード** オプション。

![chlimage_1-64](assets/chlimage_1-64.png)

Adobe PhoneGap Buildでリモートビルドを呼び出すには、次をクリックします **リモートのビルド**.

>[!NOTE]
>
>何らかの理由でビルドが失敗した場合（以下の赤いiOS アイコンは、Platform が失敗したことを示します）、アイコンの上にマウスポインターを置くと、エラーメッセージが表示されます。 または、タイルの下部にある 3 つのドット「。..」をクリックして、直接移動することもできます。 `https://build.phonegap.com` （認証が必要）を行い、ビルドを直接監視および管理します。

### PhoneGap CLI によるアプリケーションの構築 {#building-your-application-with-phonegap-cli}

PhoneGap は、アプリケーションをローカルに構築するためのコマンドラインインターフェイスを提供します。

PhoneGap コマンドラインインターフェイス（CLI）を使用して、コンピューター上で PhoneGap アプリケーションをコンパイルします。 AEM コンテンツをアプリケーションに含めるには、AEMがモバイルアプリケーションのコンテンツ、コンテンツ同期設定、その他の必要なアセットを含む ZIP ファイルを作成します。 ZIP ファイルをダウンロードし、ビルドに含めます。

PhoneGap の CLI を活用するには、次の機能を含むローカル環境を設定する必要があります。

1. Platform SDK （iOS、Android™、WindowsPhone など）と、
1. PhoneGap CLI

詳しくは、こちらを参照してください `https://docs.phonegap.com/references/phonegap-cli/`.

前提条件をインストールしたら、簡単なアプリを作成し、シミュレーターまたはデバイスで実行することで、簡単なテストを実施します。ターミナルの try:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>追加 – 接続されたデバイスで実行しない場合は、この行の最後でエミュレートします。

上記の手順が正しく機能することを確認したら、 **PhoneGap Build** タイル先 **ソースをダウンロード**. ファイルをローカルシステムに保存して解凍します。 完了したら、次の操作を行います。

* その保存されたファイル（フォルダー）に移動します
* 「phonegap run ios」（または android など）を実行します。

### その他のリソース {#additional-resources}

作成者と開発者の役割と責任については、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けの開発](/help/mobile/developing-in-phonegap.md)
* [AEMでのAdobe PhoneGap Enterprise 向けオーサリング](/help/mobile/phonegap.md)
