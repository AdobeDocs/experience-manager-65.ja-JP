---
title: 参照レターテンプレート
description: AEM Formsには、Correspondence Management のレターレイアウトテンプレートが用意されており、これを使用してレターをすばやく作成できます。
products: SG_EXPERIENCEMANAGER/6.3/FORMS
content-type: reference
topic-tags: correspondence-management
exl-id: 40d127b5-1ce6-41fb-ac4c-2bf7ae79da82
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 21%

---

# 参照レターテンプレート {#reference-letter-templates}

Correspondence Management のレターテンプレートには、一般的なフォームフィールド、ヘッダーやフッターなどのレイアウト機能、コンテンツを配置するための空の「ターゲット領域」が含まれています。

Correspondence Management のレターテンプレートは、[AEM Forms アドオンパッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)で入手できます。使用するブランディングやビジネスニーズに応じて、Designer でテンプレートをカスタマイズできます。このパッケージには、次のテンプレートが含まれています。

* クラシック
* クラシックシンプル
* バランス（左）
* バランス（右）
* Visual Left
* ビジュアルトップ
* ビジュアルトップ — クラシック

パッケージをインストールすると、レイアウトテンプレート (XDP) が次の場所にある templates-folder に一覧表示されます。

`https://'[server]:[port]'/[context-root]/aem/forms.html/content/dam/formsanddocuments/templates-folder`

このパッケージのすべてのテンプレートで共通するフィールドは次のとおりです。

* 日付
* 挨拶
* 終了テキスト
* 署名テキスト

![一覧表示されたすべての CM レターテンプレート](assets/templatescorrespondence.png)

AEM-FORMS-6.3-REFERENCE-LAYOUT-TEMPLATES パッケージをインストールすると、テンプレートが templates-folder に一覧表示されます。

## クラシック {#classic}

上にロゴが付いているクラシックテンプレートは、普通のプロフェッショナルなレターに適しています。

![クラシック](assets/classic.png)

クラシックPDFを使用して作成されたレターのテンプレートプレビュー

## クラシックシンプル {#classic-simple}

電話番号とメールアドレスを取得するためのフィールドが含まれています。クラシックシンプルテンプレートは、クラシックテンプレートに似ていますが、受信者のアドレスを入力できるフィールドがない点が異なります。

![連絡先情報フラグメント](assets/classicsimple.png)

クラシックシンプルテンプレートを使用して作成されたレターのPDFプレビュー

## バランス（左） {#balanced-left}

バランスレフトテンプレートでは、レターの左側にロゴが表示されます。

![balancedleft](assets/balancedleft.png)

バランスレフトPDFを使用して作成されたレターのテンプレートプレビュー

## バランス（右） {#balanced-right}

バランスライトテンプレートは、会社のロゴを左側に表示し、レター自体に受信者のアドレスを入力するスペースを提供します。 バランスライトテンプレートには、レターに複数のページが含まれる場合にリフローするフッターも含まれています。

![balancedright](assets/balancedright.png)

バランスライトテンプレートを使用して作成されたレターのPDFプレビュー

## Visual Left {#visual-left}

Visual Left テンプレートのページ左側には、会社のロゴがサイドヘッドの上に配置されたサイドヘッドがあります。 Visual Left テンプレートには件名フィールドがありますが、フッターはありません。

![visualleft](assets/visualleft.png)

Visual Left テンプレートを使用して作成されたレターのPDFプレビュー

## ビジュアルトップ {#visual-top}

ビジュアルトップテンプレートの上部に視覚的な余白が表示されます。 「ビジュアルトップ」テンプレートには、ページ自体に受信者のアドレスを入力するためのフィールドがあります。 ビジュアルトップテンプレートには、複数ページに拡張されるレターの件名フィールドとフッターが含まれます。

![visualtop](assets/visualtop.png)

ビジュアルトップテンプレートを使用して作成されたレターのPDFプレビュー

## ビジュアルトップ — クラシック {#visual-top-classic}

ビジュアルトップ — クラシックテンプレートでは、ページの上に会社のロゴが付いたヘッダーが表示されます。 ビジュアルトップ — クラシックテンプレートには、件名を入力するフィールドがありますが、フッターはありません。

![visualtopclassic](assets/visualtopclassic.png)

ビジュアルトップ - クラシックのテンプレートを使用して作成されたレターの PDF プレビュー
