---
title: Correspondence Management でカスタム特殊文字を使用する
seo-title: Correspondence Management でカスタム特殊文字を使用する
description: Correspondence Management でカスタム特殊文字を追加する方法について説明します。
seo-description: Correspondence Management でカスタム特殊文字を追加する方法について説明します。
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Correspondence Management でカスタム特殊文字を使用する{#custom-special-characters-in-correspondence-management}

## 概要 {#overview}

Correspondence Managementhas では210 種類の特殊文字に初期状態から対応しており、レターに簡単に挿入できます。

たとえば、次の特殊文字を挿入できます。

* 通貨記号（€、¥、£など）
* 数学記号（∑、√、∂、^など）
* 句読点の記‟号と

レターでは、次の場所で特殊文字を挿入することができます。

* In the [text editor](/help/forms/using/document-fragments.md#createtext)
* In an [editable, inline module in a correspondence](../../forms/using/create-correspondence.md#managecontent)

![specialcharactersinlinemodule](assets/specialcharactersinlinemodule.png)

管理者は、カスタマイズすることで特殊文字を増やしたり、カスタムの特殊文字を追加したりすることができます。この記事では、カスタムの特殊文字を対以下する方法について説明します。

## Correspondence Management でカスタム特殊文字を追加・編集する {#creatingfolderstructure}

カスタム特殊文字の追加手順は次のとおりです。

1. Go to `https://'[server]:[port]'/[ContextPath]/crx/de` and login as Administrator.
1. In the apps folder, create a folder named **[!UICONTROL specialcharacters]** with path/structure similar to the specialcharacters folder (located in the textEditorConfig folder under libs):

   1. Right-click the **specialcharacters** folder at the following path and select **Overlay Node**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **オーバーレイの場所：** /apps/

      **ノードタイプを一致：** チェック済み

      >[!NOTE]
      >
      >/libsブランチは変更しないでください。 次の操作を行った場合はこのブランチが変更されるため、各自で加えた変更はすべて失われます。
      >
      >
      >
      >    * インスタンス上でのアップグレード
      >    * ホットフィックスの適用
      >    * 機能パックのインストール


   1. 「**OK**」をクリックし、「**すべて保存**」をクリックします。指定したパスに「specialcharacters」フォルダーが作成されます。

      オーバーレイを作成したら、ノード構造タグを確認します。オーバーレイを使用して/ apps 内に作成された各ノードは、そのノードの/libs 内で定義されているのと同じクラスとプロパティを持つ必要があります。/apps の下にあるノード構造にプロパティまたはタグがない場合は、タグを /libs 内の対応するノードと同期させます。



1. **[!UICONTROL textEditorConfig]** ノードには次のプロパティや値があることを確認してください。

   | 名前 | タイプ | 値 |
   |---|---|---|
   | cmConfigurationType | 文字列 | cmTextEditorConfiguration |
   | cssPath | 文字列 | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Right-click the **[!UICONTROL specialcharacters]** folder at the following path and select **Create > Child Node** and then click **Save All**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;YourChildNode>

1. 「テキストエディタ\Correspondence UI の作成」ページを更新します。追加したノードは、UI 内の特殊文字リストで最後のノードです。
1. 「**すべて保存**」をクリックします。
1. 必要に応じて、次のように特殊文字を変更します。

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
     <li>「/追加apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」の下に必須のプロパティを持つ子ノード。</li>
     <li>「すべて保存」をクリックします。</li>
     <li>変更を表示するには、「テキストエディタ\Correspondence UI の作成」ページを更新します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>既存の特殊文字プロパティを更新する</td>
   <td>
    <ol>
     <li>更新するノードを上で説明したようにオーバーレイし、タグとクラスを検証します。</li>
     <li>caption、value、end value、multipliCation などの値を変更します。 </li>
     <li>「すべて保存」をクリックします。 </li>
     <li>変更を表示するには、「テキストエディタ\Correspondence UI の作成」ページを更新します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>特殊文字を非表示にする</td>
   <td>
    <ol>
     <li>非表示にするノードを「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」の下にオーバーレイします。</li>
     <li>非表示にす追加るノード（アプリケーションの下）に対するsling:hideResource (Boolean)プロパティ。 </li>
     <li>「すべて保存」をクリックします。 </li>
     <li>変更を表示するには、「テキストエディタ\Correspondence UI の作成」ページを更新します。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>複数の特殊文字を非表示にする</td>
   <td>
    <ol>
     <li>追加「sling:hideChildren (String or String[])」プロパティを「/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」に設定します。 </li>
     <li>ノード名（非表示にする特殊文字）を「sling:hideChildren」プロパティの値として追加します。 </li>
     <li>「すべて保存」をクリックします。 </li>
     <li>変更を表示するには、「テキストエディタ\Correspondence UI の作成」ページを更新します。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>特殊文字の並び替え</td>
   <td>
    <ol>
     <li>「/追加apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters」の下に必須のプロパティを持つ子ノード。 </li>
     <li>新しく作成された子ノードに sling:orderBefore (String) プロパティを追加します。 </li>
     <li>新たに追加した特殊文字の前に、ノード名を値として追加します。 </li>
     <li>「すべて保存」をクリックします。 </li>
     <li>変更を表示するには、「テキストエディタ\Correspondence UI の作成」ページを更新します。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

