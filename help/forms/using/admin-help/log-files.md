---
title: ログファイル
seo-title: Log files
description: 実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録され、そのログファイルは任意のテキストエディターで開くことができます。
seo-description: Events such as run-time or startup errors are recorded to the application server log files, which can be  opened using any text editor.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 26%

---

# ログファイル {#log-files}

実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録されます。 アプリケーションサーバーへのデプロイ中に問題が発生した場合は、ログファイルを使用して問題を見つけることができます。 ログファイルは、任意のテキストエディターを使用して開くことができます。

(JBoss) 次のログファイルが `[appserver root]/server/'server'/log` ディレクトリ：

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic) ドメインログファイルは、 `[appserverdomain]` ディレクトリとサーバ・ログ・ファイルが `[appserverdomain]/servers/[appserver name]/logs` ディレクトリ：

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) 次のログファイルが `[appserver root]/profiles/default/logs/[appserver name]` ディレクトリ：

* SystemErr.log
* SystemOut.log
* StartServer.log
