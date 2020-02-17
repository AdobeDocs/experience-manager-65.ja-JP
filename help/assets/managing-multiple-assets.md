---
title: 複数のアセットとコレクションの管理
description: 複数のアセットおよびコレクションのメタデータを同時に編集して、共通のメタデータの変更をすばやくプロパゲートする方法を学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# アセットとコレクションの管理 {#managing-multiple-assets-and-collections}

Adobe Enterprise Manager（AEM）Assets を使用すると、複数のアセットのメタデータを同時に編集できるので、アセットに対して共通のメタデータの変更をすばやく一括でプロパゲートできます。複数のコレクションのメタデータを同時に編集することもできます。

プロパティページを使用して、複数のアセットまたはコレクションのメタデータを変更できます。

* メタデータプロパティを共通の値に変更する
* タグを追加または変更する

メタデータプロパティの追加、変更、削除など、メタデータプロパティページをカスタマイズするには、スキーマエディターを使用します。

>[!NOTE]
>
>一括編集メソッドは、フォルダーまたはコレクションで使用可能なアセットに対して機能します。フォルダー全体で使用可能なアセットまたは共通の基準に一致するアセットについては、[検索後にメタデータを一括更新する](search-assets.md#metadataupdates)ことが可能です。

## Edit metadata properties of multiple assets {#editing-metadata-properties-of-multiple-assets}

1. Assets ユーザーインターフェイスで、編集するアセットの場所に移動します。
1. 共通のプロパティを編集するアセットを選択します。
1. ツールバーで「]**プロパティ**[!UICONTROL 」アイコンをタップまたはクリックして、選択したアセットのプロパティページを開きます。

   >[!NOTE]
   >
   >複数のアセットを選択すると、それらのアセットに対して最も下位の共通親フォームが選択されます。つまり、プロパティページには、すべての個々のアセットのプロパティページに共通のメタデータフィールドのみが表示されます。

1. 様々なタブで選択したアセットのメタデータプロパティを変更します。
1. 特定のアセットのメタデータエディターを表示するには、リストの残りのアセットの選択を解除します。メタデータエディターのフィールドには、その特定のアセットのメタデータが入力されています。

   >[!NOTE]
   >
   >* プロパティページで、アセットのリストからアセットの選択を解除することでそのアセットを削除できます。アセットリストは、デフォルトではすべてのアセットが選択されています。リストから削除するアセットのメタデータは更新されていません。
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.


1. アセットに別のメタデータスキーマを選択するには、ツールバーの「]**設定**[!UICONTROL 」アイコンをタップまたはクリックし、目的のスキーマを選択します。
1. 変更内容を保存します。
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. このオプションを選択しないと、フィールド内の既存のメタデータが新しいメタデータに置換されます。Tap/click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >1 つの値のみを指定できるフィールドの場合、「**[!UICONTROL 追加モード]**」を選択しても、フィールド内の既存の値に新しいメタデータが追加されません。

## Edit metadata properties of multiple collections {#editing-metadata-properties-of-multiple-collections}

1. コレクションコンソールで、編集するコレクションを選択します。
1. From the toolbar, tap/click **[!UICONTROL Properties]** to open the properties page for the selected collections.
1. 様々なタブで選択したコレクションのメタデータプロパティを変更します。

   >[!NOTE]
   >
   >選択したコレクションにメタデータを追加すると、そのコレクションのタグ以外の以前のメタデータが上書きされます。Any tags you add in the **[!UICONTROL Tags]** field, are appended to the existing list of tags in the metadata.

1. 特定のコレクションのメタデータのプロパティを表示するには、コレクションリストの残りのコレクションの選択を解除します。メタデータエディターのフィールドには、その特定のコレクションのメタデータが入力されています。

   >[!NOTE]
   >
   >* コレクションのプロパティページで、コレクションのリストからコレクションの選択を解除することで、そのコレクションを削除できます。コレクションリストは、デフォルトではすべてのコレクションが選択されています。削除するコレクションのメタデータは更新されていません。
   >* At the top of the list, select the check box near **[!UICONTROL Title]** to toggle between selecting the collections and clearing the list.


1. 変更内容を保存します。

## 一括メタデータ更新の上限を設定する {#configlimit}

DOS などの状況を防ぐため、AEM では Sling 要求でサポートされるパラメーターの数を制限しています。一度に多くのアセットのメタデータを更新すると、上限に到達する可能性があり、それ以上のアセットでメタデータが更新されなくなります。AEM はログに次の警告を生成します。

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

制限を変更するには、Web コンソール（**[!UICONTROL ツール]**／**[!UICONTROL オペレーション]**／**[!UICONTROL Web コンソール]**）にアクセスし、**[!UICONTROL Apache Sling 要求のパラメーター処理]** OSGi 構成で&#x200B;**[!UICONTROL 最大 POST パラメーター]** の値を変更します。
