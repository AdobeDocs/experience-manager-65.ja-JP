---
title: ドキュメントフラグメント
description: Correspondence Management では、テキスト、リスト、条件、レイアウトフラグメントなどのドキュメントフラグメントを使用して、顧客とのやり取りの静的、動的、繰り返し可能なコンポーネントを作成できます。
uuid: 053a17e5-69a5-463d-af4f-46a86534158f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 1f48548c-4222-454d-ad16-53da37170de2
feature: Correspondence Management
exl-id: ff3a4cba-a1a6-4fc9-8466-da7f28a74fb5
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 26%

---

# ドキュメントフラグメント {#document-fragments}

ドキュメントフラグメントは、インタラクティブ通信/レターを作成できる、通信の再利用可能なパーツ/コンポーネントです。 ドキュメントフラグメントは、次のいずれかの種類になります。

* **テキスト**:テキストアセットは、1 つ以上の段落で構成されるコンテンツです。 段落は静的または動的にすることができます。

   * [インタラクティブ通信内のテキスト](/help/forms/using/texts-interactive-communications.md)

* **条件**:条件を使用すると、指定されたデータに基づいて、通信の作成時に含めるコンテンツを定義できます。 条件については、制御変数で説明します。 制御変数は、データディクショナリ要素またはプレースホルダーのいずれかです。

   * [インタラクティブ通信内の条件](/help/forms/using/conditions-interactive-communications.md)

* **リスト**：リストは、テキスト、リスト、条件、画像を含む、一連のドキュメントフラグメントです。リスト要素の順序は、固定または編集可能にすることができます。 レターを作成する際に、一部またはすべてのリスト要素を使用して、再利用可能な要素のパターンを複製できます。
* **レイアウトフラグメント**:レイアウトフラグメントは、1 つ以上のレター内で使用できるレイアウトです。 レイアウトフラグメントは、繰り返し可能なパターン（特に動的テーブル）を作成するために使用します。 レイアウトには、「アドレス」や「参照番号」などの一般的なフォームフィールドを含めることができます。また、ターゲット領域を示す空のサブフォームを含めることもできます。レイアウト (XDP) は Designer で作成され、AEM Formsにアップロードされます。
