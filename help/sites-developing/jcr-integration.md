---
title: JCR 統合
seo-title: JCR Integration
description: JCR レベルでの統合が必要な場合のヒント
seo-description: Tips for when you must integrate at the JCR level
uuid: 11518baf-521e-471d-ad4f-2baa76075cfa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: e6647a11-a36e-4808-bb61-29b2895c6b1d
exl-id: 170474c1-c7f4-446c-bda4-84768d44a078
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '295'
ht-degree: 100%

---

# JCR 統合{#jcr-integration}

## JCR API よりも Sling リソース API を優先する {#prefer-the-sling-resource-api-to-jcr-api}

Sling API は、JCR API よりも高度な抽象レベルで機能します。これにより、コードの再利用性を高め、コードを基になるストレージから独立させることができます。したがって、必要に応じて ResourceProvider メカニズムを利用して外部の仮想データを含めることがより簡単になります。

## 可能な限りクエリを回避する {#avoid-queries-wherever-possible}

常に、クエリを実行するよりも、リポジトリ内を移動してデータを取得する方が速くなります。エンドユーザークエリやリポジトリ全体から構造化されたコンテンツを探す必要がある場合などクエリが必要になりますが、それ以外の場合は必要なノードに移動することをお勧めします。ナビゲーション要素、「最近の項目リスト」、項目数などのレンダリングロジックでは、常にクエリを回避してください。このような場合、階層をたどっていくか、レンダリング時に直接結果を使用できるように事前に結果をキャッシュに格納しておく方が効率的です。

## JCR 監視の範囲を制限する {#restrict-the-scope-of-jcr-observation}

リポジトリでイベントをリッスンするときには、できる限り範囲を絞り込むことが重要です。例えば、`/etc` でリッスンするよりも `/etc/mycompany` でイベントをリッスンする方がはるかに効率的です。決してリポジトリルートではイベントをリッスンしないでください。加えて、コールバックメソッドが実行すべき内容が何もない場合は、可能な限り速やかに処理を完了するようにしてください。

## JCR 管理者アクセスの使用を排除する {#eliminate-use-of-jcr-admin-access}

AEM 6 以降、ResourceResolverFactory からの管理セッションが廃止されているのと同様、管理ログインも廃止されています。代わりに、このタイプのアクセスを必要とするバックオフィス操作には、サービスアカウントを作成してください。ResourceResolverFactory を使用して、このアカウントの ResourceResolver を取得できます。
