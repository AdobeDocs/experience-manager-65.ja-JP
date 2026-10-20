---
title: Adobe Experience Manager（AEM）と web アクセシビリティのガイドライン
description: Adobe Experience Manager（AEM）と web アクセシビリティのガイドラインの概要
exl-id: db8785b9-09eb-444a-addc-74c520e710a9
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Developer, Leader, User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
    internal-label: Experience Manager 6.5
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c42c36cf-eeed-484a-8b39-a33a68192a07
    internal-label: Compliance
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 89%
---
# AEM と Web アクセシビリティのガイドライン{#aem-and-the-web-accessibility-guidelines}

ウェブコンテンツを、障害や制限の有無にかかわらず、対象オーディエンスにとって可能な限りアクセシブルであるよう設計することには、多くの社会的、経済的、法的動機があります。 このため Adobe Experience Manager（AEM）による web アクセシビリティは、優れた web デザインの重要な側面となっています。

AEM を使用して、アクセスしやすい web サイトおよびコンテンツを作成する場合、次のような影響があります。

* 管理者は、アクセシビリティ機能が正しく有効化されるように AEM を設定する必要があります。

* 作成者は、これらの機能を使用して、アクセシブルな Web サイトを作成する必要があります。

  アクセシブルなコンテンツの作成はプロセスです。 AEM には各種機能が用意されていますが、コンテンツ作成者は、アクセスしやすいコンテンツを作成するために必要な手法に従う必要があります。

* テンプレート開発者も同様に、Web サイトデザインを実装する際に、こうした問題を認識する必要があります。

Adobe Experience Manager は、[World Wide Web Consortium](#world-wide-web-consortium) が提供する [ガイドライン](#wcag-accessibility-guidelines)と連携しています。

>[!NOTE]
>
>詳細に関しては、[アドビソリューションのアクセシビリティ準拠レポート](https://www.adobe.com/accessibility/compliance.html) を参照してください。

## World Wide Web Consortium {#world-wide-web-consortium}

[World Wide Web Consortium（W3C）](https://www.w3.org/)は、Web 標準の策定を専門とする国際コミュニティです。 [Web Accessibility Initiative（WAI）](https://www.w3.org/WAI/)は、[Web コンテンツのアクセシビリティに関するガイドライン](#wcag-accessibility-guidelines)を公開しています。

## Web Content Accessibility Guidelines（WCAG）2.1 {#wcag-accessibility-guidelines}

Web デザイナーや開発者がアクセシブルな web サイトを作成できるように、[Web Accessibility Initiative（WAI）](https://www.w3.org/WAI/)は [2018年6月に Web Content Accessibility Guidelines（WCAG）2.1](https://www.w3.org/TR/WCAG/) を発行しました。

WCAG 2.1 では、[アクセシビリティレベルとそれらの準拠方法に関するガイドライン（および関連する成功基準）を提供](https://www.w3.org/TR/WCAG/#conformance)しています。

## WCAG 2.1 および AEM {#wcag-aem}

Adobe Experience Manager を使用すると、コンテンツ作成者や Web サイトの所有者は、WCAG 2.1 レベル A およびレベル AA の達成基準を満たす Web コンテンツを作成できます。

* [WCAG 2.1 クイックガイド](/help/managing/qg-wcag.md)で WCAG 2.1 の特定の側面を取り上げています。

* AEM との関係について詳しくは、[アクセシブルなコンテンツの作成](/help/sites-authoring/creating-accessible-content.md)を参照してください。

* [&#x200B; アクセス可能なサイトを作成するためのリッチテキストエディターの設定](/help/sites-administering/rte-accessible-content.md)
アクセス可能なコンテンツを生成するために管理者がAEMを設定する方法に関するガイドラインです。

* [&#x200B; アクセス可能なアダプティブ Formsの作成](/help/forms/using/creating-accessible-adaptive-forms.md)
Adobe Experience Manager（AEM）には、能力が異なるユーザー向けにアダプティブフォームの使いやすさを向上させる機能がいくつか用意されています。 このソリューションは、フォーム作成者がアクセスしやすいアダプティブフォームを作成する上でも役立ちます。

>[!NOTE]
>
>サイトを作成する際は、サイトが準拠する全体的なレベルを決めておく必要があります。

## Adobe におけるアクセシビリティ {#accessibility-at-adobe}

詳しくは、[アドビのアクセシビリティリソースセンター](https://www.adobe.com/jp/accessibility/)にアクセスしてください。
