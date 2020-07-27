---
title: '"IBM DB2 データベース：定期保守のコマンドの実行"'
seo-title: '"IBM DB2 データベース：定期保守のコマンドの実行"'
description: このドキュメントでは、AEM Forms データベースの定期保守で推奨される IBM DB2 コマンドの一覧を示します。
seo-description: このドキュメントでは、AEM Forms データベースの定期保守で推奨される IBM DB2 コマンドの一覧を示します。
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 89%

---


# IBM DB2 データベース：定期保守のコマンドの実行 {#ibm-db-database-running-commands-for-regular-maintenance}

AEM Forms データベースの定期保守には、以下の IBM DB2 コマンドが推奨されます。DB2 データベースの保守およびパフォーマンスチューニングについて詳しくは、『*IBM DB2 Administration Guide*』を参照してください。

* **runstats：**&#x200B;このコマンドは、その関連インデックスと共に、データベーステーブルの物理的特性を示す統計データを更新します。AEM Forms により生成される動的 SQL ステートメントは、更新済みのこれらの統計を自動的に使用しますが、データベース内で作成される静的 SQL ステートメントでは、`db2rbind` コマンドも実行する必要があります。
* **db2rbind:** このコマンドは、データベース内のすべてのパッケージを再バインドします。 `runstats` ユーティリティの実行後に、このコマンドを使用してデータベース内のすべてのパッケージを再検証します。
* **reorg table or index:** このコマンドは、一部のテーブルとインデックスの再編成が必要かどうかを確認します。

   データベースは増大および変更されていくので、テーブル統計データの再計算はデータベースパフォーマンスの向上に不可欠なものであり、定期的に実行する必要があります。これらのコマンドは、スクリプトを使用して手動で実行することも、cron ジョブを使用することもできます。

>[!NOTE]
>
>`runstats` コマンドを実行する前に、データベースにデータが含まれており、少なくとも 1 つのディレクトリの同期処理が実行されていることが必要です。

小規模なデータベースでは（1 万件のユーザーまたは 2,500 件のグループなど）、`runstats` コマンドを実行して同期タイミングを削減すれば十分です。

大規模なデータベースでは（10 万件のユーザーまたは 1 万件のグループなど）、`reorg` コマンドの実行前に、`runstats` コマンドを実行します。

## AEM Forms データベースでの runstats コマンドの使用 {#use-the-runstats-command-on-your-aem-forms-database}

以下の AEM Forms データベーステーブルおよびインデックスで `runstats` コマンドを実行します。

>[!NOTE]
>
>`runstats` コマンドは、最初のデータベース同期中にのみ実行する必要があります。ただし、同期プロセス中に 2 回（ユーザーとグループの同期中に 1 回、グループメンバーの同期中に 1 回）実行する必要があります。スクリプトを実行するたびに、実行が正常に完了したことを確認してください。

正しい構文と使用法について詳しくは、データベース製造元のドキュメントを参照してください。Below, `<schema>` is used to denote the schema that is associated with your DB2 user name. 単純なデフォルトの DB2 インストール環境である場合、これはデータベーススキーマ名となります。

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

## AEM Forms データベースでの reorg コマンドの実行 {#run-the-reorg-command-on-your-aem-forms-database}

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

