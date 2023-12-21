---
title: 複数ステップのフォームシーケンスの概要
description: AEM Forms を使用すると、ユーザーがアダプティブフォームを読み進み、記入する一連のフォームパネルを定義できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: 4ecdcb2659b26043f95ba1dc3e907c33f65b8834
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 100%

---

# 複数ステップのフォームシーケンスの概要{#introduction-to-multi-step-form-sequence}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html?lang=ja) |
| AEM 6.5 | この記事 |


フォーム作成者は、アダプティブフォームを使用すると非常に簡単に複数手順のデータキャプチャエクスペリエンスを作成できます。複数パネルの作成や、各パネルと別の移動パターンとの関連付けに対する組み込みサポートが付属しています。フォーム作成者は、フォームフィールドを複数の論理的なセクションにグループ分けし、グループをパネルとして表示できます。パネル間の移動はすべてパネルレイアウトを使用して制御されます。作成者は、様々なレイアウトでパネルを配置できます。例えば、ウィザードレイアウトで順番に配置することも、タブ付きレイアウトを使って臨時に配置することもできます。パネルレイアウトについては、[アダプティブフォームのレイアウトの機能](../../forms/using/layout-capabilities-adaptive-forms.md)を参照してください。

一般的なフォームの記入では、データを取得する以上に、関連する多くの手順があります。完全なフォームの送信には、フォームへの電子署名、フォームに入力した情報の検証、支払い処理など、他の手順が含まれる場合があります。これらの手順は、個々の場合によって異なります。

データ取得に一連の手順を必要とするケースや、規則により特定の手順を踏む必要があるケースでは、AEM Forms はフォーム全体でその共通の構造を適用する方法を提供します。フォーム構造の実装を事前に計画して、フォームの手順シーケンスを定義します。![複数ステップのフォームシーケンスの例](assets/formpipeline.png)

複数ステップのフォームシーケンスの例

フォームの入力、検証、署名および確認のシーケンスを作成する必要がある場合の使用例を考えてみます。このようなシーケンスを作成する手順は、次のとおりです。

1. フォームテンプレートを定義して、それに必要なパネルを追加します。シーケンスの各手順につき 1 つのパネルが必要です。ただし、パネル内にサブパネルを含めることができます。

   この例では、次のパネルを追加できます。

   * **入力**：データを取得するためのフォームフィールドが含まれます。ここではネストされたサブパネルを追加して、様々な種類の情報（個人、家族、財務など）のセクションを作成できます。

   * **検証**：XFA ベースのアダプティブフォームで使用できる&#x200B;**検証**&#x200B;コンポーネントが含まれます。入力パネルで取得した情報を検証するため、読み取り専用モードで表示します。

   * **E 署名**：XFA ベースのアダプティブフォームで使用できる&#x200B;**署名**&#x200B;コンポーネントが含まれます。E 署名には、次の署名サービスが含まれます。

      * Adobe Document Cloud 電子サインサービス
      * 手書き署名

   * **確認**：ユーザーがフォームに署名してシーケンスの確認（概要）段階に到達したときにフォーム送信の確認メッセージを表示する&#x200B;**概要**&#x200B;コンポーネントが含まれます。作成者は概要コンポーネントのテキストの構成、お礼のメッセージの表示、生成された PDF へのリンクの表示などを設定できます。

1. root パネルのレイアウトを&#x200B;**[!UICONTROL ウィザード]**&#x200B;として選択します。
1. 残りの手順を完了して、フォームテンプレートを作成します。[カスタムアダプティブフォームのテンプレートの作成](../../forms/using/custom-adaptive-forms-templates.md)を参照してください。

フォームテンプレートでフォームシーケンスを定義したら、そのテンプレートを使用して、適切なシーケンスで定義した基本構造を持つフォームを作成できます。フォームはいつでも要件に合わせてカスタマイズできます。
