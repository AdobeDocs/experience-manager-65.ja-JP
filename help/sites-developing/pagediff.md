---
title: 開発とページの差分
description: Adobe Experience Manager でページ差分機能を開発および利用する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 100%

---

# 開発とページの差分{#developing-and-page-diff}

## 機能概要 {#feature-overview}

コンテンツの作成は反復的なプロセスです。効率的に作成するには、ある反復から別の反復へと何が変わったかを確認できることが必要です。あるページバージョンを見てから別のページバージョンを見るのは非効率的であり、エラーが発生しやすくなります。作成者は、現在のページと前のバージョンを並べて比較する際に、差分がハイライト表示されるようにしたいと考えています。

ページの差分機能を使用すると、ユーザーは現在のページをローンチや以前のバージョンなどと比較できます。このユーザー機能について詳しくは、[ページの差分](/help/sites-authoring/page-diff.md)を参照してください。

## 操作の詳細 {#operation-details}

ページのバージョンを比較する場合、差分を検出しやすくするために、比較対象となる以前のバージョンが AEM によってバックグラウンドで再作成されます。これは、[並べて比較](/help/sites-developing/pagediff.md#operation-details)できるようにコンテンツをレンダリングするために必要です。

この再作成操作は AEM の内部でおこなわれるもので、ユーザーに対しては透過的であり、ユーザーの介入は必要ありません。ただし、管理者が CRXDE Lite などでリポジトリを閲覧している場合は、再作成されたこれらのバージョンがコンテンツ構造内に表示されます。

コンテンツを比較すると、比較対象のページまでのツリー全体が次の場所に再作成されます。

`/tmp/versionhistory/`

クリーンアップタスクが自動的に実行されて、この一時コンテンツがクリーンアップされます。

## 権限 {#permissions}

以前の Classic UI では、AEM の差分取得を容易にするために開発に関して特別な考慮が必要でした（例えば、`cq:text` タグライブラリの使用、`DiffService` OSGi サービスのコンポーネントへのカスタム統合など）。これは、新しい差分機能では必要なくなりました。差分は DOM 比較を介してクライアント側で実行されるからです。

ただし、デベロッパーが考慮する必要がある制限事項はいくつかあります。

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
   * ユーザーインタラクションに対して DOM を操作する JavaScript ベースのコンポーネント。

>[!NOTE]
>
>ページの差分比較は、有効な cq:editConfig ノードを持つコンポーネントに対してのみ機能します。
