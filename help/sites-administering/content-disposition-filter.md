---
title: Content Disposition フィルター
description: Content Disposition フィルターを使用して XSS 攻撃を防ぐ方法について説明します。
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 34%

---

# Content Disposition フィルター {#content-disposition-filter}

コンテンツの配置フィルターは、SVGファイルに対する XSS 攻撃に対するセキュリティ機能です。

インストールが完了すると、フィルターはすべてのアセットへのアクセスをブロックします。 例えば、オンラインで PDF を表示することができなくなります。この節では、必要に応じてフィルターを設定する方法について説明します。

## Content Disposition フィルタの設定 {#configure-content-disposition-filter}

[GitHub で Apache Sling の Content Disposition フィルター](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)を参照できます。

Content Disposition フィルターのオプションには、次の機能があります。

* **コンテンツ配置パス：** フィルターが適用されるパスのリスト。そのパスで除外する MIME タイプのリストが続きます。 このパスは絶対パスである必要があり、ワイルドカード (`*`) の末尾に置き換え、すべてのリソースパスを、指定されたパスプレフィックスと照合します。 例： `/content/*:image/jpeg,image/svg+xml` フィルターを `/content?` ただし、JPGとSVGの画像は除く。

* **除外されたリソースのパス：** 除外されたリソースのリストでは、各リソースパスに絶対パスと完全修飾パスを指定する必要があります。 プレフィックスマッチング／ワイルドカードはサポートされていません。

* **すべてのリソースパスに対して有効にする：** このフラグは、除外されたリソースパスで定義された除外されたパスを除き、すべてのパスに対してこのフィルタを有効にするかどうかを制御します。 このフラグを「true」に設定すると、コンテンツ配置パスが無視されます。 設定に関係なく、`jcr:data` または `jcr:content/jcr:data` という名前のプロパティを含むリソースパスのみが対象になります。
