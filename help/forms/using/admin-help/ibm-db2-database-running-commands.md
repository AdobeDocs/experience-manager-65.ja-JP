---
title: 「IBM DB2 データベース：定期保守のコマンドの実行」
description: このドキュメントでは、AEM Forms データベースの定期保守で推奨される IBM DB2 コマンドの一覧を示します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '391'
ht-degree: 100%

---

# IBM DB2 データベース：定期保守のコマンドの実行 {#ibm-db-database-running-commands-for-regular-maintenance}

AEM Forms データベースの定期保守には、次の IBM DB2 コマンドが推奨されます。DB2 データベースの保守およびパフォーマンスチューニングについて詳しくは、『*IBM DB2 Administration Guide*』を参照してください。

* **runstats**：このコマンドは、その関連インデックスと共に、データベーステーブルの物理的特性を示す統計データを更新します。AEM Forms により生成される動的 SQL ステートメントは、更新済みのこれらの統計を自動的に使用しますが、データベース内で作成される静的 SQL ステートメントでは、`db2rbind` コマンドも実行する必要があります。
* **db2rbind**：このコマンドは、データベース内のすべてのパッケージを再バインドします。`runstats` ユーティリティの実行後に、このコマンドを使用してデータベース内のすべてのパッケージを再検証します。
* **reorg table or index：**&#x200B;このコマンドは、一部のテーブルおよびインデックスの再編成が必要かどうかを確認します。

  データベースの増大および変化に伴い、テーブル統計データの再計算はデータベースパフォーマンスの向上に不可欠なものであり、定期的に実行する必要があります。これらのコマンドは、スクリプトを使用して手動で実行または cron ジョブを使用して実行できます。

>[!NOTE]
>
>`runstats` コマンドを実行する前に、データベースにデータが含まれており、少なくとも 1 つのディレクトリの同期処理が実行されていることが必要です。

小規模なデータベースでは（1 万件のユーザーまたは 2,500 件のグループなど）、`runstats` コマンドを実行して同期タイミングを削減すれば十分です。

大規模なデータベースでは（10 万件のユーザーまたは 1 万件のグループなど）、`runstats` コマンドの実行前に、`reorg` コマンドを実行します。

## AEM Forms データベースでの runstats コマンドの使用 {#use-the-runstats-command-on-your-aem-forms-database}

以下の AEM Forms データベーステーブルおよびインデックスで `runstats` コマンドを実行します。

>[!NOTE]
>
>`runstats` コマンドは、最初のデータベース同期中にのみ実行する必要があります。ただし、プロセス中に 2 回（ユーザーとグループの同期中に 1 回、グループメンバーの同期中に 1 回）実行する必要があります。スクリプトを実行するたびに、実行が正常に完了したことを確認します。

正しい構文と使用法について詳しくは、データベース製造元のドキュメントを参照してください。以下では、`<schema>` を使って、DB2 ユーザー名に関連付けられたスキーマを示します。単純なデフォルトの DB2 インストールの場合、これはデータベーススキーマ名となります。

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
