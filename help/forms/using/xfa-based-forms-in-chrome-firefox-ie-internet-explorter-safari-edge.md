---
title: Google Chrome、Firefox、Microsoft&reg; Edge、Microsoft&reg; Internet Explorer、または Apple Safari で XFA ベースの PDF フォームを開けない
description: Google Chrome、Firefox、Microsoft&reg; Edge、Microsoft&reg; Internet Explorer、または Apple Safari で XFA ベースの PDF フォームを開けない
feature: Adaptive Forms
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 93%

---

# Google Chrome、Firefox、Microsoft® Edge、Microsoft® Internet Explorer、Apple Safari で XFA ベースの PDF フォームを開けない{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

最近の多くのブラウザーバージョンには、XFA ベースの PDF フォームに対する独自の制限付きサポートが含まれています。これらのブラウザーで XFA ベースの PDF フォームを開くことはできますが、提供される機能は限られています。最新のブラウザーで XFA ベースの PDF フォームを開いたり送信したりできない場合は、次のいずれかの方法を使用します。

* XFA ベースの PDF フォームを開いて送信するには、[Adobe® Acrobat®](https://www.adobe.com/jp/acrobat.html) または [Adobe® Adobe® Reader®](https://get.adobe.com/jp/reader/) のバージョン 8 以降を使用します。
* AcrobatとReaderは、Microsoft® Windows®上でPDFを保護表示モードで開くように設定できます。これにより、XFA ベースのPDF formsが開かなくなります。 Acrobat または Reader の保護ビューモードが無効になっていることを確認します。 詳しくは、[保護されたビュー（Windows のみ）](https://helpx.adobe.com/jp/reader/using/protected-mode-windows.html)を参照してください。
* （フォーム開発者向け）Adobe Experience Manager Forms は次の機能もサポートしています。

   * [XFA ベースのフォームを HTML5 フォームにレンダリング](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?lang=ja#key-capabilities-of-html-forms-br)して、iPad のようなモバイルデバイスで動作するブラウザーなど、HTML5 をサポートしているブラウザーでフォームを開くことができるようにします。フォームの HTML5 レンディションは、フォームデザインのレイアウトを保持し、XFA フォームテンプレートに埋め込まれたほとんどのフォームロジック（JavaScript、フォーム計算、フォーム検証など）をサポートします。
   * [XFA ベースのフォームをモバイルレスポンシブなアダプティブフォームに変換](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=ja#create-an-adaptive-form-based-on-an-xfa-form-template)します。これらのフォームは、レスポンシブレイアウトやパーソナライズ機能を提供し、フィールドやセクションを必要に応じて追加または削除することで、ユーザーの応答に動的に適応します。また、様々なデータソース、レコードのドキュメント機能、パフォーマンス評価のための Adobe Analytics への簡単な接続を利用するためにすぐに使用できるコネクタも用意されています。詳細情報は、[主な特長と機能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=ja)を参照してください。
これにより、XFA フォームに対するテクノロジー投資が保護され、エンドユーザーに最適なエクスペリエンスを継続的に提供することができます。詳しくは、[Adobe Experience Manager Forms 製品ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=ja)を参照してください。
