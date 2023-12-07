---
title: プロセスデータの削除
description: 長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎるため、AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。 プロセスデータをパージする方法を参照してください。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 3%

---

# プロセスデータの削除 {#purging-process-data}

長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎるため、AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。 レコードが不要になった場合は、プロセスデータをパージすることをお勧めします。 AEM forms には、プロセスデータをパージするいくつかの方法が用意されています。

* 管理コンソールを使用して、長期間有効なプロセスに関連する古いレコードを 1 回限り削除したり、定期的な自動削除をスケジュールしたりできます。 ( 詳しくは、 [ジョブマネージャーデータベースからレコードをパージします](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* AEM forms Java API と Web サービス API を使用して、長期間有効なプロセスに関連するプロセスデータをプログラムによってパージできます。 (「プロセス・データのパージ」( [AEM forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp).)
* プロセス名と他のパラメータに基づいてプロセスをパージするには、プロセスパージツールを使用します。 詳しくは、プロセスパージツールの readme ファイル ( *[aem_forms ルート]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
