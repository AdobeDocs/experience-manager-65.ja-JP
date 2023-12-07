---
title: 「IBM DB2 データベース：定期保守のコマンドの実行」
description: このドキュメントでは、AEM Forms データベースの定期保守で推奨される IBM DB2 コマンドの一覧を示します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 67%

---

# IBM DB2 データベース：定期保守のコマンドの実行 {#ibm-db-database-running-commands-for-regular-maintenance}

AEM forms データベースの定期的なメンテナンスをおこなうには、次のIBM DB2 コマンドを使用することをお勧めします。 DB2 データベースのメンテナンスとパフォーマンスチューニングについて詳しくは、 *IBM DB2 管理ガイド*.

* **runstats**：このコマンドは、その関連インデックスと共に、データベーステーブルの物理的特性を示す統計データを更新します。AEM Forms により生成される動的 SQL ステートメントは、更新済みのこれらの統計を自動的に使用しますが、データベース内で作成される静的 SQL ステートメントでは、`db2rbind` コマンドも実行する必要があります。
* **db2rbind**：このコマンドは、データベース内のすべてのパッケージを再バインドします。`runstats` ユーティリティの実行後に、このコマンドを使用してデータベース内のすべてのパッケージを再検証します。
* **reorg table or index：**&#x200B;このコマンドは、一部のテーブルおよびインデックスの再編成が必要かどうかを確認します。

  データベースの拡大と変化に伴い、テーブル統計の再計算は、データベースのパフォーマンスを向上させるために重要で、定期的に行う必要があります。 これらのコマンドは、スクリプトを使用して手動で実行するか、cron ジョブを使用して実行できます。

>[!NOTE]
>
>`runstats` コマンドを実行する前に、データベースにデータが含まれており、少なくとも 1 つのディレクトリの同期処理が実行されていることが必要です。

小規模なデータベースでは（1 万件のユーザーまたは 2,500 件のグループなど）、`runstats` コマンドを実行して同期タイミングを削減すれば十分です。

大規模なデータベースでは（10 万件のユーザーまたは 1 万件のグループなど）、`runstats` コマンドの実行前に、`reorg` コマンドを実行します。

## AEM Forms データベースでの runstats コマンドの使用 {#use-the-runstats-command-on-your-aem-forms-database}

以下の AEM Forms データベーステーブルおよびインデックスで `runstats` コマンドを実行します。

>[!NOTE]
>
>`runstats` コマンドは、最初のデータベース同期中にのみ実行する必要があります。ただし、このプロセス中に 2 回実行する必要があります。1 回はユーザーとグループの同期中、もう 1 回はグループメンバーの同期中です。 スクリプトを実行するたびに、必ずスクリプトが完全に実行されます。

正しい構文と使用法について詳しくは、データベース製造元のドキュメントを参照してください。以下では、`<schema>` を使って、DB2 ユーザー名に関連付けられたスキーマを示します。単純なデフォルトの DB2 インストールがある場合、これはデータベーススキーマ名です。

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGROUPENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY FOR INDEXES ALL
```

## AEM forms データベースで reorg コマンドを実行します。 {#run-the-reorg-command-on-your-aem-forms-database}

以下の AEM Forms データベーステーブルおよびインデックスで `reorg` コマンドを実行します。正しい構文と使用法について詳しくは、データベース製造元のドキュメントを参照してください。

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
```
