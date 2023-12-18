---
title: オーバーレイ
description: Adobe Experience Manager は、オーバーレイという原則を利用して、コンソールおよびその他の機能を拡張し、カスタマイズできるようにします。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: ht
source-wordcount: '604'
ht-degree: 100%

---

# オーバーレイ{#overlays}

Adobe Experience Manager（AEM）（旧称 CQ）は、以前からオーバーレイという原則を利用して、[コンソール](/help/sites-developing/customizing-consoles-touch.md)およびその他の機能（[ページオーサリング](/help/sites-developing/customizing-page-authoring-touch.md)など）を拡張し、カスタマイズできるようにしてきました。

オーバーレイは様々なコンテキストで使用される用語です。このコンテキスト（AEM の拡張）では、オーバーレイとは、事前定義された機能を取得し、（標準機能をカスタマイズするため）その上に独自の定義を適用することを意味します。

標準インスタンスでは、事前定義された機能は `/libs` に保持されるので、オーバーレイは `/apps` ブランチに定義（カスタマイズ）することが推奨されます。AEM がリソースを見つけるために検索するパスは、最初に `/apps` ブランチを検索し、次に `/libs` ブランチを検索します（[検索パスは必要に応じて設定可能](#configuring-the-search-paths)）。このメカニズムにより、オーバーレイ（およびそこに定義されているカスタマイズ）が優先されることになります。

AEM 6.0 以降、オーバーレイの実装方法と使用方法が以下のように変更されました。

* AEM 6.0 以降 - [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) に関連するオーバーレイ（つまり、タッチ操作対応 UI）

   * 方法

      * `/apps` の下に適切な `/libs` 構造を再構築します。

        これには 1:1 のコピーは不要です。[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) は、必要な元の定義を相互参照するために使用されるからです。Sling Resource Merger は、差分メカニズムによってリソースにアクセスおよびマージするサービスを提供します。

      * `/apps` の下に、変更を加えます。

   * メリット

      * `/libs` 以下の変更に対する堅牢性が高まります。
      * 必須項目のみを再定義します。

* Granite 以外によるオーバーレイおよび AEM 6.0 より前のオーバーレイ

   * メソッド

      * コンテンツを `/libs` から `/apps` にコピーします。

        プロパティを含め、サブブランチ全体をコピーします。

      * `/apps` の下に、変更を加えます。

   * デメリット

      * `/libs` 以下で変更しても変更内容は失われませんが、`/apps` 以下のオーバーレイでは一部の変更作業をやり直す必要がある場合があります。

>[!CAUTION]
>
>[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) および関連する手法は、[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) と併用する場合に限り使用できます。つまり、オーバーレイをスケルトン構造で作成する方法は、標準のタッチ操作対応 UI にのみ適しています。
>
>他のエリア（クラシック UI を含む）のオーバーレイでは、適切なノードとサブ構造全体をコピーし、必要な変更を加えます。

オーバーレイは、[コンソールの設定](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)、[サイドパネル内にあるアセットブラウザーへの選択カテゴリの作成](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser)（ページのオーサリング時に使用）など、多くの変更において推奨される方法です。オーバーレイは、次の理由で必要になります。

* `/libs` ブランチ&#x200B;**では変更&#x200B;***しないこと*
このブランチは以下のことを実行するたびに変更される可能性があるため、行った変更が失われる可能性があります。

   * インスタンスをアップグレード
   * ホットフィックスを適用
   * 機能パックをインストール

* オーバーレイにより、変更を 1 個所に集中させるため、必要に応じて変更の追跡、移行、バックアップまたはデバッグを実行しやすくなります。

## 検索パスの設定 {#configuring-the-search-paths}

オーバーレイの場合、配信されるリソースは、取得されたリソースとプロパティの集計で、定義可能な以下の検索パスに応じます。

* [OSGi 設定](/help/sites-deploying/configuring-osgi.md)で **Apache Sling Resource Resolver Factory** 用に定義された、リソースの **リゾルバー検索パス**。

   * 検索パスの順序は、上から下の順で、それぞれの優先順位を示します。
   * 標準インストールの場合、主なデフォルトは `/apps` と `/libs` で、`/apps` のコンテンツの方が `/libs` のコンテンツより優先されます（つまり、前者が後者を&#x200B;*オーバーレイ*&#x200B;します）。

* スクリプトの保存場所への JCR:READ アクセス権を 2 人のサービスユーザーに付与する必要があります。この 2 人のユーザーは、components-search-service（com.day.cq.wcm.core でコンポーネントのアクセス／キャッシュに使用）と sling-scripting（org.apache.sling.servlets.resolver でサーブレットの検索に使用）です。
* 次の設定も、スクリプトの保存場所に応じて設定する必要があります（この例では /etc、/libs または /apps の下）。

  ```
  PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
  resource.resolver.searchpath=["/etc","/apps","/libs"]
  resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
  ```

* 最後に、サーブレットリゾルバーを設定する必要もあります（この例では /etc も追加します）。

  ```
  PID = org.apache.sling.servlets.resolver.SlingServletResolver
  servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
  ```

## 使用例 {#example-of-usage}

いくつかの例は、以下の場合に取り上げられます。

* [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)
* [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)
