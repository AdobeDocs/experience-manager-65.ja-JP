---
title: PDF Generator バックアップの制限事項
seo-title: PDF Generator backup limitations
description: PDF Generator バックアップの制限事項について説明します。
seo-description: Learn about PDF Generator backup limitations.
uuid: 9537ffde-4396-46d1-81ea-edcd25923ffb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 23386353-b2bf-49f1-947a-dd7587bba175
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '55'
ht-degree: 100%

---

# PDF Generator バックアップの制限事項 {#pdf-generator-backup-limitations}

PDF Generator がファイル変換に使用する一時ディレクトリをバックアップすることはできません。PDF Generator は、設定された間隔で一時ディレクトリのコンテンツを確認および消去するので、サービスが適切に復元されたとしても、データ損失が発生する場合があります。
