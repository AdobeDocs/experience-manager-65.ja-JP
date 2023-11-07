---
title: プロキシサーバーツール（proxy.jar）
description: Adobe Experience Managerのプロキシサーバーツール (proxy.jar) について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 3df50303-5cdd-4df0-abec-80831d2ccef7
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 8%

---

# プロキシサーバーツール（proxy.jar）{#proxy-server-tool-proxy-jar}

プロキシサーバは、クライアントとサーバとの間で要求を中継する中間サーバとして機能します。 プロキシサーバは、すべてのクライアントとサーバとのやり取りを追跡し、TCP 通信全体のログを出力します。 これにより、メインサーバーにアクセスしなくても、何が起こっているかを正確に監視できます。

プロキシサーバーは、適切なインストールフォルダーにあります。

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

プロキシサーバーを使用すると、基になる通信プロトコルに関係なく、クライアントとサーバーの間のすべてのやり取りを監視できます。 例えば、次のプロトコルを監視できます。

* Web ページの HTTP
* セキュリティで保護された Web ページの HTTPS
* 電子メールメッセージ用の SMTP
* ユーザー管理用の LDAP

例えば、TCP/IP ネットワークを介して通信する 2 つのアプリケーション (Web ブラウザーとAEMなど ) 間にプロキシサーバーを配置できます。 これにより、AEMページをリクエストしたときの動作を正確に監視できます。

## プロキシサーバーツールの起動 {#starting-the-proxy-server-tool}

このツールは、AEM インストール環境の /opt/helpers フォルダーにあります。このツールを起動するには、次のように入力します。

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### オプション {#options}

* **q（静止モード）** コンソールウィンドウにリクエストを書き込みません。 接続速度を低下させたくない場合や、出力をファイルに記録する場合（ —logfile オプションを参照）に、このオプションを使用します。
* **b（バイナリモード）** トラフィックで特定のバイトの組み合わせを探している場合は、バイナリモードを有効にします。 出力には、16 進数と文字の出力が含まれます。
* **t（タイムスタンプログエントリ）** 各ログ出力にタイムスタンプを追加します。 タイムスタンプは秒単位なので、単一のリクエストの確認には適さない場合があります。 この関数を使用して、長い期間プロキシサーバーを使用する場合は、特定の時間に発生したイベントを見つけます。
* **logfile &lt;filename> （ログファイルに書き込み）** クライアントとサーバーの会話をログファイルに書き込みます。 このパラメーターは、クワイエットモードでも機能します。
* **i &lt;numindentions> （インデントの追加）** アクティブな各接続は、読みやすくするためにインデントされます。 デフォルトは 16 レベルです。 （proxy.jar バージョン 1.16 の新機能）。

## プロキシサーバーツールの使用 {#uses-of-the-proxy-server-tool}

次のシナリオは、プロキシサーバーツールの用途の一部を示しています。

**Cookie とその値の確認**

次のログエントリの例は、プロキシの開始後に開かれた 6 番目の接続でクライアントが送信したすべての cookie とその値を示しています。

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**ヘッダーとその値の確認** 次のログエントリの例は、サーバーがキープアライブ接続を確立でき、コンテンツの長さのヘッダーが正しく設定されたことを示しています。

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**キープアライブが機能するかどうかの確認**

**キープアライブ** とは、クライアントがサーバーへの接続を再利用して、複数のファイル（ページコード、画像、スタイルシートなど）を転送することを意味します。 キープアライブを使用しない場合、クライアントはリクエストごとに新しい接続を確立する必要があります。

キープアライブが機能するかどうかを確認するには：

1. プロキシサーバーを起動します。
1. ページをリクエストします。

* キープアライブが機能している場合、接続カウンターは 5～10 接続を超えないでください。
* キープアライブが機能していない場合、接続カウンターは急速に増加します。

**失われたリクエストの検索**

複雑なサーバー設定（ファイアウォールや Dispatcher を使用している場合など）でリクエストが失われた場合、プロキシサーバーを使用して、リクエストが失われた場所を特定できます。 ファイアウォールがある場合：

1. ファイアウォールの前にプロキシを開始する
1. ファイアウォール後に別のプロキシを開始する
1. これらを使用して、リクエストの取得範囲を確認します。

**要求のハング**

リクエストが時々ハングする場合：

1. proxy.jar を起動します。
1. 待つか、アクセスログをファイルに書き込みます。各エントリにはタイムスタンプが設定されます。
1. リクエストがハングし始めると、オープンした接続の数と、問題を引き起こしているリクエストを確認できます。

## ログメッセージの形式 {#the-format-of-log-messages}

proxy.jar によって生成されるログエントリは、すべて次の形式になります。

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

例えば、Web ページのリクエストは次のようになります。

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C は、このエントリがクライアントから送信されたことを示します（Web ページのリクエストです）。
* 0 は接続番号です（接続カウンターは 0 から始まります）
* #00000バイトストリーム内のオフセット。これは最初のエントリなので、オフセットは 0 です。
* [GET &lt;?>] は、サンプルの HTTP ヘッダー（URL）におけるリクエストのコンテンツです。

接続を閉じると、次の情報がログに記録されます。

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

これは、6 番目の接続で、平均速度でクライアントとサーバーの間で渡されたバイト数を示します。

## ログ出力の例 {#an-example-of-log-output}

要求された場合に次のコードを生成する簡単なテンプレートを確認します。

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

AEMが localhost:4303 で実行されている場合は、次のようにプロキシサーバーを起動します。

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

サーバーにアクセスできます (`localhost:4303`) を使用しますが、 `localhost:4444`に設定すると、プロキシサーバーは通信をログに記録します。 ブラウザーを開き、上記のテンプレートを使用して作成されたページにアクセスしてください。その後、ログファイルを確認します。

>[!NOTE]
>
>proxy.jar バージョン 1.14 までは、1 つの接続のログエントリは同期されません。つまり、1 つのクライアント/サーバー接続のログエントリが正しい順序で必要ないことを意味します。 プロキシサーバーの新しいバージョン (>=1.14) には、この問題はありません。

起動時に、次の情報がログに書き込まれます。

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

メイン接続ページをリクエストする最初の接続 (0) の開始時に、次のヘッダーフィールドがHTMLされます。

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

クライアントはキープアライブ接続を要求するので、サーバーは同じ接続を介して複数のファイルを送信できます。

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

プロキシサーバーは、Cookie が正しく設定されているかどうかを確認するのに適したツールです。 ここでは、次の情報が表示されます。

* AEMで生成された cq3session cookie
* CFC によって生成される show mode スイッチ cookie
* JSESSIONID という名前の cookie。&lt;%@ page session=&quot;false&quot; %> を使用して明示的にオフにしない場合は、JSP によって自動的に作成されます。

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

要求後、サーバーは接続 0 を閉じます。 リクエストに疑問符が含まれているので、キープアライブはできません。 つまり、サーバーはキャッシュされたバージョンを返せないので、この時点でのコンテンツの長さを判断できません。これはキープアライブ接続に必要です。

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

ここでは、サーバーが接続 0 でHTMLコードの送信を開始します。

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

接続 0 は、HTML・ファイルが提供された直後に閉じます。

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

これで、接続 1 の出力が開始し、接続コードに含まれる画像がダウンロードされます。HTML1:

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

この場合も、クライアントはキープアライブ接続を要求します。

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

接続 1 では、画像が静的なのでコンテンツの長さがわかるので、サーバーはキープアライブを提供できます。

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

サーバーが接続 1 の画像のコンテンツ長を返します。

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

キープアライブタイムアウトに達すると、接続 1 も閉じます。

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

上記の例は、2 つの接続が順番に発生するので、比較的簡単です。

* まず、サーバーがHTMLコードを返す
* 次に、ブラウザーが画像をリクエストし、新しい接続を開きます。

実際には、ページは、画像、スタイルシート、JavaScript ファイルなどに対して、多数の並列リクエストを生成する場合があります。 つまり、ログには、並列オープン接続の重複するエントリが存在します。 この場合、Adobeでは、読みやすさを向上させるために —i オプションを使用することをお勧めします。
