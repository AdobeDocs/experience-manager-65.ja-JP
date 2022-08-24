---
title: ローンチの作成
seo-title: Creating Launches
description: ローンチを作成し、既存の web ページの新しいバージョンを更新して後でアクティブ化できるようにします。ローンチを作成するとき、タイトルとソースページを指定します。
seo-description: Create a launch to enable the updating of a new version of existing web pages for future activation. When you create a Launch, you specify a title and the source page.
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 8ab21067-c19a-4faa-8bf0-cd9f21f6df70
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 100%

---

# ローンチの作成 {#creating-launches}

ローンチを作成し、既存の web ページの新しいバージョンを更新して後でアクティブ化できるようにします。ローンチを作成する際は、タイトルとソースページを指定します。

* タイトルは、**サイドキック**&#x200B;に表示されます。作成者はサイドキックからローンチにアクセスして作業できます。
* デフォルトで、ソースページの子ページがローンチに含まれています。希望に応じて、ソースページのみを使用することもできます。
* デフォルトでは、[ライブコピー](/help/sites-administering/msm.md)によってソースページの変更に合わせてローンチページが自動的に更新されます。静的なコピーを作成して自動更新をおこなわないように指定できます。

オプションとして、**ローンチ日**（と時間）を指定して、ローンチページを昇格およびアクティベートするタイミングを定義できます。ただし、**ローンチ日**&#x200B;は&#x200B;**実稼動準備完了**&#x200B;フラグと組み合わせた場合のみ機能します（[ローンチ設定の編集](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)を参照）。アクションが実際に自動的におこなわれるようにするには、両方を設定する必要があります。

## ローンチの作成 {#creating-a-launch}

次の手順を使用して、ローンチを作成します。

1. Web サイトの管理ページ（[http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)）を開きます。
1. 「**新規...**」をクリックし、「**新しいローンチ...**」をクリックします。
1. **ローンチを作成**&#x200B;ダイアログで、次のプロパティの値を指定します。

   * **ローンチタイトル**：ローンチの名前。作成者にとって意味のある名前にしてください。
   * **ソースページ**：ローンチを作成するページのパス。デフォルトでは、すべての子ページが含まれます。
   * **サブページを除外**：ソースページのみのローンチを作成し、子ページのローンチを作成しない場合は、このオプションを選択します。デフォルトでは、このオプションは選択されていません。
   * **同期を維持**：ソースページに変更があったときにローンチページのコンテンツを自動的に更新する場合は、このオプションを選択します。これは、ローンチを[ライブコピー](/help/sites-administering/msm.md)にすることで達成します。
   * **ローンチ日**：ローンチコピーがアクティブ化される日付と時間（「**実稼動準備完了**」フラグによって変わります。[ローンチ - イベントの順序](/help/sites-authoring/launches.md#launches-the-order-of-events)を参照してください）。

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. 「**作成**」をクリックします。

## ローンチの削除 {#deleting-a-launch}

ローンチを削除することもできます。

1. [ローンチコンソール](/help/sites-classic-ui-authoring/classic-launches.md)で、必要なローンチを選択します。
1. 「**削除**」をクリックします。このとき、次のように確認を求められます。

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >ネストされたローンチを削除する場合は、まず下位のローンチを削除する必要があります。
