---
title: リモートAdobe Experience Manager GraphQLクエリのコンテンツフラグメントに対する認証
description: ヘッドレスコンテンツ配信を保護するためにリモートAdobe Experience Manager GraphQLクエリに必要な認証を理解します。
feature: Content Fragments,GraphQL API
exl-id: 167f3318-7bc7-48fc-aaa9-73da43433f2f
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# リモートAdobe Experience Manager GraphQLクエリのコンテンツフラグメントに対する認証 {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

主な用途 [コンテンツフラグメント配信用Adobe Experience Manager (AEM)GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) は、サードパーティのアプリケーションまたはサービスからのリモートクエリを受け入れます。 これらのリモートクエリでヘッドレスコンテンツ配信を保護するには、認証済み API アクセスが必要になる場合があります。

>[!NOTE]
>
>テストおよび開発の場合は、 [GraphiQL インターフェイス](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface).

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
