---
title: 大量の保護された情報の配布
description: ドキュメントを量産する環境で、Document Security はドキュメントに対してではなく、ユーザーに対するライセンスの関連付けをサポートしています。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '320'
ht-degree: 100%

---

# 大量の保護された情報の配布 {#high-volume-secure-information-delivery}

通信会社で保護された月次請求書を生成する場合など、ドキュメントを量産する環境では、ドキュメントごとに固有のライセンスを作成すると大量のリソースが消費されます。このような場合、Document Security はドキュメントに対してではなく、ユーザーに対するライセンスの関連付けをサポートしています。1 人のユーザーに対して生成されるライセンスは、そのユーザーに対して保護されているすべてのドキュメントで使用されます。

この方法の利点の 1 つは、Document Security のデータベースのサイズが、ドキュメント数ではなくユーザー数に比例して増加することです。また、ライセンスを作成する必要があるのは 1 人のユーザーにつき 1 回だけなので、ライセンス作成後は同じポリシーを使用してすばやくドキュメントを保護できます。オフラインアクセス、ドキュメント有効期限、失効などの機能は、この方法で保護されたすべてのドキュメントでもサポートされています。

Document Security は抽象ポリシーもサポートしています。抽象ポリシーとは、ドキュメントのセキュリティ設定や使用権限などのすべてのポリシー属性を含む一方で、プリンシパルのリストは含まないポリシーテンプレートのことです。管理者は、抽象ポリシーから任意の数のポリシーを作成し、ドキュメントへのアクセス権をプリンシパルごとに個別に設定できます。抽象ポリシーが変更されても、その抽象ポリシーから生成された実際のポリシーは変更されません。

通信会社で月次請求書を生成する場合などには、抽象ポリシーを作成してユーザーを作成し、ユーザーごとに一意のライセンスを生成します。これらのライセンスは後で、各ユーザーのドキュメントに適用されます。

抽象ポリシーの作成は、Document Security Java SDK を使用した場合にのみサポートされます。ただし、抽象ポリシーから作成したポリシーは、Document Security web ページで管理できます。この方法で作成したポリシーの挙動に関しては、Document Security web ページで作成したポリシーと同じです。

詳しくは、「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp)」を参照してください。
