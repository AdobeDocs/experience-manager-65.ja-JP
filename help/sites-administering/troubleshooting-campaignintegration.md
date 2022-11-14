---
title: Adobe Campaign 統合に関するトラブルシューティング
seo-title: Troubleshooting your Adobe Campaign Integration
description: Adobe Campaign 統合に関する問題をトラブルシューティングする方法について説明します。
seo-description: Learn how to troubleshoot issues with the Adobe Campaign Integration.
uuid: 835ac2c3-ef2f-4963-9047-aeda3647b114
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b1d45f01-78de-423c-8f6b-5cb7067c3a2f
exl-id: 317bab41-3504-4e46-9ddc-72e291a34e06
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 99%

---

# Adobe Campaign 統合に関するトラブルシューティング{#troubleshooting-your-adobe-campaign-integration}

>[!NOTE]
>
>このページは Campaign Classic に適用されます。

次のトラブルシューティングヒントは、AEM を Adobe Campaign と統合する際に発生する最も一般的な問題を解決するのに役立ちます。

## トラブルシューティングに関する一般的なヒント {#general-troubleshooting-tips}

両方の統合において、HTTP の呼び出し（AEM から Adobe Campaign、Adobe Campaign から AEM）が送信されているかどうかをチェックできます。

* 統合でエラーが発生しているときは、それらの呼び出しがもう一方に届いていることを確認します（ファイアウォールや SSL の問題を回避するため）。
* AEM の機能では、JSON の呼び出しが AEM オーサーインターフェイスからリクエストされます。HTTP 500 のエラーは発生しません。HTTP 500 のエラーが発生した場合は、`error.log` で詳細を確認してください。
* AEM でキャンペーンクラスのデバッグレベルを上げることも問題のトラブルシューティングに役立ちます。

## 接続に失敗する場合 {#if-the-connection-fails}

Adobe Campaign で **aemserver** 演算子が設定されていることをチェックします。

## 画像が Adobe Campaign コンソールに表示されない場合 {#if-images-do-not-appear-in-the-adobe-campaign-console}

HTML ソースをチェックし、クライアントマシンから URL を開くことができることを検証します。URL に localhost:4503 が含まれている場合、オーサーインスタンスの Day CQ Link Externalizer の設定を、Adobe Campaign コンソールマシンから到達できるパブリッシュインスタンスを指すように変更します。

[Externalizer の設定](/help/sites-administering/campaignstandard.md#configuring-the-externalizer) を参照してください。

## AEM から Adobe Campaign に接続できない場合 {#if-you-cannot-connect-from-aem-to-adobe-campaign}

Adobe Campaign で次のエラーメッセージを探します。

`No datasource defined in the instance 'default'.`

`Make sure the DNS alias used to access the server is correct (for example, avoid hard-coded IP addresses). (iRc=16384)`

この問題を修正するには、**$CAMPAIGN_HOME/conf/config-&lt;instance-name>.xml** で次を変更します。

`<dataStore hosts="*" lang="en_GB">`

## Adobe Campaign ダイアログにデータが表示されない場合 {#if-no-data-displays-in-the-adobe-campaign-dialog}

Adobe Campaign で、ポート番号の末尾がスラッシュ（/）で終わらないようにします。

![chlimage_1-149](assets/chlimage_1-149.png)

## setlocale について警告が表示される場合 {#if-you-get-a-warning-about-your-setlocale}

Apache HTTPD サービスを開始しており、「`"Warning: setlocale: LC_CTYPE cannot change locale"`」というエラーが表示される場合は、システムに **en_CA.ISO-8859-15 locale** がインストールされていることを確認してください。

`local -a` を使用することで、インストールされているかどうかをチェックできます。インストールされていない場合は、**/usr/local/neolane/nl6/env.sh** スクリプトをパッチして、ロケールをインストールされたロケールに変更します。

## スクリプト「get_nms_amcGetSeedMetaData_jssp」のコンパイル中にエラーが発生した場合 {#if-you-get-an-error-while-compiling-script-get-nms-amcgetseedmetadata-jssp}

AEM ログファイルに次のエラーメッセージが表示される場合：

`com.day.cq.mcm.campaign.impl.CampaignConnectorImpl Internal Adobe Campaign error: response body is Error while compiling script 'get_nms_amcGetSeedMetaData_jssp' line 45: String.prototype.toJSON called on incompatible XML.`

次の回避策を使用します。

1. **$CAMPAIGN_HOME/datakit/nms/fra/js/amcIntegration.js** ファイルを開きます。
1. メソッド「amcGetSeedMetaData」の 467 行目を変更します。
1. `label : [inclView.@label](mailto:inclView.@label)` を `label : String([inclView.@label](mailto:inclView.@label))` に変更します。

1. 保存.
1. サーバーを再起動します。

## Adobe Campaign で「同期」ボタンをクリックしたときにエラーが表示される場合 {#if-adobe-campaign-displays-an-error-when-clicking-the-synchronize-button}

Adobe Campaign Classic で「**同期**」ボタンをクリックすると、次のエラーが表示される場合：

`Error while executing the method ‘aemListContent' of service [nms:delivery](https://nmsdelivery/)`

この問題を解決するには、外部アカウントで設定されている AEM の接続 URL にマシンからアクセスできることを確認してください。

**localhost** から IP アドレスに切り替えるとこの問題が解決します。

## 「Cannot parse XTK Date+Time &#39;undefined」というエラーが発生する場合 {#if-you-get-a-cannot-parse-xtk-date-time-undefined-error}

「同期」をクリックした後に、「Cannot parse XTK Date+Time &#39;undefined&#39;: not a valid XTK value」とページのスクリプトが発生した内容のエラーが発生します。

これは AEM インスタンスに期限切れの Adobe Campaign の情報が残っている場合に発生します。AEM 上にあるすべての Campaign 統合設定を削除して再構築することで、この問題を解決します。次に、新しいテンプレートを作成します。

## クラウドサービスをセットアップしているときに SSL に接続するとエラーが発生する場合 {#if-a-connection-to-ssl-displays-an-error-when-setting-up-the-cloud-service}

AEM の error.log に、次のログが表示されます。

```xml
javax.net.ssl.SSLProtocolException: handshake alert:  unrecognized_name
at sun.security.ssl.ClientHandshaker.handshakeAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.recvAlert(Unknown Source)
at sun.security.ssl.SSLSocketImpl.readRecord(Unknown Source)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(Unknown Source)
at sun.security.ssl.SSLSocketImpl.writeRecord(Unknown Source)
at sun.security.ssl.AppOutputStream.write(Unknown Source)
```

チケットを切って Adobe Campaign のサポートチームにサポートを依頼してください。

## 同期ダイアログに想定していた https のリンクではなく http のリンクが表示される場合 {#if-you-see-http-instead-of-an-expected-https-links-in-the-synchronization-dialog}

セットアップは次のとおりです。

* AEM Author との通信に https を使用して Adobe Campaign をホストした
* リバースプロキシが SSL を終了している
* オンプレミスの AEM オーサーインスタンス

Adobe Campaign の配信でコンテンツを同期しようとすると、AEM はニュースレターのリストを返します。ただし、リスト内のニュースレターへの URL は http のアドレスです。リスト内のいずれかの項目を選択すると、エラーが発生します。

この問題を解決するには：

* 元のプロトコルをヘッダーとして渡すように、ディスパッチャーまたはリバースプロキシを設定する必要があります。
* OSGi 設定（[https://&lt;host>:&lt;port>/system/console/configMgr](http://localhost:4502/system/console/configMgr)）の *Apache Felix Http Service SSL Filter* をそれぞれのヘッダー設定に合わせて設定する必要があります。[https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter](https://felix.apache.org/documentation/subprojects/apache-felix-http-service.html#using-the-ssl-filter) を参照

## 自身で作成したカスタムテンプレートをページのプロパティで選択できない場合 {#if-the-custom-template-i-created-cannot-be-selected-in-page-properties}

Adobe Campaign のメールテンプレートを作成する際には、テンプレートの **jcr:content** ノードにプロパティ **acMapping** と値 **mapRecipient** を指定する必要があります。指定しない場合、AEM の「**ページのプロパティ**」フィールドで Adobe Campaign のテンプレートを選択できなくなります（フィールドが無効化されています）。

## ログに「com.day.cq.mcm.campaign.servlets.util.ParameterMapper」というエラーが発生する場合 {#if-you-get-the-error-com-day-cq-mcm-campaign-servlets-util-parametermapper-in-your-logs}

カスタムテンプレートを使用しているときに、ログに「com.day.cq.mcm.campaign.servlets.util.ParameterMapper」というエラーが発生します。この場合は、[パッケージ共有](/help/sites-administering/package-manager.md#package-share)からフィーチャーパック 6576 をインストールしてください。これは、acMapping プロパティの値が recipient.firstName 以外に設定されている場合に、Adobe Campaign Manager 側で空の値が作成される問題です。
