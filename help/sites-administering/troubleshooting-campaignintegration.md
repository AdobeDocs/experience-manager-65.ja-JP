---
title: Adobe Campaign Classic統合のトラブルシューティング
description: Adobe Campaign Classic統合に関する問題のトラブルシューティング方法について説明します。
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
source-git-commit: 0d91e54fde32f2fafb9a616ed4e957e9590fff26
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 5%

---


# Adobe Campaign Classic統合のトラブルシューティング{#troubleshooting-your-adobe-campaign-classic-integration}

Adobe Campaign Classic(ACC) 統合に関する問題のトラブルシューティング方法について説明します。

次のトラブルシューティングのヒントは、AEMを ACC と統合する際に発生する可能性のある最も一般的な問題の解決に役立ちます。

## トラブルシューティングに関する一般的なヒント {#general-troubleshooting-tips}

両方のソリューション (AEM / Adobe Campaign Classic、Adobe Campaign Classic / AEM) で HTTP 呼び出しが送受信されているかどうかを確認します。 これは、ファイアウォール/SSL の問題を回避するためです。

* AEM機能の場合は、AEMオーサーインターフェイスから JSON 呼び出しがリクエストされます
   * HTTP-500 エラーは発生しません。
   * HTTP 500 のエラーが発生した場合は、`error.log` で詳細を確認してください。
* AEMでキャンペーンクラスのデバッグレベルを上げると、問題のトラブルシューティングにも役立ちます。

## 接続に失敗した場合 {#when-the-connection-fails}

設定済みの **aemserver** 演算子をAdobe Campaign Classicで使用します。

## 画像がAdobe Campaign Classicコンソールに表示されない場合 {#if-images-do-not-appear-in-the-adobe-campaign-console}

HTMLソースを確認し、クライアントマシンから URL を開けることを検証します。 URL に `localhost:4503` この設定で、AEMオーサーインスタンス上の Day CQ Link Externalizer の設定を、Adobe Campaign Classicコンソールマシンからアクセスできるパブリッシュインスタンスを指すように変更します。

[Externalizer の設定](/help/sites-administering/campaignstandard.md#configuring-the-externalizer) を参照してください。

## AEMからAdobe Campaign Classicに接続できない場合  {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Adobe Campaign Classicで次のエラーメッセージを探します。

* `No datasource defined in the instance 'default'.`

* `Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

この問題を修正するには、 `$CAMPAIGN_HOME/conf/config-<instance-name>.xml`:

* `<dataStore hosts="*" lang="en_GB">`

## Adobe Campaign Classicダイアログにデータが表示されない場合 {#if-no-data-displays-in-the-adobe-campaign-dialog}

Adobe Campaign Classicで、末尾にスラッシュ (`/`) をクリックします。

![chlimage_1-149](assets/chlimage_1-149.png)

## Setlocale に関する警告が表示された場合 {#if-you-get-a-warning-about-your-setlocale}

Adobe Campaign Classic用の Apache HTTPD サービスを開始すると、エラーが表示される場合があります `Warning: setlocale: LC_CTYPE cannot change locale`

次の条件を満たしていることを確認します。 `en_CA.ISO-8859-15 locale` をAdobe Campaign Classicサーバーにインストールする必要があります。

* `local -a` を使用することで、インストールされているかどうかをチェックできます。
* インストールされていない場合は、 `/usr/local/neolane/nl6/env.sh` スクリプトを作成し、ロケールをインストール済みのロケールに変更します。

## スクリプト「get_nms_amcGetSeedMetaData_jssp」のコンパイル中にエラーが発生した場合 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

AEMログファイルに次のエラーメッセージが表示される場合。

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

Adobe Campaign Classicサーバーで次の回避策を使用します。

1. ファイルを開く `$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js`
1. メソッドの 467 行を修正します `amcGetSeedMetaData`
1. `label : [inclView.@label](mailto:inclView.@label)` を `label : String([inclView.@label](mailto:inclView.@label))` に変更します。
1. 保存.
1. サーバーを再起動します。

## 「同期」ボタンのクリック時にAdobe Campaign Classicでエラーが表示される場合 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

クリック時に **同期** ボタンがAdobe Campaign Classicに表示される場合は、次のエラーが発生することがあります。

* `Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

この問題を修正するには、AEM接続 URL が **外部アカウント** Adobe Campaign Classicでは、マシンからアクセスできます。

スイッチ `localhost` を URL の IP アドレスに追加すると、多くの場合、この問題が解決されます。

## 「Cannot parse XTK Date+Time &#39;undefined&#39;」エラーが表示された場合 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

クリック後 **同期** AEMでは、ページ上のスクリプトが発生したというエラーが表示される場合があります。

* `Cannot parse XTK Date+Time 'undefined': not a valid XTK value.`

これは、AEMインスタンス上に古いAdobe Campaign Classic情報が存在する場合に発生します。 この問題を解決するには、次の方法があります。

1. AEM上にあるすべてのAdobe Campaign Classic統合設定の削除
1. 統合を再構築しています。
1. 新しいテンプレートを作成します。

## Cloud Serviceの設定時に SSL への接続でエラーが表示される場合 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

次の情報がに表示された場合は、Adobe Campaignサポートチームとチケットを発行してください。 `error.log` AEM.

```text
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

## 同期ダイアログに、期待される HTTPS リンクではなく HTTP リンクが表示される場合 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

AEMは、Adobe Campaign Classic配信でコンテンツを同期しようとすると、ニュースレターのリストを返します。 ただし、リスト内のニュースレターへの URL は、HTTPS ではなく HTTP アドレスになる場合があります。 リスト内の項目の 1 つを選択すると、エラーが発生します。 これは、次の設定で発生する可能性があります。

* AEM オーサーとの通信に https を使用してホストされたAdobe Campaign
* リバースプロキシが SSL を終了しています
* オンプレミスの AEM オーサーインスタンス

この問題を解決するには：

* 元のプロトコルをヘッダーとして渡すようにAEM Dispatcher またはリバースプロキシを設定する必要があります。
* この **Apache Felix Http Service SSL Filter** AEMの OSGi 設定では、必要なヘッダー設定を使用して設定する必要があります。
   * `https://<host>:<port>/system/console/configMgr`
   * [https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter) を参照

## ページプロパティでカスタムテンプレートを選択することはできません {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

AEM for Adobe Campaign Classicでメールテンプレートを作成する場合は、プロパティを含める必要があります `acMapping` 値 `mapRecipient` 内 `jcr:content` 」ノードを選択しないと、Adobe Campaign Classicテンプレートを **ページプロパティ** AEM. フィールドは無効に表示されます。

## AEMログに「com.day.cq.mcm.campaign.servlets.util.ParameterMapper」というエラーが表示される場合 {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

エラーが表示される場合があります `com.day.cq.mcm.campaign.servlets.util.ParameterMapper` (AEMで、カスタムテンプレートを使用する際に )

これは、 `acMapping` プロパティが `recipient.firstName`を指定した場合、空の値がAdobe Campaign Manager で作成されます。

この場合は、次の URL からAEM用の機能パック 6576 をインストールします。 [パッケージ共有](/help/sites-administering/package-manager.md#package-share).
