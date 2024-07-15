---
title: Java&trade; パッケージ名の命名規則
description: Java&trade; パッケージ名での命名規則とハイフンの使用について説明します。
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

基になるCRX プラットフォームでは、実際のアンダースコア `_ ` とハイフン `-` を区別できる必要があります。 したがって、JCR では、ハイフンを Unicode 値（u002d）に置き換え、アンダースコア `_` でエスケープする必要があります。

例えば、リポジトリーパスが **/apps/my-example/component/info/Info.java** の場合、パッケージ名は `java package apps.my_002dexample.component.info;` にする必要があります

アンダースコアも同様にエスケープする必要があるので、`_` が `_005f` になります。
