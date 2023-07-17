---
title: インストール時の admin パスワードの設定
description: Adobe Experience Managerのインストール時に管理者パスワードを変更する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 5%

---

# インストール時の admin パスワードの設定{#configure-the-admin-password-on-installation}

## 概要 {#overview}

バージョン 6.3 以降、Adobe Experience Manager(AEM) では、新しいインスタンスをインストールする際に、コマンドラインを使用して管理者パスワードを設定できます。

以前のバージョンのAEMでは、管理者アカウントのパスワードと他の様々なコンソールのパスワードをインストール後に変更する必要がありました。

この機能により、AEMインスタンスのインストール中にリポジトリとサーブレットエンジンの新しい管理者パスワードを設定できる機能が追加され、後で手動で設定する必要がなくなります。

>[!CAUTION]
>
>Felix コンソールは対象外で、パスワードを手動で変更する必要があります。 詳しくは、 [セキュリティチェックリストセクション](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## 使用方法 {#how-do-i-use-it}

この機能は、ファイルシステムエクスプローラから JAR をダブルクリックするのではなく、コマンドラインを使用してAEMをインストールする場合に自動的にトリガーされます。

コマンドラインからAEMインスタンスを実行するための一般的な構文は次のとおりです。

```shell
java -jar aem6.3.jar
```

コマンドラインからインスタンスを実行すると、インストールプロセス中に admin パスワードを変更するオプションが表示されます。

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>管理者パスワードを変更するプロンプトは、新しいAEMインスタンスのインストール時にのみ表示されます。

## -nointeractive フラグの使用 {#using-the-nointeractive-flag}

プロパティファイルからパスワードを指定することもできます。 これは、 `-nointeractive` ～と組み合わされた旗 `-Dadmin.password.file` システムプロパティ。

次に例を示します。

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

内のパスワード `passwordfile.properties` ファイルの形式は次のとおりです。

```xml
admin.password = 12345678
```

>[!NOTE]
>
>単に `-nointeractive` パラメーターに `-Dadmin.password.file` システムプロパティの場合、AEMはデフォルトの admin パスワードを使用しますが、変更を求めることはありません。つまり、以前のバージョンの動作をレプリケートします。 この非インタラクティブモードは、インストールスクリプトのコマンドラインを使用して自動インストールに使用できます。
