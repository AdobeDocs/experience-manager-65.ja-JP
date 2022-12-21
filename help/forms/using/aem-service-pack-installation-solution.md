---
title: 最新の 6.5.15.0サービスパックがインストールされると、CRX/bundle と開始ページサービスが使用できなくなる
description: 最新の 6.5.15.0サービスパックがインストールされると、CRX/bundle と開始ページサービスが使用できなくなる
source-git-commit: 813d8ffc53dc1928674367c9568b6269642cecb7
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 16%

---


# AEM (6.5.15.0) Service Pack のインストール後、サービスを利用できないエラーが発生しました {#steps-to-resolve-error-after-installing-service-pack}

## 問題 {#issue}

インストール後 [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)を含めない場合、エラーは次のように発生します。
* エラー [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException:org.apache.sling.scripting.console を解決できません

AEM 6.5.15.0サービスパックをインストールした後、CRX/bundle をパックし、開始ページに「サービスを使用できません」というエラーが表示されます。

## 適用先 {#applies-to}

このソリューションは次の場合に適用されます。
* JBoss EAP 7.4.0 上で動作するサーバーを除くすべての JEE サーバー上のAEM Forms

## ソリューション {#solution}

>[!NOTE]
>
>トラブルシューティング手順は、JBoss EAP 7.4 以外のすべてのアプリケーションサーバーに適用されます。

インストール後 [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)CRX/bundle と開始ページに「サービスを使用できません」というエラーが表示された場合は、次の手順を実行します。

1. アプリケーションサーバーを停止します。
1. `[aem-forms root]\crx-repository\launchpad\felix\bundle52` に移動します。
1. を `bundle.info` ファイル。
1. を開きます。 `bundle.info` ファイルを ant テキストエディターで検索し、バンドル名を `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >例えば、 `bundle.info` under `bundle52` 次を含まない `org.apache.felix.http.bridge` バンドル、 `org.apache.felix.http.bridge`. 次に、 [aem-forms ルート]\crx-repository\launchpad\felix\bundle[x] 次の手順をこの場所で実行します。

1. 次のURLに移動：: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. を検索 `bundle.jar` をクリックし、 `bundle.jar` から `bundle.jar.bak`.
1. コピー `bundle.jar` この場所で [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. アプリケーションサーバーを起動し、ログが安定するのを待って、バンドルの状態を確認します。
1. すべてのバンドルがアクティブ状態になったら、 `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` からのサーブレットフラグメント `system/console/bundles` 次からダウンロード： [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) アプリケーションサーバーが安定するのを待ちます。
1. アプリケーションサーバーを停止します。
1. に移動します。 `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` をクリックし、 `bundle.jar`.
1. 名前を変更 `bundle.jar.bak` から `bundle.jar`.
1. アプリケーションサーバーを起動します。