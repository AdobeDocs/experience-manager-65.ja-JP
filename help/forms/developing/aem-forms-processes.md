---
title: AEM Formsプロセスについて
seo-title: AEM Formsプロセスについて
description: 'null'
seo-description: 'null'
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# AEM Formsプロセスについて {#understanding-aem-forms-processes}

一般的な使用例は、AEM Formsサービスのセットが1つのドキュメントを操作する場合です。 Workbenchを使用してプロセスを作成することで、サービスコンテナにリクエストを送信できます。 プロセスは、自動化するビジネスプロセスを表します。 プロセスの作成について詳しくは、「Workbenchの使用」を [参照してください](https://www.adobe.com/go/learn_aemforms_workbench_63)。

プロセスがアクティブ化されると、そのプロセスはサービスになり、他のサービスと同様に呼び出すことができます。 Encryptionサービスなどの標準サービスとプロセスに由来するサービスの違いの1つは、後者には1つの操作で多くのアクションを実行できる点です。 これに対し、標準的なサービスには多くの操作があります。 通常、各操作は1つの操作（ドキュメントへのポリシーの適用やドキュメントの暗号化など）を実行します。

プロセスには、短時間のみ有効なプロセスと長期間有効なプロセスがあります。 短時間のみ有効なプロセスとは、呼び出し元の同じ実行スレッドで同期的に実行される操作です。 短時間のみ有効な操作は、クライアントアプリケーションがメソッドを呼び出して戻り値を待つ、ほとんどのプログラミング言語での標準的な動作と同じです。

ただし、次のような要因が原因で、プロセスを同期的に完了できない状況があります。

* プロセスは、かなりの期間に及ぶ場合があります。
* プロセスは組織の境界をまたぐことができます。
* プロセスを終了するには、外部入力が必要です。 例えば、不在の管理者にフォームが送信される場合を考えてみます。 この場合、マネージャーがフォームを返して入力するまで、プロセスは完了しません。

   この種のプロセスは、長期間有効なプロセスと呼ばれます。 長期間有効なプロセスは非同期で実行され、リソースの許容範囲内でシステムがやり取りし、操作の追跡と監視を行うことができます。 長期間有効なプロセスが呼び出されると、AEM Formsは、長期間有効なプロセスステータスを追跡するレコードの一部として呼び出し識別子の値を作成します。 レコードはAEM formsデータベースに保存されます。 長期間有効なプロセスレコードは、不要になった場合に削除できます。

   **注意**:短時間のみ有効なプロセスが呼び出された場合、AEM Formsはレコードを作成しません。

   呼び出し識別子の値を使用して、長期間有効なプロセスのステータスを追跡できます。 例えば、プロセス呼び出し識別子の値を使用して、実行中のプロセスインスタンスの終了など、Process Manager操作を実行できます。

**短時間のみ有効なプロセスの例**

次の図は、 *MyApplication/EncryptDocumentという短時間のみ有効なプロセスの例です*。

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このプロセスの呼び出し方法について説明するコード例に従うには、Workbenchを使用して名前を付けたプロセスを `MyApplication/EncryptDocument` 作成します。 （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

この短時間のみ有効なプロセスを呼び出すと、次のアクションが実行されます。

1. プロセスに渡される、保護されていないPDFドキュメントを入力値として取得します。
1. PDF ドキュメントをパスワードで暗号化します。このプロセスの入力パラメーターの名前は `inDoc` で、データタイプはdocumentです。
1. パスワードで暗号化されたPDFドキュメントをPDFファイルとしてローカルファイルシステムに保存します。 このプロセスは、暗号化されたPDFドキュメントを出力値として返します。 このプロセスの出力パラメーターの名前はで `outDoc` 、データタイプはdocumentです。

   このプロセスは、呼び出し元の同じ実行スレッドで同期的に完了します。 この短時間のみ有効なプロセスの名前はで、 `MyApplication/EncryptDocument`その操作はです `invoke`。

   >[!NOTE]
   >
   >通常、短時間のみ有効なプロセスは3つ以上のアクションで構成されます。 プロセスはWorkbenchを使用して作成します。 （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

   *AEM formsによるプログラミ*&#x200B;ングでは、この短時間のみ有効なプロセスをプログラムで呼び出す次の方法について説明します。

   * [AEM Forms Remotingを使用して保護されていないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) （Flexアプリケーションを使用）
   * [呼び出しAPI](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) (Java Invocation API)を使用した短時間のみ有効なプロセスの呼び出し
   * [Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （Webサービスの例）
   * [MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （Webサービスの例）
   * [SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （Webサービスの例）
   * [HTTP経由のBLOBデータを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （Webサービスの例）
   * [DIMEを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （Webサービスの例）
   * [RESTを使用したMyApplication/EncryptDocumentプロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-rest.md)

**長期間有効なプロセスの例**

次の図は、長期間有効なプロセスの例です。

このプロセスは、申込者がローンフォームを送信したときに呼び出されます。 ローン担当者がローン要求を承認または拒否するまで、処理は完了しません。 この長期間有効なプロセスの名前は *FirstAppSolution/PreLoanProcessで* 、操作はです `invoke_Async`。 このプロセスは、非同期で呼び出す必要があります。 For information about programmatically invoking this long-lived process, see [Invoking Human-Centric Long-Lived Processes](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>このプロセスは、「最初のAEM Formsアプリケーションの作成」で指定さ [れたチュートリアルに従って作成できます](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)。