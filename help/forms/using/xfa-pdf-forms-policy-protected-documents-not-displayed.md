---
title: XFA ベースの PDF フォームとポリシーで保護されたドキュメントに関する表示の問題
description: XFA ベースの PDF フォームとポリシーで保護されたドキュメントに関する表示の問題
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: c9beefac-14e9-466c-b5bd-44ffab1fb820
source-git-commit: 913e249ba52f1ee262ed78167ce3b2a857e86213
workflow-type: ht
source-wordcount: '390'
ht-degree: 100%

---

# XFA ベースの PDF フォームとポリシーで保護されたドキュメントに関する表示の問題

Adobe LiveCycle Rights Management を使用して XFA ベースの PDF フォームまたはポリシーで保護されたドキュメントを開くことができない場合は、次の理由を確認します。

* XFA ベースの PDF フォームとポリシーで保護されたドキュメントには、Adobe® Acrobat® または Adobe® Reader® バージョン 8 以降が必要です。最新の Reader または Acrobat のダウンロードについて詳しくは、[Adobe ダウンロード](https://www.adobe.com/jp/downloads.html)を参照してください。
* Mozilla Firefox および Google Chrome などのブラウザーには、XFA ベースの PDF フォームをサポートしていない組み込みの PDF ビューアが提供されています。これらのブラウザーで XFA ベースの PDF フォームを表示するには、Acrobat または Reader を使用して PDF を開くように設定する必要があります。詳しくは、Mozilla Firefox および Google Chrome の XFA ベースの PDF フォームを参照してください。
* Acrobat と Reader は、Microsoft® Windows® 上では、PDF を保護ビューモードで開くように設定することができます。これにより、XFA ベースの PDF フォームとポリシーで保護されたドキュメントが開かなくなります。Acrobat または Reader の保護ビューモードが無効になっていることを確認します。 詳しくは、[保護されたビュー（Windows のみ）](https://helpx.adobe.com/jp/acrobat/kb/end-of-support-acrobat-x-reader-x.html)を参照してください。
* モバイルデバイスで XFA ベースの PDF フォームまたはポリシーで保護されたドキュメントにアクセスする場合は、次の点を考慮します。

   * ポリシーで保護されたドキュメントをモバイルデバイスで開くには、Adobe Reader モバイル版が必要です。詳しくは、[Adobe Reader モバイルアプリ](https://www.adobe.com/jp/acrobat/mobile/acrobat-reader.html)を参照してください。
   * iOS、Android、Blackberry のモバイルデバイスおよびスマートフォンは、XFA フォームでの Adobe Reader プラグインをサポートしていません。 LiveCycle ES4 は、HTML5 を使用してモバイルデバイスをターゲットにするサービスを提供しています。フォーム作成者は、フォームをこれらのデバイスで使用できるようにするために、そのサービスを使用する必要があります。
   * Windows 8 モバイルデバイスで Metro スタイルを使用している場合は、クラシック表示に変更するか、LiveCycle ES4 で HTML5 を活用します。

>[!NOTE]
>
>LiveCycle ES4 は、iPad のようなモバイルデバイスで動作するブラウザーなど、HTML5 をサポートしているブラウザーでフォームを開くことができるように、XFA ベースのフォームを HTML5 にレンダリングするサポートを提供しています。フォームの HTML5 レンディションは、フォームデザインのレイアウトを保持し、XFA フォームテンプレートに埋め込まれたほとんどのフォームロジック（JavaScript、フォーム計算、フォーム検証など）をサポートします。この方法により、XFA フォームに対するテクノロジー投資は、Adobe Reader プラグインの実行が不可能なデバイスに簡単に引き継がれます。
>>詳しくは、[LiveCycle 製品へのアップグレードドキュメント](https://business.adobe.com/products/experience-manager/forms/aem-forms.html)を参照してください。

[法律上の注意](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [オンラインプライバシーポリシー](https://www.adobe.com/jp/privacy.html)
