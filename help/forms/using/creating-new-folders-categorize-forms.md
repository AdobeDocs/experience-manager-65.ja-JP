---
title: フォームを分類するための新しいフォルダーの作成
seo-title: Create new folders to categorize forms
description: フォルダーを使用して、フォームテンプレート、PDF、リソース、およびアダプティブフォームを整理します。
seo-description: Use folders to organize your form templates, PDFs, resources, and adaptive forms.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Admin
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: ht
source-wordcount: '393'
ht-degree: 100%

---

# フォームを分類するための新しいフォルダーの作成 {#create-new-folders-to-categorize-forms}

フォルダーを使用することでアセットをより良く整理できます。AEM Forms はさまざまなタイプのアセット（フォームテンプレート、PDF、ドキュメント、リソース、およびアダプティブフォームと、さまざまなメタデータ）をサポートしているので、フォルダーを使用して必要な条件に基づきフォームを分類できます。

AEM Forms では、フォルダーのタイトルを変更できます。タイトルは、フォルダーがリポジトリ内で保存されるノードの名前と同じではありません。タイトルはフォルダーのメタデータとして保持されます。フォルダーのタイトルを変更しても、フォルダー内にあるアセットのパスは影響されません。

## フォルダーの作成 {#create-a-folder}

次のいずれかの方法で、AEM Forms でフォルダーを作成できます。

* アセットを含む ZIP ファイルを必要なフォルダー構造にアップロードする（[AEM Forms での XDP および PDF ドキュメントの取得](/help/forms/using/get-xdp-pdf-documents-aem.md)を参照）

* 新しい空白フォルダーを作成する

1. `https://<server>:<port>/aem/forms.html` で、AEM Forms ユーザーインターフェイスにログインします。
1. フォルダーを作成する場所に移動します。
1. ツールバーの ![aem6forms_add](assets/aem6forms_add.png) アイコンをクリックし、「**[!UICONTROL フォルダーを作成]**」を選択します。

1. 以下の詳細を入力します。

   * **タイトル**：フォルダーの表示名
   * **名前**：*（必須）*&#x200B;リポジトリー内のフォルダーを保存するノード名

   >[!NOTE]
   >
   >デフォルトでは、名前フィールドの値がタイトルから自動入力されます。名前には、英数字、ハイフン（-）、下線（_）のみを含めることができます。タイトルにその他の特殊文字を入力すると、それらは自動的にハイフンに置換され、この新しい名前を確認するよう指示されます。提示された名前をそのまま使用するか、またはそれを編集できます。

1. 「**[!UICONTROL 送信]」をクリックします。**

   定義したタイトルを持つ新しいフォルダーは、アセットリスト内の現在の場所に表示されます。

   指定した名前を持つフォルダーが既に存在する場合は、送信はエラーになり失敗します。名前フィールドの横に表示されるエラー ![aem6forms_error_alert](assets/aem6forms_error_alert.png) アイコンの上にマウスポインターを置くと、エラーメッセージを見ることができます。

### フォルダータイトルの編集 {#edit-the-folder-title-br}

1. タイトルを編集するフォルダーを選択します。
1. ツールバーで、編集 ![aem6forms_edit](assets/aem6forms_edit.png) アイコンをクリックします。
1. 新しいタイトルを入力します。テキストフィールドは、フォルダータイトルの現在の値で自動入力されます。それを新しい値に変更できます。
1. 「**[!UICONTROL 送信]」をクリックします。**
