---
title: オーバーレイ
seo-title: オーバーレイ
description: AEM は、オーバーレイという原理を利用して、開発者がコンソールおよびその他の機能を拡張し、カスタマイズできるようにします
seo-description: AEM は、オーバーレイという原理を利用して、開発者がコンソールおよびその他の機能を拡張し、カスタマイズできるようにします
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 64%

---


# オーバーレイ{#overlays}

AEM（旧称 CQ）は、以前からオーバーレイという原理を利用して、開発者が[コンソール](/help/sites-developing/customizing-consoles-touch.md)およびその他の機能（[ページオーサリング](/help/sites-developing/customizing-page-authoring-touch.md)など）を拡張し、カスタマイズできるようにしてきました。

オーバーレイは様々なコンテキストで使用される用語です。このコンテキスト（AEM の拡張）では、オーバーレイとは、「事前定義済みの機能に対して独自の定義を強制的に付加する（標準の機能をカスタマイズする）こと」を表します。

標準インスタンスでは、定義済みの機能は`/libs`の下に保持され、`/apps`ブランチの下にオーバーレイ（カスタマイズ）を定義することをお勧めします。 AEMは、リソースを検索するために検索パスを使用し、最初に`/apps`ブランチを検索し、次に`/libs`ブランチを検索します（[検索パスは](#configuring-the-search-paths)に設定できます）。 このメカニズムにより、オーバーレイ（およびそこに定義されているカスタマイズ）が優先されることになります。

AEM 6.0 以降、オーバーレイの実装方法と使用方法が次のように変更されました。

* AEM 6.0 以降 - [Granite](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 関連のオーバーレイ（つまりタッチ操作対応 UI）

   * 方法

      * `/apps` の下に適切な `/libs` 構造を再構築します。

         これは1:1のコピーを必要としません。[Sling Resource Marger](/help/sites-developing/sling-resource-merger.md)は、必要な元の定義を相互参照するために使用されます。 Sling Resource Merger は、差分メカニズムによってリソースにアクセスおよびマージするためのサービスを提供します。

      * 変更は `/apps` 以下でおこないます。
   * メリット

      * `/libs` 以下の変更に対する堅牢性が高まります。
      * 実際に必要な項目のみを再定義できます。


* Granite 以外によるオーバーレイおよび AEM 6.0 より前のバージョンでのオーバーレイ

   * メソッド

      * `/libs`から`/apps`にコンテンツをコピー

         プロパティを含むサブブランチ全体をコピーする必要があります。

      * 変更は `/apps` 以下でおこないます。
   * デメリット

      * `/libs`の下で何かが変更されても変更は失われませんが、`/apps`の下でオーバーレイで発生する特定の変更を再作成する必要がある場合があります。


>[!CAUTION]
>
>[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) および関連する手法は、[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) と併用する場合に限り使用できます。つまり、オーバーレイをスケルトン構造で作成する方法は、標準のタッチ操作対応 UI でのみ使用できます。
>
>他の領域（クラシック UI など）でのオーバーレイには、該当するノードとサブ構造全体をコピーして、必要な変更を加えます。

オーバーレイは、[コンソールの設定](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)、[サイドパネル内にあるアセットブラウザーへの選択カテゴリの作成](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser)（ページのオーサリング時に使用）など、多くの変更において推奨される方法です。オーバーレイは、次の理由で必要になります。

* ****&#x200B;は`/libs`ブランチ&#x200B;**に変更を加えてはなりません
次の操作を行うと、このブランチが変更される可能性があるので、行った変更はすべて失われる可能性があります。

   * インスタンス上のアップグレード
   * ホットフィックスの適用
   * 機能パックのインストール

* オーバーレイにより、変更を 1 箇所に集中させることができます。そのため、必要に応じて変更の追跡、移行、バックアップ、デバッグを実行しやすくなります。

## 検索パスの設定  {#configuring-the-search-paths}

オーバーレイの場合、配信されるリソースは、取得されたリソースとプロパティの集合体で、定義可能な以下の検索パスに応じます。

* **OSGi 設定**&#x200B;で [Apache Sling Resource Resolver Factory](/help/sites-deploying/configuring-osgi.md) 用に定義された、リソースの **Resolver Search Path**。

   * 検索パスの順序は、上から下の順で、それぞれの優先順位を示します。
   * 標準インストールでは、主なデフォルトは`/apps`, `/libs`です。したがって、`/apps`の内容は`/libs`の内容よりも高い優先度を持ちます（つまり、*overlays*&#x200B;です）。

* 2人のサービスユーザーは、スクリプトが保存されている場所へのJCR:READアクセス権が必要です。 これらのユーザーは、components-search-service(com.day.cq.wcm.coreto access/cacheコンポーネントで使用)およびsling-scripting（org.apache.sling.servlets.resolverでサーブレットを検索するために使用）。
* 次の設定も、スクリプトの配置場所に応じて設定する必要があります（この例では/etc、/libs、または/appsの下）。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最後に、サーブレットリゾルバーも設定する必要があります（この例では/etcも追加します）。

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 使用例 {#example-of-usage}

以下のページで、一部の例が紹介されています。

* [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)
* [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)

