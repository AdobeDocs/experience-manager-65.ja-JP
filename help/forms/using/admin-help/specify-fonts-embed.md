---
title: 埋め込むフォントを指定する
description: アダプティブフォームに埋め込むフォントの指定方法について説明します。Forms サービスで生成されるフォームに埋め込むフォント、または埋め込まないフォントを指定できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 100%

---

# 埋め込むフォントを指定する{#specify-fonts-to-embed}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Output で使用されるフォームに常に埋め込むフォント、または埋め込まないフォントを指定できます。フォントを埋め込むと、フォームのファイルサイズが大きくなります。ユーザーのシステムに通常存在しない珍しいフォントを埋め込みます。インストールされるような一般的なフォントは埋め込まないでください。

>[!NOTE]
>
>Output のカスタム XCI ファイルを指定している場合、これらの設定は、XCI ファイルのフォントの埋め込みオプションにより変更されます（[Output のファイルの場所の指定](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)を参照）。

1. 管理コンソールで、サービス／Output をクリックします。
1. 「フォントの埋め込み設定」の「常に埋め込むフォント」ボックスに、フォームに埋め込むフォントの名前をコンマで区切って入力します。指定するフォントは、生成されたフォームで使用されている場合にのみそのフォームに埋め込まれます。サービスに渡される XCI ファイルでフォントの埋め込みオプションが有効になっていると、この設定は無視されます。このオプションが有効の場合、PDF で使用されるすべてのフォントが常に埋め込まれます。
1. 「常に埋め込まないフォント」ボックスで、フォームに埋め込まないフォントの名前をコンマで区切って入力します。指定するフォントは、生成された PDF で使用されていても、その PDF に埋め込まれません。サービスに渡される XCI ファイルでフォントの埋め込みオプションが無効になっていると、この設定は無視されます。このオプションが無効の場合、PDF で使用されるフォントは一切埋め込まれません。
1. 「保存」をクリックします。
