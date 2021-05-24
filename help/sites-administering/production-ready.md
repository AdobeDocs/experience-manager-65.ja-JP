---
title: 実稼動準備モードでの AEM の実行
seo-title: 実稼動準備モードでの AEM の実行
description: 実稼動準備モードで AEM を実行する方法について説明します。
seo-description: 実稼動準備モードで AEM を実行する方法について説明します。
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 80%

---

# 実稼動準備モードでの AEM の実行{#running-aem-in-production-ready-mode}

AEM 6.1では、Adobeは、実稼動環境でのデプロイメント用にAEMインスタンスの準備に必要な手順の自動化を目的とした新しい`"nosamplecontent"`実行モードを導入しました。

この新しい実行モードは、セキュリティチェックリストに記載されているセキュリティのベストプラクティスに従うようにインスタンスを自動的に設定するだけでなく、サンプルの Geometrixx アプリケーションと設定をプロセスですべて削除します。

>[!NOTE]
>
>実用的な理由から、AEM の実稼動準備モードはインスタンスの保護に必要な大部分のタスクにのみ対応しているので、実稼動環境で運用を開始する前に[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を確認しておくことを強くお勧めします。
>
>また、AEM を実稼動準備モードを実行すると CRXDE Lite へのアクセスが無効になります。デバッグのためにアクセスする必要がある場合は、[AEM での CRXDE Lite の有効化](/help/sites-administering/enabling-crxde-lite.md)を参照してください。

![chlimage_1-83](assets/chlimage_1-83a.png)

AEMを実稼動準備モードで実行するには、`-r`実行モードスイッチを介して`nosamplecontent`を既存の起動引数に追加するだけです。

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例えば次に示すように、実稼動準備モードを使用して、MongoDB 永続性を備えたオーサーインスタンスを起動できます。

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 実稼動準備モードによる変更点 {#changes-part-of-the-production-ready-mode}

具体的には、AEM を実稼動準備モードで実行すると、次の設定が変更されます。

1. 実稼動準備モードでは、**CRXDE サポートバンドル**（`com.adobe.granite.crxde-support`）がデフォルトで無効になります。このバンドルは、アドビの Maven 公開リポジトリからいつでもインストールできます。AEM 6.1 に必要なバージョンは 3.0.0 です。

1. **Apache Sling Simple WebDAV Access To Repositories**（`org.apache.sling.jcr.webdav`）バンドルはオーサーインスタンスでのみ使用できます。****

1. 新しく作成されたユーザーは、初回ログイン時にパスワードを変更する必要があります。これは admin ユーザーには適用されません。
1. **「Generate debug** info」は **Apache Sling Java Script Handlerでは無効になっています**。

1. **Apache Sling JSP Script Handler** では、「**Mapped Content**」と「**Generate Debug Info**」が無効になります。

1. **Day CQ WCM Filter** は、`edit`オーサー&#x200B;**インスタンスでは**   に設定され、`disabled`パブリッシュ&#x200B;**インスタンスでは** に設定されます。

1. **AdobeGranite HTML Library Manager**&#x200B;は次の設定で設定されます。

   1. **縮小：** `enabled`
   1. **デバッグ:** `disabled`
   1. **Gzip:** `enabled`
   1. **タイミング：** `disabled`

1. **Apache Sling GET Servlet** は、次に示すセキュアな設定をサポートするようにデフォルトで設定されます。

| **設定** | **作成者** | **公開** |
|---|---|---|
| TXT rendition | disabled | 無効 |
| HTML rendition | 無効 | 無効 |
| JSON rendition | enabled | 有効 |
| XML rendition | 無効 | 無効 |
| json.maximumresults | 1000 | 100 |
| Auto Index | 無効 | 無効 |
