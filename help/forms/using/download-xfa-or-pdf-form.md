---
title: XFA または PDF フォームテンプレートのダウンロード
description: リポジトリからローカルシステムにフォームを書き出し、ダウンロードしたフォームを新しいリポジトリに移行することができます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: aa28c6c8-3ede-445b-a351-eeb0c9f9aec4
    internal-label: Interactive Communication
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 100%
---
# XFA または PDF フォームテンプレートのダウンロード {#download-an-xfa-or-a-pdf-form-template}

ダウンロード操作では、その名のとおり、リポジトリからローカルシステムにフォームを書き出すことができます。 この操作をアップロード操作と組み合わせることにより、あるリポジトリから別のリポジトリへとフォームを移行することができます。

AEM Forms では、次のアセットタイプのダウンロード操作がサポートされています。

* フォームテンプレート（XFA フォーム）
* PDF forms
* ドキュメント（非インタラクティブ PDF ファイル）

AEM Forms では、これらのフォームタイプを個別にダウンロードするか、サポートされているフォームを 1 つまたは複数含むフォルダーでダウンロードすることができます。

これらのアセットの他に、`Resource` タイプのアセットもフォルダー内に存在すればダウンロードすることができます。 この機能は、XFA フォームで参照されているリソースを、フォームとともにダウンロードできるようにするためのものです。

## 1 つまたは複数のフォームのダウンロード {#download-one-or-more-forms}

1. `https://<server>:<port>/aem/forms.html` で、AEM Forms のユーザーインターフェイスにログインします。

1. ダウンロードしたいアセットの場所に移動します。

1. アセットを選択します。 ツールバーの「**[!UICONTROL ダウンロード]** ![aem6forms_download](assets/aem6forms_download.png)」アイコンをクリックします。

   >[!NOTE]
   >
   >ダウンロードするフォームは 1 つだけ選択することができます。 複数のフォームをダウンロードする場合は、フォルダーとしてダウンロードする必要があります。

1. 表示されるダイアログボックスで、「**[!UICONTROL ダウンロード]**」をクリックします。

   AEM Forms が、選択したファイルまたはフォルダーを含む ZIP ファイルを生成します。

   フォルダーをダウンロードする場合、フォルダー内のサポートされているアセットが、既存の階層にダウンロードされます。

   ZIP ファイルは、ご利用のシステムの `Downloads` フォルダーに保存されます。

## アップロード操作に関する考慮事項 {#related-considerations-for-the-upload-operation}

* ZIP ファイルは、同じリポジトリ内の別の場所、または別のリポジトリにアップロードすることができます。
* フォルダー内のアセットの階層は、アップロード操作の間も保持されます。
* ダウンロードされたアセットに対してダウンロード前に行われたメタデータの変更は、アップロード時に反映されます。
