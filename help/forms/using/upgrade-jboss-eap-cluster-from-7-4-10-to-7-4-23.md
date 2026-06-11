---
title: JEE上のAEM FormsのJBoss EAP クラスターを7.4.10から7.4.23にアップグレードします。
description: JEE上のAEM FormsのJBoss EAP クラスターを7.4.10から7.4.23にアップグレードする追加の手順。
exl-id: 2c9e7f41-a8d6-4b03-8e5c-1a4f6d9e0b72
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE
role: User, Developer
source-git-commit: dffa92539a8205387d21d3873ab9424508182f19
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---

# JEE上のAEM FormsのJBoss EAP クラスターを7.4.10から7.4.23にアップグレードします。 {#upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23}

## 概要 {#overview}

JEE上のAEM Formsのバージョン 7.4.10から7.4.23にJBoss EAP クラスターをアップグレードする場合は、スタンドアロンのアップグレード手順を超えた追加の設定が必要です。 キャッシュロケーター、マスタースレーブ認証、ホストバインディング、ドメインコントローラー設定などのクラスター固有の設定は、新しいJBoss インストールで更新する必要があります。

## 適用先 {#applies-to}

この記事の適用対象：

* クラスター環境でJBoss EAP 7.4.10上で動作するJEE上のAEM Forms
* WindowsおよびLinuxでのマスタースレーブ JBoss EAP設定

## 前提条件 {#prerequisites}

既存のインストールから新しい設定ファイルへの接続URL、ユーザー名、パスワードのコピーを含む、JEE[&#128279;](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md)上のAEM FormsのJBoss EAPを7.4.10から7.4.23にアップグレードするすべての手順を完了します。

## 手順 {#steps}

次の追加のクラスター固有の手順を実行します。

### domain.conf.batの更新 {#update-domain-conf-bat}

1. `domain.conf.bat`で、既存の設定のロケーター情報を新しいファイルに追加します。

   ```text
   set "JAVA_OPTS=%JAVA_OPTS% -Doak.documentMK.maxServerTimeDiffMillis=-1"
   set "JAVA_OPTS=%JAVA_OPTS% -Dadobe.cache.cluster-locators=<ip-address-master>[22345],<ip-address-slave>[22345]"
   set "JAVA_OPTS=%JAVA_OPTS% -DentityExpansionLimit=10000"
   ```

### マスタースレーブ認証の設定 {#configure-master-slave-authentication}

1. マスターノードでマスタースレーブ認証用の新しいユーザーを作成します。
1. スレーブノードで、`host.xml`のユーザーパスワードを更新します。

   ```xml
   <server-identities>
       <secret value="Y2hhbmdlaXQ="/>
   </server-identities>
   ```

### host.xmlでのIP アドレスの更新 {#update-ip-addresses-in-host-xml}

1. `host.xml`のマスターノードとスレーブノードの両方のIP アドレスを更新します。

   ```xml
   <interfaces>
       <interface name="management">
           <inet-address value="${jboss.bind.address.management:<ip-address>}"/>
       </interface>
       <interface name="public">
           <inet-address value="${jboss.bind.address:<ip-address>}"/>
       </interface>
   </interfaces>
   ```

### ドメイン設定からのデプロイメントの削除 {#remove-deployments-from-domain-configuration}

1. 新しい`domain_<db>.xml` ファイルに`<deployments>` セクションがないことを確認してください。
1. 次のブロックを既存の設定からコピーしないでください。

   ```xml
   <deployments>
       <deployment name="adobe-forms-ivs-jboss.ear" runtime-name="adobe-forms-ivs-jboss.ear"/>
       <deployment name="adobe-livecycle-cq-author.ear" runtime-name="adobe-livecycle-cq-author.ear"/>
       <deployment name="adobe-livecycle-jboss.ear" runtime-name="adobe-livecycle-jboss.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win32.ear" runtime-name="adobe-livecycle-native-jboss-x86_win32.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win64.ear" runtime-name="adobe-livecycle-native-jboss-x86_win64.ear"/>
       <deployment name="adobe-output-ivs-jboss.ear" runtime-name="adobe-output-ivs-jboss.ear"/>
       <deployment name="adobe-workspace-client.ear" runtime-name="adobe-workspace-client.ear"/>
   </deployments>
   ```

### ドメイン設定でのドライバークラスの更新 {#update-driver-class-in-domain-configuration}

1. データベースエンジンに基づいて、`domain_<db>.xml`のドライバークラスの節を更新します。

   **MSSQL:**

   ```xml
   <xa-datasource-class>com.microsoft.sqlserver.jdbc.SQLServerXADataSource</xa-datasource-class>
   ```

   **Oracle:**

   ```xml
   <xa-datasource-class>oracle.jdbc.xa.client.OracleXADataSource</xa-datasource-class>
   ```

### スレーブノード上のドメインコントローラーの更新 {#update-domain-controller-on-slave-nodes}

1. マスターIP アドレス、ポート `9999`、ユーザー名`slave1`、領域`ManagementRealm`を使用して、`host.xml`のスレーブノードのドメインコントローラーブロックを更新します。

   ```xml
   <remote host="<ip-address>" port="9999" username="slave1" realm="ManagementRealm"/>
   ```

### jboss-cli.xmlの更新 {#update-jboss-cli-xml}

1. マスターノードとスレーブノードの両方で、`jboss-cli.xml`の`<host>` エントリを更新します。
