---
title: リファラーフィルターの「空の値を許可」への設定
seo-title: リファラーフィルターを「空の値を許可」に設定
description: このページでは、リファラーフィルターについて説明します。AEM Mobile アプリケーションビューアで AEM オーサーインスタンス上のアプリを表示できるようにするには、HTML リファラーフィルターが「空の値を許可」に設定する必要があります。
seo-description: このページでは、リファラーフィルターについて説明します。AEM Mobile アプリケーションビューアで AEM オーサーインスタンス上のアプリを表示できるようにするには、HTML リファラーフィルターが「空の値を許可」に設定する必要があります。
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 90%

---

# リファラーフィルターを「空の値を許可」に設定{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

AEM Mobile アプリケーションビューアで AEM オーサーインスタンス上のアプリを表示できるようにするには、HTML リファラーフィルターが「空の値を許可」に設定する必要があります。

開発中およびステージング中のアプリケーションをアプリケーションビューアでレビューしない場合は、リファラーフィルターのデフォルト設定を変更する必要はありません。

実行中のAEMオーサーインスタンス内で、次の場所に移動します。[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)を検索し、「Apache Sling Referrer Filter」を検索します。 リファラーフィルターをクリックして編集し、「空の値を許可」チェックボックスをオンにします（下図を参照）。次に、「保存」ボタンをクリックして、ブラウザーページを閉じます。

![リファラーフィルターの設定](assets/chlimage_1-106.png)
