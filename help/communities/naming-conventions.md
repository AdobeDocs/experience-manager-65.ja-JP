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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%
---
# 命名規則 {#naming-conventions}

## Java™ パッケージ名のハイフン {#hyphens-in-java-package-name}

Java™ クラスの場所を作成する場合、パッケージ名はリポジトリーフォルダーの場所とパス内のハイフンが適切にエスケープされた場所と一致する必要があります。

リポジトリ項目の名前にハイフンを使用することは、AEM開発では推奨される方法ですが、Java™ パッケージ名ではハイフンは違法です。

基になるCRX プラットフォームは、実際のアンダースコア `_ `とハイフン `-`を区別できる必要があります。 したがって、JCRでは、ハイフンをUnicode値（u002d）に置き換え、アンダースコア `_`でエスケープする必要があります。

例えば、リポジトリパスが&#x200B;**/apps/my-example/component/info/Info.java**&#x200B;の場合、パッケージ名は`java package apps.my_002dexample.component.info;`である必要があります

アンダースコアも同様にエスケープする必要があります。例えば、`_`が`_005f`になります。
