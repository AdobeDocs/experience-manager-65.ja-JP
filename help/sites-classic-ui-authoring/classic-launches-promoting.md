---
title: ローンチの昇格
seo-title: Promoting Launches
description: コンテンツを公開する前にソース（実稼動）に戻すには、ローンチページを昇格させる必要があります。ローンチページが昇格されると、ソースページの対応するページが、昇格済みのページのコンテンツに置き換わります。
seo-description: You need to promote launch pages to move the content back into the source (production) before publishing. When a launch page is promoted, the corresponding page of the source pages is replaced with the content of the promoted page.
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 100%

---

# ローンチの昇格{#promoting-launches}

コンテンツを公開する前にソース（実稼動）に戻すには、ローンチページを昇格させる必要があります。ローンチページが昇格されると、ソースページの対応するページが、昇格済みのページのコンテンツに置き換わります。ローンチページを昇格させるときには、次のオプションを使用できます。

* 現在のページのみを昇格させるか、ローンチ全体を昇格させるか。
* 現在のページの子ページを昇格するかどうか。
* すべてのローンチを昇格させるか、変更したページのみを昇格させるか。

## ローンチページの昇格 {#promoting-launch-pages}

ページを昇格させるには、昇格させるローンチページの編集中に、次の手順を実行します。

1. サイドキックの「**ページ**」タブで、「**ローンチを昇格**」をクリックします。
1. 昇格するページを指定します。

   * （デフォルト）現在のページのみを昇格させるには、「**ページの変更を実稼動版に昇格**」を選択します。
   * 現在のページの子ページも昇格させるには、「**サブページを含める**」を選択します。
   * ローンチ内のすべてのページを昇格させるには、「**完全なローンチを実稼動版に昇格**」を選択します。

1. 実稼動版ページをワークフローパッケージに追加する場合は、「**ワークフローパッケージに追加**」を選択してワークフローパッケージを選択します。
1. 「**昇格**」をクリックします。

## AEM ワークフローを使用した昇格済みページの処理 {#processing-promoted-pages-using-aem-workflow}

次のワークフローモデルを使用して、昇格済みのローンチページの一括処理をおこないます。

1. ワークフローパッケージを作成します。
1. 作成者がローンチページを昇格するとき、ワークフローパッケージにローンチページを保存します。
1. このパッケージをペイロードとして使用し、ワークフローモデルを開始します。

ページが昇格されたときに自動的にワークフローを開始するには、パッケージノードの[ワークフローランチャーを設定](/help/sites-administering/workflows-starting.md#workflows-launchers)します。

例えば、作成者がローンチページを昇格したとき、ページのアクティベートのリクエストを自動的に生成することができます。パッケージノードが変更されたときにリクエストのアクティベートワークフローを開始するよう、ワークフローランチャーを設定します。

![chlimage_1-136](assets/chlimage_1-136.png)
