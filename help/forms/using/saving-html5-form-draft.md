---
title: HTML5 フォームのドラフトでの保存
description: HTML5 フォームをドラフトとして保存し、後でフォームへの記入を再開します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 54%

---

# HTML5 フォームのドラフトでの保存 {#saving-an-html-form-as-a-draft}

HTML5 のフォームをドラフトとして保存し、後でフォームへの記入を再開できます。 Forms Portal を使用すると、すべてのユーザーが Adobe Portal フォームを保存および復元することができます。5. 「ドラフトとして保存」機能を有効にするには、プロファイルのノードに次の設定を追加します。

## 「ドラフトとして保存」機能を許可するためのカスタムプロファイル {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms では初期状態で「**ドラフトとして保存**」プロファイルを使用できます。「ドラフトとして保存」プロファイルを使用してフォームをレンダリングすると、HTML5 フォームのドラフト機能を有効にすることができます。 フォームのHTMLレンダリングプロファイルを [Forms Manager](/help/forms/using/introduction-managing-forms.md).

既存の[カスタムプロファイル](/help/forms/using/custom-profile.md)に対して「ドラフトとして保存」機能を有効にするには、カスタムプロファイルのノードに次のプロパティを追加します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ名</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>文字列</td>
   <td>true</td>
   <td><p>ドラフトとして保存機能を有効にする</p> <p>を設定します。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>文字列</td>
   <td>true</td>
   <td><p>添付ファイルのアップロードを許可</p> <p>をこのプロファイルに置き換えます。</p> </td>
  </tr>
 </tbody>
</table>

## ドラフトの保存と一覧表示 {#drafts-storage-and-listing}

フォームに対して「ドラフトとして保存」機能を有効にした後、フォームを保存すると、そのフォームは [ドラフトと送信コンポーネント](/help/forms/using/draft-submission-component.md). ドラフトと送信コンポーネントで、保存されたフォームを取得して入力を開始できます。

ドラフトと送信コンポーネントのフォームの一覧表示を有効にするには、プロファイルのノードに次のプロパティを追加します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ名</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>文字列</td>
   <td>true</td>
   <td>ドラフトとフォームを送信した後、<br />フォームポータルのドラフトと送信コンポーネントに一覧表示できるようにします</td>
  </tr>
 </tbody>
</table>

デフォルトでは、AEM Forms はフォームのドラフトと送信に関連付けられたユーザーデータをパブリッシュインスタンスの /content/forms/fp ノードに保存します。カスタムのストレージプロバイダーを追加できます。詳細は、[ドラフトと送信コンポーネントのカスタムストレージ](/help/forms/using/adding-custom-storage-provider-forms.md)を参照してください。
