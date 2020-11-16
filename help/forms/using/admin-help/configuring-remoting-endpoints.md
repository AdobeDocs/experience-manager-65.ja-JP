---
title: リモートエンドポイントの設定
seo-title: リモートエンドポイントの設定
description: リモートエンドポイントの設定方法について説明します。
seo-description: リモートエンドポイントの設定方法について説明します。
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 67%

---


# リモートエンドポイントの設定 {#configuring-remoting-endpoints}

リモートエンドポイントを使用すると、Flex で作成されたアプリケーションから AEM Forms Remoting（AEM Forms では廃止されています）を使用してサービスを呼び出せるようにします。リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。エンドポイントと同じ名前を持つ Flex の宛先が作成され、Flex クライアントは、関連するサービスの操作を呼び出すために、この宛先を指すリモートオブジェクトを作成できます。

## リモートエンドポイントの設定 {#remoting-endpoint-settings}

**Flexクライアント認証方法：** 呼び出されたサービスがセキュリティが有効になっている場合に、呼び出された操作で匿名呼び出しがサポートされず、クライアントがnoまたはinvalidの資格情報を渡すときに、サーバーがクライアントに返す応答の種類を決定します。
