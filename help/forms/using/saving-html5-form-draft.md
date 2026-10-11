---
title: HTML5 フォームのドラフトでの保存
description: HTML5 フォームをドラフトとして保存し、後でフォームへの記入を再開します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 100%
---
# HTML5 フォームのドラフトでの保存 {#saving-an-html-form-as-a-draft}

HTML5 フォームをドラフトとして保存し、後でフォームへの記入を再開できます。 フォームポータルを使用すると、すべてのユーザーが HTML5 フォームを保存および復元できます。 「ドラフトとして保存」機能を有効にするには、プロファイルのノードに次の設定を追加します。

## 「ドラフトとして保存」機能を許可するためのカスタムプロファイル {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms では初期状態で「**ドラフトとして保存**」プロファイルを使用できます。 「ドラフトとして保存」プロファイルを持つフォームをレンダリングすると、HTML5 フォームのドラフト機能を有効にすることができます。 [Forms Manager](/help/forms/using/introduction-managing-forms.md) で、フォームに対する HTML レンダリングプロファイルを指定できます。

既存の[カスタムプロファイル](/help/forms/using/custom-profile.md)に対して「ドラフトとして保存」機能を有効にするには、カスタムプロファイルのノードに次のプロパティを追加します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ名</strong></td>
   <td><strong>種類</strong></td>
   <td><strong>値</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>文字列</td>
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

## ドラフトの保存と一覧表示 {#drafts-storage-and-listing}

フォームの「ドラフトとして保存」機能を有効にしてからフォームを保存すると、[ドラフトと送信コンポーネント](/help/forms/using/draft-submission-component.md)に一覧表示されます。 ドラフトと送信コンポーネントから保存しておいたフォームを取得して入力を開始できます。

ドラフトと送信コンポーネントのフォームの一覧表示を有効にするには、プロファイルのノードに次のプロパティを追加します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ名</strong></td>
   <td><strong>種類</strong></td>
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

デフォルトでは、AEM Forms はフォームのドラフトと送信に関連付けられたユーザーデータをパブリッシュインスタンスの /content/forms/fp ノードに保存します。 カスタムのストレージプロバイダーを追加できます。詳細は、[ドラフトと送信コンポーネントのカスタムストレージ](/help/forms/using/adding-custom-storage-provider-forms.md)を参照してください。
