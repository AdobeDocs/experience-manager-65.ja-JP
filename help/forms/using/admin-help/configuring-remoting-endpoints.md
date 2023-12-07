---
title: リモートエンドポイントの設定
description: リモートエンドポイントを設定する方法を説明します。 このドキュメントでは、AEM forms Remoting を使用して、Flexで構築されたアプリケーションを有効にし、サービスを呼び出す方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 36%

---

# リモートエンドポイントの設定 {#configuring-remoting-endpoints}

リモートエンドポイントを使用すると、Flexで作成されたアプリケーションで、(AEM forms では非推奨 )AEM forms Remoting を使用してサービスを呼び出すことができます。 リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。 エンドポイントと同じ名前のFlex宛先が作成され、Flexクライアントは、この宛先を指すリモートオブジェクトを作成して、関連するサービスの操作を呼び出すことができます。

## リモートエンドポイントの設定 {#remoting-endpoint-settings}

**Flex Client Authentication Method：**&#x200B;呼び出されたサービスでセキュリティが有効になっており、呼び出された操作で匿名の呼び出しがサポートされていないとき、クライアントから秘密鍵証明書が渡されないか無効な場合に、サーバーがクライアントに送り返す応答の種類を特定します。
