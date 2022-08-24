---
title: コードの落とし穴
seo-title: Code pitfalls
description: AEM の開発時に避けるべき一般的なコードの落とし穴
seo-description: Common coding pitfalls to avoid when developing for AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 100%

---

# コードの落とし穴{#code-pitfalls}

## Java コードで Sling Binding を使用しない {#avoid-sling-bindings-in-java-code}

Sling Binding はほとんどの場合、サービスにアクセスする方法として適切ではありません。代わりに、*@Reference* または *@Inject* 注釈を使用してください。

## Java コードで Thread.interrupt を使用しない {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* を不適切なタイミングで呼び出すと、Lucene ファイルや永続キャッシュファイルを含め、ファイルが閉じられることがあるので、危険です。

## Java 同期を ReadWriteLock とともに使用しない {#avoid-mixing-java-synchronization-with-readwritelocks}

競合状態が発生し、最終的にコードがデッドロックに陥ることがあります。
