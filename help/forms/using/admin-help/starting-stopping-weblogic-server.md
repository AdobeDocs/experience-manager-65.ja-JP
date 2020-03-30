---
title: WebLogic Server の起動と停止
seo-title: WebLogic Server の起動と停止
description: 一部の手順では、AEM forms モジュールをデプロイする WebLogic Server のインスタンスを起動または停止する必要があります。このドキュメントでは、WebLogic Server の開始方法と停止方法を説明します。
seo-description: 一部の手順では、AEM forms モジュールをデプロイする WebLogic Server のインスタンスを起動または停止する必要があります。このドキュメントでは、WebLogic Server の開始方法と停止方法を説明します。
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# WebLogic Server の起動と停止 {#starting-and-stopping-weblogic-server}

一部の手順では、AEM Forms モジュールをデプロイする WebLogic Server のインスタンスを起動または停止する必要があります。実行するタスクに応じて、WebLogic Server が停止しているか、実行中であるかを確認します。

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
>If you are running WebLogic Server on Red Hat® Enterprise Linux Advanced Server 4.0, set the `LD_ASSUME_KERNEL` environment variable to 2.4.19 by using the `export LD_ASSUME_KERNEL=2.4.19` command. さらに、この環境変数を設定したシェルと同じシェルから WebLogic Server を実行します。

## WebLogic Server の起動 {#start-weblogic-server}

1. From a command prompt, go to *[appserver root]*/user_projects/domains/*[appserverdomain]*.
1. 以下のコマンドを入力します。

   * (Windows) `startWebLogic.cmd`
   * (Linux、UNIX) ./ `startWebLogic.sh`

## WebLogic Server の停止 {#stop-weblogic-server}

1. Start WebLogic Server administration console by typing `https://[host name]:7001/console` in the URL line of a web browser.
1. この WebLogic 設定の作成時に使用したユーザー名とパスワードを入力して、「Log In」をクリックし、ログインします。
1. 「Change Center」で、「Lock &amp; Edit」をクリックします。
1. 「Domain Structure」で、Environment／Servers をクリックします。
1. 「AdminServer」をクリックして、Settings for AdminServer ウィンドウの「Control」タブをクリックします。
1. Server Status テーブルで AdminServer が選択されていることを確認して、「Shutdown」をクリックします。
1. 実行中のタスクが完了してから停止する場合は「When Work Completes」、完了を待たずに直ちに停止する場合は「Force Shutdown Now」を選択します。
1. Server Life Cycle Assistant ウィンドウで、「Yes」をクリックして停止を実行します。

停止すると、WebLogic Server 管理コンソールは使用できなくなり、start コマンドを実行したコマンドプロンプトが使用できるようになります。

## WebLogic 管理コンソールの起動 {#start-weblogic-administration-console}

1. If WebLogic Admin Server is not already running, from a command prompt, go to the *[appserver root]\user_projects\domains\[domainname]*directory, and enter the following command:

   * (Windows) `startWebLogic.cmd`
   * (Linux、UNIX) ./ `startWebLogic.sh`

1. Access WebLogic Server administration console by typing `https://[host name]:[port]/console` in the URL line of a web browser, where *[port]* is the non-secure listening port. デフォルトでは、このポート番号は 7001 です。
1. ログイン画面で、管理者のユーザー名とパスワードを入力して「Log In」をクリックします。

## Node Manager の起動 {#start-node-manager}

1. WebLogic Server が実行中であることを確認します。
1. From a new command prompt, go to *[appserver root]*/server/bin.
1. 以下のコマンドを入力します。

   * (Windows) `startNodeManager.cmd`
   * (Linux、UNIX) `./startNodeManager.sh`

## Node Manager の停止 {#stop-node-manager}

WebLogic Server を停止した後、Node Manager を呼び出したコマンドプロンプトを閉じることができます。

## WebLogic 管理対象サーバーの起動 {#start-a-weblogic-managed-server}

>[!NOTE]
>
>WebLogic 管理対象サーバーの起動は、WebLogic ドメインと管理対象サーバーを作成した後にのみ実行できます。

1. WebLogic Server と Node Manager が実行されていることを確認します。
1. Start WebLogic Server administration console by typing `https://host name]:[port]`/console` in the URL line of a web browser.
1. 「Domain Structure」で、Environment／Servers をクリックします。
1. 右側のウィンドウで、「Control」タブをクリックします。
1. 起動する管理対象サーバーを選択します。
1. 起動する管理対象サーバーの下にある「Start」ボタンをクリックします。

## WebLogic 管理対象サーバーの停止 {#stop-a-weblogic-managed-server}

1. Start WebLogic Server administration console by typing `https://`*[host name]:[port ]*`/console`in the URL line of a web browser.
1. 「Domain Structure」で、Environment／Servers をクリックします。
1. 右側のウィンドウで、「Control」タブをクリックします。
1. 停止する管理対象サーバーを選択します。
1. 停止する管理対象サーバーの下にある「Shutdown」ボタンをクリックします。
1. 実行中のタスクが完了してから停止する場合は「When Work Completes」、完了を待たずに直ちに停止する場合は「Force Shutdown Now」を選択します。
1. Server Life Cycle Assistant ウィンドウで、「Yes」をクリックして停止を実行します。

