---
title: ドキュメントフラグメント
description: Correspondence Management では、テキスト、リスト、条件、レイアウトフラグメントなどのドキュメントフラグメントを使用して、顧客とのやり取りの静的、動的、繰り返し可能なコンポーネントを作成できます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: ff3a4cba-a1a6-4fc9-8466-da7f28a74fb5
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '239'
ht-degree: 100%

---

# ドキュメントフラグメント {#document-fragments}

ドキュメントフラグメントは再利用可能な通信のパーツ／コンポーネントであり、これらを使用してインタラクティブ通信／レターを構成できます。ドキュメントフラグメントは、次のいずれかの種類になります。

* **テキスト**：テキストアセットは、1 つ以上のテキストパラグラフで構成される 1 つのコンテンツです。段落は静的または動的にすることができます。

   * [インタラクティブ通信内のテキスト](/help/forms/using/texts-interactive-communications.md)

* **条件**：条件を使用すると、指定されたデータに基づいて、通信の作成時に含めるコンテンツを定義できます。条件は、制御変数で記述されます。制御変数は、データディクショナリ要素またはプレースホルダーのいずれかです。

   * [インタラクティブ通信内の条件](/help/forms/using/conditions-interactive-communications.md)

* **リスト**：リストは、テキスト、リスト、条件、画像を含む、一連のドキュメントフラグメントです。リスト要素の順序は、固定または編集可能にすることができます。レターを作成する際に、一部またはすべてのリスト要素を使用して、再利用可能な要素のパターンを複製できます。
* **レイアウトフラグメント**：レイアウトフラグメントは、1 つ以上のレター内で使用できるレイアウトです。レイアウトフラグメントは、繰り返し可能なパターン（特に動的テーブル）を作成するために使用します。レイアウトには、「アドレス」や「参照番号」などの一般的なフォームフィールドを含めることができます。また、ターゲット領域を示す空のサブフォームを含めることもできます。レイアウト（XDP）は Designer で作成され、AEM Forms にアップロードされます。
