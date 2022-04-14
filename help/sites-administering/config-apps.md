---
title: AEM アプリケーション用の設定
seo-title: Configuring for AEM Apps
description: AEM アプリケーションの設定方法について説明します。
seo-description: Learn how to configure AEM Apps.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '141'
ht-degree: 100%

---

# AEM アプリケーション用の設定{#configuring-for-aem-apps}

Adobe Experience Manager アプリケーションには、アプリケーションのコンテンツを OTA（Over The Air）で更新する機能が提供されています。更新されたコンテンツはパブリッシュインスタンスに格納されます。デバイス上のアプリケーションがパブリッシュインスタンスに接続して更新を確認できるようにするには、空のリファラーヘッダーを使用できるようにパブリッシュインスタンスを設定する必要があります。

## 空のリファラーヘッダーの設定 {#configuring-empty-referrer-header}

リファラーフィルターサービスを設定するには：

* Apache Felix コンソール（**設定**）を次の場所で開きます。
* https://&lt;server>:&lt;port>/system/console/configMgr
* admin としてログインします。
* **Configurations** メニューで *Apache Sling Referrer Filter* を選択します。
* 「Allow Empty」フィールドにチェックマークを入れて、空のリファラーヘッダーを使用できるようにします。
* 「**保存**」をクリックして変更を保存します。

![chlimage_1-58](assets/chlimage_1-58a.png)

詳しくは、[OSGI 設定](/help/sites-deploying/osgi-configuration-settings.md)および [セキュリティチェックリスト - クロスサイトリクエストフォージェリに関する問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)を参照してください。
