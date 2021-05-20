---
title: SAP Commerce Cloud
seo-title: SAPCommerce Cloud
description: SAP Commerce Cloud を使用した e コマースのデプロイ方法について説明します。
seo-description: SAP Commerce Cloud を使用した e コマースのデプロイ方法について説明します。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 86%

---

# SAPCommerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>このページには hybris Web サイトへのリンクが含まれています。ページによっては、ログインアカウントが必要となる場合があります。

## SAPCommerce Cloud{#deploying-ecommerce-with-sap-commerce-cloud}を使用したeコマースの導入

>[!NOTE]
>
>以下の手順では、次のデモカタログを使用してデプロイメントの例を示します。
>
>`Geometrixx Outdoors Site English (US)`

[必要な e コマースパッケージ](#packages-needed-for-ecommerce-with-hybris)をデプロイすると、e コマースフレームワークのすべての機能と共に、hybris 実装（デモカタログを含む）に付属する e コマース機能のリファレンス実装が提供されます。

これは、Geometrixx Outdoorsサイトの英語（米国）ブランチ(`/content/geometrixx-outdoors/en_US`)の下で使用できます。

* [商品情報](#productinformationwithcolorvariants)（必要に応じてカラーバリエーション情報を含む）

* [買い物かごコンテンツの概要](#shoppingcartcontentoverview)
* [ユーザーのサインアップ](#customersignup)および[ユーザーのサインイン](#customersignin)

* [Access to the hybris management console](#accesstothehybrismanagementconsole)

### 技術的要件 - hybris サーバー {#technical-requirements-hybris-server}

eコマース統合フレームワークのhybris拡張が更新され、[Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris)との後方互換性を維持しながら、Hybris 5が（デフォルトで）サポートされるようになりました。

>[!NOTE]
>
>* バージョン18.11以降をサポートします。
>* [hybris 5 サーバー](https://www.hybris.com/en/architecture-technology)を実行するには Java 7 が必要です。
>* hybris のアドオンである [Telco Accelerator](https://www.hybris.com/en/products/telecommunication) は、AEM 拡張でサポートされません。

>



### hybris を使用した e コマースに必要なパッケージ  {#packages-needed-for-ecommerce-with-hybris}

e コマース機能をインストールするには、以下が必要です。

* hybrisサーバー
* AEM e コマースフレームワーク：

   * AEM の標準インストールの一部です。

* AEM Geometrixx-all パッケージ：

   * `cq-geometrixx-all-pkg`

* AEM hybris コンテンツパッケージ：

   * `cq-hybris-content-6.3.2`
   * hybris 固有の API 実装
   * `cq-geometrixx-hybris-content-6.3.2`
   * hybris ( `geometrixx-outdoors/en_US` )の使用を説明する参照実装

### hybris を使用した e コマースのインストール {#installation-of-ecommerce-with-hybris}

（デモカタログ Geometrixx Outdoors を使用して）包括的な設定をインストールするには、次の基本的な手順に従います。

1. [AEM をインストール](/help/sites-deploying/deploy.md)します。
1. Geometrixx-all パッケージをインストールします。

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. [パッケージマネージャー](/help/sites-administering/package-manager.md)を使用して、デモコンテンツパッケージをインストールします。

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [hybris サーバーをダウンロードして構築](#download-and-build-your-hybris-server)します。
1. e コマースエンジンにカタログを構成します。

   1. [Geometrixx Outdoors ストアを設定](#setup-the-geometrixx-outdoors-store)します。

1. AEM で必要な補助ページを[作成](/help/sites-authoring/qg-page-authoring.md)します。

>[!CAUTION]
>
>hybris サーバーを使用するには、hybris のライセンスが別途必要です。

>[!NOTE]
>
>開発者は、[API のドキュメント](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)をダウンロードすることもできます。

### hybris サーバーのダウンロードと構築 {#download-and-build-your-hybris-server}

この手順では、hybris サーバーをダウンロードして構築します。また、hybris と CQ の接続に必要な初期設定もおこないます。拡張はデフォルト設定で使用できます。

>[!CAUTION]
>
>5.5.1 より前の hybris バージョンはサポートされていません。

>[!NOTE]
>
>この手順を完了するには、システムに [Groovy](https://groovy-lang.org/) がインストールされている必要があります。

1. hybris ダウンロードサイトから、hybris Commerce Suite のディストリビューションファイルをダウンロードします。****

   >[!CAUTION]
   >
   >このサイトにアクセスするには hybris のアカウントが必要です。

1. ディストリビューションファイルを必要な場所（&lt;hybris-root-directory> が示す場所）に展開します。
1. コマンドラインから、次のコマンドを実行します。

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >次のコマンドの実行中、
   >
   >`ant clean all`
   >
   >必要に応じて`Return`を押します。

1. 次のファイルを、展開したhybris配布物のルートフォルダーにダウンロードします。

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
   * サーバーを起動します。

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >お使いのシステムによっては、いくつかの手順が完了するまでに数分かかる場合があります。

1. ブラウザーで次の URL にアクセスし、**hybris 管理コンソールに移動**&#x200B;します。

   [http://localhost:9002](http://localhost:9002)

1. 「**初期化**」をクリックし、初期化処理（既存データの削除）を確認します。

   コンソールに進行状況が表示されます。「`FINISHED`」は処理が完了したことを示します。

   >[!NOTE]
   >
   >お使いのシステムによっては、この処理が完了するまでに数分かかる場合があります。

### Geometrixx Outdoors ストアの設定 {#setup-the-geometrixx-outdoors-store}

この手順では、デモストア Geometrixx Online をアップロードして設定します。

1. hybris インスタンスを起動します。コマンドラインから、次のコマンドを実行します。

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. ブラウザーで次の URL にアクセスし、hybris 管理コンソールに移動します。****

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   次の資格情報を使用します。
   * ユーザー名：admin
   * パスワード：ニムダ

1. サイドバーナビゲーションから、**システム**&#x200B;と&#x200B;**ツール**&#x200B;を展開します。 次に、「**読み込み**」を選択して、**ウィザード : CSV の読み込み**&#x200B;ウィンドウを開きます。
1. 「**設定**」タブで、次の読み込みファイルをアップロードします。********

[ファイルを入手](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. 「**ロケール設定**」を次のように設定します。

   `en_US - English (United States)`

1. 「**リソース**」タブを開きます。
1. 次のメディア Zip をアップロードします。********

[ファイルを入手](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. 「**開始**」をクリックして、指定したファイルを読み込みます。「**結果**」タブにログエントリが表示されます。

1. 「完了」をクリックして読み込みウィンドウを閉じます。****

1. サイドバーから、「**システム**」、「**ツール**」、「**読み込み**」を順に選択します。

1. 次の読み込みファイルをアップロードします。********

[ファイルを入手](/help/sites-deploying/assets/base-store.csv)

   hybris 5.7 の場合は、次の手順を使用してください。

[ファイルを入手](/help/sites-deploying/assets/base-store-5_7.csv)

1. 「**ロケール設定**」を次のように設定します。

   `en_US - English (United States)`

1. 「**開始**」をクリックして、指定したファイルを読み込みます。「**結果**」タブにログエントリが表示されます。

1. 「完了」をクリックして読み込みウィンドウを閉じます。****

1. これで、商品をを操作して、読み込んだカタログと製品を表示できます。

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
