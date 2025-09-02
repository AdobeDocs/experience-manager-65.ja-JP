---
title: AEM Forms on JEE での XXE、Struts 開発モード設定、リモートコード実行の脆弱性の軽減
description: AEM Forms on JEE での XXE、設定、リモートコード実行の脆弱性の軽減
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 9fade12f-a038-4fd6-8767-1c30966574c5
solution: Experience Manager, Experience Manager Forms
release-date: 2025-08-05T00:00:00Z
source-git-commit: 3f64cfa688ef1f0090b7ce0d821324593cbea693
workflow-type: ht
source-wordcount: '675'
ht-degree: 100%

---

# AEM Forms on JEE での RCE（CVE-2025-49533）、Struts 開発モード設定（CVE-2025-54253）、XXE（CVE-2025-54254）、脆弱性の軽減 {#mitigating-xxe-configuration-rce-vulnerabilities-aem-forms}

## クイックリファレンス

| **影響レベル** | **影響を受けるバージョン** | **推奨されるアクション** |
|---|---|---|
| **重要** | AEM 6.5 Forms on JEE サービスパック 23（6.5.23.0） | [最新のホットフィックスをインストール](#option-1-for-users-on-version-65230-install-latest-hotfix) |
| **重要** | AEM 6.5 Forms on JEE サービスパック 18～22（6.5.18.0～6.5.22.0） | [手動で修正をインストール](#option-2-for-users-on-65180---65220-manual-hotfix-installation) |
| **重要** | AEM 6.5 Forms on JEE サービスパック 17（6.5.17.0）以前 | サポートされているサービスパックバージョンにアップグレードし、新しいバージョンに推奨される軽減手順を適用します |
| **影響なし** | AEM Forms on OSGi、Workbench、Cloud Service | アクションは必要ありません |

**対処された脆弱性：**

- リモートコード実行（CVE-2025-49533）
- 設定のセキュリティの問題（CVE-2025-54253）
- XML 外部エンティティ（XXE）処理（CVE-2025-54254）

## 概要

### 影響を受けるもの

| 脆弱性 | 影響 | 影響を受けるコンポーネント |
|---|---|---|
| **CVE-2025-49533**：リモートコード実行 | GetDocumentServlet での未認証のコード実行 | AEM 6.5 Forms on JEE サービスパック 23（6.5.23.0）以前 |
| **CVE-2025-54253**：設定の問題 | 管理 UI で有効化された Struts 開発モード | AEM 6.5 Forms on JEE サービスパック 23（6.5.23.0）以前 |
| **CVE-2025-54254**：XXE 処理 | Document Security モジュールにより、不正ファイルアクセスが許可されます | AEM 6.5 Forms on JEE サービスパック 23（6.5.23.0）以前 |


### 影響を受けないもの

- Experience Manager Forms Workbench（すべてのバージョン）
- OSGi 版 Experience Manager Forms（すべてのバージョン）
- Experience Manager Forms as a Cloud Service

## 解決策オプション


### 始める前に

変更する前に、変更または更新する EAR ファイルまたは DSC ファイルのバックアップを作成します。

- デプロイメントディレクトリで、元の EAR ファイルまたは DSC ファイルを見つけます。
- ファイルをデプロイメントディレクトリの外部の安全なバックアップ場所にコピーします。
- 更新を進める前に、バックアップが完了し、アクセス可能であることを確認します。

この予防措置により、更新プロセス中に問題が発生した場合に元の状態を復元できます。

### オプション 1：（バージョン 6.5.23.0 のユーザーの場合）最新のホットフィックスのインストール

1. [6.5.23.0](/help/release-notes/aem-forms-hotfix.md) のホットフィックスをダウンロードします。
1. 標準の[ホットフィックス／パッチのインストール手順](/help/release-notes/jee-patch-installer-65.md)に従います
1. IBM WebSphere または Oracle WebLogic で Document Security（旧称 Rights Management）を使用している場合は、AEM Forms サーバーを起動する前に、次の Java システムプロパティ（JVM 引数）を設定します。

   ```
   -Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
   ```

1. アプリケーションサーバーを再起動します

### オプション 2：（6.5.18.0～6.5.22.0 のユーザーの場合）手動のホットフィックスのインストール

+++6.5.18.0～6.5.22.0 の手動のホットフィックスのインストール

**手順 1：ホットフィックスパッケージをダウンロードして抽出**

- Adobe ソフトウェア配布ポータルから [6.5.18.0～6.5.22 のホットフィックス](/help/release-notes/aem-forms-hotfix.md)をダウンロードします
- ローカルで抽出します

**手順 2：正しいバージョンフォルダーに移動**

- 環境にインストールされているサービスパックのバージョンに基づいて、一致するフォルダーに移動します。

  サービスパック 20 の例のフォルダーは次のとおりです。

  ```
  <extracted-hotfix>/SP20/
  ```

**手順 3：デプロイメントディレクトリを見つける**

- AEM Forms on JEE サーバーで、次の場所に移動します。

  ```
  [AEM installation directory]/deploy
  ```

  例：`adobe/adobe-experience-manager-forms/deploy`



**手順 4：EAR ファイルを更新して置き換える**

>[!BEGINTABS]

>[!TAB JBoss]

1. `adobe-core-jboss.ear` を開き、`adminui.war` を次に置き換えます

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adminui.war
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/jboss/adminui.war` のように指定します。

1. `adobe-core-jboss.ear` 内で、`lib/` フォルダーに移動し、`adobe-uisupport.jar` を次に置き換えます。

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar` のように指定します。

1. EAR を保存します。変更が適切に保存されていることを確認します。


1. `adobe-edcserver-jboss.ear` を次に置き換えます

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-edcserver-jboss.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/jboss/adobe-edcserver-jboss.ear` のように指定します。

1. `adobe-forms-jboss.ear` を次に置き換えます

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-forms-jboss.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/jboss/adobe-forms-jboss.ear` のように指定します。



>[!TAB WebLogic]

1. `adobe-core-weblogic.ear` を開き、`adminui.war` を次に置き換えます

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adminui.war
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/weblogic/adminui.war` のように指定します。

1. `adobe-core-weblogic.ear` 内で、`adobe-uisupport.jar` を次に置き換えます。

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar` のように指定します。

1. EAR を保存します。変更が適切に保存されていることを確認します。


1. `adobe-edcserver-weblogic.ear` を次に置き換えます

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-edcserver-weblogic.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-edcserver-weblogic.ear` のように指定します。

1. `adobe-forms-weblogic.ear` を次に置き換えます

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-forms-weblogic.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-forms-weblogic.ear` のように指定します。

>[!TAB WebSphere]

1. `adobe-core-websphere.ear` を開き、`adminui.war` を次に置き換えます

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adminui.war
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/websphere/adminui.war` のように指定します。

1. `adobe-core-websphere.ear` 内で、`adobe-uisupport.jar` を次に置き換えます。

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar` のように指定します。

1. EAR を保存します。変更が適切に保存されていることを確認します。


1. `adobe-edcserver-websphere.ear` を次に置き換えます

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-edcserver-websphere.ear
   ```

   例えば、`adobe-xxe-configuration-hotfix/SP20/websphere/adobe-edcserver-websphere.ear` のように指定します。

1. `adobe-forms-websphere.ear` を次に置き換えます

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-forms-websphere.ear
   ```

   例：`adobe-xxe-configuration-hotfix/SP20/websphere/adobe-forms-websphere.ear`

>[!ENDTABS]



**手順 5：`adobe-rightsmanagement-<appserver>-dsc.jar` ファイルを次に更新**

```
adobe-xxe-configuration-hotfix/SP[version]/<appserver>/adobe-rightsmanagement-<appserver>-dsc.jar
```

例：`adobe-xxe-configuration-hotfix/SP20/jboss/adobe-rightsmanagement-jboss-dsc.jar`

**手順 6：WebSphere および WebLogic での Document Security の追加設定**：

Document Security（旧称 Rights Management）を使用している場合は、AEM Forms サーバーを起動する前に、次の Java システムプロパティ（JVM 引数）を設定します。

```
-Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
```


**手順 7：Configuration Manager を再実行**

- Configuration Manager を起動して、更新された EAR を再デプロイし、ホットフィックスを適用します

+++

### オプション 3：（6.5.17.0 以前のユーザーの場合）パスのアップグレード

1. [サポートされているサービスパックバージョンにアップグレードします](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)
1. 新しいバージョンに基づいて、上記のオプション 1 またはオプション 2 に従います

## 参照

- [CWE-611：XML 外部エンティティ参照の不適切な制限](https://cwe.mitre.org/data/definitions/611.html)
- [CWE-16：設定](https://cwe.mitre.org/data/definitions/16.html)
- [OWASP XXE 防止チートシート](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_XXE_Processing)
- [Adobe Experience Manager Forms セキュリティのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=ja)