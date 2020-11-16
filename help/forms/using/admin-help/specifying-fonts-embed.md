---
title: 埋め込むフォントの指定
seo-title: 埋め込むフォントの指定
description: 埋め込むフォントの指定方法について説明します。
seo-description: 埋め込むフォントの指定方法について説明します。
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 80%

---


# 埋め込むフォントの指定 {#specifying-fonts-to-embed}

Forms サービスで生成されるフォームに常に埋め込むフォント、または埋め込まないフォントを指定できます。フォントを埋め込むと、フォームのファイルサイズが大きくなります。ユーザーのシステムに通常存在しない珍しいフォントを埋め込みます。通常インストールされているような一般的なフォントは埋め込まないでください。

>[!NOTE]
>
>Forms のカスタム XCI ファイルを指定している場合、これらの設定より、XCI ファイルのフォントの埋め込みオプションが優先されます（[Forms の場所の設定](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)を参照）。

1. In administration console, click **[!UICONTROL Services > Forms]**.
1. Under **[!UICONTROL Font Embedding Settings]**, in the **[!UICONTROL Always Embed Fonts]** box, type the names of the fonts to embed with the forms, separated by commas. 指定するフォントは、生成されたフォームで使用されている場合にのみそのフォームに埋め込まれます。サービスに渡される XCI ファイルでフォントの埋め込みオプションが有効になっていると、この設定は無視されます。この場合は、PDF で使用されるすべてのフォントが常に埋め込まれるためです。
1. In the **[!UICONTROL Never Embed Fonts]** box, type the names of the fonts not to embed with the forms, separated by commas. 指定するフォントは、生成された PDF で使用されていてもその PDF に埋め込まれません。サービスに渡される XCI ファイルでフォントの埋め込みオプションが無効になっていると、この設定は無視されます。この場合は、PDF で使用されるフォントが一切埋め込まれないためです。
1. 「**[!UICONTROL 保存]**」をクリックします。

