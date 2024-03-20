---
title: CSRF 対策フレームワーク
description: このフレームワークでは、トークンを利用して、クライアントのリクエストが正当なものであることを保証します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 100%

---

# CSRF 対策フレームワーク {#the-csrf-protection-framework}

アドビでは、Apache Sling リファラーフィルター以外にも、この種の攻撃を防ぐための新しい CSRF 対策フレームワークを用意しています。

このフレームワークでは、トークンを利用して、クライアントのリクエストが正当なものであることを保証します。トークンは、フォームがクライアントに送信されるときに生成され、フォームがサーバーに返されるときに検証されます。

>[!NOTE]
>
>パブリッシュインスタンスでは、匿名ユーザーのトークンはありません。

## 要件 {#requirements}

### 依存関係 {#dependencies}

`granite.jquery` の依存関係を使用するコンポーネントは、CSRF 対策フレームワークのメリットを自動的に活用できます。いずれかのコンポーネントがこのメリットを活用できない場合は、フレームワークを使用する前に `granite.csrf.standalone` に対して依存関係を宣言する必要があります。

### 暗号鍵のレプリケーション {#replicating-crypto-keys}

トークンを利用するには、デプロイメント内のすべてのインスタンスに HMAC バイナリをレプリケートする必要があります。詳しくは、[HMAC キーのレプリケーション](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key)を参照してください。

>[!NOTE]
>
>CSRF 対策フレームワークを使用するには、必要な[Dispatcher 設定の変更](https://helpx.adobe.com/jp/experience-manager/brand-portal/user-guide.html)を行ってください。

>[!NOTE]
>
>Web アプリケーションでマニフェストキャッシュを使用する場合、トークンがオフラインで CSRF トークンの生成を呼び出さないように、「**&amp;ast;**」をマニフェストに追加してください。詳しくは、こちらの[リンク](https://www.w3.org/TR/offline-webapps/)を参照してください。
>
CSRF 攻撃とその対策について詳しくは、[クロスサイトリクエストフォージェリに関する OWASP のページ](https://owasp.org/www-community/attacks/csrf)を参照してください。
