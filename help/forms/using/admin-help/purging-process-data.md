---
title: プロセスデータの削除
description: 長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎて、結果的に AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。プロセスデータを削除する方法を確認してください。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '199'
ht-degree: 100%

---

# プロセスデータの削除 {#purging-process-data}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎて、結果的に AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。レコードが不要になったら、プロセスデータを削除することをお勧めします。AEM Forms には、プロセスデータを削除するいくつかの方法が用意されています。

* 管理コンソールを使用して、長期間有効なプロセスに関連する古いレコードを一度に削除したり、定期的に自動で削除するようにスケジュールしたりできます（[ジョブマネージャーのデータベースからの古いレコードの削除](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)を参照）。
* AEM Forms の Java API および Web サービス API を使用して、長期間有効なプロセスに関連するプロセスデータをプログラムで削除できます（[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp)の「プロセスデータの削除」を参照）。
* プロセス名および他のパラメーターに基づいてプロセスをクリアするには、プロセス削除ツールを使用します。詳しくは、*[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt にあるプロセス削除ツールの ReadMe ファイルを参照してください。
