---
title: Adobe Experience Managerのサービスユーザー
description: Adobe Experience Managerのサービスユーザーについて説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
source-git-commit: f317783f3320e3987c7468aa0b2471e525b0387a
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 35%

---


# Adobe Experience Manager(AEM) のサービスユーザー {#service-users-in-aem}

## 概要 {#overview}

これまで、AEM で管理セッションやリソースリゾルバーを取得する主な方法は、Sling に用意されている `SlingRepository.loginAdministrative()` および `ResourceResolverFactory.getAdministrativeResourceResolver()` メソッドを使用することでした。

ただし、これらのメソッドはいずれも[最小権限の原則](https://ja.wikipedia.org/wiki/%E6%9C%80%E5%B0%8F%E6%A8%A9%E9%99%90%E3%81%AE%E5%8E%9F%E5%89%87)に基づいて設計されておらず、開発者がコンテンツの構造や対応するアクセス制御レベル（ACL）を早期に適切に計画しないことがよくあります。そのため、このようなサービスに脆弱性があると、コード自体を動作させるのに管理者権限が不要であっても、`admin` ユーザーへの権限のエスカレーションが発生することがよくあります。

## 管理セッションを段階的に廃止する方法 {#how-to-phase-out-admin-sessions}

### 優先度 0：機能はアクティブ/必要/中断されていますか。 {#priority-is-the-feature-active-needed-derelict}

管理セッションが使用されていなかったり、機能が完全に無効化されている場合があります。現在の実装環境がこれに当てはまる場合は、機能を削除するか、[NOP コード](https://ja.wikipedia.org/wiki/NOP)を埋め込んでください。

### 優先度 1：リクエストセッションを使用する {#priority-use-the-request-session}

可能な限り機能をリファクタリングし、指定された認証済みのリクエストセッションを使用して、コンテンツの読み取りや書き込みをおこなうことができるようにします。 これができない場合は、多くの場合、次の優先度に従って適用することで達成できます。

### 優先度 2：コンテンツの再構築 {#priority-restructure-content}

問題の多くは、コンテンツの再構築によって解決できます。 再構築を行う際は、次のシンプルなルールに留意してください。

* **アクセス制御の変更**

   * 実際にアクセスを必要とするユーザーまたはグループが実際にアクセス権を持っていることを確認します。

* **コンテンツ構造を調整**

   * アクセス制御が使用可能なリクエストセッションと一致する場所など、他の場所に移動します。
   * コンテンツの精度を変更する。

* **コードのリファクタリングを行って適切なサービスになるようにする**

   * ビジネスロジックを JSP コードからサービスに移動します。 これにより、異なるコンテンツモデリングが可能になります。

また、開発する新機能が、次の原則に従っていることを確認します。

* **コンテンツ構造はセキュリティ要件に基づいて進める必要があります**

   * アクセス制御の管理は自然に行われる
   * アクセス制御は、アプリケーションではなく、リポジトリによって適用される必要があります

* **ノードタイプを使用する**

   * 設定可能なプロパティのセットを制限する

* **プライバシー設定に配慮する**

   * プライベートプロファイルがある場合、例えば、プライベートで見つかったプロファイルの画像、E メールまたは姓名を公開しないようにします `/profile` ノード。

## 厳格なアクセス制御 {#strict-access-control}

コンテンツの再構築時にアクセス制御を適用したり、新しいサービスユーザーに対してアクセス制御を適用する場合には、可能な限り厳格な ACL を適用する必要があります。考えられるすべてのアクセス制御機能を使用してください。

* 例えば、`jcr:read` を `/apps` に適用するのではなく、`/apps/*/components/*/analytics` にのみ適用します。

* [制限](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)を使用します。

* ノードタイプに対する ACL の適用
* 権限の制限

   * 例えば、プロパティの書き込みのみが必要な場合は、`jcr:write` 権限を付与するのではなく、代わりに `jcr:modifyProperties` を使用してください。

## サービスユーザーとマッピング {#service-users-and-mappings}

上記の処理が失敗した場合、Sling 7 では、Service User Mapping サービスが提供されます。このサービスでは、バンドルとユーザーのマッピングおよび次の 2 つの対応する API メソッドを設定できます。

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

メソッドは、設定されたユーザーの権限のみを持つセッション/リソースリゾルバーを返します。 これらのメソッドの特徴は次のとおりです。

* サービスをユーザーにマッピングできます。
* サブサービスユーザーの定義が可能になります。
* 中央設定ポイントは `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl` です。
* `service-id` = `service-name` [&quot;:&quot; subservice-name]

* `service-id` は、認証用にリソースリゾルバーまたは JCR リポジトリユーザー ID（あるいはその両方）にマッピングされます。
* `service-name` は、サービスを提供するバンドルの記号名です。

## その他のRecommendations {#other-recommendations}

### admin-session のサービスユーザーへの置き換え {#replacing-the-admin-session-with-a-service-user}

サービスユーザーは、パスワードが設定されていない JCR ユーザーで、特定のタスクの実行に必要な最小限の権限が設定されています。 パスワードが設定されていない場合、サービスユーザーとのログインは不可能になります。

管理セッションを廃止する方法の 1 つは、管理セッションをサービスユーザーセッションに置き換えることです。 必要に応じて、複数のサブサービスユーザーに置き換えることもできます。

admin セッションをサービスユーザーに置き換えるには、次の手順を実行する必要があります。

1. 最小権限の原則を念頭に置いて、サービスに必要な権限を特定します。
1. 必要な権限設定で既にユーザーが使用できるかどうかを確認します。 必要に応じた既存のユーザーがない場合は、システムサービスユーザーを作成します。 サービスユーザーを作成するには、RTC が必要です。 複数のサブサービスユーザー（例えば、書き込み用と読み取り用に 1 つ）を作成して、アクセスをさらに区分化すると効果的な場合があります。
1. ユーザーの ACE を設定し、テストします。
1. サービスおよび `user/sub-users` に `service-user` マッピングを追加します。

1. サービスユーザーの sling 機能をバンドルから使用できるようにします。つまり、`org.apache.sling.api` を最新バージョンに更新します。

1. コード内の `admin-session` を `loginService` API または `getServiceResourceResolver` API に置き換えます。

## サービスユーザーの作成 {#creating-a-new-service-user}

AEMサービスユーザーのリストに含まれるユーザーがユースケースに適用されないこと、および対応する RTC の問題が承認されたことを確認したら、先に進み、新しいユーザーをデフォルトコンテンツに追加できます。

推奨されるアプローチは、リポジトリエクスプローラー（*https://&lt;server>:&lt;port>/crx/explorer/index.jsp*）を使用するサービスユーザーを作成することです。

目標は、有効な `jcr:uuid` プロパティ（コンテンツパッケージのインストールを使用してユーザーを作成する必要があります）

サービスユーザーは次の方法で作成できます。

1. *https://&lt;server>:&lt;port>/crx/explorer/index.jsp* のリポジトリエクスプローラーにアクセスします。
1. 管理者としてログインするには、 **ログイン** リンクをクリックします。
1. 次に、システムユーザーを作成し、名前を付けます。 ユーザーをシステムユーザーとして作成するには、中間パスをに設定します。 `system` 必要に応じて、オプションのサブフォルダーを追加します。

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. システムユーザーノードが次のようになっていることを確認します。

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >サービスユーザーに関連付けられた mixin タイプはありません。 これは、システムユーザーに対するアクセス制御ポリシーが存在しないことを意味します。

対応する .content.xml をバンドルのコンテンツに追加する際には、`rep:authorizableId` を設定し、プライマリタイプを `rep:SystemUser` にしてください。次のようになります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## ServiceUserMapper 構成に構成の修正を追加しています {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

サービスから対応するシステムユーザーにマッピングを追加するには、 [`ServiceUserMapper`](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html) サービス。 このモジュラーを維持するために、 [Sling 修正メカニズム](https://issues.apache.org/jira/browse/SLING-3578). このような設定をバンドルにインストールする場合は、次を使用することをお勧めします。 [Sling の初期コンテンツの読み込み](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. バンドルの src/main/resources フォルダーの下にサブフォルダー SLING-INF/content を作成します。
1. このフォルダーに、org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended — という名前のファイルを作成します。&lt;some unique=&quot;&quot; name=&quot;&quot; for=&quot;&quot; your=&quot;&quot; factory=&quot;&quot; configuration=&quot;&quot;>.xml を作成し、ファクトリ設定の内容（すべてのサブサービスユーザーマッピングを含む）を保存します。 例：

1. バンドルの `src/main/resources` フォルダーの下に `SLING-INF/content` フォルダーを作成します。
1. このフォルダーにファイルを作成します `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` をファクトリ設定のコンテンツ（すべてのサブサービスユーザーマッピングを含む）に置き換えます。

   説明のために、という名前のファイルを使用します。 `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. バンドルの `pom.xml` 内の `maven-bundle-plugin` 設定で Sling の初期コンテンツを参照します。例：

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. バンドルをインストールし、ファクトリ設定がインストールされていることを確認します。 手順は次のとおりです。

   * Web コンソール（*https://serverhost:serveraddress/system/console/configMgr*）にアクセスします。
   * **Apache Sling Service User Mapper Service Amendment** を探します。
   * リンクをクリックして、設定が適切に行われていることを確認します。

## サービスでの共有セッションの処理 {#dealing-with-shared-sessions-in-services}

`loginAdministrative()` を呼び出すと、多くの場合、共有セッションも表示されます。これらのセッションはサービスのアクティベート時に取得され、サービスが停止された場合にのみログアウトされます。これは一般的な動作ですが、次の 2 つの問題を伴います。

* **セキュリティ：** このような管理セッションは、共有セッションにバインドされているリソースや他のオブジェクトをキャッシュして返すために使用されます。 呼び出しスタックの後半で、これらのオブジェクトは、高い特権を持つセッションやリソースリゾルバーに適応することができ、多くの場合、呼び出し元が操作している管理者セッションであることが明確ではありません。
* **パフォーマンス：** Oak では、共有セッションはパフォーマンスの問題を引き起こす可能性があるので、それらを使用することはお勧めしません。

このセキュリティリスクに対する最も明白な解決策は、`loginAdministrative()` の呼び出しを `loginService()` に置き換え、権限が制限されたユーザーを対象とすることです。ただし、これは、潜在的なパフォーマンス低下には影響しません。 この問題を軽減するには、セッションと関連付けられていないオブジェクト内で要求されたすべての情報をラップします。 次に、オンデマンドでセッションを作成（または破棄）します。

推奨されるアプローチは、呼び出し元がセッションの作成/破壊を制御できるように、サービスの API をリファクタリングすることです。

## JSP での管理セッション {#administrative-sessions-in-jsps}

JSP では、関連するサービスがないので `loginService()` を使用できません。ただし、JSP の管理セッションは、通常、MVC パラダイムの違反の兆候を示しています。

これは、次の 2 つの方法で修正できます。

1. ユーザーセッションで操作できるようにコンテンツを再構築する。
1. JSP で使用できる API を提供するサービスにロジックを抽出します。

推奨される方法は前者です。

## イベント、レプリケーションプリプロセッサー、ジョブの処理 {#processing-events-replication-preprocessors-and-jobs}

イベントまたはジョブ（場合によってはワークフロー）を処理する際に、イベントをトリガーした対応するセッションが失われます。 これにより、多くの場合、管理セッションを使用して作業を行うイベントハンドラーやジョブプロセッサが発生します。 この問題を解決する方法は、それぞれ長所と短所があり、考えられる方法が異なります。

1. `user-id` をイベントペイロードに渡し、代理実行を使用します。

    **メリット：**&#x200B;容易に使用できます。

   **デメリット：** `loginAdministrative()` を使用する必要があります。既に認証済みのリクエストを再認証します。

1. データにアクセスできるサービスユーザーを作成または再利用します。

   **メリット：**&#x200B;現在の設計と一貫しています。変更が最小限で済みます。

   **デメリット：** 強力なサービスユーザーが柔軟である必要があり、権限のエスカレーションを容易に引き起こすことができます。 セキュリティモデルに抜け道ができます。

1. `Subject` のシリアル化をイベントペイロードに渡し、そのサブジェクトに基づいて `ResourceResolver` を作成します。例えば、`ResourceResolverFactory` で JAAS `doAsPrivileged` を使用します。

   **メリット：**&#x200B;セキュリティの観点からクリーンな実装が行えます。再認証を避け、元の権限で動作します。 セキュリティ関連のコードは、イベントの消費者に対して透過的です。

   **デメリット：**&#x200B;リファクタリングが必要です。セキュリティ関連のコードがイベントの消費者に対して透過的であるという事実も、問題を引き起こす可能性があります。

第 3 のアプローチは、推奨される処理技術です。

## ワークフロープロセス {#workflow-processes}

ワークフロープロセスの実装内で、ワークフローをトリガーした対応するユーザーセッションは失われます。 これにより、頻繁に管理セッションを使用して作業を実行するワークフロープロセスが発生します。

これらの問題を修正するには、 [イベント、レプリケーションプリプロセッサー、ジョブの処理](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) を使用します。

## SlingPOSTプロセッサーと削除済みページ {#sling-post-processors-and-deleted-pages}

SlingPOST・プロセッサの実装で使用される管理セッションが 2 つあります。 通常、管理セッションは、処理中のPOST内で削除を保留しているノードにアクセスするために使用されます。 その結果、これらはリクエストセッションからは使用できなくなります。 削除待ちのノードにアクセスして、アクセス不可のメタデータを開示することができます。
