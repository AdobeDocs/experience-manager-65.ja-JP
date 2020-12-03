---
title: ページプロパティのビューのカスタマイズ
seo-title: ページプロパティのビューのカスタマイズ
description: どのページにも、必要に応じて編集できる一連のプロパティがあります
seo-description: どのページにも、必要に応じて編集できる一連のプロパティがあります
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
translation-type: tm+mt
source-git-commit: c38c27d6f7172734f80735dd2f42cfa7bf58ad1d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 75%

---


# ページプロパティのビューのカスタマイズ{#customizing-views-of-page-properties}

どのページにも、ユーザーが表示および編集できる一連の[プロパティ](/help/sites-authoring/editing-page-properties.md)があります。ページ作成時に使用されるプロパティもあれば（作成ビュー）、後の段階で表示および編集できるプロパティもあります（編集ビュー）。これらのページプロパティは、適切なページコンポーネントのダイアログ（`cq:dialog`）によって定義され、使用可能になります。

>[!CAUTION]
>
>ページプロパティのビューのカスタマイズは、クラシック UI では使用できません。

各ページプロパティのデフォルト状態は次のとおりです。

* 作成ビューでは非表示（例：**ページを作成**&#x200B;ウィザード）

* 編集ビューでは表示（例：**プロパティを表示**）

変更が必要な場合は、フィールドを明確に設定する必要があります。それには適切なノードプロパティを使用します。

* 作成ビューで表示するページプロパティ（例：**ページを作成**&#x200B;ウィザード）：

   * 名前：`cq:showOnCreate`
   * 型：`Boolean`

* 編集表示で使用できるページプロパティ(例：**表示**/**編集**) **プロパティ**&#x200B;オプション):

   * 名前：`cq:hideOnEdit`
   * 型：`Boolean`

例として、基盤となるページコンポーネントの「**基本**」タブの「**他のタイトルと説明**」の下にグループ化されたフィールドの設定を参照してください。**が** に設定されているので、これらのフィールドは`cq:showOnCreate`ページを作成`true`ウィザードに表示されます。

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>ページプロパティのカスタマイズのガイドについては、[ページプロパティの拡張チュートリアル](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html)を参照してください。

## ページプロパティの設定 {#configuring-your-page-properties}

ページコンポーネントのダイアログを設定し、適切なノードプロパティを適用することによって、表示するフィールドを設定することもできます。

例えば、デフォルトでは、[**ページを作成**&#x200B;ウィザード](/help/sites-authoring/managing-pages.md#creating-a-new-page)には「**その他のタイトルと説明**」の下にグループ化されたフィールドが表示されます。これらのフィールドを非表示にするには、次のように設定します。

1. `/apps`の下にページコンポーネントを作成します。
1. ページコンポーネントの`basic`セクションに対して、[Sling Resource Marger](/help/sites-developing/sling-resource-merger.md)が提供する&#x200B;*ダイアログdiff*&#x200B;を使用して上書きを作成します。例：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >リファレンスとして、以下を参照してください。
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   ただし、******&#x200B;は`/libs`パス内の何も変更しないでください。
   `/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
   設定およびその他の変更に推奨される方法は次のとおりです。
   1. `/apps`の下に必要な項目（例：`/libs`に存在する項目）を再作成します
   1. `/apps` 内で変更作業をおこないます。


1. `basic`の`path`プロパティを設定して、基本タブの上書きを指定します（次の手順も参照してください）。 次に例を示します。

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 対応するパスに`basic` - `moretitles`セクションの上書きを作成します。例：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 適切なノードプロパティを適用します。

   * **名前**：`cq:showOnCreate`
   * **型**：`Boolean`
   * **値**: `false`

   **ページを作成**&#x200B;ウィザードに「**その他のタイトルと説明**」セクションが表示されなくなります。

>[!NOTE]
ライブコピーと一緒に使用するページプロパティを設定する場合、詳しくは、[ページプロパティに対する MSM ロックの設定](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui)を参照してください。

## ページプロパティの設定サンプル  {#sample-configuration-of-page-properties}

このサンプルは、[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) のダイアログ差分比較の手法を示しており、[`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties) が使用されています。また、`cq:showOnCreate`と`cq:hideOnEdit`の両方の使い方を説明します。

GitHub のコード

このページのコードは GitHub にあります

* [GitHubでaem-authoring-extension-page-dialogプロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
