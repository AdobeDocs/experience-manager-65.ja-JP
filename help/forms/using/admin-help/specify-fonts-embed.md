---
title: 埋め込むフォントの指定
seo-title: 埋め込むフォントの指定
description: 埋め込むフォントの指定方法について説明します。
seo-description: 埋め込むフォントの指定方法について説明します。
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 100%

---


# 埋め込むフォントの指定{#specify-fonts-to-embed}

Output で使用されるフォームに常に埋め込むフォント、または埋め込まないフォントを指定できます。フォントを埋め込むと、フォームのファイルサイズが大きくなります。ユーザーのシステムに通常存在しない珍しいフォントを埋め込みます。インストールされるような一般的なフォントは埋め込まないでください。

>[!NOTE]
>
>Output のカスタム XCI ファイルを指定している場合、これらの設定は、XCI ファイルのフォントの埋め込みオプションにより変更されます（[Output のファイルの場所の指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)を参照）。

1. 管理コンソールで、サービス／Output をクリックします。
1. 「フォントの埋め込み設定」の「常に埋め込むフォント」ボックスに、フォームに埋め込むフォントの名前をコンマで区切って入力します。指定するフォントは、生成されたフォームで使用されている場合にのみそのフォームに埋め込まれます。サービスに渡される XCI ファイルでフォントの埋め込みオプションが有効になっていると、この設定は無視されます。このオプションが有効の場合、PDF で使用されるすべてのフォントが常に埋め込まれます。
1. 「常に埋め込まないフォント」ボックスで、フォームに埋め込まないフォントの名前をコンマで区切って入力します。指定するフォントは、生成された PDF で使用されていてもその PDF に埋め込まれません。サービスに渡される XCI ファイルでフォントの埋め込みオプションが無効になっていると、この設定は無視されます。このオプションが無効の場合、PDF で使用されるフォントは一切埋め込まれません。
1. 「保存」をクリックします。

