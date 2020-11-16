---
title: 大量の保護された情報の配布
seo-title: 大量の保護された情報の配布
description: ドキュメントを量産する環境で、Document Security はドキュメントに対してではなく、ユーザーに対するライセンスの関連付けをサポートしています。
seo-description: ドキュメントを量産する環境で、Document Security はドキュメントに対してではなく、ユーザーに対するライセンスの関連付けをサポートしています。
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 98%

---


# 大量の保護された情報の配布 {#high-volume-secure-information-delivery}

通信会社で使用される保護された月次請求書の生成など、ドキュメントを量産する環境では、ドキュメントごとに固有のライセンスを作成すると大量のリソースが消費されます。このような場合、Document Security はドキュメントに対してではなく、ユーザーに対するライセンスの関連付けをサポートしています。1 人のユーザーに対して生成されるライセンスは、そのユーザーのすべての保護されたドキュメントで使用されます。

この方法の利点の 1 つは、Document Security のデータベースのサイズが、ドキュメント数ではなくユーザー数に比例して拡大することです。また、ライセンスを作成する必要があるのは 1 人のユーザーにつき 1 回だけなので、ライセンス作成後は同じポリシーを使用してすばやくドキュメントを保護できます。オフラインアクセス、ドキュメント有効期限、失効などの機能は、この方法で保護されたドキュメントでもすべてサポートされます。

Document Security は抽象ポリシーもサポートしています。抽象ポリシーとは、ドキュメントのセキュリティ設定や使用権限などすべてのポリシー属性を含む一方、プリンシパルのリストは含まないポリシーテンプレートのことです。管理者は、抽象ポリシーから任意の数のポリシーを作成し、ドキュメントへのアクセス権を持つプリンシパルを別個に設定できます。抽象ポリシーが変更されても、その抽象ポリシーから生成された実際のポリシーは変更されません。

通信会社で使用される月次請求書の生成の場合、抽象ポリシーを作成してユーザーを作成したら、ユーザーごとに一意のライセンスを生成します。これらのライセンスは後で、各ユーザーのドキュメントに適用されます。

抽象ポリシーの作成は、Document Security Java SDK を使用した場合にのみサポートされます。ただし、抽象ポリシーから作成したポリシーは、Document Security Web ページで管理できます。この方法で作成したポリシーは、挙動に関しては Document Security Web ページで作成したものとまったく変わりません。

詳しくは、「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63)」を参照してください。
