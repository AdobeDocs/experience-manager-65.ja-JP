---
title: リモートエンドポイントの設定
description: リモートエンドポイントの設定方法について説明します。このドキュメントでは、Flex で作成されたアプリケーションが AEM Forms Remoting を使用してサービスを呼び出せるようにする方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 100%

---

# リモートエンドポイントの設定 {#configuring-remoting-endpoints}

リモートエンドポイントを使用すると、Flex で作成されたアプリケーションから AEM Forms Remoting（AEM Forms では廃止済み）を使用してサービスを呼呼び出すことができます。リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。エンドポイントと同じ名前を持つ Flex の宛先が作成され、Flex クライアントは、関連するサービスの操作を呼び出すために、この宛先を指すリモートオブジェクトを作成できます。

## リモートエンドポイントの設定 {#remoting-endpoint-settings}

**Flex Client Authentication Method：**&#x200B;呼び出されたサービスでセキュリティが有効になっており、呼び出された操作で匿名の呼び出しがサポートされていないとき、クライアントから秘密鍵証明書が渡されないか無効な場合に、サーバーがクライアントに送り返す応答の種類を特定します。
