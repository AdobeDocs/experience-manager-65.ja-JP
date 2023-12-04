---
title: HTML5 フォームでの手書き署名の使用
seo-title: Using Scribble Signature in HTML5 forms
description: HTML5 のフォームは、タッチデバイスでの使用が増えています。また、署名をサポートするための一般的な要件の 1 つがあります。 モバイルデバイスでのドキュメントの署名は、モバイルデバイスでのフォームの署名において受け入れられる方法となっています。
seo-description: HTML5 forms are increasingly used on touch devices, and one common requirement is to support signatures. Signing documents on mobile devices is becoming an accepted way of signing forms on mobile devices.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 22%

---

# HTML5 フォームでの手書き署名の使用{#using-scribble-signature-in-html-forms}

HTML5 のフォームは、タッチデバイスで使用される傾向が強まっています。また、共通の要件の 1 つは、署名をサポートすることです。 スタイラスや指での手書きは、モバイルデバイス上でフォームに署名する際に受け入れられる方法となっています。 HTML5 のフォームとForms Designer で、フォームに手書き署名フィールドを挿入するオプションが有効になりました。 フォームがブラウザーでレンダリングされると、スタイラス、マウス、またはタッチを使用して、これらのフィールドに署名できます。

## 手書き署名フィールドを使用してフォームをデザインする方法 {#how-to-design-a-form-using-scribble-signature-field}

1. Forms Designer でフォームを開きます。
1. ページ上に手書き署名フィールドをドラッグ＆ドロップします。

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Forms Designer で選択されたフィールドの寸法は、フィールドがレンダリングされる際に反映されます。ただし、レンダリングされた署名ボックスのサイズは、Forms Designer で指定されたサイズではなく、フィールドの縦横比に基づいて計算されます。

1. 手書き署名フィールドを設定します。

   「手書き署名」フィールドは、デフォルトで、iPadでの署名プロセス中、位置情報を必須としてマークします（他のデバイスではオプションです）。 このデフォルトの動作は `geoLocMandatoryOnIpad` プロパティの値を変更することでオーバーライドできます。このプロパティは、手書き署名フィールドにエクストラとして公開されます。 変更する手順は次のとおりです。

   1. フォームで、手書き署名フィールドを選択します。
   1. 「**XML Source**」タブを選択します。

      >[!NOTE]
      >
      >「XML Source」タブを開くには、**表示**／**XML Source** をクリックします。

   1. `<field>` タグ内にある `<ui>` タグを見つけて、ソースコードを次のようになるように変更します。

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. を選択します。 **デザインビュー** タブをクリックします。 確認ボックスで、 **はい**.
   1. フォームを保存します。

1. サポートされているデバイス/デスクトップブラウザーでフォームをレンダリングします。

## 手書き署名とのやり取り {#interfacing-with-the-scribble-signatures}

### 署名 {#signing}

手書き署名フィールドがフォームに追加されてレンダリングされたら、フィールドをクリックまたはタップすると、ダイアログボックスが開きます。 ユーザは、マウス、指、またはスタイラスを使用して、点線の長方形で指定された描画領域に署名を手書きできます。

![geolocation](assets/geolocation.png)

**A.** ブラシ **B.** 消しゴム **C.** 位置 **D.** 位置情報

### ジオタギング {#geo-tagging}

手書き中に位置情報アイコンをクリックすると、フィールドに地理的な位置と時間の情報が埋め込まれます。

>[!NOTE]
>
iPadでは、デフォルトで、位置情報の埋め込みは必須です。

iPadでは、位置情報アイコンはデフォルトでは表示されず、位置情報は、 **OK**.

iPad では、この設定はフィールドの初期化パラメーターで `geoLocManadatoryOnIpad` パラメーターの値を `0` に変更することで変えられます。

* 位置情報が必須の場合、ユーザは描画領域を縮小して表示されます。 位置情報テキストは、ユーザーがクリックすると追加されます **OK** アイコンが残りの領域に表示されます。
* その他の場合は、ユーザーには完全な描画可能領域が表示されます。 位置情報を埋め込む場合、この領域は位置情報テキストに合わせてサイズ変更されます。

### 署名のクリア {#clearing-a-signature}

この機能を使用するときに、ユーザーは&#x200B;**消しゴム**&#x200B;アイコンをクリックしてフィールドを消去し、始めからやり直すことができます。位置情報が追加された場合も、消去されます。

### 署名の保存 {#saving-a-signature}

クリック **OK** アイコンは手書きメモを画像としてフィールドに保存します。 画像と値をサーバーに送信して、さらに処理することができます。 ユーザーが **OK**&#x200B;に設定されている場合、手書きメモファイルはロックされます。 手書きウィジェットを使用して署名を再び編集することはできません。

手書きフィールドをタップまたはクリックすると、読み取り専用モードでダイアログボックスが開きます。

![3](assets/3.png)

### ペンサイズの選択 {#selecting-pen-size}

「**Brushes**」アイコンをクリックして、使用可能なペンサイズのリストを表示します。ペンのサイズをクリックして、対応するペンを使用します。

### フォームから署名を削除する {#delete-signatures-from-the-form}

フォームから署名を削除するには、次の手順を実行します。

* （モバイルデバイス）署名フィールドを長押しし、確認ダイアログで、 **はい**.
* （デスクトップ）署名フィールドにマウスポインターを置き、 **キャンセル** アイコンをクリックし、確認ダイアログで、 **はい**.
