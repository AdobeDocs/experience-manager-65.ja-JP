---
title: Oracle データベースの最大オープンカーソル数のしきい値
description: Oracle でオープンカーソルの最大値を設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '82'
ht-degree: 100%

---

# Oracle データベースの最大オープンカーソル数のしきい値 {#oracle-database-maximum-open-cursors-threshold}

Oracle でオープンカーソルの最大値を設定する場合、使用しているアプリケーションに適合するように数値を調整することが必要な場合があります。一般的な読み込みでは、平均的なオープンカーソル数は 2,700 なので、上限の指定を 3,000 から開始することをお勧めします。詳しくは、[https://www.orafaq.com/node/758](https://www.orafaq.com/node/758) を参照してください。
