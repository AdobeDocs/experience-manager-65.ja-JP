---
title: サーバー側のカスタマイズ
description: Adobe Experience Manager Communitiesのサーバーサイドのカスタマイズの詳細。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 190735bc-1909-4b92-ba4f-a221c0cd5be7
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 1%

---

# サーバー側のカスタマイズ {#server-side-customization}

| **[⇐機能エッセンシャル](essentials.md)** | **[クライアントサイドのカスタマイズ ⇒](client-customize.md)** |
|---|---|
|   | **[SCF ハンドルバーのヘルパー⇒](handlebars-helpers.md)** |

## Java™ API {#java-apis}

>[!NOTE]
>
>Communities APIのパッケージの場所は、あるメジャーリリースから次のメジャーリリースにアップグレードする際に変更される可能性があります。

### SocialComponent インターフェイス {#socialcomponent-interface}

ソーシャルコンポーネントは、AEM Communities機能のリソースを表すPOJOです。 理想的には、各SocialComponentは特定のresourceTypeを表し、公開されたGETterはクライアントにデータを提供するため、リソースは正確に表されます。 必要に応じて、すべてのビジネスおよびビューロジックは、サイト訪問者のセッション情報を含むSocialComponentにカプセル化されます。

インターフェイスは、リソースを表すために必要なGETterの基本セットを定義します。 重要なのは、このインターフェイスが、Handlebars テンプレートをレンダリングし、GET JSON エンドポイントをリソースに公開するために必要なMap&lt;String, Object> getAsMap （）およびString toJSONString （） メソッドを規定していることです。

すべてのSocialComponent クラスは、インターフェイス `com.adobe.cq.social.scf.SocialComponent`を実装する必要があります

### SocialCollectionComponent インターフェイス {#socialcollectioncomponent-interface}

SocialCollectionComponent インターフェイスは、SocialComponent インターフェイスを拡張して、他のリソースのコレクションであるリソースをより適切に表現します。

すべてのSocialCollectionComponent クラスは、com.adobe.cq.social.scf.SocialCollectionComponent インターフェイスを実装する必要があります

### SocialComponentFactory インターフェイス {#socialcomponentfactory-interface}

SocialComponentFactory （ファクトリー）は、フレームワークにSocialComponentを登録します。 このファクトリーは、フレームワークに、特定のresourceTypeで利用できるSocialComponentsと、複数のSocialComponentsが識別されたときの優先度ランキングを知らせる手段を提供します。

SocialComponentFactoryは、選択したSocialComponentのインスタンスを作成し、DI プラクティスを使用してSocialComponentがファクトリから必要とするすべての依存関係を注入できるようにします。

SocialComponentFactoryはOSGi サービスであり、コンストラクターを介してSocialComponentに渡すことができる他のOSGi サービスにアクセスできます。

すべてのSocialComponentFactory クラスは、インターフェイス `com.adobe.cq.social.scf.SocialComponentFactory`を実装する必要があります

SocialComponentFactory.getPriority （） メソッドの実装は、getResourceType （）によって返される、特定のresourceTypeに使用されるファクトリの最大値を返す必要があります。

### SocialComponentFactoryManager インターフェイス {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager （マネージャー）は、フレームワークに登録されているすべてのSocialComponentsを管理し、特定のリソース（resourceType）に使用するSocialComponentFactoryを選択する責任があります。 特定のresourceTypeに対してファクトリが登録されていない場合、マネージャーは、特定のリソースに対して最も近いスーパータイプを持つファクトリを返します。

SocialComponentFactoryManagerはOSGi サービスであり、コンストラクターを介してSocialComponentに渡すことができる他のOSGi サービスにアクセスできます。

OSGi サービスへのハンドルは、`com.adobe.cq.social.scf.SocialComponentFactoryManager`を呼び出すことによって取得されます

### HTTP API - POST リクエスト {#http-api-post-requests}

#### PostOperation クラス {#postoperation-class}

HTTP API POST エンドポイントは、`SlingPostOperation` インターフェイス （パッケージ `org.apache.sling.servlets.post`）を実装して定義されたPostOperation クラスです。

`PostOperation` エンドポイント実装は、操作が応答する値に`sling.post.operation`を設定します。 :operation パラメーターがその値に設定されているすべてのPOST リクエストは、この実装クラスにデリゲートされます。

`PostOperation`は、操作に必要なアクションを実行する`SocialOperation`を呼び出します。

`PostOperation`は`SocialOperation`から結果を受け取り、適切な応答をクライアントに返します。

#### SocialOperation クラス {#socialoperation-class}

各`SocialOperation` エンドポイントは、AbstractSocialOperation クラスを拡張し、メソッド `performOperation()`を上書きします。 このメソッドは、操作を完了し、`SocialOperationResult`を返すか、`OperationException`をスローするために必要なすべてのアクションを実行します。 この場合、メッセージを含むHTTP エラーステータスが使用可能な場合は、通常のJSON レスポンスまたは成功HTTP ステータスコードの代わりに返されます。

`AbstractSocialOperation`を拡張すると、`SocialComponents`を再利用してJSON応答を送信できるようになります。

#### SocialOperationResult クラス {#socialoperationresult-class}

`SocialOperationResult` クラスは`SocialOperation`の結果として返され、`SocialComponent`、HTTP ステータスコード、およびHTTP ステータスメッセージで構成されます。

`SocialComponent`は、操作の影響を受けたリソースを表します。

作成操作の場合、`SocialOperationResult`に含まれる`SocialComponent`は作成されたリソースを表し、更新操作の場合は、操作によって変更されたリソースを表します。 削除操作に対して`SocialComponent`は返されません。

使用される成功HTTP ステータスコードは次のとおりです。

* 201 for Create operations
* 200：更新操作
* 204の削除操作

#### OperationException クラス {#operationexception-class}

リクエストが無効であるか、他のエラーが発生した場合、操作を実行すると`OperationExcepton`がスローされます。 例えば、内部エラー、不正なパラメーター値、不適切な権限などです。 `OperationException`は、HTTP ステータス コードとエラーメッセージで構成され、`PostOperatoin`への応答としてクライアントに返されます。

#### OperationService クラス {#operationservice-class}

ソーシャル コンポーネント フレームワークでは、操作を実行するビジネス ロジックを`SocialOperation` クラス内に実装せず、代わりにOSGi サービスにデリゲートすることをお勧めします。 ビジネスロジックにOSGi サービスを使用すると、`SocialOperation` エンドポイントによって動作する`SocialComponent`を他のコードと統合し、異なるビジネスロジックを適用できます。

すべての`OperationService` クラスは`AbstractOperationService`を拡張し、実行されている操作に接続できる追加の拡張機能を許可します。 サービス内の各操作は、`SocialOperation` クラスで表されます。 `OperationExtensions` クラスは、メソッドを呼び出すことで、操作実行中に呼び出すことができます

* `performBeforeActions()`

  事前チェック/前処理と検証が可能
* `performAfterActions()`

  リソースをさらに編集したり、カスタムイベントやワークフローなどを呼び出したりできます。

#### OperationExtension クラス {#operationextension-class}

`OperationExtension` クラスは、ビジネス ニーズに合わせて操作をカスタマイズできるように、操作に挿入できるカスタム コードです。 コンポーネントのコンシューマーは、コンポーネントに機能を動的かつ段階的に追加できます。 拡張機能/フックパターンを使用すると、開発者は拡張機能に専念でき、操作やコンポーネント全体をコピーして上書きする必要がなくなります。

## サンプルコード {#sample-code}

サンプルコードは、[Adobe Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) リポジトリで入手できます。 プロジェクトの先頭に`aem-communities`または`aem-scf`が付いたプロジェクトを検索します。

## ベストプラクティス {#best-practices}

AEM Communities開発者向けの様々なコーディングガイドラインとベストプラクティスについては、[ コーディングガイドライン ](code-guide.md)の節を参照してください。

ユーザー生成コンテンツへのアクセスについて詳しくは、[UGC](srp.md)のストレージリソースプロバイダー（SRP）も参照してください。

| **[⇐機能エッセンシャル](essentials.md)** | **[クライアントサイドのカスタマイズ ⇒](client-customize.md)** |
|---|---|
|   | **[SCF ハンドルバーのヘルパー⇒](handlebars-helpers.md)** |
