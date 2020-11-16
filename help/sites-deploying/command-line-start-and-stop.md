---
title: コマンドラインによる起動と停止
seo-title: コマンドラインによる起動と停止
description: コマンドラインから AEM の起動と停止をおこなう方法を学習します。
seo-description: コマンドラインから AEM の起動と停止をおこなう方法を学習します。
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
translation-type: tm+mt
source-git-commit: 3f53945579eaf5de1ed0b071aa9cce30dded89f1
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 78%

---


# コマンドラインによる起動と停止{#command-line-start-and-stop}

## コマンドラインからの Adobe Experience Manager の起動 {#starting-adobe-experience-manager-from-the-command-line}

この `start` スクリプトは&lt;cq-installation>/bin *ディレクトリ* にあります。 Unix版とWindows版の両方が提供されます。 スクリプトでは、 *&lt;cq-installation>ディレクトリにインストールされたインスタンスを開始し* ます。

これらの2つのバージョンは、AEMインスタンスの開始と調整に使用できる環境変数のリストをサポートしています。

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
   <td>このサーバーがリッスンするインターフェイス<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>実行モードをコンマで区切って指定<br /> </td>
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
>author や publish など、一部の実行モードは、AEM を最初に起動する前に設定する必要があり、後から変更することはできません。実稼動環境で使用する予定の AEM インスタンスを設定する前に、[実行モードのドキュメント](/help/sites-deploying/configure-runmodes.md)で詳細を参照してください。

### Windows プラットフォームの start.bat スクリプトの例 {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Unix プラットフォームの start スクリプトの例 {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>start スクリプトは、*&lt;cq-installation>/app* フォルダーの下にインストールされている AEM Quickstart を起動します。

## Adobe Experience Manager の停止 {#stopping-adobe-experience-manager}

AEM を停止するには、次のいずれかを実行します。

* 使用しているプラットフォームに応じて、

   * スクリプトまたはコマンドラインから AEM を起動した場合は、**Ctrl+C**&#x200B;キーを押してサーバーをシャットダウンします。
   * UNIX で start スクリプトを使用した場合は、stop スクリプトを使用して AEM を停止する必要があります。

* jar ファイルをダブルクリックして AEM を起動した場合は、起動ウィンドウで「**オン**」ボタンをクリックして（ボタンが「**オフ**」に変化します）サーバーをシャットダウンします。

   ![chlimage_1-63](assets/chlimage_1-63.png)

## コマンドラインからの Adobe Experience Manager の停止 {#stopping-adobe-experience-manager-from-the-command-line}

この `stop` スクリプトは&lt;cq-installation>/bin *ディレクトリ* にあります。 Unix版とWindows版の両方が提供されます。 このスクリプトは、 *&lt;cq-installation>ディレクトリにインストールされた実行中のインスタンスを停止します* 。

### Unix プラットフォームの stop スクリプトの例 {#unix-platform-stop-script-example}

```shell
./stop
```

### Windows プラットフォームの stop.bat スクリプトの例 {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

リポジトリを事前設定するだけ（場所の変更なし）の場合に必要なのは次の手順だけです。

* extract `repository.xml` to the required location

* update `repository.xml` as required

* 作成 `bootstrap.properties` し定義する `repository.config`

これも、実際のインストールを開始する前におこないます。

