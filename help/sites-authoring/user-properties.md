---
title: アカウント環境の設定
description: AEMでは、アカウントおよびオーサー環境の特定の側面を設定できます
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 6079431d-7d08-4973-8bb4-a8d10626a795
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 53%

---

# アカウント環境の設定 {#configuring-your-account-environment}

AEM では、アカウントおよびオーサー環境の特定項目を設定できます。

[ヘッダー](/help/sites-authoring/basic-handling.md#the-header)および関連する[環境設定](#userpreferences)ダイアログの「[ユーザー](/help/sites-authoring/user-properties.md#user-settings)」オプションを使用すると、ユーザーオプションを変更できます。

まず、ヘッダーの「[ユーザー](/help/sites-authoring/user-properties.md#user-settings)」オプションにアクセスします。

## ユーザー設定 {#user-settings}

The **ユーザー** 設定ダイアログでは、次の設定を実行できます。

* 次のユーザーとして操作

   * を使用 [次のユーザーとして動作](/help/sites-administering/security.md#impersonating-another-user) 機能は、ユーザーが別のユーザーに代わって作業できる機能です。

* プロファイル

   * [ユーザー設定](/help/sites-administering/security.md)への便利なリンクを提供します。

* [環境設定](/help/sites-authoring/user-properties.md#my-preferences)

   * ユーザー独自の様々な環境設定を指定します。

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### 環境設定 {#my-preferences}

**環境設定**&#x200B;ダイアログには、ヘッダーの「[ユーザー](/help/sites-authoring/user-properties.md#user-settings)」オプションを使用してアクセスできます。

各ユーザーは、自分の特定のプロパティを設定できます。

![screen-shot_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **言語**

  これにより、オーサリング環境の UI で使用する言語が定義されます。 使用可能なリストから必要な言語を選択します。

  この設定は、クラシック UI にも使用されます。

* **ウィンドウ管理**

  これにより、動作またはウィンドウを開くことが定義されます。 次のいずれかを選択します。

   * **複数のウィンドウ** （デフォルト）

      * ページが新しいウィンドウで開きます。

   * **単一ウィンドウ**

      * 現在のウィンドウでページが開きます。

* **アセットのデスクトップアクションを表示**

  このオプションを使用するには、AEMデスクトップアプリケーションが必要です。

* **注釈カラー**

  これは、注釈を作成する際に使用されるデフォルトの色を定義します。

   * カラーブロックをクリックして、スウォッチセレクターを開き、色を選択します。
   * または、フィールドに目的のカラーの 16 進コードを入力します。

* **相対的な日付の表示**

  読みやすさを向上させるために、AEMでは、過去 7 日以内の日付を相対日付（3 日前など）としてレンダリングし、古い日付を正確な日付（2017 年 3 月 20 日など）としてレンダリングします。

  このオプションは、システムの日付の表示方法を定義します。以下のオプションが利用できます。

   * **常に正確な日付を表示**：常に正確な日付が表示されます（相対日付は表示されません）。
   * **1 日**：1 日以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。

   * **7 日（デフォルト）**：7 日以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。

   * **1 ヶ月**：1 ヶ月以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。

   * **1 年**：1 年以内の日付に相対日付が表示され、それ以外は正確な日付が表示されます。

   * **常に相対日付を表示**：正確な日付は表示されず、相対日付のみが表示されます。

* **ショートカットを有効にする**

  AEMでは、オーサリングの効率を高めるいくつかのキーボードショートカットがサポートされています。

   * [ページ編集時のキーボードショートカット](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [コンソールのキーボードショートカット](/help/sites-authoring/keyboard-shortcuts.md)

  このオプションは、キーボードショートカットを有効にします。 デフォルトでは有効になっていますが、例えばユーザーに特定のアクセシビリティ要件がある場合などに、無効にすることができます。

* **従来のオーサリング機能を使用**

  このオプションは、[クラシック UI](/help/sites-classic-ui-authoring/home.md) ベースのページオーサリングを有効にします。デフォルトでは、標準 UI が使用されます。

* **アセットのホームページを有効にする**

  このオプションは、システム管理者がアセットのホームページエクスペリエンスを組織全体で有効にしている場合にのみ使用できます。

* **Stock 設定**

  このオプションを使用すると、Adobe Stockの優先設定を指定できます。この設定は、システム管理者が有効にしている場合にのみ使用できます [Adobe Stock統合](/help/assets/aem-assets-adobe-stock.md).
