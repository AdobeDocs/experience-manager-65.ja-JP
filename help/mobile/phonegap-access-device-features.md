---
title: デバイス機能へのアクセス
description: デバイスの機能にアクセスするAdobe Experience Manager（AEM）コンポーネントの構築について説明します。 AEM PhoneGap Kitchen シンク GitHub リポジトリは、いくつかのコア Cordova API の使用方法を説明する機能的なAEM アプリを開発者に提供します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 385f7924-e8ab-4dcb-83f0-7b81bead3dda
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 18%

---

# デバイス機能へのアクセス{#access-device-features}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

## デバイス機能にアクセスするAdobe Experience Manager（AEM）コンポーネントの構築 {#building-aem-components-that-access-device-features}

この [AEM PhoneGap キッチン シンク](https://github.com/blefebvre/aem-phonegap-kitchen-sink) GitHub リポジトリは、複数のコア Cordova API の使用方法を説明する機能的なAEM アプリを開発者に提供します。 PhoneGap CLI を使用してiOSまたは Android™ で実行すると、アプリが次のページに開き、アプリで示される各デバイス API へのリンクが含まれます。

![chlimage_1-107](assets/chlimage_1-107.png)

これらの各デバイス API コンポーネントのソースコードは次のとおりです [github で入手可能](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/apps/brucelefebvre/kitchen-sink/components).

各 API の使用方法について詳しくは、Cordova プラグインのドキュメント （`https://docs.phonegap.com/en/4.0.0/cordova_plugins_pluginapis.md.html`）に設定します。

## 次の手順 {#the-next-steps}

参照： [Adobeモバイル分析を使用したアプリパフォーマンスの追跡](/help/mobile/phonegap-intro-to-app-analytics.md).
