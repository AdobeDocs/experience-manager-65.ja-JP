---
title: PDF Generator バックアップの制限事項
description: PDF Generator バックアップの制限事項について説明します。 設定された間隔でコンテンツを消去するので、PDF Generator が使用する一時ディレクトリをバックアップすることはできません。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
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
source-wordcount: '73'
ht-degree: 100%
---
# PDF Generator バックアップの制限事項 {#pdf-generator-backup-limitations}

PDF Generator がファイル変換に使用する一時ディレクトリをバックアップすることはできません。 PDF Generator は、設定された間隔で一時ディレクトリのコンテンツを確認および消去するので、サービスが適切に復元されたとしても、データ損失が発生する場合があります。
