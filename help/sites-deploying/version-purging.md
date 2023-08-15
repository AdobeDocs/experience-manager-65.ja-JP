---
title: バージョンのパージ
seo-title: Version Purging
description: この記事では、バージョンのパージに使用できるオプションについて説明します。
seo-description: This article describes the available options for version purging.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 55%

---

# バージョンのパージ{#version-purging}

標準インストールでは、コンテンツの更新後にページをアクティベートすると、AEMはページまたはノードの新しいバージョンを作成します。

>[!NOTE]
>
>コンテンツを変更しない場合は、ページがアクティベートされたが新しいバージョンは作成されないことを示すメッセージが表示されます

リクエストに応じて、 **バージョン管理** サイドキックのタブ。 これらのバージョンはリポジトリに保存され、必要に応じて復元できます。

これらのバージョンはパージされないので、リポジトリのサイズは時間の経過と共に大きくなるので、管理する必要があります。

AEMには、リポジトリの管理に役立つ様々なメカニズムが付属しています。

* [バージョンマネージャー](#version-manager)
新しいバージョンが作成されると古いバージョンをパージするように設定できます。

* の [バージョンをパージ](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) ツールこれは、リポジトリの監視および保守の一環として使用されます。
これにより、次のパラメーターに従って、ノードの古いバージョンまたはノードの階層を削除するように介入できます。

   * リポジトリに保持するバージョンの最大数
この数値を超えると、最も古いバージョンが削除されます。

   * リポジトリに保持するバージョンの期間の最大値
バージョンの期間がこの値を超えると、リポジトリからパージされます。

* [バージョンパージのメンテナンスタスク](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks)。バージョンのパージメンテナンスタスクをスケジュールして、古いバージョンを自動的に削除できます。これにより、バージョンのパージツールを手動で実行する必要性を最小限に抑えることができます。

>[!CAUTION]
>
>リポジトリサイズを最適化するには、バージョンパージタスクを頻繁に実行する必要があります。 トラフィック量が限られている場合は、このタスクを営業時間外にスケジュールする必要があります。

## バージョンマネージャー {#version-manager}

パージツールを使用した明示的なパージに加えて、バージョンマネージャーでは、新しいバージョンが作成されたときに古いバージョンをパージするように設定できます。

バージョンマネージャーを設定するには、次の[設定を作成](/help/sites-deploying/configuring-osgi.md)します。

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

以下のオプションが利用できます。

* `versionmanager.createVersionOnActivation`（ブール値、デフォルト：true）
ページがアクティベートされた際に、バージョンを作成するかどうかを指定します。
レプリケーションエージェントがバージョンの作成を抑制するように設定されていない限り、バージョンが作成されます。これはバージョンマネージャーで順守されます。
アクティベーションが `versionmanager.ivPaths` に含まれているパスで行われた場合にのみバージョンが作成されます（以下を参照）。

* `versionmanager.ivPaths`（String[]、デフォルト：`{"/"}`）
`versionmanager.createVersionOnActivation` が true の場合に、アクティベーションによりバージョンが暗黙的に作成されるパスを指定します。

* `versionmanager.purgingEnabled`（ブール値、デフォルト：false）
新しいバージョンが作成された際のパージを有効にするかどうかを指定します。

* `versionmanager.purgePaths`（String[]、デフォルト：{&quot;/content&quot;}）
新しいバージョンが作成された際にバージョンをパージするパスを指定します。

* `versionmanager.maxAgeDays`（整数、デフォルト：30）
バージョンパージで、設定した値より古いバージョンが削除されます。この値が 1 未満の場合、バージョンの期間に基づいたパージは実行されません。

* `versionmanager.maxNumberVersions`（整数、デフォルト：5）
バージョンパージで、n 番目に新しいバージョンより古いバージョンが削除されます。この値が 1 未満の場合、バージョンの数に基づいたパージは実行されません。

* `versionmanager.minNumberVersions`（整数、デフォルト：0）
期間にかかわらず保持するバージョン数の最小数。この値を 1 未満の値に設定した場合、保持されるバージョンの最小数はありません。

>[!NOTE]
>
>多数のバージョンをリポジトリに保持することはお勧めしません。 そのため、バージョンのパージ操作を設定する際は、パージから多くのバージョンが除外されないように注意してください。除外しないと、リポジトリのサイズが適切に最適化されません。 業務上の要件で多数のバージョンを保持する場合は、Adobe サポートに連絡して、リポジトリサイズを最適化する代替方法をご相談ください。

### 保持オプションの組み合わせ {#combining-retention-options}

どのバージョンを保持するかを定義するオプション（`maxAgeDays`、`maxNumberVersions`、`minNumberVersions`）は、要件に応じて組み合わせることができます。

例えば、保持するバージョンの最大数と、保持する最も古いバージョンを定義する場合は、次のようになります。

* 設定:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* 次を使用：

   * 過去 60 日以内に作成された 10 個のバージョン
   * 過去 30 日以内に作成されたバージョンのうち 3 つ

* 次のことを意味します。

   * 最新 3 つのバージョンが保持されます

例えば、保持するバージョンの最大数と最小数、および保持する最も古いバージョンを定義する場合は、次のようになります。

* 設定:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 次を使用：

   * 60 日前に作成された 5 つのバージョン

* 次のことを意味します。

   * 3 つのバージョンが保持されます

## バージョンのパージツール {#purge-versions-tool}

[バージョンのパージ](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)ツールを使用すると、リポジトリ内のノードまたはノードの階層のバージョンをパージすることができます。このツールの主な目的は、古いバージョンのノードを削除してリポジトリのサイズを縮小することです。
