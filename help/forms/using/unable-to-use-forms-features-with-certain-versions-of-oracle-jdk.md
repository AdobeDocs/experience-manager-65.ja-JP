---
title: 特定のバージョンの Oracle JDK で Experience Manager Forms が使用できません
description: 特定のバージョンの Oracle JDK で Experience Manager Forms が使用できません
exl-id: 6a8a7cb7-77d6-4bfc-82f3-82d0fddfc10a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 95%
---
# 特定のバージョンの Oracle JDK で Experience Manager Forms が使用できません {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

この問題は、以下のバージョンに該当します。

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## 問題 {#issue}

ユーザーに次の例外が発生しました：
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 理由 {#reason}

次のバージョン以上の Oracle JDK（Java Development Kit）で Experience Manager Forms を実行すると、例外が発生します。

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

上記およびそれ以降のバージョンの Java には、JVM（Java 仮想マシン）に新しい XML 処理制限が含まれており、特定の Forms 固有の操作が失敗します。

## 対処方法 {#workaround}

1. Experience Manager Forms サーバーを停止します。
1. アプリケーションサーバーに次の JVM 引数を設定します。

   `-Djdk.xml.xpathExprOpLimit=2000`

   デフォルトの制限に達しないように、JVM のシステム プロパティを適度に高い値に設定します。

1. Experience Manager Forms サーバーを起動します。
