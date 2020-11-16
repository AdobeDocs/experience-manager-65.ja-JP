---
title: JCR 統合
seo-title: JCR 統合
description: JCR レベルでの統合が必要な場合のヒント
seo-description: JCR レベルでの統合が必要な場合のヒント
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 78%

---


# JCR 統合{#jcr-integration}

## JCR API よりも Sling リソース API を優先する {#prefer-the-sling-resource-api-to-jcr-api}

Sling API は、JCR API よりも高度な抽象レベルで機能します。これにより、コードの再利用性を高め、コードを基になるストレージから独立させることができます。したがって、必要に応じて ResourceProvider メカニズムを利用して外部の仮想データを含めることがより簡単になります。

## 可能な限りクエリを回避する {#avoid-queries-wherever-possible}

常に、クエリを実行するよりも、リポジトリ内を移動してデータを取得する方が速くなります。エンドユーザークエリやリポジトリ全体から構造化されたコンテンツを探す必要がある場合などクエリが必要になりますが、それ以外の場合は必要なノードに移動することをお勧めします。ナビゲーションコンポーネント、「最新のアイテムリスト」、アイテムの数などのレンダリングロジックでは、クエリは常に避ける必要があります。 このような場合、階層をたどっていくか、レンダリング時に直接結果を使用できるように事前に結果をキャッシュに格納しておく方が効率的です。

## JCR 監視の範囲を制限する {#restrict-the-scope-of-jcr-observation}

リポジトリでのイベントをリスンするときには、できる限り範囲を絞り込むことが重要です。For example, it is much better to listen for an event at `/etc/mycompany` than to listen at `/etc`. リポジトリのルートでイベントをリッスンしないでください。 また、コールバックメソッドが実行する必要がない場合は、できるだけ早くコールバックメソッドを実行するようにしてください。

## JCR 管理者アクセスの使用を排除する {#eliminate-use-of-jcr-admin-access}

AEM 6 以降、ResourceResolverFactory からの管理セッションが廃止されているのと同様、管理ログインも廃止されています。代わりに、このタイプのアクセスを必要とするバックオフィス操作用にサービスアカウントを作成してください。ResourceResolverFactory を使用して、このアカウントの ResourceResolver を取得できます。
