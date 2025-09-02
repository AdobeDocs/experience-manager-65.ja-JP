---
title: ユニバーサルエディター
description: ユニバーサルエディターの柔軟性と、AEM 6.5 を使用してヘッドレスエクスペリエンスを強化する方法について説明します。
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: 9f91063e51aa599ef48967f832aa359ecf100fc2
workflow-type: ht
source-wordcount: '1183'
ht-degree: 100%

---


# ユニバーサルエディター {#universal-editor}

ユニバーサルエディターの柔軟性と、AEM 6.5 を使用してヘッドレスエクスペリエンスを強化する方法について説明します。

## 概要 {#overview}

ユニバーサルエディターは、Adobe Experience Manager Sites の一部である多用途のビジュアルエディターです。これにより、作成者は任意のヘッドレスエクスペリエンスで What You See Is What You Get（WYSIWYG）編集を利用できるようになります。

* ユニバーサルエディターはあらゆる形式の AEM ヘッドレスコンテンツに対して同じ一貫したビジュアル編集をサポートしているので、作成者はその柔軟性の恩恵を受けることができます。
* ユニバーサルエディターは実装の真の分離もサポートしているので、開発者はユニバーサルエディターの汎用性の恩恵を受けることができます。これにより、開発者は SDK やテクノロジの制約を受けずに、事実上任意のフレームワークやアーキテクチャを利用できるようになります。

詳しくは、[ユニバーサルエディターの AEM as a Cloud Service ドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)を参照してください。

## アーキテクチャ {#architecture}

ユニバーサルエディターは、AEM と連携してヘッドレスでコンテンツを作成するサービスです。

* ユニバーサルエディターは、`https://experience.adobe.com/#/aem/editor/canvas` でホストされ、AEM 6.5 でレンダリングされたページを編集できます。
* AEM ページは、AEM オーサーインスタンスから Dispatcher を通じてユニバーサルエディターで読み取られます。
* Dispatcher と同じホストで実行されるニバーサルエディターサービスは、変更を AEM オーサーインスタンスに書き戻します。

![ユニバーサルエディターを使用したオーサーフロー](assets/author-flow.png)

## 要件 {#requirements}

ユニバーサルエディターは、以下でサポートされています。

* AEM 6.5
   * オンプレミスと AMS ホスティングの両方がサポートされています。
* [AEM 6.5 LTS](https://experienceleague.adobe.com/ja/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * オンプレミスと AMS ホスティングの両方がサポートされています。
* [AEM as a Cloud Service](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)

このドキュメントでは、ユニバーサルエディターの AEM 6.5 のサポートに焦点を当てています。AEM 6.5 でユニバーサルエディターを使用するには、次が必要です。

* AEM 6.5 サービスパック 23 以降
   * サービスパック 21 および 22 は、[機能パック](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip)でもサポートされます。
* Dispatcher が適切に設定されている

## 設定 {#setup}

ユニバーサルエディターをテストするには、次の操作が必要です。

1. [ローカルのユニバーサルエディターサービスを設定します。](#set-up-ue)
1. [ユニバーサルエディターサービスを許可するために Dispatcher を調整します。](#update-dispatcher)

設定が完了したら、[アプリケーションを実装してユニバーサルエディターを使用](#instrumentation)できます。

### サービスの設定 {#configure-services}

ユニバーサルエディターでは、追加の設定が必要ないくつかのパッケージを活用します。

#### `login-token` cookie の SameSite 属性を設定します。 {#samesite-attribute}

1. Configuration Manager を開きます。
   * `http://<host>:<port>/system/console/configMgr`
1. リストで **Adobe Granite Token Authentication Handler** を見つけて、「**設定値を変更**」をクリックします。
1. ダイアログで、**login-token cookie の SameSite 属性**（`token.samesite.cookie.attr`）の値を `Partitioned` に変更します。
1. 「**保存**」をクリックします。

#### `SAMEORIGIN` ヘッダーの X-Frame オプションを削除します。 {#sameorigin}

1. Configuration Manager を開きます。
   * `http://<host>:<port>/system/console/configMgr`
1. リストで **Apache Sling Main Servlet** を見つけて、「**設定値を編集**」をクリックします。
1. **追加の応答ヘッダー**&#x200B;属性（`sling.additional.response.headers`）から `X-Frame-Options=SAMEORIGIN` 値が存在する場合は削除します。
1. 「**保存**」をクリックします。

#### Adobe Granite Query Parameter Authentication Handler を設定します。 {#query-parameter}

1. Configuration Manager を開きます。
   * `http://<host>:<port>/system/console/configMgr`
1. リストで **Adobe Granite Query Parameter Authentication Handler** を見つけて、「**設定値を編集**」をクリックします。
1. 「**パス**」フィールド（`path`）に、`/` を追加して有効にします。
   * 値が空の場合は、認証ハンドラーが無効になります。
1. 「**保存**」をクリックします。

#### ユニバーサルエディターを開くコンテンツパスまたは `sling:resourceTypes` を定義します。 {#paths}

1. Configuration Manager を開きます。
   * `http://<host>:<port>/system/console/configMgr`
1. リストで&#x200B;**ユニバーサルエディター URL サービス**&#x200B;を見つけて、「**設定値を編集**」をクリックします。
1. ユニバーサルエディターを開くコンテンツパスまたは `sling:resourceTypes` を定義します。 
   * 「**ユニバーサルエディターを開くマッピング**」フィールドに、ユニバーサルエディターを開くパスを指定します。
   * 「**ユニバーサルエディターで開く Sling:resourceTypes**」フィールドに、ユニバーサルエディターによって直接開かれるリソースのリストを指定します。
1. 「**保存**」をクリックします。
1. [Externalizer の設定](/help/sites-developing/externalizer.md)を確認し、少なくともローカル、オーサー、パブリッシュ環境が次の例のように設定されていることを確認します。

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

これらの設定手順が完了すると、AEM は次の順序でページのユニバーサルエディターを開きます。

1. AEM は `Universal Editor Opening Mapping` の下にあるマッピングを確認し、コンテンツがそこに定義されているパスの下にある場合は、ユニバーサルエディターが開かれます。
1. `Universal Editor Opening Mapping` で定義されたパスの下にないコンテンツの場合、AEM はコンテンツの `resourceType` が、**ユニバーサルエディターで開かれる Sling:resourceTypes** で定義されたものと一致するかどうかを確認し、コンテンツがこれらのタイプのいずれかに一致する場合は、`${author}${path}.html` でユニバーサルエディターが開かれます。
1. それ以外の場合は、AEM によってページエディターが開かれます。

次の変数は、`Universal Editor Opening Mapping` でマッピングを定義するために使用できます。

* `path`：開くリソースのコンテンツパス
* `localhost`：スキーマなしの `localhost` の Externalizer エントリ（例：`localhost:4502`）
* `author`：スキーマなしのオーサーの Externalizer エントリ（例：`localhost:4502`）
* `publish`：スキーマなしのパブリッシュの Externalizer エントリ（例：`localhost:4503`）
* `preview`：スキーマなしのプレビューの Externalizer エントリ（例：`localhost:4504`）
* `env`：定義された Sling 実行モードに基づく `prod`、`stage`、`dev`
* `token`：`QueryTokenAuthenticationHandler` に必要なクエリトークン

マッピングの例：

* AEM オーサーの `/content/foo` の下にあるすべてのページを開きます。
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * これにより、`https://localhost:4502/content/foo/x.html?login-token=<token>` が開きます。
* リモート NextJS サーバー上の `/content/bar` の下にあるすべてのページを開き、すべての変数を情報として指定します
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * これにより、`https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>` が開きます。

### ユニバーサルエディターサービスの設定 {#set-up-ue}

AEM を更新および設定すると、独自のローカル開発およびテスト用にローカルのユニバーサルエディターサービスを設定できます。

1. Node.js バージョン 20 以降をインストールします。
1. [ソフトウェア配布](https://experienceleague.adobe.com/ja/docs/experience-cloud/software-distribution/home)から最新のユニバーサルエディターサービスをダウンロードして展開します
1. 環境変数または `.env` ファイルを通じてユニバーサルエディターサービスを設定します。
   * [詳しくは、AEM as a Cloud Service ユニバーサルエディターのドキュメントを参照してください。](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * 内部 IP の書き換えが必要な場合は、`UES_MAPPING` オプションを使用する必要があります。
1. `universal-editor-service.cjs` を実行します

### Dispatcher の更新 {#update-dispatcher}

AEM が設定され、ローカルのユニバーサルエディターサービスが実行されている場合は、[Dispatcher で](https://experienceleague.adobe.com/ja/docs/experience-manager-dispatcher/using/dispatcher)新しいサービスのリバースプロキシを許可する必要があります。

1. オーサーインスタンスの vhost ファイルを調整して、リバースプロキシを含めます。

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080 がデフォルトのポートです。[`.env` ファイル](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)の `UES_PORT` パラメーターを使用して変更した場合は、ここでポート値をそれに応じて調整する必要があります。

1. Apache を再起動します。

## アプリの実装 {#instrumentation}

AEM が更新され、ローカルのユニバーサルエディターサービスが実行されている場合は、ユニバーサルエディターを使用してヘッドレスコンテンツの編集を開始できます。

ただし、ユニバーサルエディターを利用するには、アプリを実装する必要があります。これには、エディターにコンテンツを保持する方法と場所を指示するメタタグを含める必要があります。この実装について詳しくは、[AEM as a Cloud Service のユニバーサルエディターのドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)を参照してください。

AEM as a Cloud Service のユニバーサルエディターに関するドキュメントに従う場合、AEM 6.5 で使用する際に次の変更が適用されます。

* メタタグのプロトコルは、`aem` の代わりに `aem65` にする必要があります。

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* ユニバーサルエディターサービスのエンドポイントは、メタタグを通じて通知する必要があります。

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* コンポーネント定義の `plugins` セクションでは、`aem` の代わりに `aem65` を使用する必要があります。

>[!TIP]
>
>ユニバーサルエディターの基本を学ぶ開発者向けの包括的なガイドについて詳しくは、この節で説明されている AEM 6.5 のサポートに必要な変更に留意しながら、AEM as a Cloud Service ドキュメントの[AEM 開発者向けユニバーサルエディターの概要](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview)を参照してください。

## AEM 6.5 と AEM as a Cloud Service の違い {#differences}

AEM 6.5 のユニバーサルエディターは、UI や多くの設定を含め、AEM as a Cloud Service と広く同じように動作します。ただし、注意する必要がある違いもいくつかあります。

* 6.5 のユニバーサルエディターは、ヘッドレスユースケースのみをサポートします。
* ユニバーサルエディターの設定は、6.5 ではわずかに異なります（現在のドキュメントで[説明しているように](#setup)）。
* 6.5 のユニバーサルエディターでは、AEM as a Cloud Service とは異なるアセットピッカーとコンテンツフラグメントピッカーが使用されます。
