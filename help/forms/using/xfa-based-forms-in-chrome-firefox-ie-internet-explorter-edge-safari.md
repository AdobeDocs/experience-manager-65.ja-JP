---
title: Google Chrome、Firefox、Microsoft Edge、Microsoft Internet Explorer、Apple Safari で XFA ベースのPDF formsを開けない
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
source-git-commit: abaef885f1324c4e0e4c5d74485d5b419ff88e2b
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Google Chrome、Firefox、Microsoft Edge、Microsoft Internet Explorer、Apple Safari で XFA ベースのPDF formsを開けない{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

最近の多くのブラウザーバージョンには、XFA ベースのバージョンに対する独自の制限付きサポートが含まれていますPDF forms。 これらのブラウザーは XFA ベースのPDF formsを開くことができますが、提供される機能は制限されます。 最新のブラウザーで XFA ベースのPDFフォームを開いたり送信したりできない場合は、次のいずれかの方法を使用します。

* 用途 [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) または [Adobe®Adobe®Reader®](https://get.adobe.com/jp/reader/)、バージョン 8 以降：XFA ベースのPDF formsを開いて送信します。
* AcrobatとReaderは、Microsoft® Windows®上でPDFを保護ビューモードで開くようにを設定できます。これにより、XFA ベースのPDF formsが開かなくなります。 AcrobatまたはReaderの保護ビューモードが無効になっていることを確認します。 詳しくは、 [保護ビュー（Windows のみ）](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (Forms Developers の場合 )Adobe Experience Manager Formsは、
   * [XFA ベースのフォームをHTML5 Formsにレンダリング](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) これにより、iPadなどのモバイルデバイスで実行されているブラウザーも含め、HTML5 をサポートするブラウザーでフォームを開くことができます。 フォームのHTML5 レンディションはフォームデザインのレイアウトを維持し、XFA フォームテンプレートに埋め込まれるほとんどのフォームロジック（JavaScript、フォームの計算、フォームの検証など）をサポートします。
   * [XFA ベースフォームをモバイルレスポンシブアダプティブFormsに変換する](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). これらのフォームはレスポンシブレイアウト、パーソナライゼーション機能を提供し、必要に応じてフィールドやセクションを追加または削除することで、ユーザーの応答に動的に適応します。 また、各種データソース用の標準コネクタ、レコードのドキュメント機能、Adobe Analyticsへの簡単な接続によるパフォーマンス評価も提供されます。 詳しくは、 [主な特長と機能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/key-features.html).

これにより、XFA フォームに対する技術投資が保護され、エンドユーザーに最適なエクスペリエンスを提供し続けます。 詳しくは、 [Adobe Experience Manager Forms製品ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html).
