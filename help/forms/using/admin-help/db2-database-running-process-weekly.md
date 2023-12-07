---
title: "DB2 データベース：毎週プロセスを実行"
description: AEM Forms DB2 データベースのパフォーマンスを向上させる方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 26%

---

# DB2 データベース：週単位のプロセス実行{#db-database-running-a-process-weekly}

AEM forms DB2 データベースの実行が遅くなり始めた場合は、次のプロセスを週単位で実行すると、パフォーマンスが向上します。

1. DB2 コントロールセンターを起動します。

   (Windows) スタート/プログラム/IBM DB2/General Administration Tools/Control Center を選択します。

   （Linux および UNIX）コマンドプロンプトから、`db2jcc` コマンドを入力します。

1. DB2 コントロールセンターのオブジェクトツリーで、[ すべてのデータベース ] をクリックします。
1. AEM forms 用に作成したデータベースをクリックし、 Tables フォルダーをクリックします。
1. コンテンツ・ペインですべてのデータベース・テーブルを選択し、右クリックして「統計の実行」を選択します。
1. 統計/インデックス統計に移動します。
1. 「すべてのインデックスに関する統計情報を収集」を選択し、「拡張された詳細な統計情報を含むインデックスに関する統計情報を収集」を選択して、「OK」をクリックします。

プロセスが完了すると、メッセージが表示されます。 メッセージを閉じます。
