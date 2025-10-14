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
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 4%

---

# Adobe PhoneGap Build の設定 {#configure-your-adobe-phonegap-build-cloud-service}

{{ue-over-mobile}}

アプリケーションダッシュボードの **0&rbrace;PhoneGap Buildタイル &rbrace; を使用すると、Adobe PhoneGap Build サービスを通じて PhoneGap モバイルアプリケーションを作成および配布できます。**

**アプリを管理** タイル内で定義されたサポートされるすべてのプラットフォームは、**PhoneGap Build** タイルでリモートビルドをプッシュする際にPhoneGap Buildでビルドされます。

リモートビルドをプッシュしてソースを `https://build.phonegap.com` またはダウンロードし、`https://docs.phonegap.com/references/phonegap-cli/` で PhoneGap CLI を使用してローカルにビルドできます。

![PhoneGap Build タイル &#x200B;](assets/chlimage_1-60.png)

## Cloud Serviceの設定 {#configuring-the-cloud-service}

PhoneGap Buildを利用するには、PhoneGap Buildアカウント情報を使用してAEM PhoneGap BuildCloud Serviceを設定する必要があります。

現在アカウントをお持ちでない場合は、`https://build.phonegap.com` に移動して新規登録してください。 Adobe Creative Cloud メンバーシップをお持ちの場合、最大 25 個のプライベートアプリ（非オープンソースアプリ）をサポートしている場合があります。

PhoneGap Buildアカウントがアクティブであることを確認したら、AEM Cloud Management Console、特に [PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) （http://localhost:4502/etc/cloudservices/phonegap-build.html）に移動します。

**設定を管理** タイルを使用して、新しいクラウドサービスCloud Serviceを設定します。

### Cloud Serviceを管理タイルの使用 {#using-manage-cloud-services-tile}

**PhoneGap Build** タイルを使用してアプリのビルドを開始する前に、AEM Mobile ダッシュボードから **設定の管理** タイルを使用して、クラウドサービスをCloud Serviceする必要があります。

アプリにクラウドサービスを設定するには、次の手順に従います。

1. **Cloud Serviceを管理** タイルの右上隅をクリックします。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. **Cloud Serviceを追加または編集** 画面から「**PhoneGap Build**」オプションを選択します。

   「**次へ**」をクリックします。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. クラウド設定を作成できるように、資格情報を入力します。

   検証が完了したら、「**送信**」をクリックします。 この設定済みのクラウドCloud Serviceが **設定を管理** タイルに表示されるようになりました。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### PhoneGap Buildを使用したアプリケーションの構築 {#building-your-application-with-phonegap-build}

クラウドサービスを設定したら、**PhoneGap Build** タイルを使用してアプリケーションを構築できます。 右上隅をクリックして、「リモートをビルド **または** Sourceをダウンロード **オプションから選択** ます。

![chlimage_1-64](assets/chlimage_1-64.png)

Adobe PhoneGap Buildでリモートビルドを呼び出すには、「**リモートをビルド**」をクリックします。

>[!NOTE]
>
>何らかの理由でビルドが失敗した場合（以下の赤いiOS アイコンは、Platform が失敗したことを示します）、アイコンの上にマウスポインターを置くと、エラーメッセージが表示されます。 または、タイルの下部にあるトリプルドット「。..」をクリックして、`https://build.phonegap.com` （認証する必要があります）に直接移動し、ビルドを直接監視および管理することもできます。

### PhoneGap CLI によるアプリケーションの構築 {#building-your-application-with-phonegap-cli}

PhoneGap は、アプリケーションをローカルに構築するためのコマンドラインインターフェイスを提供します。

PhoneGap コマンドラインインターフェイス（CLI）を使用して、コンピューター上で PhoneGap アプリケーションをコンパイルします。 AEM コンテンツをアプリケーションに含めるには、AEMがモバイルアプリケーションのコンテンツ、コンテンツ同期設定、その他の必要なアセットを含む ZIP ファイルを作成します。 ZIP ファイルをダウンロードし、ビルドに含めます。

PhoneGap の CLI を活用するには、次の機能を含むローカル環境を設定する必要があります。

1. Platform SDK（iOS、Android™、WindowsPhone など）および
1. PhoneGap CLI

詳しくは、`https://docs.phonegap.com/references/phonegap-cli/` を参照してください。

前提条件をインストールしたら、簡単なアプリを作成し、シミュレーターまたはデバイスで実行することで、簡単なテストを実施します。ターミナルの try:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>追加 – 接続されたデバイスで実行しない場合は、この行の最後でエミュレートします。

上記が機能することを確認したら、**PhoneGap Build** タイルを使用して **Sourceをダウンロード** します。 ファイルをローカルシステムに保存して解凍します。 完了したら、次の操作を行います。

* その保存されたファイル（フォルダー）に移動します
* 「phonegap run ios」（または android など）を実行します。

### その他のリソース {#additional-resources}

作成者と開発者の役割と責任については、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けの開発](/help/mobile/developing-in-phonegap.md)
* [AEMでのAdobe PhoneGap Enterprise 向けオーサリング](/help/mobile/phonegap.md)
