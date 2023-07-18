---
title: 新しい Granite UI フィールドコンポーネントの作成
description: Granite UI は、フィールドと呼ばれる、フォームで使用するように設計された様々なコンポーネントを提供します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: 26c0411d6cc16f4361cfa9e6b563eba0bfafab1e
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 26%

---

# 新しい Granite UI フィールドコンポーネントの作成{#creating-a-new-granite-ui-field-component}

Granite UI には、フォームで使用するようにデザインされた幅広いコンポーネントが用意されています。これらを Granite の UI 用語では「フィールド」と呼びます&#x200B;*。*&#x200B;標準の Granite フォームコンポーネントは、次の場所で使用できます。

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>これらの Granite UI フォームフィールドは、 [コンポーネントダイアログ](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>フィールドについて詳しくは、 [Granite UI ドキュメント](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Granite UI Foundation フレームワークを使用して、Granite コンポーネントを開発または拡張します。 これには次の 2 つの要素があります。

* サーバー側：

   * 基盤コンポーネントのコレクション

      * 基盤 — モジュラー型、合成可能、レイヤブル、再利用可能
      * コンポーネント - Sling コンポーネント

   * アプリケーション開発を支援するヘルパー

* クライアント側：

   * ハイパーメディア駆動型のユーザーインターフェイスを通じて一般的なインタラクションパターンを実現するための語彙 (HTML言語の拡張 ) を提供する clientlibs のコレクション。

一般的な Granite UI コンポーネントである `field` は、以下の 2 つのファイルで構成されています。

* `init.jsp`:は一般的な処理を処理します。ラベル付け、説明、およびフィールドのレンダリング時に必要となるフォーム値の提供。
* `render.jsp`:ここで、フィールドの実際のレンダリングが実行されます。カスタムフィールドに対して上書きする必要があります。次に含まれる `init.jsp`.

詳しくは、 [Granite UI ドキュメント — フィールド](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) 」を参照してください。

詳しくは、例えば、以下を参照してください。

* `cqgems/customizingfield/components/colorpicker`

   * [コードサンプル](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)で提供

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>このメカニズムは JSP を使用するので、i18n と XSS は標準では提供されません。 つまり、文字列を国際化してエスケープする必要があります。 次のディレクトリには、標準インスタンスの汎用フィールドが含まれています。これらを参照として使用できます。
>
>`/libs/granite/ui/components/foundation/form` ディレクトリ

## コンポーネント用のサーバーサイドスクリプトの作成 {#creating-the-server-side-script-for-the-component}

カスタマイズしたフィールドは、`render.jsp` スクリプトのみを上書きする必要があります。このスクリプトは、コンポーネントのマークアップを提供します。JSP （つまり、レンダリングスクリプト）はマークアップのラッパーと見なすことができます。

1. を使用するコンポーネントを作成する `sling:resourceSuperType` 継承元のプロパティ：

   `/libs/granite/ui/components/foundation/form/field`

1. 以下のスクリプトを上書きします。

   `render.jsp`

   このスクリプトでは、ハイパーメディアマークアップ（つまり、ハイパーメディアアフォーダンスを含む、エンリッチメントされたマークアップ）を生成し、生成された要素の操作方法をクライアントが把握できるようにします。 これは、Granite UI のサーバー側のコーディングスタイルに従う必要があります。

   カスタマイズする際に守る必要のある唯一の&#x200B;*決まりごと*&#x200B;は、以下を使用して、リクエストからフォーム値（`init.jsp` で初期化）を読み取ることです。

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   詳しくは、標準搭載の Granite UI フィールドの実装を参照してください。例： `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >現時点では、JSP が推奨されるスクリプティングメソッドです。HTL では、あるコンポーネントから別のコンポーネントに情報を渡すことは（フォームやフィールドのコンテキストで頻繁に行われます）容易には実現できません。

## コンポーネントのクライアントライブラリの作成 {#creating-the-client-library-for-the-component}

特定のクライアント側の動作をコンポーネントに追加するには：

1. カテゴリ `cq.authoring.dialog` のクライアントライブラリを作成します。
1. カテゴリ `cq.authoring.dialog` のクライアントライブラリを作成し、その内部に `JS`／`CSS` を定義します。

   クライアントライブラリの内部に `JS`／`CSS` を定義します。

   >[!NOTE]
   >
   >現時点では、Granite UI には、JS 動作を直接追加するために使用できる、標準のリスナーやフックは用意されていません。 そのため、コンポーネントに JS 動作を追加するには、JS フックをカスタムクラスに実装し、マークアップの生成中にコンポーネントに割り当てる必要があります。
