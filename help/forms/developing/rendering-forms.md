---
title: フォームのレンダリング
seo-title: フォームのレンダリング
description: 'null'
seo-description: 'null'
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# フォームのレンダリング {#rendering-forms}

**Formsサービスについて**

Formsサービスを使用すると、通常はDesignerで作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。 フォーム作成者は、Formsサービスが様々なブラウザー環境でPDF、SWFまたはHTMLでレンダリングする単一のフォームデザインを開発できます。

エンドユーザーがフォームを要求すると、クライアントアプリケーションはFormsサービスに要求を送信し、Formsサービスは適切な形式でフォームを返します。 Formsサービスは、要求を受け取るとすぐに、データをフォームデザインとマージし、目的の形式でフォームを配信します。 Formサービスの出力はインタラクティブフォームで、通常はPDFドキュメントです。 インタラクティブフォームを使用すると、ユーザーはフォーム上のフィールドに入力できます。

クライアントアプリケーションの種類に応じて、フォームをクライアントWebブラウザーに書き込んだり、フォームをPDFファイルとして保存したりできます。 Webベースのアプリケーションは、Webブラウザーにフォームを書き込むことができます。 デスクトップアプリケーションは、フォームをPDFファイルとして保存できます。 WebブラウザーとPDFファイルに書き出す方法を示すために、「 *Rendering Forms* 」セクションのクイック開始は次のように整理されています。

* 厳密に型指定されたJava API（SOAPモード）の例は、Javaサーブレットです。
* Webサービス(Java Base64)の例はJavaサーブレットです。
* Webサービス(MTOM)の例は、コンソールアプリケーションです(すべてのクイック開始にMTOMの例があるわけではありません)。

>[!NOTE]
>
> Javaサーブレットを使用してFormsサービスを呼び出すWebアプリケーションの作成について詳しくは、「フォームをレンダリングする [Web アプリケーションの作成」を参照してくださ](/help/forms/developing/creating-web-applications-renders-forms.md)い。

フォームデザイン（XDPファイル）またはPDFドキュメントをFormsサービスに渡すには、次の2つの方法があります。

* URL値を使用してフォームデザインを参照できます。 この方法では、オブジェクトを使用 `URLSpec` します。 コンテンツルートは、オブジェクトのメソッドを使用してForms `URLSpec` サービスに渡さ `setContentRootURI` れます。 フォームデザイン名( `formQuery`)は、別のパラメーターとして渡されます。 2つの値が連結され、フォームデザインの絶対参照が取得されます。 (「フォームのレンダリング」セクションにあるクイッ *ク開始のほとんどは* 、この方法を使用します)。
* フォームデザインを含 `com.adobe.idp.Document` むフォームをFormsサービスに渡すことができます。 フォームデザインを含むオブジ `renderPDFForm2` ェクトを、と `renderHTMLForm2` いう名前で受け取 `com.adobe.idp.Document` る2つの新しいメソッドが追加されました。 (Formsサービ [スへのドキュメントの引き渡しを参照)。](/help/forms/developing/passing-documents-forms-service.md)

Formsサービスを使用して、次のタスクを実行できます。

* インタラクティブPDFフォームのレンダリング (インタラクティブPDF [フォームのレンダリングを参照](/help/forms/developing/rendering-interactive-pdf-forms.md))。
* クライアントでフォームをレンダリングします。 (「クライアント [でのフォームのレンダリング](/help/forms/developing/rendering-forms-client.md)」を参照)。
* フラグメントに基づいてフォームをレンダリングする。(See [Rendering Forms Based on Fragments](/help/forms/developing/rendering-forms-based-fragments.md).)
* 権限を付与されたフォームをレンダリングします。 (権限を付与さ [れたフォームのレンダリングを参照](/help/forms/developing/rendering-rights-enabled-forms.md))。
* フォームをHTMLとしてレンダリングする。 (「フォーム [のHTMLとしてのレンダリング](/help/forms/developing/rendering-forms-html.md)」を参照)。
* カスタムCSSファイルを使用したHTMLフォームのレンダリング([カスタムCSSファイルを使用したHTMLフォームのレンダリング](/help/forms/developing/rendering-html-forms-using-custom.md))
* 送信されたフォームを処理します。 (送信済みのフ [ォームの処理を参照](/help/forms/developing/handling-submitted-forms.md))。
* 送信されたXMLドキュメントを使用したPDFデータの作成を参照してください。 (送信済みXML [ドキュメントを使用したPDFデータの作成を参照](/help/forms/developing/creating-pdf-documents-submitted-xml.md))。
* フォームの自動埋め込み (編集可能な [レイアウトでのフォームの自動埋め込みを参照](/help/forms/developing/prepopulating-forms-flowable-layouts.md))。
* 渡すドキュメント。 (Formsサービ [スへのドキュメントの引き渡しを参照)。](/help/forms/developing/passing-documents-forms-service.md)
* フォームデータを計算します。 (Calculating [Form Data](/help/forms/developing/calculating-form-data.md)を参照)。
* アプリの最適化を参照してください。 (「Formsサ [ービスのパフォーマンスの最適化](/help/forms/developing/optimizing-performance-forms-service.md)」を参照)。

   ***ヒント&#x200B;**:Adobe Developer Webサイトには、Formsサービスを呼び出してフォームをレンダリングするASP.NETアプリケーションの作成方法を説明する次の記事が含まれています。 フォーム[レンダリングASP.NETアプリケーションの作成を参照してくださ](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)い。*

