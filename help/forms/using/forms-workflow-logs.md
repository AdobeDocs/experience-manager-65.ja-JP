---
title: AEM Formsワークフローのログイン
seo-title: AEM Formsワークフローのログイン
description: ログを使用してAEM Formsのワークフローの問題をデバッグします。
seo-description: ログを使用してAEM Formsのワークフローの問題をデバッグします。
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 5%

---

# AEM Formsワークフローのログイン{#logging-in-aem-forms-workflows}

Formsのワークフローステップでは、ワークフロー関連の問題をデバッグするための詳細なログが便利に提供されます。 AEM Formsワークフローのデバッグログを有効にしてログを表示します。

デフォルトでは、すべてのログ情報は&#x200B;**error.log**&#x200B;ファイル（*/crx-repository/logs/*&#x200B;ディレクトリ）にあります。

フォームワークフローのデバッグログには、次のものが含まれます。

* 各ワークフローステップのエントリ。 以下に例を示します。\
   `[DEBUG] "Executing Invoke DDX Process step"`

* 各ワークフローステップの終了 以下に例を示します。\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* サービス呼び出しメッセージ。 以下に例を示します。\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* サービス終了メッセージ。 以下に例を示します。\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* メタデータマップから読み取られた変数。 以下に例を示します。\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* JCRリポジトリで書き込まれる変数。 以下に例を示します。

   ```verilog
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* 完全なスタックトレースを含む例外メッセージ。 以下に例を示します。\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 動的ステップのメタデータパラメータ。 以下に例を示します。

   ```verilog
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

次の例は、ドキュメントに署名ステップのログを示しています。

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

* 正しいAdobe Sign設定を使用している。
* Adobe Signサービスは、契約の作成に成功すると終了します。
* ドキュメントに署名ステップは、成功メッセージと共に終了します。

例外がある場合は、完全なスタックトレースを表示して、エラーの原因を評価できます。

## AEM Formsワークフローのデバッグログを有効にする{#enable-debug-logging-for-aem-forms-workflows}

AEM Formsワークフローのデバッグログを有効にするには、次の手順を実行します。

1. AEM Webコンソール設定マネージャー( )に移動します。

   https://&#39;[server]:[port]&#39;/system/console/configMgr

1. **[!UICONTROL Sling]** > **[!UICONTROL Log Support]**&#x200B;を選択します。
1. **[!UICONTROL 「新しいロガーを追加」をタップします。]**
1. 「**[!UICONTROL ログレベル]**」として「**[!UICONTROL デバッグ]**」を選択します。
1. ログファイルの場所を指定します。 ログファイルのデフォルトの場所は次のとおりです。*logs\error.log*
1. **[!UICONTROL Logger]**&#x200B;列に&#x200B;**com.adobe.granite.workflow.core**&#x200B;というパッケージ名を指定します。

   これらの手順を実行すると、**com.adobe.granite.workflow.core**&#x200B;パッケージのデバッグログを保存できます。 **[!UICONTROL +]**&#x200B;をタップし、次のパッケージ名をリストに追加します。

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
