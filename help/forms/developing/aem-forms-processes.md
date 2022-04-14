---
title: AEM Forms プロセスについて
seo-title: Understanding AEM Forms Processes
description: AEM Forms プロセスについて
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
role: Developer
exl-id: 434ac316-8a01-43a6-844b-1b792f60fa21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '803'
ht-degree: 100%

---

# AEM Forms プロセスについて {#understanding-aem-forms-processes}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

使用例として一般的なのは、一連の AEM Forms サービスが単一のドキュメントを操作するというものです。Workbench を使用してプロセスを作成することで、サービスコンテナにリクエストを送信できます。1 つのプロセスが、自動化対象の 1 つのビジネスプロセスを表します。プロセスの作成について詳しくは、[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63_jp)を参照してください。

プロセスがアクティブ化されると、そのプロセスはサービスになり、他のサービスと同様に呼び出すことができます。Encryption サービスなどの標準サービスと、プロセスから生成されるサービスとの違いの 1 つは、後者には多くのアクションを実行する 1 つの操作があるという点です。これに対し、標準のサービスには多くの操作があります。通常、各操作は 1 つのアクション（ドキュメントへのポリシーの適用やドキュメントの暗号化など）を実行します。

プロセスは、短時間のみ有効なものでも長期間有効なものでもかまいません。短時間のみ有効なプロセスとは、同期的に実行される操作のことで、呼び出し元と同じ実行スレッドで実行される操作です。短時間のみ有効な操作は、ほとんどのプログラミング言語で見られる標準的な動作に相当します。つまり、クライアントアプリケーションがメソッドを呼び出し、戻り値を待つ動作です。

ただし、次のような要因により、プロセスを同期的に完了できない場合があります。

* プロセスが長い時間を要する。
* プロセスが、複数の組織にまたがっている。
* プロセスを完了するには、他人による入力が必要。例えば、外出中の上司にフォームを送信した場合を考えてみましょう。この場合、上司が帰社しフォームを入力するまで、プロセスは完了しません。

   こうしたタイプのプロセスは、長期間有効なプロセスと呼ばれます。 長期間有効なプロセスは非同期で実行されるため、システムはリソースの余裕があるときに処理することができ、操作の追跡や監視をすることも可能です。長期間有効なプロセスが呼び出されると、AEM Forms は、長期間有効なプロセスのステータスを追跡するレコードの一部として、呼び出し識別子の値を作成します。レコードは AEM Forms データベースに保存されます。長期間有効なプロセスレコードは、不要になればパージできます。

>[!NOTE]
>
>短時間のみ有効なプロセスを呼び出した場合は、AEM Forms でレコードは作成されません。

呼び出し識別子の値を使用して、長期間有効なプロセスのステータスを追跡できます。例えば、プロセス呼び出し識別子の値を使用して、実行中のプロセスインスタンスの終了などといった Process Manager の操作を実行できます。

**短時間のみ有効なプロセスの例**

以下の図は、*MyApplication/EncryptDocument* という名前の短時間のみ有効なプロセスの例です。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスには基づいていません。このプロセスを呼び出す方法を説明するコード例に沿って理解を深めるには、Workbench を使用して `MyApplication/EncryptDocument` という名前のプロセスを作成します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63_jp)を参照してください）。

この短時間のみ有効なプロセスを呼び出すと、次のアクションを実行します。

1. プロセスに入力値として渡された保護されていない PDF ドキュメントを取得します。
1. この PDF ドキュメントにパスワードを指定して暗号化します。このプロセスの入力パラメーターの名前は `inDoc` で、データタイプは document です。
1. パスワードで暗号化した PDF ドキュメントを PDF ファイルとしてローカルファイルシステムに保存します。このプロセスでは、暗号化された PDF ドキュメントが出力値として返されます。このプロセスの出力パラメーターの名前は `outDoc` で、データタイプは document です。

   このプロセスは、呼び出し元と同じ実行スレッドで同期的に完了します。この短時間のみ有効なプロセスの名前は `MyApplication/EncryptDocument` で、操作の名前は `invoke` です。

   >[!NOTE]
   >
   >通常、短時間のみ有効なプロセスは 3 つより多くのアクションで構成されます。プロセスを作成する際は、Workbench を使用します。（[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63_jp)を参照してください）。

   *AEM Forms によるプログラミング*&#x200B;では、この短時間のみ有効なプロセスをプログラムで呼び出すことができる次の方法について説明しています。

   * [AEM Forms Remoting を使用して保護されていないドキュメントを渡すことにより、短時間のみ有効なプロセスを呼び出す](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)（Flex アプリケーションを使用）
   * [呼び出し API を使用した短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api)（Java 呼び出し API）
   * [Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)（web サービスの例）
   * [MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （web サービスの例）
   * [SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （web サービスの例）
   * [HTTP 経由での BLOB データを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （web サービスの例）
   * [DIME を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （web サービスの例）
   * [REST を使用した MyApplication/EncryptDocument プロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-rest.md)

**長期間有効なプロセスの例**

次の図は、長期間有効なプロセスの例です。

このプロセスは、申込者がローンフォームを送信すると呼び出されます。ローン担当者がローン申し込みを承認または却下するまで、処理は完了しません。この長期間有効なプロセスの名前は *FirstAppSolution/PreLoanProcess* でその動作は `invoke_Async` です。このプロセスは非同期で呼び出す必要があります。プログラムによる長期間有効なプロセスの呼び出しの詳細については、[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照してください。

>[!NOTE]
>
>このプロセスは、[初めての AEM Forms アプリケーションの作成](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)で指定されたチュートリアルに従って作成できます。
