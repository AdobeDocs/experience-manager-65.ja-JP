---
title: サーバー側のカスタマイズ
description: Adobe Experience Manager Communities でサーバーサイドのカスタマイズを使用する方法を説明します。
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
source-wordcount: '889'
ht-degree: 1%

---

# サーバー側のカスタマイズ {#server-side-customization}

| **[⇐機能の基本事項](essentials.md)** | **[クライアントサイドのカスタマイズ ⇒](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars ヘルパー⇒](handlebars-helpers.md)** |

## Java™ API {#java-apis}

>[!NOTE]
>
>Communities API のパッケージの場所は、メジャーリリースから次のリリースにアップグレードする際に変更される可能性があります。

### SocialComponent インターフェイス {#socialcomponent-interface}

ソーシャルコンポーネントは、AEM Communities機能のリソースを表す POJO です。 理想的には、各 SocialComponent は、リソースが正確に表されるように、クライアントにデータを提供する公開された GETter を持つ特定の resourceType を表します。 必要に応じて、サイト訪問者のセッション情報を含む、すべてのビジネスおよび表示ロジックが SocialComponent にカプセル化されます。

インターフェイスは、リソースを表すために必要な GETter の基本的なセットを定義します。 重要なのは、インターフェイスがマップを規定していることです&lt;string object=&quot;&quot;> Handlebars テンプレートのレンダリングとリソースのGET JSON エンドポイントの公開に必要な getAsMap （） メソッドと String toJSONString （） メソッド。

すべての SocialComponent クラスは、インターフェイスを実装する必要があります `com.adobe.cq.social.scf.SocialComponent`

### SocialCollectionComponent インターフェイス {#socialcollectioncomponent-interface}

SocialCollectionComponent インターフェイスは、SocialComponent インターフェイスを拡張して、他のリソースのコレクションであるリソースをより適切に表現します。

すべての SocialCollectionComponent クラスは、インターフェイス com.adobe.cq.social.scf.SocialCollectionComponent を実装する必要があります

### SocialComponentFactory インターフェイス {#socialcomponentfactory-interface}

SocialComponentFactory （ファクトリ）は、SocialComponent をフレームワークに登録します。 ファクトリは、複数のソーシャルコンポーネントが識別された場合に、特定の resourceType に使用できるソーシャルコンポーネントとその優先度ランキングをフレームワークに知らせる手段を提供します。

SocialComponentFactory は、選択した SocialComponent のインスタンスを作成し、DI プラクティスを使用して SocialComponent で必要なすべての依存関係を工場から挿入できるようにする役割を担います。

SocialComponentFactory は OSGi サービスであり、コンストラクターを通じて SocialComponent に渡すことができる他の OSGi サービスへのアクセス権があります。

すべての SocialComponentFactory クラスは、インターフェイスを実装する必要があります `com.adobe.cq.social.scf.SocialComponentFactory`

SocialComponentFactory.getPriority （） メソッドの実装は、getResourceType （）によって返された特定の resourceType に使用されるファクトリの最大値を返す必要があります。

### SocialComponentFactoryManager インターフェイス {#socialcomponentfactorymanager-interface}

SocialComponentFactoryManager （マネージャー）は、フレームワークに登録されているすべてのソーシャルコンポーネントを管理し、特定のリソース（resourceType）に使用する SocialComponentFactory を選択する役割を担います。 特定の resourceType にファクトリが登録されていない場合、指定されたリソースに最も近いスーパータイプを持つファクトリが返されます。

SocialComponentFactoryManager は OSGi サービスであり、コンストラクターを通じて SocialComponent に渡すことができる他の OSGi サービスへのアクセス権があります。

OSGi サービスへのハンドルは、を呼び出すことによって取得されます `com.adobe.cq.social.scf.SocialComponentFactoryManager`

### HTTP API -POSTリクエスト {#http-api-post-requests}

#### PostOperation クラス {#postoperation-class}

HTTP APIPOSTエンドポイントは、を実装することで定義される PostOperation クラスです。 `SlingPostOperation` インターフェイス （パッケージ） `org.apache.sling.servlets.post`）に設定します。

この `PostOperation` エンドポイント実装セット `sling.post.operation` 操作が応答する値に設定します。 :operation パラメーターが値に設定されたすべてのPOSTリクエストは、この実装クラスにデリゲートされます。

この `PostOperation` を呼び出します `SocialOperation` 操作に必要なアクションを実行します。

この `PostOperation` から結果を受信します `SocialOperation` そして、適切な応答をクライアントに返します。

#### SocialOperation クラス {#socialoperation-class}

Each `SocialOperation` エンドポイントは、AbstractSocialOperation クラスを拡張し、メソッドをオーバーライドします `performOperation()`. このメソッドは、操作を完了し、 `SocialOperationResult` それ以外の場合は `OperationException`. この場合、メッセージを含む HTTP エラーステータスが使用可能であれば、通常の JSON 応答や成功 HTTP ステータスコードの代わりに返されます。

の拡張 `AbstractSocialOperation` ～の再利用を可能にする `SocialComponents` JSON 応答を送信します。

#### SocialOperationResult クラス {#socialoperationresult-class}

この `SocialOperationResult` クラスは、次の結果として返されます `SocialOperation` また、で構成されています。 `SocialComponent`、HTTP ステータスコードおよび HTTP ステータスメッセージ。

この `SocialComponent` 操作の影響を受けたリソースを表します。

作成操作の場合、 `SocialComponent` 次に含まれる `SocialOperationResult` は、作成されたリソースを表します。更新操作の場合は、操作によって変更されたリソースを表します。 不可 `SocialComponent` は、削除操作に対して返されます。

使用される成功 HTTP ステータスコードは次のとおりです。

* 作成操作用の 201
* 更新操作用の 200
* 削除操作用の 204

#### OperationException クラス {#operationexception-class}

An `OperationExcepton` リクエストが無効な場合や他のエラーが発生した場合、操作の実行時にスローされる。 例えば、内部エラー、パラメーター値が正しくない、権限が正しくないなど。 An `OperationException` は、HTTP ステータスコードとエラーメッセージで構成され、 `PostOperatoin`.

#### OperationService クラス {#operationservice-class}

ソーシャルコンポーネントフレームワークでは、操作の実行を担当するビジネスロジックを内に実装しないことをお勧めします `SocialOperation` クラス。代わりに OSGi サービスにデリゲートされます。 ビジネスロジックに OSGi サービスを使用すると、 `SocialComponent`。に基づいて `SocialOperation` エンドポイント：他のコードと統合し、異なるビジネスロジックを適用する。

すべて `OperationService` classes extend `AbstractOperationService`、実行されている操作に関連付けることができる追加の拡張機能を許可します。 サービス内の各操作は、 `SocialOperation` クラス。 この `OperationExtensions` クラスは、メソッドを呼び出すことによって、操作の実行中に呼び出すことができます

* `performBeforeActions()`

  チェック/前処理および検証が可能
* `performAfterActions()`

  リソースをさらに編集したり、カスタムイベントやワークフローなどを呼び出したりできます。

#### OperationExtension クラス {#operationextension-class}

この `OperationExtension` クラスは、操作に挿入できるカスタムコードの一部で、ビジネスニーズに合わせて操作をカスタマイズできます。 コンポーネントのコンシューマーは、コンポーネントに機能を動的かつ増分的に追加できます。 拡張機能/フックパターンを使用すると、開発者は拡張機能自体に専念でき、操作やコンポーネント全体をコピーして上書きする必要がなくなります。

## サンプルコード {#sample-code}

サンプルコードは次で入手できます [Adobe Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud) リポジトリ。 次のいずれかのプレフィックスが付いたプロジェクトを検索 `aem-communities` または `aem-scf`.

## ベストプラクティス {#best-practices}

を表示する [コーディングのガイドライン](code-guide.md) AEM Communities開発者向けの様々なコーディングガイドラインとベストプラクティスについての節です。

関連トピック [UGC 用ストレージリソースプロバイダー（SRP）](srp.md) ユーザー生成コンテンツへのアクセスについて説明します。

| **[⇐機能の基本事項](essentials.md)** | **[クライアントサイドのカスタマイズ ⇒](client-customize.md)** |
|---|---|
|   | **[SCF Handlebars ヘルパー⇒](handlebars-helpers.md)** |
