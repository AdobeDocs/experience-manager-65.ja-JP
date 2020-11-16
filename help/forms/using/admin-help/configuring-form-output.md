---
title: フォーム出力の設定
seo-title: フォーム出力の設定
description: フォーム出力を設定する方法について説明します。
seo-description: フォーム出力を設定する方法について説明します。
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 94%

---


# フォーム出力の設定{#configuring-form-output}

## Web ブラウザーに返す HTML 出力の形式の指定 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「Form 出力」の「出力形式」で次のどちらかのオプションを選択します。

   **フル HTML：**&#x200B;すべての HTML タグを含む形（完全な HTML ページ）でフォームをレンダリングします。これがデフォルト値です。

   **フォーム本文：** (完全なHTMLページではな `<BODY>` く)タグ内のフォームをレンダリングする場合。

1. 「保存」をクリックします。

## PDF コンテンツのレンダリング位置の指定 {#specify-the-location-where-pdf-content-is-rendered}

1. 「Form 出力」の「レンダリング位置」リストで次のいずれかのオプションを選択します。

   **クライアント：** Adobe Acrobat または Adobe Reader 内で PDF フォームをレンダリングします。クライアント側でレンダリングを行うと AEM Forms のパフォーマンスが向上します。ただし、これは PDFForm 変換にのみ適用されます。

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

