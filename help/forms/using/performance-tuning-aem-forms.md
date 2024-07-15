---
title: AEM Forms サーバーのパフォーマンスチューニング
description: AEM Forms が最適に動作するように、キャッシュ設定と JVM パラメーターを微調整できます。また、web サーバーを使用すると、AEM Forms デプロイメントのパフォーマンスを向上させることができます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: 22926757-9cdb-4f8a-9bd9-16ddbc3f954a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 100%

---

# AEM Forms サーバーのパフォーマンスチューニング{#performance-tuning-of-aem-forms-server}

この記事では、ボトルネックを減らし、AEM Forms デプロイメントのパフォーマンスを最適化するために実装できる戦略とベストプラクティスについて説明します。

## キャッシュ設定 {#cache-settings}

AEM Forms のキャッシュ戦略は、次の場所にある AEM web 設定コンソールの **Mobile Forms の設定**&#x200B;コンポーネントで設定および制御できます。

* (OSGi 上の AEM Forms) `https://'[server]:[port]'/system/console/configMgr`
* (JEE での AEM Forms) `https://'[server]:[port]'/lc/system/console/configMgr`

キャッシュに使用できるオプションを次に示します。

* **なし**：アーティファクトをキャッシュしません。これにより、実際にはパフォーマンスが低下し、キャッシュがないために高いメモリ可用性が必要になります。
* **保守的**：インラインフラグメントや画像を含むテンプレートなど、フォームのレンダリング前に生成される中間アーティファクトのみをキャッシュするように指示します。
* **アグレッシブ**：保守的なキャッシュレベルのすべてのアーティファクトに加えて、レンダリングされた HTML コンテンツを含め、キャッシュ可能なほぼすべてのものを強制的にキャッシュします。最良のパフォーマンスが得られますが、キャッシュされたアーティファクトの保存に多くのメモリが消費されます。アグレッシブキャッシュ戦略を使用すると、レンダリングされたコンテンツがキャッシュされるので、フォームのレンダリング時に一定時間のパフォーマンスが得られます。

AEM Forms のデフォルトのキャッシュ設定は、最適なパフォーマンスを得るのに十分でない可能性があります。そのため、次の設定を使用することをお勧めします。

* **キャッシュ戦略**：アグレッシブ
* **キャッシュサイズ**（フォーム数）：必要に応じて
* **最大オブジェクトサイズ**：必要に応じて

![Mobile Forms の設定](assets/snap.png)

>[!NOTE]
>
>AEM Dispatcher を使用してアダプティブフォームをキャッシュする場合、データが事前入力されたフォームが含まれているアダプティブフォームもキャッシュされます。このようなフォームが AEM Dispatcher のキャッシュから提供されると、事前入力されたデータや古いデータがユーザーに提供される場合があります。このため、AEM Dispatcher の使用は、データが事前入力されていないアダプティブフォームをキャッシュする場合に制限してください。また、Dispatcher のキャッシュでは、キャッシュされたフラグメントは自動的には無効になりません。そのため、フォームフラグメントをキャッシュするために使用しないでください。このようなフォームやフラグメントには、[アダプティブフォームのキャッシュ](../../forms/using/configure-adaptive-forms-cache.md)を使用します。

## JVM パラメーター {#jvm-parameters}

最適なパフォーマンスを得るために、次の JVM `init` 引数を使用して、`Java heap` と `PermGen` を設定することをお勧めします。

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>推奨設定は、Windows 2008 R2 8 コアおよび Oracle HotSpot 1.7 (64 ビット) JDK を対象とし、ご使用のシステム構成に従ってスケールアップまたはスケールダウンする必要があります。

## Web サーバーの使用 {#using-a-web-server}

アダプティブフォームと HTML5 フォームは、HTML5 形式でレンダリングされます。フォームサイズやフォーム内の画像などの要因によって、結果の出力が大きくなる場合があります。データ転送を最適化するために推奨されるアプローチは、リクエストが提供される web サーバーを使用して HTML 応答を圧縮することです。このアプローチでは、応答サイズ、ネットワークトラフィック、およびサーバーとクライアントマシンの間でのデータのストリーミングに要する時間を削減できます。

例えば、JBoss® 搭載の Apache Web Server 2.0 32 ビット上で圧縮を有効にするには、次の手順を実行します。

>[!NOTE]
>
>次の手順は Apache Web Server 2.0 32 ビット以外のサーバーには適用されません。その他のサーバーに固有の手順については、対応する製品ドキュメントを参照してください。

次の手順は、Apache Web Server で圧縮を有効にするために必要な変更を示しています。

**お使いのオペレーティングシステムに適した Apache Web Server ソフトウェアを入手します。**

* Windows：Apache HTTP Server Project のサイトから Apache Web Server をダウンロードします。
* Solaris™ 64 ビット：Solaris™ の Sunfreeware web サイトから Apache Web Server をダウンロードします。
* Linux®：Linux® システムには Apache Web Server がプレインストールされています。

Apache は HTTP プロトコルを使用して CRX と通信できます。これらの設定は、HTTP を使用した最適化のためのものです。

1. `APACHE_HOME/conf/httpd.conf` ファイル内で次のモジュール設定をコメント解除します。

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Linux® の場合、デフォルトの `APACHE_HOME` は `/etc/httpd/` です。

1. crx のポート 4502 のプロキシを設定します。次の設定を `APACHE_HOME/conf/httpd.conf` 設定ファイルに追加します。

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 圧縮を有効化します。次の設定を `APACHE_HOME/conf/httpd.conf` 設定ファイルに追加します。

   **HTML5 フォームの場合**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Do not compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **アダプティブフォームの場合**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Do not compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   crx サーバーにアクセスするには、`https://'server':80` を使用します。ここで、`server` は Apache サーバーが実行されているサーバーの名前です。

## AEM Forms が稼働しているサーバーでのウイルス対策ソフトウェアの使用 {#using-an-antivirus-on-server-running-aem-forms}

ウイルス対策ソフトウェアが実行されているサーバーでは、パフォーマンスが低下する場合があります。常時オンになっているウイルス対策（オンアクセススキャン）ソフトウェアは、システムのすべてのファイルをスキャンします。そのため、サーバーと AEM Forms のパフォーマンスが低下する可能性があります。

パフォーマンスを改善するには、以下に示す AEM Forms のファイルとフォルダーを常時オン（オンアクセス）スキャンから除外するようにウイルス対策ソフトウェアを設定してください。

* AEM のインストールディレクトリ。このディレクトリ全体を除外できない場合は、以下の項目を除外してください。

   * [AEM インストールディレクトリ]\crx-repository\temp
   * [AEM インストールディレクトリ]\crx-repository\repository
   * [AEM インストールディレクトリ]\crx-repository\launchpad

* アプリケーションサーバーの一時ディレクトリ。デフォルトの場所は以下のとおりです。

   * （JBoss®）[AEM installation directory]\jboss\standalone\tmp
   * （WebLogic）\Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * （WebSphere®）\Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **（AEM Forms on JEE のみ）**&#x200B;グローバルドキュメントストレージ（GDS）ディレクトリ。デフォルトの場所は以下のとおりです。

   * （JBoss®）[appserver root]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * （WebSphere®）[appserver root]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **（AEM Forms on JEE のみ）** AEM Forms サーバーのログと一時ディレクトリ。デフォルトの場所は以下のとおりです。

   * サーバーログ - [AEM Forms インストールディレクトリ]\Adobe\AEM forms\[app-server]\server\all\logs
   * 一時ディレクトリ - [AEM Forms インストールディレクトリ]\temp

>[!NOTE]
>
>* GDS と一時ディレクトリで異なる場所を使用している場合は、AdminUI`https://'[server]:[port]'/adminui` を開いて&#x200B;**ホーム／設定／コアシステム設定／コア設定**&#x200B;に移動し、現在使用している場所を確認してください。
>
* 上記のディレクトリを除外しても AEM Forms サーバーのパフォーマンスが改善されない場合は、Java™ 実行可能ファイル（java.exe）も除外してください。
>
