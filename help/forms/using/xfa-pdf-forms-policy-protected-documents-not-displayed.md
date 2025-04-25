---
title: XFA ベースのPDF formsおよびポリシーで保護されたドキュメントの問題を表示
description: XFA ベースのPDF formsおよびポリシーで保護されたドキュメントの問題を表示
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# XFA ベースのPDF formsおよびポリシーで保護されたドキュメントの問題を表示

XFA ベースのPDF フォームまたはポリシーで保護されたドキュメントを Adobe LiveCycle Rights Management で開くことができない場合は、次の理由を確認してください。

* XFA ベースのPDF formsとポリシーで保護されたドキュメントには、Adobe® Acrobat® またはAdobe® Reader® のバージョン 8 以降が必要です。 最新のAdobeまたはAcrobatのダウンロードについては ](https://www.adobe.com/downloads.html)[Readerのダウンロード } を参照してください。
* Mozilla Firefox やGoogle Chromeなどのブラウザーには、XFA ベースのPDF formsをサポートしないPDF ビューアが組み込まれています。 これらのブラウザーで XFA ベースのPDF formsを表示するには、AcrobatまたはReaderを使用して PDF を開くように設定する必要があります。 詳しくは、Mozilla Firefox での XFA ベースのPDF formsおよびGoogle Chromeを参照してください。
* AcrobatおよびReaderは、Microsoft® Windows® 上では、PDF を保護ビューモードで開くように設定することができます。これにより、XFA ベースのPDF formsおよびポリシーで保護されたドキュメントが開かなくなります。 Acrobat または Reader の保護ビューモードが無効になっていることを確認します。 詳しくは、[保護されたビュー（Windows のみ）](https://helpx.adobe.com/acrobat/kb/end-of-support-acrobat-x-reader-x.html)を参照してください。
* XFA ベースのPDF formsまたはポリシーで保護されたドキュメントにモバイルデバイスでアクセスする場合は、次の点を考慮してください。

   * ポリシーで保護されたドキュメントをモバイルデバイスで開くには、モバイル用 Adobe Reader が必要です。 詳しくは、[Adobe Reader モバイルアプリ ](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html) を参照してください。
   * iOS、Android、Blackberry のモバイルデバイスとスマートフォンでは、XFA フォームを含む Adobe Reader プラグインがサポートされていません。 LiveCycle ES4 には、HTML5 を使用してモバイルデバイスをターゲットにするサービスがあります。これらのデバイスでフォームを使用できるようにするには、フォーム作成者がそのサービスを使用する必要があります。
   * Windows 8 モバイルデバイスで Metro スタイルを使用している場合は、クラシック表示に切り替えるか、LiveCycle ES4 でHTML5 を利用します。

>[!NOTE]
>
>LiveCycle ES4 では、XFA ベースのフォームをHTML5 にレンダリングすることができます。これにより、iPadのようなモバイルデバイスで動作するブラウザーなど、HTML5 をサポートしているブラウザーでフォームを開くことができます。 HTML5 レンディションのフォームは、フォームデザインのレイアウトを維持し、XFA フォームテンプレートに埋め込まれたほとんどのフォームロジック（JavaScript、フォーム計算、フォーム検証など）をサポートします。 このようにして、XFA フォームに対するテクノロジー投資は、Adobe Reader プラグインを実行できないデバイスに簡単に引き継がれます。
>詳しくは、「[LiveCycle 製品ドキュメントへのアップグレード ](https://business.adobe.com/products/experience-manager/forms/aem-forms.html) を参照してください。

[ 法律上の注意 ](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [ オンラインプライバシーポリシー ](https://www.adobe.com/jp/privacy.html)