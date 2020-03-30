---
title: '"Correspondence Management：トラブルシューティング"'
seo-title: Correspondence Management のトラブルシューティング
description: Correspondence Management のトラブルシューティング
seo-description: Correspondence Management のトラブルシューティング
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Correspondence Management：トラブルシューティング {#correspondence-management-troubleshooting}

## レターの保存時にエラーが発生する {#errors-when-saving-a-letter}

### OS クリップボードと内部 AEM クリップボードを使用した {#issue}

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

### OS クリップボードと内部 AEM クリップボードを使用した {#issue-1}

レターをプレビューしている間、レターに含まれる未公開のテキストアセットが公開されていても、「レターの読み込み中のエラー: XML 入力からアセットを読み込めませんでした」というエラーが表示される。

### 対処方法 {#workaround-1}

次の手順を使用して公開インスタンスの文字キャッシュをリセットし、レターのプレビューを再試行します。

1. に移動し、管 **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** 理者としてログインします。
1. Select **Correspondence Management Configurations**.
1. 「**Correspondence Management の設定**」で、「**レターのキャッシュを有効にする**」を無効にして「**保存**」をクリックします。
1. Enable **Enable Letter Cache** and then click **Save**.
1. レターを再度プレビューします。

