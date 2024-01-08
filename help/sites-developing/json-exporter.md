---
title: コンテンツサービス用の JSON エクスポーター
description: AEM コンテンツサービスは、web ページだけに焦点を置かずに AEM のコンテンツの記述と配信を一般化するように設計されています。AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM web ページとは異なるチャネルにコンテンツを配信できます。
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 100%

---

# コンテンツサービス用の JSON エクスポーター{#json-exporter-for-content-services}

AEM コンテンツサービスは、web ページだけに焦点を置かずに AEM のコンテンツの記述と配信を一般化するように設計されています。

AEM コンテンツサービスにより、あらゆるクライアントで使用できる標準化された方法で、従来の AEM web ページとは異なるチャネルにコンテンツを配信できます。そうしたチャネルの例を次に示します。

* [単一ページアプリケーション](spa-walkthrough.md)
* ネイティブモバイルアプリケーション
* AEM の外部の他のチャネルおよびタッチポイント

構造化コンテンツを使用するコンテンツフラグメントでは、JSON エクスポーターを使用して任意の AEM ページのコンテンツを JSON データモデル形式で配信することにより、コンテンツサービスを提供できます。このメソッドは、独自のアプリケーションで使用できます。

>[!NOTE]
>
>ここで説明する機能は、[コアコンポーネントのリリース 1.1.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) 以降のすべてのコンポーネントで使用できます。

## JSON エクスポーターとコンテンツフラグメントコアコンポーネント {#json-exporter-with-content-fragment-core-components}

AEM JSON エクスポーターを使用すると、任意の AEM ページのコンテンツを JSON データモデル形式で配信できます。このメソッドは、独自のアプリケーションで使用できます。

AEM 内では、セレクター `model` と `.json` 拡張機能を使用して配信します。

`.model.json`

1. 例えば、次のような URL があります。

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. 次のようなコンテンツを配信します。

   ![chlimage_1-192](assets/chlimage_1-192.png)

代わりに、構造化コンテンツフラグメントのコンテンツを、ターゲット設定して配信することもできます。

フラグメントへのパス全体を使用します（`jcr:content` を経由）。例えば、次のような接尾辞を付けます。

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

ページには、単一のコンテンツフラグメントまたは様々なタイプの複数のコンポーネントを含めることができます。また、リストコンポーネントなどのメカニズムを使用して、関連するコンテンツを自動的に検索することもできます。

* 例えば、次のような URL があります。

  ```shell
  http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
  ```

* 次のようなコンテンツを配信します。

  ![chlimage_1-193](assets/chlimage_1-193.png)

  >[!NOTE]
  >
  >このデータにアクセスして使用するように[独自のコンポーネントを変更する](/help/sites-developing/json-exporter-components.md)ことができます。

  >[!NOTE]
  >
  >標準的な実装ではありませんが、[複数のセレクターがサポートされています](json-exporter-components.md#multiple-selectors)。ただし、`model` セレクターを最初に指定する必要があります。

### その他の情報 {#further-information}

関連トピック：

* Assets HTTP API

   * [Assets HTTP API](/help/assets/mac-api-assets.md)

* Sling モデル：

   * [Sling モデル - 1.3.0 以降のモデルクラスとリソースタイプの関連付け](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM と JSON：

   * [JSON 形式でページ情報を取得](/help/sites-developing/pageinfo.md)

## 関連ドキュメント {#related-documentation}

詳しくは、以下を参照してください。

* [Assets ユーザーガイドのコンテンツフラグメントに関するトピック](/help/assets/content-fragments/content-fragments.md)

* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
* [コンテンツフラグメントを使用したオーサリング](/help/sites-authoring/content-fragments.md)
* [コンポーネントの JSON エクスポートを有効化](/help/sites-developing/json-exporter-components.md)

* [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)および[コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja)
