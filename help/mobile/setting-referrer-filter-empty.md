---
title: リファラーフィルターの「空の値を許可」への設定
description: リファラーフィルターについて詳しく見る。 Adobe Experience Manager（AEM）モバイルアプリケーションビューアでオーサーインスタンス上のアプリケーションを表示できるようにするには、HTML リファラーフィルターを「空を許可」に設定する必要があります。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
solution: Experience Manager
feature: Mobile
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 12%
---
# リファラーフィルターの「空の値を許可」への設定{#setting-your-referrer-filter-to-allow-empty}

{{ue-over-mobile}}

Adobe Experience Manager（AEM）モバイルアプリケーションビューアでオーサーインスタンス上のアプリケーションを表示できるようにするには、HTML リファラーフィルターを「空を許可」に設定する必要があります。

アプリケーションビューアを使用して開発状態およびステージング状態のアプリケーションをレビューしない場合は、リファラーフィルターのデフォルト設定を変更する必要はありません。

実行中のAEMのオーサーインスタンス内で、[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)に移動し、「Apache Sling Referrer Filter」を検索します。 クリックしてリファラーフィルターを編集し、「空を許可」チェックボックスをオンにします（下の画像を参照）。 次に保存ボタンを押してブラウザーページを閉じます。

![&#x200B; リファラーフィルター設定](assets/chlimage_1-106.png)
