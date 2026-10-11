---
title: ページでのリンクコンポーネントの埋め込み
description: リンクコンポーネントを使用して、任意のページからアダプティブドキュメントまたはアダプティブフォームにリンクできます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: eb45adf2-d0f3-4de6-92ac-fb146953e989
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: fa155e29-cba2-5e77-9efd-4824be5ce4c8
    internal-label: Forms Portal
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 100%
---
# ページでのリンクコンポーネントの埋め込み{#embedding-link-component-in-a-page}

## 前提条件 {#prerequisites}

リンクコンポーネントは、Document Services カテゴリのメンバーです。 Document Services カテゴリが AEM コンポーネントブラウザーに表示されていることを確認します。 カテゴリがリスト表示されていない場合は、[フォームポータルコンポーネントの有効化](/help/forms/using/enabling-forms-portal-components.md)にリストされている手順に従います。

## リンクコンポーネント {#link-component}

フォームポータルの作成者は、リンクコンポーネントを使用してページの任意の場所からアダプティブフォームへのリンクを作成できます。 リンクコンポーネントは、コンポーネントブラウザーの Document Services セクションで利用できます。

次の手順を実行して、ページにリンクコンポーネントを追加します。

1. **リンク**&#x200B;コンポーネントをページにドラッグします。 コンポーネントを選択して、![cmppr](assets/cmppr.png) を選択します。 リンクコンポーネントを編集ダイアログが開きます。

   ![edit-link-component](assets/edit-link-component.png)

1. 「**表示**」タブで次の情報を指定します。

   * **リンクのキャプション**：リンクテキストまたはリンクのキャプション。
   * **リンクツールチップ**：リンクのツールヒント。
   * **レイアウトテンプレート**：リンクコンポーネントのレイアウト用テンプレート。

1. 「**アセット情報**」タブを開き、アセットのタイプを指定します。 アセットは、**フォーム**&#x200B;にすることができます。 選択するアセットのタイプによって、次のオプションが表示されます。

   * **アセットパス**：アセットが保存されるリポジトリパス。

   * **レンダリングタイプ**：レンダリング形式（PDF、HTML または自動）。 自動レンダリングタイプでは、ユーザーの環境が検出され、それに応じて HTML 形式または PDF 形式でフォームがレンダリングされます。 例えば、フォームがモバイルデバイスからアクセスされる場合、自動レンダリングタイプでは HTML 形式でフォームがレンダリングされます。
   * **URL の送信**：フォームデータが送信されるサーブレットの URL。
   * **HTML プロファイル**：HTML としてフォームをレンダリングするためのプロファイル。
   * **PDF プロファイル**：PDF ドキュメントとしてフォームをレンダリングするのためのプロファイル。

1. 「**詳細**」タブを開きます。 その他のパラメーターは、キーと値のペアの形式で指定できます。 リンクをクリックすると、これらのその他のパラメーターはフォームと共に渡されます。

   「**完了**」を選択して設定を保存します。

## リンクコンポーネントを使用するためのベストプラクティス {#best-practices-for-using-link-component-br}

* フォームパスに指定したパスが、レンダリング形式として許可された PDF を含むドキュメントを指す場合は、レンダリングタイプとして PDF を選択していることを確認します。
* フォームの送信 URL は複数の場所で指定でき、その優先順位は次のとおりです。

  1. 優先順位が最も高いのは、フォーム（送信ボタン）に埋め込まれている送信 URL です。
  1. 優先順位が中程度なのは、Forms Manager で説明している送信 URL です。
  1. 一番優先順位が低いのは、フォームポータルで説明している送信URLです。
