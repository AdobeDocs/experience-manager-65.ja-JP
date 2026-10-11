---
title: 参照用のアダプティブフォームフラグメント
description: AEM Forms には、フォームをすばやく作成するためにアセットとして使用できるアダプティブフォームフラグメントが用意されています。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
exl-id: 933c164e-7c39-4d2e-834b-53a3c2b4ec90
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 100%
---
# 参照用のアダプティブフォームフラグメント{#reference-adaptive-form-fragments}

[アダプティブフォームフラグメント](../../forms/using/adaptive-form-fragments.md)は、フォームの作成時に使用できるフィールドのグループまたはフィールドのグループを含むパネルです。 これを使用してフォームを簡単にすばやく作成できます。 サイドバーのアセットブラウザーを使用して、アダプティブフォームフラグメントをフォームにドラッグ＆ドロップし、それをフォームエディターで編集できます。

アダプティブフォームの作成者を対象に、[AEM Forms アドオンパッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)で参照用のフラグメントが提供されています。 次のフラグメントが含まれています。

* アドレス
* 連絡先情報
* クレジットカード情報
* 現在の職業
* 扶養家族の情報
* 職歴
* 収入と支出
* 名前
* 利用条件
* 手書き付き利用条件

パッケージをインストールすると、フォームとドキュメントの下に参照用フラグメントを含む参照用フラグメントフォルダーが作成されます。 パッケージのインストールについては、[パッケージの作業方法](/help/sites-administering/package-manager.md)を参照してください。

![すべてのフラグメントが表示されている](assets/ootb-frags.png)

## アドレス {#address}

郵送先住所を指定するためのフィールドが含まれています。 使用できるフィールドは、アドレス、郵便番号、市、州および国です。 指定された米国の郵便番号に対応する市と州を入力する事前設定済みの web サービスも含まれています。

![住所フラグメント](assets/address.png)

<!--
[Click to enlarge

](assets/address-1.png)
-->

## 連絡先情報 {#contact-information}

電話番号とメールアドレスを取得するためのフィールドが含まれています。

![連絡先情報フラグメント](assets/contact-info.png)

<!--
[Click to enlarge

](assets/contact-info-1.png)
-->

## クレジットカード情報 {#credit-card-information}

支払い処理に使用できるクレジットカード情報を取得するためのフィールドが含まれています。
[![クレジットカード情報フラグメント](assets/cc-info.png)](assets/cc-info-1.png)

## 現在の職業 {#current-employment}

雇用形態、雇用分野、役職、会社名、入社日など、現在の職業の詳細を取得するためのフィールドが含まれています。

![現在の職業フラグメント](assets/current-emp.png)

<!--
[Click to enlarge

](assets/current-emp-1.png)
-->

## 扶養家族の情報 {#dependents-information}

1 人以上の扶養家族に関する情報（名前、関係、年齢など）を表形式で指定するためのフィールドが含まれています。

![扶養家族の情報フラグメント](assets/dependents-info.png)

<!--
[Click to enlarge

](assets/dependents-info-1.png)
-->

## 職歴 {#employment-history}

職歴を取得するためのフィールドが含まれています。 複数の会社を追加できます。

![職歴フラグメント](assets/emp-history.png)

<!--
[Click to enlarge

](assets/emp-history-1.png)
-->

## 収入と支出 {#income-expenditure}

1 か月のキャッシュフローと支出を取得するためのフィールドが含まれています。 ユーザーに詳しい財務情報を提供するように求めるフォームでは、このフラグメントを使用して収入と支出を取得できます。

![収入と支出フラグメント](assets/income.png)

<!--
[Click to enlarge

](assets/income-1.png)
-->

## 名前 {#name}

敬称、名、ミドルネームおよび姓を指定するためのフィールドが含まれています。

![名前フラグメント](assets/name.png)

<!--
[Click to enlarge

](assets/name-1.png)
-->

## 利用条件 {#terms-conditions}

ユーザーがフォームを送信する前に同意する利用条件を指定します。

![利用条件フラグメント](assets/tnc.png)

<!--
[Click to enlarge

](assets/tnc-1.png)
-->

## 手書き付き利用条件 {#terms-conditions-with-scribble}

ユーザーがフォームを送信する前に同意して署名する利用条件を指定します。

![署名付き利用条件](assets/tnc-scribble.png)

<!--
[Click to enlarge

](assets/tnc-scribble-1.png)
-->
