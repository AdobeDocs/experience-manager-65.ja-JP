---
title: コンポーネントの JSON 書き出しの有効化
seo-title: コンポーネントの JSON 書き出しの有効化
description: モデラーフレームワークに基づいてコンテンツの JSON 書き出しを生成するように、コンポーネントを適応させることができます。
seo-description: モデラーフレームワークに基づいてコンテンツの JSON 書き出しを生成するように、コンポーネントを適応させることができます。
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 98%

---


# コンポーネントの JSON 書き出しの有効化{#enabling-json-export-for-a-component}

モデラーフレームワークに基づいてコンテンツの JSON 書き出しを生成するように、コンポーネントを適応させることができます。

## 概要 {#overview}

JSON 書き出しは、[Sling Model](https://sling.apache.org/documentation/bundles/models.html) と [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) フレームワーク（それ自体が [Jackson 注釈](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)に依存）に基づいています。

つまり、JSON を書き出す必要がある場合、コンポーネントには Sling Model が必要です。そのため、次の 2 つの手順に従って、コンポーネントで JSON 書き出しを有効にする必要があります。

* [コンポーネントに Sling Model を定義する](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Sling Model インターフェイスに注釈を付ける](#annotate-the-sling-model-interface)

## コンポーネントに Sling Model を定義する     {#define-a-sling-model-for-the-component}

まず、コンポーネントに Sling Model を定義する必要があります。

>[!NOTE]
>
>Sling Model の使用例については、[AEM での Sling Model Exporter の開発](https://helpx.adobe.com/jp/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html)の記事を参照してください。

Sling Model の実装クラスに次のような注釈を付ける必要があります。

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

これにより、`.model` セレクターと `.json` 拡張子を使用して、コンポーネントをそれ自体に書き出すことができます。

さらに、Sling Model クラスが `ComponentExporter` インターフェイスに適応できるように指定されます。

>[!NOTE]
>
>Jackson 注釈は通常 Sling Model クラスレベルではなく、Model インターフェイスレベルで指定されます。これは、JSON 書き出しがコンポーネント API の一部とみなされるようにするためです。

>[!NOTE]
>
>`ExporterConstants` クラスと `ComponentExporter` クラスは `com.adobe.cq.export.json` バンドルから取得されます。

### 複数のセレクターの使用 {#multiple-selectors}

標準的なユースケースではありませんが、`model` セレクターに加えて複数のセレクターを設定することができます。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

ただし、その場合は、`model` セレクターを最初のセレクターにし、拡張子を `.json` にする必要があります。

## Sling Model インターフェイスに注釈を付ける {#annotate-the-sling-model-interface}

JSON エクスポーターフレームワークで認識されるようにするには、モデルインターフェイスに `ComponentExporter` インターフェイス（またはコンテナコンポーネントの場合は `ContainerExporter`）を実装する必要があります。

対応する Sling Model インターフェイス（`MyComponent`）には、[Jackson 注釈](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)を使用して注釈が付けられ、どのように書き出し（シリアル化）がおこなわれるかが定義されます。

Model インターフェイスには、シリアル化されるメソッドを定義するために適切に注釈を付ける必要があります。デフォルトでは、getter の通常の命名規則に準拠するすべてのメソッドがシリアル化され、JSON プロパティ名が getter 名からそのまま派生されます。これを回避または上書きするには、`@JsonIgnore` または `@JsonProperty` を使用して JSON プロパティの名前を変更します。

## 例 {#example}

コアコンポーネントでは、JSON 書き出しが[コアコンポーネントのリリース 1.1.0](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html) からサポートされており、参照として使用できます。

例えば、画像コアコンポーネントの Sling Model 実装とその注釈されたインターフェイスを参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-core-wcm-components プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)としてダウンロードします

## 関連ドキュメント {#related-documentation}

詳しくは、以下を参照してください。

* [Assets ユーザーガイドのコンテンツフラグメントに関するトピック](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
* [コンテンツフラグメントを使用したオーサリング](/help/sites-authoring/content-fragments.md)
* [コンテンツサービス用の JSON エクスポーター](/help/sites-developing/json-exporter.md)
* [コアコンポーネント](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)および[コンテンツフラグメントコンポーネント](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

