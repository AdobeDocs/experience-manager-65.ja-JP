---
title: AEM Forms Workspace における既存のプロセスデータを使用した新しいプロセスの開始
description: AEM Forms Workspace で既存のプロセスデータを使用した新しいプロセスを開始する方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 6fa97c06-9238-4444-b67f-983ef3b6fdc8
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 94%
---
# AEM Forms Workspace における既存のプロセスデータを使用した新しいプロセスの開始{#initiating-a-new-process-with-existing-process-data-in-aem-forms-workspace}

既存のプロセスデータを使用して新しいプロセスを開始することができます。 既存のプロセスデータから新しいプロセスを開始する必要が生じるのは、同一のフォームを頻繁に使用する必要があり、その内容が有給休暇フォームとほとんど変わらないような場合です。 この機能を使用すると、フォームの入力が多い場合など、ユーザーが時間と労力を節約できます。

既存のプロセスデータから新しいプロセスを開始する手順は次のとおりです。

1. 次のいずれかの操作を行います。

   * 「トラッキング」で、使用するデータが含まれているプロセスインスタンスをクリックします。 右パネルにある「プロセス履歴」ビューでスタートポイントに対応するタスク行をクリックします。
   * 「トラッキング」で、プロセスインスタンスのリストを表示する検索テンプレートを検索します。 使用するデータが含まれているインスタンスを選択します。
   * 「**[!UICONTROL TODO]**」タブで、タスクを選択します。 「**[!UICONTROL 履歴]**」タブをクリックし、プロセスインスタンスを開始したタスクを選択します。

   ![タスクを選択](assets/start3_new.png) ![タスクを選択](assets/start1_new.png)

1. 「タスクアクション」ツールバーで、「**[!UICONTROL 開始]**」をクリックします。 データが事前入力された新しいプロセスインスタンスのアダプティブフォームが表示されます。

1. 必要に応じてデータを更新し、「**[!UICONTROL 完了]**」またはフォーム上の適切なボタンをクリックします。
