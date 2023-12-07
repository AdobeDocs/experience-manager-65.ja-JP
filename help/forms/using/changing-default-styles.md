---
title: HTML5 フォームのデフォルトスタイルの変更
description: HTML5 フォームのスタイル設定は CSS に基づいています。 フォームのデフォルトのスタイルを変更できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 4c84cfd1-50a4-416f-b4a5-7f2f4c7f10af
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 43%

---

# HTML5 フォームのデフォルトスタイルの変更{#changing-default-styles-of-html-forms}

HTML5 のフォームはHTML5 機能を使用してレンダリングされ、レンダリングされたフォームのスタイル設定は CSS を使用しておこなわれます。 HTML5 フォームのデフォルトの外観は、PDFレンディションに似ています。 開発者は、カスタム CSS を使用して、HTML5 フォームのデフォルトの外観を変更できます。

この記事では、HTML5 フォームのスタイルを変更するための詳細手順を説明します。[スタイルの概要](/help/forms/using/css-styles.md)の記事では、HTML5 フォームのさまざまなスタイル設定を詳しく解説します。この記事に記載されている手順を実行する前に、「スタイルの概要」の記事を必ずお読みください。

次の 2 つの画像はデフォルトのスタイルとカスタマイズされたスタイルの違いを示しています。

![pictures-002-small](assets/pictures-002-small.png)

## フォームのスタイル設定 {#style-your-forms}

1. **カスタムスタイルを追加するプロファイルを選択**

   **https://&lt;server>:&lt;port>/crx/de** の URL で CRX DE インターフェイスにアクセスし、プロファイルを作成するか、既存のプロファイルを選択します。プロファイルの作成方法については、 [プロファイルの作成](/help/forms/using/custom-profile.md)

1. **HTML5 フォームのスタイル設定用の CSS スタイルシートの作成**

   プロファイルレンダラーを作成したフォルダーに移動し、CSS スタイルシートファイルを作成します。 以下の手順に従います。

   1. フォルダーを右クリックし、「 」を選択します。 **作成** > **ファイルを作成** メニューから

   1. ファイルを作成ダイアログで、スタイルシートの名前を入力します。 拡張子.css を必ず使用してください（例： stylesheet.css）。
   1. ナビゲーションペインから、作成した CSS ファイルを開きます。
   1. スタイル設定するコンポーネントの CSS クラスを定義し、それらのクラスにスタイルを追加します。

   HTML5 フォーム内の特定のコンポーネントに対して作成する CSS クラスについては、 [スタイルの概要](/help/forms/using/css-styles.md).

1. **プロファイルレンダラーにスタイルシートを含める**

   CRX DE でプロファイルレンダラーページ（jsp ファイル）を開き、CSS ファイルを XFA クライアントライブラリのすぐ下のページに含めます。 次の手順を実行して、CSS ファイルをプロファイルに含めます。

   1. レンダラーページで次の行を検索します。

      &lt;cq:includeClientLib categories=&quot;xfaforms.profile&quot; />

   1. 次の行を上記の行の下に挿入して、スタイルシートを含めます。

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1.  ファイルを保存します。
