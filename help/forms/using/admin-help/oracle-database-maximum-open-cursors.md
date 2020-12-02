---
title: Oracle データベースの最大オープンカーソル数のしきい値
seo-title: Oracle データベースの最大オープンカーソル数のしきい値
description: Oracle でオープンカーソルの最大値を設定する方法について説明します。
seo-description: Oracle でオープンカーソルの最大値を設定する方法について説明します。
uuid: c1d20997-f853-4772-b1c6-8cea73221d0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d3565776-1b7d-498c-9840-b17f80170d9b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 89%

---


# Oracle データベースの最大オープンカーソル数のしきい値 {#oracle-database-maximum-open-cursors-threshold}

Oracle でオープンカーソルの最大値を設定する場合、使用しているアプリケーションに適合するように数値の調整が必要になる場合があります。一般的な読み込みでは、平均的なオープンカーソル数は 2,700 なので、上限の指定を 3,000 から開始することをお勧めします。詳しくは、[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758)を参照してください。
