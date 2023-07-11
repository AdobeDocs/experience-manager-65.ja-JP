---
title: 開発とページの差分
description: 開発とページの差分
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 35%

---

# 開発とページの差分{#developing-and-page-diff}

## 機能概要 {#feature-overview}

コンテンツの作成は反復的なプロセスです。 効率的にオーサリングを行うには、何がイテレーションから別のイテレーションに変わったかを確認できる必要があります。 あるページバージョンを見てから別のページバージョンを見るのは非効率的であり、エラーが発生しやすくなります。作成者は、現在のページを前のバージョンと並べて比較し、違いを強調表示したいと考えています。

ページの差分を使用すると、ユーザーは現在のページを起動回数、以前のバージョンなどと比較できます。 このユーザー機能の詳細については、 [ページの差分](/help/sites-authoring/page-diff.md).

## 操作の詳細 {#operation-details}

ページのバージョンを比較する場合、比較対象となる以前のバージョンがAEMによってバックグラウンドで再作成され、差分が容易になります。 これは、[並べて比較](/help/sites-developing/pagediff.md#operation-details)できるようにコンテンツをレンダリングするために必要です。

この再作成操作は AEM の内部でおこなわれるもので、ユーザーに対しては透過的であり、ユーザーの介入は必要ありません。ただし、管理者がリポジトリを閲覧している場合、例えば、CRXDE Lite内で再作成されたこれらのバージョンは、コンテンツ構造内に表示されます。

コンテンツを比較すると、比較対象のページまでのツリー全体が次の場所に再作成されます。

`/tmp/versionhistory/`

クリーンアップタスクが自動的に実行されて、この一時コンテンツがクリーンアップされます。

## 権限 {#permissions}

以前の Classic UI では、AEM の差分取得を容易にするために開発に関して特別な考慮が必要でした（例えば、`cq:text` タグライブラリの使用、`DiffService` OSGi サービスのコンポーネントへのカスタム統合など）。差分は DOM 比較を通じてクライアント側で実行されるので、新しい差分機能ではこれが不要になりました。

ただし、開発者が考慮する必要があるいくつかの制限があります。

* この機能では、AEM製品に名前空間化されていない CSS クラスを使用します。 同じ名前の他のカスタム CSS クラスまたはサードパーティの CSS クラスがページに含まれている場合、差分の表示に影響が及ぶ可能性があります。

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* 差分はクライアント側で、ページの読み込み時に実行されるので、クライアント側の差分サービスの実行後に DOM を調整した場合、その調整は考慮されません。 これは、

   * AJAX を使用してコンテンツを取り込むコンポーネント
   * 単一ページアプリケーション
   * ユーザーの操作に応じて DOM を操作する JavaScript ベースのコンポーネント。

>[!NOTE]
>
>ページの差分比較は、有効な cq:editConfig ノードを持つコンポーネントに対してのみ機能します。
