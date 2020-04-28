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
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# サーバー側のカスタマイズ {#server-side-customization}

| **[⇐ 機能の基本事項](essentials.md)** | **[クライアント側のカスタマイズ ⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars ヘルパー ⇒](handlebars-helpers.md)** |

## Java API {#java-apis}

>[!NOTE]
>
>Communities API のパッケージの場所は、次のメジャーリリースにアップグレードされる際に変更されることがあります。


### SocialComponent インターフェイス {#socialcomponent-interface}

SocialComponent は、AEM Communities 機能のリソースを表す POJO です。各SocialComponentは、特定のresourceTypeを、公開されたGETterを使用して表し、クライアントにデータを提供して、リソースを正確に表現するのが理想的です。 必要に応じて、すべてのビジネスロジックと表示ロジックが、サイト訪問者のセッション情報を含むSocialComponentにカプセル化されます。

このインターフェイスは、リソースを表すために必要な GETter の基本セットを定義します。重要なことは、インターフェイスは、Handlebars テンプレートをレンダリングしリソースの GET JSON エンドポイントを公開するために必要な、Map&lt;String, Object> getAsMap() および String toJSONString() メソッドを規定するということです。

All SocialComponent classes must implement the interface `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent インターフェイス {#socialcollectioncomponent-interface}

SocialCollectionComponent インターフェイスは、他のリソースのコレクションであるリソースをより適切に表すように SocialComponent インターフェイスを拡張します。

すべてのSocialCollectionComponentクラスは、com.adobe.cq.soscial.scf.SocialCollectionComponentインターフェイスを実装する必要があります

### SocialComponentFactory インターフェイス {#socialcomponentfactory-interface}

SocialComponentFactory（ファクトリ）は、SocialComponent をフレームワークに登録します。ファクトリは、複数のSocialComponentsが識別された場合に、特定のresourceTypeで使用できるSocialComponentsが何であるか、およびその優先順位がフレームワークに通知する手段を提供します。

SocialComponentFactory は、選択された SocialComponent のインスタンスを作成し、SocialComponent に必要なすべての依存関係をファクトリから DI パッケージを使用して挿入できるようにします。

SocialComponentFactory は OSGi サービスであり、コンストラクター経由で SocialComponent に渡すことができる他の OSGi サービスにアクセスできます。

すべての SocialComponentFactory クラスは、インターフェイス `com.adobe.cq.social.scf.SocialComponentFactory` を実装する必要があります。

SocialComponentFactory.getPriority()メソッドの実装は、getResourceType()が返す、指定されたresourceTypeにファクトリが使用されるように、最も高い値を返す必要があります。

### SocialComponentFactoryManager インターフェイス {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager（マネージャー）は、フレームワークに登録されたすべての SocialComponent を管理し、特定のリソース（resourceType）に対して使用される SocialComponentFactory を選択します。特定のresourceTypeにファクトリが登録されていない場合、マネージャは、指定されたリソースに最も近いスーパータイプを持つファクトリを返します。

SocialComponentFactoryManager は OSGi サービスであり、コンストラクター経由で SocialComponent に渡すことができる他の OSGi サービスにアクセスできます。

OSGi サービスへのハンドルは、`com.adobe.cq.social.scf.SocialComponentFactoryManager` を呼び出すことによって取得されます。

### HTTP API - POST 要求 {#http-api-post-requests}

#### PostOperation クラス {#postoperation-class}

HTTP API POST エンドポイントは、`SlingPostOperation` インターフェイス（パッケージ`org.apache.sling.servlets.post` ）を実装することによって定義される PostOperation クラスです。

`PostOperation` エンドポイント実装は、`sling.post.operation` を操作の応答先の値に設定します。その値に設定された :operation パラメーターを持つすべての POST 要求は、この実装クラスに委任されます。

`PostOperation` は、操作に必要なアクションを実行する `SocialOperation` を呼び出します。

`PostOperation` は、結果を `SocialOperation` から受け取り、適切な応答をクライアントに返します。

#### SocialOperation クラス {#socialoperation-class}

Each `SocialOperation` endpoint extends the AbstractSocialOperation class and overrides the method `performOperation()`. このメソッドは、操作の完了に必要なすべてのアクションを実行し、`SocialOperationResult` を返すか、または `OperationException` をスローします。後者の場合は、HTTP エラーステータスとメッセージ（使用可能な場合）が、通常の JSON 応答または成功 HTTP ステータスコードの代わりに返されます。

Extending `AbstractSocialOperation` makes possible the reuse of `SocialComponents` to send JSON responses.

#### SocialOperationResult クラス {#socialoperationresult-class}

`SocialOperationResult` クラスは、`SocialOperation` の結果として返され、`SocialComponent`、HTTP ステータスコードおよび HTTP ステータスメッセージで構成されます。

`SocialComponent` は、操作の影響を受けたリソースを表します。

作成操作の場合、`SocialComponent` に含まれる `SocialOperationResult` は作成されたリソースを表し、更新操作の場合、操作によって変更されたリソースを表します。削除操作の場合は `SocialComponent` は返されません。

使用される成功HTTPステータスコードは次のとおりです。

* 作成操作の場合は 201
* 更新操作の場合は 200
* 削除操作の場合は 204

#### OperationException クラス {#operationexception-class}

`OperationExcepton` は、操作の実行時に、要求が無効であるかその他のエラーが発生した場合に（内部エラー、不正なパラメーター値、不適切な権限など）スローされることがあります。`OperationException` は、HTTP ステータスコードおよびエラーメッセージで構成され、これらは `PostOperatoin` に対する応答としてクライアントに返されます。

#### OperationService クラス {#operationservice-class}

The social component framework recommends that the business logic responsible for performing the operation not be implemented within the `SocialOperation` class, but instead delegated to an OSGi service. ビジネスロジックの OSGi サービスを使用すると、`SocialComponent`（`SocialOperation` エンドポイントの影響を受ける）を他のコードと統合でき、異なるビジネスロジックを適用できます。

すべての `OperationService` クラスは `AbstractOperationService` を拡張し、実行される操作に関連付けることができる追加拡張を可能にします。サービス内の各操作は `SocialOperation` クラスによって表されます。`OperationExtensions` クラスは、操作の実行中に以下のメソッドを呼び出すことによって呼び出すことができます。

* `performBeforeActions()`

   事前確認/前処理と検証を許可
* `performAfterActions()`

   リソースをさらに変更したり、カスタムリソースやワークフローを呼び出したりできます。

#### OperationExtension クラス {#operationextension-class}

`OperationExtension` クラスは、操作に挿入できるコードのカスタム部分であり、ビジネスニーズに合うように操作をカスタマイズできます。コンポーネントのユーザーは、動的および増分的にコンポーネントに機能を追加できます。拡張／フックパターンにより、開発者は拡張自体に集中でき、操作およびコンポーネント全体をコピーして上書きする必要はなくなります。

## サンプルコード {#sample-code}

サンプルコードを [Adobe Marketing Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) リポジトリで入手できます。Search for projects prefixed with either `aem-communities` or `aem-scf`.

## ベストプラクティス {#best-practices}

AEM Communities 開発者向けの様々なコーディングガイドラインおよびベストプラクティスについては、[コーディングのガイドライン](code-guide.md)の節を参照してください。

See also [Storage Resource Provider (SRP) for UGC](srp.md) to learn about accessing user generated content.

| **[⇐ 機能の基本事項](essentials.md)** | **[クライアント側のカスタマイズ ⇒](client-customize.md)** |
|---|---|
|  | **[SCF Handlebars ヘルパー ⇒](handlebars-helpers.md)** |

