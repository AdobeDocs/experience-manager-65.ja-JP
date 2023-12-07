---
title: 埋め込むフォントの指定
description: アダプティブフォームに埋め込むフォントを指定する方法を説明します。 Formsサービスで生成されるフォームに埋め込むフォントと埋め込まないフォントを指定できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 22%

---

# 埋め込むフォントの指定{#specify-fonts-to-embed}

Output で使用されるフォームに常に埋め込むフォントと埋め込まないフォントを指定できます。 フォントを埋め込むと、フォームのファイルサイズが大きくなります。 ユーザーがシステムに持っていない可能性の高い珍しいフォントを埋め込み、インストールする一般的なフォントを埋め込みません。

>[!NOTE]
>
>Output のカスタム XCI ファイルを指定した場合、XCI ファイルのフォントの埋め込みオプションがこれらの設定よりも優先されます。 ( 詳しくは、 [Output のファイルの場所を指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. 管理コンソールで、サービス／Output をクリックします。
1. 「フォントの埋め込み設定」の「常に埋め込むフォント」ボックスに、フォームに埋め込むフォントの名前をコンマで区切って入力します。指定したフォントは、生成後のフォームに埋め込まれます（フォーム内で使用されている場合）。 サービスに渡される XCI ファイルで、埋め込みフォントオプションがオンになっている場合、この設定は無視されます。 その場合、PDFで使用されるすべてのフォントが常に埋め込まれます。
1. 「常に埋め込まないフォント」ボックスで、フォームに埋め込まないフォントの名前をコンマで区切って入力します。指定したフォントは、生成されたPDFで使用されている場合でも、PDFに埋め込まれません。 サービスに渡される XCI ファイルで、埋め込みフォントオプションがオフになっている場合、この設定は無視されます。 その場合、埋め込まれるフォントはPDFにはありません。
1. 「保存」をクリックします。
