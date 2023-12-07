---
title: フォーム出力の設定
description: フォーム出力の設定方法を説明します。 フォーム出力を設定し、この機能を有効にするには、フォームを送信する前にカスタムスクリプトを使用します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 38%

---

# フォーム出力の設定{#configuring-form-output}

## Web ブラウザーに返されるHTML出力のタイプを指定します {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 管理コンソールで、サービス/Forms をクリックします。
1. 「フォーム出力」の「出力タイプ」リストで、次のいずれかのオプションを選択します。

   **フルHTML:** 完全なHTMLタグ（完全なタグページ）内でフォームをレンダリングするには、次の手順に従います。HTML。 この値がデフォルトです。

   **Body のみ：** `<BODY>` タグの範囲（完全な HTML ページではない）でフォームを処理します。

1. 「保存」をクリックします。

## PDFコンテンツがレンダリングされる場所を指定 {#specify-the-location-where-pdf-content-is-rendered}

1. 「フォーム出力」の「レンダリング先」リストで、次のいずれかのオプションを選択します。

   **クライアント：** Adobe AcrobatまたはAdobe Reader内でPDF formsをレンダリングするには： クライアントサイドレンダリングを使用すると、AEM forms のパフォーマンスが向上し、PDFForm 変換にのみ適用されます。

   **サーバー：** アプリケーションPDF forms上でアプリケーションをレンダリングする。

   **自動：** XDP ファイルの `dynamicRender` 設定値の示す位置で PDF フォームをレンダリングします。この値がデフォルトです。

1. 「保存」をクリックします。

## フォーム送信前のカスタムスクリプトの呼び出しの設定 {#configuring-invocation-of-custom-scripts-before-form-submit}

この機能を有効にするには、次の手順を実行します。

1. 管理コンソールにログインします。
1. に移動します。 **サービス** > **フォーム**.
1. 「出力形式」で「Body のみ」を指定します。
1. 設定を保存します。
1. HTML コードの head セクションで JavaScript 変数 __CUSTOM_SCRIPTS_VERSION を宣言し、その値を 1 に設定します。

   >[!NOTE]
   >
   >*この機能を無効にするには、JavaScript 変数を削除するか、その値を 0 に設定します。*
