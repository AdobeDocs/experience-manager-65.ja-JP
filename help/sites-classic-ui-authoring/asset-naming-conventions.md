---
title: アセットの命名規則のテスト
seo-title: アセットの命名規則
description: リポジトリのノードは、Java コンテンツリポジトリの命名規則の対象です。ただし、Adobe Experience Manager によってアセットノード名に追加の規則が課せられます。
seo-description: リポジトリのノードは、Java コンテンツリポジトリの命名規則の対象です。ただし、Adobe Experience Manager によってアセットノード名に追加の規則が課せられます。
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 98%

---

# アセットの命名規則 テスト{#naming-conventions-for-assets-testing}

リポジトリのノードは、[Java コンテンツリポジトリ](/help/sites-developing/the-basics.md#java-content-repository)の命名規則の対象です。ただし、Adobe Experience Manager によってアセットノード名に追加の規則が課せられます。

## クラシック UI {#classic-ui}

クラシック UI にはさらに厳しい制約があります。

* アセット名が有効とされるのは、明示的なノード名が次のいずれかの場合です。

   * ノード名に変換されるようにアセットタイトルが提供されている。
   * 明示的なノード名が提供されている。

* 有効な文字（アセットがクラシック UI で作成されるとき次の文字のみが有効です）：

   * a～z
   * A～Z
   * 0～9
   * _（アンダースコア）
   * `-` （ダッシュ/マイナス）
