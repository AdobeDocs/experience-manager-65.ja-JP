---
title: Google Chrome、Firefox、Microsoft&reg；で XFA ベースのPDF formsを開くことができませんEdge, Microsoft&reg;Internet Explorer またはApple Safari
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 66%

---


# Google Chrome、Firefox、Microsoft® Edge、Microsoft® Internet Explorer、Apple Safari で XFA ベースのPDF formsを開けない{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

最近の多くのブラウザーバージョンには、XFA ベースの PDF フォームに対する独自の制限付きサポートが含まれています。これらのブラウザーは XFA ベースのPDF formsを開くことができますが、提供される機能は制限されます。 最新のブラウザーで XFA ベースの PDF フォームを開いたり送信したりできない場合は、次のいずれかの方法を使用します。

* XFA ベースの PDF フォームを開いて送信するには、[Adobe® Acrobat®](https://www.adobe.com/jp/acrobat.html) または [Adobe® Adobe® Reader®](https://get.adobe.com/jp/reader/) のバージョン 8 以降を使用します。
* Acrobat と Reader は、Microsoft® Windows® 上では、PDF を保護ビューモードで開くように設定することができます。これにより、XFA ベースの PDF フォームが開かなくなります。 Acrobat または Reader の保護ビューモードが無効になっていることを確認します。 詳しくは、[保護されたビュー（Windows のみ）](https://helpx.adobe.com/jp/reader/using/protected-mode-windows.html)を参照してください。
* （フォーム開発者向け）Adobe Experience Manager Forms は次の機能もサポートしています。

   * [XFA ベースのフォームをHTML5 Formsにレンダリング](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?lang=ja#key-capabilities-of-html-forms-br) これにより、iPadなどのモバイルデバイスで実行されているブラウザーも含め、HTML5 をサポートするブラウザーでフォームを開くことができます。 フォームの HTML5 レンディションは、フォームデザインのレイアウトを保持し、XFA フォームテンプレートに埋め込まれたほとんどのフォームロジック（JavaScript、フォーム計算、フォーム検証など）をサポートします。
   * [XFA ベースのフォームをモバイルレスポンシブなアダプティブフォームに変換](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=ja#create-an-adaptive-form-based-on-an-xfa-form-template)します。これらのフォームは、レスポンシブレイアウトやパーソナライズ機能を提供し、フィールドやセクションを必要に応じて追加または削除することで、ユーザーの応答に動的に適応します。また、各種データソース用の標準コネクタ、レコードのドキュメント機能、Adobe Analyticsへの簡単な接続によるパフォーマンス評価も提供されています。 詳しくは、[主な特長と機能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=en)を参照してください。

このようにして、XFA フォームへのテクノロジー投資が保護され、エンドユーザーに最適なエクスペリエンスが継続的に提供されます。詳しくは、[Adobe Experience Manager Forms 製品ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html)を参照してください。
