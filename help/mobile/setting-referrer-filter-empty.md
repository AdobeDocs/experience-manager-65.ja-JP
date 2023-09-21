---
title: リファラーフィルターの「空の値を許可」への設定
description: リファラーフィルターについて説明します。 Adobe Experience Manager(AEM)Mobile Application Viewer でオーサーインスタンス上のアプリを表示できるようにするには、HTMLリファラーフィルターを「allow empty」に設定する必要があります。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 11%

---

# リファラーフィルターの「空の値を許可」への設定{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

Adobe Experience Manager(AEM)Mobile Application Viewer でオーサーインスタンス上のアプリを表示できるようにするには、HTMLリファラーフィルターを「allow empty」に設定する必要があります。

開発状態とステージング状態のアプリケーションをアプリケーションビューアを使用して確認する場合は、リファラーフィルタのデフォルト設定を変更する必要はありません。

実行中のAEMオーサーインスタンス内で、次の場所に移動します。 [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) 「Apache Sling Referrer Filter」を検索します。 リファラーフィルターをクリックして編集し、「空の値を許可」チェックボックスをオンにします（下図を参照）。 次に、「保存」ボタンを押し、ブラウザーページを閉じます。

![リファラーフィルター設定](assets/chlimage_1-106.png)
