---
title: HTML5 フォームのドラフトでの保存
seo-title: HTML5 フォームのドラフトでの保存
description: HTML5 フォームをドラフトとして保存し、後でフォームへの記入を再開します。
seo-description: HTML5 フォームをドラフトとして保存し、後でフォームへの記入を再開します。
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 66%

---


# HTML5 フォームのドラフトでの保存  {#saving-an-html-form-as-a-draft}

HTML5 フォームをドラフトとして保存し、後でフォームへの記入を再開できます。フォームポータルを使用すると、すべてのユーザーが HTML5 フォームを保存および復元できます。「ドラフトとして保存」機能を有効にするには、プロファイルノードに次の設定を追加します。

## 「ドラフトとして保存」機能を許可するためのカスタムプロファイル{#custom-profile-to-allow-save-as-draft-feature}

AEM Formsは初期状態で、「**ドラフトとして保存**」プロファイルを提供します。 「ドラフトとして保存」プロファイルを持つフォームをレンダリングすると、HTML5 フォームのドラフト機能を有効にすることができます。[Forms Manager](/help/forms/using/introduction-managing-forms.md) で、フォームに対する HTML レンダリングプロファイルを指定できます。

既存の[カスタムプロファイル](/help/forms/using/custom-profile.md)に対して「ドラフトとして保存」機能を有効にするには、カスタムプロファイルノードに次のプロパティを追加します。

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
   <td>String</td>
   <td>true</td>
   <td><p>このプロファイルの「ドラフトとして保存」機能を</p> <p>有効にします。</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>文字列</td>
   <td>true</td>
   <td><p>このプロファイルと一緒に添付ファイル</p> <p>をアップロードすることを許可します。</p> </td>
  </tr>
 </tbody>
</table>

## ドラフトの保存と一覧表示  {#drafts-storage-and-listing}

フォームの「ドラフトとして保存」機能を有効にしてからフォームを保存すると、[ドラフトと送信コンポーネント](/help/forms/using/draft-submission-component.md)に一覧表示されます。ドラフトと送信コンポーネントから保存しておいたフォームを取得して再入力できます。

ドラフトと送信コンポーネントのフォームリストを有効にするには、プロファイルノードに次のプロパティを追加します。

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
   <td>ドラフトとフォームを送信後に<br />Formsポータルのドラフトと送信コンポーネントに一覧表示できるようにするには</td>
  </tr>
 </tbody>
</table>

デフォルトでは、AEM Formsはフォームのドラフトと送信に関連付けられたユーザーデータを発行インスタンスの/content/forms/fpノードに保存します。 カスタムのストレージプロバイダーを追加できます。詳細は、「[ドラフトと送信コンポーネントのカスタムストレージ](/help/forms/using/adding-custom-storage-provider-forms.md)」を参照してください。
