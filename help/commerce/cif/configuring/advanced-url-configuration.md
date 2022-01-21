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
source-git-commit: 014731aa9c5c4d7d419ff8b037142b47e7b7da01
workflow-type: ht
source-wordcount: '910'
ht-degree: 100%

---

# 高度な URL 設定 {#url}

>[!NOTE]
>
> 検索エンジン最適化（SEO）は、多くのマーケティング担当者にとって重要な課題となっています。したがって、多くの AEM プロジェクトで SEO に関する課題に対処する必要があります。詳しくは、[SEO および URL 管理のベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html?lang=ja)を参照してください。

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、製品ページとカテゴリページの URL をカスタマイズする高度な設定を提供します。多くの実装では、検索エンジン最適化（SEO）用にこれらの URL をカスタマイズします。次のビデオでは、`UrlProvider` サービスと [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)の機能を設定して、製品ページとカテゴリページの URL をカスタマイズする方法について詳しく説明します。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 設定 {#configuration}

SEO の要件とニーズに応じて `UrlProvider` サービスを設定するには、プロジェクトで「CIF URL Provider configuration」の OSGI 設定を指定する必要があります。

>[!NOTE]
>
> AEM CIF コアコンポーネントのリリース 2.0.0 以降では、URL プロバイダーの設定には、1.x リリースで提供されていた設定可能なフリーテキスト形式ではなく、事前に定義された URL 形式のみが使用されます。さらに、セレクターを使用して URL 内のデータを渡すことはなくなり、代わりにサフィックスが使用されます。

### 製品ページの URL 形式 {#product}

製品ページの URL を設定するもので、次のオプションをサポートしています。

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（デフォルト）
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)の場合は次のとおりです。

* `{{page}}` は `/content/venia/us/en/products/product-page` に置き換えられます
* `{{sku}}` は製品の SKU（例：`VP09`）に置き換えられます
* `{{url_key}}` は製品の `url_key` プロパティ（例：`lenora-crochet-shorts`）に置き換えられます
* `{{url_path}}` は製品の `url_path`（例：`venia-bottoms/venia-pants/lenora-crochet-shorts`）に置き換えられます
* `{{variant_sku}}` は、現在選択されているバリアント（例：`VP09-KH-S`）に置き換えられます

`url_path` が非推奨になったため、あらかじめ定義された製品のURLフォーマットは製品の `url_rewrites` を使用し、`url_path` が利用できない場合は最もパスセグメントが多いものを代替手段として選択します。

上記のサンプルデータでは、デフォルトの URL 形式を使用して設定された製品バリアント URL は `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S` のようになります。

### カテゴリページの URL 形式 {#product-list}

カテゴリページまたは製品リストページの URL を設定するもので、次のオプションをサポートしています。

* `{{page}}.html/{{url_path}}.html`（デフォルト）
* `{{page}}.html/{{url_key}}.html`

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)の場合は次のとおりです。

* `{{page}}` は `/content/venia/us/en/products/category-page` に置き換えられます
* `{{url_key}}` はカテゴリの `url_key` プロパティに置き換えられます
* `{{url_path}}` はカテゴリの `url_path` に置き換えられます

上記のサンプルデータでは、デフォルトの URL 形式を使用して設定されたカテゴリページ URL は `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html` のようになります。

>[!NOTE]
> 
> `url_path` は、製品またはカテゴリの上位層の `url_keys` と製品またはカテゴリの `url_key` をスラッシュ `/` で区切って連結したものです。

### 特定のカテゴリーページ／製品ページ {#specific-pages}

カタログのカテゴリーまたは製品の特定のサブセットに対してのみ、[複数のカテゴリーページおよび製品ページ](multi-template-usage.md)を作成することができます。

`UrlProvider` は、そのようなページへのディープリンクをオーサー層インスタンスで生成するように事前に設定されています。 これは、編集者がプレビューモードでサイトを閲覧し、特定の製品ページまたはカテゴリーページに移動したあと編集モードに切り替えてページを編集する場合に便利な機能です。

一方、パブリッシュ層インスタンスでは、例えば検索エンジンのランキングを落とさないように、カタログページの URL を安定した状態に保つ必要があります。そのため、パブリッシュ層インスタンスは、デフォルトでは特定のカタログページへのディープリンクをレンダリングしません。 この動作を変更するには、常に特定のページの URL を生成するように _CIF URL プロバイダー固有のページ戦略_&#x200B;を設定します。

## カスタム URL 形式 {#custom-url-format}

カスタム URL 形式を指定するには、プロジェクトで [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) または [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) サービスインターフェイスを実装し、その実装を OSGi サービスとして登録します。 これらの実装が用意されている場合は、設定されている事前定義済み形式の代わりに、その実装が使用されます。 複数の実装が登録されている場合は、サービスランキングの高い実装が、サービスランキングの低い実装と入れ替わります。

カスタム URL 形式の実装では、指定されたパラメーターから URL を作成するメソッドと URL を解析して同じパラメーターを返すメソッドのペアを実装する必要があります。

## Sling マッピングとの結合 {#sling-mapping}

`UrlProvider` に加え、URL の書き換えと処理を行うために、[Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)を設定することもできます。AEM アーキタイププロジェクトでは、ポート 4503（パブリッシュ）および 80（ディスパッチャー）の Sling マッピングを設定する[設定例](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)も提供されています。

## AEM Dispatcher との統合 {#dispatcher}

URL の書き換えは、AEM Dispatcher HTTP サーバーで `mod_rewrite` モジュールを使用して行うこともできます。[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)には、生成されたサイズに対する基本的な[書き換えルール](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)が含まれている参照用 AEM Dispatcher 設定が用意されています。

## 例

[Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)プロジェクトには、製品ページとカテゴリページでのカスタム URL を使用方法を示す設定例が含まれています。これにより、各プロジェクトで、SEO のニーズに応じて、製品ページとカテゴリページの個々の URL パターンを設定できます。上記の CIF `UrlProvider` と Sling マッピングの組み合わせが使用されます。

>[!NOTE]
>
>この設定は、プロジェクトで使用する外部ドメインで調整する必要があります。Sling マッピングは、ホスト名とドメインに基づいて動作します。したがって、この設定はデフォルトで無効になっており、デプロイ前に有効にする必要があります。これを行うには、使用されているドメイン名に従って `ui.content/src/main/content/jcr_root/etc/map.publish/https` の Sling マッピング `hostname.adobeaemcloud.com` フォルダーの名前を変更し、`resource.resolver.map.location="/etc/map.publish"` をプロジェクトの `JcrResourceResolver` 設定に追加してこの設定を有効にします。

## その他のリソース

* [Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
* [AEM リソースマッピング](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html?lang=ja)
* [Sling マッピング](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
