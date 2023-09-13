---
title: エラーハンドラーによって表示されるページのカスタマイズ
description: Adobe Experience Managerには、HTTP エラーを処理するための標準的なエラーハンドラーが用意されています。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 31%

---

# エラーハンドラーによって表示されるページのカスタマイズ{#customizing-pages-shown-by-the-error-handler}

Adobe Experience Manager(AEM) には、HTTP エラーを処理するための標準的なエラーハンドラーが付属しています。例えば、次のエラーを示します。

![chlimage_1-67](assets/chlimage_1-67a.png)

エラーコードに応答するシステム提供のスクリプトが（`/libs/sling/servlet/errorhandler` の下に）あります。標準の CQ インスタンスでは、デフォルトで次のスクリプトを使用できます。

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEMは Apache Sling に基づいています。 そのため、 [エラー処理](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html) を参照してください。

>[!NOTE]
>
>オーサーインスタンスでは、 [CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md) はデフォルトで有効になっています。 これにより、常に応答コード 200 が生成されます。 デフォルトのエラーハンドラーは、応答に完全なスタックトレースを書き込むことで応答します。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は次のようになります。 *常に* 無効（有効に設定されている場合も含む）

## エラーハンドラーによって表示されるページをカスタマイズする方法 {#how-to-customize-pages-shown-by-the-error-handler}

独自のスクリプトを作成して、エラーの発生時にエラーハンドラーで表示されるページをカスタマイズできます。カスタマイズしたページは、の下に作成されます。 `/apps` デフォルトのページ ( `/libs`) をクリックします。

>[!NOTE]
>
>詳しくは、 [オーバーレイの使用](/help/sites-developing/overlays.md) を参照してください。

1. リポジトリで、デフォルトのスクリプトをコピーします。

   * コピー元：`/libs/sling/servlet/errorhandler/`
   * コピー先：`/apps/sling/servlet/errorhandler/`

   デフォルトでは宛先パスは存在しないので、初めてこの処理を行う際に作成する必要があります。

1. に移動します。 `/apps/sling/servlet/errorhandler` 次のいずれかの操作を行います。

   * 必要な情報を指定できるように、適切な既存のスクリプトを編集します。
   * 必要なコードの新しいスクリプトを作成および編集します。

1. 変更を保存し、テストします。

>[!CAUTION]
>
>404.jsp および 403.jsp ハンドラーは、CQ5 認証に対応するように設計されています。特に、これらのエラーが発生した場合にシステムログインを許可するためです。
>
>したがって、これら 2 つのハンドラーの交換は慎重に行う必要があります。

### HTTP 500 エラーへの応答のカスタマイズ {#customizing-the-response-to-http-errors}

HTTP 500 エラーはサーバー側の例外が原因で発生します。

* **[500 内部サーバーエラー](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
サーバーで予期しない状況が発生したので、要求を処理できません。

リクエストの処理で例外が発生した場合、Apache Sling フレームワーク（AEM の基盤）は次の処理を実行します。

* 例外をログに記録します。
* 戻り値：

   * HTTP 応答コード 500
   * 例外スタックトレース

  応答の本文に含まれます。

[エラーハンドラーで表示されるページをカスタマイズする](#how-to-customize-pages-shown-by-the-error-handler)ことで、`500.jsp` スクリプトを作成できます。ただし、次の場合にのみ使用されます。 `HttpServletResponse.sendError(500)` が明示的に実行されます。つまり、例外キャッチャーから実行されます。

それ以外の場合は、応答コードは 500 に設定されますが、`500.jsp` スクリプトは実行されません。

500 エラーを処理するには、エラーハンドラースクリプトのファイル名を例外クラス（またはスーパークラス）と同じにする必要があります。このような例外をすべて処理するには、スクリプトを作成します `/apps/sling/servlet/errorhandler/Throwable.js`p または `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>オーサーインスタンスでは、 [CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md) はデフォルトで有効になっています。 これにより、常に応答コード 200 が生成されます。 デフォルトのエラーハンドラーは、応答に完全なスタックトレースを書き込むことで応答します。
>
>カスタムのエラーハンドラーの場合、コード 500 を含む応答が必要なので、 [CQ WCM Debug Filter を無効にする必要があります](/help/sites-deploying/osgi-configuration-settings.md). これにより、応答コード 500 が返され、その結果、正しい Sling error-handler がトリガーされます。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は次のようになります。 *常に* 無効（有効に設定されている場合も含む）
