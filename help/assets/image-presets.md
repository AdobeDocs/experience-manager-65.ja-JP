---
title: Dynamic Media 画像プリセットの適用
description: アセットが異なるサイズ、異なる形式、または動的に生成された他の画像プロパティを使用して、画像を動的に配信できるようにする方法について説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Image Presets
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: d4b6216b-4a89-4ff0-8ac0-5a699ba23100
    internal-label: Images and videos
subfeature_v2:
  - id: a16e03b7-8456-4383-8860-31ab5ab00e9e
    internal-label: Image presets
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 100%
---
# Dynamic Media 画像プリセットの適用 {#applying-image-presets}

画像プリセットを使用すると、アセットは異なるサイズ、異なる形式、または動的に生成された他の画像プロパティで、画像を動的に配信できます。 画像を書き出す際に、プリセットを選択できます。 プリセットでは、管理者が指定した仕様に合わせて画像が再フォーマットされます。

さらに、レスポンシブな画像プリセットを選択することもできます（画像プリセットを選択したら「**[!UICONTROL RESS]**」ボタンを使用して指定します）。

この節では、画像プリセットの使用方法を説明します。 [画像プリセットの作成と設定は管理者が行うことができます](managing-image-presets.md)。

>[!NOTE]
>
>スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。 詳しくは、[スマートイメージング](imaging-faq.md)を参照してください。

作成者は画像をプレビューするときに、いつでも画像プリセットを適用できます。

>[!NOTE]
>
>Dynamic Media - Scene7 モードでは、画像プリセットは画像アセットに対してのみサポートされます。

**Dynamic Media 画像プリセットを適用するには：**

1. アセットを開き、左パネルでドロップダウンリストを選択して、「**[!UICONTROL レンディション]**」を選択します。

   >[!NOTE]
   >
   >* 静的レンディションはウィンドウの上半分に表示されます。 動的レンディションは下半分に表示されます。 動的レンディションのみの場合は、URL を使用して画像を表示できます。 「**[!UICONTROL URL]**」ボタンは、動的レンディションを選択した場合にのみ表示されます。 「**[!UICONTROL RESS]**」ボタンは、レスポンシブ画像プリセットを選択した場合にのみ表示されます。
   >
   >* アセットの詳細表示で「**[!UICONTROL レンディション]**」を選択すると、多数のレンディションがシステムによって表示されます。 表示されるプリセットの数を増やすことができます。 [表示される画像プリセットの数の増加](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)を参照してください。

   ![chlimage_1-208](assets/chlimage_1-208.png)

1. 次のいずれかの操作を行います。

   * 動的レンディションを選択して、画像プリセットをプレビューできます。
   * ポップアップウィンドウを表示するには、「**[!UICONTROL URL]**」、「**[!UICONTROL 埋め込み]**」、または「**[!UICONTROL RESS]**」を選択します。

   >[!NOTE]
   >
   >アセット&#x200B;*と*&#x200B;画像プリセットがまだ公開されていない場合、「**[!UICONTROL URL]**」ボタン（または該当する場合は「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL RESS]**」ボタン）は使用できません。
   >
   >また、Dynamic Media サーバーでは画像プリセットが自動的に公開されることにも注意が必要です。
