---
title: 整合性チェックとトラバーサルチェック
seo-title: 整合性チェックとトラバーサルチェック
description: 整合性チェックとトラバーサルチェックの実行方法について説明します。
seo-description: 整合性チェックとトラバーサルチェックの実行方法について説明します。
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 80%

---


# 整合性チェックとトラバーサルチェック{#consistency-and-traversal-checks}

アップグレード中に、ワークスペースの不整合による問題が発生することがあります。テストアップグレードを実行して不整合の問題が発生するかを確認できます。または、予防策として整合性チェックを実行できます。

テストアップグレードを実行し、ワークスペースの不整合によって失敗した場合は、crx-quickstart/logs/crx/error.log に次のようなエントリが表示されます。

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 整合性チェックの実行 {#perform-a-consistency-check}

整合性チェックを実行するには、JMX Mbean** com.adobe.granite (Repository)**の管理ページに移動します。AEMのメイン画面から、次のページに移動します。

**「Tools」>「Web Console」>「Main」（メニューバー）>「JMX」>「com.adobe.granite」(Repository)**

デフォルトのインストールでは、このページは次の場所にあります。**[|表示|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

このページの「**Operations**」セクションに、**`traversalCheck`** と **`consistencyCheck`** という 2 つのメソッドがあります。チェックを実行するには、この操作をクリックして必要なパラメーターを入力します。

![chlimage_1-117](assets/chlimage_1-117.png)

