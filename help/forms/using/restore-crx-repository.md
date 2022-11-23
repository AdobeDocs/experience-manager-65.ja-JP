---
title: JEE クラスターサーバーに適用可能な破損した CRX リポジトリを復元できません
description: 破損した CRX リポジトリを復元する手順
source-git-commit: a7d125503b0bd3c52cb3a959e2f0dde1a69cbe2b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 8%

---

# 破損した CRX リポジトリを復元できません {#unable-to-restore-corrupt-crx-repository}

## 問題 {#issue}

RDB 永続性を備えた JEE 上にAEM Formsをデプロイする場合は、AEM Formsのホストマシンとデータベースマシンを絶対時間同期にする必要があります。 ただし、何らかの理由でクロックが同期しなくなった場合、CRX リポジトリが破損し、その URL にアクセスできなくなります。 エラーは次のようになります。 `AuthenticationsupportService missing` はログファイルに含まれます。

## 解決策 {#solution}

問題を解決するには、以下の手順を実行します。
1. に移動します。  [https://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).

1. を `oak-core` バンドルを作成し、それが実行中かどうかを確認します。

1. を再起動します。 `oak-core` バンドル（実行されていない場合） 一時停止ボタンが `oak-core` バンドルの場合は、バンドルが実行状態であることを示します。

1. 問題が解決しない場合は、CRX リポジトリをバックアップから復元するか、バックアップが使用できない場合は CRX リポジトリを再構築します。

   >[!NOTE]
   >
   >上記の手順を実行する前に、CRX リポジトリのバックアップを取ります。

## 適用先 {#applies-to}

このソリューションは次の場合に適用されます。

* JEE 上のAEM Forms Cluster Server


