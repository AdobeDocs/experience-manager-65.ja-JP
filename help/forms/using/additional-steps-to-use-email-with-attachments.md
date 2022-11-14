---
title: 添付ファイル付きの電子メールを取得するための追加手順
description: 添付ファイル付きの電子メールを取得するための追加手順
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# JEE 上のAEM Formsプラットフォームの添付ファイルを含む電子メールを取得できない{#unable-to-get-email-with-attachments}

この問題は、次のバージョンに適用されます。
* Experience Manager6.5 Forms

## 問題 {#issue}

ユーザーは、「電子メールでPDFを送信」や「送信時に添付ファイルを含める」などの設定を実行できません。

## ソリューション {#solution}

1. jar を次の形式でダウンロード [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) を開き、ダウンロードした jar ファイルを解凍してマニフェストファイルを取得します。

1. のマニフェストファイルを使用 `java.mail-1.0.jar` 手順 1 から取得し、次のような新しいカスタム jar ファイルを作成しました。 `java.mail-1.5.jar`.

1. マニフェストファイルを開き、 `1.5.0` と `1.5.6` および `Bundle-Version: 1.0` と `Bundle-Version:1.5`

1. 新しいカスタム jar の作成 (`java.mail-1.5.jar`) ファイルを `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 次のフォルダー：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   上記のコマンドで、 *manifest.mf* はマニフェストファイルの名前で、 *java.mail-1.5.jar* は、上記のコマンドを実行した後に作成されるファイルの名前です。

1. ダウンロード [javax-mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. に移動します。 `http://<server name>:<port>/lc/system/console/bundles`という名前のバンドルを削除します。 `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. インストール `java.mail-1.5.jar` 手順 3 から取得します。  この手順を実行すると、JEE デプロイメントの Sling プロパティが再起動します。 次の場所にインストールされたバンドルを待ちます： `http://<server name>:<port>/lc/system/console/bundles` ステータスを次の形式で表示するには **アクティブ**.

   >注意：の場合、ステータスは **InActive**，再起動   **JBoss** から **サービスコンソール**.


1. インストール `javax.mail-1.5.6.redhat-1.jar`手順 5 でダウンロードしたファイル

1. 停止 **JBoss** から **サービスコンソール** 次のプロパティをに追加します。 **Sling.properties** ファイル：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 再起動 **JBoss**.
