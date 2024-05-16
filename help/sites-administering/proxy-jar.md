---
title: プロキシサーバーツール（proxy.jar）
description: Adobe Experience Manager のプロキシサーバーツール（proxy.jar）について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 3df50303-5cdd-4df0-abec-80831d2ccef7
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: ht
source-wordcount: '1174'
ht-degree: 100%

---

# プロキシサーバーツール（proxy.jar）{#proxy-server-tool-proxy-jar}

プロキシサーバーは、クライアントとサーバー間のリクエストをリレーする中間サーバーとして機能します。プロキシサーバーは、クライアントとサーバーのインタラクションをすべて追跡し、TCP 通信全体のログを出力します。これにより、メインのサーバーにアクセスすることなく、現状を正確に監視できます。

プロキシサーバーは、該当するインストールフォルダーにあります。

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

基盤となる通信プロトコルに関係なく、プロキシサーバーを使用して、クライアントとサーバーのインタラクションをすべて監視できます。例えば、以下のプロトコルを監視できます。

* HTTP（Web ページ用）
* HTTPS（セキュリティで保護された web ページ用）
* SMTP（メールメッセージ用）
* LDAP（ユーザー管理用）

例えば、TCP/IP ネットワーク経由で通信する任意の 2 つのアプリケーション（Web ブラウザーと AEM など）の間にプロキシサーバーを配置できます。これにより、AEM ページのリクエスト時の状況を的確に監視できます。

## プロキシサーバーツールの起動 {#starting-the-proxy-server-tool}

このツールは、AEM インストール環境の /opt/helpers フォルダーにあります。このツールを起動するには、次のように入力します。

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### オプション {#options}

* **q（静止モード）**&#x200B;コンソールウィンドウにリクエストを書き込みません。接続速度を低下させたくない場合や出力をファイルに記録する場合は、このオプションを使用します（-logfile オプションを参照）。
* **b（バイナリモード）**&#x200B;トラフィック内で特定のバイトの組み合わせを検索する場合は、バイナリモードを有効にします。出力には 16 進および文字の出力が含まれます。
* **t（タイムスタンプログエントリ）**&#x200B;各ログ出力にタイムスタンプを追加します。タイムスタンプは秒単位なので、単一のリクエストの確認には適していない場合があります。長時間プロキシサーバーを使用する場合は、特定の時刻に発生したイベントを特定するためにこのオプションを使用します。
* **logfile &lt;filename>（ログファイルに書き込み）**&#x200B;クライアントとサーバーのやり取りをログファイルに書き込みます。このパラメーターは静止モードでも使用できます。
* **i &lt;numIndentions>（インデントを追加）**&#x200B;アクティブな各接続は、読みやすくするためにインデントされます。デフォルト値は 16 レベルです（proxy.jar バージョン 1.16 の新機能です）。

## プロキシサーバーツールの使用 {#uses-of-the-proxy-server-tool}

次のシナリオは、プロキシサーバーツールの用途の一部を示しています。

**Cookie とその値の確認**

次のログエントリの例は、プロキシの起動後に開かれた 6 番目の接続でクライアントが送信したすべての Cookie とその値を示しています。

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**ヘッダーとその値の確認**&#x200B;次のログエントリの例は、サーバーがキープアライブ接続を確立して、Content-Length ヘッダーが正しく設定されたことを示しています。

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**キープアライブが機能するかどうかの確認**

**キープアライブ**&#x200B;とは、クライアントがサーバーへの接続を再利用して、複数のファイル（ページコード、画像、スタイルシートなど）を転送することを意味します。キープアライブを使用しない場合、クライアントはリクエストごとに新しい接続を確立する必要があります。

キープアライブが機能するかどうかを確認するには：

1. プロキシサーバーを起動します。
1. ページのリクエストを行います。

* キープアライブが機能している場合は、接続カウンターで接続数が 5～10 を超えることはありません。
* キープアライブが機能していない場合は、接続カウンターが急激に増加します。

**失われたリクエストの検索**

複雑なサーバー設定でリクエストが失われた場合（例えば、ファイアウォールとディスパッチャーを使用する場合）は、プロキシサーバーを使用して、リクエストがどこで失われたかを特定できます。ファイアウォールがある場合は、次の手順を実行します。

1. ファイアウォールの前にプロキシを起動します。
1. ファイアウォールの後にもう 1 つのプロキシを起動します。
1. この 2 つのプロキシを使用して、リクエストがどこまで届いているかを確認します。

**リクエストのハング**

リクエストがハングすることがある場合は、次の手順を実行します。

1. proxy.jar を起動します。
1. 待機するか、エントリごとにタイムスタンプを付けて、アクセスログをファイルに書き込みます。
1. リクエストがハングし始めたら、開いた接続の数および問題の原因となったリクエストを確認できます。

## ログメッセージの形式 {#the-format-of-log-messages}

proxy.jar が生成するログエントリはすべて次の形式になります。

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

例えば、web ページのリクエストは次のようになります。

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C は、このエントリがクライアントからのリクエスト（Web ページのリクエスト）であることを示します。
* 0 は接続数です（接続カウンターは 0 から開始します）。
* #00000 はバイトストリームのオフセットです。これは最初のエントリなので、オフセットは 0 です。
* [GET &lt;?>] は、サンプルの HTTP ヘッダー（URL）におけるリクエストのコンテンツです。

接続を閉じると、次の情報がログに記録されます。

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

これは、6 番目の接続において平均速度でクライアントとサーバー間で渡されたバイト数を示します。

## ログ出力の例 {#an-example-of-log-output}

リクエスト時に次のコードを生成する単純なテンプレートについて検討します。

```xml
<html>
  <head>
    <title>Welcome</title>
  </head>
  <body>
    Welcome to Playground<br>
    <img src="/logo.gif">
  </body>
</html>
```

AEM が localhost:4303 で実行されている場合は、プロキシサーバーを次のように起動します。

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

プロキシサーバーなしでサーバー（`localhost:4303`）にアクセスできますが、`localhost:4444` 経由でアクセスすると、プロキシサーバーは通信をログに記録します。ブラウザーを開き、上記のテンプレートを使用して作成されたページにアクセスしてください。その後、ログファイルを確認します。

>[!NOTE]
>
>proxy.jar バージョン 1.14 までは、1 つの接続のログエントリは同期されません。つまり、1 つのクライアント／サーバー接続のログエントリは、必ずしも正しい順序ではないということです。これより新しいバージョン（1.14 以降）のプロキシサーバーには、この問題はありません。

起動時に、次の情報がログに書き込まれます。

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

最初の接続（0）の開始時に、以下のヘッダーフィールドがリストされます。これはメインの HTML ページをリクエストしています。

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

クライアントがキープアライブ接続をリクエストするので、サーバーは同じ接続で複数のファイルを送信できます。

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

プロキシサーバーは、Cookie が適切に設定されているかどうかの確認に適したツールです。ここでは、以下を確認できます。

* AEM によって生成された cq3session Cookie
* CFC によって生成された表示モード切り替え Cookie
* JSESSIONID という名前の Cookie。&lt;%@ page session=&quot;false&quot; %> を使用して明示的にオフにしない場合は、JSP によって自動的に作成されます。

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

リクエスト後、サーバーは接続 0 を閉じます。リクエストに疑問符が含まれているので、キープアライブはできません。つまり、サーバーはキャッシュされているバージョンを返せないので、キープアライブ接続で必要とする、この時点でのコンテンツの長さを特定できません。

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

ここでは、サーバーが接続 0 で HTML コードの送信を開始します。

```xml
S-0-#000234 -> [<html> ]
S-0-#000242 -> [.<head> ]
S-0-#000251 -> [..<title>Welcome</title> ]
S-0-#000277 -> [.</head> ]
S-0-#000287 -> [.<body> ]
S-0-#000296 -> [..Welcome to Playground<br> ]
S-0-#000325 -> [..<img src="/author/logo.gif"> ]
S-0-#000357 -> [.</body> ]
S-0-#000367 -> [</html>]
```

HTML ファイルが送信された直後に、接続 0 が閉じられます。

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

今度は、接続 1 のための出力が開始され、HTML コードに含まれる画像がダウンロードされます。

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

再び、クライアントがキープアライブ接続をリクエストします。

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

接続 1 では、画像が静的であるためにコンテンツの長さがわかるので、サーバーはキープアライブを提供できます。

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

サーバーが接続 1 で画像のコンテンツの長さを返します。

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

コンテンツの長さが確立されたので、サーバーは接続 1 で画像データを送信します。

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

キープアライブのタイムアウトに達すると、接続 1 も同様に閉じられます。

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

上記の例は、2 つの接続が連続して発生するので、比較的単純です。

* 最初にサーバーが HTML コードを返す
* 次にブラウザーが画像をリクエストし、新しい接続を開く

実際には、ページは、画像、スタイルシート、JavaScript ファイルなどに対して、多数の並列リクエストを生成する場合があります。つまり、ログには、並列オープン接続の重複するエントリが存在します。この場合、読みやすさを向上させるために -i オプションを使用することをお勧めします。
