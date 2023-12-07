---
title: HTML5 フォームの最適化
description: Forms5 フォームの出力サイズは最適化することができますHTML。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 14309ebd-8d00-4ca5-b4ab-44d80d97d066
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 38%

---

# HTML5 フォームの最適化 {#optimizing-html-forms}

HTML5 フォームはフォームをHTML5 形式でレンダリングします。 フォームサイズやフォーム内の画像などの要因に応じて、結果の出力が大きくなる場合があります。 データ転送を最適化するために、推奨されるアプローチは要求を対処する Web サーバーを使用して HTML 応答を圧縮することです。このアプローチは、応答サイズ、ネットワークトラフィック、およびサーバーとクライアントマシンの間でのデータのストリーミングに要する時間を削減します。

この記事では、JBoss で Apache Web Server 2.0 32 ビットの圧縮を有効にするために必要な手順を説明します。

>[!NOTE]
>
>次の手順は Apache Web Server 2.0 32 ビット以外のサーバーには適用されません。

お使いのオペレーティングシステムに適した Apache Web サーバーソフトウェアを入手します。

* Windows の場合、Apache Web サーバーを Apache HTTP Server Project サイトからダウンロードします。
* Solaris 64 ビットの場合、Apache Web サーバーを Sunfreeware for Solaris Web サイトからダウンロードします。
* Linux の場合、Apache Web サーバーは Linux システムにプレインストールされています。

Apache は HTTP または AJP プロトコルを使用して JBoss と通信できます。

1. *APACHE_HOME/conf/httpd.conf* ファイル内で次のモジュール設定に対してコメント解除します。

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Linux の場合、デフォルトの APACHE_HOME ディレクトリは/etc/httpd/です。

1. JBoss のポート 8080 でプロキシを設定します。

   次の設定を *APACHE_HOME/conf/httpd.conf* 設定ファイルに追加します。

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >プロキシを使用する場合、次の設定変更が必要です。
   >
   >* アクセス：*https://&lt;server>:&lt;port>/system/console/configMgr*
   * Apache Sling Referrer Filter の設定を編集します。
   * 「Allow Hosts」で、プロキシサーバーのエントリを追加します。

1. 圧縮を有効化します。

   次の設定を *APACHE_HOME/conf/httpd.conf* 設定ファイルに追加します。

   ```xml
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. AEM サーバーにアクセスするには、https://[Apache_server]:80 を使用します。
