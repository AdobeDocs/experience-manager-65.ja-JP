---
title: Google Chrome、Firefox、Microsoft&reg、Edge、Microsoft&reg、Internet Explorer、またはApple SafariでXFA ベースのPDF formsを開くことができない
description: Google Chrome、Firefox、Microsoft&reg、Edge、Microsoft&reg、Internet Explorer、またはApple SafariでXFA ベースのPDF formsを開くことができない
feature: Adaptive Forms,Document Services
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 83%
---
# Google Chrome、Firefox、Microsoft® Edge、Microsoft® Internet Explorer、Apple Safari で XFA ベースの PDF フォームを開けない{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

最近の多くのブラウザーバージョンには、XFA ベースの PDF フォームに対する独自の制限付きサポートが含まれています。 これらのブラウザーで XFA ベースの PDF フォームを開くことはできますが、提供される機能は限られています。 最新のブラウザーで XFA ベースの PDF フォームを開いたり送信したりできない場合は、次のいずれかの方法を使用します。

* XFA ベースの PDF フォームを開いて送信するには、[Adobe® Acrobat®](https://www.adobe.com/jp/acrobat.html) または [Adobe® Adobe® Reader®](https://get.adobe.com/jp/reader/) のバージョン 8 以降を使用します。
* Acrobat と Reader は、Microsoft® Windows® 上では、PDF を保護ビューモードで開くように設定することができます。これにより、XFA ベースの PDF フォームを開けなくなります。 Acrobat または Reader の保護ビューモードが無効になっていることを確認します。 詳しくは、[保護されたビュー（Windows のみ）](https://helpx.adobe.com/jp/reader/using/protected-mode-windows.html)を参照してください。
* （フォーム開発者向け）Adobe Experience Manager Forms は次の機能もサポートしています。

  * [XFA ベースのフォームを HTML5 フォームにレンダリング](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?lang=ja#key-capabilities-of-html-forms-br)して、iPad のようなモバイルデバイスで動作するブラウザーなど、HTML5 をサポートしているブラウザーでフォームを開くことができるようにします。 フォームの HTML5 レンディションは、フォームデザインのレイアウトを保持し、XFA フォームテンプレートに埋め込まれたほとんどのフォームロジック（JavaScript、フォーム計算、フォーム検証など）をサポートします。
  * [XFA ベースのフォームをモバイルレスポンシブなアダプティブフォームに変換](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=ja#create-an-adaptive-form-based-on-an-xfa-form-template)します。 これらのフォームは、レスポンシブレイアウトやパーソナライズ機能を提供し、フィールドやセクションを必要に応じて追加または削除することで、ユーザーの応答に動的に適応します。 また、様々なデータソース向けのすぐに使用できるコネクタ、DoR 機能、パフォーマンス評価のための Adobe Analytics への容易な接続も提供します。 詳しくは、[主な機能と機能を参照してください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=ja)
    これにより、XFA フォームへの技術投資を保護し、エンドユーザーに最適なエクスペリエンスを提供し続けることができます。 詳しくは、[Adobe Experience Manager Forms 製品ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=ja)を参照してください。
