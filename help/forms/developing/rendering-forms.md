---
title: Forms のレンダリング
seo-title: Rendering Forms
description: Forms サービスを使用すると、通常は Designer で作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。フォーム作成者は、Forms サービスが様々なブラウザー環境で PDF、SWF または HTML でレンダリングする、単一のフォームデザインを開発できます。
seo-description: Use the Forms service to create interactive data capture client applications that validate, process, transform, and deliver forms typically created in Designer. Form authors can develop a single form design that the Forms service renders in PDF, SWF, or HTML in various browser environments.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: ht
source-wordcount: '571'
ht-degree: 100%

---

# Forms のレンダリング {#rendering-forms}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**Forms サービスについて**

Forms サービスを使用すると、通常は Designer で作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。フォーム作成者は、Forms サービスが様々なブラウザー環境で PDF、SWF または HTML でレンダリングする、単一のフォームデザインを開発できます。

エンドユーザーがフォームを要求すると、クライアントアプリケーションが Forms サービスに要求を送信し、このサービスが適切な形式でフォームを返します。Forms サービスは、要求を受け取るとすぐにデータをフォームデザインと結合し、目的の形式でフォームを配信します。フォームサービスの出力は、インタラクティブなフォーム（通常は PDF ドキュメント）です。インタラクティブフォームを使用すると、ユーザーはフォーム上のフィールドに入力できます。

クライアントアプリケーションの種類に応じて、フォームをクライアント ｗeb ブラウザーに書き込んだり、フォームを PDF ファイルとして保存したりできます。Web ベースのアプリケーションは、web ブラウザーにフォームを書き込むことができます。デスクトップアプリケーションは、フォームを PDF ファイルとして保存できます。Web ブラウザーと PDF ファイルに書き出す方法を示すために、*Forms のレンダリング* セクションにあるクイックスタートは、次のように整理されます。

* Java API で厳密に型指定された（SOAP モード）の例は Java サーブレットです。
* Web サービス (Java Base64) の例は Java サーブレットです。
* Web サービス（MTOM）の例は、コンソールアプリケーションです（すべてのクイックスタートに MTOM の例があるわけではありません）。

>[!NOTE]
>
>Java サーブレットを使用して Forms サービスを呼び出す web アプリケーションの作成について詳しくは、[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)を参照してください。

次の 2 つの方法のいずれかを使用して、フォームデザイン（XDP ファイル）または PDF ドキュメントを Forms サービスに渡すことができます。

* URL 値を使用してフォームデザインを参照できます。このアプローチでは、`URLSpec` オブジェクトを使用します。コンテンツルートは、`URLSpec` オブジェクトの `setContentRootURI` メソッドを使用して Forms サービスに渡されます。フォームデザイン名（`formQuery`）は別のパラメーターとして渡されます。2 つの値が連結され、フォームデザインへの絶対参照が取得されます。（ほとんどのクイックスタートは、*Forms のレンダリング*&#x200B;セクションでは、この方法を使用します）。
* フォームデザインを含む `com.adobe.idp.Document` を Forms サービスに渡すことができます。`renderPDFForm2` および `renderHTMLForm2` という名前の 2 つの新しいメソッドは、フォームデザインを含む `com.adobe.idp.Document` オブジェクトを受け入れます（[Forms サービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)を参照）。

Forms サービスを使用して、次のタスクを実行できます。

* インタラクティブ PDF Forms のレンダリング（[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照）。
* クライアントでの Forms のレンダリング（[クライアントでの Forms のレンダリング](/help/forms/developing/rendering-forms-client.md)を参照）。
* フラグメントに基づいた Forms のレンダリング（[フラグメントに基づいた Forms のレンダリング](/help/forms/developing/rendering-forms-based-fragments.md)を参照）。
* 権限が有効な Forms のレンダリング（[レンダリング権限が有効な Forms ](/help/forms/developing/rendering-rights-enabled-forms.md)を参照）。
* Forms を HTML としてレンダリング（[Forms を HTML としてレンダリング](/help/forms/developing/rendering-forms-html.md)を参照）。
* カスタム CSS ファイルを使用した HTML フォームのレンダリング（[カスタム CSS ファイルを使用した HTML フォームのレンダリング](/help/forms/developing/rendering-html-forms-using-custom.md)）
* 送信された Forms の処理（[送信された Forms の処理](/help/forms/developing/handling-submitted-forms.md)を参照）。
* 送信された XML データを使用した PDF ドキュメントの作成（[送信された XML データでの PDF ドキュメントの作成](/help/forms/developing/creating-pdf-documents-submitted-xml.md)を参照）。
* フォームの事前入力（[編集可能なレイアウトを使用した Forms の事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md)を参照）。
* ドキュメントを渡す（[Forms サービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)を参照）。
* フォームデータの計算（[フォームデータの計算](/help/forms/developing/calculating-form-data.md)を参照）。
* アプリケーションの最適化（[Forms サービスのパフォーマンスの最適化](/help/forms/developing/optimizing-performance-forms-service.md)を参照。）
