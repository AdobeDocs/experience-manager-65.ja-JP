---
title: オーバーレイ
description: Adobe Experience Managerは、オーバーレイの原則を使用して、コンソールやその他の機能を拡張およびカスタマイズできます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 36%

---

# オーバーレイ{#overlays}

Adobe Experience Manager(AEM)（以前は CQ）は、長い間、オーバーレイの原則を使用して、 [コンソール](/help/sites-developing/customizing-consoles-touch.md) その他の機能 ( 例： [ページオーサリング](/help/sites-developing/customizing-page-authoring-touch.md)) をクリックします。

オーバーレイは、多くのコンテキストで使用される用語です。 このコンテキスト (AEMの拡張 ) では、オーバーレイとは、事前定義された機能を使用し、それに対して独自の定義を課す（標準の機能をカスタマイズする）ことです。

標準インスタンスでは、事前定義された機能は、 `/libs` オーバーレイ（カスタマイズ）は、 `/apps` 分岐。 AEM がリソースを検索するときは検索パスを使用します。具体的には、最初に `/apps` ブランチを検索し、次に `/libs` ブランチを検索します（[検索パスは必要に応じて設定可能](#configuring-the-search-paths)）。このメカニズムにより、オーバーレイ（およびそこに定義されているカスタマイズ）が優先されます。

AEM 6.0 以降、オーバーレイの実装方法と使用方法が変更されました。

* AEM 6.0 以降 — 用 [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)関連するオーバーレイ（つまり、タッチ操作対応 UI）

   * 方法

      * `/apps` の下に適切な `/libs` 構造を再構築します。

        これには 1:1 のコピーは不要です。[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) は、必要な元の定義を相互参照するために使用されるからです。Sling Resource Merger は、差分（差分）メカニズムを使用してリソースにアクセスし、マージするためのサービスを提供します。

      * の下 `/apps`、変更を加えます。

   * メリット

      * `/libs` 以下の変更に対する堅牢性が高まります。
      * 必要な項目のみを再定義できます。

* AEM 6.0 より前の Granite 以外のオーバーレイとオーバーレイ

   * メソッド

      * コンテンツを `/libs` から `/apps` にコピーします。

        プロパティを含め、サブブランチ全体をコピーします。

      * の下 `/apps`、変更を加えます。

   * デメリット

      * `/libs` 以下で変更しても変更内容は失われませんが、`/apps` 以下のオーバーレイでは一部の変更作業をやり直す必要がある場合があります。

>[!CAUTION]
>
>[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) および関連する手法は、[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) と併用する場合に限り使用できます。つまり、スケルトン構造を持つオーバーレイの作成は、標準のタッチ操作対応 UI にのみ適しています。
>
>他の領域（クラシック UI を含む）のオーバーレイでは、適切なノードとサブ構造全体をコピーし、必要な変更を行います。

オーバーレイは、[コンソールの設定](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)、[サイドパネル内にあるアセットブラウザーへの選択カテゴリの作成](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser)（ページのオーサリング時に使用）など、多くの変更において推奨される方法です。オーバーレイは、次の理由で必要になります。

* ***禁止* 変更を加える `/libs` 分岐&#x200B;**このブランチは、次の操作を行うたびに変更される可能性が高いので、加えた変更はすべて失われる可能性があります。

   * インスタンスにアップグレードします。
   * ホットフィックスの適用
   * 機能パックをインストールする

* 変更を 1 か所に集約し、必要に応じて、変更の追跡、移行、バックアップ、デバッグを容易におこなえます。

## 検索パスの設定 {#configuring-the-search-paths}

オーバーレイの場合、配信されるリソースは、取得されたリソースとプロパティの集計で、定義可能な検索パスに応じて表されます。

* リソース **Resolver Search Path** 例： [OSGi 設定](/help/sites-deploying/configuring-osgi.md) （の） **Apache Sling Resource Resolver Factory**.

   * 検索パスの上から下に並ぶ順序は、それぞれの優先度を示します。
   * 標準インストールでは、主なデフォルトは次のようになります。 `/apps`, `/libs`  — その内容は `/apps` ～よりも優先度が高い `/libs` ( つまり、 *overlays* ))。

* スクリプトの保存場所への JCR:READ アクセス権を 2 人のサービスユーザーに付与する必要があります。この 2 人のユーザーは、components-search-service（com.day.cq.wcm.core でコンポーネントのアクセス／キャッシュに使用）と sling-scripting（org.apache.sling.servlets.resolver でサーブレットの検索に使用）です。
* 次の設定も、スクリプトの保存場所に応じて設定する必要があります（この例では /etc、/libs または /apps の下）。

  ```
  PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
  resource.resolver.searchpath=["/etc","/apps","/libs"]
  resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
  ```

* 最後に、サーブレットリゾルバーも設定する必要があります（この例では、 /etc も追加します）。

  ```
  PID = org.apache.sling.servlets.resolver.SlingServletResolver
  servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
  ```

## 使用例 {#example-of-usage}

以下に、いくつかの例を示します。

* [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)
* [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)
