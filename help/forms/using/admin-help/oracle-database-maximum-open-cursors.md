---
title: Oracle データベースの最大オープンカーソル数のしきい値
description: 「Oracle」でオープンカーソルの最大値を設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 23%

---

# Oracle データベースの最大オープンカーソル数のしきい値 {#oracle-database-maximum-open-cursors-threshold}

oracleのオープンカーソルの最大値を設定するには、アプリケーションに適した数値にこの値を調整する必要がある場合があります。 中程度の負荷では、開いている平均カーソル数は 2700 であることが明らかです。 上限は 3000 にすることをお勧めします。 詳しくは、[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758) を参照してください。
