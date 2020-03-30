---
title: ログファイル
seo-title: ログファイル
description: 実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録され、そのログファイルは任意のテキストエディターで開くことができます。
seo-description: 実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録され、そのログファイルは任意のテキストエディターで開くことができます。
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# ログファイル {#log-files}

実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録されます。アプリケーションサーバーへのデプロイ中に問題が発生した場合には、ログファイルを参照して問題を見つけることができます。ログファイルは、テキストエディターを使用して開くことができます。

(JBoss) The following log files are located in the `[appserver root]/server/'server'/log` directory:

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic) Domain log files are located in the `[appserverdomain]` directory, and server log files are located in the `[appserverdomain]/servers/[appserver name]/logs` directory:

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) The following log files are located in the `[appserver root]/profiles/default/logs/[appserver name]` directory:

* SystemErr.log
* SystemOut.log
* StartServer.log

