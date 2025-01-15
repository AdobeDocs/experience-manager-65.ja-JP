---
title: リファラーフィルターの「空の値を許可」への設定
description: リファラーフィルターの詳細。 Adobe Experience Manager（AEM）モバイルアプリケーションビューアがオーサーインスタンス上のアプリを表示できるようにするには、HTMLリファラーフィルターを「allow empty」に設定する必要があります。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 10%

---

# リファラーフィルターの「空の値を許可」への設定{#setting-your-referrer-filter-to-allow-empty}

{{ue-over-mobile}}

Adobe Experience Manager（AEM）モバイルアプリケーションビューアがオーサーインスタンス上のアプリを表示できるようにするには、HTMLリファラーフィルターを「allow empty」に設定する必要があります。

アプリケーションビューアを使用して開発状態とステージング状態のアプリケーションを確認しない場合は、リファラーフィルターのデフォルト設定を変更する必要はありません。

AEMの実行中のオーサーインスタンス内で、[http://localhost:4502/system/console/configMgrに移動して ](http://localhost:4502/system/console/configMgr)Apache Sling Referrer Filter」を検索します。 クリックしてリファラーフィルターを編集し、「空を許可」チェックボックスをオンにします（下図を参照）。 次に「保存」ボタンをクリックして、ブラウザーページを閉じます。

![ リファラーフィルターの設定 ](assets/chlimage_1-106.png)
