---
title: ドキュメントフラグメント
seo-title: Document Fragments
description: Correspondence Management でドキュメントフラグメント（テキスト、リスト、条件、レイアウトフラグメントなど）を使用すると、顧客対応向けに静的コンポーネント、動的コンポーネント、および繰り返し可能なコンポーネントを生成できます。
seo-description: Document Fragments, such as Text, lists, conditions, and layout fragments, in Correspondence Management let you form the static, dynamic, and repeatable components of customer correspondence.
uuid: 053a17e5-69a5-463d-af4f-46a86534158f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 1f48548c-4222-454d-ad16-53da37170de2
feature: Correspondence Management
exl-id: ff3a4cba-a1a6-4fc9-8466-da7f28a74fb5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '239'
ht-degree: 100%

---

# ドキュメントフラグメント {#document-fragments}

ドキュメントフラグメントは再利用可能な通信のパーツ／コンポーネントであり、これらを使用してインタラクティブ通信/レターを構成できます。ドキュメントフラグメントは、次のいずれかの種類になります。

* **テキスト**：テキストアセットは、1 つまたは複数の段落で構成される 1 つのコンテンツです。段落は静的または動的にすることができます。

   * [インタラクティブ通信内のテキスト](/help/forms/using/texts-interactive-communications.md)

* **条件**：条件を使用すると、提示されたデータに基づいて通信の作成時に含めるコンテンツを定義できます。制御変数を使用して条件を記述します。制御変数にはデータディクショナリ要素またはプレースホルダーがあります。

   * [インタラクティブ通信内の条件](/help/forms/using/conditions-interactive-communications.md)

* **リスト**：リストは、テキスト、リスト、条件、画像を含む、一連のドキュメントフラグメントです。リスト要素の順番は固定または編集可能にできます。レターを作成する際は、リスト要素の一部またはすべてを使用して、再利用可能な要素のパターンを複製することができます。
* **レイアウトフラグメント**：レイアウトフラグメントは、1 つ以上のレター内で使用できるレイアウトです。繰り返し可能なパターン（特に動的テーブル）を作成するには、レイアウトフラグメントを使用します。レイアウトには、「アドレス」や「参照番号」などの一般的なフォームフィールドを含めることができます。また、ターゲット領域を示す空のサブフォームを含めることもできます。レイアウト（XDP）は Designer で作成され、その後 AEM Forms にアップロードされます。
