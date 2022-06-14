---
title: WebLogic Server の起動と停止
seo-title: Starting and stopping WebLogic Server
description: 一部の手順では、AEM forms モジュールをデプロイする WebLogic Server のインスタンスを起動または停止する必要があります。このドキュメントでは、WebLogic Server の開始方法と停止方法を説明します。
seo-description: Several procedures require you to start or stop the instance of WebLogic Server where you want to deploy AEM forms modules. This document describes how to start and stop the WebLogic Server.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 100%

---


# WebLogic Server の起動と停止 {#starting-and-stopping-weblogic-server}

一部の手順では、AEM forms モジュールをデプロイする WebLogic Server のインスタンスを起動または停止する必要があります。実行するタスクに応じて、WebLogic Server が停止しているか、実行中であるかを確認します。

<table>
 <thead>
  <tr>
   <th><p>アクティビティ</p></th>
   <th><p>WebLogic の状態</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>WebLogic ドメインの作成</p></td>
   <td><p>[Stopped]</p></td>
  </tr>
  <tr>
   <td><p>WebLogic 管理対象サーバーの作成</p></td>
   <td><p>[Running]</p></td>
  </tr>
  <tr>
   <td><p>サーバースレッド数の増加</p></td>
   <td><p>[Running]</p></td>
  </tr>
  <tr>
   <td><p>AEM Forms 製品のデプロイ</p></td>
   <td><p>[Running]</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Red Hat® Enterprise Linux Advanced Server 4.0 で WebLogic Server を実行している場合は、`export LD_ASSUME_KERNEL=2.4.19` コマンドを使用して、`LD_ASSUME_KERNEL` 環境変数を 2.4.19 に設定します。さらに、この環境変数を設定したシェルと同じシェルから WebLogic Server を実行します。

## WebLogic Server の起動 {#start-weblogic-server}

1. コマンドプロンプトで *[appserver root]*/user_projects/domains/*[appserverdomain]* に移動します。
1. 以下のコマンドを入力します。

   * （Windows）`startWebLogic.cmd`
   * （Linux、UNIX）./ `startWebLogic.sh`

## WebLogic Server の停止 {#stop-weblogic-server}

1. Web ブラウザーの URL 行に `https://[host name]:7001/console` と入力して、WebLogic Server 管理コンソールを起動します。
1. この WebLogic 設定の作成時に使用したユーザー名とパスワードを入力して、「Log In」をクリックし、ログインします。
1. Change Center で、「Lock &amp; Edit」をクリックします。
1. 「Domain Structure」で、Environment／Servers をクリックします。
1. 「AdminServer」をクリックして、Settings for AdminServer ウィンドウの「Control」タブをクリックします。
1. Server Status テーブルで AdminServer が選択されていることを確認して、「Shutdown」をクリックします。
1. 実行中のタスクが完了してから停止する場合は「When Work Completes」、完了を待たずに直ちに停止する場合は「Force Shutdown Now」を選択します。
1. Server Life Cycle Assistant ウィンドウで、「Yes」をクリックして停止を実行します。

停止すると、WebLogic Server 管理コンソールは使用できなくなり、start コマンドを実行したコマンドプロンプトが使用できるようになります。

## WebLogic 管理コンソールの起動 {#start-weblogic-administration-console}

1. WebLogic 管理サーバーがまだ実行されていない場合は、コマンドプロンプトで *[appserver root]\user_projects\domains\[domainname]* ディレクトリに移動し、次のコマンドを入力します。

   * （Windows）`startWebLogic.cmd`
   * （Linux、UNIX）./ `startWebLogic.sh`

1. Web ブラウザーの URL 行に `https://[host name]:[port]/console`（ *[port]* は安全ではないリスニングポート）と入力して、WebLogic Server 管理コンソールにアクセスします。デフォルトでは、このポート番号は 7001 です。
1. ログイン画面で、管理者のユーザー名とパスワードを入力して「Log In」をクリックします。

## Node Manager の起動 {#start-node-manager}

1. WebLogic Server が実行中であることを確認します。
1. 新たに起動したコマンドプロンプトで *[appserver root]*/server/bin に移動します。
1. 以下のコマンドを入力します。

   * （Windows）`startNodeManager.cmd`
   * （Linux、UNIX）`./startNodeManager.sh`

## Node Manager の停止 {#stop-node-manager}

WebLogic Server を停止した後、Node Manager を呼び出したコマンドプロンプトを閉じることができます。

## WebLogic 管理対象サーバーの起動 {#start-a-weblogic-managed-server}

>[!NOTE]
>
>WebLogic 管理対象サーバーの起動は、WebLogic ドメインと管理対象サーバーを作成した後にのみ実行できます。

1. WebLogic Server と Node Manager が実行されていることを確認します。
1. Web ブラウザーの URL 行に `https://host name]:[port]/console` と入力して、WebLogic Server 管理コンソールを起動します。
1. 「Domain Structure」で、Environment／Servers をクリックします。
1. 右側のウィンドウで、「Control」タブをクリックします。
1. 起動する管理対象サーバーを選択します。
1. 起動する管理対象サーバーの下にある「Start」ボタンをクリックします。

## WebLogic 管理対象サーバーの停止 {#stop-a-weblogic-managed-server}

1. Web ブラウザーの URL 行に `https://`*[host name]:[port ]*`/console` と入力して、WebLogic Server 管理コンソールを起動します。
1. 「Domain Structure」で、Environment／Servers をクリックします。
1. 右側のウィンドウで、「Control」タブをクリックします。
1. 停止する管理対象サーバーを選択します。
1. 停止する管理対象サーバーの下にある「Shutdown」ボタンをクリックします。
1. 実行中のタスクが完了してから停止する場合は「When Work Completes」、完了を待たずに直ちに停止する場合は「Force Shutdown Now」を選択します。
1. Server Life Cycle Assistant ウィンドウで、「Yes」をクリックして停止を実行します。

