---
title: コンポーネントコンソール
seo-title: Components Console
description: コンポーネントコンソール
seo-description: null
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
exl-id: d79107b9-dfa4-4e80-870e-0b7ea72f0bc7
source-git-commit: e85aacd45a2bbc38f10d03915e68286f0a55364e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 61%

---

# コンポーネントコンソール {#components-console}

コンポーネントコンソールを使用すると、インスタンスに定義されたすべてのコンポーネントを参照し、各コンポーネントの主な情報を表示できます。

**ツール**／**一般**／**コンポーネント**&#x200B;からアクセスできます。コンソールでは、カード表示およびリスト表示を使用できます。コンポーネントのツリー構造がないので、列表示は使用できません。

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>コンポーネントコンソールには、システムのすべてのコンポーネントが表示されます。[コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)には、作成者が使用できるコンポーネントが表示され、ピリオド（`.`）で始まるすべてのコンポーネントグループは非表示になります。

## 検索 {#searching}

「**コンテンツのみ**」アイコン（左上）を使用して「**検索**」パネルを開き、コンポーネントの検索やフィルタリングを行うことができます。

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### コンポーネントの詳細 {#component-details}

特定のコンポーネントに関する詳細を表示するには、必要なリソースをタップまたはクリックします。 次の 3 つのタブが表示されます。

* **プロパティ**

  ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

  「プロパティ」タブでは、次のことができます。

   * コンポーネントの一般的なプロパティの表示。
   * 次の項目を表示： [アイコンまたは省略形が定義されています](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) コンポーネント用。

      * アイコンのソースをクリックすると、そのコンポーネントに移動します。

   * 次を表示： **リソースタイプ** および **リソースのスーパータイプ** （定義されている場合）。

      * 「リソーススーパータイプ」をクリックすると、そのコンポーネントが表示されます。

  >[!NOTE]
  >
  >`/apps` は実行時には編集できないので、コンポーネントコンソールは読み取り専用です。

* **ポリシー**

  ![ポリシー](assets/chlimage_1-169.png)

* **ライブ使用状況**

  ![ライブ使用状況](assets/chlimage_1-170.png)

  >[!CAUTION]
  >
  >この表示で収集される情報の性質から、照合および表示には時間がかかることがあります。

* **ドキュメント**

  開発者が [コンポーネントのドキュメント](/help/sites-developing/developing-components.md#documenting-your-component)を含めない場合、 **ドキュメント** タブをクリックします。 利用できるドキュメントがない場合は、「**ドキュメント**」タブは表示されません。

  ![ドキュメント](assets/chlimage_1-171.png)
