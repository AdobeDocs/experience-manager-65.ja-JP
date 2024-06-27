---
title: 最新の 6.5.15.0 サービスパックがインストールされると、CRX/bundle と開始ページサービスが利用できないというエラーが表示される
description: 最新の 6.5.15.0 サービスパックがインストールされると、CRX/bundle と開始ページサービスが利用できないというエラーが表示される
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '276'
ht-degree: 100%

---

# AEM（6.5.15.0）サービスパックのインストール後に、サービスが使用できないというエラーが表示される {#steps-to-resolve-error-after-installing-service-pack}

## 問題 {#issue}

[AEM 6.5.15.0 サービスパック](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)のインストール後、次のようなエラーが発生します。
* ERROR [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: Unable to resolve org.apache.sling.scripting.console

AEM 6.5.15.0 サービスパックをインストールした後、CRX/bundle と開始ページにサービスを利用できないというエラーが表示されます。

## 適用先 {#applies-to}

このソリューションは次の場合に適用されます。
* JBoss EAP 7.4.0 で実行されているサーバーを除くすべての JEE サーバー上の AEM Forms

## 解決策 {#solution}

>[!NOTE]
>
>トラブルシューティングの手順は、JBoss EAP 7.4 を除くすべてのアプリケーションサーバーに適用されます。

[AEM 6.5.15.0 サービスパック](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)のインストール後、CRX/bundle と開始ページにサービスを利用できないというエラーが表示される場合は、次の手順を実行します。

1. アプリケーションサーバーを停止します。
1. `[aem-forms root]\crx-repository\launchpad\felix\bundle52` に移動します。
1. `bundle.info` ファイルを見つけます。
1. ant テキストエディターで `bundle.info` ファイルを開き、バンドル名を `org.apache.felix.http.bridge` として検索します。

   >[!NOTE]
   >
   >`bundle52` の下の `bundle.info` に `org.apache.felix.http.bridge` バンドルが含まれていない場合は、`org.apache.felix.http.bridge` の横にある角括弧内のバンドル番号を確認してください。次に、[aem-forms root]\crx-repository\launchpad\felix\bundle[x] に移動し、次の手順をこの場所で実行します。

1. 次のURLに移動：`[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`。
1. `bundle.jar` を検索し、`bundle.jar` の名前を `bundle.jar.bak` に変更します。
1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar)からこの場所の `Bundle for AEM 6.5 Forms on JEE Service Pack 15` をコピーします。
1. アプリケーションサーバーを起動し、ログが安定するのを待ってから、バンドルの状態を確認します。
1. すべてのバンドルがアクティブな状態になったら、[AEM 6.5 Forms on JEE サービスパック 15 のフラグメント](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)を `system/console/bundles` からインストールし、アプリケーションサーバーが安定するまで待ちます。
1. アプリケーションサーバーを停止します。
1. `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` に移動し、`bundle.jar` を削除します。
1. `bundle.jar.bak` の名前を `bundle.jar` に変更します。
1. アプリケーションサーバーを起動します。
