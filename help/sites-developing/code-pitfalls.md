---
title: コードの落とし穴
description: AEM の開発時に避けるべき一般的なコードの落とし穴
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 100%

---

# コードの落とし穴{#code-pitfalls}

## Java コードで Sling Binding を使用しない {#avoid-sling-bindings-in-java-code}

Sling Binding はほとんどの場合、サービスにアクセスする方法として適切ではありません。代わりに、*@Reference* または *@Inject* 注釈を使用してください。

## Java コードで Thread.interrupt を使用しない {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* を不適切なタイミングで呼び出すと、Lucene ファイルや永続キャッシュファイルなどのファイルが閉じられる可能性があるので危険です。

## Java 同期を ReadWriteLock と共に使用しない {#avoid-mixing-java-synchronization-with-readwritelocks}

競合状態が発生し、最終的にコードのデッドロックが発生することがあります。
