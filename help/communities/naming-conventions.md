---
title: Java&trade；パッケージ名の命名規則
description: Java&trade；パッケージ名での命名規則とハイフンの使用について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 1%

---

# 命名規則 {#naming-conventions}

## Java™パッケージ名のハイフン {#hyphens-in-java-package-name}

Java™クラスの場所を作成する場合、パッケージ名は、リポジトリフォルダーの場所と一致し、パス内のハイフンが適切にエスケープされている必要があります。

AEMの開発では、リポジトリ項目の名前にハイフンを使用することが推奨されますが、ハイフンは Java™パッケージ名では無効です。

基になる CRX プラットフォームは、実際のアンダースコアを区別できる必要があります `_ `とハイフン `-`. したがって、JCR では、ハイフンを Unicode 値 (u002d) に置き換え、アンダースコアでエスケープする必要があります `_`.

例えば、リポジトリのパスが **/apps/my-example/component/info/Info.java**、パッケージ名は `java package apps.my_002dexample.component.info;`

アンダースコアも同様にエスケープする必要があり、次のようにします。 `_` 次に達する `_005f`.
