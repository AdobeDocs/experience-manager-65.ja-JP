---
title: Java&trade; パッケージ名の命名規則
description: Java&trade; パッケージ名の命名規則とハイフンの使用について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---

# 命名規則 {#naming-conventions}

## Java™ パッケージ名のハイフン {#hyphens-in-java-package-name}

Java™ クラスの場所を作成する場合、パッケージ名は、リポジトリフォルダーの場所と一致し、適切にエスケープされたパス内のハイフンと一致する必要があります。

AEMの開発では、リポジトリ項目の名前にハイフンを使用することが推奨されますが、ハイフンは Java™ パッケージ名では無効です。

基盤の CRX プラットフォームでは、実際のアンダースコアを区別できる必要があります `_ `およびハイフン `-`. したがって、JCR では、ハイフンを Unicode 値（u002d）に置き換え、アンダースコアでエスケープする必要があります `_`.

例えば、リポジトリーパスがの場合 **/apps/my-example/component/info/Info.java**&#x200B;の場合、パッケージ名はにします `java package apps.my_002dexample.component.info;`

アンダースコアも同様に、次のようにエスケープする必要があります。 `_` になり `_005f`.
