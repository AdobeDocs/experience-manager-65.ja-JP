---
title: フォーム出力の設定
description: フォーム出力を設定する方法について説明します。フォーム出力を設定し、この機能を有効にするには、フォームを送信する前にカスタムスクリプトを使用します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 100%

---

# フォーム出力の設定{#configuring-form-output}

## Web ブラウザーに返す HTML 出力の形式を指定 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「フォーム出力」の出力タイプのリストで次のいずれかのオプションを選択します。

   **完全な HTML：**&#x200B;完全な HTML タグを含む形（完全な HTML ページ）でフォームをレンダリングします。これがデフォルト値です。

   **Body のみ：** `<BODY>` タグの範囲（完全な HTML ページではない）でフォームを処理します。

1. 「保存」をクリックします。

## PDF コンテンツをレンダリングする場所を指定 {#specify-the-location-where-pdf-content-is-rendered}

1. 「フォーム出力」のレンダーのリストで次のいずれかのオプションを選択します。

   **クライアント：** Adobe Acrobat または Adobe Reader 内で PDF フォームをレンダリングします。クライアントサイドでレンダリングを行うと AEM Forms のパフォーマンスが向上します。ただし、これは PDFForm 変換にのみ適用されます。

   **サーバー：**&#x200B;アプリケーションサーバーで PDF フォームをレンダリングします。

   **自動：** XDP ファイルの `dynamicRender` 設定値の示す位置で PDF フォームをレンダリングします。これがデフォルト値です。

1. 「保存」をクリックします。

## フォーム送信前のカスタムスクリプトの呼び出しの設定 {#configuring-invocation-of-custom-scripts-before-form-submit}

この機能を有効にするには、次の手順を実行します。

1. 管理コンソールにログインします。
1. **サービス**／**Forms** をクリックします。
1. 「出力形式」で「Body のみ」を指定します。
1. 設定を保存します。
1. HTML コードの head セクションで JavaScript 変数 __CUSTOM_SCRIPTS_VERSION を宣言し、その値を 1 に設定します。

   >[!NOTE]
   >
   >*この機能を無効にするには、JavaScript 変数を削除するか、その値を 0 に設定します。*
