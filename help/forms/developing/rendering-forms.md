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
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

---


# フォームのレンダリング {#rendering-forms}

**Formsサービスについて**

Formsサービスを使用すると、通常はDesignerで作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。 フォーム作成者は、Formsサービスが様々なブラウザー環境のPDF、SWFまたはHTMLでレンダリングする単一のフォームデザインを開発できます。

エンドユーザーがフォームを要求すると、クライアントアプリケーションはFormsサービスに要求を送信し、Formsサービスは適切な形式でフォームを返します。 Formsサービスは、要求を受け取るとすぐに、データとフォームデザインを結合し、目的の形式でフォームを配信します。 Formサービスの出力はインタラクティブフォームで、通常はPDFドキュメントです。 インタラクティブフォームを使用すると、ユーザーはフォーム上のフィールドに入力できます。

クライアントアプリケーションの種類に応じて、フォームをクライアントのWebブラウザーに書き込んだり、フォームをPDFファイルとして保存したりできます。 Webベースのアプリケーションは、フォームをWebブラウザーに書き込むことができます。 デスクトップアプリケーションは、フォームをPDFファイルとして保存できます。 WebブラウザーとPDFファイルに書き出す方法をデモするには、「 *レンダリングフォーム* 」セクションにあるクイック開始を次のように整理します。

* Java APIで厳密に型指定された（SOAPモード）例は、Javaサーブレットです。
* Webサービス(Java Base64)の例はJavaサーブレットです。
* Webサービス(MTOM)の例は、コンソールアプリケーションです(すべてのクイック開始にMTOMの例があるわけではありません)。

>[!NOTE]
>
>Javaサーブレットを使用してFormsサービスを呼び出すWebアプリケーションの作成について詳しくは、「フォームをレンダリングするWeb アプリケーションの [作成](/help/forms/developing/creating-web-applications-renders-forms.md)」を参照してください。

フォームデザイン（XDPファイル）またはPDFドキュメントをFormsサービスに渡すには、次の2つの方法があります。

* URL値を使用してフォームデザインを参照できます。 この方法では、 `URLSpec` オブジェクトを使用します。 コンテンツルートは、 `URLSpec` オブジェクトの `setContentRootURI` メソッドを使用してFormsサービスに渡されます。 フォームデザイン名( `formQuery`)は、別のパラメーターとして渡されます。 2つの値が連結され、フォームデザインの絶対参照が取得されます。 (「フォームの *レンダリング* 」セクションにあるクイック開始のほとんどは、この方法を使用します)。
* フォームデザインを含むフォーム `com.adobe.idp.Document` をFormsサービスに渡すことができます。 フォームデザインを含む `renderPDFForm2` オブジェクトを、という名前で `renderHTMLForm2``com.adobe.idp.Document` 受け入れる2つの新しいメソッドが追加されました。 (Formsサービスに [ドキュメントを渡すを参照)。](/help/forms/developing/passing-documents-forms-service.md)

Formsサービスを使用して、次のタスクを実行できます。

* インタラクティブPDF formsをレンダリング (インタラクティブPDF formsの [レンダリングを参照](/help/forms/developing/rendering-interactive-pdf-forms.md))。
* クライアントでフォームをレンダリングします。 (クライアントでの [フォームのレンダリングを参照](/help/forms/developing/rendering-forms-client.md))。
* フラグメントに基づいてフォームをレンダリングする。(See [Rendering Forms Based on Fragments](/help/forms/developing/rendering-forms-based-fragments.md).)
* 権限を付与されたフォームをレンダリングします。 (権限を付与されたフォームの [レンダリングを参照](/help/forms/developing/rendering-rights-enabled-forms.md))。
* フォームをHTMLとしてレンダリング (「フォームをHTMLとして [レンダリングする」を参照](/help/forms/developing/rendering-forms-html.md))。
* カスタムCSSファイルを使用したHTMLフォームのレンダリング(カスタムCSSファイルを使用したHTMLフォームの[レンダリング](/help/forms/developing/rendering-html-forms-using-custom.md))
* 送信済みのフォームを処理します。 (送信済みのフォームの [処理を参照](/help/forms/developing/handling-submitted-forms.md))。
* 送信済みXMLデータを使用したPDFドキュメントの作成を参照してください。 (送信済みXMLデータを使用したPDFドキュメントの [作成を参照](/help/forms/developing/creating-pdf-documents-submitted-xml.md))。
* フォームの自動埋め込み (編集可能なレイアウト [を含むフォームへの自動埋め込みを参照](/help/forms/developing/prepopulating-forms-flowable-layouts.md))。
* ドキュメントを渡す。 (Formsサービスに [ドキュメントを渡すを参照)。](/help/forms/developing/passing-documents-forms-service.md)
* フォームデータを計算します。 (フォームデータの [計算を参照](/help/forms/developing/calculating-form-data.md))。
* アプリの最適化。 (「Formsサービスのパフォーマンスの [最適化](/help/forms/developing/optimizing-performance-forms-service.md)」を参照)。

   ***ヒント&#x200B;**: アドビ開発者Webサイトには、Formsサービスを呼び出してフォームをレンダリングするASP.NETアプリケーションの作成方法を説明する次の記事が含まれています。 フォームレンダリングASP.NETアプリケーションの[作成を参照してください](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)。*

