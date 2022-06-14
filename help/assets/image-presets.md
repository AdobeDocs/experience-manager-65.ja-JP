---
title: Dynamic Media 画像プリセットの適用
description: Dynamic Media での画像プリセットの適用方法を説明します
uuid: 8bafcbd0-6df0-4d5b-b2f7-116ddb4ec060
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5c1f60ac-3741-4002-9c5d-c128f118342b
feature: Image Presets
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
source-git-commit: 4b8369de9e6a10b73115d53358ce98729d92ed44
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 100%

---

# Dynamic Media 画像プリセットを適用する {#applying-image-presets}

画像プリセットを使用すると、アセットは異なるサイズ、異なる形式、または動的に生成された他の画像プロパティを持つ様々な画像を動的に配信できます。画像をエクスポートする際に、プリセットを選択できます。プリセットでは、管理者が指定した仕様に合わせて画像が再フォーマットされます。

さらに、レスポンシブな画像プリセットを選択することもできます（画像プリセットを選択したら「**[!UICONTROL RESS]**」ボタンを使用して指定します）。

ここでは、画像プリセットの使用方法を説明します。[画像プリセットの作成と設定は管理者が行うことができます](managing-image-presets.md)。

>[!NOTE]
>
>スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。詳しくは、[スマートイメージング](imaging-faq.md)を参照してください。

作成者は画像をプレビューするときに、いつでも画像プリセットを適用できます。

>[!NOTE]
>
>Dynamic Media - Scene7 モードでは、画像プリセットは画像アセットに対してのみサポートされます。

**Dynamic Media 画像プリセットを適用するには：**

1. アセットを開き、左パネルでドロップダウンリストを選択して、「**[!UICONTROL レンディション]**」を選択します。

   >[!NOTE]
   >
   >* 静的レンディションはウィンドウの上半分に表示されます。動的レンディションは下半分に表示されます。動的レンディションのみの場合は、URL を使用して画像を表示できます。「**[!UICONTROL URL]**」ボタンは、動的レンディションを選択した場合にのみ表示されます。「**[!UICONTROL RESS]**」ボタンは、レスポンシブ画像プリセットを選択した場合にのみ表示されます。
   >
   >* アセットの詳細表示で「**[!UICONTROL レンディション]**」を選択すると、多数のレンディションがシステムによって表示されます。表示されるプリセットの数を増やすことができます。[表示される画像プリセットの数の増加](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)を参照してください。


   ![chlimage_1-208](assets/chlimage_1-208.png)

1. 次のいずれかの操作を行います。

   * 動的レンディションを選択して、画像プリセットをプレビューできます。
   * ポップアップウィンドウを表示するには、「**[!UICONTROL URL]**」、「**[!UICONTROL 埋め込み]**」、または「**[!UICONTROL RESS]**」を選択します。

   >[!NOTE]
   >
   >アセット&#x200B;*と*&#x200B;画像プリセットがまだ公開されていない場合、「**[!UICONTROL URL]**」ボタン（または該当する場合は「**[!UICONTROL URL]**」ボタンと「**[!UICONTROL RESS]**」ボタン）は使用できません。
   >
   >また、Dynamic Media サーバーでは画像プリセットが自動的に公開されることにも注意が必要です。
