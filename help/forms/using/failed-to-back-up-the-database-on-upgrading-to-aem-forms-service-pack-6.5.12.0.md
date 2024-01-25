---
title: AEM Forms 6.5.12.0で以前のデータベースをバックアップできませんでした。
description: ユーザーがExperience Manager6.5.12.0にアップグレードして「MySQL をアップグレード」をクリックすると、Configuration Manager は以前のExperience Manager Formsデータベースのバックアップに失敗します。
source-git-commit: d232bfdad7b8413eb015f6fe5dd3442cebf1001d
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 7%

---

# 問題 (#issue)

ユーザーがExperience Manager6.5.12.0にアップグレードして「Upgrade MySQL」をクリックすると、Configuration Manager が以前のExperience Manager Formsデータベースのバックアップに失敗し、次のエラーが表示されます。

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 適用先 {#applies-to}

* Experience Manager 6.5 Forms

## 解決策 {#solution}

この問題を解決するには、データベースの max_packet_size を 100 M に増やすか、必要に応じて次の場所にある my.ini ファイルで増やします。 {AEM_HOME}/mysql.
