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
source-git-commit: 687cdacc2868de16a4df968dddedd330ce3317bb

---


# フォームのレンダリング {#rendering-forms}

**Formsサービスについて**

Formsサービスを使用すると、通常はDesignerで作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。 フォーム作成者は、Formsサービスが様々なブラウザー環境でPDF、SWFまたはHTMLでレンダリングする単一のフォームデザインを開発できます。

エンドユーザーがフォームを要求すると、クライアントアプリケーションはFormsサービスに要求を送信し、Formsサービスは適切な形式でフォームを返します。 Formsサービスは、要求を受け取るとすぐに、データをフォームデザインにマージし、目的の形式でフォームを配信します。 Formサービスの出力はインタラクティブフォームで、通常はPDFドキュメントです。 インタラクティブフォームを使用すると、ユーザーはフォーム上のフィールドに入力できます。

クライアントアプリケーションの種類に応じて、クライアントWebブラウザーにフォームを書き込んだり、フォームをPDFファイルとして保存したりできます。 Webベースのアプリケーションは、Webブラウザーにフォームを書き込むことができます。 デスクトップアプリケーションは、フォームをPDFファイルとして保存できます。 WebブラウザーとPDFファイルに書き出しを行う方法を示すために、「 *Rendering Forms* 」セクションのクイックスタートは次のように構成されています。

* Java APIの厳密に型指定された（SOAPモード）例はJavaサーブレットです。
* Webサービス(Java Base64)の例はJavaサーブレットです。
* Webサービス(MTOM)の例はコンソールアプリケーションです（クイックスタートの中にMTOMの例があるわけではありません）。

***注意&#x200B;**:Javaサーブレットを使用してFormsサービスを呼び出すWebアプリケーションの作成について詳しくは、「フォームをレンダリングするWebア[プリケーションの作成」を参照してください](/help/forms/developing/creating-web-applications-renders-forms.md)。*


フォームデザイン（XDPファイル）またはPDFドキュメントは、次の2つの方法のいずれかを使用してFormsサービスに渡すことができます。

* URL値を使用してフォームデザインを参照できます。 この方法では、オブジェクトを使用 `URLSpec` します。 コンテンツルートは、オブジェクトのメソッドを使用してFormsサ `URLSpec` ービスに渡さ `setContentRootURI` れます。 フォームデザイン名( `formQuery`)は、別のパラメーターとして渡されます。 2つの値が連結され、フォームデザインへの絶対参照が取得されます。 (「フォームのレンダリング」セクションにあるクイックスタ *ートのほとんどは* 、この方法を使用します)。
* フォームデザインを含 `com.adobe.idp.Document` むフォームをFormsサービスに渡すことができます。 フォームデザインを含むオブジ `renderPDFForm2` ェクトの名 `renderHTMLForm2` 前と受け `com.adobe.idp.Document` 入れる2つの新しいメソッド。 (Formsサービ [スにドキュメントを渡すを参照)。](/help/forms/developing/passing-documents-forms-service.md)

Formsサービスを使用して、次のタスクを実行できます。

* インタラクティブPDFフォームをレンダリングします。 (インタラクティブPDF [フォームのレンダリングを参照](/help/forms/developing/rendering-interactive-pdf-forms.md))。
* クライアントでフォームをレンダリングします。 (「クライアント [でのフォームのレンダリング](/help/forms/developing/rendering-forms-client.md)」を参照)。
* フラグメントに基づいてフォームをレンダリングする。(See [Rendering Forms Based on Fragments](/help/forms/developing/rendering-forms-based-fragments.md).)
* 使用権限を付与されたフォームをレンダリングします。 (権限を付与 [されたフォームのレンダリングを参照](/help/forms/developing/rendering-rights-enabled-forms.md))。
* フォームをHTMLとしてレンダリングする。 (「フォーム [のHTMLとしてのレンダリング](/help/forms/developing/rendering-forms-html.md)」を参照)。
* カスタムCSSファイルを使用したHTMLフォームのレンダリング([カスタムCSSファイルを使用したHTMLフォームのレンダリング](/help/forms/developing/rendering-html-forms-using-custom.md))
* 送信されたフォームを処理します。 (「送信済み [フォームの処理](/help/forms/developing/handling-submitted-forms.md)」を参照)。
* 送信済みXMLデータを使用したPDFドキュメントの作成を参照してください。 (送信済みXML [データを使用したPDFドキュメントの作成を参照](/help/forms/developing/creating-pdf-documents-submitted-xml.md))。
* フォームの自動埋め込み (「編集可能な [レイアウトでのフォームの自動埋め込み](/help/forms/developing/prepopulating-forms-flowable-layouts.md)」を参照)。
* ドキュメントの引き渡し (Formsサービ [スにドキュメントを渡すを参照)。](/help/forms/developing/passing-documents-forms-service.md)
* フォームデータを計算します。 (フォーム [データの計算を参照](/help/forms/developing/calculating-form-data.md))。
* アプリの最適化を参照してください。 (「Formsサ [ービスのパフォーマンスの最適化](/help/forms/developing/optimizing-performance-forms-service.md)」を参照)。

   ***ヒント&#x200B;**:Adobe Developer webサイトには、Formsサービスを呼び出してフォームをレンダリングするASP.NETアプリケーションの作成方法を説明する次の記事が含まれています。 フォーム[レンダリングASP.NETアプリケーションの作成を参照してください](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)。*

