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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 100%
---
# 大量の保護された情報の配布 {#high-volume-secure-information-delivery}

通信会社で保護された月次請求書を生成する場合など、ドキュメントを量産する環境では、ドキュメントごとに固有のライセンスを作成すると大量のリソースが消費されます。 このような場合、Document Security はドキュメントに対してではなく、ユーザーに対するライセンスの関連付けをサポートしています。 1 人のユーザーに対して生成されるライセンスは、そのユーザーに対して保護されているすべてのドキュメントで使用されます。

この方法の利点の 1 つは、Document Security のデータベースのサイズが、ドキュメント数ではなくユーザー数に比例して増加することです。 また、ライセンスを作成する必要があるのは 1 人のユーザーにつき 1 回だけなので、ライセンス作成後は同じポリシーを使用してすばやくドキュメントを保護できます。 オフラインアクセス、ドキュメント有効期限、失効などの機能は、この方法で保護されたすべてのドキュメントでもサポートされています。

Document Security は抽象ポリシーもサポートしています。 抽象ポリシーとは、ドキュメントのセキュリティ設定や使用権限などのすべてのポリシー属性を含む一方で、プリンシパルのリストは含まないポリシーテンプレートのことです。 管理者は、抽象ポリシーから任意の数のポリシーを作成し、ドキュメントへのアクセス権をプリンシパルごとに個別に設定できます。 抽象ポリシーが変更されても、その抽象ポリシーから生成された実際のポリシーは変更されません。

通信会社で月次請求書を生成する場合などには、抽象ポリシーを作成してユーザーを作成し、ユーザーごとに一意のライセンスを生成します。 これらのライセンスは後で、各ユーザーのドキュメントに適用されます。

抽象ポリシーの作成は、Document Security Java SDK を使用した場合にのみサポートされます。 ただし、抽象ポリシーから作成したポリシーは、Document Security web ページで管理できます。 この方法で作成したポリシーの挙動に関しては、Document Security web ページで作成したポリシーと同じです。

詳しくは、「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp)」を参照してください。
