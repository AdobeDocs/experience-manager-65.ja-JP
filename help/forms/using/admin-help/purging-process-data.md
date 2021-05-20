---
title: プロセスデータの削除
seo-title: プロセスデータの削除
description: 長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎて、結果的に AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。プロセスデータをパージする方法を確認してください。
seo-description: 長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎて、結果的に AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。プロセスデータをパージする方法を確認してください。
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 89%

---

# プロセスデータの削除 {#purging-process-data}

長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎて、結果的に AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。レコードが不要になったら、プロセスデータを削除することをお勧めします。AEM forms には、プロセスデータを削除するいくつかの方法が用意されています。

* 管理コンソールを使用して、長期間有効なプロセスに関連する古いレコードを一度に削除したり、定期的に自動で削除するようにスケジュールしたりできます（[ジョブマネージャーのデータベースからの古いレコードの削除](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)を参照）。
* AEM Forms の Java API および Web サービス API を使用して、長期間有効なプロセスに関連するプロセスデータをプログラムで削除できます（「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63)」の「プロセスデータの削除」を参照してください。）
* プロセス名および他のパラメーターに基づいてプロセスをクリアするには、プロセス削除ツールを使用します。詳しくは、*[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txtディレクトリにあるプロセスパージツールのreadmeファイルを参照してください。
