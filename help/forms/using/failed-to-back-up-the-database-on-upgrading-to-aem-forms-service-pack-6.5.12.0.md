---
title: MySQL の 6.5.12.0へのアップグレード中にデータベースのバックアップに失敗しました。
description: ユーザーがExperience Manager6.5.12.0にアップグレードして「MySQL をアップグレード」をクリックすると、Configuration Manager は以前のExperience Manager Formsデータベースのバックアップに失敗します。
source-git-commit: bf974331157e21b28c0daa5b878ac927ce5a2304
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 6%

---

# MySQL の 6.5.12.0へのアップグレード中にデータベースをバックアップできない (#issue)

ユーザーがExperience Manager6.5.12.0にアップグレードして「Upgrade MySQL」をクリックすると、Configuration Manager が以前のExperience Manager Formsデータベースのバックアップに失敗し、次のエラーが表示されます。

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 適用先 {#applies-to}

* Experience Manager 6.5 Forms

## 解決策 {#solution}

この問題を解決するには、データベースの max_packet_size を 100 M に増やすか、必要に応じて次の場所にある my.ini ファイルで増やします。 {AEM_HOME}/mysql.
