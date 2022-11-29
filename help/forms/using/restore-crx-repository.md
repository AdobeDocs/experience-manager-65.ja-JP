---
title: JEE クラスターサーバーに適用可能な破損した CRX リポジトリを復元できません
description: 破損した CRX リポジトリを復元する手順
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: cf034e8765317ee022aad4693ced37c3fa793ff2
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 7%

---

# 破損した CRX リポジトリを復元できません {#unable-to-restore-corrupt-crx-repository}

## 問題 {#issue}

リレーショナルデータベースを使用する JEE 上のAEM Formsの場合、AEM Formsとリレーショナルデータベースをホストするマシンでの時間は常に絶対同期にする必要があります。 これらのマシンの時間が同期しなくなった場合、JEE 上のAEM Formsサーバーの CRX リポジトリにアクセスできなくなる可能性があります。 URL が破損している可能性があり、URL 経由でアクセスできなくなる場合があります。 この `AuthenticationsupportService missing` エラーが記録されます。

## 前提条件 {#prerequisites}

以下の手順を実行する前に、CRX リポジトリのバックアップを取ります。

## 解決策 {#solution}

問題を解決するには、以下の手順を実行します。
1. `https://[AEM Forms Server]:[port]/system/console/bundles` にアクセスします。

1. を `oak-core` バンドルを作成し、それが実行中かどうかを確認します。

1. を再起動します。 `oak-core` バンドル（実行されていない場合） If  ![一時停止ボタン](/help/forms/using/assets/stop.png) アイコンが `oak-core` バンドルの場合は、バンドルが実行状態にあることを示します。

1. 問題が解決されない場合は、CRX リポジトリからバックアップから復元するか、バックアップが使用できない場合は CRX リポジトリを再構築します。


## 適用先 {#applies-to}

このソリューションは次の場合に適用されます。

* JEE 上のAEM Formsクラスター環境