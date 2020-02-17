---
title: AEM Formsワークフローへのログイン
seo-title: AEM Formsワークフローへのログイン
description: ログを使用して、AEM Formsワークフローの問題をデバッグします。
seo-description: ログを使用して、AEM Formsワークフローの問題をデバッグします。
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# AEM Formsワークフローへのログイン{#logging-in-aem-forms-workflows}

フォームワークフローの手順では、ワークフロー関連の問題をデバッグするための詳細なログが便利に提供されます。 AEM Formsワークフローのデバッグログを有効にしてログを表示します。

By default, all logging information is available in the **error.log** file at the */crx-repository/logs/* directory.

フォームワークフローのデバッグログには、次の情報が含まれます。

* 各ワークフロー手順のエントリ。 次に例を示します。\
   `[DEBUG] "Executing Invoke DDX Process step"`

* 各ワークフロー手順の終了。 次に例を示します。\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* サービス呼び出しメッセージ。 次に例を示します。\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* サービス終了メッセージ 次に例を示します。\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* メタデータマップから読み取る変数。 次に例を示します。\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* JCRリポジトリに書き込まれた変数。 次に例を示します。

   ```
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* 完全なスタックトレースを含む例外メッセージ。 次に例を示します。\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 動的ステップのメタデータパラメータ。 次に例を示します。

   ```
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

次の例は、「ドキュメントに署名」手順のログを示しています。

```xml
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

ログを使用して、次の項目を評価します。

* 正しいアドビ署名設定を使用している。
* 契約書が正常に作成されると、Adobe signサービスは終了します。
* 「ドキュメントに署名」ステップが終了し、成功メッセージが表示されます。

例外が発生した場合は、完全なスタックトレースを表示して、エラーの原因を評価できます。

## AEM Formsワークフローのデバッグログの有効化 {#enable-debug-logging-for-aem-forms-workflows}

次の手順を実行して、AEM Formsワークフローのデバッグログを有効にします。

1. AEM Web Console Configuration Manager(

   https://[server]:[port]/system/console/configMgr

1. Sling **[!UICONTROL /]** Log Supportを選択します ****。
1. Tap **[!UICONTROL Add new Logger.]**
1. 「 **[!UICONTROL Log]** Level」として「 **[!UICONTROL Debug」を選択します]**。
1. ログファイルの場所を指定します。 ログファイルのデフォルトの場所は次のとおりです。 *logs\error.log*
1. パッケージの名前を **com.adobe.granite.workflow.core** ( **[!UICONTROL Logger]** )列に指定します。

   次の手順を実行すると、 **com.adobe.granite.workflow.coreパッケージのデバッグログを保存できます** 。 「 **[!UICONTROL +」をタ]** ップし、次のパッケージ名をリストに追加します。

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace

