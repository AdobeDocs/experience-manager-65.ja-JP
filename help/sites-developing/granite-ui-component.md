---
title: 新しい Granite UI フィールドコンポーネントの作成
seo-title: 新しい Granite UI フィールドコンポーネントの作成
description: Granite UI には、「フィールド」と呼ばれる、フォームで使用するようにデザインされた幅広いコンポーネントが用意されています
seo-description: Granite UI には、「フィールド」と呼ばれる、フォームで使用するようにデザインされた幅広いコンポーネントが用意されています
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 89%

---


# 新しい Granite UI フィールドコンポーネントの作成{#creating-a-new-granite-ui-field-component}

Granite UI には、フォームで使用するようにデザインされた幅広いコンポーネントが用意されています。これらを Granite の UI 用語では「フィールド」と呼びます。**&#x200B;標準の Granite フォームコンポーネントは、次の場所にあります。

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>これらの Granite UI フォームフィールドが特に注目されるのは、これらが[コンポーネントダイアログ](/help/sites-developing/developing-components.md)で使用されるからです。

>[!NOTE]
>
>フィールドについて詳しくは、[Granite UI に関するドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)を参照してください。

Granite コンポーネントを開発または拡張するには、Granite UI の基盤フレームワークを使用します。このフレームワークには次の 2 つの要素があります。

* サーバー側：

   * 基盤コンポーネントのコレクション

      * 基盤 - モジュール式、組み立て可能、階層化可能、再利用可能
      * コンポーネント - Sling コンポーネント
   * アプリケーション開発を支援するためのヘルパー


* クライアント側：

   * ハイパーメディア駆動型 UI を使用して一般的なインタラクションパターンを実現するための語彙（HTML 言語の拡張）を提供するクライアントライブラリのコレクション

The generic Granite UI component `field` is composed of two files of interest:

* `init.jsp`：ラベル付けや説明などの一般的な処理を扱い、フィールドをレンダリングする際に必要になるフォーム値を提供します。
* `render.jsp`：フィールドの実際のレンダリングを実行します。カスタムフィールドに対してはオーバーライドされます。`init.jsp` にインクルードされます。

詳しくは、[Granite UI に関するドキュメント - フィールド](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html)を参照してください。

例えば、次を参照してください。

* `cqgems/customizingfield/components/colorpicker`

   * [コードサンプル](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)で提供

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>このメカニズムは JSP を使用しているので、i18n および XSS はデフォルトでは提供されません。つまり、文字列を国際化およびエスケープする必要があります。以下のディレクトリには、標準インスタンスの一般的なフィールドが含まれています。これらをリファレンスとして使用できます。
>
>`/libs/granite/ui/components/foundation/form` で

## コンポーネント用のサーバー側スクリプトの作成 {#creating-the-server-side-script-for-the-component}

カスタマイズしたフィールドは、`render.jsp` スクリプトのみをオーバーライドする必要があります。このスクリプトは、コンポーネントのマークアップを提供します。この JSP（レンダリングスクリプト）は、マークアップのラッパーと見なすことができます。

1. `sling:resourceSuperType` プロパティを使用して、以下から継承する新しいコンポーネントを作成します。

   `/libs/granite/ui/components/foundation/form/field`

1. 次のスクリプトをオーバーライドします。

   `render.jsp`

   このスクリプトでは、クライアントが生成された要素とやり取りする方法を理解できるように、ハイパーメディアマークアップ（ハイパーメディアアフォーダンスを含む、拡張されたマークアップ）を生成する必要があります。Granite UI のサーバー側コーディングスタイルに従ってください。

   カスタマイズする際に守るべき唯一の決まり事は&#x200B;**、以下を使用して、リクエストからフォーム値（`init.jsp` で初期化）を読み取ることです。

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   For more details, please refer to the implementation of out-ot-the-box Granite UI fields; for example, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >現時点では、HTL ではコンポーネント間の情報の受け渡し（フォーム／フィールドのコンテキストでは非常に頻繁におこなわれます）を簡単には実現できないので、スクリプティングメソッドとして JSP が推奨されます。

## コンポーネント用のクライアントライブラリの作成 {#creating-the-client-library-for-the-component}

特定のクライアント側動作をコンポーネントに追加するには：

1. カテゴリ `cq.authoring.dialog` のクライアントライブラリを作成します。
1. Create a clientlib of category `cq.authoring.dialog` and define your `JS`/ `CSS` inside it.

   Define your `JS`/ `CSS` inside the clientlib.

   >[!NOTE]
   >
   >現時点では、Granite UI には、JS 動作を追加するために直接使用できるデフォルトのリスナーやフックはありません。そのため、JS 動作をコンポーネントに追加するには、JS フックをカスタムクラスに実装して、マークアップの生成時にコンポーネントに割り当てる必要があります。

