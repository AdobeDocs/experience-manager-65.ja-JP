---
title: HTML5 フォームの概要
seo-title: HTML5 フォームの概要
description: HTML5 フォームは、HTML5 形式で XFA フォームテンプレートをレンダリングする Adobe Experience Manager 6.0（AEM 6.0）ソフトウェアの新しい機能です。
seo-description: HTML5 フォームは、HTML5 形式で XFA フォームテンプレートをレンダリングする Adobe Experience Manager 6.0（AEM 6.0）ソフトウェアの新しい機能です。
uuid: 63a2f000-c4c5-40e8-ab3f-c7c44c79ec09
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 672ee050-63d1-46ed-bef2-f55800208d78
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# HTML5 フォームの概要{#introduction-to-html-forms}

HTML5 フォームは、HTML5 形式で XFA フォームテンプレートをレンダリングする Adobe Experience Manager 6.0（AEM 6.0）ソフトウェアの新しい機能です。この機能により、XFA ベースの PDF がサポートされていないモバイルデバイスおよびデスクトップブラウザー上のフォームのレンダリングが可能です。 HTML5 フォームは XFA フォームテンプレートの既存の機能をサポートしているだけでなく、モバイルデバイスのための新しい機能（例えば手書き署名）も追加します。

HTML5 フォームは標準の HTML5 構造に基づいてドキュメントを生成します。HTML5 フォームは、HTML5 をサポートしている現時点のすべてのブラウザーで見ることができます。ブラウザーのための追加のブラウザープラグインをインストールする必要がありません。 For more information about supported browsers, see [Supported client platforms](https://adobe.com/go/learn_aemforms_supportedplatforms_63).

![](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## HTML5 フォームの主な機能 {#key-capabilities-of-html-forms-br}

* 既存の XFA フォームを、互換性のあるすべてのブラウザーでサポートされている HTML5 でレンダリングします。
* モバイルデバイス用のフォームをターゲットにした標準の XFA フォームデザイン機能を活用します。
* 動的 XFA 機能を HTML5 形式で使用します。
* 非常に正確な SVG テキストレイアウト（SVG 1.1）を使用して、PDF テキストレイアウトと一致させます。
* JavaScript および FormCalc のサポートを提供します。
* データ主導のイベントまたはユーザー入力に基づいてフラグメントをインタラクティブなフォームに動的にアセンブリします。
* 企業の基準に合わせてフォームの外観を設定するカスタム CSS をサポートします。
* カスタムウィジェットを有効化して、豊富なデータ取得操作を提供します。
* Web アプリへの統合をサポートします。

### マルチチャンネルプランニング {#multichannel-publishing}

フォーム開発者は XFA テンプレートを使用して PDF および HTML5 形式でフォームのレンダリングが可能です。この機能は、HTML5 フォームのデザイン実行に合わせた変更が最小限だけ必要な XFA フォームの大規模なセットがあるシナリオで有益です。XFA ベースの PDF がまだサポートされていない様々なデバイスを対象として、既存の XFA フォームを HTML5 にレンダリングすることができます。

## HTML5 フォームの管理 {#manage-html-forms}

また AEM は、AEM Forms UI を使用してすべてのフォームテンプレートをリストにして管理する際に、統一された表示方法を提供します。フォームのアクティベート、アクティベート解除、パブリッシュ、およびプレビューを実行できます。詳しくは、「[フォーム管理の概要](../../forms/using/introduction-managing-forms.md)」を参照してください。

### フォームのカスタマイズ {#forms-customization}

HTML5 フォームは、標準 HTML5 構成を使用してフォームテンプレートをレンダリングします。これにより、Web テクノロジ、主にCSS および JavaScript を使用した、HTML5 形式のフォームの拡張およびカスタマイズが容易になります。 既存のウィジェットの外観を簡単にカスタマイズし、独自のウィジェットを作成するか、フォームのカスタムスタイルを使用できます。 For more information about creating custom widgets and customizing existing widgets, see [Plug in custom widgets with HTML5 forms](../../forms/using/custom-widgets.md).
