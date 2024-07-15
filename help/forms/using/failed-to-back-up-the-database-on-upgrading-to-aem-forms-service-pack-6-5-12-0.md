---
title: MySQL 用に 6.5.12.0 にアップグレードする際にデータベースをバックアップできない問題。
description: ユーザーが Experience Manager 6.5.12.0 にアップグレードして「MySQL をアップグレード」をクリックすると、Configuration Manager が以前の Experience Manager Forms データベースをバックアップできません。
exl-id: 1af000fa-439b-4ffd-8b5a-3ba45f0c524c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 100%

---

# MySQL 用に 6.5.12.0 にアップグレードする際にデータベースをバックアップできない問題 {#issue}

ユーザーが Experience Manager 6.5.12.0 にアップグレードして「Upgrade MySQL」をクリックすると、Configuration Manager が以前の Experience Manager Forms データベースをバックアップできず、次のエラーが表示されます。

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 適用先 {#applies-to}

* Experience Manager 6.5 Forms

## 解決策 {#solution}

この問題を解決するには、{AEM_HOME}/mysql にある my.ini ファイルで、データベースの max_packet_size を 100 M に、または必要に応じて増やします。
