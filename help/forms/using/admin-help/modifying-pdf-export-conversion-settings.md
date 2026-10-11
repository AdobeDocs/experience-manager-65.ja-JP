---
title: PDF の書き出しの変換設定の変更
description: PDF の書き出しの変換設定の変更方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 48a5d992-4681-41a8-8d1d-4da6767134c2
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 100%
---
# PDF の書き出しの変換設定の変更 {#modifying-the-pdf-export-conversion-settings}

以下の手順で、PDF、EPS、DOC、TXT、RTF、XML、HTML の各ファイルの書き出しに使用される変換設定を変更します。 デフォルトでは、PDF ファイルでは、Adobe Acrobat Professional または Acrobat Standard で設定されたデフォルトの「名前を付けて保存」の設定が使用されます。 例えば、PDF ファイルを EPS に変換するための Acrobat のデフォルトの「名前を付けて保存」の設定によって、PDF ファイルの 1 ページだけが EPS に変換されます。

>[!NOTE]
>
>あるファイル形式の「名前を付けて保存」の設定を変更すると、PDF Generator から書き出されるときに、その形式のすべての変換に対して、変更した設定が適用されます。

1. Acrobat で PDF ファイルを開いた状態で、ファイル／名前を付けて保存を選択します。
1. ファイルの種類リストで、該当する形式を選択します。
1. 「設定」をクリックし、必要に応じてファイル形式を設定します。
1. 「OK」をクリックし、「保存」をクリックして PDF ファイルを書き出します。
