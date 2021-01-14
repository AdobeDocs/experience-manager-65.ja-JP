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
translation-type: tm+mt
source-git-commit: 741ba6f6ef3270414c0ddabb1a1d02d5c436b7d9
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 45%

---


# Content Disposition フィルター{#content-disposition-filter}

Content Disposition フィルターは、SVG ファイルへの XSS 攻撃に対するセキュリティ機能です。

インストールが完了すると、フィルターはすべてのアセットへのアクセスをブロックします。例えば、PDFをオンラインで表示できなかった。 このセクションでは、必要に応じてフィルターを設定する方法について説明します。

## Content Disposition フィルターの設定  {#configure-content-disposition-filter}

GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)の[Apache Sling Content Disposition Filterを表示できます。

コンテンツ廃棄フィルターのオプションには、次の機能があります。

* コンテンツ廃棄パス：フィルターが適用されるパスのリスト。そのパスで除外するMIME型のリストが続きます。このパスは絶対パスである必要があり、末尾にワイルドカード(&#39;&amp;ast;&#39;)を含めることができます。 次に例を示します。/content/&amp;ast;:image/jpeg,image/svg+xml &quot;は、/content内のjpgおよびsvg画像を除くすべてのノードにフィルターを適用します

* 除外されたリソースパス：除外されたリソースのリストです。各リソースパスは絶対パスおよび完全修飾パスとして指定する必要があります。プレフィックスマッチング／ワイルドカードはサポートされていません。

* すべてのリソースパスを有効化：このフラグは、除外されたリソースパスで定義されたパス以外のすべてのパスに対して、このフィルターを有効にするかどうかを制御します。これを「true」に設定すると、Content Disposition パスが無視されます。設定とは無関係に、「jcr:data」または「jcr:content jcr:data」という名前のプロパティを含むリソースパスのみが対象となります。

