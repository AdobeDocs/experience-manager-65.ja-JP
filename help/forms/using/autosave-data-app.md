---
title: AEM Forms アプリケーションで自動保存を使用
description: データの損失を防ぐために AEM Forms アプリケーションの自動保存機能を使用する方法について説明します。
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
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
source-wordcount: '309'
ht-degree: 86%
---
# AEM Forms アプリケーションで自動保存を使用{#using-autosave-in-aem-forms-app}

>[!NOTE]
>
>AEM Forms アプリは現在、非推奨です。 質問またはヘルプについては、[aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com)までお問い合わせください。

Adobe Experience Manager Forms アプリケーションでユーザーがデータを入力すると、自動保存の機能により一定の間隔でデータが保存されます。 AEM Forms アプリケーションの自動保存の機能は、意図せずにアプリケーションを終了した場合にデータの損失を防ぐことができます。

次のような場合に、アプリケーションが意図せず終了することがあります。

* バッテリー残量の低下によりデバイスがシャットダウンした場合
* ユーザーがアプリケーションを終了した場合
* 予期しないクラッシュが発生した場合

入力したデータを保存する間隔は、指定することができます。

>[!NOTE]
>
>自動保存の頻度は慎重に選択してください。 自動保存を頻繁に実行すると、デバイスのパフォーマンスに影響を及ぼすことがあります。

AEM Forms アプリケーションで自動保存の機能を使用するには、次の手順を実行します。

1. アプリケーションにログインし、**設定／一般**&#x200B;に移動します。
1. 一般画面で「**自動保存頻度**」オプションを使用し、入力したデータをアプリケーションで保存する間隔を選択します。
   [![自動保存頻度の設定](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. アプリケーションを再起動して同じユーザーでログインすると、未保存のタスクの復元ダイアログで、タスクを復元するように求められます。 未保存のタスクの復元ダイアログで「**OK**」をクリックすると、保存済みのタスクで作業を再開できます。 「**キャンセル**」をクリックし、最後にトリガーされた自動保存の保存済みデータを削除して、新しいタスクで作業を始めることもできます。

   「**OK**」をクリックすると、アプリケーションがクラッシュする前に最後にトリガーされた自動保存に対応するデータが使用されてタスクが復元されます。 タスクに関連付けられたフォームデータとすべての添付ファイルも復元されます。
   [![復元されたタスクを取得しています&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** 作業中のフォーム **B.** アプリが&#x200B;**C.** アプリを強制終了しました。元のデータで復元された未保存のタスクを復元ダイアログ **D.** フォームでアプリを再開しました
