---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 167d897cc5f44a2302a4ba932e238e6ba973635d
workflow-type: tm+mt
source-wordcount: '6030'
ht-degree: 88%

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
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.22.0 の内容 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0 には、新機能、お客様からリクエストされた主な機能強化、バグ修正が含まれています。また、2019年4月の 6.5 の公開当初以降にリリースされたパフォーマンス、安定性、セキュリティの改善も含まれています。 [このサービスパックを [!DNL Experience Manager] 6.5 にインストールします](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主な機能および機能強化

### Forms {#forms-sp22}

このリリースの主な機能と機能強化は次のとおりです。

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) および [Cloudflare Turnstile CAPTCHA サービス ](/help/forms/using/integrate-adaptive-forms-turnstile.md):AEM Formsは、次の Captcha サービスをサポートしています。
   * hCaptcha は、チェックボックスウィジェットを使用してユーザーに入力を要求し、ボット、スパム、自動化された不正使用からフォームを保護します。これにより、人間のユーザーのみが続行でき、オンライントランザクションのセキュリティが強化されます。
   * Cloudflare Turnstile は、自動ボット、悪意のある攻撃、スパム、不要な自動トラフィックからフォームを保護することを目的としたセキュリティ対策を提供します。フォームの送信を許可する前に、フォームの送信時にユーザーが人間であることを確認するチェックボックスが表示されます。

* アダプティブフォームのバージョン管理：
   * [ アダプティブフォームの複数のバージョンの作成 ](/help/forms/using/add-versioning-reviews-comments.md) – 既存のフォームのバリエーションを簡単に管理できるようになりました。 このプロセスにより、バージョン管理が簡素化され、フォームの最適化の比較が容易になります。これらはすべて、合理化された単一のワークフロー内で行われます。
   * [アダプティブフォームの比較](/help/forms/using/compare-forms-core-components.md)：ユーザーは 2 つのフォームを簡単に比較して、その違いを特定できるようになりました。チームメンバーがリビジョンを比較し、変更を効率的に議論できるので、共同作業がスムーズになります。

* [ インタラクティブ通信の Batch API](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel) へのフォントの埋め込みを有効にするサポートが追加されました。インタラクティブ通信では、Batch API を使用して生成されたPDFへのAdobe Ming フォントとAdobe Myungjo フォントの埋め込みがサポートされるようになりました。 この機能強化により、フォントサブセットを使用している場合でも、生成されたドキュメントで正確なテキストレンダリングが確保され、PDF 出力での多言語コンテンツのサポートが向上します。

* [PDFのアクセシビリティに関するコンテンツ API の表 ](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api) - OSGi 上のAEM Formsでは、アクセシビリティ標準のPDFを強化するために、新しい TOC タグ API をサポートするようになりました。 これにより、支援テクノロジーを使用するユーザーが PDF にアクセスしやすくなります。

* [ フラグメント XDP の解決 ](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository) - OSGi 上のAEM Formsは、プライマリ XDP で参照され、AEM CRX リポジトリに保存されたフラグメント XDP を解決するようになりました。

* [PDF/A コンプライアンスの強化 ](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents) - PDFをPDF/A 形式（1a、2a、3a）に変換してアーカイブできるようにすると同時に、アクセシビリティを確保し、これらの標準への準拠を検証できるようになりました。

* **静的PDFドキュメントのフォントの自動サイズ設定のサポート** - AEM Forms Designer、OutputService および FormsService は、静的PDFのフォントの自動サイズ設定をサポートするようになりました。 ユーザーがテキスト、数値、パスワード、日時の各フィールドのフォントサイズを 0 に設定すると、フィールド全体のサイズは変更されずに、これらのフィールド内のフォントサイズが自動調整されます。 この機能を使用するには、ユーザーがカスタム XCI にフラグ `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>` を渡します。

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

### Sites {#sites}

[ユニバーサルエディター](/help/sites-developing/universal-editor/introduction.md)が機能パックの適用により、AEM 6.5 でヘッドレスユースケースに使用できるようになりました。

### [!DNL Assets]

IPTC タブは、[!UICONTROL 代替テキスト]と[!UICONTROL 詳細な説明]テキストフィールドをサポートするようになりました。 （ASSETS-34918）

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## サービスパック 22 で修正された問題 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### アクセシビリティ {#sites-accessibility-6522}

* 注釈スウォッチセレクターボタンに、アクセス可能な名前がありませんでした。つまり、スクリーンリーダーを使用する場合、新しい 16 進数の値を入力した後に選択するボタンには、人間が理解できる名前がありません。（SITES-11992）
* 左側のパネルメニューにある次の要素はリストのように表示されますが、スクリーンリーダーではこのようにマークアップされません。

   * サイト
   * ライブコピー
   * Experience Platform Launch
   * 言語コピー
   * フォルダー
   * CSV レポート（SITES-2874）

* AEM コア web コンテンツ管理には、リッチテキストエディターのハイパーリンクにアクセシビリティラベルが必要です。テキストコンポーネントでハイパーリンクを使用する場合は、アクセシビリティの目的でスクリーンリーダーがリンクテキストを正確に読み取って伝えることができるように、アンカータグに `aria-label` 属性を含める必要があります。（SITES-11511）
* AEM では、リスト表示のテーブルヘッダー内のインタラクティブ要素には、必要な「ボタン」の役割がありません。そのため、NVDA スクリーンリーダーは、タイトル、名前、変更済み、公開済み、プレビュー、テンプレート、操作、ワークフローのテーブルヘッダーに予期されるボタンの役割を通知しません。NVDA などの支援テクノロジーとの互換性を確保するのに、テーブルヘッダー内の各インタラクティブ要素に「ボタン」の役割を割り当てる必要があります。（SITES-10962）


#### 管理者ユーザーインターフェイス{#sites-adminui-6522}

* AEM の一部のインスタンスでは、バージョンプレビューと比較機能が複数のページにわたって期待どおりに動作していませんでした。具体的には以下のとおりです。

   * **プレビューの問題：**&#x200B;ページバージョンをプレビューしようとすると、最初にエラーが表示されます。再試行すると、プレビューに空白のページが表示されます。
   * **バージョン比較の問題：**「現在のバージョンと比較」機能では、バージョン間の違いはハイライト表示されず、現在のバージョンのみが表示されました。（SITES-23988）

* コピー＆ペーストアクション中に `plaintext` に設定された `defaultPasteMode` を使用すると、リッチテキストエディター（RTE）フィールドに予期しない `<br>` タグが表示されます。この問題により、同じコンテンツに対して異なるマークアップが生成され、お客様の翻訳メモリ内で同じテキストコンテンツが 2 回翻訳されることになります。（SITES-23606）
* AEM 6.5.20.0 では、**公開を管理**&#x200B;機能で機能に関する問題が発生しました。ノードを選択し、今後の公開のスケジュールを設定する際、子ノードを含めようとすると、「選択した項目の子リソースを取得できませんでした」というエラーメッセージが表示される場合があります。 この問題により、「**子を含める**」オプションの使用がブロックされ、意図したコンテンツ階層の完全な公開が妨げられていました。（SITES-23000）
* テンプレートがパブリッシュインスタンスに正常に複製されたにもかかわらず、テンプレートの「公開済み」タイムスタンプがオーサー環境で更新されませんでした。予期される動作は、オーサーインスタンスのタイムスタンプが最新の公開を反映することでしたが、この更新は意図したとおりに行われませんでした。（SITES-21585）
* AEM オーサー環境での受信リンクの数に不一致がありました。左側のサイドパネルには、クラシック UI と比較してリンクが少なく表示されました。また、正当な受信リンクの一部が機能しません。（SITES-24837）
* AEM のタイムライン表示でページバージョンを表示すると、読み込み時間が非常に長くなることが報告されていました。バージョンの表示には、最大 19 分かかりました。この問題は、AEM 6.4.8 から 6.5.18 へのアップグレード以降継続しており、ワークフローの効率が大幅に低下していました。（SITES-22468、SITES-22467）

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* アップグレードされた AEM 6.5.17 では、コンテンツフラグメントを保存すると、次のエラーが発生しました：*エラー：コンテンツフラグメントを保存できませんでした。*（SITES-22993）
* AEM のパブリッシャーの `ContentFragmentModelOmniSearchHandler` で、閉じられていないリソースリゾルバーに関する問題が特定されました。（SITES-24903）


#### [!DNL Content Fragments] - 管理者{#sites-admin-6522}

メール通知内のリンクをクリックすると、ユーザーはデフォルトのアセットビューアまたはエディターに移動します。ワークフロー内のアセットがコンテンツフラグメントであると判断された場合でも、コンテンツフラグメントエディターの代わりに、これが実行されます。（SITES-24338）


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6522}

複数行テキストフィールド項目を含むコンテンツフラグメントを使用する場合、GraphQL を使用してクエリを実行する際に生成されるマークアップは、HTML で指定された書式設定を保持していませんでした。例えば、リストの後に改行がなかった場合などです。最後の段落がリストの一部になったことが影響しました。（SITES-23233）


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### コアバックエンド{#sites-core-backend-6522}

* AEM オーサーインスタンスで `SegmentNotFoundException` エラーが繰り返し発生することが報告されました。オーサーを再起動すると問題は一時的に解決しましたが、それ以上の発生を防ぐには長期的な修正が必要でした。（SITES-22573）
* AEM Sites のタイムライン機能に関して、特に注釈の欠落している `cq:lastModified` プロパティの処理に関して問題が発生しました。AEM 6.5.20 を適用した後、既存のコンテンツで欠落しているプロパティを修正する必要があるかどうか、またはタイムラインが更新されてそのプロパティがなくても正しく機能するかどうかについて不確実性がありました。（SITES-21861）


#### コアコンポーネント{#sites-core-components-6522}

* AEM 6.5.18 から 6.5.21 へのアップグレード後、コンポーネントのライブ使用状況を確認する機能に問題が特定されました。ライブ使用状況ページで追加の項目をスクロールしようとすると、UI に「項目をさらに読み込み中」と表示されたにもかかわらず、テーブルにそれ以上の結果を読み込めませんでした。（SITES-23919）
* 2 つのタブを含む AEM コンポーネントダイアログボックスの必須フィールドの検証に関する問題が報告されました。タブ 1 にはリッチテキストエディター（RTE）とテキストフィールドが含まれ、タブ 2 にはパスフィールドとテキストフィールドが含まれていました。すべてのフィールドが必須としてマークされている（`required=true`）にもかかわらず、すべての必須フィールドに入力した後でも、タブ 1 にエラー通知が正しく保持されません。これに対し、タブ 2 のエラーは期待どおりにクリアされました。（SITES-23243）
* AEM 6.5.21 に移行した後、HTML テンプレート言語の `data-sly-include` ステートメントが期待どおりに機能しなくなり、特に `appendPath` 式および `prependPath` 式のサポートができなくなりました。その結果、移行前は正しく動作していたにもかかわらず、含まれているリソースの出力が適切にレンダリングされませんでした。この問題により、パス操作にこれらの式に依存するリソースのレンダリングが失敗しました。（GRANITE-52970）


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### エクスペリエンスフラグメント{#sites-experiencefragments-6522}

* リスト表示で&#x200B;**タイトル**&#x200B;列ヘッダーをクリックしても、エクスペリエンスフラグメントは期待どおりにタイトルで並べ替えられません。画面の素早いちらつきが発生しますが、並べ替えられません。（SITES-23706）

* AEM 6.5.17 では、標準機能を使用してページコンポーネントをエクスペリエンスフラグメントに変換する際に問題が発生しました。変換後、エクスペリエンスフラグメントが使用されているページでは正しく表示されていたにもかかわらず、編集中に空のように見えました。この問題は、ノードの作成が不適切であったことから発生しました。コンポーネントノードがルート／コンテナノードの外部に配置され、テンプレートの構造に違反していました。フラグメントの編集可能性を復元するには、コンポーネントノードを手動で正しいルート／コンテナノードに移動する必要がありました。（SITES-22974）

* AEM 6.5.11 から 6.5.20 に移行した後、エクスペリエンスフラグメントのクラウド設定が正しく保存されませんでした。設定は `crx/de` に保存されているように見えますが、設定コンソールを再度開いても表示されないので、永続性に関する問題が示されます。（SITES-22287）


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### ローンチ{#sites-launches-6522}

AEM 実稼動環境でタグ付けフィルターを使用してエクスペリエンスフラグメントアセットを追加すると、ユーザーは選択できましたが、「**言語コピーを作成**」を選択した後にエラーが発生しました。予想される動作は、タグ付けフィルターから選択したエクスペリエンスフラグメントアセットが翻訳プロジェクトに追加されることになっていたということでした。（SITES-24152）

#### リンクチェッカー{#sites-link-checker-6522}

HTTP クライアントが基本認証の前に NTLM を試行するので、LinkCheckerTask は認証に失敗し、複数回の試行が失敗すると、プロキシがユーザーをブロックします。代わりに、システムではプロキシに対して認証するために基本認証を使用し、LinkCheckerTask サービスが正しく機能できるようにする必要があります。（SITES-25034）


#### MSM - ライブコピー{#sites-msm-live-copies-6522}

* SEO ロボットタグをプライマリコピーに適用し、ライブコピーページにロールアウトすると、値は `crx/de` に正しく表示されました。ただし、ライブコピーページのページプロパティのユーザーインターフェイスには値が反映されませんでした。（SITES-23475）
* ユーザーインターフェイスを通じてローンチを昇格しようとすると、ローンチに関連するエラーが表示されていました。ローンチを昇格ウィザードが空のままだったので、昇格プロセスを完了できませんでした。（SITES-19718）
* ライブコピーを作成してロールアウトを実行しようとした後、AEM のエクスペリエンスフラグメントで問題が発生しました。ユーザーがロールアウト画面からエクスペリエンスフラグメント管理画面に戻ろうとした場合に `NotFound` エラーが発生した際に問題が発生しました。（SITES-21933）


#### ページエディター{#sites-pageeditor-6522}

* 「取り消し」ボタンをクリックすると、テキストが最後のバージョンに変更されるだけでなく、コンポーネントの位置も変更されます。（SITES-17465）
* コピーしたコンテナコンポーネントをペーストすると、視覚的に 2 回表示され、ページ上に 3 つのインスタンスが存在することになります。ただし、ページを更新すると重複が消えたので、この問題は一時的な視覚的な不具合である可能性が高いと考えられます。（SITES-21890）
* キーボードの Tab キーまたは Shift + Tab キーを使用してコンポーネントの左側のパネルを移動している際に、複数のテキスト要素が視覚的にもタブモードでも明確に表示されませんでした。この問題はアクセシビリティに影響し、キーボードナビゲーション中にこれらのコンポーネントを特定または操作することが困難になりました。（SITES-2266）

#### レプリケーション{#sites-replication-6522}

AEM 6.5.18 および 6.5.19 では、親ページを非アクティブ化すると、子ページごとに複数の非アクティブ化リクエストが生成されました。この問題により、GraphQL エンドポイントの一括非公開も機能しなくなりました。（NPR-42075、NPR42010）


### [!DNL Assets]{#assets-6522}

* 接続されたアセット機能を使用している間、AEM Assets で行われた更新は AEM Sites 環境に反映されません。（ASSETS-42344）
* Experience Manager 内のある場所から別の場所にアセットを移動する際に、アセットの公開ステータスに関する問題が発生します。（ASSETS-41158）
* API を使用してアセットをアップロードすると、`unclosed resource resolver` というエラーメッセージが表示されます。（ASSETS-41049）
* Adobe Experience Manager サービスパック 21 にアップグレードした後の `AssetReferenceResolverImpl` 参照クエリに関する問題が発生します。（ASSETS-40384）
* AEM バージョン 6.5.19 では、検索パネルの結果から 1 つのオプションを削除すると、他のすべての使用可能なチェックボックスもオフになります。（ASSETS-37335）
* 一括メタデータ書き出し操作の実行中に、Excel 出力にジャンク値が表示されます。（ASSETS-37260）
* AEM バージョン 6.5.19 では、UTF-8 形式の SVG ファイルをアップロードすると、出力がぼやけます。（ASSETS-36616）
* 接続されたアセット設定内に `Fetch original rendition for Dynamic Media Connected Assets` オプションがありません。（ASSETS-41726）
* 必須フィールドに値を定義しなくても、アセットプロパティは保存されます。（ASSETS-37914）
* アセットの処理ステータスが「失敗」または「メタデータ失敗」の場合、キャプションとオーディオトラックの UI は適切に機能しません。 （ASSETS-37281）
* アセットメタデータを保存して編集しようとすると、言語名が表示されません。 （ASSETS-37281）

#### [!DNL Dynamic Media]{#assets-dm-6522}

Dynamic Media へのビデオのアップロードが失敗し、ユーザーインターフェイスにプロセス失敗エラーが表示されると、実稼動環境の問題により移行プロセスが中断されました。（ASSETS-36038）

<!--

### [!DNL Forms]{#forms-6522}

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.22.0 Forms add-on package release is scheduled for Thursday, November 28, 2024. A list of Forms fixes and enhancements is added to this section post the release.

-->

### Forms {#forms-bug-fixes-sp22}

* AEM Formsに保存されたドラフトの添付ファイル用に生成された URL が、設定された Apache Sling Resource Resolver Factory マッピングを反映していません。 （FORMS-16949）
* AEM Forms Service Pack 19 （6.5.19.0）でユーザーがレターをプレビューすると、スペースが見つからず、文字 `x` が一部の場所に表示されるので、コンテンツが適切に配置されません。 （FORMS-16670）
* AEM Forms サービスパック 18（6.5.18.0）のユーザーが CIFS プロトコルを使用してファイルを印刷しようとすると、次のエラーが発生して失敗します。（FORMS-16629）
  `ALC-OUT-001-401: Unknown error while printing using CIFS on the Printer: \\\\\\\\NSMVPLUETEST01\\\\TH_Test`。
* ユーザーが AEM Forms サービスパック 17（6.5.17.0）から AEM Forms サービスパック 20（6.5.20.0）にアップグレードすると、フォームコンテナレベルでルールエディターアイコンが表示されません。（FORMS-16430）
* ユーザーをAEM Forms サービスパック 17 （6.5.17.0）からAEM Forms サービスパック 21 （6.5.21.0）にアップグレードすると、変更されたアダプティブフォームの送信 URL パスが機能しなくなります。 （FORMS15894）
* AEM Forms サービスパック 19（6.5.19.0）では、AEM Forms 6.5 PDF/A 検証は特定のファイルに対して `creation date and modification date mismatch with timezone` というエラーで失敗しますが、Acrobat Pro PDF/A 検証では準拠性チェックに対してスムーズに実行されます。（FORMS-15840）
* OSGi 上のAEM Forms サービスパック 15 （6.5.15.0）のサイトページで「ドラフトと送信」コンポーネントを使用してフォームドラフトを削除すると、削除が失敗します。 （FORMS-15755）
* ユーザーの SharePoint リストに 999 を超えるエントリがあり、フォームに添付ファイルが含まれている場合、フォームの送信は失敗します。（FORMS-15057）
* 終了日が開始日よりも前にならないように確認する検証ルールと、検証メッセージのカスタムスクリプトが追加されます。 ただし、終了日が開始日より前の場合、検証はトリガーされません。 （FORMS-14757）
* ユーザーがアダプティブフォーム内のテーブルに表示/非表示機能を使用すると、フィールドサイズが縮小します。 行を追加および削除すると、フィールドサイズが自動的に修正されます。（FORMS-14756）
* ユーザーが AEM Forms サービスパック 19（6.5.19.0）でフォームを印刷すると、一部のフォームがサーバー上で正しくレンダリングされず、印刷処理中にエラーが発生します。（FORMS14734）
* AEM Forms サービスパック 15 （6.5.15.0）からサービスパック 19 （6.5.19.0）にアップデートすると、問題が発生します。 `num{$zzz,zz9.99}` として設定されたカスタム表示パターンが、プレビューおよびエージェント UI で正しくレンダリングされない。 （FORMS-14694）
* ユーザーが保存されたデータ XML を使用してインタラクティブなコミュニケーションでレターをプレビューすると、レターは AEM UI で「読み込み中」状態で停止します。同じ XML を使用してレターを再度プレビューすると、正常に機能します。（FORMS-14521）
* AEM Forms サービスパック 20 （6.5.20.0）で、アダプティブフォームの「メールを送信」ボタンを使用して添付ファイル付きのメールを送信すると、問題が発生します。 添付ファイル名がインラインではなく次の行に表示されます。 （FORMS-14426）
* 箇条書きリストがデフォルトの「ディスク」スタイルに設定されたPDFをAEM Formsで生成すると、Adobe Acrobat アクセシビリティツールのアクセシビリティチェックでPDFが失敗します。 「箇条書き」および「正方形」スタイルのリストは、アクセシビリティチェックを通過します。 （FORMS-13802、LC-3922179）
* スタンドアロンの RHEL8 JBoss® セットアップで AEMForms-6.5.0-0065 から AEMForms-6.5.0-0087 にアップグレードすると、LiveCycleサービスコンテナに接続できません。 （FORMS-15907） *
* JEE 上のAEM FormsのAEM Workspaceで、以前に送信したフォームを選択して新しいフォームプロセスを開始すると、問題が発生します。 データが事前入力されたFormsは、以前に送信されたすべてのデータを上書きし、手動で入力されたフィールドを削除します。 （FORMS-15376）
* AEM Forms サービスパック 20（6.5.20.0）で、ユーザーが PDFG サービスを使用して Tiff ファイルを PDF に変換すると、次のエラーが発生して失敗します。（FORMS-14879）ALC-PDG-011-028-入力画像ファイルの PDF への変換中にエラーが発生しました。com/sun/image/codec/jpeg/JPEGCodec
* JEE 上の AEM Forms jar ファイルのアップグレード：`commons-collections:commons-collections:jar` ライブラリが含まれるようになり、次のような様々な AEM Forms JEE ジョブでの依存関係の解決と機能が向上しました。
   * ジョブ処理とエラー処理を改善する Assembler ジョブの機能強化。
   * ドキュメントの生成と変換の操作をよりスムーズにする PDF Generator（PDFG）ジョブの機能強化。
   * バージョン間の安定した移行を確保しながらアップグレードプロセスを改善する LC-Upgrade ジョブの機能強化。
   * ドキュメント処理のセキュリティを確保し、Rights Management機能を向上させるためのRights Managementジョブの強化。
   * より信頼性の高いジョブ処理とシステム管理を実現する Process Management ジョブの機能強化。


#### XMLFM {#forms-xmlfm-sp22}

* AEM Forms サービスパック 21（6.5.21.0）では、ユーザーが XMLFM を使用して PDF に非標準のタグを追加すると、ドキュメントが PDF 仕様の要件に準拠しなくなります。（LC-3922484）
* ユーザーが AEM Forms サービスパック 20（6.5.20.0）の Output サービスを使用して PDF を生成すると、CORBA.COMM_FAILURE で失敗し、`15:04:35,973 ERROR [com.adobe.formServer.PA.XMLFormAgentWrapper] (default task-14) ALCOUT-002-013: XMLFormFactory, PAexecute failure: "org.omg.CORBA.COMM_FAILURE"` というエラーが表示されます。アクセシビリティの役割「参照」が XDP テンプレートのサブフォームから除外されると、サービスは正常に渡されます。 ただし、この役割は 508 準拠に必要です。（LC-3922402）
* ユーザーが XFA フォームを AcroForm PDF に変換すると、失敗します。（LC-3922363）
* AEM Forms サービスパック 19（6.5.19.0）では、ユーザーが名前のないサブフォームを含む XDP を作成すると、名前のないサブフォームの FS_DATA_SOM は空として表示されます。（LC-3922034）

#### Forms Designer {#forms-designer-sp22}

* ユーザーが AEM Forms Designer バージョン 6.5.21.0 でフラグメントフォルダーを選択してフラグメントライブラリを開くと、クラッシュします。（LC-3922439）
* ユーザーが 32 ビット版 AEM Forms Designer バージョン 6.5.20.0 をアンインストールし、AEM Forms Designer バージョン 6.5.21.0 をインストールすると、Forms Designer は起動に失敗します。エラーログには、Java ランタイム環境（JRE）のメモリ割り当てが不十分であることが示されます。（LC-3922404）
* ユーザーが AEM Forms Designer バージョン 6.5.20.0 をインストールした後、メニューに「マクロ」オプションが表示されず、デフォルトの「アクセシビリティチェッカー」マクロのみが表示され、実行に失敗します。（LC-3922321）
* ユーザーが AEM Forms Designer バージョン 6.5.20.0 で XDP の作成に新しいテンプレートの場所を追加すると、Forms Designer がクラッシュします。（LC-3922316）
* AEM Forms 6.5 サービスパック 15 （6.5.15.0） OSGI で、ExportData メソッドを使用して出力を生成すると、不完全で誤ったデータが生成されます。 （LC-3922340）


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### 基盤 {#foundation-6522}

AEM Assets コンソールで、DITA ドキュメントを並べ替えようとする際に問題が発生しました。パスブラウザーダイアログボックスの上部にあるパンくずリストに、ルートの親のノードタイトルではなくノード名が誤って表示されます。正しいノードタイトルは、パンくずリスト内の項目を選択した後にのみ表示され、一時的な表示エラーを示します。（NPR-42106）


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### Communities {#foundation-communities-6522}

AEM 6.5.19 から 6.5.20 にアップグレードした後、`UgcSearch` の呼び出し後に `Connection evic` スレッドが適切に閉じられないという問題が発生しました。実稼動環境で確認されたこの問題により、これらのスレッドが時間の経過と共に持続して蓄積され、パフォーマンスに影響を与える可能性があります。（NPR-42019）


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* CRX パッケージマネージャーの左側のサイドメニューの&#x200B;**グループ**&#x200B;に従って並べ替えが機能していませんでした。（GRANITE-53277）
* AEM のパッケージマネージャーは、デフォルトで下位バージョンのパッケージのインストールを制限しますが、古いバージョンの強制インストールは許可します。ただし、強制インストールオプションを使用すると、標準パイプラインを通じた今後のインストールが妨げられる可能性があります。例えば、バージョン 1.21 をインストールし、バージョン 1.24 を追加した場合、インストールは成功し、両方のバージョンがリストされます。ただし、バージョン 1.24 を上書きしてバージョン 1.22 をインストールしようとするとパイプラインを通じて失敗しますが、強制インストールを行うとすべてのバージョンがリストされます。同様に、パイプラインではダウングレードが許可されないので、バージョン 1.24 が既に存在する場合はバージョン 1.23 のインストールがブロックされます。（GRANITE-53263）


#### Granite{#foundation-granite-6522}

* スナップショットパッケージは、cURL コマンドを使用して AEM にインストールされていました。インストール中に、JCR インストーラーは OSGi インストーラーを通じてパッケージをスキャンし、追加の OSGi バンドルまたは設定が必要ないことを確認しました。パッケージバージョンに「スナップショット」が含まれている場合、OSGi インストーラーは VLT をトリガーして対応するスナップショットパッケージを作成します。ただし、各 AEM オーサーインスタンスは独自の OSGi インストーラーを実行するので、両方のインスタンスが同時にスナップショットを生成しようとし、リポジトリ内でセッションの競合が発生する場合があります。（NPR-42003）
* AEM 6.5.21 では、`ScriptDependencyResolver` にロックの競合が存在していました。（GRANITE-53181）
* AEM を 6.5.21 にアップグレードした後、`data-sly-use` などの相対パスを Sightly（HTL）構文で使用した際に問題が発生しました。（GRANITE-53080）


#### 統合{#foundation-integrations-6522}

* Cloud Services ユーザーインターフェイスに法的帰属に関するステートメントが追加されました。（FORMS-16373）
* **fd-cloudservice** ユーザーが hCaptcha および Turnstile 設定にアクセスするための読み取り権限を追加し、Captcha のレンダリングと検証に必要なクライアント ID とクライアント秘密鍵を取得できるようになりました。さらに、これらの設定へのアクセス権を管理するために、アクセス制御リストモデルが実装されました。（FORMS-16360）


#### ローカライゼーション{#foundation-localization-6522}

![ハンマーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) ツール／**セキュリティ**／![ユーザーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **ユーザー**&#x200B;のユーザー管理ページで、テーブルの&#x200B;**ステータス**&#x200B;列のデータが垂直に表示されていました。（GRANITE-48304）


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### プラットフォーム{#foundation-platform-6522}

* AEM 6.5.18 で導入されたエンタープライズ情報管理トラッキングにより、製品採用スコアの計算に異常が発生しました。アドビ指標ライブラリが Omega トラッキングライブラリによって提供されたユーザーデータを上書きすることで、この問題が発生しました。その結果、2024年2月以降、多くの AEM Sites および AEM Assets のお客様の採用スコアがゼロに低下しました。（CQ-4358438）
* 実稼動環境で、ガベージコレクターによるタグの処理が不適切に行われるという重大な問題が特定されました。具体的には、タグを移動または名前変更する際、ガベージコレクターが `cq:MovedTo` プロパティを更新できず、タグがページから消えてしまいます。（CQ-4358293）
* AEM 6.5.19 の ContextHub の問題により、コンテキストパスを AEM インスタンスに追加した際にセグメントが正しく解決されませんでした。この問題は、ページコンポーネントによって生成された JavaScript オブジェクト内の URL フィールドに特に影響し、必要なコンテキストパスプレフィックスが欠落していました。この省略により、セグメントが期待どおりに機能しなくなりました。（SITES-21852）
* AEM クイックスタートを更新し、ライブラリ `commons-collections-3.2.2-adobe-2` を使用するようにしました。この更新により、アプリケーションは引き続きスムーズに実行できるようになります。（NPR-42150）
* AEM 6.5 の SMTP OAuth2 設定は、AEM as a Cloud Service で使用する設定とは大きく異なります。設定を効率化し、一貫性を確保するために、AEM 6.5 の設定を AEM as a Cloud Service で使用する標準に合わせる必要がありました。（GRANITE-53273）
* ![コンパスアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg)／![プロジェクトアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg) プロジェクトをクリックし、マウスポインタを ![左パネルアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![山形下向き](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) アイコンの上に合わせると、ツールチップテキスト「コンテンツのみ」の前に抑音符号が表示されるという問題が見つかりました。（CQ-4356633）

#### セキュリティ{#foundation-security-6522}

* AEM の古い JSAFE 暗号化ライブラリ（バージョン 6.0.0）で問題が発生しました。AEM 6.5.22 には、JSAFE バージョン 6.2.5 のパッチ適用バンドルが含まれています。（NPR-42006）
* XSS チェック中に許可されたプロトコルを検証する際、ハンドラーは「http」と「https」を比較します。ただし、URL オブジェクトの `protocol` プロパティは、`http:` や `https:` のように末尾にコロンが付いた値を返しました。この不一致により、検証の問題が発生しました。正確な解析を確実に行うには、プロトコルチェックでコロンを考慮するか、それに応じて比較ロジックを調整する必要がありました。（NPR-42119）
* IBM® WebSphere® Liberty プロファイルおよび Semeru Java 8.0 に AEM 6.5.21（以前のバージョンは AEM 6.5.19）をインストールした後、ページを開くことができませんでした。エラーログには、異なるバンドルに必要なサーブレットバージョンに関連する問題が示されていました。この問題に対処するには、問題に関連している `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` への依存関係を元に戻す必要がありました。（NPR-42116）
* いくつかのブラウザーでは、Cookie へのクロスサイトアクセスを許可するのに使用される **SameSite=None Cookie** のサポートが段階的に廃止されています。代替として、**パーティション分割された Cookie** が導入されています。これらの Cookie は、使用されるコンテキストによってストレージを分離し、サイト間のトラッキングを防ぎながら、埋め込みサードパーティコンテンツなどの特定のパーティション内で Cookie が機能できるようにすることで、プライバシーとセキュリティを強化します。（GRANITE-51953）


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### 翻訳{#foundation-translation-6522}

* コアコンポーネントの最近の変更に対するサポートをデフォルトの翻訳ルールに追加しました。（NPR-42029）
* AEM Forms での XLIFF ファイルの書き出しに関する問題が特定されました。「**選択対象を XLIFF として書き出し（文字列のみ）**」オプションを使用すると、コンポーネントのシーケンスが一貫して維持されませんでした。ただし、特定の言語の XLIFF を書き出す場合、シーケンスは正しいままです。この問題を示すために、**DE-CH_Export.xliff**（正しいシーケンス）と **String_Export.xliff**（正しくないシーケンス）の 2 つのファイルが提供されました。（NPR-42118）


#### ユーザーインターフェイス{#foundation-ui-6522}

* `coralui-component-dialog` は、`cq-dialog-actions` の配置を変更し、AEM のダイアログボックス内のアクションボタンのレイアウトや動作に影響を与える可能性がありました。（NPR-42294）
* AEM のカラーピッカー機能に不具合が発生していました。アクセスすると、空白のモーダルが表示され、カラー選択ができなくなりました。この問題は、ステージ環境に AEM 6.5.20 をインストールした後に発生しました。カラーピッカーは、更新&#x200B;*前*&#x200B;は正しく動作していました。（NPR-42163）
* ![ハンマーアイコン](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **ツール**／**ワークフロー**／**モデル**／任意のモデルを選択／**ワークフローを開始**&#x200B;で、**ワークフローを実行**&#x200B;ダイアログボックスの「ペイロード」フィールドに「参照」アイコンが表示されませんでした。（NPR-42162）


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A -->


## [!DNL Experience Manager] 6.5.22.0 のインストール{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0 には [!DNL Experience Manager] 6.5 が必要です。手順について詳しくは、[アップグレードに関するドキュメント](/help/sites-deploying/upgrade.md)を参照してください。<!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.22.0 をインストールします。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.22.0 パッケージを削除またはアンインストールすることを推奨しません。したがって、パッケージをインストールする前に、ロールバックする必要がある場合に備えて `crx-repository` のバックアップを作成する必要があります。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### [!DNL Experience Manager] 6.5 へのサービスパックのインストール{#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip)からサービスパックをダウンロードします。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、**[!UICONTROL パッケージをアップロード]**&#x200B;を選択して、パッケージをアップロードします。 詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、**[!UICONTROL インストール]**&#x200B;を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。 [Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログボックスが終了することがあります。アドビでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.22.0 のインストール方法は 2 つあります。<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。 パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。 ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.22.0 では、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

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

[!DNL Experience Manager] 6.5.22.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/)で入手できます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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

* コンテンツフラグメント - 大きなフラグメントツリーに対する DoS 保護が原因でプレビューに失敗します。詳しくは、[GraphQL Query Executor のデフォルト設定オプションに関するナレッジベース記事](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-23945)（SITES-17934）を参照してください。


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

* ユーザーが AEM 6.5 Forms サービスパック 18 または 19 からサービスパック 20 または 21 にアップグレードした際、JSP コンパイルエラーが発生しました。このエラーにより、アダプティブフォームを開いたり、作成したりすることができませんでした。また、他の AEM インターフェイスでも問題が発生しました。これらのインターフェイスには、ページエディター、AEM Forms UI、ワークフローエディター、システム概要 UI が含まれていました。（FORMS-15256）

  このような問題が発生した場合は、次の手順を実行して解決します。
   1. CRXDE のディレクトリ `/libs/fd/aemforms/install/` に移動します。
   1. `com.adobe.granite.ui.commons-5.10.26.jar` という名前のバンドルを削除します。
   1. AEM サーバーを再起動します。

* Forms アドオンを使用して AEM Forms サービスパック 20（6.5.20.0）にアップデートすると、資格情報に基づく認証を使用する従来の Adobe Analytics Cloud Service に依存する設定が機能しなくなります。この問題により、分析ルールが正しく実行されなくなりました。ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （FORMS-15428）

* ユーザーが JEE サーバー上で AEM Forms サービスパック 20（6.5.20.0）に更新し、Output サービスを使用して PDF を生成すると、PDF がアクセシビリティに関する問題を伴ってレンダリングされます。ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。（LC-3922112）
* ユーザーが JEE 上の Output サービスを使用してタグ付き PDF を生成すると、「不適切な構造の警告」が表示されます。ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （LC-3922038）
* AEM Forms JEE でフォームを送信すると、繰り返し XML 要素のインスタンスがデータから削除されます。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （LC-3922017）
* Linux® 環境のユーザーがアダプティブフォーム（JEE 上）を HTML でレンダリングすると、正しくレンダリングされません。ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （LC-3921957）
* ユーザーが AEM Forms JEE の Output サービスを使用して XTG ファイルを PostScript 形式に変換する際に、エラー `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE` が発生して失敗します。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （LC-3921720）
* JEE サーバーで AEM Forms サービスパック 18（6.5.18.0）にアップグレードした後、ユーザーがフォームを送信すると、HTML5 または PDF フォームのレンダリングに失敗し、XMLFM がクラッシュします。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （LC-3921718）
* インタラクティブ通信エージェント UI の印刷プレビューでは、すべてのフィールド値に通貨記号（ドル記号 $ など）が一貫して表示されません。999 までの値の場合は表示されますが、1000 以上の値の場合は表示されません。（FORMS-16557）
* インタラクティブ通信内でネストされたレイアウトフラグメントの XDP に対する変更は、IC エディターに反映されません。（FORMS-16575）
* インタラクティブ通信エージェント UI の印刷プレビューでは、一部の計算値が正しく表示されません。（FORMS-16603）
* 印刷プレビューでレターを表示すると、コンテンツが変更されます。つまり、いくつかのスペースが消え、特定の文字が `x` に置き換えられます。 （FORMS-15681）
* ユーザーが WebLogic 14c インスタンスを設定すると、JBoss® で動作している JEE 上のAEM Forms サービスパック 21 （6.5.21.0）での PDFG サービスが、SLF4J ライブラリを含んだクラスローダーの競合が原因で失敗します。 エラーは次のように表示されます。（CQDOC-22178）：

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature
  ```

## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、この [!DNL Experience Manager] 6.5 サービスパックリリースに含まれている OSGi バンドルとコンテンツパッケージのリストが記載されています。

* [Experience Manager 6.5.22.0 に含まれている OSGi バンドルのリスト](/help/release-notes/assets/65220-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.22.0 に含まれているコンテンツパッケージのリスト](/help/release-notes/assets/65220-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/ja/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-65)
>* [アドビ製品アップデートの優先通知を購読](https://www.adobe.com/subscription/priority-product-update.html)
