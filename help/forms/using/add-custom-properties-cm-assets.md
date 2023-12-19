---
title: Correspondence Management アセットにカスタムプロパティを追加
description: Correspondence Management アセットへのカスタムプロパティの追加方法について説明します。
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Correspondence Management
exl-id: ba2e145d-51ee-4844-a9e1-9927971d25a1
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '4431'
ht-degree: 97%

---

# Correspondence Management アセットへのカスタムプロパティの追加{#add-custom-properties-to-correspondence-management-assets}

## 概要 {#overview}

Correspondence Management のユーザーインターフェイスをカスタマイズし、独自のプロパティとタブのセットをユーザーに表示できます。このカスタマイズには、特定のアセットタイプとレター、またはすべてのアセットタイプとレターへのカスタムフィールド／プロパティおよびタブの追加が含まれます。

## Correspondence Management アセットにカスタムプロパティを追加 {#adding-custom-properties-to-correspondence-management-assets}

次のシナリオでは、Correspondence Management アセットおよびレターにプロパティやタブを追加する方法を示します。

* すべてのアセットタイプへの共通プロパティの追加
* すべてのアセットタイプへの共通タブの追加
* 特定のアセットタイプへのカスタムプロパティの追加

これらのシナリオでプロパティ、パスおよび値を調整することにより、要件に従い、様々なアセットのセットにカスタムプロパティおよびタブを追加できます。

### シナリオ：すべてのアセットタイプへの共通フィールド（プロパティ）の追加 {#scenario-adding-a-common-field-property-to-all-the-asset-types}

このシナリオでは、すべてのアセットタイプ（テキスト、リスト、条件、レイアウトフラグメント）とレターにカスタムプロパティを追加する方法を示します。このシナリオを使用して、すべてのアセットおよびレターにプロパティ「受信者の場所」を追加できます。「受診者の場所」プロパティにより、アセットまたはレターが関連する配信地域を特定できます。

>[!NOTE]
>
>カスタムプロパティを既に追加している場合は、そのプロパティがアセット作成ページに表示されるようになります。このようなプロパティを非表示にする方法については、「アセット作成ページとプロパティページでカスタムプロパティを表示／非表示」を参照してください。

![すべてのアセットタイプに追加されたカスタムプロパティ](assets/lcoationofrecipientsui.png)

すべてのアセットタイプおよびレターにカスタムプロパティを追加するには、次の手順を実行します。

1. `https://'[server]:[port]'/[ContextPath]/crx/de` に移動して、管理者でログインします。
1. 次の手順に従って、apps フォルダーに、（ccrui フォルダー内の）css フォルダーと同様のパス/構造で css という名前のフォルダーを作成します。

   1. 以下のパスにある items フォルダーを右クリックし、**ノードをオーバーレイ**&#x200B;を選択します。

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![ノードをオーバーレイ](assets/itemsoverlaynode.png)

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：**/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items

      **場所：** /apps/

      **ノードタイプを一致させる：**&#x200B;選択済み

      ![ノードをオーバーレイ](assets/cmmetapropertiesoverlaynode.png)

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

   1. 「**すべて保存**」をクリックします。

1. 次の手順を使用し、新規作成した items フォルダーにすべてのアセットのカスタムプロパティ用のノードを追加します（例：GeoLocation）。

   1. items フォルダーを右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。

      ![CRX でのノードの作成](assets/itemscreatenode.png)

   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** GeoLocation（または、このプロパティに与える任意の名前）

      **型：** nt:unstructured

      ![ノードを作成：GeoLocation](assets/geographicallocationcreatenode.png)

   1. 作成した新しいノード（ここでは「GeoLocation」）をクリックします。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「GeoLocation」）に次のプロパティを追加します。

      | **名前** | **種類** | **値** |
      |---|---|---|
      | fieldLabel | 文字列 | フィールド／プロパティに与える名前。（ここでは「受信者の場所」） |
      | name | 文字列 | `./extendedproperties/GeoLocation`（値は items ノードで作成したフィールド名と同じにします） |
      | renderReadOnly | ブール値 | true |
      | sling:resourceType | 文字列 | `granite/ui/components/coral/foundation/form/textfield` |

   1. 「**すべて保存**」をクリックします。

1. カスタマイズした内容を表示するには、アセット（テキスト、リスト、条件、レイアウトフラグメント）またはレターにポインタを合わせて、「**プロパティを表示**」をクリックし、「**編集**」をクリックします。新しいフィールド（受信者の場所）がアセット／レタープロパティの「基本」タブに表示されます。

   >[!NOTE]
   >
   >カスタマイズ内容を UI に表示するには、ブラウザーキャッシュを消去する必要が出る場合があります。

   ![すべてのアセットに追加されたカスタムプロパティ](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >追加したすべてのアセットの共通プロパティは、アセットプロパティの「基本」タブに表示されます。デフォルトでは、すべてのアセットに追加された共通のプロパティは、プロパティページとアセット作成ページに表示されます。 共通のプロパティを非表示にするには、<!--link to show / hide properties]--> を実行する必要があります。

### シナリオ：カスタムプロパティ／フィールドにカスタムドロップダウンおよび値を追加 {#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}

このシナリオでは、すべてのアセットタイプにカスタムプロパティを追加し、ドロップダウン値を追加する方法について説明します。

1. 次のパスにある items フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. 新しく作成したオーバーレイノード（/apps/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items）の下に、タイプ nt:unstructured のドロップダウン（ここでは `geographicallocation`）を作成する必要があるプロパティ（フィールド）のそれぞれのノードを作成します。
1. 次のプロパティをノード（ここでは「geographicallocation」）に追加し、「**すべて保存**」をクリックします。

   <table>
   <tbody>
   <tr>
      <td><strong>名前</strong></td>
      <td><strong>タイプ</strong></td>
      <td><strong>値</strong></td>
   </tr>
   <tr>
      <td>fieldLabel</td>
      <td>文字列</td>
      <td>フィールド／プロパティに与える名前。（ここでは「geographicallocation」）</td>
   </tr>
   <tr>
      <td>name</td>
      <td>文字列</td>
      <td>。/extendedproperties/geographicallocation（値は items ノードで作成したフィールド名と同じにします）</td>
   </tr>
   <tr>
      <td>renderReadOnly</td>
      <td>ブール値</td>
      <td>true</td>
   </tr>
   <tr>
      <td>sling:resourceType</td>
      <td>文字列</td>
      <td>granite/ui/components/coral/foundation/form/select<br /> </td>
   </tr>
   </tbody>
   </table>

1. プロパティノード（ここでは「geographicallocation」）に、`items` という名前の新しいノードを追加します。items ノードで、ドロップダウンの値ごとにノードを追加します。ドロップダウンのデフォルト値として機能するように、最初のノードを空白として追加し、ユーザーがフィールドに値を指定しないようにオプションを追加することをお勧めします。複数のオプション／ドロップダウンの値を追加するには、次の手順を繰り返します。

   1. プロパティノード（ここでは geographicalLocation）を右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. フィールド名に `item1,` を入力し、タイプは nt:unstructured のままにして、「**OK**」をクリックします。
   1. 次のプロパティを新しく作成したノード（ここでは「item1」）に追加し、「**すべて保存**」をクリックします。

      <table>
         <tbody>
         <tr>
          <td><strong>名前</strong></td>
          <td><strong>タイプ</strong></td>
          <td><strong>値</strong></td>
         </tr>
         <tr>
          <td>text</td>
          <td>文字列</td>
          <td>これは、ユーザーに表示されるドロップダウンオプションの値です。空白（デフォルト）値の場合は空白のままにします。または、「<strong>国際</strong>」や「<strong>米国内</strong>」<br />などの値を入力します。 </td>
         </tr>
         <tr>
          <td>value</td>
          <td>文字列</td>
          <td>テキストに対して CRXDE に保存される値。一意のキーワードを入力します。<br /> </td>
         </tr>
         </tbody>
   </table>

   ![customizationdropdownvaluescrxde](assets/customizationdropdownvaluescrxde.png)

カスタムドロップダウンは、アセットプロパティで次のように表示されます。

![drop-down_customization](assets/drop-down_customization.png)

### シナリオ：すべてのアセットタイプの共通タブ {#scenario-common-tab-for-all-asset-types}

このシナリオでは、すべてのアセットタイプ（テキスト、リスト、条件、レイアウトフラグメント）とレターにカスタムタブ「受信者」を追加する方法を示します。「受信者」タブに、受信者に関連するすべてのカスタムプロパティの配置を計画できます。

![すべてのアセットタイプに追加されたカスタムタブ](assets/recipientstab.png)

次の手順を使用して、すべてのアセットにフィールド付きのタブを追加できます。

1. `https://'[server]:[port]'/[ContextPath]/crx/de` にアクセスし、管理者としてログインします。
1. 次の手順を使用して、apps フォルダに、（コンテンツフォルダ内の）cmmetadataproperties フォルダに似たパス/構造を持つ cmmetadataproperties という名前のフォルダを作成します。

   1. 次のパスにある cmmetadataproperties フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![ノードをオーバーレイ](assets/cmmetadatapropertiesoverlaynode.png)

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/content/cmmetadataproperties

      **場所：** /apps/

      **ノードタイプを一致させる：**&#x200B;選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

      ![CRX で作成されたオーバーレイフォルダー構造](assets/cmmetadatapropertiesappsfolder.png)

      「**すべて保存**」をクリックします。

1. cmmetadataproperties フォルダーに、すべてのアセット用のカスタムタブを作成するためのノードを追加します（例：commontab）。手順は次のとおりです。

   1. cmmetadataproperties フォルダーを右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。

      ![ノードを作成](assets/cmmetadatapropertiescreatenode.png)

   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** commontab（または、このプロパティに与える任意の名前）

      **タイプ：** nt:unstructured

   1. 新しく作成したノードをクリックします（ここでは「commontab」）。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「commontab」）に次のプロパティを追加します。

      <table>
         <tbody>
         <tr>
          <td><strong>名前</strong></td>
          <td><strong>タイプ</strong></td>
          <td><strong>値</strong></td>
         </tr>
         <tr>
          <td>jcr:title</td>
          <td>文字列</td>
          <td>列に付ける名前。（ここでは「受信者」）</td>
         </tr>
         <tr>
          <td>sling:resourceType</td>
          <td>文字列</td>
          <td>granite/ui/components/coral/foundation/container<br /> </td>
   </tr>
         </tbody>
       </table>

   1. 「**すべて保存**」をクリックします。

1. 最後の手順で作成したタブノード（ここでは「commontab」）に対して、次の手順を使用して item という名前のノードを作成します。

   1. 関連のノード（ここでは「commontab」）を右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** items

      **タイプ：** nt:unstructured

   1. 「**すべて保存**」をクリックします。

1. 前の手順で作成した items ノード（commontab の下）で、カスタムタブ（commontab）内の列（ここでは「Column1」）を作成するためのノードを追加します。手順は次のとおりです（さらに列を追加するには、この手順を繰り返します）。

   1. items ノードを右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** Column1（または、このノードに与える任意の名前。この名前はユーザーインターフェイスには表示されません。）

      **タイプ：** nt:unstructured

   1. 次のプロパティをノード（ここでは「Column1」）に追加し、「**すべて保存**」をクリックします。

      <table>
         <tbody>
         <tr>
           <td><strong>名前</strong></td>
           <td><strong>タイプ</strong></td>
           <td><strong>値</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>文字列</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. 前の手順で作成したノード（ここでは「Column1」）に、item という名前のノードを作成します。手順は次のとおりです。

   1. ノード（ここでは「Column1」）を右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** items

      **タイプ：** nt:unstructured

   1. 「**すべて保存**」をクリックします。

1. カスタムタブ（ここでは受信者）でフィールドを作成するには、ノード（ここでは GeographicalLocation）を追加します。このプロパティは、作成した列に対応します。次の手順を実行して、フィールドを作成します（さらにフィールド／ノードを作成するには、これらの手順を繰り返します）。：

   1. items ノードを右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** GeographicalLocation（またはフィールドプロパティの別の名前）

      **タイプ：** nt:unstructured

   1. 次のプロパティをフィールドノード（ここでは Geographicallocation）に追加し、「**すべて保存**」をクリックします。

      | **名前** | **種類** | **値** |
      |---|---|---|
      | fieldLabel | 文字列 | 受信者の場所（またはフィールドに与える任意の名前） |
      | name | 文字列 | 。/extendedproperties/GeographicalLocation |
      | renderReadOnly | ブール値 | true |
      | sling:resourceType | 文字列 | `/libs/granite/ui/components/coral/foundation/form/textfield` |

1. レターにこのタブを追加するには、次のパスにある以下の items フォルダーに類似したパス／構造でオーバーレイフォルダーを作成します。

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   レターまたは異なるアセットに対してオーバーレイを作成するには、[assettype] を text、condition、list、datadictionary または fragment に置き換えて、次のパスを使用します。

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. 次のパスにある items フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス:** `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

      **場所：**/apps/

      **ノードタイプを一致させる：**&#x200B;選択済み

   1. 「**OK**」をクリックします。フォルダーが作成されます。「**すべて保存**」をクリックします。

1. 新規作成した items フォルダーに、アセットのカスタムタブ用のノードを追加します（ここでは「mytab」とします。この名前はユーザーインターフェイスには表示されません）。手順は次のとおりです。

   1. items フォルダーを右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** mytab（またはこのプロパティに与える名前）

      **タイプ：** nt:unstructured

   1. 作成した新しいノードをクリックします（ここでは mytab）。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「customtab」）に次の 2 つのプロパティを追加します。

      <table>
         <tbody>
         <tr>
           <td><strong>名前</strong></td>
           <td><strong>タイプ</strong></td>
           <td><strong>値</strong></td>
         </tr>
         <tr>
           <td>path<br /> </td>
           <td>文字列</td>
           <td>fd/cm/ma/gui/content/cmmetadataproperties/commontab<br /> </td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>文字列</td>
           <td>granite/ui/components/coral/foundation/include<br /> </td>
         </tr>
         </tbody>
       </table>

   1. 「**すべて保存**」をクリックします。

1. カスタマイズ内容を表示するには、関連するアセット（ここではレター）の上にポインタを合わせ、「プロパティを表示」をクリックし、「**編集**」をクリックします。新しいタブ（受信者）とフィールド（受信者の場所）がユーザーインターフェイスに表示されます。

   >[!NOTE]
   >
   >カスタマイズ内容を UI に表示するには、ブラウザーキャッシュを消去する必要が出る場合があります。

   ![レターに追加されたカスタムタブ](assets/recipientstab-1.png)

### シナリオ：特定のアセットタイプのカスタムプロパティを追加 {#scenario-adding-custom-properties-for-specific-asset-types}

このシナリオでは、すべてのテキストアセットのフィールドなど、特定のアセットタイプにプロパティを追加する方法を示します。このプロセスを使用すると、次のいずれかにプロパティを追加できます。

* テキスト
* 条件
* リスト
* レイアウトフラグメント
* データディクショナリ
* レター

例えば、テキストアセットにのみ、プロパティ「受信者の場所」を追加して、アセットが関連する地域を特定することができます。![アセットに追加されたカスタムプロパティ](assets/newtabui.png)

アセットタイプにプロパティを追加するには、次の手順を実行します。

1. `https://'[server]:[port]'/[ContextPath]/crx/de` に移動して、管理者としてログインします。
1. アセットタイプ（テキストなど）でタブを作成するには、apps フォルダーに以下のフォルダー構造を作成します。

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [AssetType] = text、condition、list、letter、datadictionary または fragment

   次の手順に従って、このフォルダー構造を作成します。

   1. 以下のパスにある items フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      例えば、テキストアセットのプロパティを作成する場合は、次のフォルダーを選択します。

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![ノードをオーバーレイ](assets/textitemstabsitemsoverlaynode1.png)

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items

      **場所：**/apps/

      **ノードタイプを一致させる：**&#x200B;選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

      「**すべて保存**」をクリックします。

1. 次の手順を使用し、新規作成した items フォルダーにアセットのカスタムタブ用のノードを追加します（例：customtab）。

   1. items フォルダーを右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** customtab（または、このプロパティに与える任意の名前）

      **タイプ：** nt:unstructured

   1. 作成した新しいノード（ここでは「customtab」）をクリックします。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「customtab」）に次の 2 つのプロパティを追加します。

      | **名前** | **種類** | **値** |
      |---|---|---|
      | sling:resourceType | 文字列 | granite/ui/components/coral/foundation/container |
      | jcr:title | 文字列 | ユーザーインターフェイス上のフィールドの名前（ここでは「My tab」） |

   1. 「**すべて保存**」をクリックします。

1. 次の手順を使用し、前の手順で作成したノード（ここでは customtab）に item という名前のノードを作成します。

   1. ノード（ここでは「customtab」）を右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** items

      **タイプ：** nt:unstructured

   1. 「**すべて保存**」をクリックします。

1. 次の手順を使用し、前の手順で作成した items ノード（customtab の下）で、カスタムタブ内の列（ここでは Column1）を作成するためのノードを追加します（さらに列を追加するには、この手順を繰り返します）。

   1. items ノードを右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** Column1（または、このノードに与える任意の名前）

      **タイプ：** nt:unstructured

   1. 次のプロパティをノード（ここでは Column1）に追加してから、「**すべて保存**」をクリックしてください。

      <table>
         <tbody>
         <tr>
           <td><strong>名前</strong></td>
           <td><strong>タイプ</strong></td>
           <td><strong>値</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>文字列</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. 次の手順を使用し、作成する各列（前の手順で作成した列、ここでは Column1）に item という名前のノードを作成します。

   1. 関連する列ノード（ここでは「Column1」）を右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** items

      **タイプ：** nt:unstructured

   1. 「**すべて保存**」をクリックします。

1. 作成した各列で、items ノードに、ユーザーインターフェイス内の新しいタブにフィールドを作成するためのノードを作成します。列でさらにフィールドを作成するには、この手順を繰り返します。

   1. 関連ノード（ここでは「Column1」の下の「items」）を右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：**&#x200B;任意の名前（ここでは GeoLocation）

      **タイプ：** nt:unstructured

   1. 次のプロパティをノードに追加して、「**すべて保存**」をクリックします。

      | **名前** | **種類** | **値** |
      |---|---|---|
      | fieldLabel | 文字列 | 受信者の場所（またはフィールドに与える任意の名前） |
      | name | 文字列 | `./extendedproperties/GeoLocation` |
      | renderReadOnly | ブール値 | true |
      | sling:resourceType | 文字列 | granite/ui/components/coral/foundation/form/textfield |

1. カスタマイズ内容を表示するには、関連するアセット（ここではテキスト）の上にポインタを合わせ、「プロパティを表示」をクリックし、「**編集**」をクリックします。新しいタブとフィールド（受信者の場所）がユーザーインターフェイスに表示されます。

   >[!NOTE]
   >
   >カスタマイズ内容を UI に表示するには、ブラウザーキャッシュを消去する必要が出る場合があります。

   ![特定のアセットに追加されたカスタムプロパティ](assets/newtabui-1.png)

### アセット作成ページでのカスタムプロパティの表示 {#display-custom-properties-on-the-asset-creation-page}

アセット作成ページにはタブレイアウトがないので、デフォルトでは、新しいタブに追加されたカスタムプロパティはプロパティページにのみ表示され、アセット作成ページには表示されません。アセット作成ページに他のプロパティと共にカスタムプロパティを表示するには、次の手順を実行する必要があります。

1. 以下のパスにある items フォルダーを右クリックしてから、「**ノードをオーバーレイ**」を選択してください。

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. ノードをオーバーレイのダイアログで、レターに次の値が表示されていることを確認します。その他のアセットタイプについては、パスは以下の表に示す通りです。

   **パス：** /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items

   **場所：**/apps/

   **ノードタイプを一致させる：**&#x200B;選択済み

   アセットのタイプに応じて、パスを次のようにする必要があります。

   | **アセット／ドキュメントタイプ** | **追加するパス** |
   |---|---|
   | テキスト | /libs/fd/cm/ma/gui/content/createasset/createtext/jcr:content/body/items/form/items/textwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | リスト | /libs/fd/cm/ma/gui/content/createasset/createlist/jcr:content/body/items/form/items/listwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | 条件 | /libs/fd/cm/ma/gui/content/createasset/createcondition/jcr:content/body/items/form/items/conditionwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | フラグメント | /libs/fd/cm/ma/gui/content/createasset/createfragment/jcr:content/body/items/form/items/fragmentwizard/items/properties/items/properties/items/tabs2/items/tab1/items |
   | レター | /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items |

1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

1. 作成したオーバーレイ items ノードに、名前が col4（またはその他の任意の名前）のノードを作成し、「**すべて保存**」をクリックします。

   例えば、以下は、レターに対して作成されたオーバーレイノードです。

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 次のプロパティを新しく作成したノード（ここでは「col4」）に追加し、「**すべて保存**」をクリックします。

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>値</strong></td>
  </tr>
  <tr>
   <td>path</td>
   <td>文字列</td>
   <td><p>このパスは、以下の場所で作成された列へのポインターです。</p>
    <ul>
     <li>すべてのアセットタイプ用の共通タブの場合：/apps/fd/cm/ma/gui/content/cmmetadataproperties/commontab/items/col1</li>
     <li>様々なアセットタイプ用の様々なプロパティの場合：/apps/fd/cm/ma/gui/content/cmmetadataproperties/properties//items/tabs/items/customtab/items/col1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>文字列</td>
   <td> granite/ui/components/coral/foundation/include<br /> </td>
  </tr>
 </tbody>
</table>

![customfieldappearinginmainproperties](assets/customfieldappearinginmainproperties.png)

レターを作成するための UI に表示される、カスタムプロパティ、言語

## カスタムプロパティを表示するリスト表示のカスタマイズ {#customize-the-list-view-to-show-custom-properties}

Correspondence Management アセットにカスタムプロパティを追加した後、CRX/DE でさらに変更を行って、カスタムプロパティが Correspondence Management UI に表示されるようにする必要があります。

Correspondence Management のアセットリスト UI にカスタムプロパティを表示するには、次の手順を実行します。

1. `https://'[server]:[port]'/[ContextPath]/crx/de`に移動して、管理者としてログインしてください。
1. apps フォルダーに以下のフォルダー構造を作成します。

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   次の手順に従って、このフォルダー構造を作成します。

   1. 次のパスにある columns フォルダーを右クリックしてから、「**ノードをオーバーレイ**」を選択してください。

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：**/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns

      **場所：**/apps/

      **ノードタイプを一致させる：**&#x200B;選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

      「**すべて保存**」をクリックします。

1. 作成したプロパティごとに、ユーザーインターフェイスで列を作成するためのノードを列ノードに作成します。UI でさらに列を作成するには、この手順を繰り返します。

   1. 関連するノード（列）を右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：**&#x200B;任意の名前（ここでは GeographicalLocation）

      **タイプ：** nt:unstructured

   1. 次のプロパティをノードに追加して、「**すべて保存**」をクリックします。

      <table>
         <tbody>
         <tr>
           <td><strong>名前</strong></td>
           <td><strong>タイプ</strong></td>
           <td><strong>値</strong></td>
         </tr>
         <tr>
           <td>jcr:primaryType</td>
           <td>名前</td>
           <td><p>nt:unstructured</p> </td>
         </tr>
         <tr>
           <td>jcr:title</td>
           <td>文字列</td>
           <td><p>GeographicalLocation</p> <p>この値は、UI に列ヘッダーとして表示されます。 </p> </td>
         </tr>
         <tr>
           <td>sortable</td>
           <td>ブール値</td>
           <td><p>true</p> <p>値を「true」に設定した場合、ユーザーはこの列内の値を並べ替えることができます。 </p> </td>
         </tr>
         </tbody>
       </table>

1. apps フォルダーに以下のフォルダー構造を作成します。

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   次の手順に従って、このフォルダー構造を作成します。

   1. 次のパスにある columns フォルダーを右クリックしてから、「**ノードをオーバーレイ**」を選択してください。

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：**/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage

      **場所：**/apps/

      **ノードタイプを一致させる：**&#x200B;選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

      「**すべて保存**」をクリックします。

1. 以下の場所から childlistpage.jsp ファイルをコピーします。

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   ファイルを次の場所に貼り付けます。

   /apps//fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/

1. childlistpage.jsp ファイル（/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp）を開き、次の変更を行います。

   1. ファイルの 19 行目に以下の内容を追加します（著作権表記の後）。

      ```jsp
      <%@page import="java.util.Map"%>
      ```

   1. 各カスタムプロパティの値を取得する関数の次のコードを、ファイルの最後に追加します。

      ```jsp
      <%!
          private String getCustomPropertyValue(Map<String, Object> extendedProperties, String propertyName) {
      
              String propertyValue = "";
              if (extendedProperties.containsKey(propertyName)) {
                  propertyValue = (String) extendedProperties.get(propertyName);
              }
      
              return propertyValue;
          }
      %>
      ```

   1. &lt;tr> タグ (&lt;tr &lt;%= attrs.build() %>>): の前に以下を追加します。

      ```jsp
      <%
          String GeoLocation = "";
          if (asset != null) {
                  Map<String, Object> extendedProperties = asset.getExtendedProperties();
                  if (extendedProperties != null) {
                      GeoLocation = getCustomPropertyValue(extendedProperties,"GeoLocation");
                  }
          }
      %>
      ```

      このコードで、GeoLocation はカスタムのノードまたはフィールドの作成時に name プロパティで設定した値です。カスタムのノードまたはフィールドを作成する際に、プロパティの名前を /extendedproperties/ prefix: ./extendedproperties/GeoLocation で指定しました。このコードで、プレフィックスは不要です。

   1. UI に新しいプロパティを表示するには、終了 tr (&lt;/tr>) タグの前に TD タグを以下のように追加します。

      ```jsp
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      列をさらに追加するには、手順 6.3 と 6.4 を繰り返します。

   1. 「**すべて保存**」をクリックします。

1. カスタマイズ内容を表示するには、カスタムプロパティを追加したドキュメントフラグメントまたはレターのリスト表示を開きます。

   この手順で追加された UI 列とプロパティは、すべてのアセットタイプに対して表示されます。ただし、これらのプロパティの値は、最初にカスタムプロパティを追加したアセットタイプに対してのみ、入力および表示できます。

   例えば、「シナリオ：特定のアセットタイプのカスタムプロパティの追加」を使用してテキストアセットにカスタムプロパティを追加した場合、テキストアセットにのみカスタムプロパティを入力できます。ただし、そのカスタムプロパティを UI に表示する場合、列はすべてのアセットタイプで表示されます。

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. （オプション）デフォルトでは、新しい列は UI の最後の列として表示されます。列を特定の位置に表示するには、次のプロパティを列ノードに追加します。

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td>
   <td><strong>タイプ</strong></td>
   <td><strong>値</strong></td>
  </tr>
  <tr>
   <td>sling:orderBefore</td>
   <td>文字列</td>
   <td><p>パス「/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns」にある列ノードの名前。この前にカスタム列を UI に表示する必要があります。</p> <p>ここで、「バージョン列」の前（左側）に「地理的な場所」列を表示する場合は、プロパティ sling:orderBefore を GeoLocation ノード（パス「"/apps/fd/cm/ma/gui/cmassets/jcr:content/views/list/columns/GeoLocation"」）に追加し、プロパティの値を version に設定します。</p> </td>
  </tr>
 </tbody>
</table>

sling:orderBefore プロパティを追加して列の位置を指定する場合は、この手順の手順 6.4 で指定した対応する &lt;td> タグの順序も更新する必要があります。例えば、この場合、地理的な場所の &lt;td> タグがバージョン列の &lt;td> タグの前に配置されていることを確認する必要があります。

```xml
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
```

## カスタムプロパティの検索を有効にする {#enable-search-for-custom-properties}

デフォルトでは、フルテキスト検索には、CRX/DE を使用して UI に追加したカスタムプロパティは含まれません。

カスタムプロパティを検索に含めるには、カスタムプロパティのインデックス作成を許可する必要があります。

カスタムプロパティのインデックス作成を可能にするには、次の手順を実行します。

1. `https://'[server]:[port]'/[ContextPath]/crx/de`に移動して、管理者としてログインしてください。
1. `/oak:index/cmLucene`に移動して、その下に&#x200B;**aggregates**&#x200B;という名前のノードを追加してください。

   1. cmLucene フォルダーを右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** aggregates

      **タイプ：** nt:unstructured

   1. 「**すべて保存**」をクリックします。

1. 新規作成した aggregates フォルダーに、ノード cm:resource を追加します。cm:resource の下に、include0 という名前のノードを追加します。

   1. aggregates フォルダーを右クリックし、**作成**／**ノードを作成**&#x200B;を選択します。ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** cm:resource

      **タイプ：** nt:unstructured

   1. cm:resource フォルダーを右クリックして、**作成**／**ノードを作成**&#x200B;を選択します。ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** include0

      **型：** nt:unstructured

   1. 作成した新しいノード（ここでは「include0」）をクリックします。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「include0」）に次のプロパティを追加します。

      <table>
         <tbody>
         <tr>
           <td><strong>名前</strong></td>
           <td><strong>タイプ</strong></td>
           <td><strong>値</strong></td>
         </tr>
         <tr>
           <td>path</td>
           <td>文字列</td>
           <td>extendedProperties<br /> </td>
         </tr>
         </tbody>
       </table>

   1. 「**すべて保存**」をクリックします。

1. 次の場所にあるプロパティに移動し、その下にノードを追加します。`/oak:index/cmLucene/indexRules/cm:resource/properties`

   検索に追加する各カスタムプロパティについて、この手順を繰り返します。

   1. properties フォルダーを右クリックして、**作成**／**ノードを作成**&#x200B;を選択します。
   1. ノードを作成ダイアログに次の値が表示されていることを確認し、「**OK**」をクリックします。

      **名前：** location（または、検索に追加するカスタムプロパティの名前）

      **型：** nt:unstructured

   1. 作成した新しいノード（ここでは「location」）をクリックします。CRX にノードのプロパティが表示されます。
   1. このノード（ここでは「location」）に次のプロパティを追加します。

      | **名前** | **種類** | **値** |
      |---|---|---|
      | analyzed | 文字列 | true |
      | name | 文字列 | extendedProperties/location（または、検索に追加するプロパティの名前） |
      | propertyIndex | ブール値 | true |
      | useInSuggest | ブール値 | true |

   1. 「**すべて保存**」をクリックします。

1. フルテキスト検索でカスタムプロパティの値を使用して関連アセットを検索できるようになりました。

>[!NOTE]
>
>まだ検索できない場合は、インデックス作成の問題が原因の可能性があります。インデックスを再作成するには、次のノードに移動し、プロパティ「re-index」の値を true に変更します。
>
>/oak:index/cmLucene およびプロパティの値の変更

## 検索ページのデフォルト表示を変更 {#change-default-view-of-the-search-page}

1. `https://'[server]:[port]'/[ContextPath]/crx/de` にアクセスし、管理者としてログインします。
1. apps フォルダーに、 /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views の list フォルダーに似たパス/構造で list という名前のフォルダーを作成します。

   1. 次のパスにある items フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：**/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list

      **場所：**/apps/

      **ノードタイプを一致させる：**&#x200B;選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

   1. 「**すべて保存**」をクリックします。

1. 新しく作成したノード list で、次のプロパティを追加し、「**すべて保存**」をクリックします。

   <table>
   <tbody>
   <tr>
      <td><strong>名前</strong></td>
      <td><strong>タイプ</strong></td>
      <td><strong>値</strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>文字列</td>
      <td>card</td>
   </tr>
   </tbody>
   </table>

1. カスタマイズにより、フォームとドキュメント、アセット、サイトを含むすべてのコンソールでリスト表示に検索結果が表示されます。

## アセットページのデフォルト表示を変更 {#change-default-view-of-the-assets-page}

>[!NOTE]
>
>以下の手順により、フォーム、ドキュメント、アセット、サイトなどのすべてのコンソールのデフォルト表示が変更されます。

1. `https://'[server]:[port]'/[ContextPath]/crx/de` にアクセスし、管理者としてログインします。
1. apps フォルダーに、次のリストフォルダーに類似したパス/構造で list という名前のフォルダーを作成します。

   /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/

   1. 次のパスにある items フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list

      **場所：** /apps/

      **ノードタイプを一致させる：**&#x200B;選択済み

   1. 「**OK**」をクリックします。apps フォルダーにフォルダー構造が作成されます。

   1. 「**すべて保存**」をクリックします。

1. 新しく作成したノード list で、次のプロパティを追加し、「**すべて保存**」をクリックします。

   <table>
   <tbody>
   <tr>
      <td><strong>名前</strong></td>
      <td><strong>タイプ</strong></td>
      <td><strong>値</strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>文字列</td>
      <td>card</td>
   </tr>
   </tbody>
   </table>

1. ブラウザーの Cookie を消去するか、ブラウザーの匿名モードを使用して、アセットを表示します。アセットページは、デフォルトではカードレイアウトで表示されます。

## アセット作成ページとプロパティページでカスタムプロパティを表示／非表示 {#show-hide-custom-properties-on-asset-creation-and-properties-pages}

カスタムプロパティを表示または非表示にするには、次の手順を実行します。

1. カスタムプロパティノード（geographicallocation など）の下に、「granite:rendercondition」という名前で「nt:unstructured」タイプのノードを作成します。
1. 次のプロパティをノードに追加し、「**すべて保存**」をクリックします。

   <table>
   <tbody>
   <tr>
      <td><strong>名前</strong></td>
      <td><strong>タイプ</strong></td>
      <td><strong>値</strong></td>
   </tr>
   <tr>
      <td>sling:resourceType<br /> </td>
      <td>文字列</td>
      <td>fd/cm/ma/gui/components/admin/assetsproperties/custompropertyconfig<br /> </td>
   </tr>
   </tbody>
   </table>

1. アセット作成ページでこのプロパティを非表示にするには、次のプロパティを追加し、「**すべて保存**」をクリックします。

   <table>
   <tbody>
   <tr>
      <td><strong>名前</strong></td>
      <td><strong>タイプ</strong></td>
      <td><strong>値</strong></td>
   </tr>
   <tr>
      <td>hideOnCreate<br /> </td>
      <td>ブール値</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

1. アセットのプロパティページでカスタムプロパティを非表示にするには、次のプロパティを追加し、「**すべて保存**」をクリックします。

   <table>
   <tbody>
   <tr>
      <td><strong>名前</strong></td>
      <td><strong>タイプ</strong></td>
      <td><strong>値</strong></td>
   </tr>
   <tr>
      <td>hideOnEdit<br /> </td>
      <td>ブール値</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

   値を再び表示するには、プロパティの値を `false` に再設定するか、プロパティエントリを削除します。
