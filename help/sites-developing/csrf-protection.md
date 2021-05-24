---
title: CSRF 対策フレームワーク
seo-title: CSRF 対策フレームワーク
description: このフレームワークでは、トークンを利用して、クライアントの要求が正当なものであることを保証します
seo-description: このフレームワークでは、トークンを利用して、クライアントの要求が正当なものであることを保証します
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 63%

---

# CSRF 対策フレームワーク{#the-csrf-protection-framework}

アドビでは、Apache Sling Referrer Filter 以外にも、この種の攻撃を防ぐための新しい CSRF 対策フレームワークを用意しています。

このフレームワークでは、トークンを利用して、クライアントの要求が正当なものであることを保証します。トークンは、フォームがクライアントに送信されるときに生成され、フォームがサーバーに返されるときに検証されます。

>[!NOTE]
>
>パブリッシュインスタンスでは、匿名ユーザーのトークンはありません。

## 要件 {#requirements}

### 依存関係 {#dependencies}

`granite.jquery`依存関係に依存するコンポーネントは、CSRF保護フレームワークのメリットを自動的に受けます。 どのコンポーネントでも該当しない場合は、フレームワークを使用する前に`granite.csrf.standalone`に依存関係を宣言する必要があります。

### 暗号鍵のレプリケーション {#replicating-crypto-keys}

トークンを利用するには、デプロイメント内のすべてのインスタンスに`/etc/keys/hmac`バイナリをレプリケートする必要があります。 HMAC 鍵をすべてのインスタンスにコピーするには、鍵を格納するパッケージを作成し、パッケージマネージャーを使用してすべてのインスタンスにインストールする方法が便利です。

>[!NOTE]
>
>CSRF 対策フレームワークを使用するには、必要な[ディスパッチャー設定の変更](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)をおこなってください。

>[!NOTE]
>
>Webアプリケーションでマニフェストキャッシュを使用する場合、トークンがCSRFトークン生成呼び出しをオフラインで受け取らないようにするために、「**&amp;ast;**」をマニフェストに追加します。 詳しくは、こちらの[リンク](https://www.w3.org/TR/offline-webapps/)を参照してください。
>
>CSRF 攻撃とその軽減方法について詳しくは、[OWASP のクロスサイトリクエストフォージェリに関するページ](https://owasp.org/www-community/attacks/csrf)を参照してください。
