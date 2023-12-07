---
title: アセットの命名規則のテスト
description: リポジトリーのノードは、Java コンテンツリポジトリーの命名規則の対象です。ただし、アセットノード名には Adobe Experience Manager によって追加の規則が課せられます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 69%

---

# アセットの命名規則のテスト{#naming-conventions-for-assets-testing}

リポジトリーのノードは、[Java コンテンツリポジトリー](/help/sites-developing/the-basics.md#java-content-repository)の命名規則の対象です。ただし、アセットノード名には Adobe Experience Manager によって追加の規則が課せられます。

## クラシック UI {#classic-ui}

クラシック UI にはさらに厳しい制約があります。

* 次のいずれかの場合に、明示的なノード名でアセット名を検証します。

   * ノード名に変換するために、アセットのタイトルが指定されます。
   * 明示的なノード名が提供されている。

* 有効な文字（クラシック UI でアセットを作成した場合、実際には次の文字のみが有効です）:

   * a～z
   * A～Z
   * 0～9
   * _（アンダースコア）
   * `-`（ダッシュ／マイナス）
