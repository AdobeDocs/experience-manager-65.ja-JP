---
title: コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証
description: ヘッドレスコンテンツ配信を保護するためにリモート AEM GraphQL クエリに必要な認証について説明します。
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: 9278ba4fe85edca4ab5741f89c0fc0ef2cf2764d
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 61%

---

# コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

主な用途 [Adobe Experience Manager (AEM) コンテンツフラグメント配信用の GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md) は、サードパーティのアプリケーションまたはサービスからのリモートクエリを受け入れます。 ヘッドレスコンテンツ配信を保護するために、これらのリモートクエリには、認証済み API アクセスが必要な場合があります。

>[!NOTE]
>
>テストおよび開発の場合は、[GraphiQL インターフェイス](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface)を使用して AEM GraphQL API に直接アクセスすることもできます。

認証の場合、サードパーティのサービスは、AEMアカウントのユーザー名とパスワードを使用して認証する必要があります。

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
