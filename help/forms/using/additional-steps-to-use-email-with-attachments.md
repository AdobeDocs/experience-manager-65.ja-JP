---
title: 添付ファイル付きのメールを受信するための追加手順
description: JEE 上の AEM Forms プラットフォームで添付ファイルを含む電子メールを取得できない場合のエラーの修正方法を説明します。
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '270'
ht-degree: 100%

---

# AEM Forms on JEE プラットフォームで添付ファイル付きのメールを受信できない{#unable-to-get-email-with-attachments}

この問題が該当するのは、次のバージョンです。

* Experience Manager 6.5 Forms

## 問題 {#issue}

ユーザーが「メールで PDF を送信」や「送信時に添付ファイルを含める」などを設定する操作を実行できません。

## 解決策 {#solution}

1. jar を [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) としてダウンロードし、ダウンロードした jar ファイルを解凍してマニフェストファイルを取得します。

1. 手順 1 で取得した `java.mail-1.0.jar` のマニフェストファイルを使用して、カスタム jar ファイル（例：`java.mail-1.5.jar`）を作成します。

1. マニフェストファイルを開き、`1.5.0` を `1.5.6` に、`Bundle-Version: 1.0` を `Bundle-Version:1.5` にすべて置き換えます。

1. `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` フォルダーで、次のようにコマンドを使用して、カスタム jar（`java.mail-1.5.jar`）ファイルを作成します。
   `jar -cfm java.mail-1.5.jar manifest.mf`

   上記のコマンドで、*manifest.mf* はマニフェストファイルの名前で、*java.mail-1.5.jar* は、上記のコマンドを実行した後に作成されるファイルの名前です。

1. [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1) をダウンロードします。

1. `http://<server name>:<port>/lc/system/console/bundles` に移動し、`JavaMail API (com.sun.mail.javax.mail) version 1.6.2` という名前のバンドルを削除します。

1. 手順 3 で取得した `java.mail-1.5.jar` をインストールします。この手順を実行すると、JEE デプロイメントの Sling プロパティが再起動されます。`http://<server name>:<port>/lc/system/console/bundles` にインストールされたバンドルのステータス表示が&#x200B;**アクティブ**&#x200B;になるまで待ちます。

   >メモ：ステータスが&#x200B;**非アクティブ**&#x200B;のままの場合は、**サービスコンソール**&#x200B;から **JBoss®** を再起動します。


1. 手順 5 でダウンロードした `javax.mail-1.5.6.redhat-1.jar` ファイルをインストールします。

1. **サービスコンソール**&#x200B;から **JBoss®** を停止し、次のプロパティを **Sling.properties** ファイルに追加します。
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. **JBoss®** を再起動します。

>[!NOTE]
>
> SDK を再起動するには、「Ctrl + C」コマンドを使用することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。
