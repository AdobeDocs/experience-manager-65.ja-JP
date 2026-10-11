---
title: バージョンのパージ
description: この記事では、バージョンのパージで使用できるオプションについて説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
solution: Experience Manager, Experience Manager Sites
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 76%
---
# バージョンのパージ{#version-purging}

標準インストールの場合、コンテンツの更新後にページをアクティベートすると、Adobe Experience Manager（AEM）によってページまたはノードのバージョンが作成されます。

>[!NOTE]
>
>コンテンツが変更されない場合は、ページがアクティベート済みで、新しいバージョンが作成されないことを示すメッセージが表示されます。

サイドキックの「**バージョン管理**」タブを使用すると、リクエストに応じて追加のバージョンを作成できます。 これらのバージョンはリポジトリに格納され、必要に応じて復元できます。

これらのバージョンはパージされることがなく、時間の経過と共にリポジトリーのサイズが大きくなるので、管理が必要です。

AEM には、リポジトリの管理に役立つ様々なメカニズムが備わっています。

* バージョン マネージャー[](#version-manager)
これは、新しいバージョンが作成されたときに古いバージョンをパージするように設定できます。

* [ バージョンのパージ ](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) ツール
これは、リポジトリの監視とメンテナンスの一部として使用されます。
このツールを使用すると、次のパラメーターに従って、ノードまたはノード階層の古いバージョンを削除できます。

  * リポジトリに保持されるバージョンの最大数。
    この数値を超えると、最も古いバージョンが削除されます。

  * リポジトリ内に保持されているバージョンの最大有効期間。
    バージョンの年齢がこの値を超えると、リポジトリからパージされます。

* [バージョンパージのメンテナンスタスク](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks)。 バージョンのパージメンテナンスタスクをスケジュールして、古いバージョンを自動的に削除できます。 これにより、バージョンのパージツールを手動で実行する必要性を最小限に抑えることができます。

>[!CAUTION]
>
>リポジトリサイズを最適化するには、バージョンのパージタスクを頻繁に実行します。 トラフィック量が限られている場合は、このタスクを営業時間外にスケジュールする必要があります。

## バージョンマネージャー {#version-manager}

パージツールを使用した明示的なパージに加えて、新しいバージョンの作成時に古いバージョンをパージするようにバージョンマネージャーを構成できます。

バージョンマネージャーを設定するには、次の[設定を作成](/help/sites-deploying/configuring-osgi.md)します。

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

以下のオプションが利用できます。

* `versionmanager.createVersionOnActivation` （ブール値、デフォルト：true）
ページがアクティブ化されたときにバージョンを作成するかどうかを指定します。
レプリケーションエージェントがバージョンの作成を抑制するように設定されている場合を除き、バージョンが作成されます。この設定はバージョンマネージャーでも尊重されます。
アクティベーションが `versionmanager.ivPaths` に含まれているパスで行われた場合にのみバージョンが作成されます（以下を参照）。

* `versionmanager.ivPaths` （String[]、既定値：`{"/"}`）
`versionmanager.createVersionOnActivation`がtrueに設定されている場合に、ライセンス認証時に暗黙的に作成されるバージョンのパスを指定します。

* `versionmanager.purgingEnabled` （ブール値、デフォルト：false）
新しいバージョンの作成時にパージを有効にするかどうかを定義します。

* `versionmanager.purgePaths` （文字列[]、デフォルト：{&quot;/content&quot;}）
新しいバージョンの作成時にバージョンをパージするパスを指定します。

* `versionmanager.maxAgeDays` （int、デフォルト：30）
バージョンのパージ時に、設定された値より古いバージョンが削除されます。 この値が 1 未満の場合、バージョンの経過日数に基づくパージは実行されません。

* `versionmanager.maxNumberVersions` （int、デフォルト 5）
バージョンのパージ時に、n番目の新しいバージョンより古いバージョンが削除されます。 この値が 1 未満の場合、バージョンの数に基づいたパージは実行されません。

* `versionmanager.minNumberVersions` （int、デフォルト 0）
期間にかかわらず保持されるバージョンの最小数。 この値を 1 未満に設定すると、保持するバージョン数の最小数は設定されません。

>[!NOTE]
>
>リポジトリに多数のバージョンを保存することはお勧めできません。 そのため、バージョンのパージ操作を設定する際は、パージ対象から多くのバージョンを除外しすぎないでください。そうしないと、リポジトリサイズが適切に最適化されません。 業務上の要件で多数のバージョンを保持する場合は、アドビサポートに連絡して、リポジトリサイズを最適化する代替方法をご相談ください。

### 保持オプションの組み合わせ {#combining-retention-options}

どのバージョンを保持するかを定義するオプション（`maxAgeDays`、`maxNumberVersions`、`minNumberVersions`）は、要件に応じて組み合わせることができます。

例えば、保持するバージョンの最大数と保持する最も古いバージョンを組み合わせて定義する場合は、次のようになります。

* 設定:

  * `maxNumberVersions` = 7

  * `maxAgeDays` = 30

* シナリオは以下の通りです。

  * 過去 60 日以内に 10 個のバージョンが作成されました。
  * そのうちの 3 個が過去 30 日以内に作成されました。

* 結果は次の通りです。

  * 最新の 3 個のバージョンが保持されます。

例えば、保持するバージョン数の最大数と最小数、および保持する最も古いバージョンを組み合わせて定義する場合は、次のようになります。

* 設定:

  * `maxNumberVersions` = 3
  * `maxAgeDays` = 30
  * `minNumberVersions` = 3

* シナリオは以下の通りです。

  * 60 日前に 5 個のバージョンが作成されました。

* 結果は次の通りです。

  * 3 個のバージョンが保持されます。

## バージョンのパージツール {#purge-versions-tool}

[バージョンのパージ](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)ツールを使用すると、リポジトリ内のノードまたはノードの階層のバージョンをパージすることができます。 このツールの主な目的は、ノードの古いバージョンを削除してリポジトリのサイズを縮小することです。
