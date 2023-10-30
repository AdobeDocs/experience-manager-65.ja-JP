---
title: 添付ファイル付きのメールを受信するための追加手順
description: JEE 上のAEM Formsプラットフォームの添付ファイルを含む電子メールを取得できない場合のエラーを修正します。
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
source-git-commit: 20b0d0db54dc30285c056a10032f02ba45f8baca
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 67%

---

# AEM Forms on JEE プラットフォームで添付ファイル付きのメールを受信できない{#unable-to-get-email-with-attachments}

この問題が該当するのは、次のバージョンです。
* Experience Manager 6.5 Forms

## 問題 {#issue}

ユーザーが「メールで PDF を送信」や「送信時に添付ファイルを含める」などを設定する操作を実行できません。

## ソリューション {#solution}

1. jar を [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) としてダウンロードし、ダウンロードした jar ファイルを解凍してマニフェストファイルを取得します。

1. のマニフェストファイルを使用 `java.mail-1.0.jar` 手順 1 から取得し、次のようなカスタム jar ファイルを作成します。 `java.mail-1.5.jar`.

1. マニフェストファイルを開き、`1.5.0` を `1.5.6` に、`Bundle-Version: 1.0` を `Bundle-Version:1.5` にすべて置き換えます。

1. カスタム jar の作成 (`java.mail-1.5.jar`) ファイルに追加します。 `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` 次のフォルダー：
   `jar -cfm java.mail-1.5.jar manifest.mf`

   上記のコマンドで、*manifest.mf* はマニフェストファイルの名前で、*java.mail-1.5.jar* は、上記のコマンドを実行した後に作成されるファイルの名前です。

1. [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1) をダウンロードします。

1. `http://<server name>:<port>/lc/system/console/bundles` に移動し、`JavaMail API (com.sun.mail.javax.mail) version 1.6.2` という名前のバンドルを削除します。

1. 手順 3 で取得した `java.mail-1.5.jar` をインストールします。この手順を実行すると、JEE デプロイメントの Sling プロパティが再起動されます。`http://<server name>:<port>/lc/system/console/bundles` にインストールされたバンドルのステータス表示が&#x200B;**アクティブ**&#x200B;になるまで待ちます。

   >注意：この場合、ステータスは「 **InActive**，再起動   **JBoss®** から **サービスコンソール**.


1. 手順 5 でダウンロードした `javax.mail-1.5.6.redhat-1.jar` ファイルをインストールします。

1. 停止 **JBoss®** から **サービスコンソール** 次のプロパティをに追加します。 **Sling.properties** ファイル：
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. 再起動 **JBoss®**.
