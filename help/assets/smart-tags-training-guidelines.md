---
title: Smart Content Serviceトレーニングガイドライン
description: アセットにスマートタグを適用するように、Adobe SenseiのAIサービスをトレーニングする
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 77%

---


# Smart Content Service training guidelines {#smart-content-service-training-guidelines}

ブランド画像に効果的にタグを付けるには、スマートコンテンツサービスで、トレーニング画像が特定のガイドラインに従っている必要があります。

## トレーニングのガイドライン {#guidelines-for-training}

最適な結果を得るには、トレーニングセット内の画像は次のガイドラインに従う必要があります。

**数とサイズ**：タグ 1 つにつき 30 以上の画像が必要です。長辺が 500 ピクセル以上である必要があります。

**一貫性**：タグの各画像は、似たような外観にする必要があります。

例えば、以下の画像は似ていないので、これらの画像すべてを `my-party`（トレーニング用）としてタグ付けするのは適切ではありません。

![トレーニングガイドラインの例を示すイラスト](/help/assets/assets/do-not-localize/coherence.png)

**対象範囲**：トレーニングの画像には十分な多様性が必要です。Experience Managerが適切なものに焦点を合わせるように、いくつかの合理的に多様な例を提供することがアイデアです。 見た目が大きく異なる画像に同じタグを適用する場合は、それぞれの種類に 5 つ以上の例を含めてください。

例えば、*model-down-pose* というタグの場合、タグ付け時、類似する画像をより正確に識別できるよう、以下のハイライト表示された画像に似たトレーニング画像を増やします。

![トレーニングガイドラインの例を示すイラスト](/help/assets/assets/do-not-localize/coverage_1.png)

**妨害物と障害物**：サービスのトレーニングには、障害物（目立つ背景、メインとなる対象と一緒に含まれる物や人物などの関連性のない付随物）が少ない画像のほうが効果的です。

例えば、*casual-shoe* というタグの場合、2 つ目の画像はトレーニングの候補として適切ではありません。

![トレーニングガイドラインの例を示すイラスト](/help/assets/assets/do-not-localize/distraction.png)

**完全性**：画像が複数のタグの対象となる場合は、適用可能なすべてのタグを追加してから、画像をトレーニングに含めます。例えば、`raincoat` と `model-side-view` などのタグの場合、対象となるアセットに両方のタグを追加してから、そのアセットをトレーニングに含めます。

![トレーニングガイドラインの例を示すイラスト](/help/assets/assets/do-not-localize/completeness.png)

## 制限事項 {#limitations}

強化されたスマートタグは、画像の学習モデルとそのタグに基づいています。 これらのモデルは、タグを識別するうえで常に完璧であるわけではありません。スマートコンテンツサービスの現行バージョンには次の制限事項があります。

* 画像内の細かい違いを認識することはできません。例えば、シャツのサイズが細身か標準かなどの違いは認識できません。
* 画像の細かい模様や部分に基づいてタグを識別することはできません。例えば、T シャツのロゴなどです。
* Tagging is supported in the locales that [!DNL Experience Manager] is supported in. 言語の一覧については、](https://docs.adobe.com/content/help/ja-JP/experience-manager-64/release-notes/smart-content-service-release-notes.translate.html)スマートコンテンツサービスのリリースノート[を参照してください。

To search for assets with smart tags (regular or enhanced), use the [!DNL Assets] Omnisearch (full-text search). スマートタグには個別の検索用述語はありません。

>[!NOTE]
>
>スマートコンテンツサービスでタグのトレーニングを実施し、それらのタグを他の画像に適用できるかどうかは、トレーニングで使用する画像の質によって決まります。最適な結果を得るには、視覚的に似ている画像を使用し、それぞれのタグについてサービスのトレーニングを実施することをお勧めします。
