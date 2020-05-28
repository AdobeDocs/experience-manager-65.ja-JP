---
title: 廃止される機能および削除された機能
description: リリースノート（Adobe Experience Manager 6.5 の廃止される機能および削除された機能）
uuid: 81d9a064-e712-4eff-bd3b-6e15513a5435
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: e8e2e01b-0117-48c3-86d8-609d29a147be
docset: aem65
translation-type: tm+mt
source-git-commit: 49209cb64c829fde396e87ca4b2e326ecf1dd941
workflow-type: tm+mt
source-wordcount: '1634'
ht-degree: 58%

---


# 廃止される機能および削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

近い将来おこなわれる AEM 機能の削除や置換を通知するため、次のルールが適用されます。

1. まず、非推奨（廃止予定）の発表がおこなわれます。非推奨ですが、機能は引き続き利用できますが、これ以上強化されることはありません。
1. 廃止された機能の削除は、早ければ、次のメジャーリリースでおこなわれます。削除の実際の期日が発表されます。

このプロセスにより、機能が実際に削除されるまでに、非推奨（廃止予定）の機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

## 廃止される機能 {#deprecated-features}

この節では、AEM 6.5 で廃止予定になっている機能について説明します。通常、将来のリリースで削除される予定になっている機能は、まず廃止予定に設定されて代替の機能が提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するために実装の変更を計画するようにお勧めします。

<table>
 <tbody>
  <tr>
   <td><b>領域</b></td>
   <td><b>機能</b></td>
   <td><b>代替手段</b></td>
  </tr>
  <tr>
   <td>Creative Cloudの統合</td>
   <td><p><a href="/help/assets/aem-cc-folder-sharing-best-practices.md">AEMからCreative Cloudへのフォルダー共有</a> （AEMからCreative Cloudへ）は、AEMのアセットにクリエイティブユーザーがアクセスできるようにする方法としてAEM 6.2で導入されました。これにより、CCアプリケーションでアセットを開いたり、変更をAEMに保存したります。 Creative Cloud アプリケーションでリリースされた新しい機能である Adobe Asset Link では、ユーザーエクスペリエンスが大幅に向上し、Photoshop、InDesign、Illustrator 内から AEM のアセットへの直接アクセスが強化されています。</p> <p>AEM／Creative Cloud フォルダー共有の統合機能がさらに強化される予定はありません。この機能は AEM に含まれてはいますが、代替ソリューションを使用することを強くお勧めします。</p> </td>
   <td>Adobe Asset LinkやAEMデスクトップアプリケーションを含む、新しいCreative Cloud統合機能に切り替えることをお勧めします。 Review <a href="/help/assets/aem-cc-integration-best-practices.md">AEM and Creative Cloud Integration Best Practices</a> for more details.</td>
  </tr>
  <tr>
   <td>Assets</td>
   <td>
    <ol>
     <li>AssetDownloadServlet は、パブリッシュインスタンスに対してデフォルトで無効になっています。詳しくは、</a>AEM セキュリティチェックリスト<a href="/help/sites-administering/security-checklist.md">を参照してください。</a></li>
     <li>ユーザーが /content/dam/collections に十分な（読み取りと書き込みの）権限を持っていない場合、ユーザーはコレクションを作成できません。</li>
    </ol> </td>
   <td>
    <ol>
     <li>設定について詳しくは、<a href="/help/sites-administering/security-checklist.md">AEM セキュリティチェックリスト</a>を参照してください。</li>
     <li>ユーザーのアクセス制御設定を保持し、適切な権限を確保します。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Adobe Search&amp;Promote</td>
   <td><p>Adobe Search &amp; Promoteとの統合は廃止されました。</p> <p>Search&amp;Promote 統合機能がさらに強化される予定はありません。Search&amp;Promote 統合は廃止中も引き続き完全にサポートされます。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>DTM タグマネージャー</td>
   <td>DTM（Dynamic Tag Manager）との統合は廃止されました。</td>
   <td>Adobe Experience Platform Launch をタグマネージャーとして使用してください。</td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>AEM 6.5 では、Adobe I/O ベースの Adobe Target Standard API（Rest API）を使用して AEM が Adobe Target サービスに接続できるようになったので、Target Classic API（XML）方式は廃止されました。</td>
   <td><a href="https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html">新しい API を使用するように統合機能を再設定してください。</a></td>
  </tr>
  <tr>
   <td>Adobe Target</td>
   <td>mbox.js を使用した AEM と Adobe Target の統合は廃止されました。</td>
   <td>at.js 1.x の使用に切り替えてください。</td>
  </tr>
  <tr>
   <td>Commerce</td>
   <td><p><a href="https://github.com/adobe/commerce-cif-api" target="_blank">CIF REST</a> は、AEMとコマースエンジンとの統合を可能にする一連のマイクロサービスとして2018年に提供されました。</p> <p>2018年の中頃にアドビがMagentoを買収した後、アドビは次の2つの理由からアプローチの変更を決定しました。 </p> <p><strong>1.</strong> Magentoには独自のコマースAPI （RESTとGraphQL）のセットがあり、2セットのAPIを維持するのは良い方法ではありません </p> <p><strong>2.</strong> 市場の動向から、お客様はGraphQLに向かって進んでいることがわかりました。これは、データをより効率的にクエリする方法であるためです。 2019年に、アドビはMagentoのGraphQL APIを真の原因として使用する新しいCommerce Integration Frameworkをリリースしました。</p> <p>アドビは、CIF RESTにこれ以上投資する予定はありません。 お客様には、交換ソリューションの使用を強くお勧めします。</p> </td>
   <td><p>AEM-Magento統合の場合、 <a href="https://github.com/adobe/aem-cif-project-archetype" target="_blank">AEM CIFアーキタイプ</a>、 <a href="https://github.com/adobe/aem-core-cif-components" target="_blank">AEM CIFコアコンポーネントに切り替えます。</a></p> <p>詳しくは、Commerce Integration Frameworkを使用した <a href="https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md" target="_blank">AEMとMagentoの統合を参照してください</a> 。</p> <p>新しいアプローチとのサードパーティ（Magentoを除く）統合のサポートは、アドビのロードマップにあります。</p> </td>
  </tr>
  <tr>
   <td>コンポーネント（AEM Sites）</td>
   <td><p>アドビでは、/libs/foundation/components に格納されている基盤コンポーネントのほとんどについては、さらに機能強化する予定はありません。</p> <p>コンポーネントフォルダーの <strong>cq:deprecated</strong> および <strong>cq:deprecatedReason</strong> プロパティを参照してください。</p> <p>AEM 6.5にはFoundation Componentsが含まれており、以前のリリースからアップグレードしたお客様は、これらをそのまま使用できます。 また、Foundation Componentsは非推奨の間も完全にサポートされたままです。 </p> </td>
   <td>今後のプロジェクトには、コアコンポーネントを使用することをお勧めします。Existing sites can remain as is or use the <a href="https://github.com/adobe/aem-modernize-tools">AEM Modernize Tools Suite</a> to refactor the site to use Core Components.</td>
  </tr>
  <tr>
   <td>コンポーネント（AEM Sites）</td>
   <td>デザインインポーターコンポーネント（/libs/wcm/designimporter/components）は、6.5 以降、廃止となりました。アドビでは、このデザインインポーター実装をさらに機能強化する予定はありません。</td>
   <td>今後のリリースで使用事例の代替実装を提供する予定です。</td>
  </tr>
  <tr>
   <td>Foundation</td>
   <td><p>Granite オフロードフレームワーク</p> <p>アセット処理を外部化するために 5.6.1 に導入されたオフロードフレームワークの機能がさらに強化される予定はありません。 </p> </td>
   <td>アドビでは、クラウドネイティブな次世代オフロードフレームワークの構築に取り組んでいます。</td>
  </tr>
  <tr>
   <td>開発者向け</td>
   <td><p>Hobbes.js</p> <p>アドビでは、hobbes.jsユーザーインターフェイステストフレームワークをさらに拡張する予定はありません。</p> </td>
   <td>Seleniumの自動化をお勧めします。</td>
  </tr>
  <tr>
   <td>開発者向け</td>
   <td><p>jQuery UI クライアントライブラリ</p> <p>配布版（クイックスタート）の一部として含まれている jQuery UI クライアントライブラリがさらに保守および更新される予定はありません。</p> </td>
   <td>プロジェクトコードベースにコードを追加する場合は、引き続きjQuery UIをコードに必要とすることをお勧めします。</td>
  </tr>
  <tr>
   <td>開発者向け</td>
   <td><p>jQuery Animationクライアントライブラリ(granite.jquery.animation)</p> <p>配布版（クイックスタート）の一部として含まれている jQuery アニメーションクライアントライブラリがさらに保守および更新される予定はありません。</p> </td>
   <td>プロジェクトコードベースにコードを追加する場合、引き続きjQuery Animationsを必要とするお客様にお勧めします。</td>
  </tr>
  <tr>
   <td>開発者向け</td>
   <td><p>Handlebars クライアントライブラリ</p> <p>配布版（クイックスタート）の一部として含まれている Handlebars クライアントライブラリがさらに保守および更新される予定はありません。</p> </td>
   <td>コードをプロジェクトのコードベースに追加する際に、引き続きコードのハンドルバーが必要な場合は、この方法をお勧めします。</td>
  </tr>
  <tr>
   <td>開発者向け</td>
   <td><p>Lawnchair クライアントライブラリ</p> <p>配布版（クイックスタート）の一部として含まれている Lawnchair クライアントライブラリがさらに保守および更新される予定はありません。</p> </td>
   <td>Adobeは、コードをプロジェクトのコードベースに追加するために、引き続きLawnchairを必要とするお客様を推奨します。</td>
  </tr>
  <tr>
   <td>開発者向け</td>
   <td><p>Granite.Sling.js クライアントライブラリ</p> <p>配布版（クイックスタート）の一部として含まれている Granite.Sling.js クライアントライブラリの機能がさらに強化される予定はありません。</p> </td>
   <td>ライブラリの機能に依存しているお客様は、コードを使用しなくなるようにリファクタリングすることをお勧めします。</td>
  </tr>
  <tr>
   <td>開発者向け</td>
   <td>YUI を使用した JavaScript クライアントライブラリの圧縮／軽量化。YUI ライブラリがさらに更新される予定はありません。AEM 6.4までは、YUIはJavaScriptを縮小するようにデフォルト設定されていましたが、Google Closure Compiler(GCC)に切り替えるオプションもありました。 AEM 6.5 以降は、GCC がデフォルトになっています。</td>
   <td>AEM 6.5にアップグレードしてGCCに切り替えて導入することをお勧めします</td>
  </tr>
  <tr>
   <td>開発者向け</td>
   <td><p>CRXDE Lite のクラシック UI ダイアログエディター</p> <p>配布版（クイックスタート）の一部として含まれているクラシック UI ダイアログエディターの機能がさらに強化される予定はありません。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Forms</td>
   <td><p>AEM MobileとのAEM Formsの統合&lt;は廃止されました。 </p> </td>
   <td>代替機能はありません </td>
  </tr>
 </tbody>
</table>

## 削除された機能 {#removed-features}

この節では、AEM 6.5から削除された機能と機能に関するリストを示します。以前のリリースでは、これらの機能は非推奨としてマークされていました。

| 領域 | 機能 | 代替手段 |
|--- |--- |--- |
| Analytics の Activity Map | AEM に組み込まれている Activity Map のバージョン。 | Adobe Analytics API 内のセキュリティ変更により、AEM に含まれているバージョンの Activity Map は使用できなくなりました。Adobe Analytics [](https://docs.adobe.complugin /content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)が提供するActivityMapプラグインを使用します。 |
| 統合 | ExactTarget統合は、デフォルトの配布(Quickstart)から削除され、使用できなくなりました。 | 代替機能はありません |
| 統合 | Salesforce Force API との統合はデフォルトの配布版（クイックスタート）から削除され、パッケージ共有からインストールする追加パッケージになりました。 | 機能は引き続き利用できます。 |
| Forms | Adobe Central 製品がサポートされなくなったので、Adobe Central Migration Bridge サービスのサポートが削除されました。 | 代替機能はありません |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 代替機能はありません |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 代替機能はありません |
| Forms | LiveCycle ES4 SP1からJEE上のAEM 6.5 Formsへのシングルホップアップグレードは使用できません | AEM Formsアップグレードドキュメントの [利用可能なアップグレードパス](../forms/using/upgrade.md) を参照してください。 |
| Forms | JEE上のAEM FormsからUPDベースのクラスタリングサポートを削除しました。 | JEE上のAEM Formsでは、TCPベースのクラスタリングのみを使用できます。 UDPマルチキャストサーバーを以前のバージョンからJEE上のAEM 5.5 Formsにアップグレードする場合は、手動設定を実行してTCPベースのGemfireクラスタリングに切り替えます。 詳細な手順については、「JEE上のAEM 6.5 formsへの [アップグレード」を参照してください。](../forms/using/upgrade-forms-jee.md) |
| 開発者向け | デフォルトの配布版（クイックスタート）から Firebug Lite が削除されました | ブラウザー組み込みのデベロッパーコンソールを使用してください。 |
| 開発者向け | Remove `customJavaScriptPath` support in HTML Client Library Manager. | 代替機能はありません |
| Assets | AEM 6.5では、アセットのオフロード機能が削除されました。 | 代替機能はありません |
| キャッシュ | `system/console/slingjsp` が削除されました。 | クラスとスライトリーキャッシュは、Apache Sling Commons FileSystem ClassLoaderバンドルの下に格納されます。 AEM Webコンソールでバンドル番号を確認し、キャッシュフォルダーをファイルシステムから直接削除できます(`crx-quickstart/launchpad/felix/bundle<ID>`)。 |

## 次期リリースに関する予告 {#pre-announcement-for-next-release}

このセクションで予告する将来のリリースの変更内容は、廃止ではありませんが、お客様に影響します。計画を立てる際の参考情報としてご覧ください。

| 領域 | 機能 | お知らせ |
|--- |--- |--- |
| Foundation | UI フレームワーク | Coral UI 2 コンポーネントは 2019 年に廃止される予定です。Coral UI 3 は AEM 6.2 で導入され、AEM 6.5 は完全に Coral 3 に基づいています。Coral 2 を使用してカスタム UI を構築しているお客様およびパートナー様については、Coral 3 へのリファクタリングをおこなうことをお勧めします。アドビでは、Coral 2 のダイアログを Coral 3 に変換するツールを提供しています（](/help/sites-developing/dialog-conversion.md)詳細情報[）。 |
