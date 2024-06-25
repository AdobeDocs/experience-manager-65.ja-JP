---
title: PDF Generator バックアップの制限事項
description: PDF Generator バックアップの制限事項について説明します。設定された間隔でコンテンツを消去するので、PDF Generator が使用する一時ディレクトリをバックアップすることはできません。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '73'
ht-degree: 100%

---

# PDF Generator バックアップの制限事項 {#pdf-generator-backup-limitations}

PDF Generator がファイル変換に使用する一時ディレクトリをバックアップすることはできません。PDF Generator は、設定された間隔で一時ディレクトリのコンテンツを確認および消去するので、サービスが適切に復元されたとしても、データ損失が発生する場合があります。
