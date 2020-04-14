---
title: AEM 6.5以前のService Packリリースノート
description: Adobe Experience Manager 6.5 Service Pack 3以前に固有のリリースノートです。
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# 以前のサービスパックに含まれていたホットフィックスと機能パック {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## Adobe Experience Manager 6.5.3.0

[!DNL Adobe Experience Manager] 6.5.3.0は、パフォーマンス、安定性、セキュリティ、お客様向けの主要な修正、および2019年4月のGAリリース(GA)以降にリリースされた機能強化を含む重要なリリ **ースです**。 6.5の上にインストールで [!DNL Adobe Experience Manager] きます。

このサービスパックリリースの主なハイライトは次のとおりです。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.10.6 に更新しました。

* [!DNL Experience Manager Assets] deflate64アルゴリズムを使用して作成されたZIPアーカイブをサポートするようになりました。

* 作成日の新しい列（並べ替え可能）が、DAMリスト表示およびアセット検索結果のリスト表示に追加されました。

* 「名前」列に基づくアセットの並べ替えが、アセットの表示で有効になりました。

* [!DNL Dynamic Media] スマート切り抜きビデオアセットがサポートされるようになりました。 スマート切り抜きは、機械学習を中心とした機能で、フレームを移動しながらビデオを再切り抜きし、シーンの焦点に合わせて移動します。

* [!DNL Dynamic Media] は、スマートイメージングをサポートしています。

* 「不在」 [環境設定を](../forms/using/configure-out-of-office-settings.md) ワークフローで [!DNL Experience Manager] 設定

* 受信トレイま [たは受信トレイの項目を](../forms/using/configure-shared-queues-osgi.md) 、他のユーザーと共有で [!DNL Experience Manager] きます。

* バッチ・モ [ードでのインタラクティブ通信の生成](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

* ContextHubにバンドルされているjQueryのバージョンを3.4.1に更新しました。

### アセット {#assets-6530-enhancements}

**製品の機能強化**

* [!DNL Experience Manager Assets] deflate64アルゴリズム(NPR-27573)を使用して作成されたZIPアーカイブをサポートするようになりました。

* 作成日の新しい列（並べ替え可能）が、DAMリスト表示およびリスト表示(NPR-31312)のアセット検索結果に追加されました。

* 「名前」列に基づくアセットの並べ替えが、リスト表示(NPR-31299)で許可されました。

* GLB、GLTF、OBJおよびSTLアセットファイルは、DAMの「アセットの詳細」ページでのアセットのプレビューをサポートします(CQ-4282277)。

* ReplicationOnModifyListenerイベントは、(CQ-4281279)でのチャンクのアップロード中に、チャンクノ [!DNL Dynamic Media] ードに対してトリガーされます。

* [!DNL Dynamic Media] スマート切り抜きビデオアセットがサポートされるようになりました。 スマート切り抜きは、機械学習を中心とした機能で、フレームを移動しながらビデオを再切り抜きし、シーンの焦点に合わせて調整します(CQ-4278995)。

* [!DNL Dynamic Media] は、スマートイメージング(CQ-4222249)をサポートしています。

* 検索/参照表示ーが、クエリパラメーターが要求で渡される場合に、Foundationピッカーでデフォルトの表示ーとして設定されています(NPR-31601)。

**安定性および**

* 一部のPDFドキュメントのメタデータは、タイトルの変更時に更新およびPDFに保存されません(NPR-31629)。

* アセットの共有は、名前にプラス「+」文字を含むアセット(NPR-31547)では機能しません。

* デフォルトの検索フォーム「アセット管理者*検索レール」での編集が期待どおりに機能しない(NPR-31502)。

* アセットの検索にOmnisearchをアセット表示で使用する場合、提案が表示されません(NPR-31496)。

* 同じアセットが別のユーザーによって異なるコレクションで参照されている場合、参照先のアセットが別の場所に移動しても、コレクション内のアセット参照は更新されません(NPR-31486)。

* 重複のIPTCタグがアセットメタデータ(NPR-31328)に追加されます。

* フィルターレール(NPR-31316)から検索がトリガーされた場合、右上隅の検索結果カウントは正確に更新されません。

* ファイルタイプフィルターの第2レベルのチェックボックスの選択を解除すると、すべてのチェックボックスがオフになり、検索バーのテキストが選択/選択解除されたプロパティと同期しなくなります(NPR-31287)。

* すべてのメンバー（ユーザー/グループ）をフォルダーのMembersセクションから削除することはできません。すべてのユーザーを削除しようとすると、ログインしたユーザーがリスト(NPR-31171)に追加されます。

* ファイル名にプラス記号「+」が付いたアセットは削除できません(NPR-31162)。

* 「作成」ドロップダウンメニューは、フォルダーを選択する際にトップメニューに表示され、「フォルダー」は作成オプションとして表示されません(NPR-30877)。

* パス上のDeny jcr:removeChildNodesおよびjcr:removeNodeのACLがユーザー(NPR-30840)に適用される場合、作成/FileUploadアクション項目が見つかりません。

* 特定のmp4アセットがアップロードされると、DAMワークフローが古い状態になり、残りのすべてのワークフローが古い状態になります(NPR-30662)。

* メモリ不足エラーは、（数ギガバイトの）大きなPDFファイルがDAMにアップロードされ、そのサブアセットが処理されるときに発生します(NPR-30614)。

* アセットの一括移動が失敗し、警告メッセージが表示されている(NPR-30610)。

* Scene7モード(NPR-31630)で実行中にアセットを別のフォルダに移動すると、ア [!DNL Experience Manager] セット名が小 [!DNL Dynamic Media]文字に変更されます。

* Scene 7会社名(NPR-31340)と同じ名前のフォルダに存在する画像のリモート画像セットの編集中にエラーが発生する。

* [!DNL Dynamic Media] 参照を含むアセットが公開されない(NPR-31180)。

* 7-Scene7モ [!DNL Dynamic Media]ードからへのアップロードに [!DNL Dynamic Media Classic] 時間がかかりすぎて完了しない(NPR-31048)。

* 画像アセットに追加されたホットスポットは、アセットの詳細ページのインタラクティブ画像ビューアでは表示されません(NPR-30979)。

* 大量のスリングジョブが作成され、でアセットに対して行われたアクションがScene 7に渡されると、「処理」 [!DNL Experience manager Assets] バナーが再び表示されます(NPR-30947)。

* アセットとアセットの言語コピーを作成する際に競合が発生し、Scene 7(NPR-30932)にアップロードされません。

* ハイブリッドモードで実行 [!DNL Experience Manager][!DNL Dynamic Media]したときにダウンロードされたダイナミックレンディションが壊れる（画像コンテンツタイプではなく、コンテンツが「画像が見つかりません」のテキストタイプ）(NPR-30876)。

* [!DNL Dynamic Media] Adobe Experience Managerで、ビデオのエンコードワークフローで、Scene7モードからScene7モ [!DNL Dynamic Media Classic] ードに移行さ [!DNL Dynamic Media]れたビデオのサムネールの生成に失敗する(CQ-4282011)。

* 異なるScene7会社IDを使用して、アセットを別のインスタンスに移行する際にIpsApiExceptionが発生する問題を修正しました。(CQ-4280548)

* 3Dアセットのサムネールは、サポートされている3Dモデルが(CQ-4283701)に取り込まれ [!DNL Experience Manager] る場合には情報になりません。

* 3Dアセットにカメラ表示がほとんどない場合は、スクロールボタンがビューアに表示されます(CQ-4283322)。

* アセットの詳細ページのDimensionalViewerでプレビューした、アップロードされた3Dモデルのコンテナの高さが正しくありません。(CQ-4283309)

* Internet Explorer 11およびSafariのSmartCropVideoViewerではビデオを再生できません(CQ-4281422)。

* 複数のアセットを1つのフォルダから別のフォルダに移動するための移動ボタンの使用は、 [!DNL Experience Manager][!DNL Dynamic Media]Scene7ランモードでの実行に失敗します(CQ-4280384)。

* MIMEタイプがMP4以外の場合、アセットの詳細にビデオが歪んで表示される(CQ-4279704)。

* ビデオプロファイルを含むフォルダーに新たに取り込まれたビデオは、エンコードの割合が100 %に達した後も、処理状態のままとなります。(CQ-4279389)

* フォルダからアセットを移動すると、理想的に必要な数よりも多くのSlingジョブ（Scene 7 API呼び出し）が作成されます(CQ-4278664)。

* 画像セット（またはメディアセット）が作成され、DAMで適切な命名規則を使用して名前が付けられると、画像セットの名前がScene 7で小文字に変更されます(CQ-428112)。

* Scene 7 Migratorが正しく公開状態を設定しない(CQ-4263492)。

* タッチUI検索（Omnisearchで実行）の結果ページが自動的に上にスクロールし、コンテンツフラグメントでのユーザーのスクロール位置が失われます。(CQ-4282898)

* PDFファイルのインデックスが作成されず、内のコンテンツを検索できない(CQ-4278916)。

* エラー「グループがユーザー選択によって一覧表示されていません：異なる「と」を持つ閉じたユーザーグループを追加する際に「false to equal true」が `principalName` 予期さ `authorizableId` れる問題が発生します(CQ-4278177)。

* アセットUI列の表示に、特定のテナントのDAMルートパスに関係なく、すべてのパスが表示される(CQ-4278175)。

* アセットセレクターの検索が期待どおりに動作しない(CQ-4275886)。

* レンディションワークフローが失敗する(CQ-4271928)。

* DAMイベントの削除は、最新の(maxSavedActivities)イベントデータを削除し、以前に作成されたデータを保持します(NPR-31336)。

* タッチUI検索（Omnisearchを通じて行われる）の結果ページは、自動的に上にスクロールし、ユーザーのスクロール位置が失われます(NPR-31307)。

* すべてを選択した後で、タッチ操作対応UI(NPR-31118)で一部の項目（フォルダー/個々のアセット）の選択を解除しても、アクションバーとアセット数が更新されない。

* アセットのジョブの詳 [!DNL Experience Manager] 細をポーリング中に、に例外が表示されます(CQ-4283569)。

### Sites {#sites}

* LiveCopyの継承が壊れている場合、ライブコピーページには、LiveCopyリンクの代わりに言語コピーリンクが表示されます(NPR-30980)。
* 新しいBlueprintの場合、レコード数が40を超えると、最初の40レコードのみが表示されます。 Blueprintでは、残りのレコードの空白行が表示されます(NPR-31182)。
* ユーザーがメニューのdescriptionプロパティに日本語または韓国語の文字を追加すると、メニューには、日本語と韓国語のテキストに対してゆがんだ文字が表示されます。 (NPR-31331).
* リッチテキストエディター(RTE)では、埋め込みテーブルをリスト項目として挿入できません(NPR-30879)。
* 標準で、scaffolding Rich Text Editor(RTE)を使用できます。 要素にインラインフォントサイズを予期せず適用します(NPR-31284)。
* ユーザーが左側のパネルのフィールドにフォーカスし、キーボードショートカットを使用してコンテンツを貼り付けると、左側のパネルのフィールドからコピーしたコンテンツではなく、ページエディターのクリップボードのコンテンツが貼り付けられます(NPR-31172)。
* ユーザが複数フィールドにファイルアップロードフィールドを追加すると、画像パスは、複数フィールドノード(NPR-30882)ではなく、コンポーネントノードに格納されます。
* ResponsiveGridExporter APIは、com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporterインターフェイスを返しません。 com.day.cq.wcm.foundation.model.implパッケージは、プライベートパッケージとして宣言されています(NPR-31398)。
* 一部のExperienceFragmentsを含むページがエディター以外のモードで（プレフィックスが付いていない「作成者」または「発行者」のいずれかで）開かれると、要求はHTTPステータスエラーコード500(NPR-30743)で終了します。 `editor.html``wcmmode=disabled`
* ユーザーは、パスワードを変更したり、プロファイルページにアクセスしたりできません(NPR-31161)。

### 検索とユーザーインターフェイス {#search-ui-interface}

* 検索結果ページでカード表示からリスト表示に切り替えると、ページがスクロールされるまでに遅延が生じます(NPR-31286)。

* 「すべてを選択」チェックボックスは、 [!DNL Sites] UIのリスト表示(NPR-31614)で非表示になっています。

* 検索結果ページの「すべて選択」の数が正しくありません(NPR-31120)。

* メタデータエディターには、存在しないタグ(NPR-31119)が表示されます。

### 翻訳 {#translation}

* 翻訳ジョブ(NPR-31270)で「期日」オプションを選択すると、2つのカレンダーポップアップが表示されます。

### プラットフォーム {#platform}

* Webコンソールの「MIME type」オプションが機能しません(NPR-31108)。

* シングルサインオン(NPR-31165)を設定する場合、クライアント証明書は受け入れられません。

* Jetty ベースの HTTP サービスのバッファーサイズ設定でアップデートが保存されない。（NPR-30925）

* QueryBuilderで、xpathクエリ(NPR-31322) ``fn:name()`` のorderbyがサポートされるようになりました。

* 重複アクティベーションツリーは、 [!DNL Experience Manager] 6.3(NPR-31513)からのアップグレード時に作成されます。

* 転送された要求は、Sling認証(NPR-30013)中に設定された応答ヘッダーを保持しません。

* ピッカーコンポーネント内の検索が機能しない(NPR-31692)。

* Apache POIとApache Tikaバンドル(NPR-31018)の異なるバージョンが原 [!DNL Experience Manager Communities] 因で、ZIPファイルを投稿に添付すると、エラーが表示されます。

* バンド ``org.apache.sling.distribution.api`` ルは設定マネージャーで非表示になっているので、カスタムバンドル(NPR-31720)では使用できません。

### プロジェクト {#projects}

* カレンダー表示の切り替えが機能しない(NPR-31271)。

### Brand Portal {#assets-brand-portal}

**製品の機能強化**

* のアセットソーシング読み込みワ [!DNL Experience Manager Assets][!DNL Brand Portal][!DNL Experience Manager]ークフローが、からに新しく作成されたアセットのみを取り込むように変更され、複製を避けるために、NEWフォルダーに既に存在するアセットをスキップします(CQ-4278527)。

**安定性および**

* アセットソーシング機能で新しい貢献度フォルダーを作成すると、誤ったアイコンが表示される(CQ-4282825)。
* 新しい貢献度フォルダーを作成すると、1つまたは両方のサブフォルダー（NEWおよびSHARED）が貢献度フォルダー(CQ-4282424)内に表示されません。
* 貢献度フォルダー内の新しいアセットを最後から受け取った後に、貢献度フ [!DNL Experience Manager] ォルダーをからに再 [!DNL Brand Portal] 公開しようとすると、システムで例外がス [!DNL Brand Portal] ローされます(CQ-4279740)。
* 貢献度フォルダー（ネストされたフォルダー）内に貢献度フォルダーを作成することは、複雑さを避けるために禁止されています(CQ-4278391)。
* 管理コンソールからインポートしたユーザ [!DNL Brand Portal] リスト（.csvファイル）のアップロード時に例外がス [!DNL Experience Manager] ローされます。 .csvファイル内の「電子メール」、「FirstName」、「LastName」フィールドのみが必須です(CQ-4278390)。

### Communities {#communities}

**安定性および**

* グループを管理するクイックリンク（「開く」、「編集」、「公開」、「削除」の各グループ）は、コミュニティ管理者（グループ管理者/サイト管理者）(NPR-31627)には表示されません。
* 送信されたブログは、ページを手動で更新または再読み込みしない限り表示されません(NPR-31599)。
* 「メンション」機能で使用されるJCRクエリでは大文字と小文字が区別され、結果を返すのに時間がかかりすぎます(NPR-31475)。
* [!DNL Experience Manager] 6.5 UberJarファイルで例外がスローされ、バ `cq-social-translation` ンドルが6.5 UberJarフ [!DNL Experience Manager] ァイルに存在しない(NPR-31186)。
* 新しい脆弱性(NPR-30967)に対処するために、Jackson Databindライブラリがバージョン2.9.9.3に更新されました。
* アクティビティと通知タイトルに一貫性がない。（NPR-30941）
* Pagination is not working properly in [!DNL Communities] Blogs (NPR-30914).
* Analytics reports are not populated in [!DNL Experience Manager] author environment, blank page appears (NPR-30913).

### Oak {#oak}

* Luceneのインデックスの更新により、作成者サーバーの動作が遅くなる(NPR-31548)。

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Packにはの修正が含まれていませ [!DNL Experience Manager Forms]ん。 別の Forms アドオンパッケージを使用して配布されます。In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. 詳しくは、「Experience Manager Formsのインスト [ール」アドオンおよび「JEE上の](#install-aem-forms-add-on-package) Experience Manager Formsのイ [ンストール」を参照してください](#install-aem-forms-jee-installer)。

#### Forms アドオンパッケージ {#forms-add-on-package-6530}

**アダプティブフォーム**

* 文字列には、アダプティブフォームのローカライズ時に辞書キーが含まれます(NPR-31110)。

**インタラクティブコミュニケーション**

* **MissingNode.toString()は、Jacksonライブラリを2.10.0(NPR-31549)にアップグレードした後に、不正確な結果を返します。**

* テキストエディターは、Microsoft Wordからコピーしたテキストからスペース文字をランダムに削除します(NPR-31113)。

**Correspondence Management**

* LiveCycle ES4SP1から6.5(NPR-31615)にレターを移行する際に、キャプションとツールチッ [!DNL Experience Manager] プが表示されない。

* **レターをドラフトとして保存する際に** 、テキストフローの書式設定がサポートされなくなりました。(NPR-30463)

**ワークフロー**

* CPU使用率が100%の場合(NPR-31233)、OSGiワークフローが失敗する。

**HTML5 のフォーム**

* XDP フォームの HTML5 プレビューを生成すると、サブフォームのインスタンス追加中にちらつきが表示される。（NPR-30909）

#### JEE上のFormsインストーラー {#forms-jee-installer-6530}

**Forms - ドキュメントサービス**

* .NETプロジェクトでMTOMを使用するSOAP Webサービスで、AssemblerServiceClient呼び出しおよびHtmlToPDF2メソッドの例外が表示されます(NPR-4281771)。

**Foundation JEE**

* アクションの設定では、「Invoke a Forms Workflow submit action」(NPR-31478)のプロセス名は読み込まれません。

### 含まれている機能パック {#feature-packs-included-6530}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] Oracle 18c(NPR-29155)のフォームサポート。

## Adobe Experience Manager 6.5.2.0

[!DNL Adobe Experience Manager] 6.5.2.0は、パフォーマンス、安定性、セキュリティ、お客様向けの主要な修正、および2019年4月のGA(General Availability)以降にリリースされた機能強化を含む重要なリリ [!DNL Adobe Experience Manager] ースで ****&#x200B;す。 6.5の上にインストールで [!DNL Experience Manager] きます。

このサービスパックリリースの主なハイライトは次のとおりです。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）がバージョン 1.10.3 に更新されました。
* Added a configuration property to allow exporting Experience Fragments directly to user-defined workspaces for [!DNL Adobe Target].
* Assets ユーザーは、視覚的に類似した画像を検索できます。[!DNL Experience Manager] は、ユーザーが選択した画像に類似した、DAM リポジトリのスマートタグ付き画像を表示します。[ビジュアル検索](../assets/search-assets.md#visualsearch)を参照してください。

* Connected Assets 機能が強化されて、リモート DAM デプロイメントからドキュメントを取得できるようになりました。サイト作成者は、サポートされているドキュメントタイプをコンテンツファインダーで検索およびフィルタリングできるようになりました。リモートドキュメントは、Web ページのダウンロードコンポーネントに追加できます。[Connected Assets の使用](../assets/use-assets-across-connected-assets-instances.md)を参照してください。

* 複数値のフィルターをサポートするために、より多くのMIMEタイプを使用してEnhanceDocument typeオプションを設定します。
* 外部の再処理ワークフローが導入されて、複数のリソースがサポートされるようになりました。
* レプリケーシ [!DNL Dynamic Media] ョンにデフォルトのアセットフィルターを使用して、パフォーマンスを最適化。
* DMS7（Dynamic Media Scene7）の切り抜きおよび回転のアセット編集オプションが復活しました。
* VideoPlayer で読み込み時にビデオをミュートするオプションが実装されました。
* アセット UI の列表示にテナント固有のコンテンツのみ表示されるように修正しました。
* スタイルアコーディオンの変更が検索結果に反映されるように修正しました。

### アセット {#assets}

**製品の機能強化**

* Connected Assets 機能が強化されて、リモート DAM デプロイメントからドキュメントを取得できるようになりました。サイト作成者は、サポートされているドキュメントタイプをコンテンツファインダーで検索およびフィルタリングできるようになりました。リモートドキュメントは、Web ページのダウンロードコンポーネントに追加できます。CQ-4270245 のホットフィックス. [Connected Assets の使用](/help/assets/use-assets-across-connected-assets-instances.md)を参照してください。

* [!DNL Experience Manager Assets] ユーザーは、視覚的に類似した画像を検索できます。[!DNL Experience Manager] は、ユーザーが選択した画像に類似した、DAM リポジトリのスマートタグ付き画像を表示します。[ビジュアル検索](../assets/search-assets.md#visualsearch)を参照してください。

**安定性および**

* ACP API で生成された URL およびフォルダーメタデータのアセットパスが URL エンコードされません。GRANITE-26198：CQ-4271814 のホットフィックス
* Unzipping an archive with a folder having a percent sign (%) in its name can not be opened using [!DNL Experience Manager Assets] interface. NPR-29989：CQ-4270467 のホットフィックス
* タッチ操作対応UI:パブリケーションの管理ウィザードでは、参照がポストリクエスト本文のページの後に追加され、ページの後にすべてのアセットが発行され、ページがレンダリングされると、発行インスタンスの一部のアセットが失われます。 NPR-29985：CQ-4270724 のホットフィックス
* 名前に特殊文字（URI エンコードされる文字）を含む関連アセットに対して、アセットの関連付け解除機能が機能しません。NPR-30387：CQ-4274446 のホットフィックス
* コンテンツフラグメントを編集すると、間違ったユーザーでバージョンが作成されます。
* テナントベースのシステムで、コレクションの作成が途中で失敗します。NPR-30114：CQ-4272948 のホットフィックス
* アセット UI の列表示が現在のテナントの DAM ルートパスを無視して、すべてのテナント DAM パスにアクセスします。NPR-30636：CQ-4275481 のホットフィックス
* 挿入された画像を表示できてしまうので、制限されているファイルに対する警告ウィンドウ経由で、クロスサイトスクリプティング（XSS）攻撃を受ける可能性があります。NPR-30617：CQ-4270133 のホットフィックス
* MultiTenant:フォルダーのプロパティを保存するテナントは、「プロパティを編集できません。権限が不十分です。」 ので、紛らわしくなります。NPR-30545：CQ-4275333 のホットフィックス
* アセットセレクターダイアログでアセットを選択できないので、関連ソース置換機能を使用してソースを更新できません。NPR-30502：CQ-4275029 のホットフィックス
* [!UICONTROL DAMアセットの更新ワークフロー] — 大きなサイズのmp4ファイルのアップロード時に古い状態になっています。 NPR-30480：CQ-4271352 のホットフィックス
* ペイロードが空の場合、「レビュータスクを作成」機能が機能しないので、後続のレビュータスク関連アクションがすべて失敗します。NPR-30468：CQ-4274263 のホットフィックス
* Datapower によって Adobe スマートタグの接続に関する問題が発生します。NPR-30026：CQ-4269457 のホットフィックス
* Assets UI の列表示で、レールに残ったフィルターを開こうとするとエラーが発生します。NPR-30501：CQ-4273862 のホットフィックス
* アセットフォルダーの非公開のユーザーグループ（CUG）プロパティに LDAP から同期されたグループを追加した場合、グループの保存や取得がおこなわれません。NPR-30615：CQ-4274689 のホットフィックス
* フィルターの検索スタイルおよび方向フィールドのオートコンプリート値が検索クエリに適用されません。NPR-30620：CQ-4275724 のホットフィックス
* 名前にスペースや「&amp;」文字が含まれるフォルダーのアセット共有リンクで、一部のアセットに対して空白の灰色カードが表示されます。NPR-30557：CQ-4270187 のホットフィックス
* フォルダーメタデータスキーマフォームでデータ型が自動的に検出されないので、フォーム送信で関連するタイプヒントが作成されません。NPR-30599：CQ-4275227 のホットフィックス
* DMS7 のオーサリング UI で切り抜きと回転のアセット編集オプションが無効になっています。NPR-30118：CQ-4273221 のホットフィックス
* Share Link feature is not working on [!DNL Experience Manager] instance with DMS7 configuration. NPR-30080、NPR-30492：CQ-4273651 のホットフィックス
* Adding the [!DNL Dynamic Media]–Scene7 component to the page, and then publishing the page does not trigger the dmscene7 configuration every time. NPR-30641：CQ-4275962 のホットフィックス
* Added an IPSJobJournal in [!DNL Experience Manager] to create only one Intrusion Prevention Systems (IPS) job per processing profile. NPR-30490：CQ-4273614 のホットフィックス
* [!DNL Dynamic Media]:デフォルトのフィルターを追加し、公開ノードに複製されるアセットを除外する [!DNL Experience Manager] ようにしました。 NPR-30538：CQ-4274678 のホットフィックス
* 外部の再処理ワークフローが導入されて、複数のリソースがサポートされ、フォルダーをペイロードとして使用できるようになりました。ワークフローには 2 つのステップがあります。次のステップへのメタデータマップを通じてハンドルなしでアセットを再処理するステップと、単一の IPS ジョブですべてのアセットをアセットハンドルなしで S7 に再アップロードするステップです。For more details, see Configuring [!DNL Dynamic Media] Cloud Services. NPR-30489：CQ-4272903 のホットフィックス
* 正しい CSV の後に間違った CSV をアップロードすると、正しい CSV が消去されます。CQ-4277694、CQ-4277814 のホットフィックス
* 削除する投稿フォルダーに固有のアイコンが間違っています。CQ-4277580 のホットフィックス
* 「アセット投稿」タブのユーザーピッカーでユーザーを選択しても、ユーザーの名前がテーブルに表示されず、プロパティページのユーザーの削除ダイアログに間違ったテキストが表示されます。CQ-4277875 のホットフィックス
* ユーザーピッカーでユーザーを選択して「追加」をクリックしても、投稿者をアセット投稿フォルダーに追加できません。CQ-4277824、CQ-4278087 のホットフィックス
* ユーザーピッカーで小文字のユーザー名による検索が機能しません。CQ-4277958、CQ-4277930 のホットフィックス
* 管理者以外のユーザーでも、アセット投稿フォルダーの新しいフォルダーにアセットを公開できます。CQ-4278200 のホットフィックス
* 投稿者をアセット投稿フォルダーに追加するオプションが dam-user（管理者以外）にありません。CQ-4278192 のホットフィックス
* アセット投稿フォルダーに「作成」ボタンが表示されます。CQ-4277560 のホットフィックス
* Sorting search query by relevance returns [!DNL InDesign] documents along with [!DNL InDesign] templates. CQ-4273864 のホットフィックス
* ユーザーのメール ID が大文字の場合、以前にチェックアウトしたアセットをチェックインできません。CQ-4276575 のホットフィックス
* 削除操作は、選択されているプリセットにのみ適用され、操作後に画面上のリストが自動的に更新されると、既に更新されている他のプリセットが表示されます。CQ-4261461 のホットフィックス
* Configuring [!DNL Dynamic Media] Cloud Services in [!DNL Dynamic Media]–Hybrid mode results in multiple empty report suites created in [!DNL Analytics], and with no report suite id stored in [!DNL Experience Manager], resulting in report suite duplication. CQ-4249780 のホットフィックス
* Rename operation in [!DNL Experience Manager] asset to duplicated name fails to synchronize to Scene7. CQ-4276763 のホットフィックス
* ユーザー生成コンテンツが検索フィルターパネルに正しく表示されません。CQ-4273875 のホットフィックス
* 類似検索オプションが TIFF 画像に使用できません。CQ-4278238 のホットフィックス
* VideoPlayer で読み込み時にビデオをミュートするオプションが実装されました。CQ-4266465 のホットフィックス
* ビューア — ビデオビューア：poster=noneは、外部ビデオが使用されている場合に正しく機能しません。 CQ-4265536 のホットフィックス
* IE11 および MS Edge ブラウザーでビデオ再生中に待機アイコンが表示されます。CQ-4251539 のホットフィックス
* 3.8 SDKおよび5.13ビューアのREADMEファイルは更新されず、以前のリリースの情報が含まれています。 CQ-4273737 のホットフィックス
* コンテンツフラグメントが、変更を保存する前でもバージョン管理されます。NPR-30616：CQ-4273088 のホットフィックス
* サムネール処理で Asset#getMetadata(String) が Asset#getMetadataValueFromJcr(String) に置き換わります。NPR-30491：CQ-4273067 のホットフィックス
* jpg をアップロードすると、「ReplicateOnModifyWorker Replicating UPDATED」というメッセージがアセットごとに複数回表示され、パフォーマンスが低下します。
* 「アーカイブを抽出」機能を使用して zip アーカイブを解凍すると、名前やタイトルにパーセント（％）が含まれるフォルダーで問題が発生します。NPR-29990：CQ-4270467 のホットフィックス

### Sites {#sites-6520}

* LiveCopyの継承が壊れている場合、ライブコピーページには、LiveCopyリンクではなく言語コピーリンクが表示されます。 (NPR-30980)
* 新しいBlueprintの場合、レコード数が40を超えると、最初の40レコードのみが表示されます。 残りのレコードの空白行がBlueprintに表示されます。 (NPR-31182)
* テキストコンポーネントのリッチテキストエディター(RTE)プラグインは、日本語と韓国語のテキストに対して歪んだ文字を表示します。 (NPR-31331)
* リッチテキストエディター(RTE)では、埋め込みテーブルを埋め込みアイテムとして挿入することはリストできません。 (NPR-30879)
* 要素にインラインフォントサイズが適用され、初期設定のスキャフォールドのリッチテキストエディター(RTE)が予期せず適用される。 (NPR-31284)
* ユーザーが左側のパネルのフィールドにフォーカスし、キーボードショートカットを使用してコンテンツを貼り付けると、左側のパネルのフィールドからコピーしたコンテンツではなく、ページエディターのクリップボードのコンテンツが貼り付けられます。 (NPR-31172)
* ユーザが複数フィールドにファイルアップロードフィールドを追加すると、画像パスは、複数フィールドノードではなく、コンポーネントノードに保存されます。 (NPR-30882)
* ResponsiveGridExporter APIは、com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporterインターフェイスを返しません。 com.day.cq.wcm.foundation.model.implパッケージは、プライベートパッケージとして宣言されています。 (NPR-31398)
* 一部のExperienceFragmentsを含むページがエディター以外のモードで（プレフィックスが付いていない「作成者」で、または「発行者」で）開かれると、リクエストはHTTPステータスエラーコ `editor.html``wcmmode=disabled`ード500で終了します。 (NPR-30743)

### WCM - ページエディター {#wcm-page-editor-6520}

**製品の機能強化**

* 複数値のフィルターをサポートするために、より多くのMIMEタイプでDocumentタイプのオプションを拡張します。 CQ-4270694 のホットフィックス

### コンテンツフラグメント管理 {#content-fragment-management-6520}

* コンテンツフラグメントモデル UI で使用されるクエリが非常に遅く、最終的にエラーになります。CQ-4270807 のホットフィックス

### UI - 基礎 {#ui-foundation}

* 特定のユーザーインターフェイス内でユーザーが「m」、「p」、「e」を使用できないようにするショートカットトリガー。NPR-30355：GRANITE-26346 のホットフィックス
* Closing [!DNL Experience Manager Assets] Search UI does not reset the left rail to Content selection preventing the user from opening the filter rail the second time subsequently. NPR-30509：CQ-4274716 のホットフィックス
* Multi-tenant environment: [!DNL Experience Manager Assets] UI top navigation is not available and throwing JavaScript error. NPR-30104：GRANITE-26344 のホットフィックス

### 翻訳 {#translation-6520}

* 翻訳の問題 - 機械翻訳を使用して翻訳されているコンポーネントはごくわずかです。NPR-30079：CQ-4273764 のホットフィックス

### プラットフォーム {#platform-6520}

* [!DNL Experience Manager] のデフォルトメール送信者が TLS v1.2 を介してリモート SMTP サーバーにメールを送信できません。NPR-30476：GRANITE-26605 のホットフィックス

### プロジェクト {#projects-6520}

* フォルダー内のアセットを削除した後でも、dam:folderThumbnailPaths 値が更新されず、古いサムネールが表示されます。NPR-30424：CQ-4273667 のホットフィックス
* 「移動」オプションを完了しても、アセットのタイトルと名前が元のまま変更されません。NPR-30647：CQ-4276265 のホットフィックス

### コミュニティ {#communities-6520}

* ユーザー同期診断がまったく機能しません。NPR-30004、NPR-29943：CQ-4270287、CQ-4271348 のホットフィックス

### Sling {#sling}

* インスタンスを 6.3.3.2 から 6.5 にアップグレードすると、OSGi 設定が重複します。NPR-30130：CQ-4274016 のホットフィックス

### 統合 {#integration}

* パブリッシュインスタンスを再起動するまで、カスタマイズされたコンテンツがインスタンス上で正しく表示されません。NPR-30377：CQ-4273706 のホットフィックス
* Web サイトで Launch を設定すると、ライブラリアドレスの先頭にスラッシュ（/）が付加され、毎回手動の対応が必要になります。NPR-30694：CQ-4275501 のホットフィックス

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Packにはの修正が含まれていませ [!DNL Experience Manager Forms]ん。 They are delivered using a separate [!DNL Forms] add-on package. In addition, a cumulative installer is released that includes fixes for [!DNL Experience Manager Forms] on JEE. For more information, see [Install Experience Manager Forms add-on](#install-aem-forms-add-on-package) and [Install Experience Manager Forms JEE installer](#forms-jee-installer).

The key highlights for [!DNL Experience Manager] 6.5.2.0 forms are:

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager] Forms OSGi.

#### Forms アドオンパッケージ {#forms-add-on-package}

**バックエンド統合**

* AWS ホスト型負荷分散 URL を使用してフォームデータモデルを設定できません。NPR-30123：CQ-4273359 のホットフィックス
* Web Service Definition Language(WSDL)を使用してフォームデータモデル(FDM)を作成する際、次のエラー・メッセージが返 `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` されます：NPR-30477:CQ-4272921の修正プログラム

**Correspondence Management**

* 「通信作成用UI(CCR UI)のレンディションが、コンソールで次のエラーが発生して断続的に失敗する：
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**インタラクティブコミュニケーション**

* フォームデータモデルで必須とマークされたフィールドが、「通信を作成」UI（CCR UI）で必要に応じて表示されます。NPR-30623：CQ-4274902 のホットフィックス

**Forms - ワークフロー**

* 監視フォルダーのマッピングされていない出力変数が原因で、呼び出しが失敗します。CQ-4264451 のホットフィックス

**HTML5 のフォーム**

* カスタムコードまたはプロジェクトを2回目にデプロイすると、ページはレンダリングされず、次のエラーが発生します。

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539：CQ-4272509 のホットフィックス

* 参照モードで NonVisual Desktop Access を使用して HTML5 フォームを読み取る場合、Chrome ブラウザーがフォームデザインの各スケーラブルベクターグラフィック（SVG）の前に「グラフィック」を読み取ります。NPR-30449：CQ-4274732 のホットフィックス

#### Forms JEE インストーラー {#forms-jee-installer}

**Forms - Document Security**

* タイムスタンプ付きの署名を適用すると、次のエラーで失敗します：ALC-DSC-003-000 : com.adobe.idp.dsc.DSCInvocationException : 呼び出しエラー。NPR-30820：CQ-4275852 のホットフィックス

**Forms - ドキュメントサービス**

* 「SubmitURL」にアンパサンド（＆）が含まれている場合、renderpdf サーブレットに対して POST 要求がおこなわれると、ログに解析エラーが表示されます。NPR-30865：CQ-4278232 のホットフィックス

**Forms - Foundation JEE**

* HTMLtoPDFサービスで、JMXコンソールにmaxReuseCountが表示されない。 NPR-30134、NPR-30304：CQ-4273763 のホットフィックス
* Adding or editing a Web Service connection by invoking web services from [!DNL Experience Manager Forms] Workbench throws an error: ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105：CQ-4273217 のホットフィックス

### 含まれている機能パック {#feature-packs-included}

>[!NOTE]
>
>For [!DNL Experience Manager Forms] customers, it is essential to install [!DNL Experience Manager Forms] add-on package after installing any [!DNL Experience Manager] Service Pack, Cumulative Fix Pack, or Feature Pack.

#### Sites {#sites-feature-packs-included}

* Added a configuration property to allow exporting Experience Fragments directly to user-defined workspaces for [!DNL Adobe Target]. NPR-29189：CQ-4249782 のホットフィックス

#### Forms - ドキュメントサービス {#forms-document-services-1}

* Added &#39;Auto&#39; setting to `RenderAtClient` in `PDFFormRenderOptions` API for [!DNL Experience Manager Forms] OSGi. NPR-30759：CQ-4278193 のホットフィックス

## Adobe Experience Manager 6.5.1.0 {#release-6510}

[!DNL Adobe Experience Manager] 6.5.1.0は、パフォーマンス、安定性、セキュリティ、お客様向けの主要な修正、および2019年4月のGA(General Availability)以降にリリースされた機能強化を含む重要なリリ [!DNL Adobe Experience Manager]*ースです。* 6.5の上にインストールで [!DNL Experience Manager] きます。

このサービスパックリリースの主なハイライトは次のとおりです。

* 追跡イベントに dynamic-UI-state をカスタム属性として含めることが可能になりました。
* Included support for the delivery of 360-degree video assets in [!DNL Dynamic Media]–Scene7 mode.
* Enabled *Japanese Word Wrap* feature via the styles plugin of Rich Text Editor. For more information, see [Configure Japanese word wrap](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap)

### Assets

* DAM DMGateway インターフェイスが更新されて、S3 マルチパートがサポートされるようになりました。NPR-29740：CQ-4226303 のホットフィックス
* レンディションプレビュー `Only empty tenantId is currently supported` を6.5にアップグレードすると、エ [!DNL Experience Manager] ラーが発生する。NPR-29986:CQ-4272353の修正プログラム
* ジョブの削除を許可する削除ダイアログが表示されません。NPR-29720：CQ-4271074 のホットフィックス
* After adding asset title in the properties page, when a user attempts to close the page, [!DNL Experience Manager] opens the properties page again. NPR-29627：CQ-4264929 のホットフィックス
* VersioningTimelineEventProvider は、nt:version タイプのノードと共にルートバージョンを提供する必要があります。GRANITE-26063 のホットフィックス
* Implemented the ability to upload and play 360 spherical videos in [!DNL Experience Manager] DM-Scene7 mode. CQ-4265131 のホットフィックス
* ソースが編集されている場合、ライブコピーが間違ったステータスを取得します。CQ-4265451 のホットフィックス
* Enabled Multi-Site Manager support for [!DNL Experience Manager Assets]. CQ-4271453、CQ-4268621、CQ-4257491 のホットフィックス
* [!DNL Experience Manager] インターフェイスには、タイムラインヒストリーの現在のバージョンのアセットに対する追加のエントリが表示され、最新のチェックインコメントが表示されま [!DNL Adobe Asset Link]す。 CQ-4262864 のホットフィックス
* プロパティが見つからない場合、コンテンツフラグメントのタイムラインにエラーメッセージが表示されます。 CQ-4272560 のホットフィックス
* Scene 7 ビデオプレーヤーで全画面表示に拡大すると問題が発生します。CQ-4266700 のホットフィックス
* ZoomVerticalViewer：使用されている画像アセットが 1 つだけの場合に、パンボタンが表示されることがあります。CQ-4264795 のホットフィックス
* ライブコピーの子ノードを削除すると、liveRelationship の接続が解除される必要があります。CQ-4270395 のホットフィックス
* メタデータスキーマにグローバル設定のアイテムのみが含まれ、アクティブテナントのアイテムが欠落しています。URL の formPath 値が変更されても、デフォルト値に戻ります。NPR-29945：CQ-4262898 のホットフィックス
* Publish image presets to [!DNL Brand Portal] fails with 500 error code. NPR-29510：CQ-4268659 のホットフィックス

### Sites

* ロールアウト時に空のプロパティと複数のプロパティがブループリントから伝播されません。ブループリントを使用したライブコピーのリセットは、コンポーネントでは機能しません。NPR-29253：CQ-4264928、CQ-4264926、CQ-4267722 のホットフィックス
* CoralUI, when used with `Multifield`, stores the `fileReferenceParameter` at the component level instead of multifield level. NPR-29537：CQ-4266129 のホットフィックス
* Enhancement of [!DNL Experience Manager] text component and Text Editor to Japanese. NPR-29785：CQ-4265090 のホットフィックス
* タイムワープで復元されたページは、バージョン管理時に正しい画像を参照する必要があります。NPR-29431：CQ-4262638 のホットフィックス
* 親から子へのスタイルシステムノードの継承に関する問題。 NPR-29516：CQ-4270330 のホットフィックス
* An error message while setting up the social posting to [!DNL Facebook] authentication. NPR-29211：CQ-4266630 のホットフィックス
* コンテンツフラグメントにレンダリングされたサムネールに、日時フィールドの内部カレンダー表現が表示されます。NPR-29531：CQ-4269362 のホットフィックス
* Coral2 実装で「権限」タブを開いても、ボタンが表示されません。CQ-4269419 のホットフィックス

### Commerce

* e コマースの遅延コンテンツ移行を実行すると、ConstraintViolationException が発生します。NPR-29247：CQ-4264383 のホットフィックス

### コンテンツフラグメント管理

* Parsing error when opening a Content Fragment which has characters dollar `($)` and open brace `({)`. CQ-4270266 のホットフィックス

### エクスペリエンスフラグメント

* エクスペリエン [!DNL Experience Manager] スフラグメントの書き出し先 [!DNL Adobe Target]: CQ-4265469 のホットフィックス
* エクスペリエンスフラグメントのターゲットへの書き出しが、スマート画像で失敗する。 CQ-4269606 のホットフィックス

* カード表示で Omnisearch を通じてエクスペリエンスフラグメントを移動しようとすると、行き詰まります。CQ-4263848 のホットフィックス

### WCM - ページエディター

* 無効なセレクターを使用すると、クロスサイトスクリプティング（XSS）が反映されます。CQ-4270397 のホットフィックス

### レプリケーション

* `cq/replication/components/agent` コンポーネントの出力でユーザー提供のデータがエスケープされないので、保存されたクロスサイトスクリプティング（XSS）の脆弱性がある。CQ-4266263 のホットフィックス

### ワークフロー

* ダイアログ参加者のカレンダーピッカーフィールドが機能しません。NPR-29727：CQ-4270423 のホットフィックス

### WCM - SPA エディター

* 事前にレンダリングされたコンテンツをリモートエンドポイントから取得できるようになりました。CQ-4270238 のホットフィックス
* サーバー側でレンダリングされた SPA テンプレートページを開くと、ログに警告が記録されます。CQ-4270238 のホットフィックス

### WCM - MSM

* Upgrade to [!DNL Experience Manager] 6.4.3 makes Multi-Site Manager take a long time to roll out. CQ-4271410 のホットフィックス

### 統合

* BrightEdge 認証情報が失敗し、接続エラーが発生します。NPR-29168：CQ-4265872 のホットフィックス

* An exception message is displayed when trying to edit and save the [!DNL Experience Manager] launch configuration. NPR-29176：CQ-4265782／CQ-4266153 のホットフィックス

### ユーザーインターフェイス

* Foundation の追跡 API で特定のイベントを追跡中に、dynamic-UI-state をカスタム属性として追跡できるようになりました。GRANITE-26283 のホットフィックス
* 送信ボタンに追跡機能を設定できません。GRANITE-26326 のホットフィックス
* ウィザードで、送信ボタンに追跡機能を設定できません。NPR-29995、NPR-30025：CQ-4264289 のホットフィックス

### Communities

* メンバープロフィールページのドロップダウンに新しいバッジを整列配置できません。NPR-29381：CQ-4267987 のホットフィックス
* モデレーター権限のない訪問者とメンバーが、URL を貼り付けて未承認または承認待ちの投稿を表示できます。NPR-29724：CQ-4271124、CQ-4271441 のホットフィックス
* コミュニティにユーザーがログインする際、応答時間が長くなり、最大 40〜50 秒かかる場合があります。NPR-29677：CQ-4269444 のホットフィックス

### レプリケーション

* レプリケーションエージェントコンポーネントは、権限のないユーザーに機密情報が開示される脆弱性の影響を受けやすくなっています。NPR-29611：GRANITE-25070 のホットフィックス

* Session leak during OAuth for every replication to [!DNL Brand Portal]. NPR-30001：GRANITE-26196 のホットフィックス

### プロジェクト

* Publish [!DNL Experience Manager Assets] from [!DNL Experience Manager] Author /content/dam/mac folder to [!DNL Brand Portal] doesn&#39;t work. NPR-29819：CQ-4271118 のホットフィックス

### プラットフォーム

* キャッシュの無効化時に HtmlLibraryManager が crx-quickstart の内容をすべて削除します。NPR-29863：GRANITE-26197 のホットフィックス

### Felix

* Java11\を使用する場合、メモリ使用量の詳細はシステムコンソールに表示されません。 NPR-29669

### Forms

The key highlights for [!DNL Experience Manager Forms] 6.5.1.0 are:

* OSGi only: Added a new attribute `PAGECOUNT` in Output and Forms Service.

* OSGIのみ：Formsサービスを使用したスタティックPDFファイルの作成のサポートを有効にしました。
* 管理者およびルートユーザーに対して XMLForm.exe の権限が有効になりました。
* Dynamics オンプレミス統合で ADFS v3.0 がサポートされるようになりました。

#### Forms アドオンパッケージ

**バックエンド統合**

* 保護された Web サービス定義言語（WSDL）の取得に失敗します。NPR-29944：CQ-4270777 のホットフィックス
* When [!DNL Experience Manager Forms]  is installed on IBM WebSphere, creating a form data model based on SOAP fails. CQ-4251134 のホットフィックス
* Microsoft Dynamics オンプレミス統合で Active Directory Federation Services（ADFS）v3.0 がサポートされるようになりました。CQ-4270586 のホットフィックス
* データソースのタイトルが変更されても、更新されたタイトルがフォームデータモデルに表示されません。CQ-4265599 のホットフィックス
* エンティティまたは属性の名前にハイフンまたはスペースが含まれている場合、式はそのようなエンティティや属性を評価できません。 CQ-4225129 のホットフィックス

* プリミティブ文字列出力にコロンが含まれている場合、誤った出力が表示されます。 CQ-4260825 のホットフィックス

* REST API 出力からコンテンツが想定されない場合でも、フォームデータモデルの呼び出し操作でエラーが発生します。CQ-4268828 のホットフィックス

**アダプティブフォーム**

* 遅延読み込み中にアダプティブフォームフラグメントに新しいインスタンスを追加できません。NPR-29818：CQ-4269875 のホットフィックス
* 検証コンポーネントが「レコードのドキュメント」テンプレートのエラーを記録または表示しません。CQ-4272999 のホットフィックス
* アダプティブフォームのレイアウトエディターを無効にできるようになりました。CQ-4270810 のホットフィックス
* Restored the verify step for Adaptive Forms in [!DNL Experience Manager] 6.5. Hotfix for CQ-4269583

* Adaptive Form field validation failure breaks [!DNL Adobe Sign]. CQ-4269463 のホットフィックス
* When an [!DNL Experience Manager Forms] instance has more than 20 adaptive form fragments and name of all the form fragments starts with the same string, the search returns no or only recent 20 created fragments. CQ-4264414、CQ-4264914 のホットフィックス

* アダプティブフォームアプリケーションを大きなデータセットと共に使用すると、パフォーマンスの問題が発生する。. CQ-4235310 のホットフィックス

* 匿名アカウントでパブリッシュインスタンスにアクセスすると、GuideRuntime スクリプトを読み込めません。CQ-4268679 のホットフィックス

**Forms - インタラクティブコミュニケーション**

* インタラクティブコミュニケーションテンプレートで、許可されたコンポーネントのリストにヘッダーおよびフッターコンポーネントが表示されません。CQ-4237895 のホットフィックス
* 画像フィールドを含んだインタラクティブコミュニケーション印刷テンプレートを作成すると、グラフのタイトルが空白に設定されます。CQ-4264772 のホットフィックス
* グラフの線の色が削除されると、未定義に設定されます。CQ-4264762 のホットフィックス
* 変更の同期を維持すると、ドキュメントフラグメントで行ったレイアウトレイヤーの変更が消えます。 CQ-4266054 のホットフィックス
* テキストフィールドにバインドされたドキュメントフラグメント内部のフォームデータモデル要素で、継承アイコンが表示されずに、バインディングが可能になっています。CQ-4261089 のホットフィックス
* 印刷チャネルレンダリング API に、データを API のパラメーターとして渡すオプションがありません。CQ-4263540 のホットフィックス
* 連結タイプが「テキストフラグメント」から「なし」/「文字列フィールド/変数のデータモデルオブジェクト」に変更された場合、「エージェントが編集可能」チェックボックスがオフになると、エージェントの設定が表示されない。 CQ-4261953 のホットフィックス
* エージェントUIの送信時に、結果のWebデータjsonファイルに、継承がキャンセルされた連結されていないフィールドの情報が格納されます。 CQ-4265621 のホットフィックス

**Forms - ワークフロー**

* アダプティブフォームアプリのアウトボックスからフォームを再送信すると、データが失われます。NPR-28345：CQ-4260929 のホットフィックス
* 非可変ケースの場合、保存中にドキュメントが閉じられません。CQ-4269784 のホットフィックス
* アダプティブフォームアプリでは、Microsoft Windows 8.1 のサポートを終了しました。CQ-4265274 のホットフィックス
* When an image of more than 2 MB is attached as a field level attachment to a form in the Android version of [!DNL Experience Manager Forms] app, the app crashes. CQ-4265578 のホットフィックス

* タスクの割り当てでインタラクティブコミュニケーション印刷チャネルの事前入力オプションを有効にしました。CQ-4265577 のホットフィックス
* タスクの割り当て先グループのメンバーになるまで、共有タスクを表示できません。CQ-4248733 のホットフィックス
* Windows では、アダプティブフォームアプリでの JEE アプリケーションの保存または送信がブロックされます。CQ-4268704 のホットフィックス
* フォームデータモデル変数に関連付けられているフォームデータモデルが表示されません。CQ-4266554 のホットフィックス
* 変数サポートを使用したドキュメント署名のステータス変数がサポートされていません。CQ-4266312 のホットフィックス
* ウムラウト文字が含まれていると、ワークスペースからの送信に失敗します。CQ-4263172 のホットフィックス
* アップグレードされたセットアップで、ワークフローを編集用に開くと、監視フォルダーのユーザーインターフェイス（UI）にワークフロー名ではなくエラーが表示されます。CQ-4238579 のホットフィックス

**Forms - 管理**

* xsd または schema.json 以外の拡張子のファイルがアップロードされると、アップロードがおこなわれず、エラーメッセージも生成されません。CQ-4266716 のホットフィックス

**Forms - Correspondence Management**

* [!DNL Experience Manager Forms] 6.5通信を作成UI(CCR UI)は、6.3で作成された通信を開くことがで [!DNL Experience Manager Forms] きません。CQ-4266392の修正プログラム
* DDE データ型が数値型の場合、XDP の Sum 関数が機能しません。CQ-4227403 のホットフィックス
* アセットの公開時にアセットの最終変更時刻が更新されないので、メモリ内キャッシュの無効化ロジックを更新する必要があります。CQ-4250465 のホットフィックス
* DD およびレターのドキュメントフラグメントを公開できません。CQ-4272893 のホットフィックス

#### Forms JEE インストーラー

**PDF Generator**

* 64 ビット JDK では CAD ファイルから PDF への変換が失敗します。NPR-29924、NPR-29925：CQ-4272113 のホットフィックス
* HTML から PDF への変換の名前が PhantomJS から WebToPDF に変わりました。NPR-29933：CQ-4234545 のホットフィックス
* zip ファイルを PDF に変換中にエラーが発生します。CQ-4268628 のホットフィックス

**Forms - Designer**

* When a full accessibility check is performed on the static PDF created using [!DNL Experience Manager Forms Designer], the Primary Language check fails due to missing language attribute. CQ-4272923、CQ-4271002 のホットフィックス

**Forms - Document Security**

* ハードウェアセキュリティモジュール(HSM)を使用したデジタル署名が、Java 11およびJava 8\上のOSGi Linuxで機能していません。 NPR-29838：CQ-4270441 のホットフィックス
* ハードウェアセキュリティモジュール（HSM）を使用したデジタル署名が、JEE Linux およびサポートされているすべてのアプリサーバー（JBoss および Websphere）で機能しません。NPR-29839：CQ-4266721 のホットフィックス
* PAdES（PDF Advanced Electronic Signatures）を使用して PDF の署名を検証すると、InvalidOperationException が発生します。NPR-29842：CQ-4244837 のホットフィックス
* Office 2019\のドキュメントセキュリティ拡張機能のサポートを追加しました。 CQ-4254369、CQ-4259764 のホットフィックス

**Forms - ドキュメントサービス**

* PDFは、フォームフィールドを使用したPDF/A-1bへの変換に失敗し、表示方法が示されません。 NPR-29940：CQ-4269618 のホットフィックス

* OSGi:レンダリング中に生成されたページ数を特定できません。 NPR-28922：CQ-4270870 のホットフィックス
* のFormsサービスを使用したスタティックPDFファイルのサポートを有効にしまし [!DNL Experience Manager Forms OSGi]た。 NPR-28572：CQ-4270869 のホットフィックス
* XMLForm.exe の権限を変更できません。NPR-29828、NPR-29237：CQ-4267080 のホットフィックス
* The static PDF created by the [!DNL Experience Manager Forms] server’s output module does not populate the language attribute/tag with the language of the document created. NPR-27332：CQ-4271002 のホットフィックス

**Forms - Foundation JEE**

* 最終成果物で pdfg_srt を使用できないと、インストーラーが失敗します。NPR-29854：CQ-4270137 のホットフィックス
* LCBackupMode.sh が機能しません。NPR-29840：CQ-4269424 のホットフィックス
* WebSphere のユーザーインターフェイス（UI）から UDP ポート参照を削除する必要があります。CQ-4264782 のホットフィックス

### 含まれている機能パック

#### アセット — 含まれる

* Enabled Multi-Site Manager support for [!DNL Experience Manager Assets]. For more information, see [Reuse assets using MSM for Experience Manager Assets](https://helpx.adobe.com/experience-manager/6-5/help/assets/reuse-assets-using-msm.html). NPR-29199：CQ-4259922 のホットフィックス

#### サイト — 含まれる

* エクスペリエン [!DNL Experience Manager] スフラグメントの書き出し先 [!DNL Adobe Target]: For more details, see [The Experience Fragment Link Rewriter Provider - HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML). CQ-4265469 のホットフィックス

#### Forms - ドキュメントサービス  — 含まれる

* OSGiのみ：OutputおよびFormsサービスに新しい属性PAGECOUNTが追加されました。 NPR-28922：CQ-4270870 のホットフィックス
* OSGiのみ：Formsサービスを使用したスタティックPDFファイルの作成のサポートを有効にしました。 NPR-28572：CQ-4270869 のホットフィックス
* 管理者およびルートユーザーに対して XMLForm.exe の権限が有効になりました。NPR-29237：CQ-4267080 のホットフィックス

### OSGi バンドルとコンテンツパッケージ

The following text documents list the OSGi bundles and Content Packages included in [!DNL Experience Manager] 6.5.1.0

List of OSGi bundles included in [!DNL Experience Manager] 6.5.1.0

[ファイルを入手](assets/6_5-bundle-list.txt)

List of Content Packages included in [!DNL Experience Manager] 6.5.1.0

[ファイルを入手](assets/6_5-content-package-list.txt)
