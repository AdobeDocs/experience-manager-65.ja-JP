---
title: AEM SDK を再起動する方法は？
description: AEM SDK を再起動するためのベストプラクティス
role: Admin, Developer, User
feature: Adaptive Forms
source-git-commit: 5a8c0ce8c5c764bb7eeeb645527dbde6ccace497
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---


# AEM SDK の再起動

Java™プロセスを停止してAEM SDK を再起動した場合、AEM開発環境で不整合が生じる可能性があり、エラーは次のように発生します。

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## 解決策

AEM SDK を再起動するには、アクティブなコマンドウィンドウに移動して、 `Ctrl + C` コマンドを使用して SDK を再起動します。

「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。 別の方法 (Java™プロセスの停止など ) を使用してAEM SDK を再起動すると、AEM開発環境で不整合が生じる場合があります。
