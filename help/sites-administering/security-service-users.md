---
title: Adobe Experience Manager のサービスユーザー
description: Adobe Experience Manager のサービスユーザーについて説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 86%

---


# Adobe Experience Manager（AEM）のサービスユーザー {#service-users-in-aem}

## 概要 {#overview}

これまで、AEM で管理セッションやリソースリゾルバーを取得する主な方法は、Sling に用意されている `SlingRepository.loginAdministrative()` および `ResourceResolverFactory.getAdministrativeResourceResolver()` メソッドを使用することでした。

ただし、これらのメソッドはどちらも [最小権限の原則](https://ja.wikipedia.org/wiki/%E6%9C%80%E5%B0%8F%E6%A8%A9%E9%99%90%E3%81%AE%E5%8E%9F%E5%89%87). これにより、開発者がコンテンツの構造や対応するアクセス制御レベル（ACL）を早期に適切に計画しないことがよくあります。 そのため、このようなサービスに脆弱性があると、コード自体を動作させるのに管理者権限が不要であっても、`admin` ユーザーへの権限のエスカレーションが発生することがよくあります。

## 管理セッションの廃止方法 {#how-to-phase-out-admin-sessions}

### 優先度 0：機能がアクティブであるか、必要であるか、放置されているかの確認 {#priority-is-the-feature-active-needed-derelict}

管理セッションが使用されていなかったり、機能が完全に無効化されている場合があります。実装に問題がある場合は、機能を削除するか、合わせるようにします [NOP コード](https://ja.wikipedia.org/wiki/NOP).

### 優先度 1：リクエストセッションの使用 {#priority-use-the-request-session}

可能な限り、機能のリファクタリングをおこなって、コンテンツの読み取りや書き込みに特定の認証済みリクエストセッションを使用できるようにしてください。それが可能でなくても、ほとんどの場合は、以降で説明する方法に従って優先度を適用することによって対応できます。

### 優先度 2：コンテンツの再構築 {#priority-restructure-content}

問題の多くは、コンテンツを再構築することによって解決できます。再構築する際には、次のシンプルなルールに留意してください。

* **アクセス制御を変更する**

   * 本当にアクセスを必要とするユーザーまたはグループに実際にアクセス権を付与するようにします。

* **コンテンツ構造を調整する**

   * コンテンツを他の場所（使用可能なリクエストセッションとアクセス制御が一致する場所など）に移動します。
   * コンテンツの精度を変更します。

* **コードのリファクタリングを行って適切なサービスになるようにする**

   * JSP コードからサービスにビジネスロジックを移動します。こうすると、様々なコンテンツモデリングが可能になります。

また、新機能を開発する場合は、次の原則に従ってください。

* **セキュリティ要件に従ってコンテンツ構造を決定する**

   * アクセス制御の管理は自然な形で行う必要があります。
   * アクセス制御はアプリケーションではなくリポジトリによって適用する必要があります。

* **ノードタイプの使用**

   * 設定可能なプロパティセットを制限します。

* **プライバシー設定に配慮する**

   * 非公開プロファイルがある場合、例えば非公開の `/profile` ノードにあるプロファイル画像、メールアドレス、氏名を公開しないようにします。

## 厳格なアクセス制御 {#strict-access-control}

コンテンツの再構築時にアクセス制御を適用したり、新しいサービスユーザーに対してアクセス制御を適用する場合には、可能な限り厳格な ACL を適用する必要があります。考えられるすべてのアクセス制御機能を使用してください。

* 例えば、`jcr:read` を `/apps` に適用するのではなく、`/apps/*/components/*/analytics` にのみ適用します。

* [制限](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)を使用します。

* ノードタイプに ACL を適用します。
* 権限を制限します。

   * 例えば、プロパティの書き込みのみが必要な場合は、`jcr:write` 権限を付与するのではなく、代わりに `jcr:modifyProperties` を使用してください。

## サービスユーザーとマッピング {#service-users-and-mappings}

上記が失敗した場合、Sling 7 はサービスユーザーマッピングサービスを提供します。このサービスを使用して、バンドルとユーザーのマッピングおよび対応する 2 つの API メソッドを設定できます。

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

これらのメソッドは、設定されたユーザーの権限のみを持つセッションまたはリソースリゾルバーを返します。これらのメソッドの特徴は次のとおりです。

* サービスをユーザーにマッピングできます。
* サブサービスユーザーを定義できます。
* 中央設定ポイントは `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl` です。
* `service-id` = `service-name` [&quot;:&quot; subservice-name]

* `service-id` は、認証用にリソースリゾルバーまたは JCR リポジトリユーザー ID（あるいはその両方）にマッピングされます。
* `service-name` は、サービスを提供するバンドルの記号名です。

## その他の推奨事項 {#other-recommendations}

### admin-session を service-user に置き換える {#replacing-the-admin-session-with-a-service-user}

サービスユーザーとは、パスワードが設定されておらず、特定のタスクを実行するために必要な最小限の権限を持つ JCR ユーザーのことです。パスワードが設定されていない場合は、サービスユーザーでログインできません。

管理セッションを無効にする方法の 1 つは、管理セッションをサービスユーザーセッションに置き換えることです。必要に応じて、複数のサブサービスユーザーに置き換えることもできます。

管理セッションをサービスユーザーに置き換えるには、次の手順を実行します。

1. 最小権限の原則を念頭に置いて、サービスに必要な権限を特定します。
1. 必要な権限が正確に設定されたユーザーが既に存在するかどうかをチェックします。既存のユーザーがニーズを満たさない場合は、システムサービスユーザーを作成します。サービスユーザーを作成するには、RTC が必要です。複数のサブサービスユーザー（例えば、書き込み用と読み取り用に 1 つずつ）を作成して、アクセスをさらに区分化すると効果的な場合があります。
1. ユーザーの ACE を設定し、テストします。
1. サービスおよび `user/sub-users` に `service-user` マッピングを追加します。

1. サービスユーザーの sling 機能をバンドルから使用できるようにします。つまり、`org.apache.sling.api` を最新バージョンに更新します。

1. コード内の `admin-session` を `loginService` API または `getServiceResourceResolver` API に置き換えます。

## サービスユーザーの作成 {#creating-a-new-service-user}

AEM サービスユーザーのリストに自分のユースケースに適用可能なユーザーがなく、対応する RTC の問題が承認されたことを確認したら、新しいユーザーをデフォルトコンテンツに追加します。

推奨されるアプローチは、リポジトリエクスプローラー（*https://&lt;server>:&lt;port>/crx/explorer/index.jsp*）を使用するサービスユーザーを作成することです。

目的は、有効な `jcr:uuid` プロパティを取得することです。このプロパティは、コンテンツパッケージのインストール環境を使用してユーザーを作成する場合に必須です。

サービスユーザーは次の方法で作成できます。

1. *https://&lt;server>:&lt;port>/crx/explorer/index.jsp* のリポジトリエクスプローラーにアクセスします。
1. 画面の左上隅にある「**ログイン**」リンクをクリックして、管理者としてログインします。
1. 次に、システムユーザーを作成して名前を付けます。ユーザーをシステムユーザーとして作成するには、中間パスとして `system` を設定し、ニーズに合わせてオプションのサブフォルダーを追加します。

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. システムユーザーノードが次のようになっていることを確認します。

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >サービスユーザーには mixin タイプが関連付けられていません。これは、システムユーザーのアクセス制御ポリシーがないことを意味します。

対応する .content.xml をバンドルのコンテンツに追加する際には、`rep:authorizableId` を設定し、プライマリタイプを `rep:SystemUser` にしてください。次のようになります。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## ServiceUserMapper 設定への修正の追加 {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

サービスから対応するシステムユーザーへのマッピングを追加するには、[`ServiceUserMapper` ](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html) サービスのファクトリ設定を作成する必要があります。このモジュラーを維持するために、[Sling 修正メカニズム](https://issues.apache.org/jira/browse/SLING-3578)を使用してこのような設定を指定できます。このような設定をバンドルと共にインストールする場合は、[Sling の初期コンテンツ読み込み機能](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html)を使用することをお勧めします。

1. バンドルの src/main/resources フォルダーの下にサブフォルダー SLING-INF/content を作成します。
1. このフォルダーに、ファクトリ設定の内容（すべてのサブサービスユーザーマッピングを含む）を定義した org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-&lt;ファクトリ設定の一意の名前>.xml という名前のファイルを作成します。例：

1. バンドルの `src/main/resources` フォルダーの下に `SLING-INF/content` フォルダーを作成します。
1. このフォルダーに、ファイルを作成します `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` ファクトリ設定の内容（すべてのサブサービスユーザーマッピングを含む）。

   説明のために、`org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml` というファイルを取り上げます。

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

1. バンドルをインストールし、ファクトリ設定がインストールされていることを確認します。手順は次のとおりです。

   * Web コンソール（*https://serverhost:serveraddress/system/console/configMgr*）にアクセスします。
   * **Apache Sling Service User Mapper Service Amendment** を探します。
   * リンクをクリックすると、設定が適切に行われているかどうかを確認できます。

## サービスでの共有セッションの処理 {#dealing-with-shared-sessions-in-services}

`loginAdministrative()` を呼び出すと、多くの場合、共有セッションも表示されます。これらのセッションはサービスのアクティベート時に取得され、サービスが停止された場合にのみログアウトされます。これは一般的な動作ですが、次の 2 つの問題を伴います。

* **セキュリティ：**&#x200B;このような管理セッションは、共有セッションにバインドされているリソースや他のオブジェクトをキャッシュして返すために使用されます。後から呼び出しスタックで、これらのオブジェクトは、昇格された権限を持つセッションまたはリソースリゾルバーに適応させることができます。 多くの場合、呼び出し元が操作している管理セッションであることは明らかではありません。
* **パフォーマンス：** Oak では、共有セッションはパフォーマンスの問題を引き起こす可能性があるので、共有セッションの使用はお勧めしません。

このセキュリティリスクに対する最も明白な解決策は、`loginAdministrative()` の呼び出しを `loginService()` に置き換え、権限が制限されたユーザーを対象とすることです。ただし、パフォーマンスが低下する可能性があっても、影響はありません。 これを軽減するには、要求されたすべての情報をセッションと関連付けられていないオブジェクトにラップすることが考えられます。次に、オンデマンドでセッションを作成（または破棄）します。

推奨されるアプローチは、サービスの API のリファクタリングを行って、呼び出し元がセッションの作成と破棄を制御できるようにすることです。

## JSP での管理セッション {#administrative-sessions-in-jsps}

JSP では、関連するサービスがないので `loginService()` を使用できません。ただし、JSP の管理セッションは、通常、MVC パラダイムの違反の兆候を示しています。

これは、次の 2 つの方法で修正できます。

1. ユーザーセッションで操作できるようにコンテンツを再構築する。
1. JSP で使用できる API を提供するサービスにロジックを抽出する。

推奨される方法は前者です。

## イベント、レプリケーションプリプロセッサー、およびジョブの処理 {#processing-events-replication-preprocessors-and-jobs}

イベントやジョブ、場合によってはワークフローを処理すると、イベントをトリガーした対応するセッションが失われます。このため、イベントハンドラーやジョブプロセッサーは、しばしば管理セッションを使用して作業を行うことになります。この問題を解決するにはさまざまなアプローチが考えられますが、それぞれにメリットとデメリットがあります。

1. `user-id` をイベントペイロードに渡し、代理実行を使用します。

    **メリット：**&#x200B;容易に使用できます。

   **デメリット：** `loginAdministrative()` を使用する必要があります。認証済みの要求が再認証されます。

1. データへのアクセス権を持つサービスユーザーを作成または再利用します。

   **メリット：**&#x200B;現在の設計と一貫しています。変更が最小限で済みます。

   **デメリット：**&#x200B;強力なサービスユーザーに柔軟性を持たせる必要があり、権限のエスカレーションが必要になる可能性が高くなります。セキュリティモデルに抜け道ができます。

1. `Subject` のシリアル化をイベントペイロードに渡し、そのサブジェクトに基づいて `ResourceResolver` を作成します。例えば、`ResourceResolverFactory` で JAAS `doAsPrivileged` を使用します。

   **メリット：**&#x200B;セキュリティの観点からクリーンな実装が行えます。再認証は回避し、元の権限で動作します。セキュリティ関連のコードは、イベントの消費者に対して透過的です。

   **デメリット：**&#x200B;リファクタリングが必要です。セキュリティ関連のコードがイベントの消費者に対して透過的であることから、問題に発展する可能性もあります。

第 3 のアプローチは、推奨される処理技術です。

## ワークフロープロセス {#workflow-processes}

ワークフロープロセスの実装内で、ワークフローのトリガーとなった当該ユーザーセッションは失われます。これにより、頻繁に管理セッションを使用して作業を実行するワークフロープロセスが発生します。

このような問題を修正するには、[イベント、レプリケーション、プリプロセッサーおよびジョブの処理](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs)で説明したものと同じアプローチを使用することをお勧めします。

## Sling POSTプロセッサーと削除されたページ {#sling-post-processors-and-deleted-pages}

Sling POST プロセッサーの実装では、いくつかの管理セッションが使用されます。通常、管理セッションは、処理中の POST 内で削除待ちになっているノードにアクセスするために使用されます。そのため、リクエストセッションからは使用できません。削除待ちのノードにアクセスして、本来アクセス不可のメタデータを開示できます。
