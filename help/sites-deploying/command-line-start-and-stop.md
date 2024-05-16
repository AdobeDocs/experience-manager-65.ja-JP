---
title: コマンドラインによる起動と停止
description: コマンドラインから Adobe Experience Manager の起動と停止を行う方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: ht
source-wordcount: '352'
ht-degree: 100%

---

# コマンドラインによる起動と停止{#command-line-start-and-stop}

## コマンドラインからの Adobe Experience Manager の起動 {#starting-adobe-experience-manager-from-the-command-line}

`start` スクリプトは、*&lt;cq-installation>/bin* ディレクトリの下で使用できます。UNIX® 版と Windows 版の両方が用意されています。スクリプトは、*&lt;cq-installation>* ディレクトリにインストールされているインスタンスを開始します。

これら 2 つのバージョンは、Adobe Experience Manager（AEM）インスタンスの開始や調整に使用できる、環境変数のリストをサポートしています。

<table>
 <tbody>
  <tr>
   <td><strong>環境変数 </strong></td>
   <td><strong>説明 </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>停止およびステータススクリプトに使用する TCP ポート<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>ホスト名<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>このサーバーがリッスンする必要があるインターフェイス<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>コンマで区切られた実行モード<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>jar ファイルの名前<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>JAAS の使用（true の場合）<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>JAAS 設定のパス<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>デフォルトの JVM オプション<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>オーサーやパブリッシュなどの一部の実行モードは、最初に AEM を起動する前に設定する必要があり、後で変更することはできません。実稼動環境で使用する AEM インスタンスを設定する前に、[実行モードのドキュメント](/help/sites-deploying/configure-runmodes.md)を参照してください。

### Windows プラットフォームの start.bat スクリプトの例 {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### UNIX® プラットフォームの start スクリプトの例 {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>start スクリプトは、*&lt;cq-installation>/app* フォルダーの下にインストールされている AEM Quickstart を起動します。

## Adobe Experience Manager の停止 {#stopping-adobe-experience-manager}

AEM を停止するには、次のいずれかを実行します。

* 使用するプラットフォームに応じて：

   * スクリプトまたはコマンドラインから AEM を起動した場合は、**Ctrl+C**&#x200B;キーを押してサーバーをシャットダウンします。
   * UNIX® で start スクリプトを使用した場合は、stop スクリプトを使用して AEM を停止する必要があります。

* jar ファイルをダブルクリックして AEM を起動した場合は、起動ウィンドウで「**オン**」ボタンをクリックして（ボタンが「**オフ**」に変化します）サーバーをシャットダウンします。

  ![chlimage_1-63](assets/chlimage_1-63.png)

## コマンドラインからの Adobe Experience Manager の停止 {#stopping-adobe-experience-manager-from-the-command-line}

`stop` スクリプトは、*&lt;cq-installation>/bin* ディレクトリの下で使用できます。UNIX® 版と Windows 版の両方が用意されています。スクリプトは、*&lt;cq-installation>* ディレクトリにインストールされている実行中のインスタンスを停止します。

### UNIX® プラットフォームの stop スクリプトの例 {#unix-platform-stop-script-example}

```shell
./stop
```

### Windows プラットフォームの stop.bat スクリプトの例 {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

リポジトリを事前設定するだけ（場所の変更なし）の場合に必要なのは次の手順だけです。

* `repository.xml` を目的の場所に抽出する

* 必要に応じて `repository.xml` を更新する

* `bootstrap.properties` を作成し `repository.config` を定義する

これも、実際のインストールを開始する前におこないます。
