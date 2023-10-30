---
title: 埋め込むフォントの指定
description: アダプティブフォームに埋め込むフォントを指定する方法を説明します。 Formsサービスで生成されるフォームに埋め込むフォントと埋め込まないフォントを指定できます。
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 22%

---

# 埋め込むフォントの指定 {#specifying-fonts-to-embed}

Formsサービスで生成されるフォームに常に埋め込むフォントと埋め込まないフォントを指定できます。 フォントを埋め込むと、フォームのファイルサイズが大きくなります。 ユーザーがごく一般的でないフォントをシステムに埋め込みます。 一般的にインストールされている一般的なフォントは埋め込まないでください。

>[!NOTE]
>
>Formsのカスタム XCI ファイルを指定した場合、XCI ファイルのフォントの埋め込みオプションがこれらの設定よりも優先されます。 ( 詳しくは、 [Formsの場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. 管理コンソールで、**[!UICONTROL サービス／Forms]** をクリックします。
1. 「**[!UICONTROL フォントの埋め込み設定]**」の「**[!UICONTROL 常に埋め込むフォント]**」ボックスに、フォームに埋め込むフォントの名前をコンマで区切って入力します。指定したフォントは、生成後のフォームに埋め込まれます（フォーム内で使用されている場合）。 サービスに渡される XCI ファイルでフォントの埋め込みオプションがオンになっている場合、このPDFは無視されます。この場合、フォントで使用されるすべてのフォントが常に埋め込まれるからです。
1. 「**[!UICONTROL 常に埋め込まないフォント]**」ボックスで、フォームに埋め込まないフォントの名前をコンマで区切って入力します。指定したフォントは、生成されたPDFで使用されている場合でも、PDFに埋め込まれません。 サービスに渡される XCI ファイルでフォントの埋め込みオプションがオフになっている場合、このPDFは無視されます。この場合、フォントで使用されるフォントは埋め込まれないからです。
1. 「**[!UICONTROL 保存]**」をクリックします。
