---
title: ログの使用
seo-title: Working with Logs
description: ログを使用して AEM をトラブルシューティングする方法について説明します。
seo-description: Learn how to troubleshoot AEM by working with logs.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 100%

---

# ログの使用{#working-with-logs}

ここでは、トラブルシューティングに役立つログの詳細情報を示します。

CRX では詳細なログを記録します。クイックスタートを解凍して起動すると、次の場所にログが見つかります。

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## デバッグログレベルのアクティベート {#activating-the-debug-log-level}

デフォルトのログレベルは情報（INFO）であるため、デバッグ（DEBUG）メッセージはログに記録されません。

デバッグログレベルをアクティベートするには、CRX Explorer を使用して次のプロパティを設定します。

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

このプロパティを debug に設定してください。多くのログが生成されるので、デバッグログレベルのログを不必要に長く残さないでください。

デバッグファイルの行は、通常は DEBUG で始まり、その後にログレベル、インストーラーのアクション、ログメッセージが示されます。次に例を示します。

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

ログレベルは次のとおりです。

| 0 | 重大なエラー | アクションが失敗し、インストーラーの処理を続行できません。 |
|---|---|---|
| 1 | エラー | アクションが失敗しました。インストールは続行しますが、CRX の一部が正常にインストールされなかったので、機能しません。 |
| 2 | 警告 | アクションは成功しましたが、問題が発生しました。CRX が正常に機能するかどうかは不明です。 |
| 3 | 情報 | アクションが成功しました。 |

## トラブルシューティングに使用する verbose オプション {#verbose-option-used-for-troubleshooting}

CRX の起動時には、次に示すように、–v（verbose）オプションをコマンドラインに追加できます。

` java -jar crx-<*version*>-<*edition*>.jar -v`

verbose オプションでは quickstart のログ出力の一部がコンソールに表示されるので、このオプションをトラブルシューティングに使用してください。
