---
title: 特定のバージョンのOracleJDK でExperience Manager Formsを使用できません
seo-title: Unable to use Experience Manager Forms with certain versions of Oracle JDK
description: 特定のバージョンのOracleJDK でExperience Manager Formsを使用できません
seo-description: Unable to use Experience Manager Forms with certain versions of Oracle JDK
source-git-commit: 91b012f8024350effc19613bcecfc42dee4130d9
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 5%

---

# 特定のバージョンのOracleJDK でExperience Manager Formsを使用できません {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

この問題は、次のバージョンに適用されます。

* Experience Manager6.3 Forms
* Experience Manager6.4 Forms
* Experience Manager6.5 Forms

## 問題 {#issue}

ユーザーは次の例外に遭遇しました：
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 理由 {#reason}

oracleJDK(Java Development Kit) バージョンが次のバージョン以上でExperience Manager Formsを実行すると、例外が発生します。

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

上記以降のバージョンの Java には、JVM（Java 仮想マシン）での新しい XML 処理制限が含まれています。これにより、Forms固有の操作が失敗する場合があります。

## 対処方法 {#workaround}

1. Experience Manager Forms Server を停止します。
1. アプリケーションサーバーに次の JVM 引数を設定します。

   `-Djdk.xml.xpathExprOpLimit=2000`

   JVM のシステムプロパティにはある程度大きい値を設定し、デフォルトの制限がヒットされないようにします。

1. Experience Manager Forms Server を起動します。
