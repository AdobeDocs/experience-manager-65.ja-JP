---
title: サーバー側のカスタマイズ
seo-title: サーバー側のカスタマイズ
description: AEM Communities のサーバー側のカスタマイズ
seo-description: AEM Communities のサーバー側のカスタマイズ
uuid: 5e9bc6bf-69dc-414c-a4bd-74a104d7bd8f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: df5416ec-5c63-481b-99ed-9e5a91df2432
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 74%

---

# サーバー側のカスタマイズ  {#server-side-customization}

| **[⇐ 機能の基本事項](essentials.md)** | **[クライアント側のカスタマイズ ⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars ヘルパー ⇒](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>Communities API のパッケージの場所は、次のメジャーリリースにアップグレードされる際に変更されることがあります。

### SocialComponent インターフェイス  {#socialcomponent-interface}

SocialComponent は、AEM Communities 機能のリソースを表す POJO です。理想的には、各SocialComponentは、リソースが正確に表されるように、クライアントにデータを提供する、公開されたGETterを持つ特定のresourceTypeを表します。 必要に応じて、すべてのビジネスロジックとビューロジックはSocialComponentにカプセル化されます。サイト訪問者のセッション情報も含まれます。

このインターフェイスは、リソースを表すために必要な GETter の基本セットを定義します。重要なことは、インターフェイスは、Handlebars テンプレートをレンダリングしリソースの GET JSON エンドポイントを公開するために必要な、Map&lt;String, Object> getAsMap() および String toJSONString() メソッドを規定するということです。

すべてのSocialComponentクラスは、インターフェイス`com.adobe.cq.social.scf.SocialComponent`を実装する必要があります

### SocialCollectionComponent インターフェイス {#socialcollectioncomponent-interface}

SocialCollectionComponent インターフェイスは、他のリソースのコレクションであるリソースをより適切に表すように SocialComponent インターフェイスを拡張します。

すべてのSocialCollectionComponentクラスは、インターフェイスcom.adobe.cq.social.scf.SocialCollectionComponentを実装する必要があります

### SocialComponentFactory インターフェイス {#socialcomponentfactory-interface}

SocialComponentFactory（ファクトリ）は、SocialComponent をフレームワークに登録します。ファクトリは、特定のresourceTypeに対して使用可能なSocialComponentsと、複数のSocialComponentsが識別された場合の優先順位をフレームワークに知らせる手段を提供します。

SocialComponentFactory は、選択された SocialComponent のインスタンスを作成し、SocialComponent に必要なすべての依存関係をファクトリから DI パッケージを使用して挿入できるようにします。

SocialComponentFactory は OSGi サービスであり、コンストラクター経由で SocialComponent に渡すことができる他の OSGi サービスにアクセスできます。

すべての SocialComponentFactory クラスは、インターフェイス `com.adobe.cq.social.scf.SocialComponentFactory` を実装する必要があります。

SocialComponentFactory.getPriority()メソッドの実装では、getResourceType()が返す特定のresourceTypeに対してファクトリを使用するために、最も高い値を返す必要があります。

### SocialComponentFactoryManager インターフェイス {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（マネージャー）は、フレームワークに登録されたすべての SocialComponent を管理し、特定のリソース（resourceType）に対して使用される SocialComponentFactory を選択します。特定のresourceTypeにファクトリが登録されていない場合、マネージャは指定されたリソースに最も近いスーパータイプを持つファクトリを返します。

SocialComponentFactoryManager は OSGi サービスであり、コンストラクター経由で SocialComponent に渡すことができる他の OSGi サービスにアクセスできます。

OSGi サービスへのハンドルは、`com.adobe.cq.social.scf.SocialComponentFactoryManager` を呼び出すことによって取得されます。

### HTTP API - POST 要求 {#http-api-post-requests}

#### PostOperation クラス {#postoperation-class}

HTTP API POST エンドポイントは、`SlingPostOperation` インターフェイス（パッケージ`org.apache.sling.servlets.post` ）を実装することによって定義される PostOperation クラスです。

`PostOperation` エンドポイント実装は、`sling.post.operation` を操作の応答先の値に設定します。その値に設定された :operation パラメーターを持つすべての POST 要求は、この実装クラスに委任されます。

`PostOperation` は、操作に必要なアクションを実行する `SocialOperation` を呼び出します。

`PostOperation` は、結果を `SocialOperation` から受け取り、適切な応答をクライアントに返します。

#### SocialOperation クラス {#socialoperation-class}

各`SocialOperation`エンドポイントは、AbstractSocialOperationクラスを拡張し、メソッド`performOperation()`を上書きします。 このメソッドは、操作の完了に必要なすべてのアクションを実行し、`SocialOperationResult` を返すか、または `OperationException` をスローします。後者の場合は、HTTP エラーステータスとメッセージ（使用可能な場合）が、通常の JSON 応答または成功 HTTP ステータスコードの代わりに返されます。

`AbstractSocialOperation`を拡張すると、JSON応答を送信するための`SocialComponents`の再利用が可能になります。

#### SocialOperationResult クラス {#socialoperationresult-class}

`SocialOperationResult` クラスは、`SocialOperation` の結果として返され、`SocialComponent`、HTTP ステータスコードおよび HTTP ステータスメッセージで構成されます。

`SocialComponent` は、操作の影響を受けたリソースを表します。

作成操作の場合、`SocialComponent` に含まれる `SocialOperationResult` は作成されたリソースを表し、更新操作の場合、操作によって変更されたリソースを表します。削除操作の場合は `SocialComponent` は返されません。

使用される成功HTTPステータスコードは次のとおりです。

* 作成操作の場合は 201
* 更新操作の場合は 200
* 削除操作の場合は 204

#### OperationException クラス  {#operationexception-class}

`OperationExcepton` は、操作の実行時に、要求が無効であるかその他のエラーが発生した場合に（内部エラー、不正なパラメーター値、不適切な権限など）スローされることがあります。`OperationException` は、HTTP ステータスコードおよびエラーメッセージで構成され、これらは `PostOperatoin` に対する応答としてクライアントに返されます。

#### OperationService クラス {#operationservice-class}

ソーシャルコンポーネントフレームワークでは、操作を実行するビジネスロジックを`SocialOperation`クラス内に実装せず、代わりにOSGiサービスに委任することをお勧めします。 ビジネスロジックの OSGi サービスを使用すると、`SocialComponent`（`SocialOperation` エンドポイントの影響を受ける）を他のコードと統合でき、異なるビジネスロジックを適用できます。

すべての `OperationService` クラスは `AbstractOperationService` を拡張し、実行される操作に関連付けることができる追加拡張を可能にします。サービス内の各操作は `SocialOperation` クラスによって表されます。`OperationExtensions` クラスは、操作の実行中に以下のメソッドを呼び出すことによって呼び出すことができます。

* `performBeforeActions()`

   事前チェック/前処理および検証を可能にする
* `performAfterActions()`

   リソースをさらに変更したり、カスタムイベントやワークフローなどを呼び出したりできます。

#### OperationExtension クラス {#operationextension-class}

`OperationExtension` クラスは、操作に挿入できるコードのカスタム部分であり、ビジネスニーズに合うように操作をカスタマイズできます。コンポーネントのユーザーは、動的および増分的にコンポーネントに機能を追加できます。拡張／フックパターンにより、開発者は拡張自体に集中でき、操作およびコンポーネント全体をコピーして上書きする必要はなくなります。

## サンプルコード  {#sample-code}

サンプルコードを [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) リポジトリで入手できます。`aem-communities`または`aem-scf`のプレフィックスが付いたプロジェクトを検索します。

## ベストプラクティス {#best-practices}

AEM Communities 開発者向けの様々なコーディングガイドラインおよびベストプラクティスについては、[コーディングのガイドライン](code-guide.md)の節を参照してください。

ユーザー生成コンテンツへのアクセスについては、UGC](srp.md)の[ストレージリソースプロバイダー(SRP)も参照してください。

| **[⇐ 機能の基本事項](essentials.md)** | **[クライアント側のカスタマイズ ⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars ヘルパー ⇒](handlebars-helpers.md)** |
