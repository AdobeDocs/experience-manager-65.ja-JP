---
title: JEE上のAEM FormsのJBoss EAPを7.4.10から7.4.23にアップグレードする
description: JEE スタンドアロン環境のAEM FormsでJBoss EAPを7.4.10から7.4.23にアップグレードする手順。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 8f4c2a91-6b3d-4e7f-9c12-5d8e1f0a2b34
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
source-git-commit: 652162941dd716ae797ce50709e91757dad99054
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 4%

---

# JEE上のAEM FormsのJBoss EAPを7.4.10から7.4.23にアップグレードする {#upgrade-jboss-eap-from-7-4-10-to-7-4-23}

## 概要 {#overview}

JEE上のAEM Forms スタンドアロン環境で、JBoss EAPをバージョン 7.4.10から7.4.23にアップグレードします。 アップグレードを行うには、設定ファイル、データベース資格情報、CRX リポジトリを新しいJBoss インストールに移行し、Configuration Managerを実行して設定を完了する必要があります。

## 適用先 {#applies-to}

この記事の適用対象：

* スタンドアロン環境でJBoss EAP 7.4.10上で動作するJEE上のAEM Forms
* WindowsおよびLinuxでのターンキーおよび部分的なターンキーインストールモード

>[!NOTE]
>
> JBoss クラスター環境をアップグレードする場合は、まず最初にこの記事の手順を実行し、[JEE上のAEM FormsのJBoss EAP クラスターを7.4.10から7.4.23にアップグレード &#x200B;](/help/forms/using/upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23.md)の追加手順を実行します。

## 前提条件 {#prerequisites}

始める前に：

* [Adobe Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html)からJBoss 7.4.23 パッケージをダウンロードします。
* ターゲット環境への管理アクセス権があることを確認します。
* 既存のJBoss インストールの完全なバックアップを作成します。

## 手順 {#steps}

JBoss EAPを7.4.10から7.4.23にアップグレードするには、次の手順を実行します。

### JBossのダウンロードと抽出 {#download-and-extract-jboss}

1. Adobe Software Distribution PortalからJBoss 7.4.23 ZIP パッケージをダウンロードします。
1. ZIP ファイルをローカルディレクトリに展開します。
1. 抽出したJBoss フォルダーの名前を、既存のJBoss インストールディレクトリの正確な名前に変更します。

### 既存のインストールのバックアップ {#back-up-the-existing-installation}

1. 現在のJBoss インストールディレクトリの完全バックアップを作成します。
1. バックアップにすべての設定ファイルとカスタマイズが含まれていることを確認します。

### データベースファイルの設定 {#configure-database-files}

1. 設定ディレクトリに移動します。

   * Windows：`<JBoss_Home>\standalone\configuration`
   * Linux: `<JBoss_Home>/standalone/configuration`

1. インストールモードに基づいてデータベースファイルを設定します。

   **ターンキーモード：**

   1. `lc_mysql.xml`を`lc_turnkey.xml`に変更します。
   1. 次のファイルを削除します。

      * `lc_oracle.xml`
      * `lc_mssql.xml`

   **部分的なターンキーモード：**

   1. データベース エンジンに対応する`lc_db.xml` ファイルのみを保持します。
   1. 残りの2つの`lc_db.xml`設定ファイルを削除します。

### データベース資格情報の更新 {#update-database-credentials}

1. バックアップされたJBoss インストールから`lc_turnkey.xml` ファイルを開きます。
1. 次の値をコピーします。

   * データソース URL
   * データベースのユーザー名
   * データベースパスワード

1. 新しい`lc_turnkey.xml` ファイルの対応するエントリを更新します。

### CRX リポジトリの移行 {#migrate-crx-repository}

1. 古いJBoss インストールの次のディレクトリに移動します。

   `<old_jboss>\bin\`

1. `crx-quickstart` フォルダーをコピーします。
1. フォルダーをに貼り付けます：

   `<new_jboss>\bin\`

### Configuration Managerの実行 {#run-configuration-manager}

1. アップグレードしたJBoss環境を開始します。
1. LiveCycle Configuration Manager （LCM）を起動します。
1. エンドツーエンドのConfiguration Manager ワークフローを実行します。
1. すべての設定タスクが正常に完了したことを確認します。

### アップグレード後の検証 {#post-upgrade-validation}

アップグレード後、次の点を確認します。

* すべてのサービスが正常に開始されます。
* データベースの接続が検証されます。
* アプリケーションの機能が検証されています。
