---
title: HTML5 フォームの概要
seo-title: Introduction to HTML5 forms
description: HTML5 フォームは、Adobe Experience Manager 6.0(AEM 6.0) ソフトウェアの新しい機能で、XFA フォームテンプレートをHTML5 形式でレンダリングする機能を提供します。
seo-description: HTML5 forms is a new capability in Adobe Experience Manager 6.0 (AEM 6.0) software that offers rendering of XFA form templates in HTML5 format.
uuid: 63a2f000-c4c5-40e8-ab3f-c7c44c79ec09
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 672ee050-63d1-46ed-bef2-f55800208d78
docset: aem65
feature: Mobile Forms
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 37%

---

# HTML5 フォームの概要{#introduction-to-html-forms}

HTML5 フォームは、Adobe Experience Manager 6.0(AEM 6.0) ソフトウェアの新しい機能で、XFA フォームテンプレートをHTML5 形式でレンダリングする機能を提供します。 この機能により、XFA ベースの PDF がサポートされていないモバイルデバイスおよびデスクトップブラウザー上のフォームのレンダリングが可能です。HTML5 フォームは、XFA フォームテンプレートの既存の機能をサポートしているだけでなく、モバイルデバイス用に手書き署名などの新しい機能もあります。

HTML5 フォームは、標準のHTML5 構成に基づいてドキュメントを生成します。 HTML5 フォームは、HTML5 をサポートする最新のすべてのブラウザーで表示できます。 ブラウザーのための追加のブラウザープラグインをインストールする必要がありません。サポートされるブラウザーについて詳しくは、[サポートされるクライアントプラットフォーム](https://adobe.com/go/learn_aemforms_documentation_63_jp)を参照してください。

![HTML5 フォームプレビュー](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## HTML5 フォームの主な機能 {#key-capabilities-of-html-forms-br}

* 互換性のあるすべてのブラウザーでサポートされているHTML5 の既存の XFA フォームをレンダリングします。
* 標準の XFA フォームデザイン機能を活用して、モバイルデバイス用のフォームをターゲットにします。
* 動的 XFA 機能をHTML5 形式で使用します。
* 高精度のSVGテキストレイアウト (SVG1.1) を使用して、PDFテキストレイアウトと一致させます。
* JavaScript および FormCalc のサポートを提供します。
* データ駆動型のイベントまたはユーザー入力に基づいて、フラグメントをインタラクティブなフォームに動的にアセンブリします。
* 企業の標準に従ってフォームの外観に合わせたカスタム CSS をサポートします。
* カスタムウィジェットを有効にして、豊富なデータキャプチャエクスペリエンスを提供します。
* Web アプリへの統合をサポートします。

### マルチチャネル公開 {#multichannel-publishing}

フォーム開発者は、XFA テンプレートを使用して、フォームをPDFおよびHTML5 形式でレンダリングできます。 この機能は、HTML5 フォームのデザインプラクティスに合わせて最小限の変更を加える必要がある大規模な XFA フォームセットがある場合に便利です。 既存の XFA フォームをHTML5 にレンダリングして、XFA ベースのPDFがまだサポートされていない様々なデバイスをターゲットに設定できます。

## HTML5 フォームの管理 {#manage-html-forms}

AEMには、AEM Forms UI を使用してすべてのフォームテンプレートを一覧表示および管理するための統合ビューも用意されています。 フォームのアクティベート、アクティベート解除、公開、プレビューを行うことができます。 詳しくは、 [フォーム管理の概要](../../forms/using/introduction-managing-forms.md).

### Formsのカスタマイズ {#forms-customization}

HTML5 forms は、標準のテンプレート 5 構成を使用してフォームHTMLをレンダリングします。 これにより、Web テクノロジ、主にCSS および JavaScript を使用した、HTML5 形式のフォームの拡張およびカスタマイズが容易になります。既存のウィジェットの外観を簡単にカスタマイズし、独自のウィジェットを作成するか、フォームのカスタムスタイルを使用できます。カスタムウィジェットの作成、および既存のウィジェットのカスタマイズについて詳しくは、[HTML5 フォームのプラグインカスタムウィジェット](../../forms/using/custom-widgets.md)を参照してください。
