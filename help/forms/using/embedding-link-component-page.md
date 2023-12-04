---
title: ページでのリンクコンポーネントの埋め込み
seo-title: Embedding link component in a page
description: リンクコンポーネントを使用すると、任意のページからアダプティブドキュメントやアダプティブフォームをリンクすることができます。
seo-description: You can use the link component to link an adaptive document or an adaptive form from any page.
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
exl-id: eb45adf2-d0f3-4de6-92ac-fb146953e989
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 31%

---

# ページでのリンクコンポーネントの埋め込み{#embedding-link-component-in-a-page}

## 前提条件 {#prerequisites}

リンクコンポーネントは、Document Services カテゴリのメンバーです。 Document Services カテゴリがAEMコンポーネントブラウザーに表示されていることを確認します。 カテゴリが表示されない場合は、次の手順に従います： [フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md).

## リンクコンポーネント {#link-component}

フォームポータルの作成者は、リンクコンポーネントを使用して、ページ上の任意の場所からアダプティブフォームへのリンクを作成できます。 リンクコンポーネントは、コンポーネントブラウザーの「Document Services」セクションで使用できます。

ページにリンクコンポーネントを追加するには、次の手順を実行します。

1. **リンク**&#x200B;コンポーネントをページにドラッグします。コンポーネントを選択し、「 」を選択します。 ![cmppr](assets/cmppr.png). リンクコンポーネントを編集ダイアログが開きます。

   ![edit-link-component](assets/edit-link-component.png)

1. 「**表示**」タブで次の情報を指定します。

   * **リンクのキャプション**：リンクテキストまたはリンクのキャプション。
   * **リンクツールチップ**：リンクのツールチップ。
   * **レイアウトテンプレート**：リンクコンポーネントのレイアウトのテンプレート。

1. を開きます。 **アセット情報** 」タブをクリックして、アセットのタイプを指定します。 アセットは、**フォーム**&#x200B;にすることができます。選択するアセットのタイプによって、次のオプションが表示されます。

   * **アセットパス**：アセットが保存されるリポジトリパス。

   * **レンダリングタイプ**：レンダリングフォーマット (PDF、HTML、自動 )。 自動レンダリングタイプでは、ユーザー環境が検出され、それに応じて、フォームがHTMLまたはPDFとしてレンダリングされます。 例えば、フォームがモバイルデバイスからアクセスされる場合、「自動レンダリング」タイプはフォームをHTMLでレンダリングします。
   * **URL の送信**：フォームデータが送信されるサーブレットの URL。
   * **HTMLプロファイル**：フォームをHTMLとしてレンダリングするためのプロファイル。
   * **PDFプロファイル**：フォームをレンダリングドキュメントとしてPDFするためのプロファイル。

1. 「**詳細**」タブを開きます。その他のパラメーターは、キーと値のペアの形式で指定できます。リンクをクリックすると、これらのその他のパラメーターはフォームと共に渡されます。

   「**完了**」を選択して設定を保存します。

## リンクコンポーネントを使用するためのベストプラクティス {#best-practices-for-using-link-component-br}

* フォームパスで指定したPDFが、許可されたレンダリング形式としてPDFを持つドキュメントを指す場合は、必ずレンダリングタイプとしてパスを選択してください。
* フォームの送信 URL は複数の場所で指定でき、優先順位は次のとおりです。

   1. 優先順位が最も高いのは、フォームに埋め込まれた送信 URL（送信ボタン）です。
   1. 優先度が中程度なのは、Forms Manager で説明されている送信 URL です。
   1. 一番優先順位が低いのは、フォームポータルで説明している送信URLです。
