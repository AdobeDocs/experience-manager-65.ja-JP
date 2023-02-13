---
title: 特定のバージョンの Oracle JDK で Experience Manager Forms が使用できません
seo-title: Unable to use Experience Manager Forms with certain versions of Oracle JDK
description: 特定のバージョンの Oracle JDK で Experience Manager Forms が使用できません
seo-description: Unable to use Experience Manager Forms with certain versions of Oracle JDK
exl-id: 6a8a7cb7-77d6-4bfc-82f3-82d0fddfc10a
source-git-commit: 0142b46d087d34707b09a1f172910c8b287b839d
workflow-type: ht
source-wordcount: '177'
ht-degree: 100%

---

# 特定のバージョンの Oracle JDK で Experience Manager Forms が使用できません {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

この問題は、以下のバージョンに該当します。

* Experience Manager 6.3 Forms
* Experience Manager 6.4 Forms
* Experience Manager 6.5 Forms

## 問題 {#issue}

次の例外が発生します。
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
