---
title: Firefox とChromeで XFA ベースのPDF formsを開く方法
description: Firefox とChromeで XFA ベースのPDF formsを開く方法
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# Firefox とChromeで XFA ベースのPDF formsを開く方法

## 問題

Mozilla Firefox およびGoogle Chromeで導入された組み込みのPDF ビューアでは、XFA ベースのPDF formsをサポートしていません。 したがって、XFA ベースのPDF formsは、それ以降のバージョンの Firefox やChromeでは開きません。

## 解決策

Firefox およびChromeで XFA ベースのPDF formsを使用するには、次の手順を実行して、Firefox とChromeを Adobe Reader またはAdobe Acrobatで PDF を開くように設定します。

>[!NOTE]
> 
> Adobe Reader またはAdobe Acrobatがマシンにインストールされていることを確認します。

### Firefox の設定

1. Firefox で、「**ツール」 > 「オプション**」を選択します。

1. [ オプション ] ダイアログで、[**アプリケーション**] をクリックします。

1. 「アプリケーション」タブの検索フィールドに「PDF」と入力します。

1. 検索結果のコンテンツタイプが「Portable Document Format （PDF）」の場合は、「アクション」ドロップダウンリストから「**Adobe Acrobatを使用（Firefox）**」を選択します。
   ![use-adobe-acrobat](/help/forms/using/assets/use-adobe-acrobat.png)
1. 「OK」をクリックします。

1. Firefox を再起動します。

### Chromeの設定

1. Chromeで、chrome://plugins/に移動します。

1. Chrome PDF ビューアで「無効にする」をクリックしてから、Adobe PDF プラグインで「有効にする」をクリックします。
   ![chrome-pdf-viewer](/help/forms/using/assets/chrome-image.png)
詳しくは、[GoogleのAdobe PDF プラグイン ](https://support.google.com/chrome/?hl=en&amp;visit_id=638803785294106945-2276548125&amp;rd=4&amp;topic=3421431#topic=7439538) ドキュメントを参照してください。

>[!NOTE]
> 
> LiveCycle ES4 では、XFA ベースのフォームをHTML5 にレンダリングすることができます。これにより、iPadのようなモバイルデバイスで動作するブラウザーなど、HTML5 をサポートしているブラウザーでフォームを開くことができます。 HTML5 レンディションのフォームは、フォームデザインのレイアウトを維持し、XFA フォームテンプレートに埋め込まれたほとんどのフォームロジック（JavaScript、フォーム計算、フォーム検証など）をサポートします。 このようにして、XFA フォームに対するテクノロジー投資は、Adobe Reader プラグインを実行できないデバイスに簡単に引き継がれます。
>詳しくは、[LiveCycle 製品ドキュメント ](https://business.adobe.com/products/experience-manager/forms/aem-forms.html) を参照してください。

[ 法律上の注意 ](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [ オンラインプライバシーポリシー ](https://www.adobe.com/jp/privacy.html)