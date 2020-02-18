---
title: AEM 6.5 におけるリポジトリの再構築
seo-title: AEM 6.5 におけるリポジトリの再構築
description: AEM 6.5でのリポジトリの再構築について説明します。
seo-description: AEM 6.5でのリポジトリの再構築について説明します。
uuid: bc577c82-3279-4ddd-898c-607864868db0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 274a7f5a-d509-4ca9-9ae5-30e48f34f171
docset: aem65
redirecttarget: /content/help/en/experience-manager/6-5/help/sites-deploying/repository-restructuring.html
translation-type: tm+mt
source-git-commit: bd0dc09ea230416ad3544d14440b7b74b80ec406

---


# AEM 6.5 におけるリポジトリの再構築 {#repository-restructuring-in-aem}

## 概要 {#introduction}

AEM 6.5より前のバージョンでは、JCRの予期しない領域に、アップグレード時に変更される可能性のあるカスタマーコードがデプロイされていました。 このため、正式なAEMリリース（メジャーバージョン、機能パック、サービスパック、ホットフィックス）では、カスタムコード、設定、またはコンテンツが上書きされるのが一般的でした。 逆に、カスタムのコードや設定やコンテンツが AEM の製品コードやコンテンツを上書きしてしまい、製品の機能が損なわれることもありました。

このような競合は必ずしも自動的に解決できず、特定に多くの処理時間が必要となり、解決にも人間の介入を必要としました。さらに、完全に解決されたかどうかも必ずしも明確ではありませんでした。AEM 製品コードとカスタムコードの階層を明確に記述すれば、このような競合を回避できます。

To that end, beginning in AEM 6.5 and to be continued in future releases, content is being restructured out of `/etc` to other folders in the repository, along with guidelines on what content goes  where,  adhering to the following high-level rules:

* AEM product code will always be placed in `/libs`, which must not be overwritten by custom code
* Custom  code should be placed in `/apps`, `/content`, and `/conf`

This article is organized into three sections, representing the type of content that has been moved out of `/etc`:

1. 設定
1. クライアント側ライブラリ
1. その他

各節には以下の内容が含まれています。

* 再構築された場所と追加のコンテキストを示す表。近い将来、この表をもっと読みやすいフラットな形式に作り直す予定です。
* an extensibility strategy allowing custom code to successfully extend AEM application code residing under `/libs`.

## 下位互換性 {#backwards-compatibility}

ほとんどの場合、AEM 6.5にアップグレードした後も、古い場所との下位互換性が維持されます。これは、新しく追加される場所に加えて、製品コードで保存および考慮される古い場所によって達成されます。 ほとんどの場合、条件ロジックは、既存のフォルダーが存在するかどうかを確認し、新しい場所ではなく、既存の場所からコンテンツを読み取るために使用されます。

それぞれの環境の都合に応じて、6.5 へのアップグレード後、日程を定めて古い場所を削除し、新しい場所のコンテンツを使用するようにしてください。以下の表に、場所ごとの新しいコンテンツ構造に従う手順を示します。

>[!NOTE]
>
>インプレースアップグレードが実行されたインスタンスには、新しい場所に加えて、古いコンテンツの場所も含まれます。新規インストールの場合は、新しい場所のみが含まれます。

## 表の読み方 {#how-to-read-the-tables}

各節の表には、以下の内容が記載されています。

* このコンテンツが関連する AEM ソリューション（Sites、Assets、Forms など）
* 古い（6.4 以前の）場所
* 新しい 6.5 の場所
* 新しいコンテンツ構造に準拠するための手順。例えば、6.5 へのアップグレードの数週間または数ヶ月後に、スクリプトを実行したり、手動でファイルを移動したりする必要があります。
* 6.5 よりも前のバージョンから AEM 6.4 にアップグレードする場合に古いコンテンツの場所の後方互換性を維持するために使用される AEM のアプローチ

## 設定 {#configuration}

The content locations in this section generally refer to content that resides under a `/settings` folder under `/libs`, `/apps`, or `/conf`.

### 拡張戦略 {#extensibility-strategy}

In general, but with a few exceptions, content under this section can be extended using Apache Sling&#39;s [   Context Aware   Configuration](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html) feature.

要するに、コンテキスト対応設定を使用すると、リポジトリの1つの部分のコンテンツを、リポジトリの他の部分のコンテンツ別に複数回オーバーレイできます。 例えば、のコンテンツをのコ `/libs` ンテンツでオーバーレイし、そ `/apps`の後でのコンテンツでオーバーレイすることができま `/conf`す。 Moreover, content in a global folder under `/conf` can be overlayed by a specific &quot;tenant&quot; or &quot;site&quot; (e.g. `/conf/we-retail/settings`).

通常、コンテキスト対応設定は、機能設定を拡張する方法として使用されますが、他のコンテンツタイプで使用される場合もあります。

次の表に、「設定タイプ」という名前の追加の列を示し、設定をオーバーレイできる範囲を示します。 ここでは、これらの設定タイプについて追加の詳細を示します。

**コンテキスト非対応**

* Resources happen to be in context-aware folder structures (like `/libs/settings`) but always referenced via absolute path so context awareness is not in effect.
* リソースはどこにでも配置できます。For example, Assets DRM Licenses could be at `/content/my-customer/licenses/creative-commons.html`
* 例：

   * Workflow scripts -> `/apps/settings/workflow/scripts/noop.ecma`
   * アセットDRMライセンス —> `/apps/settings/dam/drm/my-license`

**グローバルのみ**

* グローバル設定のみを持つ機能です。
* As a reference point, take the precedence of settings in this example: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global`

* AEM ではグローバル設定のみがサポートされます。テナントに対応した設定はサポートされません。
* AEMは常に、最初に/conf/globalレベルで設定を検索し始めます

* 例：

   * ワークフローランチャー -> `/libs/settings/workflow/launcher`
   * ワークフローモデル -> `/conf/global/settings/workflow/models`

**テナント対応**

* For tenant-aware configurations, see this example for the precedence of configuration paths: `/libs/settings` &lt; `/apps/settings` &lt; `/conf/global` &lt; `/conf/we-retail`, where we-retail is the tenant name. テナント対応の設定では、サブテナントもサポートされます。

* AEM では、テナント対応の設定がサポートされます。It respects `cq:conf` property on hierarchy
* 例：

   * 編集可能テンプレート -> `/conf/we-retail/settings/wcm/templates`
   * クラウド設定 —> `/conf/we-retail/settings/cloudsettings`

<table>
 <tbody>
  <tr>
   <td><strong>解決策</strong></td>
   <td><strong>前の場所</strong><br /> </td>
   <td><strong>新しい場所</strong></td>
   <td><strong>コンテキスト対応の設定タイプ</strong><br /> </td>
   <td><strong>後方互換性のアプローチ</strong></td>
   <td><strong>最新モデルに合わせるための要件</strong></td>
  </tr>
  <tr>
   <td>AEM Sites／AEM Forms</td>
   <td><p><code>/etc/cloudservices/typekit</code></p> <p><code>/etc/cloudservices/recaptcha</code></p> <p><code>/etc/cloudservices/echosign</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/typekit</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/recaptcha</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/echosign</code></p> </td>
   <td>テナント対応</td>
   <td><p>従来のクラウドサービス。</p> <p>インプレースアップグレード時に従来の設定がそのまま維持されます。フォールバックとして、AEM に、これらを列挙し、読み取るコードが残されています。</p> </td>
   <td>新しいパスに自動的に変換するために、Forms 移行 UI から遅延コンテンツ移行ユーティリティをトリガーできます。<br /> </td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/cloudservices/fdm</code></td>
   <td><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/fdm</code></td>
   <td>テナント対応</td>
   <td><p>従来のクラウドサービス。</p> <p>インプレースアップグレード時に従来の設定がそのまま維持されます。フォールバックとして、AEM に、これらを列挙し、読み取るコードが残されています。</p> </td>
   <td>新しいパスに自動的に変換するために、Forms 移行 UI から遅延コンテンツ移行ユーティリティをトリガーできます。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/adhocassetshare</code></td>
   <td><code>/libs/settings/dam/adhocassetshare</code></td>
   <td>テナント対応</td>
   <td>新しい標準（OOTB）のコンテンツ構造よりも、従来のコンテンツ構造が優先されます。</td>
   <td>Project level customizations need to be cut and pasted into the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
   <td><code>/libs/settings/dam/workflow</code></td>
   <td>テナント対応</td>
   <td>新しい標準（OOTB）のコンテンツ構造よりも、従来のコンテンツ構造が優先されます。</td>
   <td>Project level customizations need to be cut and pasted into the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/drm/licenses/</code></td>
   <td><code>/libs/settings/dam/drm</code></td>
   <td>コンテキスト非対応</td>
   <td>新しい標準（OOTB）のコンテンツ構造よりも、従来のコンテンツ構造が優先されます。</td>
   <td>Project level customizations need to be cut and pasted into the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/indesign/scripts</code></td>
   <td><code>/libs/settings/dam/indesign</code></td>
   <td>テナント対応</td>
   <td>新しい標準（OOTB）のコンテンツ構造よりも、従来のコンテンツ構造が優先されます。</td>
   <td><p>Project level customizations need to be cut and pasted under the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</p> <p>カスタマイズされたアセット取り込みワークフローを実行する場合は、メディア抽出プロセス設定に /etc の古い場所への参照が残っています。変更に対応するために、/etc 下のスクリプトを対応する /apps および /conf パスに移動するとともに、カスタマイズされたメディア抽出プロセスの引数を絶対パスから相対パスに変更する必要があります。</p> <p>詳しくは、<a href="https://helpx.adobe.com/experience-manager/6-2/help/assets/indesign.html">このページ</a>を参照してください。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video</code></td>
   <td><code>/libs/settings/dam/video</code></td>
   <td>テナント対応</td>
   <td>新しい標準（OOTB）のコンテンツ構造よりも、従来のコンテンツ構造が優先されます。</td>
   <td>Project level customizations need to be cut and pasted into the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/notification/email/default</code></td>
   <td><code>/libs/settings/dam/notification</code></td>
   <td>テナント対応</td>
   <td>新しい標準（OOTB）のコンテンツ構造よりも、従来のコンテンツ構造が優先されます。</td>
   <td>Project level customizations need to be cut and pasted into the equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</td>
  </tr>
  <tr>
   <td>AEM Sites／AEM Assets</td>
   <td><code>/etc/designs</code> </td>
   <td><code>/libs/settings/wcm/designs</code></td>
   <td>コンテキスト非対応</td>
   <td><p>利用側のサービスが、古い場所を認識します。</p> <p>従来の場所の設定が考慮されます。</p> </td>
   <td><br /> Move custom content from <code>/etc/design</code> to <code>/apps/settings/wcm/design</code> for alignment with the new repository structure. 今後は、編集可能なテンプレート機能を使用するようにサイトをアップグレードすることを検討してください。これにより、デザインモードとこのコンテンツが不要になります。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/scaffolding</code></td>
   <td><p><code>/libs/settings/wcm/template-types/scaffolding/scaffolding</code></p> <p><code>/apps/settings/wcm/template-types/scaffolding/scaffolding</code></p> </td>
   <td>コンテキスト非対応</td>
   <td>The components in the old location under <code>/etc/scaffolding</code> will continue to function, but have been deprecated.</td>
   <td>新しい場所の新しい基礎モードコンポーネントを使用することをお勧めします。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/blueprints</code></td>
   <td><p>/libs/msm（初期状態の画面とコマースのBlueprint設定用）</p> <p> </p> </td>
   <td>コンテキスト非対応</td>
   <td><p>利用側のサービスが、古い場所を認識します。</p> <p>従来の場所の設定が考慮されます。</p> </td>
   <td>設定を新しい場所にコピーする必要があります。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/mobile</code></td>
   <td><code>/libs/settings/mobile</code></td>
   <td>テナント対応</td>
   <td>機能は設定マネージャーを利用しており、フォールバックとして引き続き古い場所をサポートします。</td>
   <td>
    <ol>
     <li>構成をからに移動しま <code>/etc</code> す。 <code>/conf/&lt;tenant&gt;/settings/mobile</code></li>
     <li>その後、コンテンツの参照を以下のように更新します。</li>
    </ol> <p><code>/content/&lt;tenant&gt;/jcr:content/cq:deviceGroups{String[]}=mobile/groups/responsive</code></p> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/msm/rolloutConfigs</code></td>
   <td><code>/libs/msm/wcm/rolloutconfigs</code></td>
   <td>該当なし</td>
   <td><p>利用側のサービスが、古い場所を認識します。</p> <p>従来の場所に設定が検出されれば、それらの設定が使用されます。</p> </td>
   <td>To align with the new model, configurations need to be created in the new locations, and the old ones under <code>/etc</code> must be deleted.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/segmentation/contexthub</code></td>
   <td><code>/conf/we-retail/settings/wcm/segments</code></td>
   <td>テナント対応</td>
   <td><p>古い場所のセグメントは以下のようになります。</p>
    <ul>
     <li>オーディエンスコンソールに読み取り専用モードで残ります。</li>
     <li>引き続きページで読み込まれます（該当するパスが<strong>ページのプロパティ／パーソナライズ機能／セグメントのパス</strong>で選択されている場合）。</li>
     <li>コンテンツのターゲット設定に使用できます。</li>
    </ul> </td>
   <td><a href="/help/sites-deploying/upgrading-code-and-customizations.md#migrateconfigurations">セグメント移行ツール</a>を使用して、新しい場所に移行できます。</td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/social/config/languageOpts</code></td>
   <td><code>/libs/social/translation/languageOpts</code></td>
   <td>該当なし</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/templates</code></td>
   <td><code>/libs/settings/community/templates</code></td>
   <td> </td>
   <td><p>コードは古いテンプレートの場所を認識します。Existing templates will continue to be referred and read/write from <code>/etc</code>.</p> <p><br /> 電子メールテンプレートでは、<strong>AEM Communities Email Reply Configuration</strong> で <strong>Templates root</strong> path を設定して別のパスにカスタムテンプレートを作成している場合、そのテンプレートがそのまま使用されます。</p> </td>
   <td><p>A <a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-template-migration" target="_blank">migration utility</a> can align to the latest AEM Communities templates model.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/badging</code></td>
   <td><p><strong>バッジルール：</strong></p> <p><code>/libs/settings/community/badging</code></p> <p><strong>バッジ画像：</strong></p> <p>The out of the box images in the old location at <code>/etc/community/badging/images</code> are moved to <code>/libs/community/badging/images </code> </p> <p> </p> <p>Custom images are moved to <code>/content/community/badging/images</code>.</p> <p> </p> </td>
   <td>テナント対応</td>
   <td><p>コードは古いバッジのパスを認識します。</p> <p><br /> 最初に古いパスが存在するかがチェックされます。<br />存在しない場合は、新しいパスが使用されます。</p> </td>
   <td><p>最新のモデルに合わせるには、手動による移行が必要です。これをおこなうには、以下の手順に従います。</p>
    <ol>
     <li><strong>ツール</strong>の下の設定ブラウザーを使用して、サイトコンテキストバケットを作成します。</li>
     <li>サイトのルートに移動します。</li>
     <li><code>cq:conf</code> プロパティを、すべての設定を格納するバケットのパスに設定します。<strong>サイト編集ウィザード - クラウド設定入力</strong>から設定して変更内容を保存することもできます。</li>
     <li>Move the relevant badging rules and scoring rules from <code>etc/community/*</code> to the site context bucket created in the previous step</li>
     <li>サイトのルートの <code>badgingRules</code> および <code>scoringRules</code> プロパティを、新しいルールの場所を参照する相対パスに変更します。As an example, if <code>cq:conf</code> is set to <code>/conf/we-retail</code>, the value for <code>badgingRules</code> will be <code>community/badging/rules</code> if rules are now moved to this new bucket</li>
     <li>同様に、バッジルールノードのスコアルールへの参照も相対パスに変更します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/cloudservices/facebookconnect</code></p> <p><code>/etc/cloudservices/twitterconnect</code></p> <p><code>/etc/cloudservices/pinterestconnect</code></p> </td>
   <td><p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/facebookconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/twitterconnect</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/pinterestconnect</code></p> </td>
   <td>テナント対応</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/scoring</code></td>
   <td><code>/libs/settings/community/scoring</code></td>
   <td> </td>
   <td><p>コードは古いバッジのパスを認識します。</p> <p><br /> 最初に古いパスが存在するかがチェックされます。<br />存在しない場合は、新しいパスが使用されます。</p> </td>
   <td><p>最新のモデルに合わせるには、手動による移行手順が必要です。</p> <p>手順は、上記のバッジルールと同じです。</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/notifications</code></td>
   <td><code>/libs/settings/community/notifications</code></td>
   <td>コンテキスト非対応</td>
   <td><p>これらの設定は、後方互換性がありません。新しい場所への移行手順については、「最新モデルに合わせるための要件」の列を参照してください。<br /> </p> <br /> </td>
   <td><p>最新のモデルに合わせるには、手動による移行が必要です。You can use the Granite Configuration Manager to move the configurations to the new path under <code>/apps/settings</code>.</p> <p>Therefore, you need to set the <code>mergeList</code> property to true on the <code>/libs/settings/community/subscriptions</code> node and then add an <code>nt:unstructured</code> child node.<br /> </p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/community/subscriptions</code></td>
   <td><code>/libs/settings/community/subscriptions</code></td>
   <td>コンテキスト非対応</td>
   <td>これらの設定は、後方互換性がありません。新しい場所への移行手順については、「最新モデルに合わせるための要件」の列を参照してください。</td>
   <td><p>最新のモデルに合わせるには、手動による移行が必要です。You can use the Granite Configuration Manager to move the configurations to the new path under <code>/apps/settings</code>.</p> <p>Therefore, you need to set the <code>mergeList</code> property to true on the <code>/libs/settings/community/subscriptions</code> node and then add an <code>nt:unstructured</code> child node.</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/socialconfig/srpc/defaultconfiguration</code></td>
   <td><code>/conf/global/settings/community/srpc/defaultconfiguration</code></td>
   <td>global</td>
   <td>これらの設定には後方互換性があります。古いパスが検出されると、そのパスが使用されます。検出されない場合は、新しいパスが優先的に使用されます。</td>
   <td><p>遅延コンテンツ移行タスクは <code>CQ64CommunitiesConfigsCleanupTask</code> の形で利用できます。</p> <p>詳しくは、<a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">遅延移行に関するドキュメント</a>を参照してください。</p> </td>
  </tr>
  <tr>
   <td>AEM Communities</td>
   <td><code>/etc/watchwords</code></td>
   <td><code>/libs/community/watchwords</code></td>
   <td>該当なし</td>
   <td>これらの設定には後方互換性があります。古いパスが検出されると、そのパスが使用されます。検出されない場合は、新しいパスが優先的に使用されます。</td>
   <td><p>遅延コンテンツ移行タスクは <code>CQ64CommunitiesConfigsCleanupTask</code> の形で利用できます。</p> <p>Watchwords will have to be manually moved from <code>/etc/watchwords</code> to <code>/conf/global/settings/community/watchwords</code>.</p> </td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code> </p> <p><code>/var/workflow/models</code></p> </td>
   <td>global</td>
   <td><p>Legacy location is used if present and no configuration exists in <code>/libs</code> or <code>/conf</code>.</p> <p>When editing OOTB workflow models, context-aware overlays must be created under <code>/conf</code> to allow them to be modifiable.</p> <p>Package export needs to include the model in <code>/libs</code> or <code>/conf</code> and the runtime model in <code>/var/workflow/models.</code></p> </td>
   <td><p>Newly created models will be created in the <code>/conf/global/settings</code> location.</p> <p>Any edits in <code>/etc</code> or <code>/libs</code> require you to explicitly create an override in <code>/conf/global/settings</code> before editing can be done. The Edit button has to be selected, and it will cause the override in <code>/conf</code> to be created and editing allowed.</p> </td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/workflow/launcher</code></td>
   <td><p><code>/libs/settings/workflow/launcher</code></p> <p><code>/conf/global/settings/workflow/launcher</code></p> </td>
   <td>global</td>
   <td>Legacy location is used if present and no configuration<br /> exists in <code>/libs</code> or <code>/conf</code> locations. これにより、カスタムランチャーが維持されます。</td>
   <td><p>Newly created or edited launcher configurations are located in the <code>/conf</code> location.</p> <p>All launchers should be moved from the legacy <code>/etc</code> location to<code> /conf/global/settings/workflow/launcher.</code></p> </td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/workflow/models</code></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> </td>
   <td>global</td>
   <td>Legacy location is used if present and no configuration<br /> exists in <code>/libs</code> or <code>/conf</code> locations. これにより、カスタムワークフローモデルが維持されます。</td>
   <td><p>All workflow models should be moved from the legacy <code>/etc</code> location to <code>/conf/global/settings/workflow/models</code>.</p> <p> </p> </td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/workflow/notification</code></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
   <td>コンテキスト非対応</td>
   <td><p>後方互換性のために、従来の場所が存在する場合は従来の場所が使用されます。</p> <p>Previously, out of the box templates had to be overridden by editing them in <code>/etc</code>. Now, override should be stored in <code>/conf/global</code>.</p> </td>
   <td>詳しくは、ワークフローのドキュメントを参照してください。<br /> </td>
  </tr>
  <tr>
   <td>すべて</td>
   <td><code>/etc/cloudservices/translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> <p> </p> </td>
   <td>テナント対応</td>
   <td>従来のクラウドサービス。インプレースアップグレード時に従来の設定がそのまま維持されます。フォールバックとして、AEM に、これらを列挙し、読み取るコードが残されています。</td>
   <td><p>In order to move cloud configurations to <code>/conf</code>, you can either:</p>
    <ul>
     <li>新しいタッチ UI を使用して設定を作成します。<br />または<br /> </li>
     <li>Copy the configurations from <code>/etc/cloudservices/translation</code> to their respective new location(s)</li>
    </ul> <p>Once this is done, the configurations need to be associated with Sites via <strong>Sites &gt; Properties</strong> in the user interface.</p> <p><em>注意：これが動作するためには、翻訳コネクタが AEM 6.5 と互換性を持っている必要があります。</em></p> </td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/cloudservices/msft-translation</code></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/msft-translation</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/msft-translation</code></p> </td>
   <td>テナント対応</td>
   <td>従来のクラウドサービス。インプレースアップグレード時に従来の設定がそのまま維持されます。フォールバックとして、AEM に、これらを列挙し、読み取るコードが残されています。</td>
   <td><p>In order to move cloud configurations to <code>/conf</code>, you can either:</p>
    <ul>
     <li>新しいタッチ UI を使用して設定を作成します。または<br /> </li>
     <li>Copy older configurations from <code>/etc/cloudservices/translation</code> to their respective new location(s)</li>
    </ul> <p>Once this is done, the configurations need to be associated with Sites via <strong>Sites &gt; Properties</strong> in the user interface.</p> </td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/cloudsettings</code></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
   <td>テナント対応</td>
   <td><p>Existing entries under <code>/etc</code> remain in place on upgrading the instance.</p> <p>アップグレード後にクラウド設定 UI にアクセスすると、既存のクラウド設定が新しいリポジトリ構造にコピーされます。後方互換性のために、既存の内容は維持されます。</p> </td>
   <td><p>コンテンツモデルは同じです。コンテキスト対応設定に合わせて場所のみが変更されています。</p> <p>これらのクラウド設定を対象とする<a href="/help/sites-deploying/lazy-content-migration.md">遅延移行タスク</a>では、以下の処理がおこなわれます。</p>
    <ul>
     <li>既存のクラウド設定をにコピ <code>/etc/cloudsettings</code> ー <code>/conf/global/settings/cloudsettings</code></li>
     <li>次のすべての子を削除 <code>/etc/cloudsettings</code></li>
    </ul> <p>ただし、アップグレード後、遅延移行タスクを実行する前に、手動でおこなう必要がある手順があります。</p>
    <ul>
     <li>All references pointing to <code>/etc/cloudsettings/*</code> need to be updated to point to <code>/conf/global</code></li>
    </ul> <p>注意事項：</p>
    <ul>
     <li>The <code>/etc/cloudsettings</code> container needs to be preserved</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
   <td>グローバルのみ</td>
   <td><p>Dynamic Media - Scene モード（<code>dynamicmedia_scene7</code>7 実行モード）のクラウド設定は同じ場所で維持されます。プロセスは従来どおり機能します。クラウド設定の値を調整する必要がある場合は、2 つの方法があります。</p>
    <ol>
     <li>古いクラウド設定 UI から既存の設定を更新します。</li>
     <li>新しいタッチ UI を使用して新しいクラウド設定を作成します。この設定は、古い設定よりも優先されます。</li>
    </ol> </td>
   <td><p>最新のモデルに合わせるには、以下のスクリプトを実行する必要があります。</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/viewer</code></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
   <td>グローバルのみ</td>
   <td><p>The OOTB viewer presets will only be available in the new location, while the custom viewer preset will still be under <code>/etc</code> until a modification is incurred.</p> <p>変更されると、遅延移行によって新しい場所に保存されます。組み込みの画像サーバーは、リクエストを受け取ると、従来のパスと新しいパスの両方を検索します。したがって、組み込みのコードまたは URL を変更する必要はありません。</p> </td>
   <td><p>標準のビューアプリセットは、新しい場所でのみ利用できます。カスタムのビューアプリセットでは、以下の場所にある移行スクリプトを実行する必要があります。</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p>Similar to the backward compatibility case, you don't have to adjust the copyURL/embed code to point to <code>/conf</code>. The existing request to <code>/etc</code> will be re-routed under the hood to the correct content from <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/imageserver/macros</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
   <td>グローバルのみ</td>
   <td>The macro under <code>/etc</code> is still valid. If modify it, the modified node will be moved to the new location under <code>/conf</code> via a Lazy Migration task.</td>
   <td><p>以下の場所にある移行スクリプトを実行する必要があります。</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia/Adaptive Video Encoding</code></td>
   <td><code>/libs/settings/dam/dm/presets/video/jcr:content/Adaptive Video Encoding</code></td>
   <td>該当なし</td>
   <td><p>標準のビデオプロファイルは、プロファイルにリンクするアセットフォルダープロパティを更新することなく削除されます。</p> <p>エンコーディングプロセスには、古い場所と新しい場所を変換する機能が組み込まれています。古いパスが変換され、新しいプロファイルのパスが検索されます。</p> </td>
   <td>変更は必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
   <td>グローバルのみ</td>
   <td><p>カスタムビデオプロファイルは、変更するまでそのままで維持されます。</p> <p>その後、遅延移行タスクによって新しい場所に移動されます。エンコード時の検索は、標準のビデオプリセットと同様です。エンコードプロセスにはパス変換機能が組み込まれており、最初に古い場所でビデオプロファイルが検索され、その後新しい場所で検索されます。</p> </td>
   <td><p>最新のモデルに合わせるには、以下の場所にある移行スクリプトを実行できます。</p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
   <td>グローバルのみ</td>
   <td><p>この Dynamic Media - ハイブリッドモード（<code>dynamicmedia</code> 実行モード）のクラウド設定は、同じ場所で維持されます。プロセスは従来どおり機能します。設定値は、以下の 2 つの方法で調整することができます。</p>
    <ol>
     <li>古いクラウド設定 UI から既存の設定を更新します。</li>
     <li>新しいタッチ UI を使用して新しいクラウド設定を作成します。この設定は、古い設定よりも優先されます。</li>
    </ol> </td>
   <td><p>最新のモデルに合わせるには、移行スクリプトを実行する必要があります。スクリプトは以下の場所にあります。<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/cloudservices/youtube</code></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
   <td>グローバルのみ</td>
   <td><p>DM-Youtube のクラウド設定は、同じ場所で維持されます。プロセスは従来どおり機能します。クラウド設定値は、以下の 2 つの方法で調整することができます。</p>
    <ol>
     <li>古いクラウド設定 UI から既存の設定を更新します。</li>
     <li>新しいタッチ UI を使用して新しいクラウド設定を作成します。この設定は、古い設定よりも優先されます。</li>
    </ol> </td>
   <td><p>最新のモデルに合わせるには、移行スクリプトを実行できます。スクリプトは以下の場所にあります。<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p> </p> <p> </p> </td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/presets/analytics</code></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
   <td>グローバルのみ</td>
   <td>アクションは必要ありません。</td>
   <td><p>最新のモデルに合わせるには、移行スクリプトを実行できます。スクリプトは以下の場所にあります。<br /> </p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><p><code>/etc/notification/email/default/com.day.cq.replication</code></p> <p><code>/etc/notification/email/default/com.day.cq.wcm.core.page</code></p> </td>
   <td><code>/libs/settings/notification-templates</code></td>
   <td>グローバルのみ</td>
   <td>The templates in <code>/etc/notification/email/default/</code> are given precedence over the ones in <code>/libs/settings/notification-templates</code>.</td>
   <td>In order to align to the latest model, you can create new templates under <code>/apps/settings/notification-templates</code> and perform new modifications there.</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><p><code>/etc/msm/rolloutconfigs/launch</code></p> <p><code>/etc/msm/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td><p><code>/libs/msm/launches/rolloutconfigs/launch</code></p> <p><code>/libs/msm/launches/rolloutconfigs/pushonmodifyshallow</code></p> </td>
   <td>該当なし</td>
   <td><p>利用側のサービスが、古い場所を認識します。</p> <p>従来の場所に設定が検出されれば、それらの設定が使用されます。</p> </td>
   <td>To align with the new model, configurations need to be created in the new locations, and the old ones under <code>/etc</code> must be deleted.</td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/translation/supportedLanguages</code></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
   <td>コンテキスト非対応</td>
   <td>カスタマイズされた言語をリストに追加する必要があることに注意してください。<br /> </td>
   <td>新しいリストをオーバーレイし、追加の言語が存在する場合はその言語を追加して更新します。Alternatively, copying the old list to <code>/apps</code> location would also work.</td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
   <td>グローバルのみ</td>
   <td>インプレースアップグレード時に従来の設定がそのまま維持されます。AEM に、これらを列挙し、読み取るコードが残されています。</td>
   <td>To persist the changes, copy the XML file from <code>/etc</code> to <code>/libs</code> or <code>/conf</code>. Alternatively,<strong> </strong>remove file from <code>/etc</code>.</td>
  </tr>
 </tbody>
</table>

## クライアント側ライブラリ {#client-side-libraries}

[クライアント側ライブラリは](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/clientlibs.html) 、ブラウザーで処理されるjavascriptおよびCSSコードです。

### 拡張戦略 {#extensibility-strategy-1}

AEM は、複数の JavaScript ファイルを追加するための拡張フレームワークを備えています。Any file with the same &quot;categories&quot; property will be appended, allowing custom code to extend AEM code that resides under `/libs`.

<table>
 <tbody>
  <tr>
   <td><strong>解決策</strong></td>
   <td><strong>前の場所</strong><br /> </td>
   <td><strong>新しい場所</strong></td>
   <td><strong>後方互換性のアプローチ</strong></td>
   <td><strong>最新モデルに合わせるための要件</strong></td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/fp</code></td>
   <td><code>/libs/fd/fp/components</code></td>
   <td><p>従来のクライアントライブラリは、インプレースアップグレードでアップグレードされたインスタンスで維持されます。</p> <p>新しいクライアントライブラリでは、新旧のクライアントライブラリがマージされないように、同じカテゴリ名を持ち、「<strong><code>replaces</code></strong>」プロパティが指定されています。</p> </td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/rte</code></td>
   <td><code>/libs/fd/rte</code></td>
   <td><p>インプレースアップグレードを介してアップグレードされたインスタンス上で持続する既存のclientlib。</p> <p>新しいクライアントライブラリでは、新旧のクライアントライブラリがマージされないように、同じカテゴリ名を持ち、「<strong><code>replaces</code></strong>」プロパティが指定されています。</p> </td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/af</code></td>
   <td><code>/libs/fd/af/authoring/clientlibs</code></td>
   <td>従来のクライアントライブラリ。インプレースアップグレードでアップグレードされたインスタンスで維持されます。新しいクライアントライブラリでは、新旧のクライアントライブラリがマージされないように、同じカテゴリ名を持ち、「<strong><code>replaces</code></strong>」プロパティが指定されています。</td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/themes/themeLibrary</code></td>
   <td>AEM 6.5 の標準パッケージにはこの機能は含まれていません。</td>
   <td><p>アダプティブフォームの標準のテーマです。</p> <p>インプレースアップグレード時に従来の設定がそのまま維持されます。</p> </td>
   <td>このコンテンツは一部がユーザーにより生成されています。<code>aem-forms-reference-themes</code> という名前で、参照コンテンツパッケージとして提供されます。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/expeditor</code></td>
   <td><code>/libs/fd/expeditor/clientlibs</code></td>
   <td>従来のクライアントライブラリ。インプレースアップグレードでアップグレードされたインスタンスで維持されます。新しいクライアントライブラリでは、新旧のクライアントライブラリがマージされないように、同じカテゴリ名を持ち、「<strong><code>replaces</code></strong>」プロパティが指定されています。</td>
   <td>アクションは必要ありません。<p> </p> </td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/clientlibs/fd/fmaddon</code></td>
   <td><code>/libs/fd/fmaddon</code></td>
   <td>直接利用されない従来の Analytics および Target クライアントライブラリ。 </td>
   <td>クリーンアップフィルターを使用してアップグレード後にクリーンアップされます。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
   <td><code>/libs/dam/clientlibs</code></td>
   <td>従来のクライアントライブラリには、異なるクライアントカテゴリ名が設定されています。</td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td> </td>
   <td><code>/etc/clientlibs/ckeditor</code></td>
   <td><code>/libs/clientlibs/ckeditor</code></td>
   <td>これらは従来のクライアントライブラリです。インプレースアップグレード時に従来のクライアントライブラリがそのまま維持されます。新しいクライアントライブラリでは、新旧のクライアントライブラリがマージされないように、同じカテゴリ名を持ち、「<code>replaces</code>」プロパティが指定されています。</td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/sitecatalyst</code></td>
   <td><code>/libs/cq/analytics/clientlibs/analytics</code></td>
   <td><p>これらは従来のクライアントライブラリです。インプレースアップグレード時に従来の設定がそのまま維持されます。</p> <p>新しいクライアントライブラリには、同じカテゴリ名が設定されます。</p> </td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/personalization</code></td>
   <td><code>/libs/cq/personalization/clientlibs/personalization</code></td>
   <td><p>これらは従来のクライアントライブラリです。インプレースアップグレード時に従来の設定がそのまま維持されます。</p> <p>新しいクライアントライブラリには、同じカテゴリ名が設定されます。</p> </td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/searchpromote</code></td>
   <td><code>/libs/cq/searchpromote/clientlibs/searchpromote</code></td>
   <td><p>これらは従来のクライアントライブラリです。インプレースアップグレード時に従来の設定がそのまま維持されます。</p> <p>新しいクライアントライブラリには、同じカテゴリ名が設定されます。</p> </td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/foundation/target</code></td>
   <td><code>/libs/cq/target/clientlibs/target</code></td>
   <td><p>これらは従来のクライアントライブラリです。インプレースアップグレード時に従来の設定がそのまま維持されます。</p> <p>新しいクライアントライブラリには、同じカテゴリ名が設定されます。</p> </td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/address</code></td>
   <td><code>/libs/cq/address/clientlibs</code></td>
   <td>新しいクライアントライブラリには、同じカテゴリ名が設定されます。</td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation</code></td>
   <td><code>/libs/wcm/foundation/clientlibs</code></td>
   <td>従来のクライアントライブラリ。インプレースアップグレード時に従来の設定がそのまま維持されます。新しいクライアントライブラリでは、新旧のクライアントライブラリがマージされないように、同じカテゴリ名を持ち、「<strong>replaces</strong>」プロパティが指定されています。</td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Sites</td>
   <td><code>/etc/clientlibs/wcm/foundation/grid/grid_base.less</code></td>
   <td><p><code>/libs/wcm/foundation/clientlibs/grid/grid_base.less</code></p> </td>
   <td><p>インプレースアップグレード時に従来のファイル（/etc/clientlibs/wcm/...）は維持され、自動的には削除されません。そのため、従来の /etc/clientlibs/wcm/foundation/grid/grid_base.less への参照は引き続き有効になります。</p> <p><em>この LESS ファイルは、例外的に、クライアントライブラリのカテゴリではなく、LESS @import ステートメントを使用して絶対パスで参照されます。</em></p> <p>「grid_base.less」を参照するカスタム LESS が存在しないファイルを指している場合、編集可能なテンプレートのレイアウトモードが機能しなくなり、おこなわれた変更内容は反映されません（すべてのコンポーネントはページの全幅となります）。</p> </td>
   <td>（移動された grid_base.less ファイルを参照するすべての LESS ファイルの）カスタムコード内のすべての参照を新しい場所を指すように更新し、従来の場所を削除します。</td>
  </tr>
 </tbody>
</table>

これらは、前の節には該当しないその他の再構築の内容です。

### 拡張戦略 {#extensibility-strategy-2}

サポートされる拡張モデルについては、表の各行を参照してください。この節のコンテンツは、通常、拡張されません。

## その他 {#miscellaneous}

<table>
 <tbody>
  <tr>
   <td><strong>解決策</strong></td>
   <td><strong>前の場所</strong><br /> </td>
   <td><strong>新しい場所</strong></td>
   <td><strong>後方互換性のアプローチ</strong></td>
   <td><strong>最新モデルに合わせるための要件</strong></td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/designs/fd/fp</code></td>
   <td><code>/libs/fd/fp</code></td>
   <td><p>従来の AEM Forms ポータルの標準テンプレート。これらのテンプレートは、インプレースアップグレード後に /etc にそのまま残ります。</p> <p>In the template listing, the word<em> "deprecated</em>" will be added to the template title to differentiate them with the newer templates.</p> </td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Forms</td>
   <td><code>/etc/aep</code></td>
   <td><code>/var/fd/content/annotations</code></td>
   <td>従来の Correspondence Management の注釈ファイル。直接利用するものではありません。クリーンアップフィルターを使用してアップグレード後にクリーンアップされます。</td>
   <td>従来の場所は、クリーンアップフィルターを使用してアップグレード後にクリーンアップされます。</td>
  </tr>
  <tr>
   <td>すべて</td>
   <td><code>/etc/tags</code></td>
   <td><code>/content/cq:tags</code></td>
   <td>タグマネージャー API では、従来の場所と新しい場所の両方がサポートされます。JCR タグマネージャーファクトリ OSGi コンポーネントが開始されると、アップグレードされたインスタンスまたは従来のインスタンスのどちらで実行されているかが検出され、適切な場所が使用されます。<br /> </td>
   <td><p>新しいモデルに合わせるには、以下の手順に従います。</p>
    <ol>
     <li>古いモデル(<code>/etc/tags</code>)への参照を新しいモデル(<code>/content/cq:tags</code>)に置き換えるには、 <code>tagID.</code></li>
     <li>CRXDE Lite にログインします。</li>
     <li>タグをからに移動しま <code>/etc/tags</code> す。 <code>/content/cq:tags</code></li>
     <li>OSGiコンポーネントの再起動 <code class="code">com.day.cq.tagging.impl.JcrTagManagerFactoryImpl.
        </code></li>
    </ol> <p> </p> </td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>インフライトワークフローの処理では<br />従来の場所が使用されます。新しいワークフローでは、 <code>/var.</code></td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>すべて</td>
   <td><code>/etc/workflow/scripts</code></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
   <td><p>Existing Workflow Model Steps that reference workflow scripts in the legacy location at <code>/etc/workflow/scripts</code> will continue to point to these scripts after the upgrade, and execute properly.</p> <p>ワークフローステップ（プロセス、分割など）を作成する AEM UI では、no longer lists scripts under <code>/etc/workflow/scripts</code> in the drop-down used select to workflow scripts.</p> </td>
   <td><p>これらのスクリプトを利用するワークフローは、関連するワークフロープロセスステップを AEM で編集しない場合は、引き続き想定どおりに動作します。</p> <p>ただし、ステップを編集する場合を含め、後方互換性を完全に確保するために、お客様がアップグレードした後に以下の手動による処理が必要となります。</p>
    <ul>
     <li>The scripts must be moved from <code>/etc/workflow/scripts</code> to <code>/apps/workflow/scripts.</code></li>
     <li>Any<strong> </strong>references to <code>/etc/workflow/scripts</code> in workflow model steps must be updated to reference the new <code>/apps/workflow/scripts</code> location.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/replication/treeactivation</code></td>
   <td><code>/libs/replication/treeactivation</code></td>
   <td>ClassicUI ユーティリティページは、アップグレード時にそのまま残されます。</td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Assets</td>
   <td><code>/etc/dam/jobs</code></td>
   <td><code>/var/dam/jobs</code></td>
   <td><p>AEM Assets のダウンロードアクションの呼び出しに対して生成される zip ファイルを保持するための一時的な場所。</p> <p>クライアントがアセットのダウンロードを要求した場合、新しい場所にファイルが生成されるので、更新の必要はありません。</p> </td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/products</code></td>
   <td><code>/var/commerce/products</code></td>
   <td><p>古いコンテンツはそのまま残り、アップグレード後も使用できます。</p> <p>新しい場所への移行のための遅延移行タスクが用意されています。</p> </td>
   <td><p>移行は、遅延移行タスクを使用して実行します。 <code>CQ64CommerceMigrationTask.</code></p> <p>以下の手順が実行されます。</p>
    <ul>
     <li>新しい場所を指すように古い場所の参照が変更されます。</li>
     <li>古い場所から新しい場所にコンテンツが移動されます。</li>
     <li><p>システム全体で最終的に新しい場所が利用されるように、古い場所が削除されます。</p> </li>
    </ul> <p>タスクの対象となる場所は以下のとおりです。</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>大規模なカタログでは、以下の Java システムプロパティを AEM に渡して、Commerce 移行タスクを個別に実行することをお勧めします。</p>
    <ul>
     <li>プロパティ名: <code>com.adobe.upgrade.forcemigration</code></li>
     <li>プロパティ値: <code>com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></li>
    </ul> <p>移行後、AEM の再起動が必要です。</p> </td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/orders</code></td>
   <td><code>/var/commerce/orders</code></td>
   <td><p>古いコンテンツはそのまま残り、アップグレード後も使用できます。</p> <p>新しい場所への移行のための遅延移行タスクが用意されています。</p> </td>
   <td>See the description above for <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/collections</code></td>
   <td><code>/var/commerce/collections</code></td>
   <td><p>古いコンテンツはそのまま残り、アップグレード後も使用できます。</p> <p>新しい場所への移行のための遅延移行タスクが用意されています。</p> </td>
   <td>See the description above for <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/classifications</code></td>
   <td><code>/var/commerce/classifications</code></td>
   <td>アクションは必要ありません。</td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/shipping-methods</code></td>
   <td><code>/var/commerce/shipping-methods</code></td>
   <td><p>古いコンテンツはそのまま残り、アップグレード後も使用できます。</p> <p>新しい場所への移行のための遅延移行タスクが用意されています。</p> </td>
   <td>See the description above for <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>AEM Commerce</td>
   <td><code>/etc/commerce/payment-methods</code></td>
   <td><code>/var/commerce/payment-methods</code></td>
   <td><p>古いコンテンツはそのまま残り、アップグレード後も使用できます。</p> <p>新しい場所への移行のための遅延移行タスクが用意されています。</p> </td>
   <td>See the description above for <code>/etc/commerce/products</code>.</td>
  </tr>
  <tr>
   <td>すべての </td>
   <td><code>/etc/taskmanagement</code></td>
   <td><code>/var/taskmanagement</code></td>
   <td><p>新しいタスクは、 <code>/var/taskmanagement</code></p> <p>従来の場所にある既存のタスクは、引き続き AEM インボックスに表示されます。</p> </td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>すべて</td>
   <td><code>/etc/workflow/packages</code></td>
   <td><code>/var/workflow/packages</code></td>
   <td><p>AEM Package Managerで作成されたAEMパッケージは、 <code>/etc/workflow/packages.</code></p> <p>AEMサイトとワークフローで作成された他のパッケージは、引き続き<code>/var/workflow/packages.</code></p> <p>Packages found in both <code>/etc/workflow/packages</code> and <code>/var/workflow/packages</code> can still be edited via AEM's Package Manager. </p> </td>
   <td><p>アクションは必要ありません。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>すべて</td>
   <td><code>/etc/workflow/instances</code></td>
   <td><code>/var/workflow/instances</code></td>
   <td>New workflow instances will be created under <code>/var</code> automatically.</td>
   <td>アクションは必要ありません。</td>
  </tr>
  <tr>
   <td>すべて</td>
   <td><code>/etc/commerce/searchpromote</code></td>
   <td><code>/var/cq/searchpromote</code></td>
   <td><p>Search&amp;Promote のフィードコンテンツの新しい場所。</p> <p>古い URL も引き続き動作し、リクエストはサーブレットフィルターによって新しい場所に転送されます。</p> </td>
   <td>アクションは必要ありません。<br /><br /> </td>
  </tr>
  <tr>
   <td>すべて</td>
   <td><code>/etc/dtm-hook</code></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
   <td><p>DTM Web フックの新しい場所。</p> <p>古い URL も引き続き動作し、リクエストはサーブレットフィルターによって新しい場所に転送されます。</p> </td>
   <td>アクションは必要ありません。<br /><br /> </td>
  </tr>
 </tbody>
</table>

