---
title: AEM SDK を再起動するにはどうすればよいですか？
description: AEM SDK を再起動するためのベストプラクティス
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
exl-id: f5d69d04-b842-4329-b1b3-57b88266d13d
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 15%

---

# AEM SDK の再起動

Java™ プロセスを停止してAEM SDK を再起動すると、AEM開発環境で不整合が発生する場合があります。次のようなエラーが発生します。

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## 解決策

AEM SDK を再起動するには、アクティブなコマンドウィンドウに移動し、キーを押します `Ctrl + C` SDK を再起動するコマンド。

SDK を再起動するには、「Ctrl + C」コマンドを使用することをお勧めします。Java™ プロセスの停止などの別の方法を使用してAEM SDK を再起動すると、AEM開発環境で不一致が発生する場合があります。
