---
title: Content Disposition フィルター
seo-title: Content Disposition フィルター
description: XSS攻撃を防ぐためのコンテンツ廃棄フィルターの使用方法を説明します。
seo-description: XSS攻撃を防ぐためのコンテンツ廃棄フィルターの使用方法を説明します。
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: cd895fcab5adce600ce230fb6867392e45963c16
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 30%

---

# Content Disposition フィルター {#content-disposition-filter}

Content Disposition フィルターは、SVG ファイルへの XSS 攻撃に対するセキュリティ機能です。

インストールが完了すると、フィルターはすべてのアセットへのアクセスをブロックします。例えば、PDFをオンラインで表示できなかった。 このセクションでは、必要に応じてフィルターを設定する方法について説明します。

## Content Disposition フィルターの設定  {#configure-content-disposition-filter}

GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)で、[Apache Sling Content Disposition Filterを表示できます。

Content Dispositionフィルターオプションには、次の機能があります。

* **Content Disposition Paths:** フィルターが適用されるパスのリストの後に、そのパスで除外するMIMEタイプのリストが続きます。このパスは絶対パスで、指定されたパスプレフィックスを持つすべてのリソースパスに一致するワイルドカード(`*`)を末尾に含める必要があります。例：`/content/*:image/jpeg,image/svg+xml`は、「/content」内のすべてのノードにフィルターを適用しますか？ jpgおよびsvg画像を除く

* **除外されたリソースパス：** 除外されたリソースのリスト。各リソースパスは絶対パスと完全修飾パスとして指定する必要があります。プレフィックスマッチング／ワイルドカードはサポートされていません。

* **Enable For All Resource Paths:** このフラグは、除外されたリソースパスで定義された除外されたパスを除き、すべてのパスに対してこのフィルターを有効にするかどうかを制御します。これを「true」に設定すると、Content Disposition パスが無視されます。設定とは無関係に、`jcr:data`または`jcr:content/jcr:data`という名前のプロパティを含むリソースパスのみが対象となります。
