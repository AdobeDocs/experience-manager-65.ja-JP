---
title: MySQL の 6.5.12.0へのアップグレード中にデータベースのバックアップに失敗しました。
description: ユーザーがExperience Manager6.5.12.0にアップグレードして「MySQL をアップグレード」をクリックすると、Configuration Manager は以前のExperience Manager Formsデータベースのバックアップに失敗します。
source-git-commit: a6b1e97fd694f0fa1396697c42d84daaa9a6ac68
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 6%

---

# MySQL 用に 6.5.12.0にアップグレード中にデータベースをバックアップできなかった問題 {#issue}

ユーザーがExperience Manager6.5.12.0にアップグレードして「Upgrade MySQL」をクリックすると、Configuration Manager が以前のExperience Manager Formsデータベースのバックアップに失敗し、次のエラーが表示されます。

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 適用先 {#applies-to}

* Experience Manager 6.5 Forms

## 解決策 {#solution}

この問題を解決するには、データベースの max_packet_size を 100 M に増やすか、必要に応じて次の場所にある my.ini ファイルで増やします。 {AEM_HOME}/mysql.
