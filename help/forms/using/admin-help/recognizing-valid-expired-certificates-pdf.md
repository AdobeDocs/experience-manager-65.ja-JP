---
title: PDF ドキュメントでの有効な証明書と期限切れ証明書の認識
description: 証明書ドキュメントで有効な証明書と期限切れの証明書を認識するPDFを説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 8%

---

# PDF ドキュメントでの有効な証明書と期限切れ証明書の認識 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Reader拡張機能によって使用権限が適用されたPDFドキュメントがAdobe Readerで開かれると、ステータスバーが表示され、PDFドキュメントで有効になっている特定の使用権限が示されます。

PDFドキュメントの使用権限を指定した電子証明書の有効期限が切れ、PDFドキュメントがAdobe Readerで開かれると、PDFドキュメントに使用権限があることがユーザーに通知されますが、これらの権限は無効になります。 メッセージは、PDFドキュメントが変更または改ざんされたことを示しますが、必ずしもそうではありません。 Adobe Readerは、証明書の有効期限が切れたり、ドキュメントが変更されたりすると、このメッセージを表示します。 Adobe Reader 7.0.x 以降では、現在問題が発生しているケースを特定できません。

ダイアログボックスを閉じると、Adobe ReaderがPDFドキュメントを開きます。 Acrobat Reader DC拡張機能を使用して適用された使用権限は、期待どおりに使用できません。 PDFドキュメントがインタラクティブフォームの場合、フォームフィールドはロックされ、ユーザーはフォームデータを変更できません。
