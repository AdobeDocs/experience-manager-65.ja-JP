---
title: JEE クラスターサーバーに適用可能な破損した CRX リポジトリを復元できません
description: 破損した CRX リポジトリを復元する手順
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: c4f776b08cb8cc8c6eea78a3757735e063bec20c
workflow-type: ht
source-wordcount: '179'
ht-degree: 100%

---

# 破損した CRX リポジトリを復元できません {#unable-to-restore-corrupt-crx-repository}

## 問題 {#issue}

リレーショナルデータベースを使用する JEE 上の AEM Forms の場合、AEM Forms とリレーショナルデータベースをホストするマシンでの時間は常に絶対同期にする必要があります。 これらのマシンの時間が同期しなくなった場合、JEE 上の AEM Forms サーバーの CRX リポジトリにアクセスできなくなる可能性があります。 破損しているように見え、URL 経由でアクセスできなくなる場合があります。この `AuthenticationsupportService missing` エラーが記録されます。

## 前提条件 {#prerequisites}

以下の手順を実行する前に、CRX リポジトリのバックアップを取ります。

## 解決策 {#solution}

問題を解決するには、以下の手順を実行します。
1. `https://[AEM Forms Server]:[port]/system/console/bundles` にアクセスします。

1. `oak-core` バンドルを見つけて、実行中かどうかを確認します。

1. 実行されていない場合は、`oak-core` バンドルを再起動します。![「一時停止」ボタン](/help/forms/using/assets/stop.png)アイコンが `oak-core` バンドルの前にある場合、バンドルが実行状態であることを示しています。

1. それでも問題が解決されない場合は、バックアップの CRX リポジトリから復元するか、バックアップが使用できない場合は CRX リポジトリを再構築します。


## 適用先 {#applies-to}

このソリューションは次の場合に適用されます。

* JEE クラスター上の AEM Forms