---
title: AEM アプリケーション用の設定
description: Adobe Experience Manager Apps を使用して、アプリケーション OTA のコンテンツを（空中で）更新する方法を学びます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 41%

---

# AEM アプリケーション用の設定{#configuring-for-aem-apps}

Adobe Experience Managerアプリでは、OTA（無線）アプリケーションのコンテンツを更新できます。 更新されたコンテンツは、パブリッシュインスタンスに保存されます。 デバイス上のアプリがパブリッシュインスタンスに接続して更新を確認できるようにするには、パブリッシュインスタンスが空のリファラーヘッダーを許可するように設定されている必要があります。

## 空のリファラーヘッダーの設定 {#configuring-empty-referrer-header}

リファラーフィルターサービスを設定するには：

* Apache Felix コンソール（**設定**）を次の場所で開きます。
* https://&lt;server>:&lt;port>/system/console/configMgr
* admin としてログインします。
* **Configurations** メニューで *Apache Sling Referrer Filter* を選択します。
* 「Allow Empty」フィールドをチェックして、空のリファラーヘッダーや見つからないリファラーヘッダーを許可します。
* 「**保存**」をクリックして変更を保存します。

![chlimage_1-58](assets/chlimage_1-58a.png)

詳しくは、[OSGI 設定](/help/sites-deploying/osgi-configuration-settings.md)および [セキュリティチェックリスト - クロスサイトリクエストフォージェリに関する問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)を参照してください。
