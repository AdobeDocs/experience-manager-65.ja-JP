---
title: CSRF 対策フレームワーク
seo-title: The CSRF Protection Framework
description: このフレームワークでは、トークンを使用して、クライアントの要求が正当なものであることを保証します
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 39%

---

# CSRF 対策フレームワーク {#the-csrf-protection-framework}

Apache Sling Referrer Filter に加えて、Adobeは、この種の攻撃から保護する新しい CSRF 保護フレームワークも提供します。

このフレームワークでは、トークンを使用して、クライアントの要求が正当なものであることを保証します。 トークンは、フォームがクライアントに送信されるときに生成され、フォームがサーバーに送り返されるときに検証されます。

>[!NOTE]
>
>匿名ユーザーのパブリッシュインスタンスにはトークンがありません。

## 要件 {#requirements}

### 依存関係 {#dependencies}

`granite.jquery` 依存関係を信頼する任意のコンポーネント は、CSRF 保護フレームワークのメリットを自動的に受けます。どのコンポーネントにも当てはまらない場合、このフレームワークを使用するには `granite.csrf.standalone` への依存関係を宣言する必要があります。

### 暗号鍵のレプリケーション {#replicating-crypto-keys}

トークンを利用するには、デプロイメント内のすべてのインスタンスに HMAC バイナリをレプリケートする必要があります。 詳しくは、[HMAC キーのレプリケーション](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key)を参照してください。

>[!NOTE]
>
>必ず必要な [Dispatcher 設定の変更](https://helpx.adobe.com/jp/experience-manager/brand-portal/user-guide.html) CSRF 保護フレームワークを使用する場合。

>[!NOTE]
>
>Web アプリケーションでマニフェストキャッシュを使用する場合は、必ず「**&amp;ast;**」をマニフェストに追加して、トークンが CSRF トークン生成呼び出しをオフラインで受け取らないようにします。 詳しくは、こちらの[リンク](https://www.w3.org/TR/offline-webapps/)を参照してください。
>
>CSRF 攻撃とその対策について詳しくは、[クロスサイトリクエストフォージェリに関する OWASP のページ](https://owasp.org/www-community/attacks/csrf)を参照してください。
