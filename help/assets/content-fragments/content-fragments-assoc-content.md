---
title: 関連コンテンツ
description: AEM 関連のコンテンツ機能によって接続を提供する方法を理解し、フラグメントをコンテンツページに追加する際に、オプションでアセットをフラグメントと共に使用できるようにして、ヘッドレスコンテンツ配信の柔軟性を高めます。
feature: Content Fragments
role: User
exl-id: 8b93fd6e-47d1-46fd-901b-621caa25be7b
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
subfeature_v2:
  - id: b7f5d1e0-aa2f-4a55-83f4-c2b35a8bd3a7
    internal-label: Content fragments
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 100%
---
# 関連コンテンツ{#associated-content}

AEM の関連コンテンツ機能により関連性を付加して、フラグメントをコンテンツページに追加する際に、アセットを（オプションで）フラグメントと共に使用できるようになります。 これにより、[ページ上のコンテンツフラグメントを使用する際に広範なアセットにアクセスでき](/help/sites-authoring/content-fragments.md#using-associated-content)、ヘッドレスコンテンツ配信の柔軟性が向上すると共に、適切なアセットの検索に必要な時間も短縮されます。 関連するコンテンツは、コンテンツフラグメントエディターを使用して設定できます。

## 関連コンテンツの追加 {#adding-associated-content}

>[!NOTE]
>
>[ビジュアルアセット（画像など）](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)をフラグメントやページに追加するための様々な方法があります。

関連付けを行うには、最初に[メディアアセットをコレクションに追加する](/help/assets/manage-collections.md)必要があります。 それが完了した後で以下を実行できます。

1. フラグメントを開き、サイドパネルから「**関連コンテンツ**」を選択します。

   ![関連コンテンツ](assets/cfm-assoc-content-01.png)

1. コレクションが既に関連付けられているかどうかに応じて、次のいずれかを選択します。

   * **コンテンツを関連付け** - これが最初に関連付けられるコレクションになります
   * **コレクションを関連付け** - 関連付けられたコレクションが既に設定されています

1. 必要なコレクションを選択します。

   選択したコレクションにフラグメント自体をオプションで追加できます。これによりトラッキングに役立ちます。

   ![コレクションの選択](assets/cfm-assoc-content-02.png)

1. 確定します（「**選択**」を使用）。 コレクションが関連付けられて表示されます。

   ![cfm-6420-05](assets/cfm-assoc-content-03.png)

## 関連コンテンツの編集 {#editing-associated-content}

コレクションを関連付けると、次の操作を実行できます。

* 関連付けの&#x200B;**削除**
* コレクションへの&#x200B;**アセットの追加**
* 追加のアクションを実行するアセットの選択
* アセットの編集
