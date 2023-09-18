---
title: Correspondence Management でカスタム特殊文字を使用する
description: Correspondence Management でカスタム特殊文字を追加する方法を説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 41%

---

# Correspondence Management でカスタム特殊文字を使用する{#custom-special-characters-in-correspondence-management}

## 概要 {#overview}

Correspondence Management には、210 個の特殊文字に対するデフォルトのサポートが組み込まれており、レターに簡単に挿入できます。

たとえば、次の特殊文字を挿入できます。

* 通貨記号（€、￥、£ など）
* 数学記号（∑、√、∂、^ など）
* 句読点（「、」 など）

レターでは、次の場所で特殊文字を挿入することができます。

* [テキストエディター](/help/forms/using/document-fragments.md#createtext)
* [通信内の編集可能なインラインモジュール](../../forms/using/create-correspondence.md#managecontent)

![specialcharactersinlinemodule](assets/specialcharactersinlinemodule.png)

管理者は、カスタマイズすることで特殊文字を増やしたり、カスタムの特殊文字を追加したりすることができます。この記事では、追加のカスタム特殊文字のサポートを追加する方法について説明します。

## Correspondence Management でカスタム特殊文字のサポートを追加または変更します {#creatingfolderstructure}

カスタム特殊文字のサポートを追加するには、次の手順を実行します。

1. `https://'[server]:[port]'/[ContextPath]/crx/de` にアクセスし、管理者としてログインします。
1. apps フォルダーに、 **[!UICONTROL 特殊文字]** specialcharacters フォルダー（「libs」の下の textEditorConfig フォルダー）に似たパス/構造を持つ：

   1. 次のパスにある「**specialcharacters**」フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **オーバーレイの場所：** /apps/

      **ノードタイプを一致させる**：オン

      >[!NOTE]
      >
      >/libs ブランチは変更しないでください。 このブランチは、次の操作を行うたびに変更される可能性が高いので、加えた変更はすべて失われる場合があります。
      >
      >
      >
      >    * インスタンスでのアップグレード
      >    * ホットフィックスの適用
      >    * 機能パックのインストール
      >
      >

   1. 「**OK**」をクリックし、「**すべて保存**」をクリックします。指定されたパスに「specialcharacters」フォルダーが作成されます。

      オーバーレイを作成したら、ノード構造タグを確認します。 オーバーレイを使用して/apps で作成された各ノードは、そのノードの/libs で定義されたのと同じクラスおよびプロパティを持つ必要があります。 /apps の下のノード構造にプロパティまたはタグがない場合は、そのタグを/libs 内の対応するノードと同期します。

1. 次の点を確認します。 **[!UICONTROL textEditorConfig]** ノードには次のプロパティと値があります。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | cmConfigurationType | 文字列 | cmTextEditorConfiguration |
   | cssPath | 文字列 | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. 次のパスにある「**[!UICONTROL specialcharacters]**」フォルダーを右クリックし、**作成／子ノード**&#x200B;を選択して「**すべて保存**」をクリックします。

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;yourchildnode>

1. テキストエディタ\通信 UI の作成ページを更新します。 追加したノードは、UI の特殊文字のリストの最後のノードです。
1. 「**すべて保存**」をクリックします。
1. 必要に応じて特殊文字を変更します。

<table>
 <tbody>
  <tr>
   <td><strong>To...</strong></td>
   <td><strong>次の手順を実行します。</strong></td>
  </tr>
  <tr>
   <td>カスタマイズした特殊文字を追加する</td>
   <td>
    <ol>
     <li>必須プロパティを使用して、「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」の下に子ノードを追加します。</li>
     <li>「すべて保存」をクリックします。</li>
     <li>テキストエディタ\Correspondence UI を作成して、変更を表示します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>既存の特殊文字のプロパティを更新する</td>
   <td>
    <ol>
     <li>上述のように更新するノードをオーバーレイし、タグとクラスを検証します。</li>
     <li>caption、value、endValue、multipliCation などの値を変更します。 </li>
     <li>「すべて保存」をクリックします。 </li>
     <li>テキストエディタ\Correspondence UI を作成して、変更を表示します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>特殊文字を非表示にする</td>
   <td>
    <ol>
     <li>非表示にするノードを「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」の下にオーバーレイします。</li>
     <li>非表示にするノード（アプリケーションの下）に、sling:hideResource （ブール値）プロパティを追加します。 </li>
     <li>「すべて保存」をクリックします。 </li>
     <li>テキストエディタ\Correspondence UI を作成して、変更を表示します。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>複数の特殊文字を非表示にする</td>
   <td>
    <ol>
     <li>「sling:hideChildren (String or String[])」プロパティを「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」に追加します。 </li>
     <li>ノード名（非表示にする特殊文字）を「sling:hideChildren」プロパティの値として追加します。 </li>
     <li>「すべて保存」をクリックします。 </li>
     <li>テキストエディタ\Correspondence UI を作成して、変更を表示します。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>特殊文字の並べ替え</td>
   <td>
    <ol>
     <li>必須プロパティを使用して、「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」の下に子ノードを追加します。 </li>
     <li>新しく作成した子ノードに「sling:orderBefore (String)」プロパティを追加します。 </li>
     <li>ノード名を、新しく追加した特殊文字を表示する前の値として追加します。 </li>
     <li>「すべて保存」をクリックします。 </li>
     <li>テキストエディタ\Correspondence UI を作成して、変更を表示します。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
