---
title: AEM 6.5 Service Pack リリースノート
description: Adobe Experience Manager 6.5 Service Pack 3 固有のリリースノート
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 37d0225f69800225e82f253ad9dbab8b2b30ac5e

---


# Adobe Experience Manager 6.5 Service packリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | **Adobe Experience Manager 6.5** |
|---|---|
| バージョン | 6.5.3.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2019 年 12 月 12 日 |
| ダウンロード URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0)、ソフ [トウェア配布](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aem.html#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.3.zip) |

## Adobe Experience Manager 6.5.3.0の機能 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.3.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of 6.5 release in **April 2019**. Adobe Experience Manager (AEM) 6.5の上にインストールできます。

このサービスパックリリースの主なハイライトは次のとおりです。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.10.6 に更新しました。

* Experience Manager Assetsで、Deflate 64アルゴリズムを使用して作成されたZIPアーカイブがサポートされるようになりました。

* 作成日の新しい列（並べ替え可能）が、DAMリストビューおよびリストビューのアセット検索結果に追加されました。

* 「名前」列に基づくアセットの並べ替えがリストビューで有効になりました。

* ダイナミックメディアで、スマート切り抜きビデオアセットがサポートされるようになりました。 スマート切り抜きは、機械学習を中心とした機能で、フレームを移動しながら、シーンの焦点に合わせてビデオを再切り抜きします。

* ダイナミックメディアはスマートイメージングをサポートします。

* AEMワークフ [ローで不在環境設定を](../forms/using/configure-out-of-office-settings.md) 「設定」できます。

* AEMワークフロー [で、「受信トレイ」または](../forms/using/configure-shared-queues-osgi.md) 「受信トレイ」項目を他のユーザーと共有できます。

* バッチモ [ードでのインタラクティブ通信の生成](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

* ContextHubにバンドルされているjQueryのバージョンを3.4.1に更新しました。

### 変更点の一覧 {#list-of-changes}

#### アセット {#assets-6530-enhancements}

**製品の機能強化**

* Experience Manager Assetsで、Deflate 64アルゴリズム(NPR-27573)を使用して作成されたZIPアーカイブがサポートされるようになりました。

* 作成日の新しい列（並べ替え可能）が、DAMリスト表示とリスト表示のアセット検索結果に追加されました(NPR-31312)。

* 「名前」列に基づくアセットの並べ替えがリスト表示で許可されました(NPR-31299)。

* GLB、GLTF、OBJおよびSTLアセットファイルは、DAMのアセットの詳細ページでのアセットのプレビューをサポートします(CQ-4282277)。

* ダイナミックメディアでのチャンクのアップロード中に、チャンクノードに対してReplicationOnModifyListenerイベントがトリガーされます。(CQ-4281279)

* ダイナミックメディアで、スマート切り抜きビデオアセットがサポートされるようになりました。 スマート切り抜きは、機械学習を中心とした機能で、フレームを移動しながらビデオを再切り抜きして、シーンの焦点に合わせます(CQ-4278995)。

* ダイナミックメディアは、スマートイメージング(CQ-4222249)をサポートします。

* クエリパラメーターが要求で渡された場合、検索/参照ビューがFoundationピッカーのデフォルトビューとして設定されました(NPR-31601)。

**安定性および**

* 一部のPDFドキュメントのメタデータが、タイトルの変更時に更新およびPDFに保存されません(NPR-31629)。

* 名前にプラス記号「+」が含まれるアセット(NPR-31547)では、アセットの共有が機能しません。

* デフォルトの検索フォーム「アセット管理者*検索レール」での編集が期待どおりに動作しません(NPR-31502)。

* アセットビューでOmnisearchを使用してアセットを検索する場合、提案が表示されません(NPR-31496)。

* 同じアセットが別のユーザーによって異なるコレクションで参照される場合、参照先のアセットが別の場所に移動しても、コレクション内のアセット参照は更新されません(NPR-31486)。

* 重複するIPTCタグがアセットメタデータ(NPR-31328)に追加されます。

* フィルタレール(NPR-31316)から検索がトリガされると、右上隅の検索結果カウントが正確に更新されません。

* ファイルタイプフィルターで2番目のレベルのチェックボックスの選択を解除すると、すべてのチェックボックスがオフになり、検索バーのテキストが選択/選択解除されたプロパティと同期されません(NPR-31287)。

* すべてのメンバー（ユーザー/グループ）をフォルダーのMembersセクションから削除することはできません。すべてのユーザーを削除しようとすると、ログインしたユーザーがリストに追加されます(NPR-31171)。

* ファイル名にプラス記号「+」が付いたアセットは削除できません(NPR-31162)。

* 「作成」ドロップダウンメニューは、フォルダーを選択する際にトップメニューに表示され、作成オプションとして「フォルダー」が表示されません(NPR-30877)。

* パス上の「Deny jcr:removeChildNodes」と「jcr:removeNode」のACLがユーザーに適用される場合、作成/FileUploadアクション項目が見つかりません(NPR-30840)。

* 特定のmp4アセットがアップロードされると、DAMワークフローが古い状態になり、残りのすべてのワークフローが古い状態になります(NPR-30662)。

* メモリ不足エラーは、（数ギガバイトの）大きなPDFファイルがDAMにアップロードされ、そのサブアセットが処理されるとき(NPR-30614)に発生します。

* アセットのバルク移動が失敗し、警告メッセージが表示される(NPR-30610)。

* Dynamic Media Scene 7ランモード(NPR-31630)で実行されているAEMで、アセットを別のフォルダーに移動すると、アセット名が小文字に変更されます。

* Scene 7の会社名(NPR-31340)と同じ名前のフォルダに存在する画像について、リモート画像セットの編集中にエラーが発生する。

* 参照を含むダイナミックメディアアセットが公開されない(NPR-31180)。

* AEMダイナミックメディア — Scene 7ランモードからScene 7へのアップロードに時間がかかりすぎて完了しません(NPR-31048)。

* 画像アセットに追加されたホットスポットは、アセットの詳細ページのインタラクティブ画像ビューアでは表示されません(NPR-30979)。

* 大量のスリングジョブが作成され、AEM Assets内のアセットに対して行われた操作がScene 7に渡されると、「処理」バナーが再表示されます(NPR-30947)。

* アセットとアセットの言語コピーを作成すると競合が発生し、Scene 7(NPR-30932)にアップロードされません。

* ダイナミックメディアハイブリッドモードで実行されているAEMからダウンロードされたダイナミックレンディションが壊れる（画像コンテンツタイプではなく、コンテンツが「画像が見つかりません」のテキストタイプ）(NPR-30876)。

* Scene 7からDynamic Media - Scene 7実行モードに移行したビデオのサムネールを生成できない。(CQ-4282011)

* 異なるScene7会社IDを使用して、あるインスタンスから別のインスタンスにアセットを移行中にIpsApiExceptionが発生する問題を修正しました。(CQ-4280548)

* サポートされている3DモデルがAEMにインジェストされる場合、3Dアセットのサムネールは情報ではありません(CQ-4283701)。

* 3Dアセットのカメラビューが少ない場合は、スクロールボタンがビューアに表示されます(CQ-4283322)。

* アセットの詳細ページのDimensionalViewerでプレビューした、アップロードされた3Dモデルのコンテナの高さが正しくありません。(CQ-4283309)

* Internet Explorer 11およびSafariのSmartCropVideoViewerではビデオを再生できません。(CQ-4281422)

* ダイナミックメディア — scene7ランモード(CQ-4280384)で実行されているAEMで、1つのフォルダから別のフォルダに複数のアセットを移動するための移動ボタンの使用が失敗する。

* MIMEタイプがMP4以外の場合、アセットの詳細に歪んだビデオが表示される(CQ-4279704)。

* ビデオプロファイルを含むフォルダーに新しく取り込んだビデオは、エンコードの割合が100 %に達した後も、処理状態のままになります。(CQ-4279389)

* フォルダからアセットを移動すると、理想的に必要なジョブ(CQ-4278664)よりも多くのSlingジョブ（Scene 7 API呼び出し）が作成されます。

* 画像セット（またはメディアセット）を作成し、DAMで適切な命名規則を使用して名前を付けると、Scene7で画像セットの名前が小文字に変更されます(CQ-4281112)。

* Scene 7 Migratorが正しく公開状態に設定されない(CQ-4263492)。

* タッチUI検索（Omnisearchで実行）の結果ページが自動的に上にスクロールし、コンテンツフラグメントでのユーザーのスクロール位置が失われます。(CQ-4282898)

* PDFファイルのインデックスが作成されず、内のコンテンツを検索できない(CQ-4278916)

* エラー「ユーザー選択によってグループが一覧表示されていません：「false to equal true」が期待される問題は、異なると共に閉じたユーザーグループを追加す `principalName` る際に `authorizableId` 発生している問題を修正しました。(CQ-4278177)

* アセットUI列ビューに、特定のテナントのDAMルートパスに関係なく、すべてのパスが表示されます。(CQ-4278175)

* アセットセレクターの検索が期待どおりに動作しません。(CQ-4275886)

* レンディションワークフローが失敗する(CQ-4271928)

* 「DAMイベントの削除」は最新の(maxSavedActivities)イベントデータを削除し、以前に作成されたデータを保持します(NPR-31336)。

* タッチUI検索（Omnisearchで実行）の結果ページは自動的に上にスクロールし、ユーザーのスクロール位置が失われます(NPR-31307)。

* すべてを選択した後で、タッチUI(NPR-31118)で一部の項目（フォルダー/個々のアセット）の選択を解除しても、アクションバーとアセット数は更新されません。

* アセットのジョブの詳細をポーリング中に、AEMに例外が表示されます(CQ-4283569)。

* DAMのXSS脆弱性(NPR-31654)。

#### Sites {#sites}

* LiveCopyの継承が壊れている場合、ライブコピーページには、LiveCopyリンクの代わりに言語コピーリンクが表示されます(NPR-30980)。
* 新しいBlueprintの場合、レコード数が40を超えると、最初の40レコードのみが表示されます。 Blueprintでは、残りのレコードに対して空白行が表示されます(NPR-31182)。
* ユーザーがメニューのdescriptionプロパティに日本語または韓国語の文字を追加すると、メニューに日本語および韓国語のテキストに対して歪んだ文字が表示されます。 (NPR-31331).
* リッチテキストエディター(RTE)では、埋め込まれたテーブルをリスト項目として挿入できません(NPR-30879)。
* 初期設定で、Scaffolding Rich Text Editor(RTE)を使用できます。 要素に予期せずインラインフォントサイズを適用します(NPR-31284)。
* ユーザーが左のレールフィールドにフォーカスし、キーボードショートカットを使用してコンテンツを貼り付けると、左のレールフィールドからコピーしたコンテンツではなく、ページエディターのクリップボードのコンテンツが貼り付けられます。
* ユーザがファイルアップロードフィールドをマルチフィールドに追加すると、画像パスはマルチフィールドノード(NPR-30882)ではなくコンポーネントノードに格納されます。
* ResponsiveGridExporter APIは、com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporterインターフェイスを返しません。 com.day.cq.wcm.foundation.model.implパッケージがプライベートパッケージとして宣言されています(NPR-31398)。
* 一部のExperienceFragmentsを含むページがエディター以外のモードで（プレフィックスが付いていない作成者で、または発行者で）開かれると、要求はHTTPステータスエラーコード500(NPR-30743)で終了します。 `editor.html``wcmmode=disabled`
* ユーザーはパスワードを変更したり、自分のプロファイルページにアクセスしたりできません(NPR-31161)。
* ユーザデータを含むJavaScriptファイルがサーバ側で生成される(NPR-30822)。
* AEMオーサリングUIでは、外部コンテンツ(NPR-29745)を使用したフィッシングが可能です。
* AEM 6.5メタデータエディター(NPR-31017)のエクスプレッション言語注入脆弱性。

#### 検索とユーザーインターフェイス {#search-ui-interface}

* 検索結果ページでカード表示からリスト表示に切り替えると、ページがスクロールされるまでに遅延が生じます(NPR-31286)。

* 「すべて選択」チェックボックスは、サイトUIのリスト表示(NPR-31614)で非表示になっています。

* 検索結果ページの「すべて選択」のカウントが正しくありません(NPR-31120)。

* メタデータエディターには、存在しないタグ(NPR-31119)が表示されます。

#### 翻訳 {#translation}

* 翻訳ジョブ(NPR-31270)で「期日」オプションを選択すると、2つのカレンダーポップアップが表示されます。

#### プラットフォーム {#platform}

* Webコンソールの「MIMEタイプ」オプションが機能しません(NPR-31108)。

* シングルサインオン(NPR-31165)を設定する場合、クライアント証明書は受け入れられません。

* Jetty ベースの HTTP サービスのバッファーサイズ設定でアップデートが保存されない。（NPR-30925）

* QueryBuilderで、xpathクエリでorderbyがサ ``fn:name()`` ポートされるようになりました(NPR-31322)。

* AEM 6.3(NPR-31513)からのアップグレード時に、アクティベーションツリーが複製されます。

* 転送された要求は、Sling認証(NPR-30013)中に設定された応答ヘッダーを保持しません。

* ピッカーコンポーネント内での検索が動作しない(NPR-31692)。

* Apache POIとApache Tikaバンドル(NPR-31018)の異なるバージョンが原因で、ZIPファイルをAEM Communitiesの投稿に添付すると、エラーが表示されます。

* このバ ``org.apache.sling.distribution.api`` ンドルは設定マネージャーで非表示になっているので、カスタムバンドル(NPR-31720)では使用できません。

#### プロジェクト {#projects}

* カレンダービューの切り替えが機能しない(NPR-31271)。

#### Brand Portal {#assets-brand-portal}

**製品の機能強化**

* AEM Assetsのアセットソーシングインポートワークフローが変更され、新しく作成したアセットのみがBrand PortalからAEMに取得され、複製を避けるためにNEWフォルダーに既に存在するアセットをスキップします。(CQ-4278527)

**安定性および**

* アセットソーシング機能で新しい貢献度フォルダーを作成すると、正しくないアイコンが表示される(CQ-4282825)。
* 新しい貢献度フォルダーを作成すると、1つまたは両方のサブフォルダー（NEWおよびSHARED）が貢献度フォルダー内に表示されません(CQ-4282424)。
* Brand PortalエンドからContributionフォルダーの新しいアセットを受け取った後に、ユーザーがAEMからBrand Portalに貢献度フォルダーを再公開しようとすると、システムで例外がスローされます。(CQ-4279740)
* 貢献度フォルダー（ネストされたフォルダー）内に貢献度フォルダーを作成することは、複雑さを避けるために禁止されています。(CQ-4278391)
* AEM管理コンソールから読み込んだBrand portalユーザーリスト（.csvファイル）のアップロード時に例外がスローされます。 .csvファイル内の「電子メール」、「FirstName」および「LastName」フィールドのみが必須です(CQ-4278390)。

#### Communities {#communities}

**安定性および**

* グループ管理用のクイックリンク（「開く」、「編集」、「公開」、「削除」の各グループ）は、コミュニティ管理者（グループ管理者/サイト管理者）(NPR-31627)には表示されません。
* 送信されたブログは、ページを手動で更新/再読み込みしない限り表示されません(NPR-31599)。
* 「メンション」機能で使用されるJCRクエリでは、大文字と小文字が区別され、結果を返すのに時間がかかりすぎます(NPR-31475)。
* AEM 6.5 UberJarファイルで例外がスローされ、AEM 6.5 UberJar `cq-social-translation` ファイル(NPR-31186)にバンドルが見つかりません。
* Jackson Databindライブラリがバージョン2.9.9.3に更新され、新しい脆弱性(NPR-30967)に対応しました。
* アクティビティと通知タイトルに一貫性がない。（NPR-30941）
* Communities ブログでページネーションが正しく機能していない。（NPR-30914）
* 分析レポートが AEM のオーサー環境に入力されず、空白ページが表示される（NPR-30913）。

#### Oak {#oak}

* Luceneのインデックスの更新により、作成者サーバーの速度が低下する原因となっています(NPR-31548)。

#### Forms {#forms-6530}

>[!NOTE]
>
>AEM サービスパックには、AEM Forms の修正は含まれません。別の Forms アドオンパッケージを使用して配布されます。さらに、JEE上のAEM Formsの修正を含む累積的インストーラーがリリースされました。 For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

##### Forms アドオンパッケージ {#forms-add-on-package-6530}

**アダプティブフォーム**

* 文字列には、アダプティブフォームのローカライズ中に辞書キーが含まれます(NPR-31110)。

**インタラクティブコミュニケーション**

* **Jacksonライブラリを2.10.0(NPR-31549)にアップグレードした後、MissingNode.toString()** が不正確な結果を返す。

* テキストエディターは、Microsoft wordからコピーしたテキストからスペース文字をランダムに削除します(NPR-31113)。

**Correspondence Management**

* LiveCycle ES4SP1からAEM 6.5(NPR-31615)にレターを移行する際に、キャプションとツールチップが表示されない。

* **レターをドラフトとして保存中に表示される** 、テキストフローのフォーマットはサポートされなくなりました(NPR-30463)。

**ワークフロー**

* 100%のCPU使用率(NPR-31233)が原因でOSGiワークフローが失敗する。

**HTML5 のフォーム**

* XDP フォームの HTML5 プレビューを生成すると、サブフォームのインスタンス追加中にちらつきが表示される。（NPR-30909）

##### JEE上のFormsインストーラー {#forms-jee-installer-6530}

**Forms - ドキュメントサービス**

* .NETプロジェクトでMTOMを使用するSOAP webサービスで、AssemblerServiceClient呼び出しおよびHtmlToPDF2メソッドの例外が表示されます(NPR-4281771)。

**Foundation JEE**

* アクションの設定で、「Invoke a Forms Workflow submit action」(NPR-31478)のプロセス名が読み込まれません。

### 含まれている機能パック {#feature-packs-included-6530}

>[!NOTE]
>
>AEM Forms ユーザーは、AEM サービスパック、累積修正パック、機能パックのいずれかをインストールした後で、AEM Forms アドオンパッケージをインストールすることが不可欠です。

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* AEM FormsはOracle 18c(NPR-29155)をサポートします。

## Install 6.5.3.0 {#install}

**セットアップ要件**

* AEM 6.5.3.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* サービスパックは AEM 6.5 インスタンスから直接アクセスできるパッケージ共有からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.5.3.0 をインストールしてください。
* サービスパックをインストールする前に、AEM インスタンスのスナップショットまたは新規バックアップを必ず作成します。
* インストールする前にインスタンスを再起動してください。これは、インスタンスがまだ更新モードになっている場合（インスタンスが以前のバージョンから更新されたばかりの場合）にのみ必要ですが、インスタンスが長期間実行されていた場合にはお勧めします。

>[!CAUTION]
>
>AEM 6.5.3.0 パッケージを削除またはアンインストールすることはお勧めしません。

### パッケージ共有による Service Pack のインストール {#install-service-pack-via-package-share}

既存の AEM 6.5 インスタンスに Service Pack をインストールするには、次の手順を実行します。

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.3.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0).

1. パッケージマネージャーを使用してダウンロードしたパッケージをインストールします。

>[!NOTE]
>
>**6.5.3.0 のインストール中に、パッケージマネージャー UI のダイアログが途中で終了することがあります。**
>
>そのため、エラーログが安定するのを待ってから、インスタンスにアクセスすることをお勧めします。アップデーターバンドルのアンインストールに関連する特定のログを待ってから、インストールが正常に完了することを確認する必要があります。 通常は、Safari で発生しますが、任意のブラウザーで断続的に発生する可能性があります。

**自動インストール**

実行中のインスタンスに AEM 6.5.3.0 を自動的にインストールするには、次の 2 つの方法があります。

A.パッケージを。.*/crx-quickstart/install* folder while the server is available online. パッケージは自動的にインストールされます。

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.3.0 では、ブートストラップインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ(/system/console/ productinfo)の「インストール済み製品」に更新済みのバージョン文 `Adobe Experience Manager, Version 6.5.3.0` 字列が表示されます。

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. OSGIバンドルorg.apache.jackrabbit.oak-coreはバージョン1.10.6以降です(Webコンソールを使用：/system/console/bundles)。

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>AEM Forms を使用していない場合はスキップしてください。AEM Forms の修正は、個別のアドオンパッケージを介して配信されます。

>[!NOTE]
>
>AEM 6.5.3.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). 古いバージョンのAEM Forms互換パッケージを使用し、AEM 6.5.3.0に更新する場合は、Formsアドオンパッケージのインストール後に、最新バージョンのAEM Forms互換パッケージをインストールします。

1. AEM Service Pack がインストールされていることを確認してください。
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE上のAEM Formsに関する修正は、別のインストーラーを使用して提供されます。

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0007](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0007.html).

#### Workbench インストーラー

これはフルインストーラーなので、パッチバージョンよりもファイルサイズが大きくなります。Workbenchの以前のバージョンをアンインストールしてから、新しいバージョンをインストールします。

## UberJar {#uber-jar}

The UberJar for AEM 6.5.3.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.3/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.3.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 廃止される機能 {#removed-deprecated-features}

この節では、AEM 6.5.3.0で非推奨とマークされている機能について説明します。将来のリリースで削除される予定の機能は、まず非推奨に設定され、代わりに使用するオプションが用意されています。

お客様には、現在の導入における機能を利用しているかどうかを確認し、代替オプションを使用するように実装を変更する計画を立てることをお勧めします。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. AEM 6.5でAEMとTargetの統合が更新され、Adobe IMSとI/Oを介した認証を使用するTarget Standard APIがサポートされるようになり、AEMページの解析とパーソナライゼーションの実装に関するAdobe launchの役割が増えているので、オプトインウィザードは機能的になりません。 | 各AEMクラウドサービスを使用したシステム接続、Adobe IMS認証、Adobe I/O統合の設定 |

## 既知の問題 {#known-issues}

* AEM 6.5.3.0 **のインストール後に「** Connected assets configuration **」ウィザードが404エラーメッセージを返す場合は、Package Managerを使用して、** cq-remotedam-client-ui-content **および** cq-remotedam-client-ui-componentsパッケージを手動で再インストールします。
* AEM 6.5.x.xのインストール中に、次のエラーメッセージと警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して AEM に Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * com.adobe.granite.maintenance.impl.TaskScheduler : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計関数を使用すると、アダプティブフォームのサーバー側検証に失敗します。 CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。

## OSGi バンドルとコンテンツパッケージが含まれています {#osgi-bundles-and-content-packages-included}

次のドキュメントには、AEM 6.5.3.0 に含まれている OSGi バンドルとコンテンツパッケージの一覧が記載されています。

AEM 6.5.3.0 に含まれている OSGi バンドルの一覧

[ファイルを入手](assets/6530_bundles.txt)

AEM 6.5.3.0 に含まれているコンテンツパッケージの一覧

[ファイルを入手](assets/sp_6530_packages.txt)

## 参考リソース {#helpful-resources}

* [AEM 6.5 リリースノート](/help/release-notes/release-notes.md)
* [AEM 製品ページ](https://www.adobe.com/solutions/web-experience-management.html)
* [AEM 開発者のサポート](https://docs.adobe.com/content/ddc/en.html)
* [AEM 6.5 ドキュメント](https://helpx.adobe.com/support/experience-manager/6-5.html)
* Subscribe to [Adobe Priority Product Updates](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html)

## 制限付きサイト {#restricted-sites}

以下のサイトは既存ユーザーのみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [カスタマーサポート](https://daycare.day.com/public/contact.html)へのお問い合わせサポートポータルへのアクセスについて詳しくは、「サポートポ [ータルへのアクセス」を参照してくださ](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)い。
