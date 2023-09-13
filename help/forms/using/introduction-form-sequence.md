---
title: 複数ステップのフォームシーケンスの概要
description: AEM Formsでは、アダプティブフォーム内をユーザーが移動して入力する一連のフォームパネルを定義できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 37%

---

# 複数ステップのフォームシーケンスの概要{#introduction-to-multi-step-form-sequence}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブFormsの作成における大幅な進歩を表し、印象的なユーザーエクスペリエンスを実現します。 この記事では、基盤コンポーネントを使用したアダプティブFormsのオーサリングに関する古いアプローチについて説明します。 </span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html) |
| AEM 6.5 | この記事 |


アダプティブフォームを使用すると、フォーム作成者は、複数手順のデータキャプチャエクスペリエンスを非常に簡単に作成できます。 複数パネルの作成や、各パネルと別の移動パターンとの関連付けに対する組み込みサポートが付属しています。フォーム作成者は、フォームフィールドを論理セクションにグループ化し、グループをパネルとして表すことができます。 パネル間の移動はすべてパネルレイアウトを使用して制御されます。作成者は、様々なレイアウトでパネルを配置できます。例えば、ウィザードレイアウトで順番に配置することも、タブ付きレイアウトを使って臨時に配置することもできます。パネルレイアウトについて詳しくは、 [アダプティブフォームのレイアウト機能](../../forms/using/layout-capabilities-adaptive-forms.md).

一般的なフォーム入力操作では、データを取り込むだけでなく、より多くの手順が必要になります。 完全なフォーム送信には、フォームへの電子署名、フォームに入力された情報の検証、支払いの処理など、他の手順も含めることができます。 場合によって異なります。

データの取得に一連の手順が必要な場合や、規制に応じて特定の手順を実行する必要がある場合は、AEM Formsを使用すると、フォーム全体で共通の構造を適用することができます。 フォーム構造の実装を事前に計画し、フォームの手順の順序を定義します。 ![複数ステップのフォームシーケンスの例](assets/formpipeline.png)

複数ステップのフォームシーケンスの例

フォームの入力、検証、署名、確認の手順のシーケンスを作成する必要がある使用例を見てみましょう。 このようなシーケンスを作成する手順は、次のとおりです。

1. フォームテンプレートを定義し、そのテンプレートに必要なパネルを追加します。 シーケンスの各段階につき 1 つのパネルが必要です。ただし、パネル内にサブパネルを含めることはできます。

   この例では、次のパネルを追加できます。

   * **塗り**：データを取得するためのフォームフィールドが含まれます。 ここで、ネストされたサブパネルを含めて、個人、家族、財務など、様々な種類の情報のセクションを作成できます。

   * **検証**：XFA ベースのアダプティブフォームで使用できる&#x200B;**検証**&#x200B;コンポーネントが含まれます。入力パネルで取得した情報を検証するため、読み取り専用モードで表示します。

   * **E 署名**：XFA ベースのアダプティブフォームで使用できる&#x200B;**署名**&#x200B;コンポーネントが含まれます。次の署名サービスを提供します。

      * Adobe Document Cloud 電子サインサービス
      * 手書き署名

   * **確認**：ユーザーがフォームに署名してシーケンスの確認（概要）段階に到達したときにフォーム送信の確認メッセージを表示する&#x200B;**概要**&#x200B;コンポーネントが含まれます。作成者は概要コンポーネントのテキストの構成、お礼のメッセージの表示、生成された PDF へのリンクの表示などを設定できます。

1. root パネルのレイアウトを **[!UICONTROL ウィザード]** として選択します。
1. 残りの手順を実行して、フォームテンプレートを作成します。 詳しくは、 [カスタムアダプティブフォームテンプレートの作成](../../forms/using/custom-adaptive-forms-templates.md).

フォームテンプレートでフォームシーケンスを定義した後は、このシーケンスを使用して、基本構造をその場のシーケンスとして定義したフォームを作成できます。 必要に応じて、いつでもフォームをカスタマイズできます。
