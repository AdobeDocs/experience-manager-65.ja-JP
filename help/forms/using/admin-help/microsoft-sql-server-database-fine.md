---
title: "Microsoft SQL Server データベース：設定の最適なチューニング"
description: Microsoft SQL Server データベースの設定を微調整する方法を説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---

# Microsoft SQL Server データベース：設定の最適なチューニング {#microsoft-sql-server-database-fine-tuning-the-configuration}

Microsoft SQL Server を使用する場合は、デフォルトの設定を変更する必要があります。 Enterprise Manager でローカル・サーバーを右クリックして、Oracle・ダイアログ・ボックスにアクセスします。

## メモリ設定 {#memory-settings}

最小メモリ割り当てをできるだけ大きい数に変更します。 データベースが別のコンピュータで実行されている場合は、すべてのメモリを使用します。 デフォルト設定では、積極的にメモリを割り当てないので、ほとんどのデータベースでのパフォーマンスが低下します。 実稼動マシンにメモリを割り当てる際は、最も積極的に行う必要があります。

## プロセッサー設定 {#processor-settings}

プロセッサの設定を変更し、最も重要な点は、[Windows での SQL Server の優先度を上げる ] チェックボックスをオンにして、サーバができるだけ多くのサイクルを使用できるようにします。 [NT ファイバを使用 ] の設定はあまり重要ではありませんが、この設定を選択することもできます。

## データベース設定 {#database-settings}

データベース設定を変更します。 最も重要な設定は、クラッシュ後に回復を待機する最大時間を指定する [ 回復間隔 ] です。 デフォルト設定は 1 分です。 5 ～ 15 分の大きな値を使用すると、サーバはデータベースログからデータベースファイルに変更を書き戻す時間を長くするので、パフォーマンスが向上します。

>[!NOTE]
>
>この設定では、起動時に実行する必要のあるログファイルの再生の長さのみが変更されるので、トランザクション動作に影響はありません。

ログとデータ・ファイルの両方の「Space Allocated」サイズを、初期のデータベースよりも大きく設定します。 1 年間にデータベースがどの程度増大するかを検討します。 ログファイルとデータファイルは、連続した範囲で割り当てられ、データがディスク全体で断片化されるのを防ぐのが理想的です。
