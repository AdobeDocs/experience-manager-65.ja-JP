---
title: '[!DNL Adobe Experience Manager] 6.5 Service Pack リリースノート'
description: Release notes specific to [!DNL Adobe Experience Manager] 6.5 Service Pack 7
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 0389508f7870dd2ce6ed7bfc5fb8a9bc88fedffb
workflow-type: tm+mt
source-wordcount: '3796'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] 6.5 Service Pack リリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.7.0 |
| 種類 | Service Pack のリリース |
| 日付 | 2020年11月26日 |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## What&#39;s included in [!DNL Adobe Experience Manager] 6.5.7.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.7.0は、2019年4月の6.5リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの向上を含む重要なアップデートです。 Service Packは6. [!DNL Adobe Experience Manager] 5にインストールされています。

6.5.7.0で導入された主な機能および機能強化には、次のものが含まれ [!DNL Adobe Experience Manager] ます。

* [ [!UICONTROL 名前]]、[最終変更日]、 [!UICONTROL [] 最終ロールアウト日  ]の各プロパティを使用して、ロールアウトに使用できるライブコピーページを並べ替えます。

* ページの移動やMSMロールアウトを非同期操作として実行し、実行時のパフォーマンスへの影響を軽減します。

* カードと列の表示ーでデジタルアセットを並べ替えることができます。

* [!DNL Assets] アクセシビリティを [!DNL Dynamic Media] 強化しました。 強化された機能は、キーボードナビゲーション、スクリーンリーダーの使用、類似の支援テクノロジー(AT)の使用に関連しています。 詳しくは、 [[!DNL Assets] 拡張機能](#assets-6570) および [[!DNL Dynamic Media] 拡張機能を参照してください](#dynamic-media-6570)。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.22.5 に更新しました。

6.5.7.0で導入された機能および拡張機能の完全なリストについては、 [!DNL Experience Manager] 「 [6.5 Service Pack 7の新機能 [!DNL Adobe Experience Manager] 」を参照してください](new-features-latest-service-pack.md)。

6.5.7.0リリースに加えられた修正のリスト [!DNL Experience Manager] を次に示します。

### [!DNL Sites] {#sites-6570}

* ページの「 [!UICONTROL タイムラップ] 」オプションを開き、「タイムライン」サイドレールオプションを開いたままにし、 [!UICONTROL サイト] コンソールに移動すると、 `Failed to Load` エラーが発生します(NPR-34951)。

* 「 [!UICONTROL 時間の折り返し] 」オプションでは、選択した日付と時間の範囲(NPR-34951)の画像は表示されません。

* コンテンツフラグメントを含むページ `getHeader()` からフィルターが呼び出されると、 `java.lang.AbstractMethodError` エラーが発生します(NPR-34942)。

* ページのパスに複数のコンテンツサブ文字列が含まれる場合、プレビューはレンダリングに失敗し、バージョン比較関数も失敗します(NPR-34740)。

* コンポーネントの `String` type labelプロパティに数値を設定する場合は、コンポーネントを削除し、削除操作を元に戻すことができます。 ただし、削除を取り消すと、labelプロパティの値がから `String` (NPR-34739)に変更され `Long` ます。

* ページにレイアウトがロックされたテンプレートに基づいてエクスペリエンスフラグメントを追加する場合、次の例外が発生します(NPR-34632)。

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* フォルダーを移動すると、トラバーサルの問題が発生し、次のエラーが発生します(NPR-34554)。

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* 新しいアセットが作成、発行および新しい場所への移動されると、 `Request to complete move operation` ワークフローが作成され、中止された状態になります。 新しいアセットをアップロードし、 `move` 操作を実行すると、保留状態の `Request to complete move operation` ワークフローが作成されます(NPR-34543)。

* エクスペリエンスフラグメントを [!DNL Experience Manager] 6.5.2環境から [!DNL Target] Standardに書き出す場合、Workspaceプロパティが [!DNL Target] Standard(NPR-34557)で使用できないので、APIの呼び出しは失敗します。

* 「 [!UICONTROL 投稿を] 管理 [!UICONTROL 」オプションが非表示になる(NPR-34542)ので、ユーザーは「投稿を] 管理」オプションを使用してページを投稿することはできません。

* テキストにいくつかのスタイルを追加すると、 `<div>` タグがテキストに追加され、そのスタイルはテキストに適用できなくなります(NPR-34531)。

* ポップアップメニューで項目を選択し、必要なファイルを更新した場合、ダイアログの値は保存されません。他のメニューの必須フィールドは空です(NPR-34529)。

* カスタムテンプレートからページを作成し、それを設計図の階層内に移動すると、ライブコピーの階層内のページに表示されているページ開始から以前に削除されたコンポーネントが表示されます(NPR-34527)。

* 記事のスタイルがコンテンツに適用されると、そのスタイルを削除できなくなります(NPR-34486)。

* エクスペリエンスフラグメントのすべてのライブコピーとコピーは、同じ [!DNL Adobe Target] オファーID(NPR-34469)を指します。

* 番号付きのリスト(NPR-34455)に加え、箇条書きのリスト項目が表示されます。

* 「ソースと比較」オプションで、ソースページと編集済みのページ(NPR-34285)の違いが表示されません。

* ページを削除する場合、バージョン管理の詳細は設定できません(NPR-34159)。

* ユーザーが「 [!UICONTROL Open Selection] 」ダイアログ・オプションを選択すると、キーボード・フォーカスがページ上の非表示のコントロール(CQ-4307779、CQ-4293601)に移動します。

* 作成者上の発行済みフォルダーを移動した場合、そのフォルダーパスは発行インスタンス上で更新されません(CQ-4305144)。

* ユーザーが「すべてを `Enter` 選択 [!UICONTROL 」オプションのキーを選択した場合、キーボードフォーカスは「] コントロールを [!UICONTROL 作成] 」オプション(CQ-4293599)に移動しません。

* キーを選択すると、フォーカスは親コントロール(CQ-4293593、CQ-4293590)に復元されません。 `Esc`

* WCAGによる [!DNL Sites] UIおよびコアコンポーネントへの準拠が改善されました。(CQ-4293448)

* [!UICONTROL この] ページに対して、ズーム [!UICONTROL 機能と][!DNL Sites Editor] スケール機能が無効になっています(CQ-4282353)。

* 「右に回転」オプションを使用すると、スクリーンリーダーは現在の回転または反転の状態のナレーションを停止します(CQ-4282128)。

* 「完了」および「キャンセル」設定ダイアログボタンに、複数のタブストップがある(CQ-4274601)

* 同じレベルで同じ名前のページを移動することはできません(NPR-35041)。

* 「Clear (x)」オプションを選択した後、キーボードフォーカスが「 [!UICONTROL Filter] （フィルタ）」フィールドに移動しない(CQ-4293581)。

* 6.5.6.0にアップグレードすると、継承された段落システムの動作が変わり、正しく機能しません(NPR-35117)。 [!DNL Experience Manager]

* キーボードユーザーは、 [!UICONTROL ページの「] アクション [!DNL AEM Sites] 」セクションを選択した後、タブフォーカスを適切な順序に移動できません。(CQ-4307786)

* コンテンツフラグメントの編集時に、RTEツールバーのリンクターゲットメニューリストでオプションを選択すると、コンテンツフラグメント作成者ダイアログ開始がちらつきにします(CQ-4305532)。

* キーボードユーザーは、 [!UICONTROL コンポーネント] (Component)ドロップダウンリストの下向き矢印キーを使用してオプションを選択できません(CQ-4295097)。

* ページの「 [!UICONTROL アセット][!DNL Sites] 」タブにあるカレンダーメニューで日付を選択した場合、タブのフォーカスが適切な順序にずれることはありません(CQ-4293600)。

* サイトページの編集時に使用できるリンクまたはテキストオプションを削除した後で、キーボードユーザーの次または前のオプションにタブフォーカスが移動することはありません。(CQ-4293597)

* キーボードユーザーは、使用可能なオプションを表示してキーを押すと、 [!UICONTROL 「アクション]`Esc` 」セクションの「その他のオプション」にタブフォーカスを戻すことができません。(CQ-4293592)

* 「 [!UICONTROL 編集] 」モードで画像の「 [!UICONTROL 回転] 」オプションを有効にすると、タブのフォーカスが「回転」のままになるのではなく、キーボードユーザーの「 [!UICONTROL やり直し] 」オプションに移動します(CQ-4293587)。

* 「 [!UICONTROL リンクとアクション] 」タブにある「選択を [!UICONTROL 開く] 」ダイアログで、「キャンセル  」オプションの後に、タブフォーカスがページ内の非表示の要素に移動します(CQ-4293579)。

* キーボードユーザーが画像を編集する場合、「 [!UICONTROL Finish] 」オプションに移動し、Enterキーを押しても、スクリーンリーダーは完了を読み上げません。(CQ-4282351)

* 「 [!UICONTROL リンクとアクション] 」ダイアログで使用できる「上へ移動」および「下へ移動」オプションは、スクリーンリーダーおよびキーボードユーザーは使用できません。(CQ-4281120)

* キーボードユーザーは、 [!UICONTROL プロパティ] ページ(CQ-4293581、NPR-34653)の「閉じる」(X)オプションに移動した後、タブフォーカスを復元できません。

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0では、次の問題が [!DNL Assets] 修正され、次の機能強化が行われました。

* アクセシビリティに関して、このリリースで強化された機能は次 [!DNL Experience Manager Assets] のとおりです。 詳しくは、の [アクセシビリティ機能を参照してください [!DNL Assets]](/help/assets/accessibility.md)。

   * キーボードを使用してタイムラインを移動する場合、キーはフォーカスを失わずに「すべてを `Esc` 表示  」オプションを折りたたむことがあります。(CQ-4293598)
   * キーボードのTabキーを使用して移動する場合、追加したタグから最後のタグを削除した後も、タグフィールドはフォーカスを保持します(NPR-35109)。
   * [!DNL Experience Manager] コンポーネントに、スクリーンリーダーが使用する名前、役割、値に関する適切な情報が含まれるようになりました(NPR-34255)。
   * 「種類/サイズ」コンボボックス、「リンク」コンボボックス、「言語」コンボボックス、または「テキスト」編集ボックスを削除すると、キーボードフォーカスは次または前のユーザーインターフェイス要素、またはより関連性の高いユーザーインターフェイス要素(CQ-4293585)に戻ります。
   * 様々なオプションの上にポインターを置くと、選択やダウンロードなどのヒントが表示されます。 画面の表示比率を使用しているユーザーは、カーソルを合わせると表示されるコンテンツが原因で、ファイルのサムネールの表示が困難になる場合があります。 キーを使用してオプションを削除した後に、フォーカスを保持できるようになりました( `Escape` CQ-4293554)。
   * ページ内にあるグリッドからグリッドセルを選択すると、フォーカスが画面に表示されるアクションバーに移動します(CQ-4282127)。
   * ビジュアルユーザーは、通常のテキストとリンクを区別できます。これは、 [!DNL Experience Manager] ホームページ内のすべてのソリューションへのリンクに視覚的なヒント（下線と山形のアイコン）が表示されるためです。(CQ-4282072)

* 次のようなユーザーエクスペリエンスの拡張が、で行われま [!DNL Assets]す。

   * カードの表示と列の表示(NPR-35097)でアセットの並べ替えを有効にします。

* 6.5にアップグレードした後、Assets HTTP APIを使用してJSONファイルが生成される場合、ファイルで使用されているエンコーディングに問題があります(NPR-35129)。

* コレクションを作成する権限が与えられていないグループのユーザー（「コレクションを作成」オプションは使用できません）は、引き続きURL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` (NPR-35115)に直接アクセスしてコレクションを作成できます。

* 名前順に並べ替えると、検索されたアセットは大文字と小文字が区別されます。 これにより、検索結果で順番に表示される大文字と小文字の違いに基づいて、2つの異なる並べ替えリストが作成されます(NPR-35068)。

* コンテンツフラグメントをエディターで開くと、警告メッセージ(`Invalid value specified for a metadata property`)がエラーログに記録されます(NPR-35012)。

* 管理者権限を持たないユーザーは、 [Experience Manager] ・デスクトップ・アプリを使用して、期限切れのアセットを編集できます。 (NPR-34993).

* 同じAssetをAssetsユーザインターフェイスにドラッグして新しいバージョンを作成した場合、メタデータの変更は永続的ではありません(NPR-34940)。

* コレクションを編集する際、ユーザーはコレクションのタイトルを削除して、変更を正常に保存できます(NPR-34889)。

* 重複画像をアップロードする際に、削除オプションが表示されます。 「削除」を選択すると、画像がアップロードされます。 DAM Update Assetワークフローもトリガーされます(NPR-34744)。

* ととを使用 [!DNL Adobe Asset Link][!DNL Adobe InDesign]する場合、検索結果にはフォルダーとコレクションは含まれませんが、アセットのみが含まれます(NPR-34699、CQ-4303666)。

* カードの表示にカーソルを重ねると、カード内のクイックアクションに（自動的に）フォーカスした結果として、画面がスクロールされます(NPR-34514)。

* 複数のアセットのプロパティを一括して編集する場合、「 [!UICONTROL 保存] 」オプションを選択すると、バルクエディタの表示が閉じ、メイン [!DNL Assets] ページにリダイレクトされます。 この動作は、「 [!UICONTROL 保存して閉じる] 」オプションの動作と同じで、予期されない動作です(NPR-34546)。

* スマートコレクションの保存後に、正しいユーザーインターフェイス設定が表示されません。 クエリは正しく保存されますが、インターフェイスには常に最後に追加されたOption predicate(NPR-34539)が表示されます。

* にアセットを追加する場合、名前空間 [!DNL Experience Manager]のないメタデータは読み込まれません(NPR-34530)。

* フォルダー上でアセットをドラッグして移動する場合、ユーザーインターフェイスには、「ライトボックスに [!UICONTROL ドロップ」および「コレクションに] ドロップ 」オプションも表示されます。 移動操作がキャンセルされた場合でも、ユーザインターフェイスは後者の2つのオプション(NPR-34526)を引き続き表示する。

* このシンボル `%>` は、コレクションページ(NPR-34499)に表示されます。

* 列表示では、上下にスクロールすると、すべてのアセットが表示される前に、重複フォルダーとアセット名が [!DNL Assets] 表示されます(NPR-34464)。

* パブリックフォルダーを作成した直後にプライベートフォルダーを作成した場合、パブリックフォルダーはプライベートフォルダー設定(NPR-34415)を使用します。

* カード表示では、カードはアルファベット順に表示されず、カードをアルファベット順に並べ替えることはできません(NPR-34234)。

* カスケード・ルールを再度開いても、ユーザー・インターフェイスでの選択は維持されません(CQ-4301452)。

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* アクセシビリティに関して、次の機能強化が [!DNL Dynamic Media] (CQ-4290306)で行われました。 詳しくは、 [アクセシビリティ機能( [!DNL Dynamic Media]](/help/assets/accessibility-dm.md))を参照してください。

   * スクリーンリーダー（JAWS、ナレーター）は、埋め込みサイズメニューオプションのメニュー項目の名前、役割、状態をナレーションします(CQ-4290927)。
   * ユーザーは、 `Tab` キー(CQ-4290926)を使用して電子メールリンクダイアログ内を移動できます。
   * スクリーンリーダーの機能強化(CQ-4290623、CQ-4290622)を考えると、ビデオエンコーディングプロファイルを作成する場合のワークフローはより使いやすくなります。
   * キーを使用してナビゲーションする場合、フォーカスはワークフロー内の適切なユーザーインターフェイス要素に移動し、インタラクティブビデオを作成します(CQ-4290621、CQ-4290620、CQ-4290619)。 `Tab`
   * 発行ページ、アセットを編集ページ、スマートトリミングを編集ページ、および画像セットエディタページが、Web標準に準拠するように改善されました。 支援テクノロジー(AT)を使用して、これらのページ内を簡単に移動し、画像の切り抜きなどの操作を行うことができるようになりました。(CQ-4290617、CQ-4290616、CQ-4290613、CQ-4290612)、CQ-4290610、CQ-4290614)
   * ビューアが改善され、ユーザーがキーボードを使用してナビゲートできるようになりました。(CQ-4290615)
   * キーボードおよびスクリーンリーダーのユーザーは切り抜き機能(CQ-4290609)を使用できます。
   * キーボードユーザーは、ホットスポットをより適切に管理できます(CQ-4290604、CQ-4290603)。

* 会社名とフォルダー名が同じ(NPR-31340) [!DNL Experience Manager] 場合、リモートイメージセットは編集できません。

* ホットスポットを画像に追加した後、または [!DNL Dynamic Media] ビデオや画像を使用して編集した後に出力をプレビューしようとすると、zインデックスの順序 [!DNL Dynamic Media][!DNL Experience Fragment] が正しくなくなります。(CQ-4307267)

* [!DNL Dynamic Media] 混在メディアセットが再処理されると、同期に失敗します。(CQ-4307184)

* 自動同期が設定されているフォルダーにアセットが移動され [!DNL Dynamic Media] た場合、そのアセットは同期されません。(CQ-4307122)

* [!DNL Dynamic Media] ネイティブのHTML5ビデオコントロール(CQ-4306977、CQ-4306727)を使用してiOSデバイスでビデオが再生されない。

* SmartCropが適用されている画像をダウンロードできません。(CQ-4304558)

* ダイナミックメディアに選択的にフォルダーを発行することはできません(CQ-4304526)。

* からビデオファイルを非公開にしても、設定 [!DNL Experience Manager] 済みのScene7導入からアダプティブビデオセットの公開が取り消されません(CQ-4304405)。

* パノラマ画像アセットをパノラマメディアコンポーネントに追加し、ページを更新すると `Uncaught ReferenceError: $ is not defined` エラーが発生します(CQ-4302810)。

* ビ [!UICONTROL ューアプリセットエディタ](Viewer Presets Editor [!UICONTROL )で] PanoramicImage/PanoramicImage_VRプリセットを編集する場合、コンポーネント内の `PanoramicView``PANORAMICVIEW_AUTOROTATE` 修飾子ラベルは使用できません(CQ-4302443)。

* ビデオがMixedMediaSet内の最初でない場合、ビデオキャプションは表示されません。(CQ-4298161)

* iPhone携帯端末上のHTML5 eCatalogビューアで、ページをめくったり、ページをめくったりすることはできません。(CQ-4296611)

* モバイルデバイスでスウォッチをスクロールすると、表示に戻るまで数秒間、スウォッチが表示領域の右と外にスクロールします(CQ-4296439)。

* ビューアプリセットのマスターレコードを作成すると、CSSとアートワークは公開されず、ビューアプリセットのみが公開されます(CQ-4262205)。

* インタラクティブビデオ/画像コンポーネントで、特定のホットスポットに対してエクスペリエンスフラグメントをリンクしようとすると、  選択したエクスペリエンスフラグメントのパスは表示されません。 代わりに、パスフィールド(NPR-35146、CQ-4298136)から空の値が返されます。

* IVVエディター(CQ-4308560)でエクスペリエンスフラグメントをプレビューできません。

* 画像にホットスポットを追加してエクスペリエンスフラグメントを選択する場合、サブフォルダーとエクスペリエンスフラグメントのバリエーションを選択できません(CQ-4307455)。

* 画像以外のアセットは、アップロード後に公開済みとして表示されません(CQ-4306415)。

#### [!DNL Experience Manager] 3Dアセット {#three-d-assets-6570}

* `DAM CQ MIME Type` サービスは、3Dアセットに誤ったMIMEタイプを適用し、誤ったレンダリングが行われます(NPR-34731)。

### [!DNL Commerce] {#commerce-6570}

* Commerce製品収集ユーザーインターフェイスでは、1つのコレクション(NPR-34502)内の15個を超える製品はリストされません。

### プラットフォーム {#platform-6570}

* HTTPSを使用したHTTPセッションは無効にされません(NPR-35083)。
* ユーザーインターフェイス `NullPointerException` から日別または週別のメンテナンスタスクを開始すると、Aが返されます(NPR-34953)。
* W3Cバリデーターは、準拠しているクライアントライブラリのJavaScriptファイルに関する警告をレポートします(NPR-34898)。
* この `AudienceOmniSearchHandler` 関数は、非推奨のインデックス(NPR-34870)を使用します。
* Experience Managerからサインアウトしても、cookieはクリアされません(NPR-34743)。
* タグ名に特殊文字(NPR-34357)が含まれている場合、 `findByTitle``TagManager` APIの機能は動作しません。
* ユーザー同期パッケージを読み込むプロセスが失敗する(NPR-34399)。
* コンポー `ariaLabel` ネントに、および `ariaLabelledby``Coral.Masonry` プロパティのサポートが追加されました(GRANITE-29962)。
* 最新のコアコンポーネントパッケージをインストールした後、コンテンツフラグメントを含むページに対してディスパッチャーキャッシュが更新されない(CQ-4306788)。
* ローカライズされたタグ名が引用符(`"`)で囲まれていると、ユーザーインターフェイスに正しく表示されません(CQ-4305439)。

### ユーザーインターフェイス {#ui-6570}

* コンポーネントプロパティの「 [!UICONTROL リンク先] 」フィールドに、指定した文字列と一致しないオートコンプリートの提案が表示されます(NPR-34865)。

* 2日間(NPR-35280)の間に毎日のメンテナンスウィンドウを配信するようにスケジュールすると、AEMで次のエラーメッセージが表示されます。

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### 統合 {#integrations-6570}

* 既存の [!DNL Adobe Launch] 設定の編集に失敗します(NPR-35045)。
* IMSの設定と [!DNL Experience Fragments] 環境(NPR-34555)を使用している [!DNL Adobe Target][!DNL Adobe Target Standard] 場合は、に書き出すことはできません。
* 「 [!UICONTROL 作成] 」オプションは、フォルダーから [!UICONTROL オーディエンスページ(NPR-35151)に移動すると、] オーディエンス  ページに表示されます。

### Sling {#sling-6570}

* デフォルトのログイン正常性チェックは、存在しないユーザーの資格情報を検証します(NPR-34686)。

### 翻訳プロジェクト {#translation-6570}

* で翻訳プロジェクトをキャンセルする場合 [!DNL Experience Manager]、キャンセル要求は翻訳プロバイダ(NPR-34433)に送られない。

### [!DNL Communities] {#communities-6570}

* 製品内の不公平な用語の例はすべて、受け入れられた等価語(NPR-34311)に置き換えられる。
* [!DNL Google+] は、ソーシャルシェアオプションのリスト(NPR-33877)から削除されました。

### [!DNL Brand Portal] {#brandportal-6570}

* ユーザインターフェイスは、 [!UICONTROL リスト表示] (NPR-34728)でのアセットの選択に応答しません。

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 予定されている [!DNL Experience Manager] Service Packのリリース日の1週間後に、アドオンパッケージをリリースします。

セキュリティ更新について詳しくは、「 [Experience Managerセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)」を参照してください。

## Install 6.5.7.0 {#install}

**設定要件と詳細情報**

* AEM 6.5.7.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Service Packのダウンロードは、Adobe [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)(SDM)で入手できます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.5.7.0 をインストールしてください。

>[!NOTE]
>
>Adobe does not recommend removing or uninstalling the [!DNL Adobe Experience Manager] 6.5.7.0 package.

### サービスパックのインストール {#install-service-pack}

既存のAdobe Experience Manager6.5インスタンスにService Packをインストールするには、次の手順を実行します。

1. インスタンスが更新モードの場合（これは、インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 Adobeでは、インスタンスの現在の稼働時間が長い場合は再起動を推奨します。

1. インストールする前に、 [Experience Managerインスタンスのスナップショットまたは新規バックアップを作成し] ます。

1. Service Packを [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip)（ソフトウェア配布）からダウンロードします。

1. Open Package Manager and click **[!UICONTROL Upload Package]** to upload the package. 詳しくは、「 [パッケージマネージャー](/help/sites-administering/package-manager.md)」を参照してください。

1. Select the package and click **[!UICONTROL Install]**.

1. S3コネクタを更新するには、Service Packのインストール後にインスタンスを停止し、既存のコネクタをinstallフォルダーに指定された新しいバイナリファイルに置き換えてから、インスタンスを再起動します。 See [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Service Packのインストール中に、Package Manager UIのダイアログが閉じることがあります。 Adobeでは、エラーログが安定するのを待ってからデプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**自動インストール**

作業インスタンスにAdobe Experience Manager6.5.7.0を自動的にインストールするには、次の2つの方法があります。

A.サーバーがオンラインで使用可能になったら、パッケージを `../crx-quickstart/install` フォルダーに配置します。 パッケージが自動的にインストールされます。

B. Package Managerの [HTTP APIを使用します](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)。 ネストされたパッケージ `cmd=install&recursive=true` がインストールされるようにを使用します。

>[!NOTE]
>
>Adobe Experience Manager6.5.7.0は、Bootstrapのインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ(`/system/console/productinfo`)の「インストール済み製品 `Adobe Experience Manager (6.5.7.0)` 」に、更新済みのバージョン文字列が表示され ます。

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. OSGiバンドル `org.apache.jackrabbit.oak-core` はバージョン1.22.3以降です(Webコンソールを使用： `/system/console/bundles`)をクリックします。

このリリースで動作が確認されたプラットフォームについて詳しくは、 [技術要件を参照してください](/help/sites-deploying/technical-requirements.md)。

### Adobe Experience Manager Formsアドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 予定されている [!DNL Experience Manager] Service Packのリリース日の1週間後に、アドオンパッケージをリリースします。

>[!NOTE]
>
>AEM Forms を使用していない場合はスキップしてください。Adobe Experience Manager Formsの修正は、別のアドオンパッケージを通じて提供されています。

1. Adobe Experience ManagerService Packがインストールされていることを確認します。
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### JEEへのAdobe Experience Manager Formsのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE上のAdobe Experience Manager Formsの修正は、別のインストーラーを使用して提供されています。

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

### UberJar {#uber-jar}

Experience Manager6.5.7.0のUberJarは、 [Maven Centralリポジトリで使用できます](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/)。

MavenプロジェクトでUberJarを使用するには、UberJarの使用 [方法を参照し](/help/sites-developing/ht-projects-maven.md) 、プロジェクトPOMに次の依存関係を含めます。

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.7</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJarおよびその他の関連アーティファクトは、AdobeのパブリックMavenリポジトリ(`repo.adobe.com`)ではなく、Maven Centralリポジトリで使用できます。 メインのUberJarファイルの名前がに変更され `uber-jar-<version>.jar`ます。 したがって、タグに値 `classifier`を `apis` 含む `dependency` タグはありません。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

以下は、6.5.7.0で非推奨としてマークされている機能と機能のリストです。 [!DNL Experience Manager] 機能は、最初は非推奨としてマークされ、今後のリリースで削除されます。 通常は、代替オプションが提供されます。

機能または機能を配置で使用するかどうかを確認します。 また、別のオプションを使用するように実装を変更することを計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | AEM **[!UICONTROL クラウドサービスのオプトイン画面は非推奨です]** 。 AEM 6.5で更新されたAEMとターゲットの統合により、AdobeIMSとI/Oを介した認証を使用するTarget Standard APIがサポートされ、AEMページの解析とパーソナライゼーションの実装でAdobe開始の役割が増加しているため、オプトインウィザードは機能的に無関係になりました。 | 各AEMクラウドサービスを介して、システム接続、AdobeIMS認証、AdobeI/O統合を設定します。 |
| コネクタ | AEM 6.5では、JCR Connector for Microsoft SharePoint 2010およびMicrosoft SharePoint 2013のAdobeが非推奨です。 | 該当なし |

## 既知の問題 {#known-issues}

* Experience Manager6.5.7.0のインストール時に、 `error.log` ファイル内の次のエラーを無視します。

   ```TXT
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy(1314)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy(1316)] : Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy(1315)] : Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.ClassNotFoundException: com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy not found by com.day.cq.dam.cq-dam-core [331])
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.collection.CollectionCreationListenerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortaltRoleProviderDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)[com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy] :  Cannot register component (org.osgi.service.component.ComponentException: The component name 'com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy' has already been registered by Bundle 331 (com.day.cq.dam.cq-dam-core) as Component of Class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   
   com.day.cq.dam.cq-dam-core bundle com.day.cq.dam.cq-dam-core:5.12.276 (331)BundleComponentActivator : Unexpected failure enabling component holder com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy (java.lang.IllegalStateException: Could not load implementation object class com.day.cq.dam.core.impl.team.MediaPortalShareHandlerDummy)
   ```

* インスタンスを6.5から6.5.7.0バージョンにアップグレードする場合は、 [!DNL Experience Manager] ファイルで `RRD4JReporter``error.log` 例外を表示できます。 インスタンスを再起動して問題を解決します。

* 6.5 Service Pack 5または [!DNL Experience Manager] 以前のService Packを6.5にインストールした場合は、アセットのカスタムワークフローモデル（で作成）のランタイムコピーが [!DNL Experience Manager]`/var/workflow/models/dam`削除されます。
ランタイムコピーを取得する場合、Adobeでは、HTTP APIを使用して、カスタムワークフローモデルのデザイン時コピーをそのランタイムコピーと同期することを推奨します。
   `<designModelPath>/jcr:content.generate.json`.

* AdobeメタデータスキーマのFormsエディタ [!UICONTROL 、およびルールの] 定義ダイアログを使用した [!UICONTROL メタデータスキーマのFormsエディタでカスケーディングルールを編集および作成する際に問題が発生した場合は、カスタマーケアにお問い合わせください] 。 既に作成および保存されているルールは、期待どおりに動作しています。

* If a folder in the hierarchy is renamed in [!DNL Experience Manager Assets] and the nested folder containing an asset is published to [!DNL Brand Portal], the title of the folder is not updated in [!DNL Brand Portal] until the root folder is published again.

* ユーザーがアダプティブフォームで初めてフィールドを設定することを選択した場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドの設定を選択すると、問題が解決します。

* インストール後に [!UICONTROL 接続されたアセットの設定] (Connected Assets Configuration `cq-remotedam-client-ui-content` )ウィザードが404エラーメッセージを返す場合は、Package Managerを使用して、パッケージ `cq-remotedam-client-ui-components` とパッケージを手動で再インストールします。

* AEM 6.5.x.xのインストール中に、次のエラーおよび警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して AEM に Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計機能が使用されると、アダプティブフォームのサーバー側検証に失敗します。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ダイナミックメディアのインタラクティブ画像のホットスポットは、買い物かご可能なバナービューアでアセットをプレビューすると表示されません。

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

AEM 6.5.7.0に含まれるOSGiバンドルとコンテンツパッケージに関する次のテキストドキュメントリストです。

* [AEM 6.5.7.0 に含まれている OSGi バンドルの一覧](assets/6570_bundles.txt)

* [AEM 6.5.7.0 に含まれているコンテンツパッケージの一覧](assets/6570_packages.txt)

## 制限付きWebサイト {#restricted-sites}

これらのWebサイトは、お客様のみ利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* カスタマーサポート [への問い合わせ方法を参照](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5リリースノート](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 製品ページ](https://www.adobe.com/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Adobe優先度の製品アップデートの購読](https://www.adobe.com/subscription/priority-product-update.html)

