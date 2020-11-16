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
translation-type: tm+mt
source-git-commit: c83c77c5c313099944dd73c8cbe63d429d84a518
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

依存関係に依存するコンポーネントはすべて、CSRF保護フレームワークのメリットを自動的に受けます。 `granite.jquery` どのコンポーネントでもこのような状況にならない場合は、フレームワークを使用する前に、に依存関係を宣言する必要 `granite.csrf.standalone` があります。

### 暗号鍵のレプリケーション {#replicating-crypto-keys}

In order to make use of the tokens, you need to replicate the `/etc/keys/hmac` binary to all of the instances in your deployment. HMAC 鍵をすべてのインスタンスにコピーするには、鍵を格納するパッケージを作成し、パッケージマネージャーを使用してすべてのインスタンスにインストールする方法が便利です。

>[!NOTE]
>
>CSRF 対策フレームワークを使用するには、必要な[ディスパッチャー設定の変更](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)をおこなってください。

>[!NOTE]
>
>If you use the manifest cache with your web application, make sure you add &quot;**&amp;ast;**&quot; to the manifest in order to make sure the token does not take the CSRF token generation call offline. 詳しくは、こちらの[リンク](https://www.w3.org/TR/offline-webapps/)を参照してください。
>
>CSRF 攻撃とその軽減方法について詳しくは、[OWASP のクロスサイトリクエストフォージェリに関するページ](https://owasp.org/www-community/attacks/csrf)を参照してください。
