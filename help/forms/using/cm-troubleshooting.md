---
title: 「Correspondence Management：トラブルシューティング」
description: AEM Forms環境でレターを保存する際に発生するエラーを処理する方法を説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 17%

---

# Correspondence Management：トラブルシューティング {#correspondence-management-troubleshooting}

## レターを保存する際のエラー {#errors-when-saving-a-letter}

### 問題 {#issue}

レターを保存する際に、次のエラーの 1 つが表示されます。

* テキストモジュールのデータ連結が存在しません
* 次に必要なプロパティ情報を指定します

### 理由 {#reason}

これらのエラーは、次のいずれかが原因で発生する可能性があります。

* データディクショナリはレターにバインドされていますが、サーバーに存在しません。
* データディクショナリは文字にバインドされていますが、名前にアンダースコア (_) が含まれています。

### 対処方法 {#workaround}

レターで使用しているデータディクショナリがサーバー上に存在し、名前にアンダースコア (_) が含まれていないことを確認します。

## レターをプレビュー中にエラーが発生しました {#error-when-previewing-a-letter}

### 問題 {#issue-1}

レターをプレビュー中に、レター内の非公開のテキストアセットが公開されている場合でも、「レターの読み込み中のエラー： XML 入力からアセットを読み込めませんでした」というエラーが表示されます。

### 対処方法 {#workaround-1}

次の手順を使用して発行インスタンスのレターキャッシュをリセットし、レターの表示を再試行します。

1. **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** に移動して管理者としてログインします。
1. 「**Correspondence Management の設定**」を選択します。
1. 「**Correspondence Management の設定**」で、「**レターのキャッシュを有効にする**」を無効にして「**保存**」をクリックします。
1. チェック **レターキャッシュを有効にする** 次に、「 **保存**.
1. レターの表示をもう一度やり直します。
