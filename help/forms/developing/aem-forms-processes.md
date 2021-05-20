---
title: AEM Formsプロセスについて
seo-title: AEM Formsプロセスについて
description: AEM Formsプロセスについて
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
role: Developer
exl-id: 434ac316-8a01-43a6-844b-1b792f60fa21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 2%

---

# AEM Formsプロセスについて{#understanding-aem-forms-processes}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

一般的な使用例としては、一連のAEM Formsサービスが1つのドキュメントに対して操作をおこなう場合が考えられます。 Workbenchを使用してプロセスを作成することで、サービスコンテナにリクエストを送信できます。 プロセスとは、自動化するビジネスプロセスを表します。 プロセスの作成について詳しくは、[Workbenchの使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください。

プロセスがアクティブ化されると、そのプロセスはサービスになり、他のサービスと同様に呼び出すことができます。 Encryptionサービスなどの標準サービスと、プロセスから生成されるサービスの違いの1つは、多くのアクションを実行する1つの操作が後者にある点です。 一方、標準的なサービスには多くの操作があります。 通常、各操作は、ドキュメントへのポリシーの適用やドキュメントの暗号化など、1つの操作を実行します。

プロセスは、短時間のみ有効でも長期間有効でもかまいません。 短時間のみ有効なプロセスとは、呼び出されたのと同じ実行スレッドで同期的に実行される操作です。 短時間のみ有効な操作は、ほとんどのプログラミング言語で見られる標準的な動作に相当します。クライアントアプリケーションがメソッドを呼び出し、戻り値を待ちます。

ただし、次の要因が原因で、プロセスを同期的に完了できない場合があります。

* 1つのプロセスは相当な時間を要する場合があります。
* プロセスは組織の境界をまたぐ場合があります。
* プロセスを終了するには、外部入力が必要です。 例えば、不在のマネージャーにフォームが送信される場合を考えます。 この場合、マネージャーがフォームに入力して戻るまで、プロセスは完了しません。

   このタイプのプロセスは、長期間有効なプロセスと呼ばれます。 長期間有効なプロセスは非同期で実行され、リソースの許可に応じてシステムがやり取りし、操作の追跡と監視が可能になります。 長期間有効なプロセスが呼び出されると、AEM Formsは、長期間有効なプロセスステータスを追跡するレコードの一部として呼び出し識別子の値を作成します。 レコードはAEM Formsデータベースに保存されます。 長期間有効なプロセスレコードは、不要になったときに削除できます。

>[!NOTE]
>
>AEM Formsは、短時間のみ有効なプロセスが呼び出された場合に、レコードを作成しません。

呼び出し識別子の値を使用して、長期間有効なプロセスのステータスを追跡できます。 例えば、プロセス呼び出し識別子の値を使用して、実行中のプロセスインスタンスの終了など、Process Managerの操作を実行できます。

**短時間のみ有効なプロセスの例**

次の図は、*MyApplication/EncryptDocument*&#x200B;という短時間のみ有効なプロセスの例です。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このプロセスの呼び出し方法を説明するコード例に従うには、Workbenchを使用して`MyApplication/EncryptDocument`という名前のプロセスを作成します。 （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

この短時間のみ有効なプロセスが呼び出されると、次のアクションが実行されます。

1. プロセスに渡される、保護されていないPDFドキュメントを入力値として取得します。
1. PDF ドキュメントをパスワードで暗号化します。このプロセスの入力パラメーターの名前は`inDoc`で、データタイプはdocumentです。
1. パスワードで暗号化されたPDFドキュメントをPDFファイルとしてローカルファイルシステムに保存します。 このプロセスは、暗号化されたPDFドキュメントを出力値として返します。 このプロセスの出力パラメーターの名前は`outDoc`で、データタイプはdocumentです。

   このプロセスは、呼び出されたのと同じ実行スレッドで同期的に完了します。 この短時間のみ有効なプロセスの名前は`MyApplication/EncryptDocument`で、操作は`invoke`です。

   >[!NOTE]
   >
   >通常、短時間のみ有効なプロセスは3つ以上のアクションで構成されます。 Workbenchを使用してプロセスを作成します。 （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

   *AEM formsによるプログ*&#x200B;ラミングでは、この短時間のみ有効なプロセスをプログラムで呼び出す次の方法について説明します。

   * [AEM Forms Remotingを使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (Flexアプリケーションの使用)
   * [呼び出しAPI（Java呼び出しAPI）を使用した短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) 
   * [Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （Webサービスの例）
   * [MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （Webサービスの例）
   * [SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （Webサービスの例）
   * [HTTP経由でのBLOBデータを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （Webサービスの例）
   * [DIMEを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （Webサービスの例）
   * [RESTを使用したMyApplication/EncryptDocumentプロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-rest.md)

**長期間有効なプロセスの例**

次の図は、長期間有効なプロセスの例です。

このプロセスは、申込者がローンフォームを送信すると呼び出されます。 ローン担当者がローン申し込みを承認または拒否するまで、プロセスは完了しません。 この長期間有効なプロセスの名前は&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;で、操作は`invoke_Async`です。 このプロセスは非同期で呼び出す必要があります。 この長期間有効なプロセスをプログラムで呼び出す方法については、[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照してください。

>[!NOTE]
>
>このプロセスは、[最初のAEM Formsアプリケーションの作成](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)で指定したチュートリアルに従って作成できます。
