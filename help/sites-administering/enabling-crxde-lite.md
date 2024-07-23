---
title: AEM での CRXDE Lite の有効化
description: Adobe Experience Manager で CRXDE Lite を有効にする方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: a3587d248569982a8f9b137602ba95dd40c47012
workflow-type: ht
source-wordcount: '261'
ht-degree: 100%

---

# AEM での CRXDE Lite の有効化 {#enabling-crxde-lite-in-aem}

AEM のインストールを可能な限り保護するために、セキュリティチェックリストでは実稼動環境で [WebDAV を無効化](/help/sites-administering/security-checklist.md#disable-webdav)することをお勧めしています。

ただし、CRXDE Lite が正しく機能するには `org.apache.sling.jcr.davex` バンドルに依存するので、WebDAV を無効にすると CRXDE Lite も無効になります。

これが発生すると、`https://serveraddress:4502/crx/de/index.jsp` にアクセスするときに空のルートノードが表示され、CRXDE Lite のリソースへのすべての HTTP リクエストが失敗します。

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

この推奨事項は攻撃対象領域を可能な限り減らすことを目的としていますが、システム管理者はコンテンツの参照や実稼動インスタンスの問題をデバッグするために CRXDE Lite にアクセスする必要がある場合があります。

[OSGi 設定](#enabling-crxde-lite-osgi)または [cURL コマンド](#enabling-crxde-lite-curl)のいずれかを使用して、CRXDE Lite を有効にできます。

>[!WARNING]
>
>これらのメソッドの動作にわずかな違いがあるので、OSGI ***または*** cURL の&#x200B;***いずれか***&#x200B;を使用する必要があります。
>
>この 2 つのメソッドには互換性が&#x200B;***ありません***。

## OSGI での CRXDE Lite の有効化 {#enabling-crxde-lite-osgi}

無効にした場合、CRXDE Lite をオンにするには次の手順を実行します。

1. OSGi コンポーネントコンソール（`http://localhost:4502/system/console/components`）に移動します。
1. 次のコンポーネントを検索します。

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. その設定オプションを確認するには、その横にあるレンチのアイコンをクリックします。

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 次の設定を作成します。

   * **ルートパス：** `/crx/server`
   * 「**絶対 URI を使用**」ボックスにチェックマークを入れます。

1. CRXDE Lite の使用が終わったら、再度 WebDAV を無効にしてください。

## cURL での CRXDE Lite の有効化 {#enabling-crxde-lite-curl}

CRXDE Lite は、次の 2 つのコマンド（両方）を実行して、cURL を使用して有効にすることもできます。

* `create-absolute-uri` を有効にする：

  ```shell
  curl -u admin:admin 'http://localhost:4502/system/console/configMgr/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet' --data-raw 'apply=true&action=ajaxConfigManager&%24location=&dav.create-absolute-uri=true&propertylist=dav.create-absolute-uri'
  ```

* `alias` を定義：

  ```shell
  curl -u admin:admin 'http://localhost:4502/system/console/configMgr/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet' --data-raw 'apply=true&action=ajaxConfigManager&%24location=&alias=/crx/server&propertylist=alias'
  ```

## その他のリソース {#other-resources}

AEM 6 のセキュリティ機能について詳しくは、次のページを参照してください。

* [AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)
* [実稼動準備モードでの AEM の実行](/help/sites-administering/production-ready.md)
