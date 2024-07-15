---
title: 静的オブジェクトの有効期限
description: 静的オブジェクトが（ある程度の期間）期限切れにならないように Adobe Experience Manager を設定する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 100%

---

# 静的オブジェクトの有効期限{#expiration-of-static-objects}

静的オブジェクト（アイコンなど）は変更されません。そのため、（ある程度の期間は）有効期限が切れないようにシステムを設定し、不要なトラフィックを減らす必要があります。

これにより、次のような影響があります。

* サーバーインフラストラクチャからリクエストがオフロードされます。
* ブラウザーでのオブジェクトのキャッシュ先がブラウザーキャッシュとなるので、ページ読み込みのパフォーマンスが向上します。

有効期限は、ファイルの「有効期限」に関する HTTP 規格によって指定されています（[RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) の第 14.21 章、「Hypertext Transfer Protocol -- HTTP 1.1」などを参照）。この規格では、ヘッダーを使用することにより、クライアントがオブジェクトを古くなるまでキャッシュできます。このようなオブジェクトは、元のサーバーに対してステータスチェックを行うことなく、特定の期間に渡ってキャッシュされます。

>[!NOTE]
>
>この設定は、Dispatcher とは別のものであり、Dispatcher に対しては機能しません。
>
>Dispatcher の目的は、Adobe Experience Manager（AEM）の手前でデータをキャッシュすることです。

動的ではなく、時間が経過しても変化しないファイルはすべてキャッシュ可能であり、またキャッシュする必要があります。Apache HTTPD サーバーの設定は、環境により、次のいずれかのようになります。

>[!CAUTION]
>
>オブジェクトが最新であるとみなされる期間を定義する際は、注意してください。*指定した期間が経過するまではステータスのチェックが行われない*&#x200B;ので、クライアントがキャッシュ内の古いコンテンツを提示する可能性があります。

1. **作成者インスタンスの場合：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   これにより、中間キャッシュ（ブラウザーキャッシュなど）で、CSS、JavaScript、PNG および GIF ファイルを、有効期限が切れるまで最大 1 か月間保存できます。つまり、AEM や web サーバーからリクエストする必要はなく、ブラウザーのキャッシュに残しておくことができます。

   サイトのその他のセクションは、いつでも変更される可能性があるので、オーサーインスタンスにはキャッシュしないでください。

1. **パブリッシュインスタンスの場合：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   これにより、中間キャッシュ（ブラウザーキャッシュなど）で、CSS、JavaScript、PNG および GIF ファイルを、最大 1 日間クライアントキャッシュに保存できます。この例では、`/content` および `/etc/designs` の下にあるすべてについてグローバル設定を示していますが、より詳細に設定する必要があります。

   サイトの更新頻度によっては、HTML ページのキャッシュも検討できます。妥当な期間は 1 時間です。

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

静的オブジェクトの設定が完了したら、該当するオブジェクトが保持されているページを選択した状態で `request.log` をスキャンして、静的オブジェクトに対する（不必要な）要求が行われていないことを確認します。
