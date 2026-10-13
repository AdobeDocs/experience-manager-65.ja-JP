---
title: フォームを分類するための新しいフォルダーの作成
description: フォルダーを使用して、フォームテンプレート、PDF、リソース、およびアダプティブフォームを整理します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 100%
---
# フォームを分類するための新しいフォルダーの作成 {#create-new-folders-to-categorize-forms}

フォルダーを使用することでアセットをより良く整理できます。 AEM Forms は様々なタイプのアセット（フォームテンプレート、PDF、ドキュメント、リソース、およびアダプティブフォームと、様々なメタデータ）をサポートしているので、フォルダーを使用して必要な条件に基づきフォームを分類できます。

AEM Forms では、フォルダーのタイトルを変更できます。 タイトルは、フォルダーがリポジトリ内で保存されるノードの名前と同じではありません。 タイトルはフォルダーのメタデータとして保持されます。 フォルダーのタイトルを変更しても、フォルダー内にあるアセットのパスは影響されません。

## フォルダーの作成 {#create-a-folder}

次のいずれかの方法で、AEM Forms でフォルダーを作成できます。

* アセットを含む ZIP ファイルを必要なフォルダー構造にアップロードする（[AEM Forms での XDP および PDF ドキュメントの取得](/help/forms/using/get-xdp-pdf-documents-aem.md)を参照）

* 空白フォルダーの作成

1. `https://<server>:<port>/aem/forms.html` で、AEM Forms ユーザーインターフェイスにログインします。
1. フォルダーを作成する場所に移動します。
1. ツールバーの ![aem6forms_add](assets/aem6forms_add.png) アイコンをクリックし、「**[!UICONTROL フォルダーを作成]**」を選択します。

1. 以下の詳細を入力します。

   * **タイトル**：フォルダーの表示名
   * **名前**：*（必須）*&#x200B;リポジトリー内のフォルダーを保存するノード名

   >[!NOTE]
   >
   >デフォルトでは、名前フィールドの値がタイトルから自動入力されます。 名前には、英数字、ハイフン（-）、下線（_）のみを含めることができます。 タイトルにその他の特殊文字を入力すると、それらは自動的にハイフンに置換され、この新しい名前を確認するよう指示されます。 提示された名前をそのまま使用するか、またはそれを編集できます。

1. 「**[!UICONTROL 送信]」をクリックします。**

   定義したタイトルを持つ新しいフォルダーは、アセットリスト内の現在の場所に表示されます。

   指定した名前を持つフォルダーが既に存在する場合は、送信はエラーになり失敗します。 名前フィールドの横に表示されるエラー ![aem6forms_error_alert](assets/aem6forms_error_alert.png) アイコンの上にマウスポインターを置くと、エラーメッセージを見ることができます。

### フォルダータイトルの編集 {#edit-the-folder-title-br}

1. タイトルを編集するフォルダーを選択します。
1. ツールバーで、編集 ![aem6forms_edit](assets/aem6forms_edit.png) アイコンをクリックします。
1. 新しいタイトルを入力します。 テキストフィールドは、フォルダータイトルの現在の値で自動入力されます。 それを新しい値に変更できます。
1. 「**[!UICONTROL 送信]」をクリックします。**
