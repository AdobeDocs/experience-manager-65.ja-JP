---
title: AEM Forms ワークフローへのログイン
description: AEM Forms Workflow の問題をデバッグし、AEM Formsワークフローのデバッグログを有効にしてログを表示する方法について説明します。
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 82%

---

# AEM Forms ワークフローへのログイン{#logging-in-aem-forms-workflows}

Forms Workflow手順では、ワークフローに関する問題をデバッグするための詳細なログが便利に提供されます。 ログを表示するには AEM Formsワークフローのデバッグログを有効にします。

デフォルトでは、すべてのログ情報は */crx-repository/logs/* ディレクトリに保存されている **error.log** ファイルにあります。

Forms ワークフローのデバッグログには、次の内容が含まれます。

* 各ワークフロー手順のエントリ。次に例を示します。\
  `[DEBUG] "Executing Invoke DDX Process step"`

* 各ワークフロー手順の終了。次に例を示します。\
  `[DEBUG] "Successfully finished Invoke DDX Process step"`

* サービス呼び出しメッセージ。次に例を示します。\
  `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* サービス終了メッセージ。次に例を示します。\
  `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* メタデータマップから読み取られた変数。次に例を示します。\
  `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* JCR リポジトリで書き込まれた変数。次に例を示します。

  ```verilog
     [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
  ```

* 完全なスタックトレースを含む例外メッセージ。次に例を示します。\
  `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 動的な手順のメタデータパラメーター。次に例を示します。

  ```verilog
  [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
   [DEBUG] Locale to be used for Document of Record is <locale>
  ```

次の例は、「ドキュメントに署名」手順のログを示しています。

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

ログを使用して次の内容を評価します。

* 正しいAdobe Sign設定を使用しています。
* 契約を正常に作成したら Adobe Sign サービスが終了すること。
* 「ドキュメントに署名」手順が成功メッセージとともに終了すること。

例外がある場合は、完全なスタックトレースを表示して、エラーの原因を評価できます。

## AEM Forms ワークフローのデバッグログの有効化 {#enable-debug-logging-for-aem-forms-workflows}

AEM Formsワークフローのデバッグログを有効にするには、次の操作を行います。

1. AEM web コンソール設定マネージャーに移動します。

   https://&#39;[server]:[port]&#39;/system/console/configMgr

1. **[!UICONTROL Sling]**／**[!UICONTROL ログのサポート]**&#x200B;を選択します。
1. 「**[!UICONTROL 新規ロガーを追加r]**」をタップします。
1. **[!UICONTROL デバッグ]**&#x200B;を&#x200B;**[!UICONTROL ログレベル]**&#x200B;として選択します。
1. ログファイルの場所を指定します。ログファイルのデフォルトの場所は *logs\error.log* です。
1. **[!UICONTROL ロガー]**&#x200B;列でパッケージの名前を **com.adobe.granite.workflow.core** として指定します。

   これらの手順を実行すると、**com.adobe.granite.workflow.core** パッケージのデバッグログを格納できるようになります。**[!UICONTROL +]** をタップして次のパッケージ名をリストに追加します。

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
