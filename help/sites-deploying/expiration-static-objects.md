---
title: 静的オブジェクトの有効期限
seo-title: 静的オブジェクトの有効期限
description: 静的オブジェクトが（ある程度の期間）期限切れにならないように AEM を設定する方法を学習します。
seo-description: 静的オブジェクトが（ある程度の期間）期限切れにならないように AEM を設定する方法を学習します。
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 89%

---


# 静的オブジェクトの有効期限{#expiration-of-static-objects}

アイコンなどの静的オブジェクトは変化しません。したがって、不必要なトラフィックを減らすために、静的オブジェクトを（ある程度の期間は）期限切れにならないように設定する必要があります。

これにより、次のような影響があります。

* サーバーインフラストラクチャから要求がオフロードされます。
* ブラウザーでのオブジェクトのキャッシュ先がブラウザーキャッシュとなるので、ページ読み込みのパフォーマンスが向上します。

有効期限は、ファイルの「有効期限」に関する HTTP 規格によって指定されています（[RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) の第 14.21 章「Hypertext Transfer Protocol -- HTTP 1.1」などを参照）。この規格では、ヘッダーを使用することで、クライアントがオブジェクトを期限切れになるまでキャッシュできます。対象となるオブジェクトは、指定された期間中はずっとキャッシュ内に維持され、生成元サーバーに対するステータスチェックはおこなわれません。

>[!NOTE]
>
>この設定は、Dispatcher とは完全に別のものであり、Dispatcher に対しては機能しません。
>
>Dispatcher の目的は、AEM の手前でデータをキャッシュすることです。

動的ではなく、時間が経過しても変化しないファイルはすべてキャッシュ可能であり、またキャッシュする必要があります。Apache HTTPD サーバーの設定は、環境により、次のいずれかのようになります。

>[!CAUTION]
>
>オブジェクトの有効期間を定義する際は、注意が必要です。指定した期間が経過するまではステータスのチェックがおこなわれないので、クライアントがキャッシュ内の古いコンテンツを提示する可能性があります。**

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

   この設定により、中間キャッシュ（ブラウザーキャッシュなど）は、CSS、Javascript、PNG および GIF の各ファイルを期限切れになるまで最長で 1 ヶ月間格納できます。つまり、これらのファイルを AEM や Web サーバーに要求する必要はなく、ブラウザーキャッシュに残しておけるということです。

   サイトのその他のセクションは、いつでも変更される可能性があるので、オーサーインスタンスにはキャッシュしないでください。

1. **発行インスタンスの場合：**

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

   これにより、中間キャッシュ（ブラウザーのキャッシュなど）でCSS、Javascript、PNG、GIFファイルをクライアントキャッシュに1日まで格納できます。 この例では、`/content`および`/etc/designs`より下のすべてに対するグローバル設定を説明しますが、より詳細な設定を行う必要があります。

   サイトの更新頻度によっては、HTML ページのキャッシュも検討できます。妥当な期間は 1 時間です。

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

静的オブジェクトの設定が完了したら、該当するオブジェクトが保持されているページを選択した状態で `request.log` をスキャンして、静的オブジェクトに対する（不必要な）要求がおこなわれていないことを確認します。
