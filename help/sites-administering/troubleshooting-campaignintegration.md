---
title: Adobe Campaign Classic 統合に関するトラブルシューティング
description: Adobe Campaign Classic 統合に関する問題のトラブルシューティング方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 100%

---


# Adobe Campaign Classic 統合に関するトラブルシューティング{#troubleshooting-your-adobe-campaign-classic-integration}

Adobe Campaign Classic（ACC）統合に関する問題のトラブルシューティング方法について説明します。

次のトラブルシューティングヒントは、AEM を ACC と統合する際に発生する最も一般的な問題を解決するのに役立ちます。

## トラブルシューティングに関する一般的なヒント {#general-troubleshooting-tips}

両方のソリューション（AEM／Adobe Campaign Classic、Adobe Campaign Classic／AEM）で HTTP 呼び出しが送受信されるかどうかを確認します。このヒントは、ファイアウォール／SSL の問題を回避するのに役立ちます。

* AEM の機能では、JSON の呼び出しが AEM オーサーインターフェイスからリクエストされます
   * これらの呼び出しでは、HTTP 500 のエラーは表示されません。
   * HTTP 500 のエラーが表示される場合は、`error.log` で詳細を確認します。
* AEM でキャンペーンクラスのデバッグレベルを上げることも問題のトラブルシューティングに役立ちます。

## 接続に失敗する場合 {#when-the-connection-fails}

Adobe Campaign で **`aemserver`** 演算子が設定されていることを確認します。

## 画像が Adobe Campaign Classic コンソールに表示されない場合 {#if-images-do-not-appear-in-the-adobe-campaign-console}

HTML ソースを確認し、クライアントマシンから URL を開くことができることを検証します。URL に `localhost:4503` が含まれている場合は、AEM オーサーインスタンスで Day CQ Link Initializer の設定を変更します。Adobe Campaign Classic コンソールマシンから到達できるパブリッシュインスタンスを指すようにします。

[Externalizer の設定](/help/sites-administering/campaignstandard.md#configuring-the-externalizer) を参照してください。

## AEM から Adobe Campaign Classic に接続できない場合  {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Adobe Campaign Classic で次のエラーメッセージを探します。

* `No datasource defined in the instance 'default'.`

* `Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

この問題を修正するには、`$CAMPAIGN_HOME/conf/config-<instance-name>.xml` で次を変更します。

* `<dataStore hosts="*" lang="en_GB">`

## Adobe Campaign Classic ダイアログにデータが表示されない場合 {#if-no-data-displays-in-the-adobe-campaign-dialog}

Adobe Campaign Classic で、ポート番号の末尾がスラッシュ（`/`）で終わらないようにします。

![Adobe Campaign Classic - ポート番号の末尾がスラッシュで終わらないようにする](assets/chlimage_1-149.png)

## setlocale について警告が表示される場合 {#if-you-get-a-warning-about-your-setlocale}

Adobe Campaign Classic の Apache HTTPD サービスを開始すると、エラー `Warning: setlocale: LC_CTYPE cannot change locale` が表示される場合があります

`en_CA.ISO-8859-15 locale` が Adobe Campaign Classic サーバーにインストールされていることを確認します。

* `local -a` を使用することで、インストールされているかどうかをチェックできます。
* インストールされていない場合は、`/usr/local/neolane/nl6/env.sh` スクリプトをパッチして、ロケールをインストールされたロケールに変更します。

## スクリプト「get_nms_amcGetSeedMetaData_jssp」のコンパイル中にエラーが表示される場合 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

AEM ログファイルに次のエラーメッセージが表示される場合：

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Adobe Campaign Classic サーバーで次の回避策を使用します。

1. ファイル `$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js` を開きます
1. メソッド `amcGetSeedMetaData` の 467 行目を変更します
1. `label : [inclView.@label](mailto:inclView.@label)` を `label : String([inclView.@label](mailto:inclView.@label))` に変更します。
1. 保存.
1. サーバーを再起動します。

## Adobe Campaign Classic で「同期」ボタンをクリックしたときにエラーが表示される場合 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Adobe Campaign Classic で「**同期**」ボタンをクリックすると、次のエラーが表示される場合があります。

* `Error while executing the method 'aemListContent' of service [nms:delivery](https://nmsdelivery/)`

この問題を修正するには、Adobe Campaign Classic の&#x200B;**外部アカウント**&#x200B;で設定されている AEM 接続 URL にマシンから到達できることを確認します。

多くの場合、URL を `localhost` から IP アドレスに切り替えると、この問題を解決できます。

## 「Cannot parse XTK Date+Time &#39;undefined&#39;」というエラーが表示される場合 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

AEM で「**同期**」をクリックした後、ページ上のスクリプトが発生したというエラーが表示される場合があります。

* `Cannot parse XTK Date+Time 'undefined': not a valid XTK value.`

このエラーは、AEM インスタンスに期限切れの Adobe Campaign Classic 情報がある場合に発生します。この問題を解決するには、次の手順に従います。

1. AEM 上にあるすべての Adobe Campaign Classic 統合設定を削除します。
1. 統合を再作成します。
1. テンプレートの作成.

## Cloud Service をセットアップしているときに SSL に接続するとエラーが発生する場合 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

AEM の `error.log` に次のメッセージが表示された場合は、Adobe Campaign サポートチームにチケットを送信します。

```text
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

## 同期ダイアログに想定していた HTTPS リンクではなく HTTP リンクが表示される場合 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

AEM は、Adobe Campaign Classic 配信でコンテンツを同期しようとすると、ニュースレターのリストを返します。ただし、リスト内のニュースレターの URL が、HTTPS アドレスではなく HTTP アドレスになる場合があります。リスト内のいずれかの項目を選択すると、エラーが発生します。このエラーは、次の設定で発生する可能性があります。

* AEM Author との通信に https を使用して Adobe Campaign をホストした場合
* リバースプロキシで SSL を終端させた場合
* AEM オーサーインスタンスがオンプレミスである場合

この問題を解決するには、以下の手順を実行します。

* 元のプロトコルをヘッダーとして渡すように、AEM ディスパッチャーまたはリバースプロキシを設定する必要があります。
* AEM の OSGi 設定において、**Apache Felix Http Service SSL Filter** の設定に適切なヘッダー設定を使用する必要があります。
   * `https://<host>:<port>/system/console/configMgr`
   * 詳しくは、[https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter](https://github.com/apache/felix-dev/tree/master/http#using-the-ssl-filter) を参照してください。

## ページのプロパティでカスタムテンプレートを選択できない場合 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

AEM で Adobe Campaign Classic 用のメールテンプレートを作成する場合は、テンプレートの `jcr:content` ノードに、プロパティ`acMapping` を値 `mapRecipient` に設定して含める必要があります。適切に行われていない場合、AEM の&#x200B;**ページプロパティ**&#x200B;で Adobe Campaign Classic テンプレートを選択することはできません。フィールドが無効になっています。

## AEM ログに「com.day.cq.mcm.campaign.servlets.util.ParameterMapper」というエラーが表示される場合 {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

カスタムテンプレートを使用すると、AEM ログに `com.day.cq.mcm.campaign.servlets.util.ParameterMapper` というエラーが表示される場合があります。

このエラーは、`acMapping` プロパティが `recipient.firstName` 以外の値に設定されている場合に、Adobe Campaign Manager で空の値が作成されることが原因で発生します。

このエラーが発生した場合は、[Package Share](/help/sites-administering/package-manager.md#package-share) から AEM の機能パック 6576 をインストールします。
