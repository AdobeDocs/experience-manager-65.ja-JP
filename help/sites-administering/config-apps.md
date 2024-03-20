---
title: AEM アプリケーション用の設定
description: Adobe Experience Manager アプリケーションを使用して、アプリケーション OTA （Over The Air）のコンテンツを更新する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 100%

---

# AEM アプリケーション用の設定{#configuring-for-aem-apps}

Adobe Experience Manager アプリケーションでは、OTA（Over The Air）アプリケーションのコンテンツを更新できます。更新されたコンテンツはパブリッシュインスタンスに格納されます。デバイス上のアプリケーションがパブリッシュインスタンスに接続して更新を確認できるようにするには、空のリファラーヘッダーを使用できるようにパブリッシュインスタンスを設定する必要があります。

## 空のリファラーヘッダーの設定 {#configuring-empty-referrer-header}

リファラーフィルターサービスを設定するには：

* Apache Felix コンソール（**設定**）を次の場所で開きます。
* https://&lt;server>:&lt;port>/system/console/configMgr
* admin としてログインします。
* **Configurations** メニューで *Apache Sling Referrer Filter* を選択します。
* 「空白を許可」フィールドにチェックマークを入れて、空のリファラーヘッダーを使用できるようにします。
* 「**保存**」をクリックして変更を保存します。

![chlimage_1-58](assets/chlimage_1-58a.png)

詳しくは、[OSGI 設定](/help/sites-deploying/osgi-configuration-settings.md)および [セキュリティチェックリスト - クロスサイトリクエストフォージェリに関する問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)を参照してください。
