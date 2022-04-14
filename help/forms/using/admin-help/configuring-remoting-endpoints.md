---
title: リモートエンドポイントの設定
seo-title: Configuring Remoting endpoints
description: リモートエンドポイントの設定方法について説明します。
seo-description: Learn how to configure remoting endpoints.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '120'
ht-degree: 100%

---

# リモートエンドポイントの設定 {#configuring-remoting-endpoints}

リモートエンドポイントを使用すると、Flex で作成されたアプリケーションから AEM Forms Remoting（AEM Forms では廃止されています）を使用してサービスを呼び出せるようにします。リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。エンドポイントと同じ名前を持つ Flex の宛先が作成され、Flex クライアントは、関連するサービスの操作を呼び出すために、この宛先を指すリモートオブジェクトを作成できます。

## リモートエンドポイントの設定 {#remoting-endpoint-settings}

**Flex Client Authentication Method：**&#x200B;呼び出されたサービスでセキュリティが有効になっており、呼び出された操作で匿名の呼び出しがサポートされていないとき、クライアントから秘密鍵証明書が渡されないか無効な場合に、サーバーがクライアントに送り返す応答の種類を特定します。
