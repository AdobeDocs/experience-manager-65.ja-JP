---
title: ログの使用
seo-title: Working with Logs
description: ログを操作してAEMのトラブルシューティングをおこなう方法を説明します。
seo-description: Learn how to troubleshoot AEM by working with logs.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 64%

---

# ログの使用{#working-with-logs}

この節では、トラブルシューティングに役立つログに関する詳細情報を示します。

>[!NOTE]
>
>ログについて詳しくは、以下を参照してください。
>
>* [AEM での監査ログのメンテナンス](/help/sites-administering/operations-audit-log.md)
>* [監査記録とログファイルの操作](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)

CRX は詳細なログを記録します。 クイックスタートを解凍して起動すると、次の場所にログが表示されます。

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## デバッグログレベルのアクティベート {#activating-the-debug-log-level}

デフォルトのログレベルは情報（INFO）であるため、デバッグ（DEBUG）メッセージはログに記録されません。

DEBUG ログレベルをアクティブにするには、CRX Explorer を使用して、

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

このプロパティを debug に設定してください。多数のログが生成されるので、デバッグログレベルのログを必要以上に長く残さないでください。

デバッグファイルの行は、通常は DEBUG で始まり、その後にログレベル、インストーラーのアクション、ログメッセージが示されます。次に例を示します。

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

ログレベルは次のとおりです。

| 0 | 重大なエラー | アクションが失敗し、インストーラーの処理を続行できません。 |
|---|---|---|
| 1 | エラー | アクションが失敗しました。インストールは続行しますが、CRX の一部が正常にインストールされなかったので、機能しません。 |
| 2 | 警告 | アクションは成功しましたが、問題が発生しました。CRX は正常に機能する場合と機能しない場合があります。 |
| 3 | 情報 | アクションが成功しました。 |

## トラブルシューティングに使用する詳細オプション {#verbose-option-used-for-troubleshooting}

CRX の起動時には、次に示すように、–v（verbose）オプションをコマンドラインに追加できます。

` java -jar crx-<*version*>-<*edition*>.jar -v`

verbose オプションでは quickstart のログ出力の一部がコンソールに表示されるので、このオプションをトラブルシューティングに使用してください。
