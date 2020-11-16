---
title: エラーハンドラーによって表示されるページのカスタマイズ
seo-title: エラーハンドラーによって表示されるページのカスタマイズ
description: AEM には、HTTP エラーを処理するための標準のエラーハンドラーが組み込まれています
seo-description: AEM には、HTTP エラーを処理するための標準のエラーハンドラーが組み込まれています
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 72%

---


# エラーハンドラーによって表示されるページのカスタマイズ{#customizing-pages-shown-by-the-error-handler}

AEMには、HTTPエラーを処理するための標準的なエラーハンドラが付属しています。例えば、次のように表示します。

![chlimage_1-67](assets/chlimage_1-67a.png)

System provided scripts exist (under `/libs/sling/servlet/errorhandler`) to respond to error codes, by default the following are available with a standard CQ instance:

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM is based on Apache Sling, so see [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) for detailed information about Sling Error Handling.

>[!NOTE]
>
>オーサーインスタンスでは、[CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md) がデフォルトで有効です。このフィルターは常に応答コード 200 を返します。デフォルトのエラーハンドラーは、応答に対してフルスタックトレースを書き込むことで応答します。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は、有効として設定されている場合も含めて常に無効になります。**

## エラーハンドラーによって表示されるページのカスタマイズ方法 {#how-to-customize-pages-shown-by-the-error-handler}

エラーが発生した場合にエラーハンドラーによって表示されるページをカスタマイズする独自のスクリプトを作成できます。 カスタマイズしたページは、デフォルトのページ(下 `/apps` のページ)の下に作成され、オーバーレイ `/libs`されます。

>[!NOTE]
>
>詳しくは、[オーバーレイの使用方法](/help/sites-developing/overlays.md)を参照してください。

1. リポジトリ内で、デフォルトスクリプトをコピーします。

   * `/libs/sling/servlet/errorhandler/` から
   * を `/apps/sling/servlet/errorhandler/`

   コピー先のパスはデフォルトでは存在しないので、最初は作成する必要があります。

1. `/apps/sling/servlet/errorhandler` に移動します。次のどちらかを実行します。

   * 既存のスクリプトを編集し、必要な情報を追加します。
   * 必要とするコード用に新しいスクリプトを作成し、編集します。

1. 変更を保存し、テストします。

>[!CAUTION]
>
>404.jsp および 403.jsp ハンドラーは、CQ5 認証に合わせて設計されています。特に、これらのエラーの発生時にシステムログインができるようになっています。
>
>そのため、これらの 2 つのハンドラーを置き換える際には十分に気をつけて作業してください。

### HTTP 500 エラーへの応答のカスタマイズ {#customizing-the-response-to-http-errors}

HTTP 500 エラーはサーバー側の例外によって発生します。

* **[500 内部サーバーエラー](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
サーバーで予期しない状況が発生したので、要求を処理できません。

要求処理の結果例外が発生した場合、Apache Slingフレームワーク(AEMが構築されているフレームワーク):

* 例外をロギングします。
* 次を返します。

   * HTTP 応答コード 500
   * 例外スタックトレース

   これらは応答の本文内で返されます。

[エラーハンドラーによって表示されるページをカスタマイズする](#how-to-customize-pages-shown-by-the-error-handler)ことで、`500.jsp` スクリプトを作成できます。However, it is only used if `HttpServletResponse.sendError(500)` is executed explicitly; i.e. from an exception catcher.

それ以外の場合は、応答コードは に設定されますが、`500.jsp`500.  スクリプトは実行されません。

500 エラーを処理するには、エラーハンドラースクリプトの名前を例外クラス（またはスーパークラス）と同じにする必要があります。このような例外をすべて処理するには、スクリプト `/apps/sling/servlet/errorhandler/Throwable.js`pまたはを作成し `/apps/sling/servlet/errorhandler/Exception.jsp`ます。

>[!CAUTION]
>
>オーサーインスタンスでは、[CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md) がデフォルトで有効です。このフィルターは常に応答コード 200 を返します。デフォルトのエラーハンドラーは、応答に対してフルスタックトレースを書き込むことで応答します。
>
>カスタムエラーハンドラーの場合、コード 500 を含む応答が必要です。そのため、[CQ WCM Debug Filter を無効にする必要があります](/help/sites-deploying/osgi-configuration-settings.md)。そうすることで、応答コード 500 が返され、それによって正しい Sling エラーハンドラーがトリガーされます。
>
>パブリッシュインスタンスでは、CQ WCM Debug Filter は、有効として設定されている場合も含めて常に無効になります。**

