---
title: Formsのレンダリング
seo-title: Formsのレンダリング
description: Formsサービスを使用して、通常はDesignerで作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成します。 フォーム作成者は、Formsサービスが様々なブラウザー環境でPDF、SWFまたはHTMLでレンダリングする単一のフォームデザインを開発できます。
seo-description: Formsサービスを使用して、通常はDesignerで作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成します。 フォーム作成者は、Formsサービスが様々なブラウザー環境でPDF、SWFまたはHTMLでレンダリングする単一のフォームデザインを開発できます。
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Forms {#rendering-forms}のレンダリング

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

**Formsサービスについて**

Formsサービスを使用すると、通常はDesignerで作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。 フォーム作成者は、Formsサービスが様々なブラウザー環境でPDF、SWFまたはHTMLでレンダリングする単一のフォームデザインを開発できます。

エンドユーザーがフォームを要求すると、クライアントアプリケーションがFormsサービスに要求を送信し、そのサービスが適切な形式でフォームを返します。 Formsサービスは、要求を受け取るとすぐに、データをフォームデザインと結合し、目的の形式でフォームを配信します。 Formサービスの出力は、インタラクティブなフォーム（通常はPDFドキュメント）です。 インタラクティブフォームを使用すると、ユーザーはフォーム上のフィールドに入力できます。

クライアントアプリケーションのタイプに応じて、フォームをクライアントWebブラウザーに書き込むか、フォームをPDFファイルとして保存できます。 Webベースのアプリケーションは、フォームをWebブラウザーに書き込むことができます。 デスクトップアプリケーションは、フォームをPDFファイルとして保存できます。 WebブラウザーとPDFファイルに書き出す方法を示すために、*「Formsのレンダリング*」セクションにあるクイックスタートは、次のように構成されています。

* Java APIで厳密に型指定された（SOAPモード）の例は、Javaサーブレットです。
* Webサービス(Java Base64)の例は、Javaサーブレットです。
* Webサービス(MTOM)の例は、コンソールアプリケーションです（すべてのクイックスタートにMTOMの例があるわけではありません）。

>[!NOTE]
>
>Javaサーブレットを使用してFormsサービスを呼び出すWebアプリケーションの作成について詳しくは、「 [Forms](/help/forms/developing/creating-web-applications-renders-forms.md)をレンダリングするWebアプリケーションの作成」を参照してください。

フォームデザイン（XDPファイル）またはPDFドキュメントをFormsサービスに渡す方法は、次の2つの方法のいずれかです。

* URL値を使用してフォームデザインを参照できます。 この方法では、`URLSpec`オブジェクトを使用します。 コンテンツルートは、`URLSpec`オブジェクトの`setContentRootURI`メソッドを使用してFormsサービスに渡されます。 フォームデザインの名前(`formQuery`)は、別のパラメーターとして渡されます。 2つの値が連結され、フォームデザインへの絶対参照が取得されます。 (ほとんどのクイックスタートは、「*Forms*&#x200B;のレンダリング」セクションにあり、この方法を使用します)。
* フォームデザインを含む`com.adobe.idp.Document`をFormsサービスに渡すことができます。 `renderPDFForm2`および`renderHTMLForm2`という2つの新しいメソッドは、フォームデザインを含む`com.adobe.idp.Document`オブジェクトを受け取ります。 ([Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)を参照)。

Formsサービスを使用して、次のタスクを実行できます。

* インタラクティブPDF formsのレンダリング ([インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照)。
* クライアントでフォームをレンダリングします。 ([クライアントでのFormsのレンダリング](/help/forms/developing/rendering-forms-client.md)を参照)。
* フラグメントに基づいてフォームをレンダリングする。([フラグメントに基づくFormsのレンダリング](/help/forms/developing/rendering-forms-based-fragments.md)を参照)。
* 権限が有効なフォームをレンダリングします。 ([権限が有効なForms](/help/forms/developing/rendering-rights-enabled-forms.md)のレンダリングを参照)。
* フォームをHTMLとしてレンダリングする。 ([FormsをHTMLとしてレンダリングする](/help/forms/developing/rendering-forms-html.md)を参照)。
* カスタムCSSファイル([カスタムCSSファイルを使用したHTML Formsのレンダリング](/help/forms/developing/rendering-html-forms-using-custom.md))
* 送信済みのフォームを処理します。 ([送信されたForms](/help/forms/developing/handling-submitted-forms.md)の処理を参照)。
* 送信済みXMLデータを使用してPDFドキュメントを作成します。 （[送信されたXMLデータを使用したPDFドキュメントの作成](/help/forms/developing/creating-pdf-documents-submitted-xml.md)を参照）。
* フォームの事前入力 ([編集可能なレイアウトを使用したFormsの事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md)を参照)。
* ドキュメントを渡す。 ([Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)を参照)。
* フォームデータを計算します。 （[フォームデータの計算](/help/forms/developing/calculating-form-data.md)を参照）。
* アプリケーションを最適化する。 (「[Formsサービスのパフォーマンスの最適化](/help/forms/developing/optimizing-performance-forms-service.md)」を参照)。

   ***ヒント&#x200B;**:Adobe開発者のWebサイトには、Formsサービスを呼び出してフォームをレンダリングするASP.NETアプリケーションの作成方法を説明する次の記事が含まれています。[ASP.NETアプリケーションをレンダリングするフォームの作成](https://www.adobe.com/devnet/livecycle/articles/asp_net.html).*を参照してください。
