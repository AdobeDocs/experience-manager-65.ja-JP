---
title: 開発とページの差分
seo-title: 開発とページの差分
description: 'null'
seo-description: 'null'
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 92%

---


# 開発とページの差分{#developing-and-page-diff}

## 機能概要 {#feature-overview}

コンテンツの作成は反復的なプロセスです。効率的にオーサリングをおこなうには、反復するごとに何が変更されたかがわかるようにする必要があります。あるページバージョンを見てから別のページバージョンを見るのは非効率的であり、エラーが発生しやすくなります。作成者は、現在のページと前のバージョンを並べて比較する際に、差分が強調表示されるようにしたいと考えています。

ページの差分機能を使用すると、ユーザーは現在のページをローンチや以前のバージョンなどと比較できます。このユーザー機能について詳しくは、[ページの差分](/help/sites-authoring/page-diff.md)を参照してください。

## 操作の詳細 {#operation-details}

ページのバージョンを比較する場合、差分を検出しやすくするために、比較対象となる以前のバージョンが AEM によってバックグラウンドで再作成されます。これは、[並べて比較](/help/sites-developing/pagediff.md#operation-details)できるようにコンテンツをレンダリングするために必要です。

この再作成操作は AEM の内部でおこなわれるもので、ユーザーに対しては透過的であり、ユーザーの介入は必要ありません。ただし、管理者が CRX DE Lite などでリポジトリーを閲覧している場合は、再作成されたこれらのバージョンがコンテンツ構造内に表示されます。

コンテンツを比較すると、比較対象のページまでのツリー全体が次の場所に再作成されます。

`/tmp/versionhistory/`

クリーンアップタスクが自動的に実行されて、この一時コンテンツがクリーンアップされます。

## 権限 {#permissions}

以前は、Classic UIでは、AEMの変更を容易にするために、特別な開発上の考慮が必要でした（例えば、`cq:text`タグライブラリを使用したり、`DiffService` OSGiサービスをコンポーネントに統合するなど）。 新しい差分機能ではこのような考慮は必要なくなりました。差分は DOM 比較を介してクライアント側で実行されるからです。

ただし、開発者が考慮する必要がある制限事項はいくつかあります。

* この機能では、AEM 製品の名前空間にない CSS クラスが使用されます。同じ名前の付いた他のカスタム CSS クラスまたはサードパーティの CSS クラスがページに含まれている場合、差分の表示に影響が及ぶ可能性があります。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 差分はクライアント側でページの読み込み時に実行されるので、クライアント側の差分サービスが実行された後に DOM を調整しても、その効果はありません。これは、次の項目に影響を与える可能性があります。

   * AJAX を使用してコンテンツを取り込むコンポーネント
   * 単一ページアプリケーション
   * ユーザーインタラクションに対して DOM を操作する JavaScript ベースのコンポーネント
