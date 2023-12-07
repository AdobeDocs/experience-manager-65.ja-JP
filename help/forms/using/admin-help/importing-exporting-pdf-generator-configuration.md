---
title: PDF Generator 設定ファイルの読み込みおよび書き出し
description: PDF Generator設定ファイルの読み込みと書き出しの方法を説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 14%

---

# PDF Generator 設定ファイルの読み込みおよび書き出し {#importing-and-exporting-pdf-generator-configuration-files}

設定ファイルには、PDF Generator、ファイルタイプ、セキュリティ設定などのPDF変換情報が含まれています。

>[!NOTE]
>
>カスタム native2pdfconfig.xml ファイルを読み込むことで、PDF Generatorのタイムアウト設定を変更することはできません。 このファイルのタイムアウト設定は、情報提供のみを目的とし、現在の設定をPDF Generatorで表示します。 タイムアウト設定を変更するには、[AEM forms のインストールおよびデプロイ](https://www.adobe.com/go/learn_aemforms_installJBoss_63_jp)の「PDF Generator のパフォーマンスパラメーターの設定」を参照してください。

## 現在の設定ファイルを書き出します {#export-your-current-configuration-file}

1. 管理コンソールで、サービス/PDF Generator/設定ファイル/設定の書き出しをクリックします。
1. 設定を書き出すには、適切なオプションを選択します。

   * すべての名前付き設定を書き出すには、「設定全体をダウンロード」を選択します。
   * 1 つのAdobe PDF設定、セキュリティ設定、またはファイルタイプ設定のみを書き出すには、[ 最小構成のダウンロード ] を選択します。

     最小限の設定を書き出す場合は、書き出すAdobe PDF、セキュリティ、ファイルタイプの設定を選択します。

1. 「ダウンロード」をクリックし、XML ファイルを適切な場所に保存します。

## 設定ファイルのインポート {#import-a-configuration-file}

>[!NOTE]
>
>読み込まれたファイルの情報に基づいて、システムが再設定されます。

1. 管理コンソールで、サービス/PDF Generator/設定ファイル/設定の読み込みをクリックします。
1. 「既存の設定ファイルを読み込む」を選択します。
1. 「設定ファイル」ボックスでファイルの場所を指定するには、「参照」をクリックしてファイルを探して選択し、「 **インポート**.

## AutoCAD ファイル内のすべての画層を変換 {#convert-all-layers-within-autocad-files}

既定では、PDF Generatorは AutoCAD ファイルの既定の画層のみを、ファイル内のすべての画層ではなくPDFに変換します。 すべての画層を変換するには、次の手順に従います。

1. 管理コンソールで、サービス/PDF Generator/設定ファイル/設定の書き出しをクリックします。
1. 「設定全体をダウンロード」を選択し、「ダウンロード」をクリックします。
1. テキストエディターで、ダウンロードしたファイルを開き、`PDFMaker` タグ内の `AutoCAD` タグの下にテキスト `convertAllPages="true"` を追加します。
1. 管理コンソールで、サービス/PDF Generator/設定ファイル/設定の読み込みをクリックします。
1. 「既存の設定ファイルを読み込む」を選択し、更新したファイルを指定して、「読み込み」をクリックします。

   変更した設定ファイルを使用して変換された AutoCAD ファイルは、すべての画層が変換されます。

## PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. 管理コンソールで、サービス/PDF Generator/設定ファイル/設定の読み込みをクリックします。
1. 「設定をデフォルト設定にリセット」を選択し、「読み込み」をクリックします。
