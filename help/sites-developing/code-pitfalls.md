---
title: コードの落とし穴
description: AEM向け開発時に避ける必要がある一般的なコーディングの落とし穴
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 10%

---

# コードの落とし穴{#code-pitfalls}

## Java コードでの Sling バインディングの回避 {#avoid-sling-bindings-in-java-code}

Sling バインディングは、90%のケースでサービスにアクセスするのに適していない方法です。 代わりに、 *@Reference* または *@Inject* 注釈。

## Java コードで Thread.interrupt を使用しない {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* は、呼び出しが間違った時点で Lucene ファイルや永続キャッシュファイルを含むファイルを閉じる可能性があるので、危険です。

## Java 同期と ReadWriteLocks を混在させない {#avoid-mixing-java-synchronization-with-readwritelocks}

競合状態に陥り、コードが最終的にデッドロックに陥る可能性があります。
