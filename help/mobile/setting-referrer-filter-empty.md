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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 21%

---

# リファラーフィルターの「空の値を許可」への設定{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

Adobe Experience Manager（AEM）モバイルアプリケーションビューアがオーサーインスタンス上のアプリを表示できるようにするには、HTMLリファラーフィルターを「allow empty」に設定する必要があります。

アプリケーションビューアを使用して開発状態とステージング状態のアプリケーションを確認しない場合は、リファラーフィルターのデフォルト設定を変更する必要はありません。

AEMの実行中のオーサーインスタンス内で、次の場所に移動します。 [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) Apache Sling Referrer Filter を探します。 クリックしてリファラーフィルターを編集し、「空を許可」チェックボックスをオンにします（下図を参照）。 次に「保存」ボタンをクリックして、ブラウザーページを閉じます。

![リファラーフィルターの設定](assets/chlimage_1-106.png)
