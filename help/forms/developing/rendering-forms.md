---
title: Formsのレンダリング
seo-title: Formsのレンダリング
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


# Formsをレンダリング{#rendering-forms}

**Formsサービスについて**

Formsサービスを使用すると、通常はDesignerで作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。 フォーム作成者は、Formsサービスが様々なブラウザー環境でPDF、SWFまたはHTMLでレンダリングする単一のフォームデザインを開発できます。

エンドユーザーがフォームを要求すると、クライアントアプリケーションは要求をFormsサービスに送信し、このサービスは適切な形式でフォームを返します。 Formsサービスは、要求を受け取るとすぐに、データとフォームデザインを結合し、目的の形式でフォームを配信します。 Formサービスの出力はインタラクティブフォームで、通常はPDFドキュメントです。 インタラクティブフォームを使用すると、ユーザーはフォーム上のフィールドに入力できます。

クライアントアプリケーションの種類に応じて、フォームをクライアントのWebブラウザーに書き込んだり、フォームをPDFファイルとして保存したりできます。 Webベースのアプリケーションは、フォームをWebブラウザーに書き込むことができます。 デスクトップアプリケーションは、フォームをPDFファイルとして保存できます。 WebブラウザーとPDFファイルへの書き出し方法をデモするために、*「Forms*&#x200B;のレンダリング」セクションにあるクイック開始ーは、次のように構成されています。

* Java APIで厳密に型指定された（SOAPモード）例は、Javaサーブレットです。
* Webサービス(Java Base64)の例はJavaサーブレットです。
* Webサービス(MTOM)の例は、コンソールアプリケーションです(すべてのクイック開始にMTOMの例があるわけではありません)。

>[!NOTE]
>
>Javaサーブレットを使用してFormsサービスを呼び出すWebアプリケーションの作成について詳しくは、[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)を参照してください。

フォームデザイン（XDPファイル）またはPDFドキュメントをFormsサービスに渡すには、次の2つの方法があります。

* URL値を使用してフォームデザインを参照できます。 この方法では、`URLSpec`オブジェクトを使用します。 コンテンツルートは、`URLSpec`オブジェクトの`setContentRootURI`メソッドを使用してFormsサービスに渡されます。 フォームデザイン名(`formQuery`)は、別のパラメーターとして渡されます。 2つの値が連結され、フォームデザインの絶対参照が取得されます。 (「*Forms*&#x200B;のレンダリング」セクションにあるクイック開始のほとんどは、この方法を使用します)。
* フォームデザインを含む`com.adobe.idp.Document`をFormsサービスに渡すことができます。 `renderPDFForm2`と`renderHTMLForm2`という2つの新しいメソッドは、フォームデザインを含む`com.adobe.idp.Document`オブジェクトを受け入れます。 (「[Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)」を参照)。

Formsサービスを使用して、次のタスクを実現できます。

* インタラクティブPDF formsをレンダリング ([インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照)。
* クライアントでフォームをレンダリングします。 ([クライアントでのFormsのレンダリング](/help/forms/developing/rendering-forms-client.md)を参照)。
* フラグメントに基づいてフォームをレンダリングする。(「[フラグメントに基づくFormsのレンダリング](/help/forms/developing/rendering-forms-based-fragments.md)」を参照)。
* 権限を付与されたフォームをレンダリングします。 (「[レンダリング権限を有効にしたForms](/help/forms/developing/rendering-rights-enabled-forms.md)」を参照)。
* フォームをHTMLとしてレンダリング ([HTMLとしてのFormsのレンダリング](/help/forms/developing/rendering-forms-html.md)を参照)。
* カスタムCSSファイルを使用したHTMLFormsのレンダリング([カスタムCSSファイルを使用したHTMLFormsのレンダリング](/help/forms/developing/rendering-html-forms-using-custom.md))
* 送信済みのフォームを処理します。 ([送信されたFormsの処理](/help/forms/developing/handling-submitted-forms.md)を参照)。
* 送信済みXMLデータを使用したPDFドキュメントの作成を参照してください。 (「[送信されたXMLデータを使用したPDFドキュメントの作成](/help/forms/developing/creating-pdf-documents-submitted-xml.md)」を参照)。
* フォームの自動埋め込み (「[編集可能なレイアウトでFormsを自動埋め込む](/help/forms/developing/prepopulating-forms-flowable-layouts.md)」を参照)。
* ドキュメントを渡す。 (「[Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)」を参照)。
* フォームデータを計算します。 （「[フォームデータの計算](/help/forms/developing/calculating-form-data.md)」を参照）。
* アプリの最適化。 (「[Formsサービスのパフォーマンスの最適化](/help/forms/developing/optimizing-performance-forms-service.md)」を参照)。

   ***ヒント&#x200B;**:Adobe開発者Webサイトには、Formsサービスを呼び出してフォームをレンダリングするASP.NETアプリケーションの作成方法を説明する次の記事が含まれています。[ASP.NETアプリケーションをレンダリングするフォームの作成](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)を参照してください。*

