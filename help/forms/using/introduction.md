---
title: HTML5 フォームの概要
description: HTML5 フォームは、HTML5 形式で XFA フォームテンプレートをレンダリングできる Adobe Experience Manager 6.0（AEM 6.0）ソフトウェアの新しい機能です。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 100%

---

# HTML5 フォームの概要{#introduction-to-html-forms}

HTML5 フォームは、HTML5 形式で XFA フォームテンプレートをレンダリングできる Adobe Experience Manager 6.0（AEM 6.0）ソフトウェアの新しい機能です。この機能により、XFA ベースの PDF がサポートされていないモバイルデバイスおよびデスクトップブラウザー上のフォームのレンダリングが可能です。HTML5 フォームは、XFA フォームテンプレートの既存の機能をサポートしているだけでなく、モバイルデバイス用に手書き署名などの新しい機能もあります。

HTML5 フォームは、標準の HTML5 構造に基づいてドキュメントを生成します。HTML5 フォームは、HTML5 をサポートする現時点のすべてのブラウザーで表示できます。ブラウザーのための追加のブラウザープラグインをインストールする必要がありません。サポートされるブラウザーについて詳しくは、[サポートされるクライアントプラットフォーム](https://adobe.com/go/learn_aemforms_documentation_63_jp)を参照してください。

![HTML5 フォームプレビュー](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## HTML5 フォームの主な機能 {#key-capabilities-of-html-forms-br}

* 既存の XFA フォームを、互換性のあるすべてのブラウザーでサポートされる HTML5 でレンダリングします。
* 標準の XFA フォームデザイン機能を活用して、モバイルデバイス用のフォームをターゲットにします。
* 動的 XFA 機能を HTML5 形式で使用します。
* 高精度の SVG テキストレイアウト（SVG 1.1）を使用して、PDF テキストレイアウトと一致させます。
* JavaScript および FormCalc のサポートを提供します。
* データ主導のイベントまたはユーザー入力に基づいてフラグメントをインタラクティブなフォームに動的にアセンブリします。
* 企業の基準に合わせて、フォームの外観を設定するカスタム CSS をサポートします。
* カスタムウィジェットを有効化して、豊富なデータ取得操作を提供します。
* Web アプリへの統合をサポートします。

### マルチチャネル公開 {#multichannel-publishing}

フォーム開発者は XFA テンプレートを使用して、PDF および HTML5 形式でフォームをレンダリングできます。この機能は、HTML5 フォームのデザイン実行に合わせた変更が最小限だけ必要な XFA フォームの大規模なセットがあるシナリオで有益です。XFA ベースの PDF がまだサポートされていない様々なデバイスを対象として、既存の XFA フォームを HTML5 にレンダリングできます。

## HTML5 フォームの管理 {#manage-html-forms}

また AEM は、AEM Forms UI を使用して、すべてのフォームテンプレートをリストにして管理する際に、統一された表示方法を提供します。フォームのアクティベート、アクティベート解除、パブリッシュおよびプレビューを実行できます。詳しくは、[フォーム管理の概要](../../forms/using/introduction-managing-forms.md)を参照してください。

### フォームのカスタマイズ {#forms-customization}

HTML5 フォームは、標準 HTML5 構成を使用して、フォームテンプレートをレンダリングします。これにより、Web テクノロジ、主にCSS および JavaScript を使用した、HTML5 形式のフォームの拡張およびカスタマイズが容易になります。既存のウィジェットの外観を簡単にカスタマイズし、独自のウィジェットを作成するか、フォームのカスタムスタイルを使用できます。カスタムウィジェットの作成、および既存のウィジェットのカスタマイズについて詳しくは、[HTML5 フォームのプラグインカスタムウィジェット](../../forms/using/custom-widgets.md)を参照してください。
