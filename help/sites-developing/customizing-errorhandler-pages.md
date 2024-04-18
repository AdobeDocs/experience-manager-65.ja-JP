---
title: エラーハンドラーによって表示されるページのカスタマイズ
description: Adobe Experience Manager には、HTTP エラーを処理するための標準のエラーハンドラーが組み込まれています。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 100%

---

# エラーハンドラーによって表示されるページのカスタマイズ{#customizing-pages-shown-by-the-error-handler}

Adobe Experience Manager（AEM）には、HTTP エラーを処理するための標準的なエラーハンドラーが付属しています。例えば、次のようなメッセージが表示されます。

![chlimage_1-67](assets/chlimage_1-67a.png)

エラーコードに応答するシステム提供のスクリプトが（`/libs/sling/servlet/errorhandler` の下に）あります。標準の CQ インスタンスでは、デフォルトで次のスクリプトを使用できます。

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM は Apache Sling に基づいています。そのため、Sling エラー処理について詳しくは、[エラー処理](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)を参照してください。

>[!NOTE]
>
>オーサーインスタンスでは、[CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md) がデフォルトで有効になっています。これにより、常に応答コード 200 を返します。デフォルトのエラーハンドラーは、応答に対してフルスタックトレースを書き込むことで応答します。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は、有効として設定されている場合も含めて&#x200B;*常に*&#x200B;無効になります。

## エラーハンドラーによって表示されるページのカスタマイズ方法 {#how-to-customize-pages-shown-by-the-error-handler}

独自のスクリプトを作成して、エラーの発生時にエラーハンドラーで表示されるページをカスタマイズできます。カスタマイズしたページが `/apps` の下に作成され、デフォルトのページ（`/libs` の下）をオーバーレイします。

>[!NOTE]
>
>詳しくは、[オーバーレイの使用](/help/sites-developing/overlays.md)を参照してください。

1. リポジトリ内で、デフォルトスクリプトを次のようにコピーします。

   * コピー元：`/libs/sling/servlet/errorhandler/`
   * コピー先：`/apps/sling/servlet/errorhandler/`

   コピー先のパスはデフォルトでは存在しないので、最初は作成する必要があります。

1. `/apps/sling/servlet/errorhandler` に移動して、次のいずれかの操作を行います。

   * 既存のスクリプトを編集し、必要な情報を追加します。
   * 必要とするコード用に新しいスクリプトを作成し、編集します。

1. 変更を保存し、テストします。

>[!CAUTION]
>
>404.jsp および 403.jsp ハンドラーは、CQ5 認証に合わせて設計されています。特に、これらのエラーの発生時にシステムログインができるようになっています。
>
>そのため、これらの 2 つのハンドラーを置き換える際には十分に気をつけて作業してください。

### HTTP 500 エラーへの応答のカスタマイズ {#customizing-the-response-to-http-errors}

HTTP 500 エラーはサーバーサイドの例外によって発生します。

* **[500 内部サーバーエラー](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
サーバーで予期しない状況が発生したので、要求を処理できません。

リクエストの処理で例外が発生した場合、Apache Sling フレームワーク（AEM の基盤）は次の処理を実行します。

* 例外をログに記録します
* 以下のものを返します

   * HTTP 応答コード 500
   * 例外スタックトレース

  これらを応答の本文に返します。

[エラーハンドラーで表示されるページをカスタマイズする](#how-to-customize-pages-shown-by-the-error-handler)ことで、`500.jsp` スクリプトを作成できます。ただし、このスクリプトが使用されるのは、`HttpServletResponse.sendError(500)` が明示的に（例外キャッチャーから）実行される場合に限ります。

それ以外の場合は、応答コードは 500 に設定されますが、`500.jsp` スクリプトは実行されません。

500 エラーを処理するには、エラーハンドラースクリプトのファイル名を例外クラス（またはスーパークラス）と同じにする必要があります。このような例外をすべて処理するには、スクリプト `/apps/sling/servlet/errorhandler/Throwable.js`p または `/apps/sling/servlet/errorhandler/Exception.jsp` を作成します。

>[!CAUTION]
>
>オーサーインスタンスでは、[CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md) はデフォルトで有効になっています。これにより、常に応答コード 200 を返します。デフォルトのエラーハンドラーは、応答に対してフルスタックトレースを書き込むことで応答します。
>
>カスタムエラーハンドラーの場合、コード 500 を含む応答が必要です。そのため、[CQ WCM Debug Filter を無効にする必要があります](/help/sites-deploying/osgi-configuration-settings.md)。そうすることで、応答コード 500 が返され、それによって正しい Sling エラーハンドラーがトリガーされます。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は、有効として設定されている場合も含めて&#x200B;*常に*&#x200B;無効になります。
