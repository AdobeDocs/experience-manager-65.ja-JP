---
title: 実稼動準備モードでの AEM の実行
description: 実稼動準備モードでAEMを実行する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 44%

---

# 実稼動準備モードでの AEM の実行{#running-aem-in-production-ready-mode}

AEM 6.1 では、Adobeで新しい `"nosamplecontent"` 実稼働環境でのデプロイメント用にAEMインスタンスを準備するために必要な手順の自動化を目的とした実行モード。

新しい実行モードでは、セキュリティチェックリストに記載されているセキュリティのベストプラクティスに従ってインスタンスが自動的に設定されるだけでなく、プロセス内のサンプルのGeometrixxアプリケーションと設定もすべて削除されます。

>[!NOTE]
>
>実際的な理由により、AEM実稼動準備モードでは、インスタンスの保護に必要なほとんどのタスクのみをカバーするので、 [セキュリティチェックリスト](/help/sites-administering/security-checklist.md) 実稼動環境での運用を開始する前に、以下を実行してください。
>
>また、AEM を実稼動準備モードを実行すると CRXDE Lite へのアクセスが無効になります。デバッグのためにアクセスする必要がある場合は、[AEM での CRXDE Lite の有効化](/help/sites-administering/enabling-crxde-lite.md)を参照してください。

![chlimage_1-83](assets/chlimage_1-83a.png)

実稼動準備モードでAEMを実行するには、 `nosamplecontent` 経由 `-r` 実行モードを既存の起動引数に切り替えます。

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例えば次に示すように、実稼動準備を使用して、MongoDB 永続性を備えたオーサーインスタンスを起動できます。

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 実稼動準備モードの変更点 {#changes-part-of-the-production-ready-mode}

具体的には、AEMを実稼動準備モードで実行する際に、次の設定変更が実行されます。

1. 実稼動準備モードでは、**CRXDE サポートバンドル**（`com.adobe.granite.crxde-support`）がデフォルトで無効になります。パブリック Maven リポジトリから、いつでもAdobeにインストールできます。 AEM 6.1 ではバージョン 3.0.0 が必要です。

1. **Apache Sling Simple WebDAV Access To Repositories**（`org.apache.sling.jcr.webdav`）バンドルは&#x200B;**オーサー**&#x200B;インスタンスでのみ使用できます。

1. 新しく作成したユーザーは、最初のログイン時にパスワードを変更する必要があります。 これは、管理者ユーザーには適用されません。
1. **デバッグ情報を生成** は **Apache Sling JavaScript Handler**.

1. **Apache Sling JSP Script Handler** では、「**Mapped Content**」と「**Generate Debug Info**」が無効になります。

1. **Day CQ WCM Filter** は、**オーサー**&#x200B;インスタンスでは `edit` に設定され、**パブリッシュ**&#x200B;インスタンスでは `disabled` に設定されます。

1. **Adobe Granite HTML ライブラリマネージャー**&#x200B;は次のように設定されます。

   1. **Minify：** `enabled`
   1. **デバッグ：** `disabled`
   1. **Gzip：** `enabled`
   1. **タイミング：** `disabled`

1. **Apache Sling GET Servlet** は、次に示すセキュアな設定をサポートするようにデフォルトで設定されます。

| **設定** | **作成者** | **公開** |
|---|---|---|
| TXT レンディション | 無効 | 無効 |
| HTMLレンディション | 無効 | 無効 |
| JSON レンディション | enabled | enabled |
| XML レンディション | 無効 | 無効 |
| json.maximumresults | 1000 | 100 |
| 自動インデックス | 無効 | 無効 |
