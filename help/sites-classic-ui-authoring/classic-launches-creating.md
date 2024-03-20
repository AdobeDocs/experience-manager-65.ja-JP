---
title: ローンチの作成
description: ローンチを作成し、既存の web ページの新しいバージョンを更新して後でアクティブ化できるようにします。ローンチの作成時には、タイトルとソースページを指定します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 8ab21067-c19a-4faa-8bf0-cd9f21f6df70
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 100%

---

# ローンチの作成 {#creating-launches}

ローンチを作成し、既存の web ページの新しいバージョンを更新して後でアクティブ化できるようにします。ローンチを作成する際は、タイトルとソースページを指定します。

* タイトルは、**サイドキック**&#x200B;に表示されます。作成者はサイドキックからローンチにアクセスして作業できます。
* デフォルトでは、ソースページの子ページがローンチに含まれています。必要に応じて、ソースページのみを使用することもできます。
* デフォルトでは、ソースページが変更されると、[ライブコピー](/help/sites-administering/msm.md)によってローンチページが自動的に更新されます。静的なコピーを作成して自動更新をおこなわないように指定できます。

オプションとして、**ローンチ日**（と時間）を指定して、ローンチページを昇格およびアクティベートするタイミングを定義できます。ただし、**ローンチ日**&#x200B;は&#x200B;**実稼動準備完了**&#x200B;フラグと組み合わせた場合のみ機能します（[ローンチ設定の編集](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)を参照）。アクションが実際に自動的におこなわれるようにするには、両方を設定する必要があります。

## ローンチの作成 {#creating-a-launch}

次の手順で、ローンチを作成します。

1. Web サイトの管理ページ（[http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)）を開きます。
1. 「**新規...**」をクリックし、「**新しいローンチ...**」をクリックします。
1. **ローンチを作成**&#x200B;ダイアログで、次のプロパティの値を指定します。

   * **ローンチタイトル**：ローンチの名前。作成者がわかりやすい名前にします。
   * **ソースページ**：ローンチを作成するページのパス。デフォルトでは、すべての子ページが含まれています。
   * **サブページを除外**：ソースページのみのローンチを作成し、子ページのローンチを作成しない場合は、このオプションを選択します。デフォルトでは、このオプションは選択されていません。
   * **同期を維持**：ソースページに変更があったときにローンチページのコンテンツを自動的に更新する場合は、このオプションを選択します。これを実現するには、ローンチを[ライブコピー](/help/sites-administering/msm.md)にします。
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
