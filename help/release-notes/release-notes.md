---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 29fa88495225f1314acea2a954737f00d98df468
workflow-type: tm+mt
source-wordcount: '4442'
ht-degree: 36%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section. -->

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.23.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2025年5月22日木曜日（PT）<!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.23.0 の内容 {#what-is-included-in-aem-6523}

[!DNL Experience Manager] 6.5.23.0 には、新機能、お客様からリクエストされた主な機能強化、バグ修正が含まれています。また、2019年4月の 6.5 の公開当初以降にリリースされたパフォーマンス、安定性、セキュリティの改善も含まれています。 [このサービスパックを [!DNL Experience Manager] 6.5 にインストールします](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

<!--
## Key features and enhancements

### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

<!--
### Forms {#forms-sp23}

Key features and enhancements in this release include the following:

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## サービスパック 23 で修正された問題 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### アクセシビリティ {#sites-accessibility-6523}

* AEM エディターページのキャンバスセクションで、完全なキーボードアクセシビリティがサポートされるようになりました。 ユーザーは、マウスのカーソルを合わせなくても、キーボードのみを使用して、セクションタイトルをアクティブ化し、ボタンを編集できます。 この更新により、WCAG 2.1.1 への準拠が保証され、ティーザー、画像、カルーセル、レイアウト、タイムワープ、注釈モーダルなど様々なコンポーネントでの操作性が向上しました。 （SITES-25256） <!-- 6.5 LTS SP1 -->
* AEM ページエディターでペルソナ、買い物かご、放棄などのボタンをアクティブ化した後、キーボードフォーカスがデモグラフィックツールバーの開始に予期せずリセットされる、アクセシビリティの問題を修正しました。 アクティブ化されたボタンにフォーカスが残り、一貫したキーボードナビゲーションとスクリーンリーダーのワークフローをサポートするようになりました。 （SITES-25306）
* AEM ページエディターで、複数のダイアログボックスおよびモデル（アセットパネルやレイアウトプレビューなど）のキャンバス要素をキーボードだけで操作できない、アクセシビリティに関する重大な問題を修正しました。 すべてのインタラクティブキャンバス要素で、キーボードのみのナビゲーションがサポートされるようになり、WCAG 2.1 達成基準 2.1.1 に準拠できるようになりました（SITE-25256）
* Sites 管理 UI で、作成ポップアップのインタラクティブリスト項目で誤った ARIA の役割が使用されるアクセシビリティの問題を修正しました。 リンクのように動作する要素は `role="menuitem"` ではなく `role="listitem"` 割り当てられ、ARIA のデザインパターンに違反し、スクリーンリーダーを混乱させました。 更新により、すべてのリストコンポーネントが適切なセマンティックの役割に従い、キーボードと支援テクノロジーのサポートが向上します。 （SITES-24493）
* ページタイトルおよびタグフィールドのアクセシビリティラベルの関連付けの問題を修正しました。 JAWS などのスクリーンリーダーを使用する場合、AEM インターフェイスは、アクセシビリティラベルを「タイトル」フィールドと「ページタイトル」フィールドに正しく関連付けるようになりました。 この修正により、ラベルの適切な読み取りが保証され、ページの作成、プロパティ、移動ワークフロー全体で ADA コンプライアンスが向上します。 （SITES-27149）
* 権限ダイアログボックスでのテーブル識別に関するアクセシビリティの問題を修正しました。 AEMの権限テーブルで正しい ARIA ロールと属性が使用されるようになり、JAWS などのスクリーンリーダーがテーブルとして適切に識別するようになりました。 この修正により、アクセシビリティコンプライアンスが向上し、ユーザーが正確なナビゲーションやコンテンツのお知らせを受け取れるようになります。 （SITES-27140）
* タイムラインのコメント入力フィールドの欠落した表示ラベルを修正しました。 アクセシビリティを向上させるために、「タイムライン」セクションの「コメント」入力フィールドの欠落したビジュアルラベルを修正しました。 これにより、スクリーンリーダーがフィールドラベルを正確に読み上げることができるようになります。 このエクスペリエンスにより、すべてのユーザー、特に支援テクノロジーに依存するユーザーのフォームのナビゲーションと送信が強化されます。 （SITES-26903）
* タイムラインコメントの省略記号ボタンのキーボードアクセシビリティを修正しました。 「タイムライン」セクションで、コメントの横にある省略記号（3 つのドット）ボタンのキーボードナビゲーションを有効にしました。 ユーザーは Tab キーを使用してボタンにアクセスし、操作できるようになりました。これにより、キーボードのみのナビゲーションに依存するユーザーのアクセシビリティが向上します。 （SITES-26891）
* 選択ダイアログボックスでの検索結果に対する NVDA/ナレーターのお知らせを改善しました。 NVDA やナレーターなどのスクリーンリーダーを使用する際に、検索結果が見つかったかどうかを通知するように、「選択を開く」ダイアログボックスを更新しました。 この改善により、支援テクノロジーに依存しているユーザーは、視覚的な確認を必要とせずに検索アクションの結果を理解できます。 （SITES-26883）
* コメント入力フィールドの横にある省略記号アイコンの ARIA 役割を修正しました。 コメント入力フィールドの横にある省略記号（3 つのドット）アイコンを更新して、正しい ARIA の役割を使用するようにし、スクリーンリーダーが要素を正確に識別できるようにします。 この改善により、アクセシビリティコンプライアンスが強化され、支援テクノロジーに依存するユーザーのエクスペリエンスが向上します。 （SITES-26881）
* Coral UI コンポーネントの無効な ARIA 属性を修正しました。 すべての ARIA 属性が有効な値を使用するように Coral UI コンポーネントを更新し、アクセシビリティコンプライアンスを向上しました。 特に、`aria-modal="dialog"` のような無効な値が誤って割り当てられているケースに対処しました。 この機能強化により、スクリーンリーダーでダイアログボックス要素が正しく解釈されるようになり、支援テクノロジーに依存するユーザーのアクセシビリティが向上します。 （SITES-26873）
* リフローシナリオでのアイコンの表示とツールチップを改善しました。 リフロー動作が強化され、**ダウンロード**、**アセットを再処理**、および **チェックアウト** アイコンのツールチップが正しく表示されるようになりました。 ビューポートのサイズ変更やブラウザーのズーム設定の変更時にアイコンとそのラベルが非表示になるアクセシビリティの問題に焦点を当てました。 この修正により、可視性を維持し、リフロー中に適切なアイコンの説明を提供することで、視力の低いユーザーがサポートされます。 （SITES-26871）

#### 管理者ユーザーインターフェイス{#sites-adminui-6523}

Externalizer エンドポイントがない、ユニバーサルエディター URL サービスの例外を修正しました。 ユニバーサルエディターの URL サービスで、例外をスローせずに、オーサー、パブリッシュまたはローカルの Externalizer エンドポイントの欠落を処理できるようになりました。 管理者ユーザーは、一部の Externalizer 設定が不完全な場合でも、ページエディターを正常に開くことができます。 （SITES-28877） <!-- LTS -->

#### クラシック UI{#sites-classicui-6523}

* クラシック UI のダイアログボックスで、ボタンを切り替えるとテキスト領域が非表示になり、その後のクリックで再度表示できなくなる問題。 この修正により、切り替え時にテキスト領域が適切に再表示され、期待される動作が復元され、動的ダイアログボックスのワークフローが中断されるのを防ぐことができます。 （SITES-30230）
* Service Pack 22 へのアップグレード後に、クラシック UI の画像アセットファインダー機能が壊れる問題を修正しました。 クラシック UI 画像アセットファインダーで、スペースや特殊文字を含むアセット名が適切に処理されるようになりました。 このアップデートにより、アセットファインダーでファイル名が正しくエンコードされ、検索の失敗が防がれ、作成者がエラーなしで画像アセットを見つけて選択できるようになります。 （SITES-29151）

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* `DeleteVariationIT.testUpdateBasic` の検証テストエラーを修正しました。 サービスパックの検証の実行中に `DeleteVariationIT.testUpdateBasic` テストが失敗しなくなりました。 この修正により、JSON 処理ロジックで欠落しているテキストマッピングの問題が修正され、テストの安定性が確保され、不要なテストの中断が回避されます。 （SITES-28022）
* AEMは、画像アセットのXMP メタデータの形式が正しくないことに起因するパフォーマンスの低下を防ぐことができるようになりました。 数値セグメントや不適格な構造など、無効または準拠していないXMP プロパティ名を含むAssetsで、処理中に繰り返し警告ログがトリガーされなくなりました。 システムは、問題のあるメタデータを除外して、アセットの取り込みと検証がエラーなく完了するようにします。 （SITES-30683） <!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] - フラグメントエディター{#sites-fragments-editor-6523}

他の作成者がチェックアウトした場合でも、他の作成者がコンテンツフラグメントを公開できます。これは、チェックアウト機能の意図した動作と反します。 この修正により、コンテンツフラグメントがチェックアウトされた際に、他のユーザーがオーサリングインターフェイスの「公開」ボタンを表示または使用できなくなります。 （SITES-30578） <!-- LTS -->

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6523}

コンテンツフラグメントスキーマでのGraphQL QueryValidationError を修正しました。 `cq-dam-cfm-graphql` バンドルを更新すると、コンテンツフラグメント参照を使用する際にスキーマ検証エラーが修正されます。 この修正により、パッケージのデプロイメント後に、手動でスキーマの再整列や再公開を行わなくても、GraphQL クエリが正しく機能するようになります。 （SITES-27001） <!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### コンポーネントコンソール{#sites-component-console-6523}

「コンポーネントライブ使用状況」ページの読み込みを改善しました。 AEMの「コンポーネントライブ使用状況」ページを最適化して、大きなデータセットをスクロールしたときに空の行が表示されないようにします。 広範な使用参照を持つコンポーネントを読み込むユーザーが、不要なギャップや空のエントリがない状態で継続的なデータ読み込みを経験できるようになりました。 このエクスペリエンスにより、コンポーネント使用状況レポート全体でページナビゲーション、トラッキングの精度、管理効率が向上します。 （SITES-26454）

#### コアバックエンド{#sites-core-backend-6523}

* 無効なアセット名が原因で発生した、固定コンテンツファインダーアセットのリスト表示の失敗。 コンテンツファインダーで、エンコードできない文字を含むアセット名が正しく処理されるようになりました。 ページエディターでのアセットのリストで、問題のある名前のアセットが検出された場合に、失敗したり例外がスローされなくなりました。 （SITES-28722）
* `SearchPathLimiter` コンポーネントが、呼び出しごとにエラーレベルでメッセージを印刷することで、過剰なログエントリを生成していた問題。 この動作は Service Pack 17 以降に開始され、非常に多くのログ量が原因でパフォーマンスに関する問題が発生しました。 この修正により、ログレベルが DEBUG にダウングレードされ、ログノイズが大幅に減少し、システムの監視と診断効率が向上します。 （SITES-29835）
* XMP メタデータの形式が正しくない場合、`ValidationDataServlet` ージ内の画像アセットの処理中にエラーが発生しました。 この修正により、準拠したメタデータ処理が保証され、無効なプロパティの冗長な解析が回避されます。 （SITE-30683） <!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### ローンチ{#sites-launches-6523}

* 12 月 25 日（PT）から 12 月 31 日（PT）の間に間違った開始日の表示が修正されました。 ローンチ UI に、12 月 25 日（PT）から 12 月 31 日（PT）までの日付と正しい年が表示されるようになりました。 この修正により、日付が翌年と誤って表示されなくなり、キャンペーンの計画およびスケジュール設定時の混乱が回避されます。 （SITES-28706）
* サービスパック 22 のアップグレード後に、AEM Launch のテンプレートが壊れる問題を修正しました。 サービスパック 22 のアップグレード後に、AEM Launch テンプレートが正しく読み込まれるようになりました。 この修正により、内部ローンチ設定の無効なデータが修正され、ユーザーはエラーやフィールドの欠落なしにローンチを表示、編集および作成できるようになります。 （SITES-28504）


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### ページエディター{#sites-pageeditor-6523}

* 低画面の解像度での AssetPicker の読み込みの問題を修正しました。 ユーザーが低い画面の解像度（1728×1117 以下）でスクロールした場合、AssetPicker がアセットを正しく読み込むようになりました。 スクロール中にアセットが見つからなくなり、異なるデバイスのブレークポイントをまたいだアセット管理が向上しました。 （SITES-28065）
* ページのロックおよびロック解除アクションに対するスクリーンリーダーの欠落アナウンスを修正しました。 ユーザーがロック/ロック解除ボタンをアクティブ化すると、ページエディターが「情報：ページがロック/ロック解除されました」というメッセージを正しく読み上げるようになりました。 この修正により、アクセシビリティコンプライアンスが向上し、スクリーンリーダーユーザーがページ編集中に動的更新を確実に受け取れるようになります。 （SITES-27143）
* AEM オーサリングにおけるコンポーネントアクションのキーボードフォーカスの動作を改善しました。 AEM オーサーツールのキーボードナビゲーションが強化され、設定、削除、変換などのアクションの後に、新しく作成または選択したコンポーネントにフォーカスが残るようになりました。 以前は、フォーカスがページの上部に移動し、アクセシビリティコンプライアンスの問題が発生していました。 この更新により、キーボードおよび支援テクノロジーのユーザーのユーザーエクスペリエンスが向上します。 これは、編集ワークフロー内で論理的なフォーカスの進捗を維持することでおこなわれます。 （SITES-26549）
* オーサーダイアログボックスのタブナビゲーションの改善。 「説明」編集ボックスに達した後もタブを前方に移動できるようにすることで、AEMのオーサーダイアログボックスのキーボードナビゲーションを強化します。 以前は、「説明」フィールドにフォーカスをトラップすると、特別なキーの組み合わせを使用せずにそれ以上のナビゲーションがブロックされていました。 この更新により、ユーザーが Tab キーのみを使用してフィールドをシームレスに移動できるようになり、アクセシビリティコンプライアンスとユーザーエクスペリエンスが向上します。 （SITES-26524）
* AEM 6.5 Service Pack 22 で、Launch タイトルにスペースを含めることができないリグレッションが導入されました。 この修正により、スペースを使用する機能が復元され、チームは期待される動作に合わせて、ローンチ名をより柔軟に定義および整理できるようになります。 （SITES-29414）
* 非表示/非表示後のレイアウトコンテナ内のコンポーネントのサイズ変更の問題を修正しました。 レイアウトコンテナを非表示または再表示した後に、ページエディターが列の値を適切に計算するようになりました。 ユーザーはエラーを起こさずにコンポーネントのサイズを変更でき、サイズ変更操作中に列は正しく表示されます。 （SITES-28463）
* ページエディターでのコンテンツツリーボタンの配置の誤りを修正しました。 ページエディターで、「コンテンツツリー」設定ボタンが、誤ったセクションではなく、意図された「ヘッドティーザー」ダイアログボックスの下に正しく配置されるようになりました。 この修正により、コンテンツツリーのダイアログボックスの CSS が更新されて、`bottom:0` ではなく `top:0` が使用されるようになり、ボタンが適切に配置されます。 （SITES-28448）


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### リッチテキストエディター{#sites-rte-6523}

平文の貼り付けモードを使用したリッチテキストエディターで、予期しない `<br>` タグを修正しました。 リッチテキストエディターが、プレーンテキスト `defaultPasteMode` ータを使用する際の切り取りと貼り付けの操作を正しく処理するようになりました。 この修正により、ユーザーが RTE フィールド内でテキストを切り取って貼り付ける際に、予期しない `<br>` タグが挿入されるのを防ぎ、コンテンツ編集中にクリーンな書式が確保されます。 （SITES-27780）

#### ユニバーサルエディター {#sites-universal-editor-6523}

* クエリパラメーターを含んだ複数のリクエストがAEMに送信される場合、login-token cookie が時間内に返されず、ログインに失敗する可能性があります。 （SITES-30659） <!-- LTS -->
* SAML ハンドラーとの互換性とサポートを確保するには、`Query Token Auth` ハンドラーが `SAML Auth` ハンドラーの *前* に実行されるように `service.ranking` プロパティを設定する必要があります。 （SITES-29684）

### [!DNL Assets]{#assets-6523}

* ![Assets](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL [!DNL AEM]Assets ]**を選択し、**[!UICONTROL  Adobe Stockを検索 ]**フォルダーに移動してストック画像を選択した後に、オンプレミス（6.5.22.0）のナビゲーションページで次の問題が発生します。
   * **[!UICONTROL ライセンスと保存]** をクリックすると空のドロップダウンが表示されるので、選択したストック画像にライセンスを取得して保存することができません。
   * ストック画像を選択するか、ストックページの URL を再入力すると、[!DNL AEM] ホームページにリダイレクトされ、Adobe Stock画像にアクセスできなくなります。 （ASSETS-48687）
* フォルダーの名前に、[!DNL AEM] オンプレミス（6.5.22.0）ナビゲーション ページの名前に `/` が含まれる場合、フォルダーの管理中に問題が発生します。 （ASSETS-46740）
* [!DNL AEM] 6.5 では、メモリ使用量が多いため、アセットの詳細ページが ![ コレクション ](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL  コレクション ]**ビューから読み込まれません。 （ASSETS-46738）
* [!DNL InDesign] as `Day CQ DAM Mime Type OSGI` Service の統合の問題によって、[!DNL InDesign] ファイルが `x-indesign` ではなく `x-adobe-indesign` と誤って認識されます。 （ASSETS-45953）
* セッショ [!DNL AEM 6.5.21] リークは、標準の **[!UICONTROL Brand Portalへのスケジュールされた公開]** ワークフローステップまで追跡されました。 （ASSETS-44104）
* **[!UICONTROL メモリ不足（OOM）]** 画像の処理および公開時に、[!DNL AEM] でエラーが表示される。 この問題は、**[!DNL Dam Asset update]** や **[!DNL Dynamic Media: Reprocess assets]** などのワークフローの非推奨メソッドが原因でした。 （ASSETS-43343）
* タイトルの更新などの小さな変更を加えた後、ローカルの Sites インスタンスで **[!DNL Connected Assets configuration]** を再度開いて再保存します。 その後、リモートインスタンスはローカルインスタンスへの接続を失います。 その結果、ローカルの Sites インスタンスとの通信を確立できません。 （ASSETS-44484）
* ま [!DNL AEM 6.5.21]、リスト表示のアセットのアップロードがキャンセルされ、2 回目のアップロードが実行され [!DNL AEM] と、「**[!UICONTROL 0 of NaN assets uploaded]**」というエラーが表示されます。 （ASSETS-44124）

#### [!DNL Dynamic Media]{#assets-dm-6523}

スマート切り抜きの生成に失敗したことを識別するためのメタデータプロパティ（`jcr:content/metadata/dam:scene7SmartCropStatus`）がアセットに追加されました。 手動または自動ワークフローを介して、スマート切り抜きの問題を伴うアセットの効率的な検索、フィルタリングおよび再処理を可能にします。 （ASSETS-46237）

#### [!DNL Dynamic Media] - ハイブリッドモード {#assets-dm-hybrid-6523}

##### Dynamic Media - ハイブリッドアドオンパッケージ（AEM 6.5.23 以降）

AEM 6.5 サービスパック 23 以降、Dynamic Media - ハイブリッドモードで新しいアドオンパッケージが利用可能になりました。このパッケージには、Dynamic Media - ハイブリッド実行モードと特別に互換性のある `cq-scene7-imaging` バンドルが含まれています。

**主な修正点**

Dynamic Media - ハイブリッドデプロイメントで、`/conf/global/settings/dam/dm/imageserver` の下の `catalog.expiration` パラメーターの更新が、レプリケーションはエラーなく成功しているにもかかわらず、サーバーまたはオーサー URL に反映されなかった問題を修正しました。この更新により、CRX/DE、サーバー応答およびパブリック配信 URL の間で、一貫性のある有効期限値が保証されます。これにより、画像変換のキャッシュ動作と信頼性が向上します。（ASSETS-44837）

**重要な検討事項**

* ベース AEM 6.5.23（およびそれ以降）のインストールの `cq-scene7-imaging` バンドルは、Dynamic Media - ハイブリッド実行モードと&#x200B;*互換性がありません*。
* サービスパック 23（以降）のみをインストールしても、Dynamic Media - ハイブリッド（`-r dynamicmedia` 実行モード）用に設定された AEM インスタンス上の既存の `cq-scene7-imaging` バンドルは&#x200B;*自動的に更新されません*。

**ハイブリッドアドオンパッケージをインストールする場合**

* AEM 6.5.19 以前から AEM 6.5.23（以降）に直接アップグレードする場合。
* Dynamic Media - ハイブリッド機能に固有の修正が必要な場合。
* 新しい Dynamic Media - ハイブリッドインスタンスを AEM 6.5 GA（一般提供）からサービスパック 23（以降）に直接デプロイする場合。

**ハイブリッドアドオンパッケージのダウンロード**

ハイブリッドアドオンパッケージは、2025 年 5 月 22 日木曜日（PT）以降、Adobe ソフトウェア配布で公開され、AEM 6.5.23 の公式リリースが付属します。ソフトウェア配布で **AEM 6.5 Dynamic Media ハイブリッドアドオンパッケージ** を検索すると、該当する機能を見つけることができます。


<!--### [!DNL Forms]{#forms-6523}

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.23.0 Forms add-on package release is scheduled for Thursday, May 29, 2025. A list of Forms fixes and enhancements is added to this section post the release.
 
#### Forms Captcha {#forms-captcha-6523} 

* Improved reCAPTCHA alerting in Adaptive Forms by updating submit error codes to 400. Also, refined log alerts to distinguish between timeouts, expirations, and bot detection failures, enhancing troubleshooting accuracy and system observability. (FORMS-19240) 
* Closed an unclosed `ResourceResolver` instance in `ReCaptchaConfigurationServiceImpl` to prevent potential resource leaks and improve system stability when using reCAPTCHA integrations in AEM Forms. (FORMS-19242) 
* Improved CAPTCHA configuration handling for AEM Forms by ensuring the correct configuration binds to each form when multiple entries exist in the `/conf/global` folder. Prevents unintended use of incorrect CAPTCHA settings when the configuration container is not explicitly selected. (FORMS-19239)-->


<!--
#### XMLFM {#forms-xmlfm-6523}

* A () -->

<!--
#### [!DNL Adaptive Forms] {#adaptive-forms-6523}

* A () -->

<!--
#### [!DNL Forms Designer] {#forms-designer-6523}

* A () -->


### 基盤 {#foundation-6523}

* Coral アラートバナーで、サービスパック 21 にアップグレードするとテキストの色が黒ではなく白く表示される問題を修正しました。 は、インターフェイス全体でアラートメッセージの適切なコントラストと読みやすさを維持するために、正しいスタイルが適用されるようにします。 （NPR-42359）
* JWT （JSON web トークン）の廃止に合わせて、スマートタグ設定での OAuth 統合のサポートが追加されました。 更新された認証方法を使用して、スマートタグ機能の継続的な機能を確保します。 （NPR-42296）

#### Apache Felix {#foundation-apachefelix-6523}

CRXのバイナリタイプのプロパティフィールドに秘密鍵ファイルをアップロードする際に発生していた NullPointerException を修正し、サービスパック 16 を通じて存在していた互換性を復元しました。 サーバーエラーや証明書の更新プロセスを中断することなく、AEM Managed Servicesでの安全なキーファイルアップロードワークフローを有効にします。 （CQ-4359178）


<!--
#### Campaign{#foundation-campaign-6523}

* A () -->

<!--
#### Cloud Services{#foundation-cloudservices-6523}

* A () -->

<!--
#### Communities {#foundation-communities-6523}

* A () -->

<!--
#### Content distribution{#foundation-content-distribution-6523}

* A () -->

<!--
#### CRX {#foundation-crx-6523}

* A () -->


#### Granite{#foundation-granite-6523}

* Service Pack 21 へのアップグレード後にHTML ページを読み込む際に遅延やエラーが発生する Apache Sling スクリプティングサービス間の OSGi 依存関係サイクルを解決しました。 `SightlyScriptingEngineFactory` および関連コンポーネントに関連する循環依存関係を排除し、スクリプトエンジンの信頼性と起動動作を向上させるために、内部サービス参照を更新しました。 （GRANITE-56808）
* JS で、Apache Sling のスクリプトを使用して、起動時に熱心にではなくオンデマンドでのみ読み込むように更新されました。これにより、スレッドの競合が解消され、読み込み中にパブリッシュサーバーが応答しなくなるリスクが軽減されます。 この変更により、スクリプトの早期解決によって発生するリソースのロックが防止されるため、高トラフィックのシナリオ中のサーバーの安定性と応答時間が向上します。 （GRANITE-56611）
* AEM オムニサーチで、入力フィールドのプレースホルダーがラベルとして正しく表示されず、視覚的に混乱する問題を修正しました。 フィルターフィールド間でプレースホルダーが適切にレンダリングされ、一貫性のある、アクセスしやすいフォームの動作が維持されるようにします。 （GRANITE-51791）
* コンテンツフラグメントモデルエディターでマルチフィールド参照を含む 30 個を超える CFM （コンテンツフラグメントモデル）を選択するとトリガーされるサーバーエラーを解決しました。 POST 操作をサポートするようにフィルター提案コンポーネントを強化しました。 この機能により、コンテンツフラグメントの作成時に大きな参照セットを適切に処理でき、大容量モデル設定の安定性が向上します。 （GRANITE-57164）
* CFM で、チェックボックスの近くをクリックすると意図せずに状態が切り替わる問題を修正しました。 クリックのアクティベーションをチェックボックス要素に限定するようにスタイルを更新し、誤ったユーザーの操作を防ぎ、フォームの操作性とアクセシビリティを向上しました。 （GRANITE-52384）


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

カスタムホストヘッダーを含んだDispatcher SSL 設定を使用しているAEMのお客様に対して、SNI 検証で HTTPS 経由の API 呼び出しがブロックされる問題を修正しました。 Jetty 設定の一部として SNI 検証を無効にするオプションを導入し、`mod_proxy` が不可能な特定のリバースプロキシ設定との互換性を有効にします。 （NPR-42614）


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### プラットフォーム{#foundation-platform-6523}

* タグがインラインで作成されたか標準のタグ作成方法を使用して作成されたかに関係なく、結合されたタグ値が常にアセット間で正しく表示されるようにすることで、一貫性のないタグ結合動作を修正しました。 `EN:title` フィールドの残値が、結合されたタグ表示を上書きするのを防ぎます。 （CQ-4358812）
* タグ編集ダイアログボックス内のタグ値におけるアンパサンド文字の繰り返しエンコーディングを修正しました。 保存のたびに「&amp;」エンティティが追加されるのを防ぎ、編集間でタグ値がクリーンで一貫性を維持し、作成されたコンテンツの表示エラーを回避します。 （CQ-4359048）
* WebSphere® 上で動作するAEM 6.5 では、アダプティブフォームの送信時にメールが配信されない `ClassCastException` エラーを修正しました。 この修正により、WebSphere® 環境で期待されるメールハンドラー設定に合わせて `com.sun.mail.handlers.text_plain` と `java.activation.DataContentHandler` の互換性が確保され、メール送信が成功します。 （NPR-42500）
* インストールが失敗し、エラー応答が空の場合にAEMが明確なメッセージを表示するようにすることで、パッケージマネージャーのエラー処理を改善しました。 この修正により、サイレントエラーが防がれ、パッケージのデプロイメント中のより迅速なデバッグに役立ちます。 （NPR-42375）

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### 翻訳{#foundation-translation-6523}

**言語コピーを更新** を使用してワークフローのコンテンツフラグメントを更新する際にトリガーされる NullPointerException （NPE）の問題を修正しました。 この修正により、翻訳参照に関連付けられたコンテンツを編集する際に、ワークフローが失敗した状態に入ったり、実行中の状態のままになったりすることがなくなります。 （NPR-42115）

#### ユーザーインターフェイス{#foundation-ui-6523}

コンポーネント編集ダイアログボックスの **完了** や **キャンセル** など、Coral UI ダイアログボックスのボタンに欠落している `title` 属性を追加して、アクセシビリティを向上させ、自動検証を有効にします。 ボタンがマークアップレンダリング全体で期待される属性を保持し、Selenium ベースの UI テストでエラーが発生しないようにします。 （NPR-42412）

#### WCM{#foundation-wcm-6523}

サービスパック 19 以降を含む環境で **言語コピーを更新** を使用すると、翻訳ジョブにページが追加されない問題を修正しました。 翻訳ワークフローが期待どおりに実行され、手動の操作なしで言語コピー間で適切なページ転送が可能になります。 （CQ-4357929）

#### ワークフロー{#foundation-workflow-6523}

`EmailNotificationServiceProcessor` でホットフィックスのデプロイメント後に `getSegmentId` メソッドが `null` を返し、ワークフローの処理中にメールトリガーが失敗する問題を修正しました。 複数のAEM インスタンスをまたいだメール通知ワークフローをサポートするために、プロセッサーが必要な `SegmentInfo` 値を取得できるようにすることで、適切なセグメント ID 解決ロジックを復元します。 （CQ-4359755）


## [!DNL Experience Manager] 6.5.23.0 のインストール {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.23.0 には [!DNL Experience Manager] 6.5 が必要です。手順について詳しくは、[アップグレードに関するドキュメント](/help/sites-deploying/upgrade.md)を参照してください。<!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.23.0 をインストールします。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.23.0 パッケージを削除またはアンインストールすることを推奨しません。したがって、パッケージをインストールする前に、ロールバックする必要がある場合に備えて `crx-repository` のバックアップを作成する必要があります。 <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### [!DNL Experience Manager] 6.5 へのサービスパックのインストール{#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.23.0.zip)からサービスパックをダウンロードします。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、**[!UICONTROL パッケージをアップロード]**&#x200B;を選択して、パッケージをアップロードします。 詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、**[!UICONTROL インストール]**&#x200B;を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。 [Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログボックスが終了することがあります。 アドビでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.23.0 のインストール方法は 2 つあります。<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。 パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。 ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.23.0 では、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.23.0)` が表示されます。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.20 以降です（web コンソールを使用：`/system/console/bundles`）。 <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### [!DNL Experience Manager] Forms へのサービスパックのインストール{#install-aem-forms-add-on-package}

Experience Manager Forms にサービスパックをインストールする手順について詳しくは、[Experience Manager Forms サービスパックのインストール手順](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)を参照してください。

>[!NOTE]
>
>[AEM 6.5 クイックスタート](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)で使用できるアダプティブフォーム機能は、探索と評価のみを目的として設計されています。 アダプティブフォームの機能には適切なライセンスが必要なので、実稼動環境で使用する場合は、AEM Forms の有効なライセンスを取得することが不可欠です。

### Experience Manager コンテンツフラグメント用の GraphQL インデックスパッケージのインストール{#install-aem-graphql-index-add-on-package}

GraphQL を使用しているお客様は、[Experience Manager コンテンツフラグメントと GraphQL インデックスパッケージ 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?lang=ja#package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip) をインストールする必要があります。

これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

このパッケージをインストールしないと、GraphQL クエリが遅くなったり失敗したりする場合があります。

>[!NOTE]
>
>このパッケージは、インスタンスごとに 1 度だけインストールします。サービスパックごとに再インストールする必要はありません。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.23.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/)で入手できます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.23</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。 メインの UberJar ファイルの名前は、`uber-jar-<version>.jar`に変更されます。 そのため `classifier` が存在せず、`apis` が値として `dependency` タグに使用されます。



## 廃止される機能および削除された機能{#removed-deprecated-features}

AEM 6.5 で非推奨（廃止予定）または削除されたすべての機能の詳細なリストについては、[ 非推奨（廃止予定）の機能と削除された機能 ](/help/release-notes/deprecated-removed-features.md/) を参照してください。

### SPA エディター {#spa-editor}

[SPA エディター ](/help/sites-developing/spa-overview.md) は、AEM 6.5 のリリース 6.5.23 以降、新しいプロジェクトで非推奨（廃止予定）になりました。SPA エディターは、既存のプロジェクトでは引き続きサポートされますが、新しいプロジェクトには使用しないでください。

AEM でヘッドレスコンテンツの管理に推奨されるエディターは次のようになりました。

* ビジュアル編集用の[ユニバーサルエディター](/help/sites-developing/universal-editor/introduction.md)。
* フォームベース編集用の[コンテンツフラグメントエディター](/help/sites-developing/universal-editor/introduction.md)。

## 既知の問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **AEM 6.5.21-6.5.23 およびAEM 6.5 LTS GA の JSP スクリプティングバンドルの問題**
AEM 6.5.21、6.5.22、6.5.23、およびAEM 6.5 LTS GA には、既知の問題を含む `org.apache.sling.scripting.jsp:2.6.0` バンドルが付属しています。 この問題は、通常、AEM インスタンスが多数の同時リクエストを処理する際に高負荷で発生します。

  この問題が発生すると、`org.apache.sling.scripting.jsp:2.6.0` への参照と共に、次の例外のいずれかがエラーログに表示される場合があります。

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  このエラーが発生した場合は、AEM インスタンスを再起動するしかありません。

  Adobeのカスタマーサポートに連絡し、このリリースノートを参照して解決してください。

* **Oak 関連**
サービスパック 13 以降で、永続性キャッシュに影響する次のエラーログが表示されるようになりました。

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  または

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  この例外を解決するには、次の手順を実行します。

   1. 次の 2 つのフォルダーを `crx-quickstart/repository/` から削除する

      * `cache`
      * `diff-cache`

   1. サービスパックをインストールするか、Experience Manager as a Cloud Serviceを再起動します。
`cache` および `diff-cache` の新しいフォルダーが自動的に作成され、`error.log` 内で `mvstore` に関連する例外は発生しなくなりました。

* コンテンツモデルのカスタム API 名を使用していた可能性のある GraphQL クエリを、代わりにコンテンツモデルのデフォルト名を使用するように更新してください。

* GraphQL クエリでは、`fragments` インデックスの代わりに `damAssetLucene` インデックスを使用する場合があります。 このアクションは結果的に、GraphQL クエリが失敗するか、実行に非常に長い時間がかかる可能性があります。

  問題を修正するには、`damAssetLucene` では、`/indexRules/dam:Asset/properties` に次の 2 つのプロパティを含むように設定する必要があります。

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  インデックス定義を変更した後、インデックス再作成が必要です（`reindex` = `true`）。

  これらの手順を行うと、GraphQL クエリの実行が高速化されます。

* コンテンツフラグメント、サイト、ページのいずれかを移動、削除または公開しようとすると、コンテンツフラグメント参照が取得される際に問題が発生します。 バックグラウンドクエリが失敗します。 つまり、この機能が動作しなくなります。
正しく動作させるには、インデックス定義ノード `/oak:index/damAssetLucene` に次のプロパティを追加する必要があります（インデックスの再作成は不要です）。

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* [!DNL Experience Manager] インスタンスを 6.5.0 ～ 6.5.4 から Java™ 11 の最新サービスパックにアップグレードすると、`error.log` ファイルに `RRD4JReporter` 例外が表示されます。 例外を停止するには、[!DNL Experience Manager] のインスタンスを再起動します。 <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。 ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* [!DNL Experience Manager] 6.5.x.x のインストール中に、次のエラーや警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して [!DNL Experience Manager] に Adobe Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」／ソース「Adobe Experience Manager」タイプではなく、「HTML」／ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：`granite/operations/maintenance` にメンテナンスウィンドウがありません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：`granite/operations/maintenance` にメンテナンスウィンドウがありません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`：登録状況を未登録に変更する処理が完了するのを待機中にタイムアウトになりました。

* AEM 6.5.15 以降、```org.apache.servicemix.bundles.rhino``` バンドルで提供される Rhino JavaScript Engine には、新しい巻上げ動作が追加されました。 strict モード（```use strict;```）を使用するスクリプトでは、正しい変数を宣言する必要があります。 そうしないと、実行されず、ランタイムエラーがスローされます。

* 公式アップデートパッケージを通じてタグ付け関連の標準コンテンツをインストールすると、`/content/cq:tags` ノードの言語プロパティがデフォルトにリセットされます。 このアクションは、サービスパック、セキュリティサービスパック、拡張機能パック、累積機能パック、パッチなどに当てはまります。 したがって、インストール前にプロパティから追加しておく必要があります。

### AEM Sites の既知の問題 {#known-issues-aem-sites-6523}

コンテンツフラグメント - 大きなフラグメントツリーに対する DoS 保護が原因でプレビューに失敗します。 詳しくは、[GraphQL Query Executor のデフォルト設定オプションに関するナレッジベース記事](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-23945)（SITES-17934）を参照してください。

<!--### Known issues for AEM Forms {#known-issues-aem-forms-6523}

* If the HTML to PDF conversion fails on a SUSE&reg; Linux&reg; (SLES 15 SP6 onwards) server with the following error:
  
  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
  then set the following environment variable and restart the server:
    `OPENSSL_CONF=/etc/ssl`

* After installing AEM Forms JEE Service Pack 21 (6.5.21.0), if you find duplicate entries of Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` under the `<AEM_Forms_Installation>/lib/caching/lib` folder (FORMS-14926), perform the following steps to resolve the issue:

  1. Stop the locators, if they are running.
  1. Stop the AEM Server. 
  1. Go to the `<AEM_Forms_Installation>/lib/caching/lib`. 
  1. Remove all the Geode patch files except `geode-*-1.15.1.2.jar`. Confirm that only the Geode jars with `version 1.15.1.2` are present.
  1. Open the command prompt in administrator mode.  
  1. Install the Geode patch using the `geode-*-1.15.1.2.jar` file. 

* If a user tries to preview a draft letter with saved XML data, it gets stuck in `Loading` state for some specific letters. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (FORMS-14521)
  
* After upgrading to AEM Forms Service Pack 6.5.21.0, the `PaperCapture` service fails to perform OCR (Optical Character Recognition) operations on PDFs. The service does not generate output in the form of a PDF or a log file. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (CQDOC-21680)

* When users upgraded from AEM 6.5 Forms Service Pack 18 or 19 to Service Pack 20 or 21, they encountered a JSP compilation error. This error prevented them from opening or creating adaptive forms. It also caused issues with other AEM interfaces. Those interfaces included the Page Editor, AEM Forms UI, Workflow editor, and System Overview UI. (FORMS-15256)

  If you face such an issue, perform the following steps to resolve it:
    1. Navigate to the directory `/libs/fd/aemforms/install/` in CRXDE.
    1. Delete the bundle with the name `com.adobe.granite.ui.commons-5.10.26.jar`.
    1. Restart your AEM Server.

* After updating to AEM Forms Service Pack 20 (6.5.20.0) with the Forms Add-On, configurations relying on the legacy Adobe Analytics Cloud Service using credential-based authentication stop working. This issue prevented analytics rules from executing correctly. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (FORMS-15428)

* When a user updates to AEM Forms Service Pack 20 (6.5.20.0) on the JEE server and generates PDFs using output services, the PDFs render with accessibility issues. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922112)
* When a user generates Tagged PDFs using the output service on JEE, it shows "Inappropriate structure warning." To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922038)
* When a form is submitted on AEM Forms JEE, the instances of a repeating XML element are removed from the data. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3922017)
* When a user in a Linux&reg; environment renders an Adaptive Form (on JEE) in HTML, it fails to render properly. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921957)
* When a user converts an XTG file to PostScript format using the Output Service on AEM Forms JEE, it fails with the error: `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921720)
* After upgrading to AEM Forms Service Pack 18 (6.5.18.0) on JEE server, when a user submits a form, it fails to render HTML5 or PDF Forms and XMLFM crashes. To download and install the hotfix, refer to the [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms) article. (LC-3921718)
* In the Print Preview of the Interactive Communications Agent UI, the currency symbol (such as the dollar sign $) is inconsistently displayed for all field values. It appears for values up to 999 but is missing for values of 1000 and above. (FORMS-16557)
* Any modifications to nested layout fragments' XDP in an Interactive Communication are not reflected in the IC editor. (FORMS-16575)
* In the Print Preview of the Interactive Communications Agent UI, some calculated values are not displayed correctly. (FORMS-16603)
* When the letter is viewed in Print Preview, the content is changed. That is, some spaces disappear, and certain letters are replaced with `x`. (FORMS-15681)
* When a user configures a WebLogic 14c instance, the PDFG service in AEM Forms Service Pack 21 (6.5.21.0) on JEE running on JBoss&reg; fails due to classloader conflicts involving the SLF4J library. The error is displayed as follows (CQDOC-22178):
  
    ```java
    Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
    the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
    @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
    (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
    have different Class objects for the type org/slf4j/ILoggerFactory used in the signature-->

## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、この [!DNL Experience Manager] 6.5 サービスパックリリースに含まれている OSGi バンドルとコンテンツパッケージのリストが記載されています。

* [Experience Manager 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) に含まれている OSGi バンドルのリスト<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.23.0](/help/release-notes/assets/65230-packages.txt) に含まれているコンテンツパッケージのリスト<!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

これらの web サイトは、のお客様のみが利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/ja/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-65)
>* [アドビ製品アップデートの優先通知を購読](https://www.adobe.com/subscription/priority-product-update.html)
