---
title: '[!DNL Adobe Experience Manager] 6.5 Service Pack リリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 Service Pack 7に関するリリースノート'
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: fa8d8c9a001b56006f1c0a30eb5a342754e63573
workflow-type: tm+mt
source-wordcount: '4227'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] 6.5 Service Pack リリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.7.0 |
| 型 | Service Pack のリリース |
| 日付 | 2020年11月26日 |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip) |

<!-- TBD: Update the SD link when SP7 is available. -->

## [!DNL Adobe Experience Manager] 6.5.7.0 {#what-s-included-in-aem}に含まれるもの

[!DNL Adobe Experience Manager] 6.5.7.0は、2019年4月の6.5リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの向上を含む重要なアップデートです。サービスパックは[!DNL Adobe Experience Manager] 6.5にインストールされています。

[!DNL Adobe Experience Manager] 6.5.7.0で導入された主な機能と強化された機能は次のとおりです。

* [!UICONTROL 名前]、[!UICONTROL 最終変更日、]、[!UICONTROL 最終ロールアウト日]の各プロパティを使用して、ロールアウトに使用できるライブコピーページを並べ替えます。

* ページの移動やMSMロールアウトを非同期操作として実行し、実行時のパフォーマンスへの影響を軽減します。

* カードと列の表示ーでデジタルアセットを並べ替えることができます。

* [!DNL Assets] アクセシビリティを [!DNL Dynamic Media] 強化しました。強化された機能は、キーボードナビゲーション、スクリーンリーダーの使用、類似の支援テクノロジー(AT)の使用に関連しています。 [[!DNL Assets] enhancements](#assets-6570)および[[!DNL Dynamic Media] enhancements](#dynamic-media-6570)を参照してください。

* [パフォーマンスを最適化するためのフォームデータモデルHTTPクライアント](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) 設定。

* [レイアウトモードで各](../../help/forms/using/resize-using-layout-mode.md#resize-components) コンポーネントのリセットオプションを使用できる

* [!DNL Experience Manager] 6.5 Service Pack 7Formsは、次の点でパフォーマンスが向上しました。

   * アダプティブフォームを送信する際に、サーバー上のフィールド値を検証する。

   * [!DNL Automated Forms Conversion service]を使用してPDFフォームをアダプティブフォームに変換する。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.22.5 に更新しました。

[!DNL Experience Manager] 6.5.7.0で導入された機能と拡張機能の完全なリストについては、[ [!DNL Adobe Experience Manager] 6.5 Service Pack 7](new-features-latest-service-pack.md)の新機能を参照してください。

[!DNL Experience Manager] 6.5.7.0リリースでの修正のリストを以下に示します。

### [!DNL Sites] {#sites-6570}

* ページの[!UICONTROL タイムラップ]オプションを開き、タイムラインサイドパネルのオプションを開いたままにし、[!UICONTROL サイト]コンソールに移動すると、`Failed to Load`エラーが発生します(NPR-34951)。

* [!UICONTROL タイムラップ]オプションでは、選択した日付と時間の範囲(NPR-34951)の画像は表示されません。

* フィルターがコンテンツフラグメントを含むページから`getHeader()`を呼び出すと、`java.lang.AbstractMethodError`エラーが発生します(NPR-34942)。

* ページのパスに複数のコンテンツサブ文字列が含まれる場合、プレビューはレンダリングに失敗し、バージョン比較関数も失敗します(NPR-34740)。

* コンポーネントの`String`タイプラベルプロパティに数値を設定すると、コンポーネントを削除して削除操作を元に戻すことができます。 ただし、削除を取り消すと、labelプロパティは`String`から`Long`に変更されます(NPR-34739)。

* ページにレイアウトがロックされたテンプレートに基づいてエクスペリエンスフラグメントを追加する場合、次の例外が発生します(NPR-34632)。

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* フォルダーを移動すると、トラバーサルの問題が発生し、次のエラーが発生します(NPR-34554)。

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* 新しいアセットが作成、発行および新しい場所への移動されると、`Request to complete move operation`ワークフローが作成され、「中止」の状態になります。 新しいアセットをアップロードし、`move`操作を実行すると、保留状態の`Request to complete move operation`ワークフローが作成されます(NPR-34543)。

* エクスペリエンスフラグメントを[!DNL Experience Manager] 6.5.2環境から[!DNL Target]標準に書き出す場合、API呼び出しは失敗します。これは、ワークスペースプロパティが[!DNL Target]標準(NPR-34557)で使用できないためです。

* [!UICONTROL 「パブリケーション]を公開」オプションが消える(NPR-34542)ので、[!UICONTROL 「パブリケーション]を管理」オプションを使用してページを公開することはできません。

* テキストにいくつかのスタイルを追加すると、`<div>`タグがテキストに追加され、そのスタイルをテキストに適用できなくなります(NPR-34531)。

* ポップアップメニューで項目を選択し、必要なファイルを更新した場合、ダイアログの値は保存されません。他のメニューの必須フィールドは空です(NPR-34529)。

* カスタムテンプレートからページを作成し、それを設計図の階層内に移動すると、ライブコピーの階層内のページに表示されているページ開始から以前に削除されたコンポーネントが表示されます(NPR-34527)。

* 記事のスタイルがコンテンツに適用されると、そのスタイルを削除できなくなります(NPR-34486)。

* エクスペリエンスフラグメントのすべてのライブコピーとコピーは、同じ[!DNL Adobe Target]オファーID(NPR-34469)を指します。

* 番号付きのリスト(NPR-34455)に加え、箇条書きのリスト項目が表示されます。

* 「ソースと比較」オプションで、ソースページと編集済みのページ(NPR-34285)の違いが表示されません。

* ページを削除する場合、バージョン管理の詳細は設定できません(NPR-34159)。

* ユーザーが「[!UICONTROL 選択範囲を開く]」ダイアログオプションを選択すると、キーボードフォーカスはページ上の非表示のコントロール(CQ-4307779、CQ-4293601)に移動します。

* 作成者上の発行済みフォルダーを移動した場合、そのフォルダーパスは発行インスタンス上で更新されません(CQ-4305144)。

* ユーザーが「[!UICONTROL すべてを選択]」オプションで`Enter`キーを選択した場合、キーボードフォーカスは[!UICONTROL コントロールを作成]オプション(CQ-4293599)に移動しません。

* `Esc`キーを選択した場合、フォーカスは親コントロール(CQ-4293593、CQ-4293590)に戻りません。

* [!DNL Sites] UIおよびコアコンポーネントのWCAG準拠が改善されました。(CQ-4293448)

* [!UICONTROL この] ページでは、Zoomand   [!DNL Sites Editor]  Scale関数が無効になっています(CQ-4282353)。

* 「右に回転」オプションを使用すると、スクリーンリーダーは現在の回転または反転の状態のナレーションを停止します(CQ-4282128)。

* 「完了」および「キャンセル」設定ダイアログボタンに、複数のタブストップがある(CQ-4274601)

* 同じレベルで同じ名前のページを移動することはできません(NPR-35041)。

* 「Clear (x)」オプションを選択した後、キーボードフォーカスが[!UICONTROL Filter]フィールド(CQ-4293581)に移動しない。

* [!DNL Experience Manager] 6.5.6.0にアップグレードすると、継承された段落システムの動作が変更され、適切に動作しません(NPR-35117)。

* キーボードユーザーは、[!DNL AEM Sites]ページの[!UICONTROL アクション]セクションを選択した後、適切な順序にタブフォーカスを移動できません(CQ-4307786)。

* コンテンツフラグメントの編集時に、RTEツールバーのリンクターゲットメニューリストでオプションを選択すると、コンテンツフラグメント作成者ダイアログ開始がちらつきにします(CQ-4305532)。

* キーボードユーザーは、[!UICONTROL コンポーネント追加]ドロップダウンリストの下向き矢印キーを使用してオプションを選択できません(CQ-4295097)。

* [!DNL Sites]ページ(CQ-4293600)の[!UICONTROL アセット]タブのカレンダーメニューで日付を選択した場合、タブのフォーカスは適切な順序に移動しません。

* サイトページの編集時に使用できるリンクまたはテキストオプションを削除した後で、キーボードユーザーの次または前のオプションにタブフォーカスが移動することはありません。(CQ-4293597)

* キーボードユーザーは、使用可能なオプションを表示して`Esc`キーを押した後、[!UICONTROL アクション]セクションの「詳細」オプションにタブフォーカスを戻すことができません。(CQ-4293592)

* [!UICONTROL 編集]モードで画像の[!UICONTROL 回転]オプションを有効にすると、タブフォーカスが、回転のままではなく、キーボードユーザーの[!UICONTROL やり直し]オプションに移動します(CQ-4293587)。

* 「[!UICONTROL リンクとアクション]」タブにある「[!UICONTROL 選択範囲を開く]」ダイアログで、「[!UICONTROL キャンセル]」オプション(CQ-4293579)の後に、タブフォーカスがページ内の非表示の要素に移動します。

* キーボードユーザーが画像を編集する際に、「[!UICONTROL 完了]」オプションに移動し、Enterキーを押しても、スクリーンリーダーは完了を読み上げません(CQ-4282351)。

* [!UICONTROL リンクとアクション]ダイアログで使用できる「上へ移動」および「下へ移動」オプションは、スクリーンリーダーおよびキーボードユーザーは使用できません(CQ-4281120)。

* [!UICONTROL プロパティ]ページ(CQ-4293581、NPR-34653)の「閉じる」(X)オプションに移動すると、キーボードユーザーはタブフォーカスを復元できません。

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0では、次の問題が [!DNL Assets] 修正され、次の機能強化が行われました。

* このリリースでは、[!DNL Experience Manager Assets]のアクセシビリティに関する次の機能強化が行われました。 詳しくは、 [!DNL Assets]](/help/assets/accessibility.md)の[アクセシビリティ機能を参照してください。

   * キーボードを使用してタイムラインを移動する場合、`Esc`キーは、フォーカスを失うことなく、[!UICONTROL すべてを表示]オプションを折りたたむことがあります。(CQ-4293598)
   * キーボードのTabキーを使用して移動する場合、追加したタグから最後のタグを削除した後も、タグフィールドはフォーカスを保持します(NPR-35109)。
   * [!DNL Experience Manager] コンポーネントに、スクリーンリーダーが使用する名前、役割、値に関する適切な情報が含まれるようになりました(NPR-34255)。
   * 「種類/サイズ」コンボボックス、「リンク」コンボボックス、「言語」コンボボックス、または「テキスト」編集ボックスを削除すると、キーボードフォーカスは次または前のユーザーインターフェイス要素、またはより関連性の高いユーザーインターフェイス要素(CQ-4293585)に戻ります。
   * オプションの上にポインターを置くと、選択やダウンロードなどのヒントが表示されます。 画面の虫めがねを使用している場合、これらのヒントが原因でファイルのサムネールが表示されないことがあります。 `Escape`キーを使用してオプションを削除した後に、フォーカスを保持できるようになりました。 (CQ-4293554).
   * ページ内にあるグリッドからグリッドセルを選択すると、フォーカスが画面に表示されるアクションバーに移動します(CQ-4282127)。
   * [!DNL Experience Manager]ホームページ(CQ-4282072)内のすべてのソリューションへのリンクに視覚的な手がかり（下線と山形のアイコン）が表示されるので、通常のテキストとリンクを視覚的に区別できます。

* [!DNL Assets]では、次のようなユーザーエクスペリエンスの拡張が行われました。

   * カードの表示と列の表示(NPR-35097)でアセットの並べ替えを有効にします。

* 6.5にアップグレードした後、Assets HTTP APIを使用してJSONファイルが生成される場合、ファイルで使用されているエンコーディングに問題があります(NPR-35129)。

* コレクションを作成する権限が与えられていないグループのユーザー（「コレクションを作成」オプションは使用できません）は、引き続きURL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections`(NPR-35115)に直接アクセスしてコレクションを作成できます。

* 名前順に並べ替えると、検索されたアセットは大文字と小文字が区別されます。 これにより、検索結果で順番に表示される大文字と小文字の違いに基づいて、2つの異なる並べ替えリストが作成されます(NPR-35068)。

* コンテンツフラグメントをエディターで開くと、警告メッセージ(`Invalid value specified for a metadata property`)がエラーログに記録されます(NPR-35012)。

* 管理者権限を持たないユーザーは、[Experience Manager]デスクトップアプリを使用して、期限切れのアセットを編集できます。 (NPR-34993).

* 同じAssetをAssetsユーザインターフェイスにドラッグして新しいバージョンを作成した場合、メタデータの変更は永続的ではありません(NPR-34940)。

* コレクションを編集する際、ユーザーはコレクションのタイトルを削除して、変更を正常に保存できます(NPR-34889)。

* 重複画像をアップロードする際に、削除オプションが表示されます。 「削除」を選択すると、画像がアップロードされます。 DAM Update Assetワークフローもトリガーされます(NPR-34744)。

* [!DNL Adobe Asset Link]を[!DNL Adobe InDesign]と共に使用する場合、検索結果にはフォルダーやコレクションは含まれず、アセットのみが含まれます(NPR-34699、CQ-430366)。

* カードの表示にカーソルを重ねると、カード内のクイックアクションに（自動的に）フォーカスした結果として、画面がスクロールされます(NPR-34514)。

* 複数のアセットのプロパティを一括編集する場合、「[!UICONTROL 保存]」オプションを選択すると、バルクエディターの表示が閉じ、メインの[!DNL Assets]ページにリダイレクトされます。 この動作は、[!UICONTROL 「保存して閉じる」]オプションの動作と同じで、予期されない動作です(NPR-34546)。

* スマートコレクションの保存後に、正しいユーザーインターフェイス設定が表示されません。 クエリは正しく保存されますが、インターフェイスには常に最後に追加されたOption predicate(NPR-34539)が表示されます。

* [!DNL Experience Manager]にアセットを追加する場合、名前空間のないメタデータは読み込まれません(NPR-34530)。

* フォルダー上のアセットをドラッグして移動すると、ユーザーインターフェイスには、「[!UICONTROL ライトボックスにドロップ]」および「[!UICONTROL コレクションにドロップ]」のオプションも表示されます。 移動操作がキャンセルされた場合でも、ユーザインターフェイスは後者の2つのオプション(NPR-34526)を引き続き表示する。

* `%>`という記号は、コレクションページ(NPR-34499)に表示される。

* 列表示では、[!DNL Assets]は、上下にスクロールするとすべてのアセットが表示される前に、重複フォルダーとアセット名を表示します(NPR-34464)。

* パブリックフォルダーを作成した直後にプライベートフォルダーを作成した場合、パブリックフォルダーはプライベートフォルダー設定(NPR-34415)を使用します。

* カード表示では、カードはアルファベット順に表示されず、カードをアルファベット順に並べ替えることはできません(NPR-34234)。

* カスケード・ルールを再度開いても、ユーザー・インターフェイスでの選択は維持されません(CQ-4301452)。

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* [!DNL Dynamic Media]のアクセシビリティに関する次の機能強化が行われました(CQ-4290306)。 詳しくは、 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md)の[アクセシビリティ機能を参照してください。

   * スクリーンリーダー（JAWS、ナレーター）は、埋め込みサイズメニューオプションのメニュー項目の名前、役割、状態をナレーションします(CQ-4290927)。
   * ユーザーは、`Tab`キー(CQ-4290926)を使用して電子メールリンクダイアログ内を移動できます。
   * スクリーンリーダーの機能強化(CQ-4290623、CQ-4290622)を考えると、ビデオエンコーディングプロファイルを作成する場合のワークフローはより使いやすくなります。
   * `Tab`キーを使用してナビゲーションする場合、フォーカスはワークフロー内の適切なユーザーインターフェイス要素に移動し、インタラクティブビデオを作成します(CQ-4290621、CQ-4290620、CQ-4290619)。
   * 発行ページ、アセットを編集ページ、スマートトリミングを編集ページ、および画像セットエディタページが、Web標準に準拠するように改善されました。 支援テクノロジー(AT)を使用して、これらのページ内を簡単に移動し、画像の切り抜きなどの操作を行うことができるようになりました。(CQ-4290617、CQ-4290616、CQ-4290613、CQ-4290612)、CQ-4290610、CQ-4290614)
   * ビューアが改善され、ユーザーがキーボードを使用してナビゲートできるようになりました。(CQ-4290615)
   * キーボードおよびスクリーンリーダーのユーザーは切り抜き機能(CQ-4290609)を使用できます。
   * キーボードユーザーは、ホットスポットをより適切に管理できます(CQ-4290604、CQ-4290603)。

* 会社ー名とフォルダー名が同じ場合(NPR-31340)、リモートイメージセットは[!DNL Experience Manager]で編集できません。

* ホットスポットを[!DNL Dynamic Media]画像に追加した後、または[!DNL Dynamic Media]ビデオまたは[!DNL Experience Fragment]をプレビュー付きで編集した後に出力を編集しようとすると、z-indexの順序が正しくなくなります(CQ-4307267)。

* [!DNL Dynamic Media] 混在メディアセットが再処理されると、同期に失敗します。(CQ-4307184)

* [!DNL Dynamic Media]への自動同期が設定されているフォルダーにアセットが移動された場合、アセットは同期されません(CQ-4307122)。

* [!DNL Dynamic Media] ネイティブのHTML5ビデオコントロール(CQ-4306977、CQ-4306727)を使用してiOSデバイスでビデオが再生されない。

* SmartCropが適用されている画像をダウンロードできません。(CQ-4304558)

* フォルダーを選択してDynamic Mediaに発行することはできません(CQ-4304526)。

* [!DNL Experience Manager]からビデオファイルを非公開にしても、設定済みのScene7導入環境からアダプティブビデオセットの公開は取り消されません(CQ-4304405)。

* パノラマ画像アセットをパノラマメディアコンポーネントに追加し、ページを更新すると`Uncaught ReferenceError: $ is not defined`エラーが発生します(CQ-4302810)。

* [!UICONTROL ビューアプリセットエディター]で、[!UICONTROL PanoramicImage/PanoramicImage_VR]プリセットを編集する場合、`PanoramicView`コンポーネントで`PANORAMICVIEW_AUTOROTATE`修飾子のラベルを使用できません(CQ-4302443)。

* ビデオがMixedMediaSet内の最初でない場合、ビデオキャプションは表示されません。(CQ-4298161)

* iPhone携帯端末上のHTML5 eCatalogビューアで、ページをめくったり、ページをめくったりすることはできません。(CQ-4296611)

* モバイルデバイスでスウォッチをスクロールすると、表示に戻るまで数秒間、スウォッチが表示領域の右と外にスクロールします(CQ-4296439)。

* ビューアプリセットのマスターレコードを作成すると、CSSとアートワークは公開されず、ビューアプリセットのみが公開されます(CQ-4262205)。

* [!UICONTROL インタラクティブビデオ/画像]コンポーネント内の特定のホットスポットに対してエクスペリエンスフラグメントをリンクしようとしても、選択したエクスペリエンスフラグメントのパスは表示されません。 代わりに、パスフィールド(NPR-35146、CQ-4298136)から空の値が返されます。

* IVVエディター(CQ-4308560)でエクスペリエンスフラグメントをプレビューできません。

* 画像にホットスポットを追加してエクスペリエンスフラグメントを選択する場合、サブフォルダーとエクスペリエンスフラグメントのバリエーションを選択できません(CQ-4307455)。

* 画像以外のアセットは、アップロード後に公開済みとして表示されません(CQ-4306415)。

#### [!DNL Experience Manager] 3Dアセット  {#three-d-assets-6570}

* `DAM CQ MIME Type` サービスは、3Dアセットに誤ったMIMEタイプを適用し、誤ったレンダリングが行われます(NPR-34731)。

### [!DNL Commerce] {#commerce-6570}

* Commerce製品収集ユーザーインターフェイスでは、1つのコレクション(NPR-34502)内の15個を超える製品はリストされません。

### プラットフォーム {#platform-6570}

* HTTPSを使用したHTTPセッションは無効にされません(NPR-35083)。
* ユーザーインターフェイス(NPR-34953)から日次または週次のメンテナンスタスクを開始する際に`NullPointerException`が返されます。
* W3Cバリデーターは、準拠しているクライアントライブラリのJavaScriptファイルに関する警告をレポートします(NPR-34898)。
* `AudienceOmniSearchHandler`関数は、非推奨のインデックスを使用します(NPR-34870)。
* Experience Managerからサインアウトしても、cookieはクリアされません(NPR-34743)。
* `TagManager` APIの`findByTitle`関数は、タグ名に特殊文字(NPR-34357)が含まれている場合は機能しません。
* ユーザー同期パッケージを読み込むプロセスが失敗する(NPR-34399)。
* `ariaLabel`および`ariaLabelledby`プロパティのサポートを`Coral.Masonry`コンポーネント(GRANITE-29962)に追加しました。
* 最新のコアコンポーネントパッケージをインストールした後、コンテンツフラグメントを含むページに対してディスパッチャーキャッシュが更新されない(CQ-4306788)。
* ローカライズされたタグ名が引用符(`"`)で囲まれていると、ユーザーインターフェイスに正しく表示されません(CQ-4305439)。

### ユーザーインターフェイス {#ui-6570}

* コンポーネントプロパティの[!UICONTROL 「]へのリンク」フィールドに、指定した文字列と一致しないオートコンプリートの提案が表示されます(NPR-34865)。

* 2日間(NPR-35280)の間に毎日のメンテナンスウィンドウを配信するようにスケジュールすると、AEMで次のエラーメッセージが表示されます。

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### 統合 {#integrations-6570}

* 既存の[!DNL Adobe Launch]設定の編集に失敗します(NPR-35045)。
* IMS設定と[!DNL Adobe Target Standard]環境(NPR-34555)を使用している場合、[!DNL Experience Fragments]を[!DNL Adobe Target]に書き出すことはできません。
* 「[!UICONTROL 作成]」オプションは、オーディエンスーから[!UICONTROL オーディエンスー]ページ(NPR-35151)に移動すると、[!UICONTROL フォルダー]ページに表示されます。

### Sling {#sling-6570}

* デフォルトのログイン正常性チェックは、存在しないユーザーの資格情報を検証します(NPR-34686)。

### 翻訳プロジェクト {#translation-6570}

* [!DNL Experience Manager]で翻訳プロジェクトをキャンセルする場合、キャンセル要求は翻訳プロバイダ(NPR-34433)に送られない。

### [!DNL Communities] {#communities-6570}

* 製品内の不公平な用語の例はすべて、受け入れられた等価語(NPR-34311)に置き換えられる。
* [!DNL Google+] は、ソーシャルシェアオプションのリスト(NPR-33877)から削除されました。

### [!DNL Brand Portal] {#brandportal-6570}

* ユーザインターフェイスは、[!UICONTROL リスト表示](NPR-34728)内のアセットの選択に応答しません。

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 予定されている [!DNL Experience Manager] Service Packのリリース日の1週間後に、アドオンパッケージをリリースします。

>[!NOTE]
>
>[!DNL Experience Manager] Service Packにはの修正が含まれていません [!DNL Forms]。これらは、別の[!DNL Forms]アドオンパッケージを使用して配信されます。 さらに、JEE上の[!DNL Experience Manager Forms]の修正を含む累積インストーラーがリリースされました。 詳しくは、「[AEM Formsアドオンのインストール](#install-aem-forms-add-on-package)」および「[JEE上のAEM Formsのインストール](#install-aem-forms-jee-installer)」を参照してください。

**アダプティブフォーム**

* [!DNL Experience Manager] Service Pack 6(NPR-35126)を適用した後、Classic UIを使用してアダプティブフォームを編集できない。

* PDFをアダプティブフォームに変換する場合、タブ付きレイアウトのフォームデータモデルを使用してネストされたパネルに値を設定することはできません。 さらに、コードエディター(NPR-35062)を使用して静的な配列でラジオボタングループの値を動的に設定する場合に問題が発生します。

* アダプティブフォームのテキストフィールドコンポーネントに日本語の文字を入力する場合、最大35文字(NPR-35039)を超える文字を指定できます。

* アダプティブフォームは、フォームの送信後に表示される&#x200B;**[!UICONTROL 「ありがとうございます」]**&#x200B;ページ(NPR-34989)に、`owner`や`status`などの不要なパラメーターを表示します。

* [!UICONTROL 添付ファイル]コンポーネントの[!UICONTROL File Selection]ダイアログには、選択に対してもサポートされていないファイルタイプも表示され、アダプティブフォームの送信中にエラーが発生します(NPR-34970)。

* フォームの前にテキストを含む[!DNL Experience Manager Sites]ページにアダプティブフォームを挿入すると、カーソルのフォーカスは、フォームの前のテキストではなく、直接フォームに移動します(NPR-34947)。

* [!UICONTROL 「] Data」オプションを使用して、 [!DNL Experience Manager] 6.2データのXMLファイルを使用してアダプティブフォームに事前入力するプレビューが適切に機能しない(NPR-35087)。

* アダプティブフォームのデータディクショナリを更新すると、アダプティブフォームがキャッシュされた値を返すので、フォームは変換されません(NPR-34845)。

* キャッシュの無効化(NPR-34567)が原因で、フラグメントのアダプティブフォームへの読み込みに時間がかかります。

* アダプティブフォームのスクリーンリーダーでタブナビゲーションが適切に機能しない(NPR-34544)。

**Correspondence Management**

* フロートタイプを含む数値データを含むXMLタグの値をドラフト(NPR-35050)として保存できません。

* ES3からアセットを移行する場合、アセットには編集不可の2つのデフォルト条件(NPR-34972)が含まれます。

* レター内のデータディクショナリを編集すると、「[!UICONTROL 貸したコンテンツ]」セクションには、有用な情報ではなく、回転する長方形が表示されます(NPR-34853)。

**インタラクティブコミュニケーション**

* [!DNL Forms]アドオンパッケージのインストール後に使用できるInteractive Communicationのロールアウト設定名。標準のロールアウト設定名(NPR-34976)を重複します。

**Document Security**

* 新しいドキュメントセキュリティポリシーを保存すると、Experience ManagerFormsは`Relative validity period is required`エラーメッセージを表示します(NPR-34679)。

* ドキュメントセキュリティでPDF 2.0ドキュメントを保護できません(CQ-4305851)。

セキュリティ更新について詳しくは、[Experience Managerのセキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)を参照してください。

## 6.5.7.0 {#install}のインストール

**設定要件と詳細情報**

* AEM 6.5.7.0ではAEM 6.5が必要です。詳細な手順については、[アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。
* Service Packのダウンロードは、Adobe[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)で入手できます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.5.7.0 をインストールしてください。

>[!NOTE]
>
>[!DNL Adobe Experience Manager] 6.5.7.0パッケージの削除またはアンインストールは、Adobeにお勧めしません。

### サービスパックのインストール {#install-service-pack}

既存のAdobe Experience Manager6.5インスタンスにService Packをインストールするには、次の手順を実行します。

1. インスタンスが更新モードの場合（これは、インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 Adobeでは、インスタンスの現在の稼働時間が長い場合は再起動を推奨します。

1. インストールする前に、[Experience Manager]インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.7.zip)からService Packをダウンロードします。

1. パッケージマネージャーを開き、「**[!UICONTROL パッケージをアップロード]**」をクリックして、パッケージをアップロードします。 詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

1. S3コネクタを更新するには、Service Packのインストール後にインスタンスを停止し、既存のコネクタをinstallフォルダーに指定された新しいバイナリファイルに置き換えてから、インスタンスを再起動します。 [AmazonS3データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>Service Packのインストール中に、Package Manager UIのダイアログが閉じることがあります。 Adobeでは、エラーログが安定するのを待ってからデプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 通常、これは[!DNL Safari]で起こりますが、どのブラウザーでも断続的に起こる可能性があります。

**自動インストール**

作業インスタンスにAdobe Experience Manager6.5.7.0を自動的にインストールするには、次の2つの方法があります。

A.サーバーがオンラインで使用できる状態で、パッケージを`../crx-quickstart/install`フォルダーに配置します。 パッケージが自動的にインストールされます。

B. Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)の[HTTP APIを使用します。 `cmd=install&recursive=true`を使用して、ネストされたパッケージをインストールします。

>[!NOTE]
>
>Adobe Experience Manager6.5.7.0は、Bootstrapのインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ(`/system/console/productinfo`)には、[!UICONTROL インストール済み製品]の下に、更新バージョン文字列`Adobe Experience Manager (6.5.7.0)`が表示されます。

1. すべてのOSGiバンドルは、OSGiコンソールで&#x200B;**[!UICONTROL ACTIVE]**&#x200B;または&#x200B;**[!UICONTROL FRAGMENT]**&#x200B;です(Webコンソールを使用：`/system/console/bundles`)。

1. OSGiバンドル`org.apache.jackrabbit.oak-core`はバージョン1.22.3以降です(Webコンソールを使用：`/system/console/bundles`)。

このリリースで動作が確認されたプラットフォームについて詳しくは、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

### Adobe Experience Manager Formsアドオンパッケージ{#install-aem-forms-add-on-package}をインストール

>[!NOTE]
>
>[!DNL Experience Manager Forms] 予定されている [!DNL Experience Manager] Service Packのリリース日の1週間後に、アドオンパッケージをリリースします。

>[!NOTE]
>
>AEM Forms を使用していない場合はスキップしてください。Adobe Experience Manager Formsの修正は、別のアドオンパッケージを通じて提供されています。

1. Adobe Experience ManagerService Packがインストールされていることを確認します。
1. [AEM Formsリリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)に記載されている、お使いのオペレーティングシステム用の対応するFormsアドオンパッケージをダウンロードしてください。
1. [AEM Formsアドオンパッケージのインストール](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)の説明に従って、Formsアドオンパッケージをインストールします。

### JEEにAdobe Experience Manager Formsをインストール{#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE上のAdobe Experience Manager Formsの修正は、別のインストーラーを使用して提供されています。

JEE上のExperience ManagerFormsの累積インストーラーのインストールとデプロイメント完了後の設定について詳しくは、[リリースノート](jee-patch-installer-65.md)を参照してください。

### UberJar {#uber-jar}

Experience Manager6.5.7.0のUberJarは、[Maven Centralリポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.7/)で入手できます。

MavenプロジェクトでUberJarを使用するには、[UberJarの使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクトPOMに次の依存関係を含めます。

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
>UberJarおよびその他の関連アーティファクトは、AdobeのパブリックMavenリポジトリ(`repo.adobe.com`)ではなく、Maven Centralリポジトリで使用できます。 メインのUberJarファイルの名前が`uber-jar-<version>.jar`に変更されます。 したがって、`dependency`タグには`apis`を値として持つ`classifier`はありません。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

以下は、[!DNL Experience Manager] 6.5.7.0で非推奨とマークされた機能と機能のリストです。機能は、最初は非推奨とされ、今後のリリースで削除されます。 通常は、代替オプションが提供されます。

機能または機能を配置で使用するかどうかを確認します。 また、別のオプションを使用するように実装を変更することを計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | **[!UICONTROL AEMクラウドサービスのオプトイン]**&#x200B;画面は非推奨です。 AEM 6.5で更新されたAEMとターゲットの統合により、AdobeIMSとI/Oを介した認証を使用するTarget Standard APIがサポートされ、AEMページの解析とパーソナライゼーションの実装でAdobe開始の役割が増加しているため、オプトインウィザードは機能的に無関係になりました。 | 各AEMクラウドサービスを使用して、システム接続、AdobeIMS認証、Adobe I/O統合を設定します。 |
| コネクタ | AEM 6.5では、JCR Connector for Microsoft SharePoint 2010およびMicrosoft SharePoint 2013のAdobeが非推奨です。 | 該当なし |

## 既知の問題 {#known-issues}

* Experience Manager6.5.7.0のインストール時に、`error.log`ファイル内の次のエラーを無視します。

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

* [!DNL Experience Manager]インスタンスを6.5から6.5.7.0バージョンにアップグレードする場合は、`RRD4JReporter`例外を`error.log`ファイルで表示できます。 インスタンスを再起動して問題を解決します。

* [!DNL Experience Manager] 6.5 Service Pack 5または以前のService Packを[!DNL Experience Manager] 6.5にインストールした場合、（`/var/workflow/models/dam`で作成した）アセットカスタムワークフローモデルのランタイムコピーが削除されます。
ランタイムコピーを取得する場合、Adobeでは、HTTP APIを使用して、カスタムワークフローモデルのデザイン時コピーをそのランタイムコピーと同期することを推奨します。
   `<designModelPath>/jcr:content.generate.json`

* [!UICONTROL AdobeメタデータスキーマFormsエディタ]および[!UICONTROL メタデータスキーマFormsエディタ]で、[!UICONTROL ルール]を定義ダイアログを使用してカスケードルールを編集および作成する際に問題が発生した場合は、カスタマーケアにお問い合わせください。 既に作成および保存されているルールは、期待どおりに動作しています。

* 階層内のフォルダーの名前が[!DNL Experience Manager Assets]に変更され、アセットを含むネストされたフォルダーが[!DNL Brand Portal]に発行された場合、ルートフォルダーが再度発行されるまで、フォルダーのタイトルは[!DNL Brand Portal]に更新されません。

* ユーザーがアダプティブフォームで初めてフィールドを設定することを選択した場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドの設定を選択すると、問題が解決します。

* [!UICONTROL 接続されたアセットの構成]ウィザードがインストール後に404エラーメッセージを返す場合は、Package Managerを使用して`cq-remotedam-client-ui-content`および`cq-remotedam-client-ui-components`パッケージを手動で再インストールします。

* AEM 6.5.x.xのインストール中に、次のエラーおよび警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して AEM に Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計機能が使用されると、アダプティブフォームのサーバー側検証に失敗します。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * 買い物かご可能なバナービューアでアセットをプレビューすると、Dynamic Mediaのインタラクティブ画像のホットスポットが表示されません。

## OSGiバンドルとコンテンツパッケージ（{#osgi-bundles-and-content-packages-included}に含まれています）

AEM 6.5.7.0に含まれるOSGiバンドルとコンテンツパッケージに関する次のテキストドキュメントリストです。

* [AEM 6.5.7.0 に含まれている OSGi バンドルの一覧](assets/6570_bundles.txt)

* [AEM 6.5.7.0 に含まれているコンテンツパッケージの一覧](assets/6570_packages.txt)

## 制限付きWebサイト{#restricted-sites}

これらのWebサイトは、お客様のみ利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [カスタマーサポートへの問い合わせ方法](https://experienceleague.adobe.com/docs/customer-one/using/home.html)を参照してください。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5リリースノート](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 製品ページ](https://www.adobe.com/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [Adobe優先度の製品アップデート](https://www.adobe.com/subscription/priority-product-update.html)のサブスクライブ

