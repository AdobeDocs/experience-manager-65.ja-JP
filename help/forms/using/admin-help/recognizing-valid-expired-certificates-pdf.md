---
title: PDF ドキュメントでの有効な証明書と期限切れ証明書の認識
seo-title: PDF ドキュメントでの有効な証明書と期限切れ証明書の認識
description: PDF ドキュメントで有効な証明書と期限切れ証明書を認識する方法について説明します。
seo-description: PDF ドキュメントで有効な証明書と期限切れ証明書を認識する方法について説明します。
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 100%

---


# PDF ドキュメントでの有効な証明書と期限切れ証明書の認識 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Reader Extensions によって使用権限が適用される PDF ドキュメントを Adobe Reader で開くと、PDF ドキュメントで有効になっている特定の使用権限についての説明がステータスバーに表示されます。

PDF ドキュメントに対する使用権限を指定する電子証明書の有効期限が切れてから、PDF ドキュメントを Adobe Reader で開くと、PDF ドキュメントには使用権限があり、その権限が無効になっていることをユーザーに伝えるダイアログボックスが表示されます。メッセージでは PDF ドキュメントが変更または改ざんされたことが通知されますが、その他にも、証明書の期限が切れるか、またはドキュメントが修正されると、Adobe Reader にこのメッセージが表示されます。Adobe Reader 7.0.x 以降では、どちらの問題が現在発生しているのかは判断できません。

ダイアログボックスを閉じると、Adobe Reader で PDF ドキュメントが開かれます。Acrobat Reader DC Extensions を使用して適用されていた使用権限は、有効期限が切れているので使用できません。PDF ドキュメントがインタラクティブフォームである場合、フォームフィールドはロックされて、フォームデータを変更することはできません。
