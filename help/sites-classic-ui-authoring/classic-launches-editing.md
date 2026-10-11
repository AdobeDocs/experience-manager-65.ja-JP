---
title: ローンチの編集
description: ページ（またはページのセット）にローンチが作成されている場合、ページのローンチコピーのコンテンツを編集できます。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 95%
---
# ローンチの編集{#editing-launches}

## ローンチページの編集 {#editing-launch-pages}

ページ（またはページのセット）にローンチが作成されている場合、ページのローンチコピーのコンテンツを編集できます。

1. 編集するページを開きます。
1. サイドキックで「**バージョン管理**」タブを選択し、「**ローンチ**」グループを展開します。 現在編集中のローンチのタイトルには太字フォントが使用されています。

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. 作業対象とするローンチを選択し、「**切り替え**」をクリックします。
1. 編集を開始します。

   >[!NOTE]
   >
   >サイドキックの「**ページ**」タブを使用して、**子ページを作成**&#x200B;するなどのアクションを実行できます。

## ローンチの設定の編集 {#editing-a-launch-configuration}

ローンチの作成後、ローンチ名およびローンチ日を変更できます。 また、ローンチに関連付ける画像を指定できます。

1. 起動管理ページ （[http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)）を開きます。

1. 必要なローンチを選択し、「**編集**」をクリックしてダイアログを開きます。

   * 「**一般**」タブで、次の情報を編集できます。

     * **タイトル**
     * **開始日**：ローンチ日と同じ
     * **実稼動準備完了**

     これらのフィールドの目的と操作について詳しくは、[ローンチ - イベントの順序](/help/sites-authoring/launches.md#launches-the-order-of-events)を参照してください。

   * 「**画像**」タブで、画像ファイルをアップロードできます。

1. 「**保存**」をクリックします。

## ページのローンチステータスの確認 {#discovering-the-launch-status-of-a-page}

ページのローンチの編集時、ローンチについての情報がサイドキックの「**バージョン管理**」タブの下部に表示されます。

* ローンチの名前。
* 最後の変更からの時間。
* 最後の変更を実行したユーザー。
* 「**実稼動準備完了**」フラグのステータス（オレンジ = 未設定、緑 = 設定済み）。

![chlimage_1-186](assets/chlimage_1-186.png)
