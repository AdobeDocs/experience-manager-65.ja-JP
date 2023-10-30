---
title: リモートエンドポイントの設定
description: リモートエンドポイントを設定する方法を説明します。 このドキュメントでは、AEM forms Remoting を使用して、Flexで構築されたアプリケーションを有効にし、サービスを呼び出す方法について説明します。
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 36%

---

# リモートエンドポイントの設定 {#configuring-remoting-endpoints}

リモートエンドポイントを使用すると、Flexで作成されたアプリケーションで、(AEM forms では非推奨 )AEM forms Remoting を使用してサービスを呼び出すことができます。 リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。 エンドポイントと同じ名前のFlex宛先が作成され、Flexクライアントは、この宛先を指すリモートオブジェクトを作成して、関連するサービスの操作を呼び出すことができます。

## リモートエンドポイントの設定 {#remoting-endpoint-settings}

**Flex Client Authentication Method：**&#x200B;呼び出されたサービスでセキュリティが有効になっており、呼び出された操作で匿名の呼び出しがサポートされていないとき、クライアントから秘密鍵証明書が渡されないか無効な場合に、サーバーがクライアントに送り返す応答の種類を特定します。
