---
title: DB2&reg; データベース：毎週プロセスを実行
description: AEM Forms DB2&reg; データベースのパフォーマンスを向上させる方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
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
source-wordcount: '149'
ht-degree: 85%
---
# DB2® データベース：週単位のプロセス実行{#db-database-running-a-process-weekly}

ご使用の AEM Forms DB2® データベースの動作が遅くなり始めたら、週単位で以下のプロセスを実行することで、パフォーマンスが向上します。

1. DB2® コントロールセンターを起動します。

   （Windows）スタート／すべてのプログラム／IBM® DB2®／General Administration Tools／Control Center を選択します。

   （Linux® および UNIX®）コマンドプロンプトから、`db2jcc` コマンドを入力します。

1. DB2® コントロールセンターのオブジェクトツリーで、「すべてのデータベース」をクリックします。
1. AEM Forms 用に作成したデータベースを選択して、表フォルダーをクリックします。
1. コンテンツパネル内のデータベーステーブルをすべて選択し、それらを右クリックして「実行統計」をクリックします。
1. Statistics／Index Statistics に移動します。
1. 「Collect Statistics For All Indexes」を選択し、「Collect Statistics For Indexes With Extended Detailed Statistics」を選択して、「OK」をクリックします。

プロセスが完了すると、メッセージが表示されます。 メッセージを閉じます。
