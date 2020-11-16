---
title: インストール時の admin パスワードの設定
seo-title: インストール時の admin パスワードの設定
description: AEM のインストール時に admin パスワードを変更する方法について説明します。
seo-description: AEM のインストール時に admin パスワードを変更する方法について説明します。
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 87%

---


# インストール時の admin パスワードの設定{#configure-the-admin-password-on-installation}

## 概要 {#overview}

バージョン 6.3 以降の AEM では、新しいインスタンスのインストール時にコマンドラインを使用して admin パスワードを設定できます。

それ以前のバージョンの AEM では、admin アカウントのパスワードと各種コンソールのパスワードをインストール終了後に変更する必要がありました。

この機能により、AEM インスタンスのインストール時にリポジトリおよび Servlet Engine 用の新しい admin パスワードを設定できるようになり、後で手動で設定する必要がなくなりました。

>[!CAUTION]
>
>ただし、この機能は Felix コンソールには対応しておらず、このコンソールのパスワードについては手動で変更する必要があります。詳しくは、関連する[セキュリティチェックリストの節](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)を参照してください。

## 使用方法 {#how-do-i-use-it}

この機能は、ファイルシステムエクスプローラーで JAR をダブルクリックする代わりに、コマンドラインから AEM をインストールする場合に自動的にトリガーされます。

コマンドラインから AEM インスタンスを実行するための一般的な構文は次のとおりです。

```shell
java -jar aem6.3.jar
```

コマンドラインからインスタンスを実行する際には、インストールプロセスの途中で admin パスワードの変更オプションが提示されます。

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>admin パスワードの変更を求めるメッセージは、新しい AEM インスタンスのインストール時にのみ表示されます。

## -nointeractive フラグの使用 {#using-the-nointeractive-flag}

プロパティファイルでパスワードを指定することもできます。これは、 `-nointeractive` systemプロパティと組み合わせたフラグを使用して行います`-Dadmin.password.file` 。

次に例を示します。

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

`passwordfile.properties` ファイル内のパスワードの書式は次のようにする必要があります。

```xml
admin.password = 12345678
```

>[!NOTE]
>
>If you simply use the `-nointeractive` parameter without the `-Dadmin.password.file` system property, AEM will use the default admin password without asking you to change it, essentially replicating behaviour from earlier versions. インストールスクリプトのコマンドラインでこの非インタラクティブモードを使用して、インストールを自動化できます。

