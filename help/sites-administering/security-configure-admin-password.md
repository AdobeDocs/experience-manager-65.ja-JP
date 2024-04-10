---
title: インストール時の admin パスワードの設定
description: Adobe Experience Managerのインストール時に管理者パスワードを変更する方法を説明します。
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
ht-degree: 6%

---

# インストール時の admin パスワードの設定{#configure-the-admin-password-on-installation}

## 概要 {#overview}

バージョン 6.3 以降、Adobe Experience Manager（AEM）では、新しいインスタンスをインストールする際にコマンドラインを使用して admin パスワードを設定できます。

以前のバージョンのAEMでは、管理者アカウントのパスワードは、その他の様々なコンソールのパスワードと共に、インストール後に変更する必要がありました。

この機能により、AEM インスタンスのインストール中にリポジトリとサーブレットエンジンの新しい管理者パスワードを設定できるので、後で手動で設定する必要がなくなります。

>[!CAUTION]
>
>この機能は Felix コンソールには対応していません。パスワードを手動で変更する必要があります。 詳しくは、関連するを参照してください [セキュリティチェックリストセクション](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## 使用方法 {#how-do-i-use-it}

この機能は、ファイルシステムエクスプローラーから JAR をダブルクリックするのではなく、コマンドラインを介してAEMをインストールすると自動的にトリガーします。

コマンドラインからAEM インスタンスを実行するための一般的な構文を以下に示します。

```shell
java -jar aem6.3.jar
```

コマンドラインからインスタンスを実行すると、インストールプロセス中に管理者パスワードを変更するオプションが表示されます。

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>管理者パスワードを変更するプロンプトは、新しいAEM インスタンスのインストール中にのみ表示されます。

## -nointeractive フラグの使用 {#using-the-nointeractive-flag}

また、プロパティファイルからパスワードを指定することもできます。 これは、 `-nointeractive` を組み合わせたフラグ `-Dadmin.password.file` システムプロパティ。

次に例を示します。

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

内のパスワード `passwordfile.properties` ファイルは次の形式にする必要があります：

```xml
admin.password = 12345678
```

>[!NOTE]
>
>を使用する場合 `-nointeractive` を含まないパラメーター `-Dadmin.password.file` システムプロパティが無効な場合、AEMはデフォルトの管理者パスワードを使用し、変更を求めるメッセージは表示されません（基本的に以前のバージョンの動作と同じになります）。 インストールスクリプトのコマンドラインでこの非インタラクティブモードを使用して、インストールを自動化できます。
