---
title: 整合性チェックとトラバーサルチェック
description: 整合性チェックとトラバーサルチェックを実行する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: ht
source-wordcount: '153'
ht-degree: 100%

---

# 整合性チェックとトラバーサルチェック{#consistency-and-traversal-checks}

アップグレード時に、ワークスペースの不整合が原因で問題が発生する可能性があります。テストのアップグレードを実行して問題が発生しているかどうかを確認するか、予防策として整合性チェックを実行できます。

テストアップグレードを実行した結果、ワークスペースの不整合によって失敗した場合は、crx-quickstart/logs/crx/error.log に次のようなエントリが表示されます。

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## 整合性チェックの実行 {#perform-a-consistency-check}

整合性チェックを実行するには、JMX Mbean **com.adobe.granite（レポジトリ）**&#x200B;の管理ページに移動します。AEM メイン画面から、次に移動してください。

**ツール／web コンソール／メイン（メニューバー）／JMX／com.adobe.granite（リポジトリ）**

デフォルトのインストールでは、このページは次の場所にあります。**[|表示|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

「**操作**」セクションには、**`traversalCheck`** と **`consistencyCheck`** という 2 つのメソッドがあります。チェックを実行するには、この操作をクリックして必要なパラメーターを入力します。

![chlimage_1-117](assets/chlimage_1-117.png)
