---
title: HTML5 フォームのデフォルトスタイルの変更
seo-title: HTML5 フォームのデフォルトスタイルの変更
description: HTML5 フォームのスタイルは CSS に基づいています。フォームのデフォルトスタイルを変更することができます。
seo-description: HTML5 フォームのスタイルは CSS に基づいています。フォームのデフォルトスタイルを変更することができます。
uuid: 5e23237d-42d8-4d29-b79e-4dc276ef65ff
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 582b0fe8-a92b-4a1d-b859-57f13f53d0d8
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 73%

---


# HTML5 フォームのデフォルトスタイルの変更{#changing-default-styles-of-html-forms}

HTML5 フォームは HTML5 機能の使用によりレンダリングされ、レンダリングされるフォームのスタイル設定は CSS の使用によって実行されます。HTML5 フォームのデフォルトの外観は、その PDF レンダリングに似ています。開発者はカスタム CSS を使用して、HTML5 フォームのデフォルトの外観を変更できます。

この記事では、HTML5フォームのスタイルを変更するための詳細手順を説明します。[スタイルの概要](/help/forms/using/css-styles.md)記事には、HTML5フォームの様々なスタイル設定に関する詳細が記載されています。 この記事に記載されている手順を実行する前に、「スタイルの概要」記事を必ずお読みください。

次の 2 つの画像はデフォルトのスタイルとカスタマイズされたスタイルの違いを示しています。

![pictures-002-small](assets/pictures-002-small.png)

## フォームのスタイル設定 {#style-your-forms}

1. **カスタムスタイルを追加するプロファイルの選択**

   URLでCRX DEインターフェイスにアクセスします。**https://&lt;server>:&lt;port>/crx/de**&#x200B;を作成し、プロファイルを作成するか、既存のプロファイルを選択します。 プロファイルの作成方法について詳しくは、[新しいプロファイルの作成](/help/forms/using/custom-profile.md)を参照してください

1. **HTML5 フォームのスタイル設定用の CSS スタイルシートの作成**

   プロファイルレンダラーを作成したフォルダーに移動し、CSS スタイルシートファイルを作成します。次の手順に従います。

   1. フォルダーを右クリックし、メニューから&#x200B;**create**/**create File**&#x200B;を選択します

   1. 「ファイルを作成」ダイアログで、スタイルシートの名前を入力します。拡張子 .css を必ず使用してください (例： stylesheet.css)。
   1. ナビゲーションペインで、作成したCSSファイルを開きます。
   1. スタイル設定するコンポーネントの CSS クラスを定義し、それらのクラスにスタイルを追加します。

   HTML5 フォームにある特定のコンポーネントに対してどの CSS クラスを作成するかについて詳しくは、「[スタイルの概要](/help/forms/using/css-styles.md)」を参照してください。

1. **Profile Renderer にスタイルシートを追加する**

   CRX DE でプロファイルレンダラーページ（jsp ファイル）を開き、CSS ファイルを XFA クライアントライブラリのすぐ下にあるページに含めます。次の手順を実行して、CSS ファイルをプロファイルに含めます。

   1. レンダラーページで次の行を検索します。

      &lt;cq:includeClientLib categories=&quot;xfaforms.profile&quot; />

   1. 次の行を上記の行の下に挿入して、スタイルシートを含めます。

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1.  ファイルを保存します。
