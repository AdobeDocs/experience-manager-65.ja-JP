---
title: コンテンツサービス用の JSON エクスポーター
seo-title: JSON Exporter for Content Services
description: AEM Content Services は、AEMでのコンテンツの説明と配信を、Web ページに焦点を当てるだけでなく、一般化するように設計されています。 従来のAEM Web ページではないチャネルに対して、あらゆるクライアントが利用できる標準化された方法を使用してコンテンツを配信します。
seo-description: AEM Content Services are designed to generalize the description and delivery of content in/from AEM beyond a focus on web pages. They provide the delivery of content to channels that are not traditional AEM web pages, using standardized methods that can be consumed by any client.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 34%

---

# コンテンツサービス用の JSON エクスポーター{#json-exporter-for-content-services}

AEM Content Services は、AEMでのコンテンツの説明と配信を、Web ページに焦点を当てるだけでなく、一般化するように設計されています。

従来のAEM Web ページではないチャネルに対して、あらゆるクライアントが利用できる標準化された方法を使用してコンテンツを配信します。 次のチャネルが含まれます。

* [単一ページアプリケーション](spa-walkthrough.md)
* ネイティブモバイルアプリケーション
* AEM の外部の他のチャネルおよびタッチポイント

構造化コンテンツを使用するコンテンツフラグメントでは、JSON エクスポーターを使用してAEMページのコンテンツを JSON データモデル形式で配信することで、コンテンツサービスを提供できます。 その後、このメソッドは、独自のアプリケーションで使用できます。

>[!NOTE]
>
>ここで説明する機能は、[コアコンポーネントのリリース 1.1.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) 以降のすべてのコンポーネントで使用できます。

## コンテンツフラグメントコアコンポーネントを使用した JSON エクスポーター {#json-exporter-with-content-fragment-core-components}

AEM JSON エクスポーターを使用して、任意のAEMページのコンテンツを JSON データモデル形式で配信できます。 その後、このメソッドは、独自のアプリケーションで使用できます。

AEM内では、セレクターを使用して配信をおこないます `model` および `.json` 拡張子。

`.model.json`

1. 例えば、次のような URL があります。

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. 次のようなコンテンツを配信します。

   ![chlimage_1-192](assets/chlimage_1-192.png)

代わりに、構造化コンテンツフラグメントのコンテンツを、ターゲット設定して配信することもできます。

フラグメントへのパス全体を ( `jcr:content`);例えば、のようなサフィックスを付けます。

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

ページには、1 つのコンテンツフラグメントを含めることも、様々なタイプの複数のコンポーネントを含めることもできます。 また、リストコンポーネントなどのメカニズムを使用して、関連するコンテンツを自動的に検索することもできます。

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

   * [Sling モデル — 130 以降のモデルクラスとリソースタイプの関連付け](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM with JSON:

   * [JSON 形式でページ情報を取得](/help/sites-developing/pageinfo.md)

## 関連ドキュメント {#related-documentation}

詳しくは、以下を参照してください。

* [Assets ユーザーガイドのコンテンツフラグメントに関するトピック](https://experienceleague.adobe.com/docs/experience-manager-64/assets/home.html?lang=en&amp;topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
* [コンテンツフラグメントを使用したオーサリング](/help/sites-authoring/content-fragments.md)
* [コンポーネントの JSON エクスポートを有効化](/help/sites-developing/json-exporter-components.md)

* [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)および[コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=en)
