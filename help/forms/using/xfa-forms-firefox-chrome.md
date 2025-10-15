---
title: Firefox と Chrome で XFA ベースの PDF フォームを開く方法
description: Firefox と Chrome で XFA ベースの PDF フォームを開く方法
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 31b52a82-5062-403e-bba7-e6a7e32ee961
source-git-commit: 913e249ba52f1ee262ed78167ce3b2a857e86213
workflow-type: ht
source-wordcount: '287'
ht-degree: 100%

---

# Firefox と Chrome で XFA ベースの PDF フォームを開く方法

## 問題

Mozilla Firefox および Google Chrome に導入された組み込みの PDF ビューアは、XFA ベースの PDF フォームをサポートしていません。したがって、XFA ベースの PDF フォームは、Firefox および Chrome の以降のバージョンでは開きません。

## 解決策

Firefox および Chrome で XFA ベースの PDF フォームを使用するには、次の手順を実行して、Firefox および Chrome を設定し、Adobe Reader または Adobe Acrobat を使用して PDF を開きます。

>[!NOTE]
> 
> Adobe Reader または Adobe Acrobat がマシンにインストールされていることを確認します。

### Firefox の設定

1. Firefox で、**ツール／オプション**&#x200B;を選択します。

1. オプションダイアログで、「**アプリケーション**」をクリックします。

1. 「アプリケーション」タブの検索フィールドに「PDF」と入力します。

1. 検索結果の Portable Document Format（PDF）コンテンツタイプの場合は、アクションドロップダウンリストから「**Adobe Acrobat を使用（Firefox 内で表示）**」を選択します。
   ![Adobe Acrobat を使用](/help/forms/using/assets/use-adobe-acrobat.png)
1. 「OK」をクリックします。

1. Firefox を再起動します。

### Chrome の設定

1. Chrome で、chrome://plugins/ に移動します。

1. Chrome PDF ビューアで「無効にする」をクリックしてから、Adobe PDF プラグインで「有効にする」をクリックします。
   ![Chrome PDF ビューア](/help/forms/using/assets/chrome-image.png)
詳しくは、Google の [Adobe PDF プラグイン](https://support.google.com/chrome/?hl=en&visit_id=638803785294106945-2276548125&rd=4&topic=3421431#topic=7439538)のドキュメントを参照してください。

>[!NOTE]
> 
> LiveCycle ES4 は、iPad のようなモバイルデバイスで動作するブラウザーなど、HTML5 をサポートしているブラウザーでフォームを開くことができるように、XFA ベースのフォームを HTML5 にレンダリングするサポートを提供しています。フォームの HTML5 レンディションは、フォームデザインのレイアウトを保持し、XFA フォームテンプレートに埋め込まれたほとんどのフォームロジック（JavaScript、フォーム計算、フォーム検証など）をサポートします。この方法により、XFA フォームに対するテクノロジー投資は、Adobe Reader プラグインの実行が不可能なデバイスに簡単に引き継がれます。
> >詳しくは、[LiveCycle 製品ドキュメント](https://business.adobe.com/jp/products/experience-manager/forms/aem-forms.html)を参照してください。

[法律上の注意](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [オンラインプライバシーポリシー](https://www.adobe.com/jp/privacy.html)
