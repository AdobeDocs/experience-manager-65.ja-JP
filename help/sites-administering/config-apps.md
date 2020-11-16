---
title: AEM アプリケーション用の設定
seo-title: AEM アプリケーション用の設定
description: AEM アプリケーションの設定方法について説明します。
seo-description: AEM アプリケーションの設定方法について説明します。
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 29%

---


# AEM アプリケーション用の設定{#configuring-for-aem-apps}

Adobe Experience Managerアプリでは、OTA（米国のみ）を使用してアプリのコンテンツを更新できます。 更新されたコンテンツは、発行インスタンスに保存されます。デバイス上のアプリが発行インスタンスに接続し、更新を確認するには、発行インスタンスが空の転送者ヘッダーを許可するように設定されている必要があります。

## 空のリファラーヘッダーの設定 {#configuring-empty-referrer-header}

リファラーフィルターサービスを設定するには：

* 次の場所にあるApache Felixコンソール(**設定**)を開きます。
* https://&lt;サーバー>:&lt;ポート番号>/system/console/configMgr
* admin としてログインします。
* In the **Configurations** menu, select: *Apache Sling Referrer Filter*
* 「空白を許可」フィールドをチェックして、転送者ヘッダーを空にする/見つからないようにします。
* 「**保存**」をクリックして変更を保存します。

![chlimage_1-58](assets/chlimage_1-58a.png)

See the [OSGI Configuration Settings](/help/sites-deploying/osgi-configuration-settings.md) and [Security Checklist - Issues with Cross-Site Request Forgery](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) for further details.
