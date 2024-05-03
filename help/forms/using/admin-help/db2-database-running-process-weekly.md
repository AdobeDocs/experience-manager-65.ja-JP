---
title: "DB2&reg; データベース：毎週プロセスを実行"
description: AEM Forms DB2&reg; データベースのパフォーマンスを向上させる方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 23%

---

# DB2® データベース：週単位のプロセス実行{#db-database-running-a-process-weekly}

AEM Forms DB2® データベースの動作が遅くなり始めた場合は、次のプロセスを毎週実行すると、パフォーマンスが向上します。

1. DB2® コントロール・センターを起動します。

   （Windows） スタート/プログラム/IBM® DB2®/一般管理ツール/コントロールセンターを選択します。

   （Linux® および UNIX®）コマンドプロンプトから、 `db2jcc` コマンド。

1. DB2® コントロール・センターのオブジェクト・ツリーで、「すべてのデータベース」をクリックします。
1. AEM Forms用に作成したデータベースをクリックし、「テーブル」フォルダーをクリックします。
1. コンテンツ・ペインでデータベース・テーブルをすべて選択し、右クリックして、「統計の実行」を選択します。
1. Statistics／Index Statistics に移動します。
1. 「Collect Statistics For All Indexes」を選択し、「Collect Statistics For Indexes With Extended Detailed Statistics」を選択して、「OK」をクリックします。

プロセスが完了すると、メッセージが表示されます。メッセージを閉じます。
