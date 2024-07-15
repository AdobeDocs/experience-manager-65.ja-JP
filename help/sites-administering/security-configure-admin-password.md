---
title: インストール時の管理者パスワードの設定
description: Adobe Experience Manager のインストール時に管理者パスワードを変更する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 100%

---

# インストール時の管理者パスワードの設定{#configure-the-admin-password-on-installation}

## 概要 {#overview}

バージョン 6.3 以降の Adobe Experience Manager（AEM）では、新しいインスタンスのインストール時にコマンドラインを使用して管理者パスワードを設定できます。

それ以前のバージョンの AEM では、管理者アカウントのパスワードと各種コンソールのパスワードをインストール後に変更する必要がありました。

この機能により、AEM インスタンスのインストール時にリポジトリおよびサーブレットエンジン用の新しい管理者パスワードを設定できるようになり、後で手動で設定する必要がなくなります。

>[!CAUTION]
>
>この機能は Felix コンソールには対応しておらず、このコンソールのパスワードについては手動で変更する必要があります。詳しくは、関連する[セキュリティチェックリストの節](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)を参照してください。

## 使用方法 {#how-do-i-use-it}

この機能は、ファイルシステムエクスプローラーで JAR をダブルクリックする代わりに、コマンドラインから AEM をインストールする場合に自動的にトリガーされます。

コマンドラインから AEM インスタンスを実行する一般的な構文は次のとおりです。

```shell
java -jar aem6.3.jar
```

コマンドラインからインスタンスを実行すると、インストールプロセス中に管理者パスワードを変更するオプションが表示されます。

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>管理者パスワードの変更を求めるメッセージは、新しい AEM インスタンスのインストール時にのみ表示されます。

## -nointeractive フラグの使用 {#using-the-nointeractive-flag}

また、プロパティファイルでパスワードを指定することもできます。これは、`-Dadmin.password.file` システムプロパティと組み合わせた `-nointeractive` フラグを使用して行われます。

次に例を示します。

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

`passwordfile.properties` ファイル内のパスワードは次の形式にする必要があります。

```xml
admin.password = 12345678
```

>[!NOTE]
>
>`-Dadmin.password.file` システムプロパティを使用せずに `-nointeractive` パラメーターだけを使用した場合は、AEM ではデフォルトの管理者パスワードが使用され、変更を求めるメッセージは表示されません（基本的に以前のバージョンの動作と同じになります）。インストールスクリプトのコマンドラインでこの非インタラクティブモードを使用して、インストールを自動化できます。
