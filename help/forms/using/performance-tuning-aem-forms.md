---
title: AEM Forms サーバーのパフォーマンスチューニング
seo-title: AEM Forms サーバーのパフォーマンスチューニング
description: AEM Forms が最適に動作するようにするために、キャッシュ設定と JVM パラメーターを微調整することができます。また、Web サーバーを使用することにより AEM Forms デプロイメントのパフォーマンスを向上することもできます。
seo-description: AEM Forms が最適に動作するようにするために、キャッシュ設定と JVM パラメーターを微調整することができます。また、Web サーバーを使用することにより AEM Forms デプロイメントのパフォーマンスを向上することもできます。
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
role: Admin
exl-id: 22926757-9cdb-4f8a-9bd9-16ddbc3f954a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 79%

---

# AEM Forms サーバーのパフォーマンスチューニング{#performance-tuning-of-aem-forms-server}

この記事では、AEM Forms デプロイメントのボトルネックを減少しパフォーマンスを最適化するための戦略とベストプラクティスを検討します。

## キャッシュ設定 {#cache-settings}

AEM Web 設定コンソールの **Mobile Forms の設定**&#x200B;コンポーネントを使用して、AEM Forms のキャッシュ方法の設定と制御を行うことができます。AEM Web 設定コンソールの URL は次のとおりです。

* (OSGi 上の AEM Forms) `https://'[server]:[port]'/system/console/configMgr`
* (JEE での AEM Forms) `https://'[server]:[port]'/lc/system/console/configMgr`

キャッシングに使用できるオプションは次のとおりです。

* **なし**：すべてのアーチファクトをキャッシュしません。これにより、実務上、パフォーマンスが低下し、キャッシュがないために高いメモリ可用度を必要とします。
* **保守的**：インラインのフラグメントや画像を含むテンプレートなど、フォームのレンダリング前に生成される中間的なアーチファクトのみをキャッシュします。
* **アグレッシブ**： 保守的キャッシングレベルのすべてのアーチファクトの他に、レンダリングされた HTML コンテンツなど、キャッシュ可能なほとんどすべてのものをキャッシュします。これにより最良のパフォーマンスが得られますが、キャッシュされたアーチファクトを保存するために多くのメモリを消費することになります。アグレッシブキャッシング戦略では、レンダリングされたコンテンツがキャッシュされるので、フォームのレンダリングにおいて一定時間のパフォーマンスが得られます。

AEM Forms のデフォルトキャッシュ設定は、最適なパフォーマンスを得るためには十分でない場合があります。したがって、次の設定を使用することを推奨します。

* **キャッシュ戦略**：アグレッシブ
* **キャッシュサイズ**（フォーム数）：必要に応じて
* **最大オブジェクトサイズ**：必要に応じて

![Mobile Forms の設定](assets/snap.png)

>[!NOTE]
>
>AEM ディスパッチャーを使用してアダプティブフォームをキャッシュする場合、データが事前入力されたフォームが含まれているアダプティブフォームもキャッシュされます。このようなフォームが AEM ディスパッチャーのキャッシュから提供されると、事前入力されたデータや古いデータがユーザーに提供される場合があります。このため、AEM ディスパッチャーの使用は、データが事前入力されていないアダプティブフォームをキャッシュする場合に制限してください。さらに、ディスパッチャーのキャッシュではキャッシュされたフラグメントが自動的に無効になりません。このため、フォームフラグメントをキャッシュする場合には使用しないでください。このようなフォームとフラグメントには、[アダプティブフォームのキャッシュ](../../forms/using/configure-adaptive-forms-cache.md)を使用してください。

## JVM パラメーター {#jvm-parameters}

最適なパフォーマンスを得るには、次のJVM `init`引数を使用して`Java heap`および`PermGen`を設定することをお勧めします。

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>推奨設定は、Windows 2008 R2 8 CoreおよびOracleHotSpot 1.7（64ビット）JDK用で、システム構成に従って拡大または縮小する必要があります。

## Web サーバーの使用 {#using-a-web-server}

アダプティブフォームおよび HTML5 フォームは HTML5 形式でレンダリングします。フォームサイズとフォーム内の画像のような要素によって、結果の出力が大きくなる場合があります。データ転送を最適化するために、推奨されるアプローチは要求を対処する Web サーバーを使用して HTML 応答を圧縮することです。このアプローチは応答サイズ、ネットワークトラフィック、およびサーバーとクライアントマシンの間でのデータのストリーミングに要する時間を減少させます。

例えば、次の手順を実行して、JBoss 搭載の Apache Web Server 2.0 32 ビット上で圧縮を有効にします。

>[!NOTE]
>
>次の手順は、Apache Web Server 2.0 32ビット以外のサーバーには適用されません。 その他のサーバーに固有の手順については、対応する製品ドキュメントを参照してください。

次の手順では、Apache Web サーバーで圧縮を有効にするために必要な変更を示します。

**オペレーティングシステムに適した Apache Web サーバーソフトウェアを入手します。**

* Windows：Apache Web サーバーを Apache HTTP Server Project サイトからダウンロードします。
* Solaris 64 ビット：Apache Web サーバーを Sunfreeware Solaris Web サイトからダウンロードします。
* Linux：Apache Web サーバーは Linux システムにプレインストールされています。

Apache は HTTP プロトコルを使用して CRX と情報をやり取りできます。HTTP を使用した場合に最適化される設定になっています。

1. `APACHE_HOME/conf/httpd.conf`ファイル内で次のモジュール設定のコメントを解除します。

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Linuxの場合、デフォルトの`APACHE_HOME`は`/etc/httpd/`です。

1. crx のポート 4502 のプロキシを設定します。次の設定を`APACHE_HOME/conf/httpd.conf`構成ファイルに追加します。

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 圧縮を有効化します。次の設定を`APACHE_HOME/conf/httpd.conf`構成ファイルに追加します。

   **HTML5 フォームの場合**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
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
           #Don’t compress
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

ウイルス対策ソフトウェアが実行されているサーバーでは、パフォーマンスが低下する場合があります。常時オンになっているウイルス対策ソフトウェア（オンアクセススキャン）は、システム上のすべてのファイルをスキャンします。そのため、サーバーと AEM Forms のパフォーマンスが低下する可能性があります。

パフォーマンスを改善するには、以下に示す AEM Forms のファイルとフォルダーを常時オンのスキャン（オンアクセススキャン）から除外するようにウイルス対策ソフトウェアを設定してください。

* AEM のインストールディレクトリ。このディレクトリ全体を除外できない場合は、以下の項目を除外してください。

   * [AEMインストールディレクトリ]\crx-repository\temp
   * [AEMインストールディレクトリ]\crx-repository\repository
   * [AEMインストールディレクトリ]\crx-repository\launchpad

* アプリケーションサーバーの一時ディレクトリ。デフォルトの場所は以下のとおりです。

   * (Jboss) [AEM installation directory]\jboss\standalone\tmp
   * Weblogic - \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * Websphere - \Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **（JEE 上の AEM Forms のみ）** Global Document Storage（GDS）ディレクトリ。デフォルトの場所は以下のとおりです。

   * (JBoss) [appserver root]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver root]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **（JEE 上の AEM Forms のみ）** AEM Forms サーバーのログファイルと一時ディレクトリ。デフォルトの場所は以下のとおりです。

   * サーバーログ — [AEM Forms installation directory]\Adobe\AEM forms\[app-server]\server\all\logs
   * 一時ディレクトリ — [AEM Forms installation directory]\temp

>[!NOTE]
>
>* GDSと一時ディレクトリに別の場所を使用している場合は、`https://'[server]:[port]'/adminui`でAdminUIを開き、**ホーム/設定/コアシステム設定/コア設定**&#x200B;に移動して、使用中の場所を確認します。

* 推奨ディレクトリを除外した後でもAEM Formsサーバーのパフォーマンスが低下した場合は、Java実行ファイル(java.exe)も除外します。


