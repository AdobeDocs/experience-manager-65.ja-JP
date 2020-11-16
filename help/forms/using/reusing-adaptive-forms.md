---
title: アダプティブフォームの再利用
seo-title: アダプティブフォームの再利用
description: 既存のアダプティブフォームを再利用して、新しいアダプティブフォームを作成することができます。
seo-description: 既存のアダプティブフォームを再利用して、新しいアダプティブフォームを作成することができます。
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 73%

---


# アダプティブフォームの再利用 {#reusing-adaptive-forms}

## 概要 {#introduction}

既存のアダプティブフォームの一部のプロパティを使用して新しいアダプティブフォームを生成する場合は、単純にコピーと貼り付けの機能を使用できます。さらに、新しいアダプティブフォームを希望のフォルダーパスに貼り付けることもできます。すべてのメタデータプロパティが複製され、XFA ベースのアダプティブフォームの XFA と XSD ベースのアダプティブフォームの XSD もコピーされます。

>[!NOTE]
>
>ステータスとレビューの詳細はコピーされません。例えば、アダプティブフォームが発行され、その後にそのアダプティブフォームをコピーした場合、貼り付けられるアダプティブフォームは未発行の状態になります。同様に、コピーされたアセットがレビュー中の場合、貼り付けられたアセットは同じレビュー中とはなりません。

### アダプティブフォームのコピー {#copy-an-adaptive-form}

次のいずれかの方法を使用して、アダプティブフォームをコピーします。

1. クイックアクションから ![aem6forms_copy](assets/aem6forms_copy.png) アイコンをクリックします。

   >[!NOTE]
   >
   >クイックアクションは、マウスのカーソルを合わせたときにサムネール上に表示されるアクション項目です。

1. アダプティブフォームを選択します。選択方法はビューによって異なります。

   If you are in card view, go to selection mode by clicking the selection ![aem6forms_check-circle](assets/aem6forms_check-circle.png) icon and click all the adaptive forms that you want to copy.

   リストビューの場合は、選択するすべてのアダプティブフォームのチェックボックスをオンにします。

   >[!NOTE]
   >
   >コピーと貼り付けの機能はアダプティブフォームのみをサポートしていますので、選択したアセットはすべてアダプティブフォームである必要があります。また、選択したすべてのアセットは同じフォルダー内のものである必要があります。

   After selecting the assets, click the copy ![aem6forms_copy](assets/aem6forms_copy.png) icon present in the toolbar to copy the selected adaptive form.

### アダプティブフォームの貼り付け {#paste-an-adaptive-form}

Clicking the copy action automatically exits the selection mode and makes the paste ![aem6forms_paste](assets/aem6forms_paste.png) icon visible. Now go to the desired folder path and click the paste ![aem6forms_paste](assets/aem6forms_paste.png) icon to paste the copied adaptive form.

同じフォルダー内に貼り付ける場合、または貼り付け先のフォルダー内に同じノード名（CRX リポジトリへの保存に使用される名前）の別のファイルがある場合は、接尾辞に 1 が追加されます（例えば、myaf は myaf1 となり、同じ場所に myaf1 がある場合は myaf が myaf2 になります）。その他のプロパティはすべて元のアダプティブフォームと同じになります。

貼り付けアイコン ![aem6forms_paste](assets/aem6forms_paste.png) （貼り付け）をクリックすると、再び非表示になります。 一度に行える貼り付け操作は一回だけです。同じアセットのコピーを再び作成するには、もう一度コピーします。

### 新しいアダプティブフォームのコンテンツの変更 {#change-contents-of-new-adaptive-form}

貼り付けたアダプティブフォームのコンテンツは、次の方法を用いて変更し、コピー元のフォームとは別のフォームにすることができます。

1. **メタデータプロパティの変更：**

   タイトルや説明など、アダプティブフォームのメタデータプロパティを変更できます。For more details about metadata properties and how they can be changed, see [Managing Form Metadata](/help/forms/using/manage-form-metadata.md)

1. **XFA/XSDベースのアダプティブFormsのXFA/XSDの変更：**

   アダプティブフォームで使用する XFA/XSD を変更できます。これらのアダプティブフォームの変更方法について詳しくは、「[フォームメタデータの管理](/help/forms/using/manage-form-metadata.md)」を参照してください。

1. **再発行:**

   貼り付けたアセットはコピー元のアセットとは別のものになります。エンドユーザーが使用できるように、新しいアセットとして発行することができます。アセットの公開方法について詳しくは、「[フォームの発行と非公開](/help/forms/using/publishing-unpublishing-forms.md)」を参照してください。

