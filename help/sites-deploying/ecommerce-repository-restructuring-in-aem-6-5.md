---
title: AEM 6.5 における e コマースリポジトリの再構築
seo-title: E-Commerce Repository Restructuring in AEM 6.5
description: AEM 6.5 e コマースの新しいリポジトリ構造に移行するために必要な変更方法について説明します。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for E-Commerce.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '202'
ht-degree: 100%

---

# AEM 6.5 における e コマースリポジトリの再構築{#e-commerce-repository-restructuring-in-aem}

[AEM 6.5 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md)の親ページで説明しているように、AEM 6.5 にアップグレードする場合は、このページを参考に、AEM の e コマースソリューションに影響を及ぼすリポジトリ変更に伴う作業量を評価する必要があります。一部の変更は AEM 6.5 アップグレードプロセス中に作業が必要ですが、それ以外は今後のアップグレードまで延期できます。

## 6.5 へのアップグレード時におこなう変更 {#with-upgrade}

### 製品、注文、コレクション、分類、発送方法、支払い方法のデータ {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p><a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">遅延移行</a>タスクを使用して、e コマースデータを移行できます。</p> <p>以下の手順が実行されます。</p>
    <ul>
     <li>新しい場所を指すように古い場所の参照が変更されます。</li>
     <li>古い場所から新しい場所にコンテンツが移動されます。</li>
     <li>システム全体で最終的に新しい場所が利用されるように、古い場所が削除されます。</li>
    </ul> <p>タスクの対象となる場所は以下のとおりです。</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>大規模なカタログでは、以下の Java システムプロパティを AEM に渡して、コマース移行タスクを個別に実行することをお勧めします。</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>移行後、AEM の再起動が必要です。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>
