---
title: AEM Forms アプリケーションで自動保存を使用
seo-title: Using autosave in AEM Forms app
description: データの損失を防ぐために AEM Forms アプリケーションの自動保存機能を使用する方法について学びます。
seo-description: Learn how to use autosave feature in AEM Forms app that lets you avoid data loss.
uuid: 00fe6a10-1a72-443d-a840-0415dc769199
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2c71cc28-b7c8-4785-9fc2-b47fa80cbd70
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 100%

---

# AEM Forms アプリケーションで自動保存を使用{#using-autosave-in-aem-forms-app}

Adobe Experience Manager Forms アプリケーションでユーザーがデータを入力すると、自動保存の機能により一定の間隔でデータが保存されます。AEM Forms アプリケーションの自動保存の機能は、意図せずにアプリケーションを終了した場合にデータの損失を防ぐことができます。

次のような場合にアプリケーションが意図せずに終了することがあります。

* バッテリー残量の低下によりデバイスがシャットダウンした場合
* ユーザーがアプリケーションを故意に終了した場合
* 予期しないクラッシュが発生した場合

入力したデータを保存する間隔は、指定することができます。

>[!NOTE]
>
>自動保存の頻度は慎重に選択してください。自動保存を頻繁に実行すると、デバイスのパフォーマンスに影響を及ぼすことがあります。

AEM Forms アプリケーションで自動保存の機能を使用するには、次の手順を実行します。

1. アプリケーションにログインし、**設定／一般**&#x200B;に移動します。
1. 一般画面で「**自動保存頻度**」オプションを使用し、入力したデータをアプリケーションで保存する間隔を選択します。
   [ ![自動保存頻度の設定](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. アプリケーションを再起動して同じユーザーでログインすると、未保存のタスクの復元ダイアログで、タスクを復元するように求められます。未保存のタスクの復元ダイアログで「**OK**」をクリックすると、保存済みのタスクで作業を再開できます。「**キャンセル**」をクリックし、最後にトリガーされた自動保存の保存済みデータを削除して、新しいタスクで作業を始めることもできます。

   「**OK**」をクリックすると、アプリケーションがクラッシュする前に最後にトリガーされた自動保存に対応するデータが使用されてタスクが復元されます。タスクに関連付けられたフォームデータとすべての添付ファイルも復元されます。
   [ ![タスクの復元&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.** 作業中のフォーム **B.** 強制終了したアプリ **C.** 未保存のタスクを復元ダイアログで再起動したアプリ **D.** 元のデータで復元されたフォーム
