---
title: ログファイル
description: 実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録され、そのログファイルは任意のテキストエディターで開くことができます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 25%

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
