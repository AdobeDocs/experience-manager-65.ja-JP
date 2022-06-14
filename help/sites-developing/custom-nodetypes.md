---
title: カスタムノードタイプ
seo-title: Custom Node Types
description: AEM は、Sling をベースにして JCR リポジトリを使用し、両方から提供されるノードタイプを使用しますが、様々なカスタムノードタイプも提供しています。
seo-description: AEM is based on Sling and uses a JCR repository with node types offered by both, but AEM also provides a range of custom node types
uuid: f2022504-e433-4b42-9cc1-eef41086483a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: aae186eb-e059-4a9d-b02d-86a86c86589d
exl-id: bfd50aa9-579e-47d5-997d-ec764c782497
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '1877'
ht-degree: 100%

---

# カスタムノードタイプ{#custom-node-types}

AEM は Sling ベースであり JCR リポジトリを使用しているので、これらが提供する次のようなノードタイプを利用できます。

* [JCR ノードタイプ](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling ノードタイプ](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

これらに加えて、AEM では様々なカスタムノードタイプも提供しています。

## 監査 {#audit}

### cq:AuditEvent {#cq-auditevent}

**説明**

監査イベントノードのノードタイプを定義します。

* `@prop cq:time`
* `@prop cq:userid`
* `@prop cq:path`
* `@prop cq:type`
* `@prop cq:category`
* `@prop cq:properties`

**定義**

* `[cq:AuditEvent]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
* `- cq:time (date)`
* `- cq:userid (string)`
* `- cq:path (string)`
* `- cq:type (string)`
* `- cq:category (string)`
* `- cq:properties (binary)`

## コメント {#comment}

### cq:Comment {#cq-comment}

**説明**

コメントノードのノードタイプを定義します。

* `@prop userIdentifier`

**定義**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:CommentAttachment {#cq-commentattachment}

**説明**

`commentattachment` ノードのノートタイプを定義します。

**定義**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:CommentContent {#cq-commentcontent}

**説明**

コメントコンテンツノードのノードタイプを定義します。

**定義**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq:GeoLocation {#cq-geolocation}

**説明**

地理的な位置を 10 進数の度（DD）で定義する mixin です。

* `@prop latitude` - 倍精度浮動小数点数としてエンコードされた緯度（十進角を使用）。
* `@prop longitude` - 倍精度浮動小数点数としてエンコードされた経度（十進角を使用）

**定義**

* `[cq:GeoLocation] mixin`
* `- latitude (double)`
* `- longitude (double)`

### cq:Trackback {#cq-trackback}

**説明**

トラックバックノードのノードタイプを定義します。

**定義**

* `[cq:Trackback] > mix:title, mix:created, mix:language, nt:unstructured`

## コア {#core}

### cq:Page {#cq-page}

**説明**

デフォルトの CQ ページを定義します。

* `@node jcr:content` - ページのプライマリコンテンツ。

**定義**

* `[cq:Page] > nt:hierarchyNode orderable`
   * `+ jcr:content (nt:base) = nt:unstructured copy primary`
   * `+ * (nt:base) = nt:base version`

### cq:PseudoPage {#cq-pseudopage}

**説明**

ノードを疑似ページとしてマークする mixin タイプを定義します。この設定により、ノードをページおよび WCM 編集をサポートするように適応させることができます。

**定義**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**説明**

ページコンテンツのデフォルトノードと、WCM によって使用される最小限のプロパティを定義します。

* `@prop jcr:title` - ページのタイトル。
* `@prop jcr:description` - このページの説明。
* `@prop cq:template` - ページの作成に使用されるテンプレートへのパス。
* `@prop cq:allowedTemplates` - 許可されたテンプレートへのパスを定義するために使用する正規表現のリスト。
* `@prop pageTitle`- 通常、`<title>` タグで表示されるタイトル。
* `@prop navTitle` - 通常、ナビゲーション内で使用されるタイトル。
* `@prop hideInNav` - ナビゲーション内でこのページを非表示にするかを指定します。
* `@prop onTime` - このページが有効になる時刻。
* `@prop offTime` - このページが無効になる時刻。
* `@prop cq:lastModified` - ページ（またはその段落）が前回変更された日付。
* `@prop cq:lastModifiedBy` - ページ（またはその段落）を前回変更したユーザー。
* `@prop jcr:language` - ページコンテンツの言語。

>[!NOTE]
>
>ページコンテンツでのこのタイプの使用は必須ではありません。

**定義**
* `[cq:PageContent] > nt:unstructured, mix:title, mix:created, cq:OwnerTaggable, sling:VanityPath, cq:ReplicationStatus, sling:Resource orderable`
   * `- cq:template (string)`
   * `- cq:allowedTemplates (string) multiple`
   * `- pageTitle (string)`
   * `- navTitle (string)`
   * `- hideInNav (boolean)`
   * `- onTime (date)`
   * `- offTime (date)`
   * `- cq:lastModified (date)`
   * `- cq:lastModifiedBy (string)`
   * `- cq:designPath (string)`
   * `- jcr:language (string)`

### cq:Template {#cq-template}

**説明**

CQ テンプレートを定義します。

* `@node jcr:content` - 新しいページのデフォルトコンテンツ。
* `@node icon.png` - 特有のアイコンを保持するファイル。
* `@node thumbnail.png` - 特有のサムネール画像を保持するファイル。
* `@node workflows` - ワークフロー設定を自動で割り当てます。設定は、次の構造に従います。
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents` - 親テンプレートとして許可されるテンプレートへのパスを定義するための正規表現パターン。
* `@prop allowedChildren` - 子テンプレートとして許可されるテンプレートへのパスを定義するための正規表現パターン。
* `@prop ranking` - ページ作成ダイアログでのテンプレートリスト内の位置。

**定義**

* `[cq:Template] > nt:hierarchyNode, mix:title`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ jcr:content (nt:base) copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `+ workflows (nt:base) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `- ranking (long)`

### cq:Component {#cq-component}

**説明**

CQ コンポーネントを定義します。

* `@prop jcr:title` - コンポーネントのタイトル。
* `@prop jcr:description` - コンポーネントの説明。
* `@node dialog` - プライマリダイアログ。
* `@prop dialogPath` - プライマリダイアログのパス（dialog の代替）。
* `@node design_dialog` - デザインダイアログ。
* `@prop cq:cellName` - デザインセルの名前。
* `@prop cq:isContainer` - これがコンテナコンポーネントであるかどうかを示します。 これにより、パス名の代わりに子コンポーネントのセル名が強制的に使用されます。例えば、`parsys` は、コンテナコンポーネントです。この値が定義されていない場合、チェックは `cq:childEditConfig` の存在に基づいて行われます。
* `@prop cq:noDecoration` - true の場合、このコンポーネントをインクルードする際に装飾用の `div` タグは描画されません。
* `@node cq:editConfig` - 編集バーのパラメーターを定義する設定。
* `@node cq:childEditConfig` - 子コンポーネントによって継承される編集設定。
* `@node cq:htmlTag` - コンポーネントがインクルードされる際に「周囲の」`div` タグに追加される追加タグ属性を定義します。
* `@node icon.png` - 特有のアイコンを保持するファイル。
* `@node thumbnail.png` - 特有のサムネール画像を保持するファイル。
* `@prop allowedParents` - 親コンポーネントとして許可されるコンポーネントのパスを定義するための正規表現パターン。
* `@prop allowedChildren` - 子コンポーネントとして許可されるコンポーネントのパスを定義するための正規表現パターン。
* `@node virtual` - コンポーネントのドラッグ＆ドロップに使用される仮想コンポーネントを反映するサブノードが含まれます。
* `@prop componentGroup` - コンポーネントグループの名前。コンポーネントのドラッグ＆ドロップで使用されます。
* `@node cq:infoProviders` - サブノードが含まれます。各サブノードには、`PageInfoProvider` を参照するプロパティ `className` があります。

**定義**

* `[cq:Component] > nt:folder, mix:title, sling:ResourceSuperType`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ dialog (nt:base) = nt:unstructured copy`
   * `- dialogPath (string)`
   * `+ design_dialog (nt:base) = nt:unstructured copy`
   * `- cq:cellName (string)`
   * `- cq:isContainer (boolean)`
   * `- cq:noDecoration (boolean)`
   * `+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:childEditConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:htmlTag (nt:base) = nt:unstructured copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `+ virtual (nt:base) = sling:Folder copy`
   * `- componentGroup (string)`
   * `+ cq:infoProviders (nt:base) = nt:unstructured copy`

### cq:ComponentMixin {#cq-componentmixin}

**説明**

CQ コンポーネントを mixin タイプとして定義します。

**定義**

`[cq:ComponentMixin] > cq:Component mixin`

### cq:EditConfig {#cq-editconfig}

**説明**

「編集バー」用の設定を定義します。

* `@prop cq:dialogMode` - ダイアログのモード：
   * `floating` - 通常のフローティングダイアログの場合
   * `inline` - インライン編集
   * `auto` - 自動検出（空きスペースによって異なる）
* `@node cq:inplaceEditing` - このコンポーネントのインプレース編集設定。
* `@prop cq:layout` - 編集バーのレイアウト：
   * `editbar` - 編集バー
   * `rollover` - ロールオーバーフレーム
   * `auto` - 自動検出
* `@node cq:formParameters` - ダイアログフォームに追加する追加パラメーター。
* `@prop cq:actions` - アクションのリスト（編集バーのボタンまたはメニュー項目）。
* `@node cq:actionConfigs` - 編集バーまたはメニュー項目のウィジェット設定。
* `@prop cq:emptyText` - 視覚的なコンテンツがない場合に表示されるテキスト。
* `@node cq:dropTargets` - `{@link cq:DropTargetConfig}` ノードのコレクション。

**定義**

* `[cq:EditConfig] > nt:unstructured, nt:hierarchyNode orderable`
   * `- cq:dialogMode (string) < 'auto', 'floating', 'inline'`
   * `- cq:layout (string) < 'editbar', 'rollover', 'auto' + cq:formParameters (nt:base) = nt:unstructured`
   * `- cq:actions (string) multiple`
   * `+ cq:actionConfigs (nt:base) = nt:unstructured`
   * `- cq:emptyText (string)`
   * `+ cq:dropTargets (nt:base) = nt:unstructured`
   * `+ cq:listeners (nt:base) = cq:EditListenersConfig`

### cq:DropTargetConfig {#cq-droptargetconfig}

**説明**

コンポーネントの 1 つのドロップターゲットを設定します。このノードの名前が、ドラッグ＆ドロップの ID として使用されます。

* `@prop accept` - このドロップターゲットによって受け入れられる MIME タイプのリスト。例：`["image/*"]`
* `@prop groups` - ソースを受け入れるドラッグ＆ドロップグループのリスト。
* `@prop propertyName` - 参照を格納するために使用されるプロパティの名前。

**定義**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq:VirtualComponent {#cq-virtualcomponent}

**説明**

仮想 CQ コンポーネントを定義します。これらは現時点で、新しいコンポーネントのドラッグ＆ドロップウィザードでのみ使用されます。

* `@prop jcr:title` - このコンポーネントのタイトル。
* `@prop jcr:description` - このコンポーネントの説明。
* `@node cq:editConfig` - この編集バーのパラメーターを定義する編集設定。
* `@node cq:childEditConfig` - 子コンポーネントによって継承される編集設定。
* `@node icon.png` - 特有のアイコンを保持するファイル。
* `@node thumbnail.png` - 特有のサムネール画像を保持するファイル。
* `@prop allowedParents` - 親コンポーネントとして許可されるコンポーネントのパスを定義するための正規表現パターン。
* `@prop allowedChildren` - 子コンポーネントとして許可されるコンポーネントのパスを定義するための正規表現パターン。
* `@prop componentGroup` - コンポーネントのドラッグ＆ドロップ用のコンポーネントグループの名前。

**定義**

`[cq:VirtualComponent] > nt:folder, mix:title`
`- * (undefined)`
`- * (undefined) multiple`
`+ * (nt:base) = nt:base multiple version`
`+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
`+ icon.png (nt:file) copy`
`+ thumbnail.png (nt:file) copy`
`- allowedParents (string) multiple`
`- allowedChildren (string) multiple`
`- componentGroup (string)`

### cq:EditListenersConfig {#cq-editlistenersconfig}

**説明**

編集イベントに対して実行される、（クライアント側の）リスナーを定義します。値は有効なクライアント側リスナーの関数を参照しているか、次の事前定義済みのショートカットが格納されている必要があります。

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate` - コンポーネントが作成された後に呼び出されます。
* `@prop afteredit` - コンポーネントが編集（変更）された後に呼び出されます。
* `@prop afterdelete` - コンポーネントが削除された後に呼び出されます。
* `@prop afterinsert` - コンポーネントがこのコンテナに追加された後に呼び出されます。
* `@prop afterremove` - コンポーネントがこのコンテナから削除された後に呼び出されます。
* `@prop aftermove` - コンポーネントがこのコンテナ内に移動された後に呼び出されます。

**定義**

* `[cq:EditListenersConfig]`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `+ &ast; (nt:base) = nt:base multiple version`
   * `- aftercreate (string)`
   * `- afteredit (string)`
   * `- afterdelete (string)`
   * `- afterinsert (string)`
   * `- afterremove (string)`
   * `- aftermove (string)`

## DAM {#dam}

### dam:AssetContent {#dam-assetcontent}

**説明**

DAM アセットのコンテンツ。

**定義**

* `[dam:AssetContent] > nt:unstructured`
   * `+ metadata (nt:unstructured)`
   * `+ renditions (nt:folder)`

### dam:Asset {#dam-asset}

**説明**

DAM アセット。

**定義**

`[dam:Asset] > nt:hierarchyNode`
`+ jcr:content (dam:AssetContent) = dam:AssetContent copy primary`
`+ * (nt:base) = nt:base version`

### dam:Thumbnail {#dam-thumbnail}

**説明**

DAM アセットを表すサムネール。

**定義**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## 配信コンテナリスト {#delivery-container-list}

### cq:containerList {#cq-containerlist}

**説明**

コンテナリスト。

**定義**

* `[cq:containerList]`
   * `mixin`

## 配信ページ {#delivery-page}

### cq:Cq4PageAttributes {#cq-cq-pageattributes}

**説明**

`cq:attributes` は、ContentBus バージョンタグ用のノードタイプです。このノードには一連のプロパティのみが含まれ、そのうち 3 つのプロパティが「created」、「csd」および「timestampe」として事前定義されています。

* `@prop created (long) mandatory copy` - バージョン情報の作成時のタイムスタンプ。通常は、以前のバージョンのチェックイン時またはページ作成時。
* `@prop csd (string) mandatory copy` - csd 標準属性。ページノードの cq:csd プロパティのコピー。
* `@prop timestamp (long) mandatory copy` - 前回のバージョン変更のタイムスタンプ。通常はチェックイン時。
* `@prop * (string) copy` - 親ノードによってバージョン管理される追加属性。

**定義**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq:Cq4ContentPage {#cq-cq-contentpage}

**説明**

ノードタイプ `cq:contentPage` には、ContentBus コンテンツページのプロパティと子ノードの定義が含まれます。この mixin タイプがタイプ `cq:page` のノードに追加されたときにのみ、ノードは ContentBus コンテンツページになります。

`cq:Cq4ContentPage` の項目は次のとおりです。

* `@prop cq:csd` - ページの ContentBus CSD。
* `@node cq:content` - ページのコンテンツ。この子ノードは、ページノードが「コンテンツなしで存在」または「削除済み」の状態の場合には存在しません。
* `@node cq:attributes` - ページ属性のリスト（以前の名称はバージョンタグ）。cq:contentPage タイプの場合、このノードは必須です。属性ノードは、ページノードがバージョン設定されるときにバージョン設定されます。

**定義**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## インポーター {#importer}

### cq:PollConfig {#cq-pollconfig}

**説明**

ポールの設定。

* `@prop source (String) mandatory` - データソース URI。必須であり、空にはできません。
* `@prop target (String)` - データソースから取得されたデータが保存されるターゲットの場所。これはオプションであり、デフォルトは cq:PollConfig ノードです。
* `@prop interval (Long)` - データソースから新しいデータまたは更新されたデータをポーリングする間隔（秒）。これはオプションであり、デフォルトでは 30 分（1800 秒）に設定されています。
* [Adobe Experience Manager の Custom Data Importer Service の作成](https://helpx.adobe.com/jp/experience-manager/using/polling.html)

**定義**

* `[cq:PollConfig]`
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**説明**

ポール設定ノードを簡単に作成するための便利なプライマリノードタイプ。

**定義**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## 場所 {#location}

### cq:GeoLocation {#cq-geolocation-1}

**説明**

地理的な場所を十進角（DD）で定義した mixin。

* `@prop latitude` - 倍精度浮動小数点数としてエンコードされた緯度（十進角を使用）。
* `@prop longitude` - 倍精度浮動小数点数としてエンコードされた経度（十進角を使用）。

**定義**

* `[cq:GeoLocation]`
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## メーラー {#mailer}

### cq:mailerMessage {#cq-mailermessage}

**説明**

MailerService ノードタイプ。メーラーは、この mixin をメッセージ定義のルートノードとして持つノードを使用します。

**定義**

* `[cq:mailerMessage]`
   * `mixin`
   * `- messageStatus (string)`
   * `= 'new'`
   * `mandatory autocreated`

## MSM {#msm}

### cq:LiveRelationship {#cq-liverelationship}

**説明**

LiveSyncCancelled mixin を定義します。プライマリソース（制御側）ノードとライブコピー（被制御側）ノードは、LiveRelationship を介して仮想的にリンクできます。

**定義**

* `[cq:LiveRelationship] mixin`
   * `- cq:lastRolledout (date)`
   * `- cq:lastRolledoutBy (string)`
   * `- cq:sourceUUID (string)`

### cq:LiveSync {#cq-livesync}

**説明**

LiveSync mixin を定義します。ノードがプライマリソース（制御側）ノードおよびライブコピー（被制御側）ノードと LiveRelationship に関係している場合、そのノードは LiveSync としてマークされます。

* `@prop cq:master` - LiveRelationship のプライマリソース（制御側）のパス。
* `@prop cq:isDeep` - 関係が子にも利用できるかどうかを定義します。
* `@prop cq:syncTrigger` - 同期がトリガーされるタイミングを定義します。
* `@node * LiveSyncAction` - 同期時に実行するアクション

**定義**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq:LiveSyncCancelled {#cq-livesynccancelled}

**説明**

LiveSyncCancelled mixin を定義します。親の 1 つが原因で LiveRelationship に関与している可能性のあるライブコピー（被制御側）ノードの LiveSync 動作をキャンセルします。

* `@prop cq:isCancelledForChildren` - LiveSync がキャンセルされるかどうかを定義します（子に対しても）。

**定義**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq:LiveSyncAction {#cq-livesyncaction}

**説明**

LiveSync に関連付けられた LiveSyncAction を定義します。

* `@prop name` - アクション名
* `@prop value` - アクション値

**定義**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq:LiveSyncConfig {#cq-livesyncconfig}

**説明**

Live Sync 設定。

**定義**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

AEM 5.4 ではリストの最後に以下を追加：

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq:BlueprintAction {#cq-blueprintaction}

**説明**

ブループリントアクション

**定義**

* `[cq:BlueprintAction] > nt:unstructured`

## Platform {#platform}

### cq:Console {#cq-console}

**説明**

コンソールノードのノードタイプを定義します。

**定義**

* `[cq:Console] > sling:VanityPath, mix:title`
   * `mixin`

## レプリケーション {#replication}

### cq:ReplicationStatus {#cq-replicationstatus}

**説明**

レプリケーションステータス情報 mixin を定義します。

* `@prop cq:lastPublished` - 前回ページが公開された日付（使用されません）。
* `@prop cq:lastPublishedBy` - 前回ページを公開したユーザー（使用されません）。
* `@prop cq:lastReplicated` - 前回ページがレプリケートされた日付。
*  `@prop cq:lastReplicatedBy` - 前回ページをレプリケートしたユーザー。
* `@prop cq:lastReplicationAction` - レプリケーションアクション：アクティベートまたはアクティベート解除。
* `@prop cq:lastReplicationStatus` - レプリケーションステータス（使用されません）。

**定義**

* `[cq:ReplicationStatus]`
   * `mixin`
   * `- cq:lastPublished (date) ignore`
   * `- cq:lastPublishedBy (string) ignore`
   * `- cq:lastReplicated (date) ignore`
   * `- cq:lastReplicatedBy (string) ignore`
   * `- cq:lastReplicationAction (string) ignore`
   * `- cq:lastReplicationStatus (string) ignore`

## セキュリティ {#security}

### cq:ApplicationPrivilege {#cq-applicationprivilege}

**説明**

アプリケーション権限を定義します。

**定義**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl}

**説明**

アプリケーション権限の ACL を定義します。

* `@prop cq:isPathDependent`
* `@node * ACEs`

**定義**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace}

**説明**

アプリケーション権限の ACE を定義します。

* `@prop path`
* `@prop deny`

**定義**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

### cq:ApplicationPrivilege {#cq-applicationprivilege-1}

**説明**

アプリケーション権限を定義します。

**定義**

* `[cq:ApplicationPrivilege] mixin`

### cq:PrivilegeAcl {#cq-privilegeacl-1}

**説明**

アプリケーション権限の ACL を定義します。

* `@prop cq:isPathDependent`
* `@node * ACEs`

**定義**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq:PrivilegeAce {#cq-privilegeace-1}

**説明**

アプリケーション権限の ACE を定義します。

* `@prop path`
* `@prop deny`

**定義**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## サイトインポーター {#site-importer}

### cq:ComponentExtractorSource {#cq-componentextractorsource}

**説明**

コンポーネントエクストラクターによって開くことができるファイルをマークする mixin タイプを定義します。

**定義**

`[cq:ComponentExtractorSource] mixin`

## タグ付け {#tagging}

### cq:Tag {#cq-tag}

**説明**

1 つのタグを定義しますが、複数のタグを含めて分類を作成することもできます。

**定義**

* `[cq:Tag] > nt:base, mix:title`
   * `- sling:resourceType (String)`
   * `- * (undefined) multiple`
   * `- * (undefined)`
   * `+ * (nt:base) = cq:Tag version`

### cq:Taggable {#cq-taggable}

**説明**

タグ付け可能コンテンツ用の抽象基本 mixin。

* `@node cq:tags`

**定義**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq:OwnerTaggable {#cq-ownertaggable}

**説明**

作成者または所有者のみにコンテンツへのタグ付けを許可します（モデレート／管理されたタグ付け）。

**定義**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq:UserTaggable {#cq-usertaggable}

**説明**

すべてのユーザー／公開 Web サイトで、cq:userContent 内部で使用されているコンテンツ（Web 2.0 スタイル）にタグを付けることができます。

**定義**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq:AllowsUserContent {#cq-allowsusercontent}

**説明**

ユーザーが変更できる `cq:userContent` サブノードを追加します。各ユーザーには、独自の `cq:userContent/<userid>` サブノード（通常、`cq:UserTaggable` mixin が含まれる）が与えられます。

**定義**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

`cq:userContent` ツリーをさらに明示的に定義する拡張バリアント

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq:UserContent {#cq-usercontent}

**説明**

ユーザーが変更できます。

**定義**

* `[cq:UserContent] > nt:unstructured`
   * `// userids`
   * `+ * (cq:UserData)`
   * `// other content`
   * `+ * (nt:base)`

### cq:UserData {#cq-userdata}

**説明**

ユーザーデータ

**定義**

* `[cq:UserData] > nt:unstructured, cq:UserTaggable`

## ウィジェット {#widgets}

### cq:ClientLibraryFolder {#cq-clientlibraryfolder}

**説明**

クライアントライブラリフォルダー

**定義**

* `[cq:ClientLibraryFolder] > sling:Folder`
   * `- categories (string) multiple`
   * `- dependencies (string) multiple`

### cq:Widget {#cq-widget}

**説明**

ウィジェット

**定義**

* `[cq:Widget] > nt:unstructured orderable`
   * `- xtype (string)`
   * `- name (string)`
   * `- title (string)`
   * `+ items (nt:base) = cq:WidgetCollection copy`

### cq:WidgetCollection {#cq-widgetcollection}

**説明**

ウィジェットのコレクション

**定義**

* `[cq:WidgetCollection] > nt:unstructured`
   * `orderable`
   * `+ * (cq:Widget) = cq:Widget copy`

### cq:Dialog {#cq-dialog}

**説明**

ダイアログ

**定義**

* `[cq:Dialog] > cq:Widget orderable`

### cq:Panel {#cq-panel}

**説明**

パネル

**定義**

`[cq:Panel] > cq:Widget orderable`

### cq:TabPanel {#cq-tabpanel}

**説明**

タブパネル

**定義**

* `[cq:TabPanel]` > `cq:Panel orderable`
   * `- activeTab (long)`

### cq:Field {#cq-field}

**説明**

フィールド

**定義**

* `[cq:Field] > cq:Widget orderable`
   * `- fieldLabel (string)`
   * `- value (string)`
   * `- ignoreData (boolean)`

## Wiki {#wiki}

### wiki:Topic {#wiki-topic}

**説明**

Wiki トピック

**定義**

* `[wiki:Topic] > nt:unstructured, nt:hierarchyNode, mix:versionable, mix:lockable`
   * `+ * (wiki:Topic) version`
   * `+ wiki:attachments (nt:folder) = nt:folder version`
   * `+ wiki:properties (wiki:Properties) = wiki:Properties copy`
   * `- wiki:text (string) mandatory primary`
   * `- wiki:lastModified (date) mandatory`
   * `- wiki:lastModifiedBy (string) mandatory`
   * `- wiki:topicName`
   * `- wiki:topicTitle`
   * `- wiki:lockedBy`
   * `- wiki:logMessage (string)`
   * `- wiki:quietSave (boolean)`

### wiki:User {#wiki-user}

**説明**

Wiki ユーザー

**定義**

* `[wiki:User] mixin`
   * `- wiki:subscriptions (string) multiple`

### wiki:Properties {#wiki-properties}

**説明**

Wiki のプロパティ

**定義**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## ワークフロー {#workflow}

### cq:Workflow {#cq-workflow}

**説明**

ワークフローインスタンスを表します。

**定義**

* `[cq:Workflow] > nt:base, mix:referenceable`
   * `- modelId (String)`
   * `- modelVersion (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- initiator (String)`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `- sling:resourceType (String) = "cq/workflow/components/instance" mandatory autocreated`
   * `+ workflowStack (nt:unstructured)`
   * `+ wait (nt:unstructured)`
   * `+ orTab (nt:unstructured)`
   * `+ data (cq:WorkflowData)`
   * `+ history (nt:unstructured)`
   * `+ metaData (nt:unstructured)`
   * `+ workItems (nt:unstructured)`

### cq:WorkItem {#cq-workitem}

**説明**

作業項目。

**定義**

* `[cq:WorkItem]`
   * `- assignee (String)`
   * `- workflowId (String)`
   * `- nodeId (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- dueTime (Date)`
   * `- sling:resourceType (String) = "cq/workflow/components/workitem" mandatory autocreated`
   * `+ metaData (nt:unstructured)`

### cq:Payload {#cq-payload}

**説明**

ペイロード

**定義**

* `[cq:Payload]`
   * `- path (Path)`
   * `- uuid (String)`
   * `- jcr:url (String)`
   * `- binary (Binary)`
   * `- javaObject (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq:WorkflowData {#cq-workflowdata}

**説明**

ワークフローデータ

**定義**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq:WorkflowModel {#cq-workflowmodel}

**説明**

ワークフロー設定を自動で割り当てます。この設定は次の構造に従います。
* `workflows`
   * `+ name1`
      * `- cq:path`
      * `- cq:workflowName`
   * `+ workflows (nt:base)`

**定義**

* `[cq:WorkflowModel] > nt:base, mix:versionable`
   * `orderable`
   * `- title (String)`
   * `- description (String)`
   * `- sling:resourceType (String) = "cq/workflow/components/model" mandatory autocreated`
   * `+ nodes (nt:unstructured)`
      * `copy`
   * `+ transitions (nt:unstructured)`
      * `copy`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:WorkflowNode {#cq-workflownode}

**説明**

ワークフローノード

**定義**

* `[cq:WorkflowNode] orderable`
   * `- title (String)`
   * `- description (String)`
   * `- maxIdleTime (long)`
   * `- type (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ metaData (nt:unstructured)`
      * `copy`
   * `+ timeoutConfiguration (nt:unstructured)`
      * `copy`

### cq:WorkflowTransition {#cq-workflowtransition}

**説明**

ワークフロー遷移

**定義**

* `[cq:WorkflowTransition] orderable`
   * `- from (String)`
   * `- to (String)`
   * `- rule (String)`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq:OrTab {#cq-ortab}

**説明**

OR タブ

**定義**

* `[cq:OrTab]`
   * `- workflowId (String) // not compulsory as this node will already be attached to the workflow node`
   * `- nodeId (String)`

### cq:Wait {#cq-wait}

**説明**

待機

**定義**

* `[cq:Wait]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- destNodeId (String)`
   * `- fromNodeId (String)`

### cq:WorkflowStack {#cq-workflowstack}

**説明**

ワークフロースタック

**定義**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq:ProcessStack {#cq-processstack}

**説明**

プロセススタック

**定義**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq:WorkflowLauncher {#cq-workflowlauncher}

**説明**

ワークフローランチャー

**定義**

* `[cq:WorkflowLauncher]`
   * `- nodetype (String)`
   * `- glob (String)`
   * `- eventType (Long)`
   * `- description (String)`
   * `- condition (String)`
   * `- workflow (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
