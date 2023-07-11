---
title: 高度な URL 設定
description: 製品ページとカテゴリページの URL をカスタマイズする方法について説明します。このカスタマイズにより、実装で URL を検索エンジン向けに最適化し、検出を促進できます。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 64%

---

# 高度な URL 設定 {#url}

>[!NOTE]
>
>検索エンジン最適化（SEO）は、多くのマーケターにとって重要な課題となっています。そのため、多くの AEM プロジェクトで SEO 対策に取り組む必要があります。詳しくは、 [SEO および URL 管理のベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html?lang=ja) を参照してください。

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、製品ページとカテゴリページの URL をカスタマイズする高度な設定を提供します。多くの実装では、検索エンジン最適化 (SEO) 用にこれらの URL をカスタマイズしています。 次のビデオでは、`UrlProvider` サービスと [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)の機能を設定して、製品ページとカテゴリページの URL をカスタマイズする方法について詳しく説明します。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

次の手順で `UrlProvider` SEO 要件と必要に応じて、サービスで「CIF URL Provider configuration」の OSGI 設定をプロジェクトで提供する必要があります。

>[!NOTE]
>
>AEM CIF コアコンポーネントのリリース 2.0.0 以降、URL プロバイダー設定では、1.x リリースで知られているフリーテキスト設定可能な形式の代わりに、事前に定義された URL 形式のみが提供されます。 さらに、セレクターを使用して URL 内のデータを渡すことはなくなり、代わりにサフィックスが使用されます。

### 製品ページの URL 形式 {#product}

製品ページの URL を設定するもので、次のオプションをサポートしています。

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（デフォルト）
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)の場合は次のとおりです。

* `{{page}}` は、 `/content/venia/us/en/products/product-page`
* `{{sku}}` が製品の SKU に置き換えられている（例： ） `VP09`
* `{{url_key}}` は製品の `url_key` プロパティ。例： `lenora-crochet-shorts`
* `{{url_path}}` は製品の `url_path`例： `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` は、現在選択されているバリアントに置き換えられます（例： ）。 `VP09-KH-S`

以降 `url_path` 廃止されました。事前定義済みの製品 URL 形式では、製品の `url_rewrites` を選択し、最も多くのパスセグメントを持つセグメントを、 `url_path` は使用できません。

上記の例のデータでは、デフォルトの URL 形式を使用して書式設定された製品バリアント URL は次のようになります。 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### カテゴリページの URL 形式 {#product-list}

カテゴリページまたは製品リストページの URL を設定するもので、次のオプションをサポートしています。

* `{{page}}.html/{{url_path}}.html`（デフォルト）
* `{{page}}.html/{{url_key}}.html`

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)の場合は次のとおりです。

* `{{page}}` は、 `/content/venia/us/en/products/category-page`
* `{{url_key}}` はカテゴリの `url_key` プロパティ
* `{{url_path}}` はカテゴリの `url_path`

上記の例のデータでは、デフォルトの URL 形式を使用して書式設定されたカテゴリページの URL は次のようになります。 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
>`url_path` は、製品またはカテゴリの上位層の `url_keys` と製品またはカテゴリの `url_key` をスラッシュ `/` で区切って連結したものです。

### 特定のカテゴリーページ／製品ページ {#specific-pages}

次を作成できます。 [複数のカテゴリおよび製品ページ](multi-template-usage.md) カタログの特定のカテゴリまたは製品のサブセットのみ。

`UrlProvider` は、そのようなページへのディープリンクをオーサー層インスタンスで生成するように事前に設定されています。 これは、編集者がプレビューモードでサイトを閲覧し、特定の製品ページまたはカテゴリーページに移動したあと編集モードに切り替えてページを編集する場合に便利な機能です。

一方、パブリッシュ層インスタンスでは、例えば検索エンジンのランキングを落とさないように、カタログページの URL を安定した状態に保つ必要があります。そのため、パブリッシュ層インスタンスは、デフォルトでは特定のカタログページへのディープリンクをレンダリングしません。 この動作を変更するには、 _CIF URL プロバイダー固有のページ戦略_ は、常に特定のページ url を生成するように設定できます。

## カスタム URL 形式 {#custom-url-format}

プロジェクトで実装できるカスタム URL 形式を指定するには、 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) または [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) サービスインターフェイスを使用し、実装を OSGi サービスとして登録します。 これらの実装が存在する場合は、設定済みの事前定義済み形式を置き換えます。 複数の実装が登録されている場合、サービスランキングが高い実装は、低いサービスランキングの実装に置き換えられます。

カスタム URL 形式の実装では、指定されたパラメーターから URL を作成するメソッドと URL を解析して同じパラメーターを返すメソッドのペアを実装する必要があります。

## Sling マッピングとの結合 {#sling-mapping}

また、 `UrlProvider`を使用する場合、 [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) を使用して、URL を書き換え、処理します。 AEM Archetype プロジェクトには、 [サンプル設定](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) ポート 4503（パブリッシュ）および 80(Dispatcher) の一部の Sling マッピングを設定する場合。

## AEM Dispatcher との統合 {#dispatcher}

URL の書き換えは、`mod_rewrite` モジュールを備えた AEM Dispatcher HTTP サーバーを使用して実行することもできます。[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype) は、既に生成されたサイズに対する基本的な [書き換えルール](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) が含まれている、参照用 AEM Dispatcher 設定を提供します。

## 例

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトには、製品ページとカテゴリページでのカスタム URL を使用方法を示す設定例が含まれています。これにより、各プロジェクトで、SEO のニーズに応じて、製品ページとカテゴリページの個々の URL パターンを設定できます。上記の CIF `UrlProvider` と Sling マッピングの組み合わせが使用されます。

>[!NOTE]
>
>この設定は、プロジェクトで使用する外部ドメインで調整する必要があります。Sling マッピングは、ホスト名とドメインに基づいて動作します。したがって、この設定はデフォルトで無効になっており、デプロイ前に有効にする必要があります。これを行うには、使用されているドメイン名に従って `ui.content/src/main/content/jcr_root/etc/map.publish/https` の Sling マッピング `hostname.adobeaemcloud.com` フォルダーの名前を変更し、`resource.resolver.map.location="/etc/map.publish"` をプロジェクトの `JcrResourceResolver` 設定に追加してこの設定を有効にします。

## その他のリソース

* [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [AEM リソースマッピング](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html?lang=ja)
* [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
