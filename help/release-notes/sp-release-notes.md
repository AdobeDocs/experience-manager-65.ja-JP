---
title: AEM 6.5 Service Pack リリースノート
description: Adobe Experience Manager 6.5 Service Pack 3 固有のリリースノート
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 9f4a460c7f64d86e35e950e512ed5b6cda1cbf2a

---


# Adobe Experience Manager 6.5 Service Packリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | **Adobe Experience Manager 6.5** |
|---|---|
| バージョン | 6.5.3.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2019 年 12 月 12 日 |
| ダウンロード URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0) |

## Adobe Experience Manager 6.5.3.0の機能 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.3.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of 6.5 release in **April 2019**. Adobe Experience Manager (AEM) 6.5の上にインストールできます。

このサービスパックリリースの主なハイライトは次のとおりです。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.10.6 に更新しました。

* Experience Manager Assetsで、Deflate 64アルゴリズムを使用して作成されたZIPアーカイブがサポートされるようになりました。

* 作成日の新しい列（並べ替え可能）が、DAMリストビューおよびリストビューのアセット検索結果に追加されました。

* 「名前」列に基づくアセットの並べ替えがリストビューで有効になりました。

* ダイナミックメディアで、スマート切り抜きビデオアセットがサポートされるようになりました。 スマート切り抜きは、機械学習を中心とした機能で、フレームを移動しながらビデオを再切り抜きし、シーンの焦点に合わせて移動します。

* ダイナミックメディアはスマートイメージングをサポートします。

* AEMワークフ [ローでの不在環境設定](../forms/using/configure-out-of-office-settings.md) の設定が可能。

* AEMワークフロ [ーで、「受信トレイ」または](../forms/using/configure-shared-queues-osgi.md) 「受信トレイ」項目を他のユーザーと共有できます。

* バッチ・モ [ードでのインタラクティブ通信の生成](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

* ContextHubにバンドルされているjQueryのバージョンを3.4.1に更新しました。

### 変更点の一覧 {#list-of-changes}

#### Assets {#assets-6530-enhancements}

**製品の機能強化**

* Experience Manager Assetsで、Deflate 64アルゴリズム(NPR-27573)を使用して作成されたZIPアーカイブがサポートされるようになりました。

* 作成日の新しい列（並べ替え可能）が、DAMのリスト表示とリスト表示のアセット検索結果に追加されました(NPR-31312)。

* 「名前」列に基づくアセットの並べ替えがリスト表示で許可されました(NPR-31299)。

* GLB、GLTF、OBJおよびSTLアセットファイルは、DAMの「アセットの詳細」ページでのアセットのプレビューをサポートします(CQ-4282277)。

* ダイナミックメディアでのチャンクのアップロード中に、チャンクノードに対してReplicationOnModifyListenerイベントがトリガーされます。(CQ-4281279)

* ダイナミックメディアで、スマート切り抜きビデオアセットがサポートされるようになりました。 スマート切り抜きは、機械学習を中心とした機能で、フレームを移動しながらビデオを再切り抜きし、シーンの焦点に合わせて調整します(CQ-4278995)。

* ダイナミックメディアは、スマートイメージング(CQ-4222249)をサポートしています。

* クエリパラメーターが要求で渡された場合、検索/参照ビューがFoundationピッカーのデフォルトのビューとして設定されました(NPR-31601)。

**安定性および**

* 一部のPDFドキュメントのメタデータが、タイトルの変更時に更新およびPDFに保存されない(NPR-31629)。

* アセットの共有は、名前にプラス「+」文字を含むアセット(NPR-31547)では機能しません。

* デフォルトの検索フォーム「アセット管理者*検索レール」での編集が期待どおりに機能しない(NPR-31502)。

* アセットビューでOmnisearchを使用してアセットを検索する場合、提案が表示されません(NPR-31496)。

* 同じアセットが別のユーザーによって異なるコレクションで参照されている場合、参照先のアセットが別の場所に移動しても、コレクション内のアセット参照は更新されません(NPR-31486)。

* 重複したIPTCタグがアセットメタデータ(NPR-31328)に追加されます。

* フィルターレール(NPR-31316)から検索がトリガーされた場合、右上隅の検索結果カウントは正確に更新されません。

* ファイルタイプフィルターの第2レベルのチェックボックスの選択を解除すると、すべてのチェックボックスがオフになり、検索バーのテキストが選択/選択解除されたプロパティと同期しなくなります(NPR-31287)。

* すべてのメンバー（ユーザー/グループ）をフォルダーのMembersセクションから削除することはできません。すべてのユーザーを削除しようとすると、ログインしたユーザーがリストに追加されます(NPR-31171)。

* ファイル名にプラス記号「+」が付いたアセットは削除できません(NPR-31162)。

* 「作成」ドロップダウンメニューは、フォルダーを選択する際にトップメニューに表示され、「フォルダー」は作成オプションとして表示されません(NPR-30877)。

* パス上のDeny jcr:removeChildNodesおよびjcr:removeNodeのACLがユーザー(NPR-30840)に適用される場合、作成/FileUploadアクション項目が見つかりません。

* 特定のmp4アセットがアップロードされると、DAMワークフローが古い状態になり、残りのすべてのワークフローが古い状態になります(NPR-30662)。

* メモリ不足エラーは、（数ギガバイトの）大きなPDFファイルがDAMにアップロードされ、そのサブアセットが処理されるときに発生します(NPR-30614)。

* アセットの一括移動が失敗し、警告メッセージが表示されている(NPR-30610)。

* Dynamic Media Scene 7ランモード(NPR-31630)で実行されているAEMで、アセットを別のフォルダーに移動すると、アセット名が小文字に変更されます。

* Scene 7の会社名(NPR-31340)と同じ名前のフォルダに存在する画像に関して、リモート画像セットの編集中にエラーが発生する。

* 参照を含むダイナミックメディアアセットが公開されない(NPR-31180)。

* AEMダイナミックメディア — Scene 7ランモードからScene 7へのアップロードが、完了するのに時間がかかりすぎています(NPR-31048)。

* 画像アセットに追加されたホットスポットは、アセットの詳細ページのインタラクティブ画像ビューアでは表示されません(NPR-30979)。

* AEM Assetsで行われたアクションがScene 7(NPR-30947)に渡されると、大量のスリングジョブが作成され、「処理」バナーが再び表示されます。

* アセットとアセットの言語コピーを作成する際に競合が発生し、Scene 7(NPR-30932)にアップロードされません。

* ダイナミックメディアハイブリッドモードで実行されているAEMからダウンロードされたダイナミックレンディションが壊れる（画像コンテンツタイプではなく、コンテンツが「画像が見つかりません」のテキストタイプ）(NPR-30876)。

* Dynamic Media Encode Videoワークフローで、Scene 7からDynamic Media - Scene 7実行モードに移行したビデオのサムネールの生成に失敗する。(CQ-4282011)

* 異なるScene7会社IDを使用して、あるインスタンスから別のインスタンスにアセットを移行中にIpsApiExceptionが発生する問題を修正しました。(CQ-4280548)

* 3Dアセットのサムネールは、サポートされている3DモデルがAEMに取り込まれた場合には情報とはなりません(CQ-4283701)。

* 3Dアセットのカメラビューが少ない場合は、スクロールボタンがビューアに表示されます(CQ-4283322)。

* アセットの詳細ページでDimensionalViewerでプレビューした、アップロードされた3Dモデルのコンテナの高さが正しくない(CQ-4283309)。

* Internet Explorer 11およびSafariのSmartCropVideoViewerではビデオを再生できません(CQ-4281422)。

* 複数のアセットを1つのフォルダから別のフォルダに移動するための移動ボタンの使用は、ダイナミックメディア — scene7 runmodeで実行されているAEMで失敗します(CQ-4280384)。

* MIMEタイプがMP4以外の場合、アセットの詳細にビデオが歪んで表示される(CQ-4279704)。

* ビデオプロファイルを含むフォルダーに新しく取り込んだビデオは、エンコードの割合が100 %に達した後も、処理状態のままになります。(CQ-4279389)

* フォルダからアセットを移動すると、理想的に必要な数よりも多くのSlingジョブ（Scene 7 API呼び出し）が作成されます(CQ-4278664)。

* 画像セット（またはメディアセット）が作成され、DAMで適切な命名規則を使用して名前が付けられると、画像セットの名前がScene 7で小文字に変更されます(CQ-428112)。

* Scene 7 Migratorが正しく公開状態を設定しない(CQ-4263492)。

* タッチUI検索（Omnisearchで実行）の結果ページが自動的に上にスクロールし、コンテンツフラグメントでのユーザーのスクロール位置が失われます。(CQ-4282898)

* PDFファイルのインデックスが作成されず、内のコンテンツを検索できない(CQ-4278916)。

* エラー「グループがユーザー選択によって一覧表示されていません：異なる「と」を持つ閉じたユーザーグループを追加する際に「false to equal true」が `principalName` 予期さ `authorizableId` れる問題が発生します(CQ-4278177)。

* アセットUIの列ビューに、特定のテナントのDAMルートパスに関係なく、すべてのパスが表示される(CQ-4278175)。

* アセットセレクターの検索が期待どおりに動作しない(CQ-4275886)。

* レンディションワークフローが失敗する(CQ-4271928)。

* DAMイベントの削除では、最新の(maxSavedActivities)イベントデータが削除され、以前に作成されたデータが保持されます(NPR-31336)。

* タッチUI検索（Omnisearchを通じて行われる）の結果ページは、自動的に上にスクロールし、ユーザーのスクロール位置が失われます(NPR-31307)。

* すべてを選択した後で、タッチ操作対応UI(NPR-31118)で一部の項目（フォルダー/個々のアセット）の選択を解除しても、アクションバーとアセット数が更新されない。

* アセットのジョブの詳細をポーリング中に、AEMに例外が表示されます(CQ-4283569)。

* DAMのXSS脆弱性(NPR-31654)。

#### Sites {#sites}

* LiveCopyの継承が壊れている場合、ライブコピーページには、LiveCopyリンクの代わりに言語コピーリンクが表示されます(NPR-30980)。
* 新しいBlueprintの場合、レコード数が40を超えると、最初の40レコードのみが表示されます。 Blueprintでは、残りのレコードの空白行が表示されます(NPR-31182)。
* ユーザーがメニューのdescriptionプロパティに日本語または韓国語の文字を追加すると、メニューには、日本語と韓国語のテキストに対してゆがんだ文字が表示されます。 (NPR-31331).
* リッチテキストエディター(RTE)では、埋め込まれたテーブルをリスト項目として挿入できません(NPR-30879)。
* 標準で、scaffolding Rich Text Editor(RTE)を使用できます。 要素にインラインフォントサイズを予期せず適用します(NPR-31284)。
* ユーザーが左側のパネルのフィールドにフォーカスし、キーボードショートカットを使用してコンテンツを貼り付けると、左側のパネルのフィールドからコピーしたコンテンツではなく、ページエディターのクリップボードのコンテンツが貼り付けられます(NPR-31172)。
* ユーザが複数フィールドにファイルアップロードフィールドを追加すると、画像パスは、複数フィールドノード(NPR-30882)ではなく、コンポーネントノードに格納されます。
* ResponsiveGridExporter APIは、com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporterインターフェイスを返しません。 com.day.cq.wcm.foundation.model.implパッケージは、プライベートパッケージとして宣言されています(NPR-31398)。
* 一部のExperienceFragmentsを含むページがエディター以外のモードで（プレフィックスが付いていない「作成者」または「発行者」のいずれかで）開かれると、要求はHTTPステータスエラーコード500(NPR-30743)で終了します。 `editor.html``wcmmode=disabled`
* ユーザーはパスワードを変更したり、自分のプロファイルページ(NPR-31161)にアクセスしたりできません。
* ユーザデータを含むJavaScriptファイルがサーバ側で生成されます(NPR-30822)。
* AEMオーサリングUIを使用すると、外部コンテンツ(NPR-29745)を使用したフィッシング詐欺が可能になります。
* AEM 6.5メタデータエディタ(NPR-31017)のエクスプレッション言語注入脆弱性。

#### 検索とユーザーインターフェイス {#search-ui-interface}

* 検索結果ページでカード表示からリスト表示に切り替えると、ページがスクロールされるまでに遅延が生じます(NPR-31286)。

* 「すべて選択」チェックボックスは、サイトUIのリスト表示(NPR-31614)で非表示になっています。

* 検索結果ページの「すべて選択」の数が正しくありません(NPR-31120)。

* メタデータエディターには、存在しないタグ(NPR-31119)が表示されます。

#### 翻訳 {#translation}

* 翻訳ジョブ(NPR-31270)で「期日」オプションを選択すると、2つのカレンダーポップアップが表示されます。

#### プラットフォーム {#platform}

* Webコンソールの「MIME type」オプションが機能しません(NPR-31108)。

* シングルサインオン(NPR-31165)を設定する場合、クライアント証明書は受け入れられません。

* Jetty ベースの HTTP サービスのバッファーサイズ設定でアップデートが保存されない。（NPR-30925）

* QueryBuilderで、xpathクエリでorderbyがサ ``fn:name()`` ポートされるようになりました(NPR-31322)。

* AEM 6.3(NPR-31513)からのアップグレード時に、アクティベーションツリーが複製されます。

* 転送された要求は、Sling認証(NPR-30013)中に設定された応答ヘッダーを保持しません。

* ピッカーコンポーネント内の検索が機能しない(NPR-31692)。

* Apache POIとApache Tikaバンドル(NPR-31018)の異なるバージョンが原因で、ZIPファイルをAEM Communitiesの投稿に添付すると、エラーが表示されます。

* バンド ``org.apache.sling.distribution.api`` ルは設定マネージャーで非表示になっているので、カスタムバンドル(NPR-31720)では使用できません。

#### プロジェクト {#projects}

* カレンダービューの切り替えが機能しない(NPR-31271)。

#### Brand Portal {#assets-brand-portal}

**製品の機能強化**

* AEM Assetsのアセットソーシングの読み込みワークフローが変更され、新しく作成したアセットのみがBrand PortalからAEMに取得され、複製を避けるために、新しいフォルダーに既に存在するアセットをスキップするようになりました。(CQ-4278527)

**安定性および**

* アセットソーシング機能で新しい貢献度フォルダーを作成すると、誤ったアイコンが表示される(CQ-4282825)。
* 新しい貢献度フォルダーを作成すると、1つまたは両方のサブフォルダー（NEWおよびSHARED）が貢献度フォルダー(CQ-4282424)内に表示されません。
* Brand Portalの最後からContributionフォルダーの新しいアセットを受け取った後に、ユーザーがAEMからBrand Portalに貢献度フォルダーを再公開しようとすると、システムで例外がスローされます。(CQ-4279740)
* 貢献度フォルダー（ネストされたフォルダー）内に貢献度フォルダーを作成することは、複雑さを避けるために禁止されています(CQ-4278391)。
* AEM管理コンソールから読み込んだBrand Portalユーザーリスト（.csvファイル）のアップロード時に例外が発生する。 .csvファイル内の「電子メール」、「FirstName」、「LastName」フィールドのみが必須です(CQ-4278390)。

#### Communities {#communities}

**安定性および**

* グループを管理するクイックリンク（「開く」、「編集」、「公開」、「削除」の各グループ）は、コミュニティ管理者（グループ管理者/サイト管理者）(NPR-31627)には表示されません。
* 送信されたブログは、ページを手動で更新または再読み込みしない限り表示されません(NPR-31599)。
* 「メンション」機能で使用されるJCRクエリでは、大文字と小文字が区別され、結果を返すのに時間がかかりすぎます(NPR-31475)。
* AEM 6.5 UberJarファイルで例外がスローされ、AEM 6.5 UberJar `cq-social-translation` ファイル(NPR-31186)にバンドルが見つかりません。
* 新しい脆弱性(NPR-30967)に対処するために、Jackson Databindライブラリがバージョン2.9.9.3に更新されました。
* アクティビティと通知タイトルに一貫性がない。（NPR-30941）
* Communities ブログでページネーションが正しく機能していない。（NPR-30914）
* 分析レポートが AEM のオーサー環境に入力されず、空白ページが表示される（NPR-30913）。

#### Oak {#oak}

* Luceneのインデックスの更新により、作成者サーバーの動作が遅くなる(NPR-31548)。

#### Forms {#forms-6530}

>[!NOTE]
>
>AEM サービスパックには、AEM Forms の修正は含まれません。別の Forms アドオンパッケージを使用して配布されます。さらに、JEE上のAEM Formsの修正を含む累積インストーラーがリリースされました。 For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

##### Forms アドオンパッケージ {#forms-add-on-package-6530}

**アダプティブフォーム**

* 文字列には、アダプティブフォームのローカライズ時に辞書キーが含まれます(NPR-31110)。

**インタラクティブコミュニケーション**

* **MissingNode.toString()は、Jacksonライブラリを2.10.0(NPR-31549)にアップグレードした後に、不正確な結果を返します。**

* テキストエディターは、Microsoft Wordからコピーしたテキストからスペース文字をランダムに削除します(NPR-31113)。

**Correspondence Management**

* LiveCycle ES4SP1からAEM 6.5(NPR-31615)にレターを移行する際に、キャプションとツールチップが表示されない。

* **レターをドラフトとして保存する際に** 、テキストフローの書式設定がサポートされなくなりました。(NPR-30463)

**ワークフロー**

* CPU使用率が100%の場合(NPR-31233)、OSGiワークフローが失敗する。

**HTML5 のフォーム**

* XDP フォームの HTML5 プレビューを生成すると、サブフォームのインスタンス追加中にちらつきが表示される。（NPR-30909）

##### JEE上のFormsインストーラー {#forms-jee-installer-6530}

**Forms - ドキュメントサービス**

* .NETプロジェクトでMTOMを使用するSOAP Webサービスで、AssemblerServiceClient呼び出しおよびHtmlToPDF2メソッドの例外が表示されます(NPR-4281771)。

**Foundation JEE**

* アクションの設定では、「Invoke a Forms Workflow submit action」(NPR-31478)のプロセス名は読み込まれません。
* JEE上のAEM Formsのユーザーが、.lcaファイルの読み込み時、または管理コンソールでのLDAPの設定時に、次のようなエラーが発生します。

   `com.ibm.ws.webcontainer.filter.FilterInstanceWrapper doFilter SRVE8109W: Uncaught exception thrown by filter um: java.lang.NoClassDefFoundError: org/apache/commons/io/IOUtils at org.apache.commons.fileupload.util.Streams.copy`

   `Error 500: javax.servlet.ServletException: java.lang.NoClassDefFoundError: org.apache.commons.io.IOUtils` (NPR-30931)


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
>そのため、エラーログが安定するのを待ってから、インスタンスにアクセスすることをお勧めします。ユーザーは、アップデーターバンドルのアンインストールに関連する特定のログを待ってから、インストールが正常に行われることを確認する必要があります。 通常は、Safari で発生しますが、任意のブラウザーで断続的に発生する可能性があります。

**自動インストール**

実行中のインスタンスに AEM 6.5.3.0 を自動的にインストールするには、次の 2 つの方法があります。

A.パッケージを。.*サーバーがオンラインで使用可能な間、* /crx-quickstart/installフォルダーを作成します。 パッケージは自動的にインストールされます。

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.3.0 では、ブートストラップインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ(/system/console/ productinfo)の「インストール済み製品」に、更新されたバージョン文字列 `Adobe Experience Manager, Version 6.5.3.0` が表示されます。

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. OSGIバンドルorg.apache.jackrabbit.oak-coreはバージョン1.10.6以降です(Use Web Console:/system/console/bundles)。

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>AEM Forms を使用していない場合はスキップしてください。AEM Forms の修正は、個別のアドオンパッケージを介して配信されます。

>[!NOTE]
>
>AEM 6.5.3.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). 古いバージョンのAEM Forms互換性パッケージを使用し、AEM 6.5.3.0にアップデートする場合は、Formsアドオンパッケージのインストール後に、最新バージョンのAEM Forms互換性パッケージをインストールします。

1. AEM Service Pack がインストールされていることを確認してください。
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE上のAEM Formsに関する修正は、別のインストーラーを使用して提供されます。

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0007](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0007.html).

#### Workbench インストーラー

これはフルインストーラーなので、パッチバージョンよりもファイルサイズが大きくなります。新しいWorkbenchをインストールする前に、以前のバージョンのWorkbenchをアンインストールします。

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

This section lists features and capabilities that have been marked as deprecated with AEM 6.5.3.0. Features that are planned to be removed in a future release are set to deprecated first, with an alternate option to use.

お客様は、現在の導入で機能を利用しているかどうかを確認し、別のオプションを使用するように実装を変更する計画を立てることをお勧めします。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. AEM 6.5でAEMとTargetの統合が更新され、Adobe IMSとI/Oを介した認証を使用するTarget Standard APIがサポートされるようになりました。また、分析とパーソナライゼーションのためのAEMページの実装に関するAdobe Launchの役割が増えているので、オプトインウィザードは機能的に無関係です。 | 各AEMクラウドサービスを介したシステム接続、Adobe IMS認証、Adobe I/O統合の設定 |

## 既知の問題 {#known-issues}

* AEM 6.5.3.0のインストール後に **Connected assets configuration** （接続されたアセットの設定）ウィザードが404エラーメッセージを返す場合は、Package Managerを使用して、 **cq-remotedam-client-ui-content** および **** cq-remotedam-client-ui-componentsパッケージを手動で再インストールします。
* AEM 6.5.x.xのインストール中に、次のエラーメッセージと警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して AEM に Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * com.adobe.granite.maintenance.impl.TaskScheduler : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計関数が使用されている場合、アダプティブフォームのサーバー側の検証に失敗します。 CQ-4274424
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
* [AEM 製品ページ](https://www.adobe.com/marketing/experience-manager.html)
* [AEM 6.5 ドキュメント](https://helpx.adobe.com/support/experience-manager/6-5.html)
* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

## 制限付きサイト {#restricted-sites}

以下のサイトは既存ユーザーのみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [カスタマーサポート](https://daycare.day.com/public/contact.html)へのお問い合わせサポートポータルへのアクセスについて詳しくは、「サポートポ [ータルへのアクセス](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)」を参照してください。
