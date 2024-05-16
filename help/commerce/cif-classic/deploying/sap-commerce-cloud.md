---
title: SAP Commerce Cloud を使用した e コマースのデプロイ
description: Adobe Experience Manager eCommerce と SAP Commerce Cloud のデプロイ方法を説明します。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: ht
source-wordcount: '712'
ht-degree: 100%

---

# SAP Commerce Cloud {#sap-commerce-cloud}

>[!NOTE]
>
>このページには、hybris web サイトへのリンクが含まれています。特定のページでは、ログインアカウントが必要です。

## SAP Commerce Cloud を使用した e コマースのデプロイ {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>以下の手順では、次のデモカタログを使用してデプロイメントの例を示します。
>
>`Geometrixx Outdoors Site English (US)`

[必要な e コマースパッケージ](#packages-needed-for-ecommerce-with-hybris)をデプロイすると、e コマースフレームワークのすべての機能と共に、hybris 実装（デモカタログを含む）に付属する e コマース機能のリファレンス実装が提供されます。

これは、Geometrixx Outdoors サイトの英語（米国）ブランチ（`/content/geometrixx-outdoors/en_US`）の配下で使用できます。

* [商品情報](#productinformationwithcolorvariants)（必要に応じてカラーバリエーション情報を含む）

* [買い物かごコンテンツの概要](#shoppingcartcontentoverview)
* [ユーザーのサインアップ](#customersignup)および[ユーザーのサインイン](#customersignin)

* [Access to the hybris management console](#accesstothehybrismanagementconsole)

### 技術的要件 - hybris サーバー {#technical-requirements-hybris-server}

e コマース統合フレームワークの Hybris 拡張が更新されて、[Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris) との下位互換性を保ちながら、Hybris 5 が（デフォルトで）サポートされるようになりました。

>[!NOTE]
>
>* バージョン 18.11 以降をサポートしています。
>* [Hybris 5 サーバー](https://www.sap.com/japan/products/crm.html)を実行するには Java™ 7 が必要です。
>* hybris のアドオンである [Telco Accelerator](https://www.sap.com/japan/products/crm.html) は、AEM 拡張機能ではサポートされていません。
>

### hybris を使用した e コマースに必要なパッケージ {#packages-needed-for-ecommerce-with-hybris}

e コマース機能をインストールするには、次が必要です。

* お使いの hybris サーバー
* AEM e コマースフレームワーク：

   * これは、標準の AEM インストールの一部です

* AEM Geometrixx オールパッケージ：

   * `cq-geometrixx-all-pkg`

* AEM hybris コンテンツパッケージ：

   * `cq-hybris-content-6.3.2`
   * hybris 固有の API 実装
   * `cq-geometrixx-hybris-content-6.3.2`
   * hybris の使用法を示すリファレンス実装（`geometrixx-outdoors/en_US`）

### hybris を使用した e コマースのインストール {#installation-of-ecommerce-with-hybris}

（デモカタログ Geometrixx Outdoors を使用して）包括的な設定をインストールするには、次の基本的な手順に従います。

1. [AEM をインストールします](/help/sites-deploying/deploy.md)。
1. Geometrixx-all パッケージのインストール

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. [パッケージマネージャー](/help/sites-administering/package-manager.md)を使用して、デモコンテンツパッケージをインストールします。

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [hybris サーバーをダウンロードして構築します](#download-and-build-your-hybris-server)。
1. e コマースエンジンでカタログを構成します。

   1. [Geometrixx Outdoors ストアを設定します](#setup-the-geometrixx-outdoors-store)。

1. AEM で必要な補助ページを[作成](/help/sites-authoring/qg-page-authoring.md)します。

>[!CAUTION]
>
>hybris サーバーを使用するには、hybris ライセンスが別途必要です。

>[!NOTE]
>
>開発者は、[API のドキュメント](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)をダウンロードすることもできます。

### hybris サーバーのダウンロードと構築 {#download-and-build-your-hybris-server}

この手順では、hybris サーバーをダウンロードして構築します。また、hybris と cq 間の接続に必要な初期設定も行います。拡張はデフォルト設定で使用できます。

>[!CAUTION]
>
>5.5.1 より前の hybris バージョンはサポートされていません。

>[!NOTE]
>
>この手順を完了するには、システムに [Groovy](https://groovy-lang.org/) がインストールされている必要があります。

1. hybris ダウンロードサイトから、**hybris Commerce Suite** のディストリビューションファイルをダウンロードします。

   >[!CAUTION]
   >
   >これにアクセスするには（hybris からの）アカウントが必要です。

1. 配布ファイルを（&lt;hybris-root-directory>と呼ばれる）必要な場所に解凍します。
1. コマンドラインから、次の操作を実行します。

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >実行時：
   >
   >`ant clean all`
   >
   >必要に応じて、`Return` キーを押します。

1. 以下のファイルを、解凍した hybris ディストリビューションのルートフォルダーにダウンロードします。

   ```
       <hybris-root-directory>
   ```


[ファイルを入手](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >hybris 5.6.0 以降の場合は、次の setup.groovy を使用してください。

   5.6.0 以降

[ファイルを入手](/help/sites-deploying/assets/setup-1.groovy)

1. コマンドラインから、次の操作を実行します。

   * （拡張の要件に従って）hybris サーバーの設定を更新します。
   * 変更後の設定で hybris サーバーを再構築します。
   * サーバーを起動します

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >システムによっては、これらのいくつかの手順が完了するまで数分かかる場合があります。

1. ブラウザーで次の URL にアクセスし、**hybris 管理コンソール**&#x200B;を表示します。

   [http://localhost:9002](http://localhost:9002)

1. 「**初期化**」をクリックし、初期化アクション（既存のデータを削除）を実行します。

   コンソールに進行状況が表示されます。「`FINISHED`」は処理が完了したことを示します。

   >[!NOTE]
   >
   >お使いのシステムによっては、この処理が完了するまでに数分かかる場合があります。

### Geometrixx Outdoors ストアを設定 {#setup-the-geometrixx-outdoors-store}

この手順では、Geometrixx オンラインのデモストアをアップロードして設定します。

1. hybris インスタンスを起動します。コマンドラインから、次の操作を実行します。

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. ブラウザーで次の URL にアクセスし、**hybris 管理コンソールに移動**&#x200B;します。

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   次の資格情報を使用します。
   * ユーザー名：admin
   * パスワード：nimda

1. サイドバーナビゲーションから、「**システム**」と「**ツール**」を展開します。次に、「**読み込み**」を選択して、**ウィザード：CSV の読み込み** ウィンドウを開きます。
1. 「**設定**」タブで、次の&#x200B;**読み込み**&#x200B;ファイル&#x200B;**をアップロードします**。

[ファイルを入手](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 「**ロケール設定**」を次のように設定します。

   `en_US - English (United States)`

1. 「**リソース**」タブを開きます。
1. 次の&#x200B;**メディア Zip** **をアップロードします**。

[ファイルを入手](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 「**開始**」をクリックして、指定したファイルを読み込みます。「**結果**」タブにログエントリが表示されます。

1. 「**完了**」をクリックして読み込みウィンドウを閉じます。

1. サイドバーから、「**システム**」、「**ツール**」、「**読み込み**」を順に選択します。

1. 次の&#x200B;**読み込みファイル** **をアップロードします**。

[ファイルを入手](/help/sites-deploying/assets/base-store.csv)

   hybris 5.7 の場合は、次の手順を使用してください。

[ファイルを入手](/help/sites-deploying/assets/base-store-5_7.csv)

1. 「**ロケール設定**」を次のように設定します。

   `en_US - English (United States)`

1. 「**開始**」をクリックして、指定したファイルを読み込みます。「**結果**」タブにログエントリが表示されます。

1. 「**完了**」をクリックして読み込みウィンドウを閉じます。

1. これで、商品をを操作して、読み込んだカタログと製品を表示できます。

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
