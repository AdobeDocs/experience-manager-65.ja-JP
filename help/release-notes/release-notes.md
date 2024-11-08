---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: bb6e843bfad3feb194dd00588dbb4a2d3539743a
workflow-type: tm+mt
source-wordcount: '4658'
ht-degree: 41%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2024年11月21日木曜日（PT）<!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.22.0 の内容 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0 には、新機能、お客様からリクエストされた主な機能強化、バグ修正が含まれています。 また、2019年4月の 6.5 の公開当初以降にリリースされたパフォーマンス、安定性、セキュリティの改善も含まれています。 [このサービスパックを [!DNL Experience Manager] 6.5 にインストールします](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主な機能および機能強化

<!-- * _6.5.22.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

このリリースの主な機能と機能強化は次のとおりです。


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## サービスパック 22 で修正された問題 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### アクセシビリティ {#sites-accessibility-6522}

* 注釈スウォッチセレクターボタンにアクセス可能な名前がありませんでした。 つまり、スクリーンリーダーを使用する場合、新しい 16 進数値の入力後に選択するボタンに、人間が理解できる名前はありません。 （SITES-11992）重要
* 左側のパネルメニューにある次の要素はリストのように表示されますが、スクリーンリーダーでそのようにマークアップされません。

   * サイト
   * ライブコピー
   * Experience Platform Launch
   * 言語コピー
   * フォルダー
   * CSV レポート （SITES-2874）

* AEM Core Web Content Management には、リッチテキストエディター内のハイパーリンクにアクセシビリティラベルが必要です。 テキストコンポーネントでハイパーリンクが使用される場合、スクリーンリーダーがアクセシビリティ目的でリンクテキストを正確に読み取り、伝えることができるように、アンカータグに `aria-label` 属性を含める必要があります。 （SITES-11511）
* AEMでは、リスト表示のテーブルヘッダー内のインタラクティブ要素に、必要な「ボタン」のロールがありません。 そのため、NVDA スクリーンリーダーは、次のテーブルヘッダー（タイトル、名前、変更済み、公開済み、プレビュー、テンプレート、操作、ワークフロー）に対して期待されるボタンロールを通知しません。 テーブルヘッダーの各インタラクティブ要素には、NVDA などの支援テクノロジーとの互換性を確保するために、「ボタン」の役割を割り当てる必要があります。 （SITES-10962）


#### 管理者ユーザーインターフェイス{#sites-adminui-6522}

* AEMの一部のインスタンスでは、複数のページでバージョンのプレビューおよび比較機能が期待どおりに動作しませんでした。 具体的には以下のとおりです。

   * **プレビューの問題：** ページバージョンをプレビューしようとすると、最初にエラーが表示される。 再試行後、プレビューすると空白のページが表示されます。
   * **バージョン比較の問題：** 「現在のバージョンと比較」機能は、バージョン間の違いを強調表示せずに現在のバージョンのみを表示しました。 （SITES-23988）重要

* コピーおよび貼り付けアクション中に `plaintext` に設定された `defaultPasteMode` を使用すると、予期しない `<br>` タグがリッチテキストエディター（RTE）フィールドに表示される。 この問題により、同じコンテンツのマークアップが異なるので、同じテキストコンテンツが顧客の翻訳メモリで 2 回翻訳されます。 （SITES-23606）重要
* AEM 6.5.20.0 では、**公開を管理** 機能に関する問題が発生していました。 ノードを選択し、今後の公開のスケジュールを設定する際、子ノードを含めようとすると、「選択したアイテムの子リソースを取得できませんでした」というエラーメッセージが表示される場合があります。 この問題は、「**子を含める**」オプションの使用をブロックしていて、意図したコンテンツ階層を完全に公開できなかった問題です。 （SITES-23000）重要
* テンプレートがパブリッシュインスタンスに正常にレプリケートされたにもかかわらず、オーサー環境でテンプレートの「公開済み」タイムスタンプが更新されていませんでした。 オーサーインスタンスのタイムスタンプが最新のパブリケーションを反映するように想定された動作でしたが、意図したとおりに更新されませんでした。 （SITES-21585）重要
* AEM オーサー環境の受信リンクの数が一致しませんでした。 左側のパネルには、クラシック UI に比べて表示されるリンクの数が少なくなりました。 また、正当な着信リンクの一部が機能しない場合もあります。 （SITES-24837）
* AEMのタイムライン ビューでページバージョンを表示すると、非常に長い読み込み時間が報告されていました。 バージョンを表示するのに最大 19 分かかっていました。 この問題は、AEM 6.4.8 から 6.5.18 にアップグレードした後も発生しており、ワークフローの効率が大幅に低下していました。 （SITES-22468 および SITES-22467）

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* アップグレードされたAEM 6.5.17 で、コンテンツフラグメントを保存すると、次のエラーが発生しました：*エラー：コンテンツフラグメントを保存できませんでした。* （SITES-22993）重要
* AEMのパブリッシャーで、`ContentFragmentModelOmniSearchHandler` のリソースリゾルバーが閉じられていない問題が特定されました。 （SITES-24903）


#### [!DNL Content Fragments] - Admin{#sites-admin-6522}

* メール通知内のリンクをクリックすると、デフォルトのアセットビューアまたはエディターに移動します。 ワークフロー内のアセットがコンテンツフラグメントと判断された場合でも、コンテンツフラグメントエディターの代わりに使用します。 （SITES-24338）重要


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6522}

* 複数行テキストフィールド項目でコンテンツフラグメントを使用する場合、GraphQLを使用してクエリを実行すると、HTMLで指定された書式が保持されなかったマークアップが表示されます。 例えば、リストの後に改行がなかった場合などです。 最後の段落がリストの一部になったことが影響しました。 （SITES-23233）


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### コアバックエンド{#sites-core-backend-6522}

* AEM オーサーインスタンスで繰り返し `SegmentNotFoundException` エラーが報告されました。 オーサーを再起動すると問題は一時的に解決しましたが、それ以上の発生を防ぐために、長期的な修正が必要でした。 （SITES-22573）
* AEM Sitesのタイムライン機能、特に注釈の欠落している `cq:lastModified` プロパティの処理に関する問題が提起されました。 AEM 6.5.20 を適用した後、既存のコンテンツに欠落しているプロパティの修正が必要かどうか、またはプロパティを使用せずにタイムラインが正しく機能するように更新されたかどうかについて、不確実性がありました。 （SITES-21861）


#### コアコンポーネント{#sites-core-components-6522}

* AEM 6.5.18 から 6.5.21 へのアップグレード後、コンポーネントのライブ使用状況をチェックする機能に問題が見つかりました。 ライブ使用状況ページで追加の項目をスクロールしようとすると、UI に「さらに項目を読み込み中」と表示されていても、テーブルはより多くの結果を読み込めませんでした。 （SITES-23919）
* 2 つのタブを含むAEM コンポーネントダイアログボックスの必須フィールドの検証に関する問題が報告されました。 タブ 1 にはリッチテキストエディター（RTE）とテキストフィールドが含まれ、タブ 2 にはパスフィールドとテキストフィールドがありました。 すべてのフィールドが必須（`required=true`）としてマークされていますが、すべての必須フィールドに入力した後でも、エラー通知がタブ 1 に正しく保持されません。 これに対し、Tab 2 のエラーは期待どおりにクリアされました。 （SITES-23243）
* AEM 6.5.21 に移行すると、HTMLテンプレートの Language `data-sly-include` ステートメントが期待どおりに機能しなくなり、特に `appendPath` 式と `prependPath` 式のサポートに失敗しました。 その結果、移行前には正しく動作していましたが、含まれるリソースの出力が正しくレンダリングされませんでした。 この問題が原因で、パス操作にこれらの式を利用するリソースのレンダリングエラーが発生しました。 （GRANITE-52970）


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### エクスペリエンスフラグメント{#sites-experiencefragments-6522}

* リスト表示で **タイトル** 列ヘッダーがクリックされた場合、エクスペリエンスフラグメントがタイトルで期待どおりに並べ替えられない。 画面の素早いちらつきが発生しますが、並べ替えは行われません。 （SITES-23706）重要

* AEM 6.5.17 では、標準機能を使用してページコンポーネントをエクスペリエンスフラグメントに変換する際に問題が発生しました。 変換後、エクスペリエンスフラグメントが使用されたページに正しく表示されているにもかかわらず、編集中にエクスペリエンスフラグメントが空のように見えた。 この問題は、ノードの作成が正しくないことから発生しました。コンポーネントノードがルート/コンテナノードの外部に配置され、テンプレートの構造に違反していました。 フラグメントの編集可能性を復元するには、コンポーネントノードを正しいルート/コンテナノードに手動で移動する必要がありました。 （SITES-22974）重要

* AEM 6.5.11 から 6.5.20 へ移行後、エクスペリエンスフラグメントでクラウド設定が正しく保存されませんでした。 設定は `crx/de` で保存されているように見えましたが、設定コンソールを再度開いても表示されず、永続性に関する問題が示されます。 （SITES-22287）重要


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### ローンチ{#sites-launches-6522}

* AEM実稼動環境でタグ付けフィルターを使用してエクスペリエンスフラグメントアセットを追加する際、ユーザーはアセットを選択できましたが、「**言語コピーを作成**」を選択した後にエラーが発生しました。 期待される動作は、タグ付けフィルターから選択されたエクスペリエンスフラグメントアセットが翻訳プロジェクトに追加されることになっていました。 （SITES-24152）重要

#### リンクチェッカー{#sites-link-checker-6522}

* HTTP クライアントが基本認証の前に NTLM を試行するため、LinkCheckerTask の認証に失敗します。この結果、プロキシは複数回の試行に失敗した後でユーザーをブロックします。 システムは、代わりに基本認証を使用してプロキシに対して認証を行い、LinkCheckerTask サービスを正しく機能させる必要があります。 （SITES-25034）重要


#### MSM - ライブコピー{#sites-msm-live-copies-6522}

* SEO ロボットタグがプライマリコピーに適用され、ライブコピーページにロールアウトされると、`crx/de` に値が正しく表示されていました。 ただし、ライブコピーページのページプロパティ配下のユーザーインターフェイスには値が反映されません。 （SITES-23475）重要
* ユーザーインターフェイスを使用してローンチを昇格しようとすると、ローンチに関連するエラーが表示されていました。 ローンチを昇格ウィザードが空のままで、昇格プロセスを完了できませんでした。 （SITES-19718）
* AEMでエクスペリエンスフラグメントがライブコピーを作成してロールアウトを実行しようとすると、問題が発生します。 ロールアウト画面からエクスペリエンスフラグメント管理画面に戻ろうとしたときに `NotFound` エラーが発生したとき、問題が発生していました。 （SITES-21933）


#### ページエディター{#sites-pageeditor-6522}

* 「取り消し」ボタンをクリックすると、テキストが最後のバージョンに変更され、コンポーネントの位置も変更されます。 （SITES-17465）ブロッカー
* コピーしたコンテナコンポーネントが貼り付けられると、視覚的に 2 回表示され、ページに 3 つのインスタンスが表示されます。 ただし、ページを更新すると、重複が消えたので、一時的な視覚的な問題である可能性が高いと考えられます。 （SITES-21890）重要
* キーボードの Tab キーまたは Shift + Tab キーを使用してコンポーネントの左側のペインを移動する際、複数のテキスト要素が視覚的にもタブモードでも明確に表示されませんでした。 この問題はアクセシビリティに影響を与えたため、キーボードナビゲーション中にこれらのコンポーネントを特定したり操作したりすることが困難になりました。 （SITES-2266）

#### レプリケーション{#sites-replication-6522}

* AEM 6.5.18 および 6.5.19 では、親ページを非アクティブ化すると、子ページごとに複数の非アクティブ化リクエストが生成されていました。 この問題は、GraphQL エンドポイントの一括非公開にも影響していました。 （NPR-42075 および NPR42010）重要


### [!DNL Assets]{#assets-6522}

* Connected Assets機能を使用する間、AEM Assetsで行われた更新は、AEM Sites環境には反映されません。 （ASSETS-42344）主 <!-- Leave the "MAJOR" status priorities in place. -->
* （ASSETS-41158）重要
* API を使用してアセットをアップロードすると、エラーメッセージ `unclosed resource resolver` 表示されます。 （ASSETS-41049）重要
* （ASSETS-40384）重要
* AEM バージョン 6.5.19 では、検索パネルの結果から 1 つのオプションを削除すると、使用可能な他のすべてのチェックボックスもオフになります。 （ASSETS-37335）重要
* 無効な値は、一括メタデータの書き出し操作の実行中に Excel 出力に表示されます。 （ASSETS-37260）重要
* AEM バージョン 6.5.19 で UTF-8 形式のSVGファイルをアップロードすると、出力がぼやけます。 （ASSETS-36616）重要
* Connected Assets設定内に `Fetch original rendition for Dynamic Media Connected Assets` オプションがありません。 （ASSETS-41726）
* 必須フィールドの値を定義しなくても、アセットのプロパティは保存されます。 （ASSETS-37914）

#### [!DNL Dynamic Media]{#assets-dm-6522}

* 実稼動環境の問題により、Dynamic Mediaへのビデオのアップロードに失敗すると、移行プロセスが中断され、ユーザーインターフェイスにプロセスエラーエラーが表示されます。 （ASSETS-36038）


### [!DNL Forms]{#forms-65220}

[!DNL Experience Manager] Forms の修正は、[!DNL Experience Manager] サービスパックリリース予定日の 1 週間後に、別のアドオンパッケージとして提供されます。この場合、AEM 6.5.22.0 Forms アドオンパッケージリリースは、2024年11月28日木曜日（PT）に予定されています。Forms の修正および機能強化のリストは、リリース後にこの節に追加されます。


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### 基盤 {#foundation-6522}

* AEM Assets コンソールで、DITA 文書を並べ替えようとした際に問題が発生しました。 パスブラウザーダイアログボックスの上部にあるパンくずリストに、ルートの親のノードタイトルではなくノード名が誤って表示されます。 正しいノードタイトルは、パンくずリスト内の項目を選択した後にのみ表示され、一時的な表示エラーを示します。 （NPR-42106）重要


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### Communities {#foundation-communities-6522}

* AEM 6.5.19 から 6.5.20 にアップグレードした後、`UgcSearch` を呼び出した後、`Connection evic` スレッドが適切に閉じられない問題が発生しました。 この問題は実稼動環境で発生し、これらのスレッドが保持され、時間の経過と共に蓄積して、パフォーマンスに影響を与える可能性があります。 （NPR-42019）重要


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* CRX パッケージマネージャーの左側のメニューの **グループ** に従って、並べ替えが機能しませんでした。 （GRANITE-53277）
* AEMのパッケージマネージャーは、デフォルトでは下位のパッケージバージョンのインストールを制限しますが、古いバージョンの強制的なインストールは許可します。 ただし、強制インストールオプションを使用すると、標準パイプラインを通じた今後のインストールが妨げられる可能性があります。 例えば、バージョン 1.21 がインストールされ、バージョン 1.24 が追加されている場合、インストールは成功し、両方のバージョンが一覧表示されます。 ただし、1.24 よりもバージョン 1.22 をインストールしようとすると、パイプラインを通じて失敗しますが、強制的にインストールした場合は機能し、すべてのバージョンが表示されます。 同様に、バージョン 1.24 が既に存在する場合は、パイプラインがダウングレードを許可しないので、バージョン 1.23 のインストールはブロックされます。 （GRANITE-53263）


#### Granite{#foundation-granite-6522}

* スナップショットパッケージは、CURL コマンドを使用してAEMにインストールされていました。 インストール中、JCR インストーラーは OSGI インストーラーを介してパッケージをスキャンし、追加の OSGI バンドルまたは設定が必要ないことを確認します。 パッケージバージョンに「SNAPSHOT」が含まれている場合、OSGI インストーラーは VLT をトリガーし、対応するスナップショットパッケージを作成しました。 ただし、各AEM オーサーインスタンスが独自の OSGI インストーラーを実行するので、両方のインスタンスがスナップショットを同時に生成しようとすると、リポジトリ内でセッションの競合が発生する可能性があります。 （NPR-42003）重要
* AEM 6.5.21 には、ロックの競合が `ScriptDependencyResolver` に存在していました。 （GRANITE-53181）重要
* AEMを 6.5.21 にアップグレードした後、`data-sly-use` などの Sightly （HTL）構文で相対パスを使用すると問題が発生します。 （GRANITE-53080）重要


#### 統合{#foundation-integrations-6522}

* Cloud Serviceユーザーインターフェイスの法的属性文を追加しました。 （FORMS-16373）
* **fd-cloudservice** ユーザーが hCaptcha および Turnstile 設定にアクセスするための読み取り権限の追加。これにより、captcha のレンダリングと検証に必要なクライアント ID とクライアント秘密鍵を取得できます。 さらに、これらの設定へのアクセスを管理するために、アクセス制御リスト モデルが実装されました。 （FORMS-16360）


#### ローカライゼーション{#foundation-localization-6522}

* ![ ハンマーアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) ツール/**セキュリティ**/![ ユーザーアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg)**ユーザー** の「ユーザー管理」ページで、テーブルの **ステータス** 列のデータが縦に表示されていました。 （GRANITE-48304）


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### プラットフォーム{#foundation-platform-6522}

* AEM 6.5.18 で導入された Enterprise Information Management のトラッキングにより、製品の採用スコアの計算に異常が生じました。 この問題は、Adobe指標ライブラリが、Omega トラッキングライブラリから提供されるユーザーデータを上書きしたために発生しました。 その結果、2024 年 2 月以降、多くのAEM SitesおよびAEM Assetsのお客様の採用スコアはゼロに低下しました。 （CQ-4358438）重大
* ガベージコレクターがタグを誤って処理していた実稼動環境で、重大な問題が特定されました。 特に、タグが移動または名前変更されると、ガベージコレクターが `cq:MovedTo` プロパティの更新に失敗し、タグがページから消えてしまいます。 （CQ-4358293）重要
* AEM 6.5.19 でコンテキストパスがAEM インスタンスに追加された場合、ContextHub の問題が原因でセグメントが正しく解決されませんでした。 この問題は、特に、ページコンポーネントで生成されたJavaScript オブジェクト内の URL フィールドに影響を与えました。ここでは、必須のコンテキストパスのプレフィックスがありません。 この省略により、セグメントが期待どおりに機能しませんでした。 （SITES-21852）
* AEM クイックスタートを更新して、ライブラリ `commons-collections-3.2.2-adobe-2` を使用するようにしました。 この更新により、アプリケーションをスムーズに実行し続けることができます。 （NPR-42150）
* AEM 6.5 の SMTP OAuth2 設定は、AEM as a Cloud Serviceで使用される設定とは大きく異なります。 設定を合理化して一貫性を確保するには、AEM as a Cloud Serviceで使用される標準に合わせてAEM 6.5 を設定する必要がありました。 （GRANITE-53273）
* ![ コンパスアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg)/![ プロジェクトアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg) プロジェクトをクリックし、![ 左パネルのアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg)![ 山形の下アイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) にマウスポインターを置くと、ツールヒントテキスト「コンテンツのみ」の前に大きなアクセントが表示される問題が見つかりました。 （CQ-4356633）

#### セキュリティ{#foundation-security-6522}

* AEMの古い JSAFE 暗号化ライブラリ（バージョン 6.0.0）で問題が発生しました。 JSAFE バージョン 6.2.5 のパッチが適用されたバンドルは、AEM 6.5.22 に含まれています。 （NPR-42006）重要
* XSS チェック中に許可されたプロトコルを検証する場合、ハンドラーは「http」および「https」と比較します。 ただし、URL オブジェクトの `protocol` プロパティは、`http:` や `https:` のように、これらの値の末尾にコロンを付けて返しました。 この不一致により、検証の問題が発生しました。 正確な解析を行うために、プロトコルのチェックでコロンを考慮するか、それに応じて比較ロジックを調整する必要があります。  （NPR-42119）
* AEM 6.5.21 （以前のバージョンはAEM 6.5.19）をIBM® WebSphere® Liberty プロファイルおよび Semeru Java 8.0 にインストールした後、ページを開くことができませんでした。 エラーログに、異なるバンドルが必要なサーブレットバージョンに関する問題が示されました。 この問題に対処するには、問題に関連するので、`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` への依存を元に戻す必要がありました。 （NPR-42116）
* 複数のブラウザーで、cookie へのクロスサイトアクセスを許可するために使用される **SameSite=None** cookie のサポートが段階的に廃止されています。 別の方法として、**パーティション Cookie** が導入されています。 これらの cookie は、使用されるコンテキストによってストレージを分離し、サイト間のトラッキングを防ぐことでプライバシーとセキュリティを強化すると同時に、埋め込みサードパーティコンテンツなどの特定のパーティション内で cookie を機能させることができます。 （GRANITE-51953）


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### 翻訳{#foundation-translation-6522}

* コアコンポーネントで最近の変更をサポートし、デフォルトの翻訳ルールを追加しました。 （NPR-42029）重要
* AEM Formsへの XLIFF ファイルの書き出しに関する問題が特定されました。 **選択を XLIFF として書き出し（文字列のみ）** オプションを使用する場合、コンポーネントのシーケンスが一貫して維持されていませんでした。 ただし、特定の言語の XLIFF を書き出す場合、シーケンスは正しいままです。 問題を示すために、**DE-CH_Export.xliff** （正しいシーケンス）と **String_Export.xliff** （間違ったシーケンス）の 2 つのファイルが提供されました。 （NPR-42118）重要


#### ユーザーインターフェイス{#foundation-ui-6522}

* `coralui-component-dialog` は `cq-dialog-actions` の配置を変更しており、AEMのダイアログボックス内のアクションボタンのレイアウトや動作に影響を与える可能性がありました。 （NPR-42294）ブロッカー
* AEMのカラーピッカー機能が正しく動作しませんでした。 アクセスすると、空白のモーダルが表示され、カラーの選択が妨げられました。 この問題は、ステージング環境にAEM 6.5.20 をインストールした後に発生していました。 カラーピッカーは更新前 *正常* 動作。 （NPR-42163）
* ![ ハンマーアイコン ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg)**ツール**/**ワークフロー**/**モデル**/任意のモデルを選択/**ワークフローを開始** で、**ワークフローを実行** ダイアログボックスの「ペイロード」フィールドに参照アイコンが表示されませんでした。 （NPR-42162）


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A 


## Install [!DNL Experience Manager] 6.5.22.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0 には [!DNL Experience Manager] 6.5 が必要です。手順について詳しくは、[アップグレードに関するドキュメント](/help/sites-deploying/upgrade.md)を参照してください。 <!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.22.0 をインストールします。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.22.0 パッケージを削除またはアンインストールすることを推奨しません。 したがって、パッケージをインストールする前に、ロールバックする必要がある場合に備えて `crx-repository` のバックアップを作成する必要があります。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### [!DNL Experience Manager] 6.5 へのサービスパックのインストール{#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip)からサービスパックをダウンロードします。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、**[!UICONTROL パッケージをアップロード]**&#x200B;を選択して、パッケージをアップロードします。 詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、**[!UICONTROL インストール]**&#x200B;を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。 [Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログボックスが終了することがあります。 アドビでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.22.0 のインストール方法は 2 つあります。<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。 パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。 ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.22.0 では、Bootstrap のインストールをサポートしていません。 <!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.22.0)` が表示されます。 <!-- UPDATE FOR EACH NEW RELEASE -->

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

[!DNL Experience Manager] 6.5.22.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/)で入手できます。 <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。 メインの UberJar ファイルの名前は、`uber-jar-<version>.jar`に変更されます。 そのため `classifier` が存在せず、`apis` が値として `dependency` タグに使用されます。


## 廃止される機能および削除された機能{#removed-deprecated-features}

[廃止される機能および削除された機能](/help/release-notes/deprecated-removed-features.md/)を参照してください。

## 既知の問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


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

### AEM Sites の既知の問題 {#known-issues-aem-sites-6522}

* 大きなフラグメントツリーの DoS 保護が原因で、コンテンツフラグメント – プレビューが失敗する。 デフォルトのGraphQL Query Executor 設定オプションについては、[KB の記事を参照してください ](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-23945) （SITES-17934）


### AEM Forms の既知の問題 {#known-issues-aem-forms-6522}


* AEM Forms JEE サービスパック 21（6.5.21.0）のインストール後、`<AEM_Forms_Installation>/lib/caching/lib` フォルダー配下に Geode JARs `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` の重複エントリが見つかった場合（FORMS-14926）、問題を解決するには、次の手順に従います。

   1. ロケーターが実行中の場合は、ロケーターを停止します。
   1. AEM サーバーを停止します。
   1. `<AEM_Forms_Installation>/lib/caching/lib` に移動します。
   1. `geode-*-1.15.1.2.jar` を除くすべての Geode パッチファイルを削除します。 `version 1.15.1.2` を含む Geode jar のみが存在することを確認します。
   1. 管理者モードでコマンドプロンプトを開きます。
   1. `geode-*-1.15.1.2.jar` ファイルを使用して Geode パッチをインストールします。

* ユーザーが保存された XML データを含むドラフトレターをプレビューしようとすると、一部の特定のレターが `Loading` 状態でスタックする。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （FORMS-14521）

* AEM Forms サービスパック 6.5.21.0 へのアップグレード後、`PaperCapture` サービスが、PDF に対して OCR（光学文字認識）処理を実行できない。 このサービスでは、PDF やログファイルの形式で出力を生成しません。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （CQDOC-21680）

* AEM 6.5 Forms サービスパック 18 または 19 からサービスパック 20 または 21 にアップグレードした際に、JSP コンパイルエラーが発生しました。 このエラーにより、アダプティブフォームを開いたり作成したりすることができませんでした。 また、他のAEM インターフェイスにも問題が発生しました。 これらのインターフェイスには、ページエディター、AEM Forms UI、ワークフローエディターおよびシステム概要 UI が含まれていました。 （FORMS-15256）

  このような問題が発生した場合は、次の手順を実行して解決します。
   1. CRXDE のディレクトリ `/libs/fd/aemforms/install/` に移動します。
   1. `com.adobe.granite.ui.commons-5.10.26.jar` という名前のバンドルを削除します。
   1. AEM サーバーを再起動します。

* Forms アドオンを使用してAEM Forms サービスパック 20 （6.5.20.0）にアップデートすると、資格情報ベースの認証を使用した従来のAdobe Analytics Cloud サービスに依存する設定が機能しなくなります。 この問題により、analytics ルールが正しく実行されませんでした。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （FORMS-15428）

* JEE サーバー上でAEM Forms サービスパック 20 （6.5.20.0）に更新し、出力サービスを使用してPDFを生成すると、PDFがレンダリングされてアクセシビリティの問題が発生します。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。（LC-3922112）
* JEE 上の Output サービスを使用してタグ付きPDFを生成すると、「不適切な構造の警告」が表示される。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （LC-3922038）
* AEM Forms JEE でフォームを送信すると、繰り返し XML 要素のインスタンスがデータから削除されます。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （LC-3922017）
* Linux® 環境で（JEE 上の）アダプティブフォームをHTMLーでレンダリングすると、が適切にレンダリングされません。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （LC-3921957）
* ユーザーが AEM Forms JEE の Output サービスを使用して XTG ファイルを PostScript 形式に変換する際に、エラー `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE` が発生して失敗します。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （LC-3921720）
* JEE サーバーで AEM Forms サービスパック 18（6.5.18.0）にアップグレードした後、ユーザーがフォームを送信すると、HTML5 または PDF フォームのレンダリングに失敗し、XMLFM がクラッシュします。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （LC-3921718）
* インタラクティブ通信エージェント UI の印刷プレビューでは、すべてのフィールド値に通貨記号（ドル記号 $ など）が一貫して表示されません。999 までの値の場合は表示されますが、1000 以上の値の場合は表示されません。（FORMS-16557）
* インタラクティブ通信内でネストされたレイアウトフラグメントの XDP に対する変更は、IC エディターに反映されません。（FORMS-16575）
* インタラクティブ通信エージェント UI の印刷プレビューでは、一部の計算値が正しく表示されません。（FORMS-16603）
* 印刷プレビューでレターを表示すると、コンテンツが変更されます。 つまり、一部のスペースが消え、特定の文字が「x」に置き換えられます（FORMS-15681）

## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、この [!DNL Experience Manager] 6.5 サービスパックリリースに含まれている OSGi バンドルとコンテンツパッケージのリストが記載されています。

* [Experience Manager 6.5.22.0 に含まれている OSGi バンドルのリスト](/help/release-notes/assets/65210-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.22.0 に含まれているコンテンツパッケージのリスト](/help/release-notes/assets/65210-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/ja/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-65)
>* [アドビ製品アップデートの優先通知を購読](https://www.adobe.com/subscription/priority-product-update.html)
