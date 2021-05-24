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
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 29%

---

# AEM アプリケーション用の設定{#configuring-for-aem-apps}

Adobe Experience Manager Appsを使用すると、アプリケーションのコンテンツを無線(OTA)で更新できます。 更新されたコンテンツは、パブリッシュインスタンスに保存されます。デバイス上のアプリがパブリッシュインスタンスに接続して更新を確認できるようにするには、空のリファラーヘッダーを許可するようにパブリッシュインスタンスを設定する必要があります。

## 空のリファラーヘッダーの設定 {#configuring-empty-referrer-header}

リファラーフィルターサービスを設定するには：

* 次の場所にあるApache Felixコンソール(**Configurations**)を開きます。
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* admin としてログインします。
* **Configurations**&#x200B;メニューで、次の項目を選択します。*Apache Sling Referrer Filter*
* 空のリファラーヘッダーを許可するには、「 Allow Empty 」フィールドをチェックします。
* 「**保存**」をクリックして変更を保存します。

![chlimage_1-58](assets/chlimage_1-58a.png)

詳しくは、 [OSGI設定](/help/sites-deploying/osgi-configuration-settings.md)および[セキュリティチェックリスト — クロスサイトリクエストフォージェリに関する問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)を参照してください。
