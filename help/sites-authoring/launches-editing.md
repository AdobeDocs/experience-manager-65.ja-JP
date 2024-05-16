---
title: ローンチの編集
description: ページ（またはページのセット）のローンチを作成した後で、ページのローンチコピーのコンテンツを編集できます。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 2d441820-b394-47c8-b4ca-a8aede590937
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Launches
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: ht
source-wordcount: '523'
ht-degree: 100%

---

# ローンチの編集 {#editing-launches}

## ローンチページの編集 {#editing-launch-pages}

ページ（またはページのセット）にローンチが作成されている場合、ページのローンチコピーのコンテンツを編集できます。

1. [「参照」のローンチ（Sites コンソール）](/help/sites-authoring/launches.md#launches-in-references-sites-console)にアクセスして使用可能なアクションを表示します。
1. 「**このページに移動**」を選択して、編集するページを開きます。

>[!NOTE]
>
>ローンチ内でページを移動することはできません。この操作を試みると、次の警告メッセージが表示されます：
>
>* 警告：このページはローンチのソースです。ページの移動は許可されません。

### ライブコピーへのローンチページサブジェクトの編集 {#editing-launch-pages-subject-to-a-live-copy}

ローンチが[ライブコピー](/help/sites-administering/msm.md)に基づいている場合は、次のようになります。

* コンポーネント（コンテンツやプロパティ）を編集するときに、ロックシンボル（小さな鍵アイコン）が表示されます。
* 「**ライブコピー**」タブが&#x200B;**ページのプロパティ**&#x200B;に表示されます。

ライブコピーは、コンテンツをソースブランチ&#x200B;*から*&#x200B;ローンチブランチ&#x200B;*に*&#x200B;同期するために使用します（ローンチを、ソースに加えられた変更を含む最新の状態に保ちます）。

標準のライブコピーを編集する場合と同じ方法で変更できます。例えば次のようにします。

* 閉じられた鍵アイコンをクリックするとこの同期が解除され、ローンチのコンテンツを新たに更新できるようになります。ロックを解除（開いた鍵アイコン）すると、ソース分岐内の同じ場所に変更を加えても、ユーザーの変更が上書きされなくなります。
* 特定のページの継承を&#x200B;**一時停止**（および&#x200B;**再開**）します。

詳しくは、「[ライブコピーのコンテンツの変更](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)」を参照してください。

## ローンチページとそのソースページの比較 {#comparing-a-launch-page-to-its-source-page}

行った変更を追跡するために、ローンチを&#x200B;**参照**&#x200B;で表示して、ローンチページをそのソースページと比較することができます。

1. **Sites** コンソールで[ローンチのソースページに移動し、該当するローンチを選択します](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources)。
1. **[参照](/help/sites-authoring/basic-handling.md#references)**&#x200B;パネルを開いて、「**ローンチ**」を選択します。
1. 特定のローンチを選択してから、次のように&#x200B;**ソースと比較します**。

   ![screen-shot_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. 2 つのページ（ローンチとソース）が左右に並んで開きます。

   この機能の使用方法について詳しくは、[ページの差分](/help/sites-authoring/page-diff.md)を参照してください。

## 使用するソースページの変更 {#changing-the-source-pages-used}

ローンチのソースページの範囲に対して、任意のタイミングでページを追加または削除できます。

1. 次のいずれかの方法を使用して、ローンチにアクセスして選択します。

   * [ローンチコンソール](/help/sites-authoring/launches.md#the-launches-console)：

      * 「**編集**」を選択します。

   * [「参照」（Sites コンソール）](/help/sites-authoring/launches.md#launches-in-references-sites-console)：使用可能なアクションを表示します。

      * 「**ローンチを編集**」を選択します。

   ソースページが表示されます。

1. 必要な変更を加え、「**保存**」で確定します。

   >[!NOTE]
   >
   >ローンチにページを追加するには、ページを共通の言語ルートの下（単一のサイト内）に配置する必要があります。

## ローンチの設定の編集 {#editing-a-launch-configuration}

ローンチのプロパティは、任意のタイミングで編集できます。

1. 次のいずれかの方法を使用して、ローンチにアクセスして選択します。

   * [ローンチコンソール](/help/sites-authoring/launches.md#the-launches-console)：

      * **プロパティ**&#x200B;を選択します。

   * [「参照」（Sites コンソール）](/help/sites-authoring/launches.md#launches-in-references-sites-console)：使用可能なアクションを表示します。

      * 「**プロパティを編集**」を選択します。

   詳細が表示されます。

1. 必要な変更を加え、「**保存**」で確定します。

   「**ローンチ日**」フィールドと「**実稼働準備完了**」フィールドの目的とインタラクションについて詳しくは、[ローンチ - イベントの順序](/help/sites-authoring/launches.md#launches-the-order-of-events)を参照してください。

## ページのローンチステータスの確認 {#discovering-the-launch-status-of-a-page}

「参照」タブから特定のローンチを選択すると、ステータスが表示されます（[「参照」のローンチ（サイトコンソール）](/help/sites-authoring/launches.md#launches-in-references-sites-console)を参照）。

![screen-shot_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
