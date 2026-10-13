---
title: 'Microsoft SQL Server データベース: 設定の微調整'
description: Microsoft SQL Server データベースの設定を微調整する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
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
source-wordcount: '299'
ht-degree: 100%
---
# Microsoft SQL Server データベース: 設定の微調整 {#microsoft-sql-server-database-fine-tuning-the-configuration}

Microsoft SQL Server を使用する場合、デフォルトの設定を変更する必要があります。 Oracle Enterprise Manager でローカルサーバーを右クリックし、プロパティのダイアログボックスにアクセスします。

## メモリ設定 {#memory-settings}

最小のメモリ割り当て値を、可能な限り大きい値に変更します。 データベースが別個のコンピューターで実行されている場合は、すべてのメモリを使用します。 デフォルトの設定では、メモリが積極的に割り当てられないため、ほとんどのデータベースでパフォーマンスが低下します。 本番マシンでは、メモリをできるだけ積極的に割り当てる必要があります。

## プロセッサー設定 {#processor-settings}

プロセッサー設定を変更し、これは最も重要なことですが、「Windows で SQL Server の優先度を上げる」チェックボックスを選択して、サーバーが可能な限り多くのサイクルを使用できるようにします。 「NT Fiber を使用」設定はあまり重要ではありませんが、これも選択するとよいでしょう。

## データベース設定 {#database-settings}

データベース設定を変更します。 最も重要な設定は「復旧間隔」です。これは、クラッシュ発生後の復旧の待機時間の最大値を指定します。 デフォルト設定は 1 分です。 大きい値（5～15 分）を使用すると、サーバーがデータベースログからデータベースファイルに変更を書き込むための時間が増加し、パフォーマンスが向上します。

>[!NOTE]
>
>この設定では、起動時に必要となるログファイルの再生にかかる時間のみが変更されるので、トランザクション動作には影響を与えません。

ログファイルとデータファイルの両方の「Space Allocated（割り当てスペース）」のサイズを、初期データベースよりもかなり大きいサイズに設定します。 データベースが 1 年でどのくらい増大する可能性があるかを考慮してください。 ログファイルおよびデータファイルを連続的に割り当て、データがすべてのディスク全体でフラグメント化されないようにすることが理想的です。
