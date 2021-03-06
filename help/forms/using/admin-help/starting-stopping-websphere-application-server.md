---
title: WebSphere Application Server の起動と停止
seo-title: Starting and stopping WebSphere Application Server
description: 一部の手順では、AEM forms 製品をデプロイする WebSphere のインスタンスを停止または起動する必要があります。ここでは、WebSphere Application Server の起動および停止方法について説明します。
seo-description: Several procedures require you to stop or start the instance of WebSphere where you want to deploy AEM forms products. This document describes how to start and stop the WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '189'
ht-degree: 100%

---

# WebSphere Application Server の起動と停止 {#starting-and-stopping-websphere-application-server}

一部の手順では、AEM forms 製品をデプロイする WebSphere のインスタンスを停止または起動する必要があります。アプリケーションサーバーが起動しているかどうかわからない場合は、まず WebSphere Application Server のステータスを表示します。

## WebSphere Application Server のステータスの表示 {#view-the-status-of-websphere-application-server}

1. コマンドプロンプトで、`[appserver root]/bin`ディレクトリに移動します。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * （Windows）`serverStatus.bat`*server_name*
   * （Linux、UNIX）/ `serverStatus.sh`*server_name*

## WebSphere Application Server の起動 {#start-websphere-application-server}

1. コマンドプロンプトで、`[appserver root]/bin`ディレクトリに移動します。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * （Windows）`startServer.bat`*server_name*
   * （Linux、UNIX）/ `startServer.sh`*server_name*

## WebSphere Application Server の停止 {#stop-websphere-application-server}

1. コマンドプロンプトで、`[appserver root]/bin`ディレクトリに移動します。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * （Windows）`stopServer.bat`*server_name*
   * （Linux、UNIX）/ `stopServer.sh`*server_name*
