---
title: '"Microsoft SQL Server データベース：設定の最適なチューニング"'
seo-title: '"Microsoft SQL Server データベース：設定の最適なチューニング"'
description: Microsoft SQL Server データベースの設定の最適なチューニング方法について説明します。
seo-description: Microsoft SQL Server データベースの設定の最適なチューニング方法について説明します。
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 100%

---


# Microsoft SQL Server データベース：設定の最適なチューニング {#microsoft-sql-server-database-fine-tuning-the-configuration}

Microsoft SQL Server を使用する場合、デフォルトの設定を変更する必要があります。Oracle Enterprise Manager でローカルサーバーを右クリックし、プロパティのダイアログボックスにアクセスします。

## メモリ設定 {#memory-settings}

最小のメモリ割り当て値を、可能な限り大きい値に変更します。データベースが別個のコンピューターで実行されている場合、すべてのメモリが使用されます。デフォルトの設定では、強制的なメモリ割り当てが行われないので、ほとんどのデータベースでパフォーマンスが低下します。実稼働マシンでは、強制的なメモリ割り当てを最大限に行う必要があります。

## プロセッサー設定 {#processor-settings}

プロセッサー設定を変更し、これは最も重要なことですが、「SQL Server の優先度を上げる」チェックボックスを選択して、サーバーが可能な限り多くのサイクルを使用できるようにします。「Use NT fibers」設定はあまり重要ではありませんが、これを選択する場合もあります。

## データベース設定 {#database-settings}

データベース設定を変更します。最も重要な設定は、「復旧間隔」です。クラッシュが発生した後に復旧を待機するまでの最大時間を指定します。デフォルトの設定は 1 分です。大きい値（5～15 分）を使用すると、サーバーがデータベースログからデータベースファイルに変更を書き込むための時間が増加し、パフォーマンスが向上します。

>[!NOTE]
>
>この設定では、起動時に必要となるログファイルの再生にかかる時間のみが変更されるので、トランザクション動作には影響を与えません。

ログファイルとデータファイルの両方の「Space Allocated」のサイズを、初期データベースよりもかなり大きいサイズに設定します。データベースが 1 年でどのくらい増大する可能性があるかを考慮してください。ログファイルおよびデータファイルを連続的に割り当て、データがすべてのディスク全体でフラグメント化されないようにすることが理想的です。
