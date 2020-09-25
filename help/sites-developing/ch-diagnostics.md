---
title: ContextHub の診断
seo-title: ContextHub の診断
description: ContextHub には、ContextHub フレームワークの概要を確認できる診断ページがあります
seo-description: ContextHub には、ContextHub フレームワークの概要を確認できる診断ページがあります
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 63%

---


# ContextHub の診断 {#contexthub-diagnostics}

ContextHub には、ContextHub フレームワークの概要を確認できる診断ページがあります。To open the page, go to the `contexthub.diagnostics.html` page of your AEM author instance, for example:

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

ContextHub の診断ページには、作成されたストアおよび UI モジュール、読み込まれているクライアントライブラリフォルダー、役立つページへのリンクに関する情報が表示されます。

>[!NOTE]
>
>診断情報が返されるようにするために、デバッグモードを有効にする必要があります。そうしないと、診断ページが空白になります。デバッグモードを有効にする方法について詳しくは、[このドキュメント](ch-configuring.md#debugging-contexthub)を参照してください。

>[!NOTE]
>
>ContextHub設定が従来のパスの下に引き続き配置されている場合、診断ページの場所は `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`です。

## ストア {#stores}

ストアセクションには、設定されているすべての ContextHub ストアが一覧表示されます。リストの各項目は、次の情報で構成されます。

* **タイトル：**&#x200B;ストアのベースとなっている[ストアタイプ](/help/sites-developing/ch-samplestores.md)。
* **パス：**&#x200B;設定を保持しているリポジトリノードへのパス。
* **リソースタイプ：**&#x200B;ストアタイプが定義されているリポジトリノードのパス。
* **クライアントライブラリ：**&#x200B;読み込まれ、ストアタイプを実装するクライアントライブラリのカテゴリ。

## モジュール {#modules}

モジュールセクションには、設定されているすべての ContextHub UI モジュールが一覧表示されます。リストの各項目は、次の情報で構成されます。

* **タイトル：** UIモジュールが基にしている [UIモジュールタイプ](/help/sites-developing/ch-samplemodules.md) 。
* **パス：**&#x200B;設定を保持しているリポジトリノードへのパス。
* **リソースタイプ：** UI モジュールタイプが定義されているリポジトリノードのパス。
* **クライアントライブラリ：**&#x200B;読み込まれ、UI モジュールタイプを実装するクライアントライブラリのカテゴリ。

## Clientlibs {#clientlibs}

Clientlibs セクションには、ContextHub によって読み込まれたすべてのクライアントライブラリフォルダーが一覧表示されます。クライアントライブラリは、次のように分類されます。

* **kernel.js：** ContextHub フレームワーク、セグメントエンジン、ストアタイプを実装するクライアントライブラリ。
* **ui.js：** ContextHub UI および UI モジュールタイプを実装するクライアントライブラリ。
* **style.css：**&#x200B;クライアントライブラリから読み込まれる CSS ファイル。

## URL {#urls}

URL セクションには、次の ContextHub 機能へのリンクが含まれます。

* **設定エディター：** ストア、UIモ [ード](ch-configuring.md) 、UIモジュールを設定できるContextHub設定ページを開きます。

* **ContextHubモジュールの設定：** /etc/cloudsettings/default/contexthub.config.kernel.jsファイルを開きます。このファイルには、ContextHubストア設定のJavaScriptオブジェクト表現が含まれています。
* **ContextHub UIの設定：** /etc/cloudsettings/default/contexthub.config.ui.jsファイルを開きます。このファイルには、ContextHub UIモード設定のJavascriptオブジェクト表現が含まれています。
* **kernel.js:** /etc/cloudsettings/default/contexthub.kernel.jsファイルを開きます。このファイルには、ContextHubフレームワーク、セグメントエンジン、ストアの種類を実装するクライアントライブラリのソースコードが含まれています。
* **ui.js:** /etc/cloudsettings/default/contexthub.ui.jsファイルを開きます。このファイルには、ContextHub UIとUIモジュールタイプを実装するクライアントライブラリのソースコードが含まれています。
* **style.css:** /etc/cloudsettings/default/contexthub.styles.cssファイルを開きます。このファイルには、ContextHub UIおよびUIモジュールのCSSスタイルが含まれています。