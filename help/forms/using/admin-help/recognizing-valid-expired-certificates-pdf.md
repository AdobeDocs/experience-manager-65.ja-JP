---
title: PDF ドキュメントでの有効な証明書と期限切れ証明書の認識
description: PDF ドキュメントでの有効な証明書と期限切れ証明書の認識方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 100%
---
# PDF ドキュメントでの有効な証明書と期限切れ証明書の認識 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Reader Extensions によって使用権限が適用される PDF ドキュメントを Adobe Reader で開くと、PDF ドキュメントで有効になっている特定の使用権限についての説明がステータスバーに表示されます。

PDF ドキュメントに対する使用権限を指定する電子証明書の有効期限が切れてから、PDF ドキュメントを Adobe Reader で開くと、PDF ドキュメントには使用権限があり、その権限が無効になっていることをユーザーに伝えるダイアログボックスが表示されます。 メッセージでは PDF ドキュメントが変更または改ざんされたことが通知されますが、必ずしもそうであるとは限りません。 証明書の期限が切れるか、またはドキュメントが修正されると、Adobe Reader にこのメッセージが表示されます。 Adobe Reader 7.0.x 以降では、どちらの問題が現在発生しているのかは判断できません。

ダイアログボックスを閉じると、Adobe Reader で PDF ドキュメントが開かれます。 Acrobat Reader DC Extensions を使用して適用された使用権限は、予想どおり使用できません。 PDF ドキュメントがインタラクティブフォームである場合、フォームフィールドはロックされて、フォームデータを変更できません。
