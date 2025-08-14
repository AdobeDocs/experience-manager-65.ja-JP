---
title: JEE 上のAEM Formsの XXE、Struts 開発モード設定、リモートコード実行の脆弱性の軽減
description: JEE 上のAEM Formsの XXE、設定、リモートコード実行の脆弱性の軽減
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 9fade12f-a038-4fd6-8767-1c30966574c5
solution: Experience Manager, Experience Manager Forms
release-date: 2025-08-05T00:00:00Z
source-git-commit: 3f64cfa688ef1f0090b7ce0d821324593cbea693
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 8%

---

# JEE 上のAEM Formsの RCE （CVE-2025-49533）、Struts 開発モード設定（CVE-2025-54253）、XXE （CVE-2025-54254）および脆弱性の軽減 {#mitigating-xxe-configuration-rce-vulnerabilities-aem-forms}

## クイックリファレンス

| **影響レベル** | **影響を受けるバージョン** | **推奨されるアクション** |
|---|---|---|
| **重大** | JEE 上のAEM 6.5 Forms サービスパック 23 （6.5.23.0） | [ 最新のホットフィックスをインストールする ](#option-1-for-users-on-version-65230-install-latest-hotfix) |
| **重大** | JEE 上のAEM 6.5 Forms サービスパック 18～22 （6.5.18.0～6.5.22.0） | [ 手動で修正をインストールする ](#option-2-for-users-on-65180---65220-manual-hotfix-installation) |
| **重大** | JEE 上のAEM 6.5 Forms サービスパック 17 （6.5.17.0）以前 | サポートされているサービスパックバージョンにアップグレードし、新しいバージョンに推奨される軽減手順を適用します |
| **影響なし** | OSGi 上のAEM Forms、Workbench、Cloud Service | アクションは必要ありません |

**対処された脆弱性：**

- リモートコード実行（CVE-2025-49533）
- 設定のセキュリティの問題（CVE-2025-54253）
- XML 外部エンティティ（XXE）処理（CVE-2025-54254）

## 概要

### 影響の対象

| 脆弱性 | 影響 | 影響を受けるコンポーネント |
|---|---|---|
| **CVE-2025-49533**：リモートコード実行 | GetDocumentServlet での認証されていないコード実行 | JEE 上のAEM 6.5 Forms サービスパック 23 （6.5.23.0）以前 |
| **CVE-2025-54253**：設定の問題 | 管理 UI で有効化された Struts 開発モード | JEE 上のAEM 6.5 Forms サービスパック 23 （6.5.23.0）以前 |
| **CVE-2025-54254**:XXE プロセス | Document Security モジュールにより、未認証のファイルアクセスが許可されます | JEE 上のAEM 6.5 Forms サービスパック 23 （6.5.23.0）以前 |


### 影響なし

- Experience Manager Forms Workbench（すべてのバージョン）
- OSGi 版 Experience Manager Forms（すべてのバージョン）
- Experience Manager Forms as a Cloud Service

## 解決オプション


### 始める前に

変更を加える前に、変更または更新する EAR ファイルまたは DSC ファイルのバックアップを作成します。

- 配置ディレクトリ内で、元の EAR または DSC ファイルを見つけます。
- ファイルを配置ディレクトリの外部の安全なバックアップの場所にコピーします。
- 更新を続行する前に、バックアップが完了し、アクセス可能であることを確認してください。

この予防策により、更新プロセス中に問題が発生した場合に備えて、元の状態に戻すことができます。

### オプション 1:（バージョン 6.5.23.0 のユーザーの場合）最新のホットフィックスのインストール

1. [6.5.23.0](/help/release-notes/aem-forms-hotfix.md) のホットフィックスをダウンロードします。
1. 標準の [ ホットフィックス/パッチのインストール手順 ](/help/release-notes/jee-patch-installer-65.md) 従います。
1. IBM WebSphere またはOracle WebLogic で Document Security （旧称Rights Management）を使用している場合は、AEM Forms サーバーを起動する前に、次の Java システムプロパティ（JVM 引数）を設定します。

   ```
   -Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
   ```

1. アプリケーションサーバーを再起動します

### オプション 2:（6.5.18.0 ～ 6.5.22.0 のユーザー用）手動のホットフィックスのインストール

+++6.5.18.0 ～ 6.5.22.0 の手動ホットフィックスのインストール

**手順 1：ホットフィックスパッケージをダウンロードして抽出する**

- Adobe ソフトウェア配布ポータルから [6.5.18.0 - 6.5.22.](/help/release-notes/aem-forms-hotfix.md) のホットフィックスをダウンロードします
- ローカルで抽出

**手順 2：正しいバージョンフォルダーに移動する**

- 環境にインストールされているサービスパックのバージョンに応じて、一致するフォルダーに移動します。

  サービスパック 20 の例のフォルダーは次のとおりです。

  ```
  <extracted-hotfix>/SP20/
  ```

**手順 3：デプロイメントディレクトリを見つける**

- JEE 上のAEM Forms サーバーで、次の場所に移動します。

  ```
  [AEM installation directory]/deploy
  ```

  例：`adobe/adobe-experience-manager-forms/deploy`



**手順 4:EAR ファイルを更新して置き換える**

>[!BEGINTABS]

>[!TAB JBoss]

1. `adobe-core-jboss.ear` を開き、`adminui.war` を

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adminui.war
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/jboss/adminui.war` のように指定します。

1. `adobe-core-jboss.ear` 内で、`lib/` フォルダーに移動し、`adobe-uisupport.jar` を次のように置き換えます。

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar` のように指定します。

1. 耳を救ってください。 変更が正しく保存されていることを確認します。


1. `adobe-edcserver-jboss.ear` を

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-edcserver-jboss.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/jboss/adobe-edcserver-jboss.ear` のように指定します。

1. `adobe-forms-jboss.ear` を

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-forms-jboss.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/jboss/adobe-forms-jboss.ear` のように指定します。



>[!TAB WebLogic]

1. `adobe-core-weblogic.ear` を開き、`adminui.war` を

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adminui.war
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/weblogic/adminui.war` のように指定します。

1. `adobe-core-weblogic.ear` 内で、`adobe-uisupport.jar` を次のように置き換えます。

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar` のように指定します。

1. 耳を救ってください。 変更が正しく保存されていることを確認します。


1. `adobe-edcserver-weblogic.ear` を

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-edcserver-weblogic.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-edcserver-weblogic.ear` のように指定します。

1. `adobe-forms-weblogic.ear` を

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-forms-weblogic.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-forms-weblogic.ear` のように指定します。

>[!TAB WebSphere]

1. `adobe-core-websphere.ear` を開き、`adminui.war` を

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adminui.war
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/websphere/adminui.war` のように指定します。

1. `adobe-core-websphere.ear` 内で、`adobe-uisupport.jar` を次のように置き換えます。

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar` のように指定します。

1. 耳を救ってください。 変更が正しく保存されていることを確認します。


1. `adobe-edcserver-websphere.ear` を

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-edcserver-websphere.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/websphere/adobe-edcserver-websphere.ear` のように指定します。

1. `adobe-forms-websphere.ear` を

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-forms-websphere.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/websphere/adobe-forms-websphere.ear` のように指定します。

>[!ENDTABS]



**手順 5:`adobe-rightsmanagement-<appserver>-dsc.jar` ファイルを** で更新

```
adobe-xxe-configuration-hotfix/SP[version]/<appserver>/adobe-rightsmanagement-<appserver>-dsc.jar
```

例えば、`adobe-xxe-configuration-hotfix/SP20/jboss/adobe-rightsmanagement-jboss-dsc.jar` のように指定します。

**手順 6:WebSphere および WebLogic での Document Security の追加設定**:

Document Security （旧称Rights Management）を使用している場合は、AEM Forms サーバーを起動する前に、次の Java システムプロパティ（JVM 引数）を設定します。

```
-Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
```


**手順 7:Configuration Manager を再実行する**

- Configuration Manager を起動して更新された EAR を再デプロイし、ホットフィックスを適用します。

+++

### オプション 3:（6.5.17.0 以前のユーザーの場合）アップグレードパス

1. [サポートされているサービスパックバージョンへのアップグレード](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)
1. 新しいバージョンに基づいて、上記のオプション 1 またはオプション 2 に従います

## 参照

- [CWE-611: XML 外部エンティティ参照の不適切な制限 ](https://cwe.mitre.org/data/definitions/611.html)
- [CWE-16：設定 ](https://cwe.mitre.org/data/definitions/16.html)
- [OWASP XXE 防止チートシート ](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_XXE_Processing)
- [Adobe Experience Manager Forms セキュリティのベストプラクティス ](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=ja)