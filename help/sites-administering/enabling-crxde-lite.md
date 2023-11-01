---
title: AEM での CRXDE Lite の有効化
description: Adobe Experience ManagerでCRXDE Liteを有効にする方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 62%

---

# AEM での CRXDE Lite の有効化 {#enabling-crxde-lite-in-aem}

AEMのインストールを可能な限り安全にするために、セキュリティチェックリストでは、 [WebDAV の無効化](/help/sites-administering/security-checklist.md#disable-webdav) 実稼動環境で使用できます。

ただし、CRXDE Lite が正しく機能するには `org.apache.sling.jcr.davex` バンドルに依存するので、WebDAV を無効にすると CRXDE Lite も無効になります。

これが発生すると、`https://serveraddress:4502/crx/de/index.jsp` にアクセスするときに空のルートノードが表示され、CRXDE Lite のリソースへのすべての HTTP リクエストが失敗します。

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

この推奨事項は、攻撃対象をできるだけ減らすことを目的としていますが、CRXDE Lite管理者は、コンテンツを参照したり、実稼動インスタンスで問題をデバッグしたりするために、システムへのアクセスが必要になる場合があります。

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

1. 横のレンチアイコンをクリックして、設定オプションを表示します。

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 次の設定を作成します。

   * **ルートパス：** `/crx/server`
   * 「**絶対 URI を使用**」ボックスにチェックマークを入れます。

1. CRXDE Lite の使用が終わったら、再度 WebDAV を無効にしてください。

## cURL での CRXDE Lite の有効化 {#enabling-crxde-lite-curl}

次のコマンドを実行して、cURL 経由でCRXDE Liteを有効にすることもできます。

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## その他のリソース {#other-resources}

AEM 6 のセキュリティ機能について詳しくは、次のページを参照してください。

* [AEM セキュリティチェックリスト](/help/sites-administering/security-checklist.md)
* [実稼動準備モードでの AEM の実行](/help/sites-administering/production-ready.md)
