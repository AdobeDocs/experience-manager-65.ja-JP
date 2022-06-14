---
title: 「Correspondence Management：トラブルシューティング」
seo-title: Correspondence Management Troubleshooting
description: Correspondence Management のトラブルシューティング
seo-description: Correspondence Management Troubleshooting
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 100%

---

# Correspondence Management：トラブルシューティング {#correspondence-management-troubleshooting}

## レターの保存時にエラーが発生する {#errors-when-saving-a-letter}

### 問題 {#issue}

レターの保存時に、次のいずれかのエラーが表示される：

* テキストモジュールにデータバインディングが存在しない
* 次の項目に必要なプロパティ情報を指定してください

### 理由 {#reason}

このエラーは次のいずれかの理由で発生します。

* データディクショナリは文字にバインドされているが、サーバー上には存在していない。
* データディクショナリは文字にバインドされているが、名前にアンダースコア（_）が含まれている。

### 対処方法 {#workaround}

レターで使用しているデータディクショナリーがサーバー上に存在しており、名前にアンダースコア（_）が含まれていないことを確認してください。

## レターのプレビュー時にエラーが発生する {#error-when-previewing-a-letter}

### 問題 {#issue-1}

レターをプレビューしている間、レターに含まれる未公開のテキストアセットが公開されていても、「レターの読み込み中のエラー: XML 入力からアセットを読み込めませんでした」というエラーが表示される。

### 対処方法 {#workaround-1}

次の手順を使用して公開インスタンスの文字キャッシュをリセットし、レターのプレビューを再試行します。

1. **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** に移動して管理者としてログインします。
1. 「**Correspondence Management の設定**」を選択します。
1. 「**Correspondence Management の設定**」で、「**レターのキャッシュを有効にする**」を無効にして「**保存**」をクリックします。
1. 「**レターのキャッシュを有効にする**」を無効にし、「**保存**」をクリックします。
1. レターの表示をもう一度やり直します。
