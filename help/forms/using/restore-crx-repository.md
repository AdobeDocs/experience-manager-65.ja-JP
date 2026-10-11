---
title: JEE クラスターサーバーに適用可能な破損した CRX リポジトリを復元できません
description: 破損している CRX リポジトリを復元する方法について説明します。
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 100%
---
# 破損した CRX リポジトリを復元できません {#unable-to-restore-corrupt-crx-repository}

## 問題 {#issue}

リレーショナルデータベースを使用する JEE 上の AEM Forms の場合、AEM Forms とリレーショナルデータベースをホストするマシンでの時間は常に絶対同期にする必要があります。 これらのマシンの時間が同期しなくなった場合、JEE 上の AEM Forms サーバーの CRX リポジトリにアクセスできなくなる可能性があります。 破損しているように見え、URL 経由でアクセスできなくなる場合があります。 この `AuthenticationsupportService missing` エラーが記録されます。

## 前提条件 {#prerequisites}

以下の手順を実行する前に、CRX リポジトリのバックアップを取ります。

## 解決策 {#solution}

1. `https://[AEM Forms Server]:[port]/system/console/bundles` にアクセスします。

1. `oak-core` バンドルを見つけて、実行中かどうかを確認します。

1. 実行されていない場合は、`oak-core` バンドルを再起動します。 ![「一時停止」ボタン](/help/forms/using/assets/stop.png)アイコンが `oak-core` バンドルの前にある場合、バンドルが実行状態であることを示しています。

1. それでも問題が解決されない場合は、バックアップの CRX リポジトリから復元するか、バックアップが使用できない場合は CRX リポジトリを再構築します。


## 適用先 {#applies-to}

このソリューションは、JEE 上の AEM Forms クラスターに適用されます。
