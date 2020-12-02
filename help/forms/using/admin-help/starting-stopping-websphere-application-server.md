---
title: WebSphere Application Server の起動と停止
seo-title: WebSphere Application Server の起動と停止
description: 一部の手順では、AEM forms 製品をデプロイする WebSphere のインスタンスを停止または起動する必要があります。ここでは、WebSphere Application Server の起動および停止方法について説明します。
seo-description: 一部の手順では、AEM forms 製品をデプロイする WebSphere のインスタンスを停止または起動する必要があります。ここでは、WebSphere Application Server の起動および停止方法について説明します。
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 82%

---


# WebSphere Application Server の起動と停止 {#starting-and-stopping-websphere-application-server}

一部の手順では、AEM Forms 製品をデプロイする WebSphere のインスタンスを停止または起動する必要があります。アプリケーションサーバーが起動しているかどうかわからない場合は、まず WebSphere Application Server のステータスを表示します。

## WebSphere Application Server のステータスの表示  {#view-the-status-of-websphere-application-server}

1. コマンドプロンプトで`[appserver root]/bin`ディレクトリに移動します。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * (Windows)`serverStatus.bat`*server_name*
   * （Linux、UNIX）/ `serverStatus.sh`*server_name*

## WebSphere Application Server の起動 {#start-websphere-application-server}

1. コマンドプロンプトで`[appserver root]/bin`ディレクトリに移動します。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * (Windows)`startServer.bat`*server_name*
   * （Linux、UNIX）/ `startServer.sh`*server_name*

## WebSphere Application Server の停止 {#stop-websphere-application-server}

1. コマンドプロンプトで`[appserver root]/bin`ディレクトリに移動します。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * (Windows)`stopServer.bat`*server_name*
   * （Linux、UNIX）/ `stopServer.sh`*server_name*

