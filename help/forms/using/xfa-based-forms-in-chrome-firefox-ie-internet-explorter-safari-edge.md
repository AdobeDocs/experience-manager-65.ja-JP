---
title: Google Chrome、Firefox、Microsoft Edge、Microsoft Internet Explorer または Apple Safari で XFA ベースの PDF フォームを開けない
description: Google Chrome、Firefox、Microsoft Edge、Microsoft Internet Explorer または Apple Safari で XFA ベースの PDF フォームを開けない
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
source-git-commit: 2f1e6eb5451e76b9688401b32d4866ed74cca84e
workflow-type: ht
source-wordcount: '372'
ht-degree: 100%

---

# Google Chrome、Firefox、Microsoft Edge、Microsoft Internet Explorer または Apple Safari で XFA ベースの PDF フォームを開けない{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

最近の多くのブラウザーバージョンには、XFA ベースの PDF フォームに対する独自の制限付きサポートが含まれています。これらのブラウザーでは XFA ベースの PDF フォームを開くことができますが、提供される機能は限られています。 最新のブラウザーで XFA ベースの PDF フォームを開いたり送信したりできない場合は、次のいずれかの方法を使用します。

* [Adobe® Acrobat®](https://www.adobe.com/jp/acrobat.html) または [Adobe® Adobe® Reader®](https://get.adobe.com/jp/reader/) バージョン 8 以降を使用して、XFA ベースの PDF フォームを開いたり送信したりします。
* Acrobat と Reader は、Microsoft® Windows® 上では、PDF を保護ビューモードで開くように設定することができます。これにより、XFA ベースの PDF フォームが開かなくなります。 Acrobat または Reader の保護ビューモードが無効になっていることを確認します。 詳しくは、 [保護されたビュー（Windows のみ）](https://helpx.adobe.com/jp/reader/using/protected-mode-windows.html)を参照してください。
* （フォーム開発者向け）Adobe Experience Manager Forms は次の機能もサポートしています。

   * [XFA ベースのフォームを HTML5 フォームにレンダリング](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?lang=ja#key-capabilities-of-html-forms-br)して、iPad のようなモバイルデバイスで動作するブラウザーなど、HTML5 をサポートしているブラウザーでフォームを開くことができるようにします。フォームの HTML5 レンディションは、フォームデザインのレイアウトを保持し、XFA フォームテンプレートに埋め込まれたほとんどのフォームロジック（JavaScript、フォーム計算、フォーム検証など）をサポートします。
   * [XFA ベースのフォームをモバイルレスポンシブなアダプティブフォームに変換](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=ja#create-an-adaptive-form-based-on-an-xfa-form-template)します。これらのフォームは、レスポンシブレイアウトやパーソナライズ機能を提供し、フィールドやセクションを必要に応じて追加または削除することで、ユーザーの応答に動的に適応します。また、さまざまなデータソースに対応する標準搭載のコネクタ、レコードのドキュメント機能およびパフォーマンス評価を目的とした Adobe Analytics への簡単な接続も提供します。詳しくは、 [主な特長と機能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/key-features.html?lang=ja)を参照してください。

このようにして、XFA フォームへのテクノロジー投資が保護され、エンドユーザーに最適なエクスペリエンスが継続的に提供されます。詳しくは、 [Adobe Experience Manager Forms の製品ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=ja)を参照してください。
