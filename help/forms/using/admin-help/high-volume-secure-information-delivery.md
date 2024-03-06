---
title: 大量の保護された情報の配布
description: Document Security は、大量実稼動環境のドキュメントに対してではなく、ユーザーに対するライセンスの関連付けをサポートします。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 5%

---

# 大量の保護された情報の配布 {#high-volume-secure-information-delivery}

通信会社の安全な月次請求書を生成するような大量生産環境では、各ドキュメントに固有のライセンスを作成すると、リソースを大量に消費する可能性があります。 このような場合、Document Security は、ドキュメントに対するライセンスの関連付けではなく、ユーザーに対するライセンスの関連付けをサポートします。 ユーザーに対して生成されたライセンスは、そのユーザーに対して保護されているすべてのドキュメントに対して使用されます。

このアプローチの利点の 1 つは、Document Security データベースのサイズが、ユーザー数ではなく、ドキュメント数に比例して大きくなるという点です。 また、1 人のユーザーに対して 1 回だけライセンスを作成する必要があるので、以降、これらのポリシーを使用してドキュメントを保護する方が速くなります。 オフラインアクセス、ドキュメントの有効期限、失効などの機能は、そのようなすべてのドキュメントでサポートされます。

Document Security は抽象ポリシーもサポートしています。 抽象ポリシーは、ドキュメントセキュリティ設定や使用権限などのすべてのポリシー属性を含むポリシーテンプレートですが、プリンシパルのリストは含まれていません。 管理者は、ドキュメントへのアクセス権を持つ別のプリンシパルを持つ抽象ポリシーから任意の数のポリシーを作成できます。 抽象ポリシーに対して行った変更は、抽象ポリシーから生成された実際のポリシーには影響しません。

通信会社の請求書の月次生成がある場合は、抽象ポリシーを作成し、ユーザーを作成してから、各ユーザーに対して一意のライセンスを生成します。 ライセンスは、後で各ユーザーのドキュメントに適用されます。

抽象ポリシーの作成は、Document Security Java SDK を通じてのみサポートされます。 ただし、Document Security Web ページから抽象ポリシーから作成したポリシーを管理することはできます。 この方法を使用して作成されるポリシーは、動作が Document Security Web ページから作成されるポリシーと同じです。

詳しくは、「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp)」を参照してください。
