---
title: CSRF 対策フレームワーク
seo-title: The CSRF Protection Framework
description: このフレームワークでは、トークンを利用して、クライアントの要求が正当なものであることを保証します
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '282'
ht-degree: 100%

---

# CSRF 対策フレームワーク{#the-csrf-protection-framework}

アドビでは、Apache Sling Referrer Filter 以外にも、この種の攻撃を防ぐための新しい CSRF 対策フレームワークを用意しています。

このフレームワークでは、トークンを利用して、クライアントの要求が正当なものであることを保証します。トークンは、フォームがクライアントに送信されるときに生成され、フォームがサーバーに返されるときに検証されます。

>[!NOTE]
>
>パブリッシュインスタンスでは、匿名ユーザーのトークンはありません。

## 要件 {#requirements}

### 依存関係 {#dependencies}

`granite.jquery` 依存関係を信頼する任意のコンポーネント は、CSRF 保護フレームワークのメリットを自動的に受けます。どのコンポーネントにも当てはまらない場合、このフレームワークを使用するには `granite.csrf.standalone` への依存関係を宣言する必要があります。

### 暗号鍵のレプリケーション {#replicating-crypto-keys}

トークンを利用するには、デプロイメント内のすべてのインスタンスに `/etc/keys/hmac` バイナリをレプリケーションする必要があります。HMAC 鍵をすべてのインスタンスにコピーするには、鍵を格納するパッケージを作成し、パッケージマネージャーを使用してすべてのインスタンスにインストールする方法が便利です。

>[!NOTE]
>
>CSRF 対策フレームワークを使用するには、必要な[ディスパッチャー設定の変更](https://helpx.adobe.com/jp/experience-manager/brand-portal/user-guide.html)を行ってください。

>[!NOTE]
>
>Web アプリケーションでマニフェストキャッシュを使用する場合、トークンがオフラインで CSRF トークンの生成を呼び出さないように、「**&amp;ast;**」をマニフェストに追加してください。詳しくは、こちらの[リンク](https://www.w3.org/TR/offline-webapps/)を参照してください。
>
>CSRF 攻撃とその対策について詳しくは、[クロスサイトリクエストフォージェリに関する OWASP のページ](https://owasp.org/www-community/attacks/csrf)を参照してください。
