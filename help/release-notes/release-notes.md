---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: dbee0e382bad460746416dac5206843ed67bdf04
workflow-type: tm+mt
source-wordcount: '6515'
ht-degree: 77%

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

## 主な機能および機能強化

<!--### Sites {#sites}

* A () -->

<!--
### [!DNL Assets]

* A ()
-->

### Forms {#forms-sp23}

このリリースの主な機能と機能強化は次のとおりです。

* [ 静的 PDF で混在テキストスタイルを含むアクセシブルなハイパーリンク ](https://helpx.adobe.com/content/dam/help/ja/experience-manager/6-5/forms/pdf/using-designer.pdf)：静的 PDF で混在テキストスタイルを含むハイパーリンクが、単一のアクセシブルな要素としてタグ付けされるようになりました。 この機能強化により、タグツリー構造が簡素化され、スクリーンリーダーのナビゲーションが改善され、アクセシビリティコンプライアンスが向上しています。

* [ 更新されたサポートされているプラットフォームのマトリックス ](/help/forms/using/aem-forms-jee-supported-platforms.md)

  最新バージョンでは、サポートされているプラットフォームマトリックスが更新され、新しいテクノロジーとの互換性が確保されています。

   * IBM Content Manager クライアント 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Microsoft® SQL Server JDBC ドライバー 12.8

   * Red Hat® Enterprise Linux® 9 （Kernel 4.x、64 ビット） 

* [ 強化されたファイル添付コンポーネント ](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment)：セキュリティ対策として、許可されたファイルタイプのチェックを回避しようとする拡張子が変更されたファイルの送信をコンポーネントが防ぐようになりました。 このようなファイルは、有効なファイルタイプのみが受け入れられるように、送信時にブロックされます。

<!--* **Two-Factor authentication with SAML for AdminUI** 

  AdminUI in AEM Forms JEE now supports two-factor authentication using Security Assertion Markup Language (SAML) single sign-on (SSO), providing stronger security and a seamless login experience for administrators, similar to what is available in HTML Workspace. 

#### New GA features in AEM Forms {#ga-aem-forms-sp23}

* A ()

#### New Beta features in AEM Forms {#beta-aem-forms-sp23}
-->

## サービスパック 23 で修正された問題 {#fixed-issues}

<!-- 6.5.23.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

### [!DNL Sites]{#sites-6523}

#### アクセシビリティ {#sites-accessibility-6523}

* AEM エディターページのキャンバスセクションで、完全なキーボードアクセシビリティがサポートされるようになりました。ユーザーは、マウスポインタを使用せずに、キーボードのみを使用して、セクションタイトルをアクティベートし、ボタンを編集できます。このアップデートでは、WCAG 2.1.1 への準拠を確保し、ティーザー、画像、カルーセル、レイアウト、タイムワープ、注釈モーダルなど様々なコンポーネントでの操作性が向上します。（SITES-25256）<!-- 6.5 LTS SP1 -->
* AEM ページエディターでペルソナ、買い物かご、中断などのボタンをアクティベートした後に、キーボードのフォーカスがデ予期せずモグラフィックツールバーの先頭へとリセットされる、アクセシビリティの問題を修正しました。アクティベートされたボタンへのフォーカスを維持し、一貫したキーボードナビゲーションとスクリーンリーダーのワークフローをサポートできるようになりました。（SITES-25306）
* AEM ページエディターで、複数のダイアログボックスおよびモーダル（アセットパネルやレイアウトプレビューなど）のキャンバス要素をキーボードだけで操作できないという、アクセシビリティに関する重大な問題を修正しました。すべてのインタラクティブキャンバス要素で、キーボードのみのナビゲーションがサポートされ、WCAG 2.1 達成基準 2.1.1 に準拠できるようになりました（SITE-25256）
* Sites 管理 UI の「作成」ポップアップのインタラクティブリスト項目で、誤った ARIA の役割が使用されるアクセシビリティの問題を修正しました。リンクのように動作する要素が `role="menuitem"` ではなく `role="listitem"` に割り当てられ、ARIA のデザインパターンに違反し、スクリーンリーダーの混乱を招いていました。こアップデートのにより、すべてのリストコンポーネントが適切なセマンティックの役割に従うようになり、キーボードと支援テクノロジーのサポートが向上します。（SITES-24493）
* ページタイトルおよびタグフィールドのアクセシビリティラベルの関連付けに関する問題を修正しました。JAWS などのスクリーンリーダーを使用する際、AEM インターフェイスで、アクセシビリティラベルが「タイトル」フィールドと「ページタイトル」フィールドに正しく関連付けられるようになりました。この修正により、ラベルが適切に読み取られ、ページの作成、プロパティ、移動ワークフロー全体で ADA コンプライアンスが向上します。（SITES-27149）
* 権限ダイアログボックスにおけるテーブル識別に関するアクセシビリティの問題を修正しました。AEM の権限テーブルで正しい ARIA ロールと属性が使用されるようになり、JAWS などのスクリーンリーダーで、これらがテーブルとして適切に識別されるようになりました。この修正により、アクセシビリティコンプライアンスが向上し、ユーザーは正確なナビゲーションやコンテンツのお知らせを受け取れるようになります。（SITES-27140）
* タイムラインのコメント入力フィールドで、欠落している表示ラベルを修正しました。アクセシビリティを向上させるために、「タイムライン」セクションの「コメント」入力フィールドで、欠落している表示ラベルを修正しました。このアップデートにより、スクリーンリーダーがフィールドラベルを正確に読み上げられるようになりました。このエクスペリエンスにより、すべてのユーザー（特に支援テクノロジーに依存するユーザー）のフォームのナビゲーションと送信を強化します。（SITES-26903）
* タイムラインコメントにおける省略記号ボタンのキーボードアクセシビリティを修正しました。「タイムライン」セクションで、コメントの横にある省略記号（3 つのドット）ボタンのキーボードナビゲーションを有効にしました。ユーザーは Tab キーを使用してボタンへのアクセスや操作ができるようになり、キーボードのみを使用したナビゲーションに依存するユーザーのアクセシビリティが向上します。（SITES-26891）
* 選択ダイアログボックスでの検索結果に対する NVDA／ナレーターのお知らせを改善しました。NVDA やナレーターなどのスクリーンリーダーを使用する際に、検索結果が見つかったかどうかを通知するように、「選択を開く」ダイアログボックスをアップデートしました。この改善により、支援テクノロジーに依存しているユーザーは、視覚的に確認しなくても検索アクションの結果を理解できるようになります。（SITES-26883）
* コメント入力フィールドの横にある省略記号アイコンの ARIA 役割を修正しました。正しい ARIA の役割を使用するように、コメント入力フィールドの横にある省略記号（3 つのドット）アイコンをアップデートし、スクリーンリーダーが要素を正確に識別できるようにしました。この改善により、アクセシビリティコンプライアンスが強化され、支援テクノロジーに依存するユーザーのエクスペリエンスが向上します。（SITES-26881）
* Coral UI コンポーネントの無効な ARIA 属性を修正しました。すべての ARIA 属性が有効な値を使用するように Coral UI コンポーネントをアップデートし、アクセシビリティコンプライアンスを向上させました。具体的には、`aria-modal="dialog"` のような無効な値が誤って割り当てられているケースに対処しました。この機能強化により、スクリーンリーダーでダイアログボックス要素が正しく解釈されるようになり、支援テクノロジーに依存するユーザーのアクセシビリティが向上します。（SITES-26873）
* リフローシナリオでのアイコンの表示とツールチップを改善しました。リフロー動作が強化され、**ダウンロード**、**アセットを再処理**&#x200B;および&#x200B;**チェックアウト**&#x200B;アイコンのツールチップが正しく表示されるようになりました。ビューポートのサイズ変更やブラウザーのズーム設定を変更すると、アイコンとそのラベルが非表示になるアクセシビリティの問題に焦点を当てました。この修正により、視力の低いユーザーをサポートするために、表示が維持され、リフロー中に適切なアイコンの説明が表示されるようになりました。（SITES-26871）

#### 管理者ユーザーインターフェイス{#sites-adminui-6523}

Externalizer エンドポイントがない、ユニバーサルエディター URL サービスの例外を修正しました。ユニバーサルエディターの URL サービスで、例外をスローせずに、オーサー、パブリッシュまたはローカルの Externalizer エンドポイントの欠落を処理できるようになりました。管理者ユーザーは、一部の Externalizer 設定が不完全な場合でも、ページエディターを正常に開くことができます。（SITES-28877）<!-- LTS -->

#### クラシック UI{#sites-classicui-6523}

* クラシック UI のダイアログボックスで、ボタンを切り替えるとテキスト領域が非表示になり、その後にクリックしても再度表示できない問題。この修正では、切り替え時にテキスト領域が適切に再表示されるようになりました。これにより、期待される動作を復元し、動的ダイアログボックスのワークフローが中断されるのを防ぎます。（SITES-30230）
* Service Pack 22 へのアップグレード後に、クラシック UI の画像アセットファインダー機能が壊れる問題を修正しました。クラシック UI 画像アセットファインダーで、スペースや特殊文字を含むアセット名が適切に処理されるようになりました。この更新により、アセットファインダーでファイル名が正しくエンコードされ、検索の失敗を防止し、作成者がエラーなしで画像アセットを見つけて選択できるようになります。（SITES-29151）

#### [!DNL Content Fragments]{#sites-contentfragments-6523}

* `DeleteVariationIT.testUpdateBasic` の検証テストの失敗を修正しました。サービスパックの検証の実行中に、`DeleteVariationIT.testUpdateBasic` テストが失敗しなくなりました。この修正により、JSON 処理ロジックで欠落しているテキストマッピングの問題が解決し、テストの安定性が確保され、不要なテストの中断が回避されます。（SITES-28022）
* AEM は、画像アセットの XMP メタデータの形式が正しくないことに起因するパフォーマンスの低下を防ぐことができるようになりました。数値セグメントや不適格な構造など、無効または準拠していないXMP プロパティ名を含むアセットで、処理中に警告ログが繰り返しトリガーされなくなりました。システムは、問題のあるメタデータを除外して、アセットの取り込みと検証がエラーなく完了できるようにします。（SITES-30683）<!-- AEM 6.5 LTS SP1 -->


<!-- #### [!DNL Content Fragments] - Admin{#sites-admin-6523}

* A () -->


#### [!DNL Content Fragments] - フラグメントエディター{#sites-fragments-editor-6523}

作成者がコンテンツフラグメントをチェックアウトした場合でも、他の作成者が引き続きコンテンツフラグメントを公開できます。これは、チェックアウト機能の意図した動作と反しています。この修正により、コンテンツフラグメントがチェックアウトされると、他のユーザーはオーサリングインターフェイスの「公開」ボタンを表示または使用できなくなります。（SITES-30578）<!-- LTS -->

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6523}

コンテンツフラグメントスキーマでの GraphQL QueryValidationError を修正しました。`cq-dam-cfm-graphql` バンドルを更新すると、コンテンツフラグメント参照を使用する際のスキーマ検証エラーが修正されます。この修正により、パッケージのデプロイメントの後に、手動でスキーマの再整列や再公開を行わなくても、GraphQL クエリの関数が正しく機能するようになります。（SITES-27001）<!-- LTS -->


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6523}

* A () -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6523}

* A () -->


#### コンポーネントコンソール{#sites-component-console-6523}

「コンポーネントのライブ使用状況」ページの読み込みを改善しました。AEMの「コンポーネントのライブ使用状況」ページを最適化して、大規模なデータセットをスクロールしたときに空の行が表示されないようにします。ユーザーが使用状況の参照範囲が非常に広いコンポーネントを読み込む際、不要なギャップや空のエントリが入ることなく連続でデータを読み込めるようになりました。このエクスペリエンスにより、コンポーネントの使用状況レポート全体でページナビゲーション、トラッキングの精度、管理効率が向上します。（SITES-26454）

#### コアバックエンド{#sites-core-backend-6523}

* 無効なアセット名が原因で発生していた、コンテンツファインダーアセットのリスト表示の失敗を修正しました。コンテンツファインダーで、エンコードできない文字を使用したアセット名が正しく処理されるようになりました。ページエディターのアセットリストで、問題のある名前のアセットが検出されても、失敗したり例外がスローされたりすることがなくなりました。（SITES-28722）
* `SearchPathLimiter` コンポーネントで、呼び出しごとに「エラー」レベルでメッセージが出力され、過剰なログエントリが生成されていた問題。この動作は Service Pack 17 以降に始まり、膨大なログに起因するパフォーマンス上の懸念が生じていました。この修正により、ログレベルが「デバッグ」にダウングレードされ、ログノイズが大幅に減少し、システムの監視と診断効率が向上します。（SITES-29835）
* XMP メタデータの形式が不適切であったため、`ValidationDataServlet` の画像アセットの処理中にエラーが発生していました。この修正により、準拠メタデータが処理され、無効なプロパティの冗長な解析が回避されます。（SITE-30683）<!-- LTS -->


<!-- #### Core Components{#sites-core-components-6523}

* A () -->

<!-- #### Campaign integration{#sites-campaign-integration-6523}

* A () -->

<!-- #### Experience Fragments{#sites-experiencefragments-6523}

* A () -->

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6523}

* A () -->


#### ローンチ{#sites-launches-6523}

* 12月25日（PT）から 12月31日（PT）の間の不正確な開始日の表示を修正しました。ローンチ UI に、12月25日（PT）から 12月31日（PT）の間の日付と正しい年が表示されるようになりました。この修正により、日付とともに誤って次の年が表示されなくなり、キャンペーンの計画およびスケジュール設定時の混乱が回避されます。（SITES-28706）
* サービスパック 22 のアップグレード後に、AEM Launch のテンプレートが壊れる問題を修正しました。サービスパック 22 のアップグレード後に、AEM Launch テンプレートが正しく読み込まれるようになりました。この修正により、内部ローンチ設定の無効なデータが修正され、ユーザーはエラーやフィールドの欠落なしでローンチを表示、編集および作成できるようになります。（SITES-28504）


<!-- #### Link Checker{#sites-link-checker-6523}

* A () -->

<!-- #### MSM - Live Copies{#sites-msm-live-copies-6523}

* A () -->


#### ページエディター{#sites-pageeditor-6523}

* 低画面解像度での AssetPicker の読み込みの問題を修正しました。ユーザーが低画面解像度（1728×1117 以下）でスクロールした場合、AssetPicker がアセットを正しく読み込むようになりました。スクロール中にアセットが欠落することがなくなり、異なるデバイスのブレークポイントをまたいだアセット管理が向上しました。（SITES-28065）
* ページのロックおよびロック解除アクションに関し、スクリーンリーダーの通知が行われない問題を修正しました。ユーザーがロック／ロック解除ボタンをアクティベートすると、ページエディターで「情報：ページがロック／ロック解除されました」というメッセージが適切に通知されるようになりました。この修正により、アクセシビリティコンプライアンスが向上し、スクリーンリーダーのユーザーはページの編集中に動的更新を受け取れるようになります。（SITES-27143）
* AEM オーサリングにおけるコンポーネントアクションのキーボードフォーカスの動作を改善しました。AEM オーサーツールのキーボードナビゲーションが強化され、設定、削除、変換などのアクションの後に、新しく作成または選択したコンポーネントにフォーカスが残るようになりました。以前は、フォーカスがページの上部に移動し、アクセシビリティコンプライアンスの問題が発生していました。このアップデートにより、キーボードおよび支援テクノロジーのユーザーのユーザーエクスペリエンスが向上します。具体的には、編集ワークフロー内で論理的なフォーカスの進捗を維持する改善が行われました。（SITES-26549）
* オーサーダイアログボックスのタブナビゲーションを改善しました。ユーザーが「説明」編集ボックスからタブ順序で前方に移動できるようにすることで、AEM のオーサーダイアログボックスのキーボードナビゲーションを強化しました。以前は、「説明」フィールドでのフォーカストラップにより、それ以降のナビゲーションを行うには、特別なキーの組み合わせを使用する必要がありました。このアップデートにより、ユーザーが Tab キーのみを使用してフィールドをシームレスに移動できるようになり、アクセシビリティコンプライアンスとユーザーエクスペリエンスが向上します。（SITES-26524）
* AEM 6.5 Service Pack 22 で、ローンチタイトルにスペースを含めることができない回帰が導入されました。この修正により、スペースを使用する機能が復元され、チームは期待される動作に合わせて、ローンチ名をより柔軟に定義および整理できるようになります。（SITES-29414）
* 非表示／非表示した後のレイアウトコンテナ内のコンポーネントのサイズ変更の問題を修正しました。レイアウトコンテナを非表示または再表示した後に、ページエディターで列の値が適切に計算されるようになりました。ユーザーはエラーなしでコンポーネントのサイズを変更でき、サイズ変更の操作中に列が正しく表示されます。（SITES-28463）
* ページエディターのコンテンツツリーボタンの配置の誤りを修正しました。ページエディターで、「コンテンツツリー」設定ボタンが誤ったセクションではなく、意図された「ヘッドティーザー」ダイアログボックスの下に正しく配置されるようになりました。この修正により、コンテンツツリーのダイアログボックスの CSS が更新され、`bottom:0` ではなく `top:0` が使用され、ボタンが適切に配置されました。（SITES-28448）


<!-- #### Replication{#sites-replication-6523}

* A () -->


#### リッチテキストエディター{#sites-rte-6523}

平文貼り付けモードを使用したリッチテキストエディターの予期しない `<br>` タグを修正しました。リッチテキストエディターで平文 `defaultPasteMode` を使用するときに、切り取りと貼り付けの操作が正しく処理されるようになりました。この修正により、ユーザーが RTE フィールド内でテキストを切り取って貼り付ける際に、予期しない `<br>` タグが挿入されるのを防ぎ、コンテンツ編集中にクリーンな書式が維持されます。（SITES-27780）

#### ユニバーサルエディター {#sites-universal-editor-6523}

* クエリパラメーターを含む複数のリクエストが AEM に送信されると、login-token cookie が時間内に返されず、ログインに失敗する可能性があります。（SITES-30659） <!-- LTS -->
* SAML ハンドラーとの互換性とサポートを確保するには、`Query Token Auth` ハンドラーが `SAML Auth` ハンドラーの *前* に実行されるように `service.ranking` プロパティを設定する必要があります。（SITES-29684）

### [!DNL Assets]{#assets-6523}

* [!DNL AEM] オンプレミス（6.5.22.0）のナビゲーションページで、![アセット](/help/assets/assets/Smock_Asset_18_N.svg)**[!UICONTROL アセット&#x200B;]**&#x200B;を選択し、**[!UICONTROL &#x200B; Adobe Stock を検索&#x200B;]**&#x200B;フォルダーに移動してストック画像を選択すると、以下の問題が発生します。
   * 「**[!UICONTROL ライセンスと保存]**」をクリックすると空のドロップダウンが表示されるため、選択したストック画像のライセンスを取得して保存することができません。
   * ストック画像を選択するか、ストックページの URL を再入力すると、[!DNL AEM] ホームページにリダイレクトされ、Adobe Stock 画像にアクセスできなくなります。（ASSETS-48687）
* [!DNL AEM]オンプレミス（6.5.22.0）ナビゲーションページでフォルダーの名前に `/` が含まれる場合、フォルダーの管理中に問題が発生します。（ASSETS-46740）
* [!DNL AEM] 6.5 では、メモリ使用量が多いため、アセットの詳細ページが ![ コレクション ](/help/assets/assets/Smock_Collection_18_N.svg)**[!UICONTROL &#x200B; コレクション&#x200B;]**&#x200B;ビューから読み込まれません。（ASSETS-46738）
* `Day CQ DAM Mime Type OSGI` Service としての [!DNL InDesign] との統合の問題によって、[!DNL InDesign] ファイルが `x-indesign` ではなく `x-adobe-indesign` と誤って認識されます。（ASSETS-45953）
* [!DNL AEM 6.5.21] セッション リークが、標準提供の **[!UICONTROL Brand Portal へのスケジュールされた公開]**&#x200B;ワークフローステップまで追跡されます。（ASSETS-44104）
* [!DNL AEM] で画像を処理および公開する際に、**[!UICONTROL メモリ不足（OOM）]**&#x200B;エラーが表示されます。この問題は、**[!DNL Dam Asset update]** や **[!DNL Dynamic Media: Reprocess assets]** など、ワークフローの廃止されたメソッドが原因で発生しました。（ASSETS-43343）
* タイトルを更新するなど、小さな変更を加えた後、ローカルの Sites インスタンスで **[!DNL Connected Assets configuration]** をもう一度開いて保存し直します。すると、リモートインスタンスからローカルインスタンスへの接続が失われます。その結果、ローカルの Sites インスタンスとの通信を確立できません。（ASSETS-44484）
* [!DNL AEM 6.5.21] では、リスト表示でアセットのアップロードがキャンセルされ、2 回目のアップロードが実行されたときに、[!DNL AEM] に「**[!UICONTROL NaN アセットのうち 0 がアップロードされました]**」というエラーが表示されます。（ASSETS-44124）

#### [!DNL Dynamic Media]{#assets-dm-6523}

スマート切り抜きの生成に失敗したことを識別するためのメタデータプロパティ（`jcr:content/metadata/dam:scene7SmartCropStatus`）がアセットに追加されました。手動または自動ワークフローで、スマート切り抜きの問題が発生しているアセットの効率的な検索、フィルタリングおよび再処理を行うことができます。（ASSETS-46237）

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

ハイブリッドアドオンパッケージは、2025年5月22日木曜日（PT）に公式リリースされる AEM 6.5.23 で、Adobe ソフトウェア配布から公開されます。ソフトウェア配布で **AEM 6.5 Dynamic Media ハイブリッドアドオンパッケージ**&#x200B;を検索すると見つけることができます。


### [!DNL Forms]{#forms-6523}

#### Forms Designer

* ユーザーが exportDataAPI を使用して XFA ベースのPDFのデータを書き出すと、Acrobat Readerを使用して手動で書き出した XML データと比較して、結果の XML は不一致を示します。 Acrobat Readerから生成された出力と比較して、一部のフィールドの値が出力に含まれていませんでした。 （LC-3922791）。

* AEM Forms 6.5.22.0 で、ユーザーが Workbench の Output サービスを使用してタグ付きPDFを生成しようとすると、生成されるPDFのコンテンツ項目のテーブルの参照タグに、追加のラベルタグが含まれます。 （LC-3922756）

* ユーザーがAEM Forms Designerでフィールドのキャプションを下揃えまたは右揃えに配置すると、タグツリーにキャプションのみが含まれ、対応する値が欠落するので、アクセシビリティタグ付けが不完全になります。 （LC-3922619）。

* AEM Forms 6.5 サービスパック 6 からAEM Forms サービスパック 20 にアップグレードすると、生成された PDF の QR コードが読み取れなくなります。 QR コードの代替テキストはアクセシビリティテストにも失敗し、スクリーンリーダーの互換性に影響を与えます。 （LC-3922551）。

* AEM Forms サービスパック 18 のエージェント UI でレターをレンダリングすると、FormService.render （） API が原因で、コンテンツが正しく表示されません。 （LC-3922461）。

#### Forms

* AEM Forms アダプティブフォームのルートパネルで「タイトルのリッチテキストを許可」を有効にすると、ネストされたパネルの「レコードのドキュメントからタイトルを除外」設定によって、自動生成されたレコードのドキュメント内のルートパネルのタイトルが正しく非表示になりません。 （FORMS-19696）。

* オンプレミスのAEM 6.5 インスタンス上の JSON スキーマで aem:afProperties を使用してカスタム sling:resourceType をコアコンポーネントに割り当てようとすると、カスタムリソースタイプが適用されません。 （FORMS-19691）。

* ユーザーが URI を使用して添付ファイルが事前入力されたアダプティブフォームを送信すると、バイナリデータがないことが原因で、フォームの送信が NullPointerException で失敗します。 （FORMS-19371）（FORMS-19486）。

* AEM 6.5 Formsの「PDFとドキュメント」セクションで、Formsをアップロードすると、タイムライン機能が機能しなくなります。 （FORMS-19407）（FORMS-19234）。

* AEM Formsの標準（OOTB）ファイル添付コンポーネントを使用してファイルをアップロードすると、セキュリティの脆弱性が特定されます。 これにより、権限のないエンティティによって送信プロセスが妨害される可能性があります。 （FORMS-19271）。

* ユーザーが、レコードのドキュメント（DoR）を自動生成するようにAEM Forms内で初期設定済みのアダプティブフォームを設定すると、Acrobat Readerのドキュメントプロパティの「タイトル」フィールドに、取り込まれた DoR のタイトルが表示されず、デフォルトでは、ファイル名の代わりにフォームのタイトルが表示されません。 （FORMS-19263）。

* ユーザーがエージェント UI でインタラクティブ通信を開くと、事前入力されたデータは完全には消去されません。削除すると、同じデータが自動的に再入力されます。 （FORMS-19151）。

* ユーザーがエージェント UI で日付フィールドをプレビューすると、VM の UTC 設定とシステムによる日付の解釈の間のタイムゾーンの不一致により、日付が予期せず変更されます。 （FORMS-19115）。

* ユーザーがフォームを送信すると、添付ファイルが重複して、同じファイルが複数アップロードされる場合があります。 （FORMS-19045）（FORMS-19051）。

* AEM 6.5 Document Security でポリシーセットにコーディネーターを追加すると、実稼動環境と下位環境の両方でエラーが発生する。 （FORMS18603、FORMS18212、FORMS19697）。

* AEM Forms サービスパック 22 で、ユーザーがデスクトップモードで空のフィールドを使用して「datepicker-calendar-icon」をクリックすると、未定義の_$focusedDate 変数が原因でエラーが発生し、関連するカスタムスクリプトが中断されます。 （FORMS-18483）（FORMS-18268）。

* AEM Forms Service Pack 19 （6.5.19.0）で、顧客がレターをプレビューする際に、「単語単位の金額」フィールドに数値が誤って表示されたり更新されたりせず、配置のずれやコンテンツ内のスペースの欠落が発生します。 （FORMS-18437、FORMS-17330、FORMS-18209、FORMS-18557、CTG-4150848、FORMS-19614、LC-3922004）

* RHEL 上のAEM Forms 6.5 SP19 で保存済みのレターをプレビューすると、コンテンツが誤って配置され、スペースが欠落し、「x」のような予期しない文字が表示されます。 （FORMS-18422）（FORMS-17641）。

* ユーザーがAEM Formsのタブ間を移動すると、最初のタブでコンポーネントを選択しても応答しなくなります。 （FORMS-18345）。

* AEM Forms 6.5.21.0 では、ユーザーが WebToPDF オプションを使用してHTML ファイルをPDFに変換すると、出力PDFにメタデータタグやタイトルタグを含むヘッダーセクションが欠落します。 （FORMS18223、FORMS17835、FORMS19642、FORMS18224）。

* AEM JEE Process Manager SDKでは、retryAction （long actionOid） メソッドを呼び出すと、tb_action_instance テーブルにある最初のアクションが誤って再試行されます。 この問題は、特定のアクション ID が指定されている場合や、ID が null の場合でも発生し、意図しない動作が生じます。 （FORMS-18187）。

* SP22 に更新すると、エラーメッセージが表示されずにドラフトの保存機能と送信機能が失敗する問題が発生します。 （FORMS-18069）。

* AEM 6.5.21.0 では、XSD ベースの基盤コンポーネントからコアコンポーネントに移行すると、JSON スキーマでのクロスファイル参照の実装ができなくなり、アダプティブFormsの移行に影響を与えます。 （FORMS-18065）。

* ユーザーがエージェント UI でレターをプレビューすると、IC 時間の変換の問題が原因で、日付フィールドに誤った値が表示される。 これらの不一致は、VM 環境とシステムの時間の解釈（UTC とローカル時間）のタイムゾーンの違いによって生じます。 （FORMS-17988）（FORMS-17248）。

* AEM Formsで通知 IC テンプレートを使用してレターをプレビューする場合、PDFの生成時間は、同じサーバー上であっても、1.5 秒から 10 秒以上と大きく異なります。 この不整合は、ビジネスクリティカルなワークフローに影響を与えます。 （FORMS-17951）。

* ユーザーが「データソース」オプションを使用してアダプティブフォーム内の手書き署名オブジェクトを XDP にバインドすると、有効な値を使用している場合でも、アスペクト比の検証エラーが繰り返し発生するので、変更を保存できません。 （FORMS-17587）。

* ユーザーがドキュメントフラグメントに対して非表示のフィールドを多く含む特定の XDP を使用すると、AEMは cm:optional プロパティを false に設定したCRX ノードを作成し、その結果、インタラクティブ通信（IC）の送信が失敗します。 （FORMS-17538）。

* AEM Forms 6.5.19.0 では、ユーザーがレターをプレビューする際、リードとフロックの桁数制限が定義されていると、数値ボックスフィールドが負の値を正しく処理できません。 この問題は、マイナス記号を数字の一部として扱う parseFloat の使用が原因で発生します。 （FORMS-17451）。

* AEM Forms 6.5 でレターをプレビューすると、Adobe.json ファイルで「*」ワイルドカードが使用され、その目的と潜在的な変更に関する懸念が生じます（FORMS-17317）。

* ユーザーが「固定レートセーバー共同アカウントの適用」でスクリーンリーダーを使用すると、見出しが誤って「クリック可能」と通知され、アクセシビリティの問題が発生します。 （FORMS-17038）。

* フォームを埋め込むと、生成された iframe に title 属性が欠落し、アクセシビリティコンプライアンスの問題が発生します。 （FORMS-17010）。

* テーマやフラグメントなどの関連する依存関係を含めなければ、Forms Manager UI を使用してフォームをダウンロードすることはできません。 （FORMS-15811）。

* ユーザーがモバイルデバイス（iOSおよびAndroid）上のフォームにアクセスすると、最初のページの「次へ」ボタンと「前へ」ボタンは無効になりますが、スクリーンリーダーは無効と識別しません。 （FORMS-15773）。

* ユーザーがフラグメントと遅延読み込みを有効にした大きなフォームを保存すると、ドラフトの取得に失敗し、ワークフローが中断されます。 （FORMS-19890、FORMS-19808）。

#### FORMS JEE

* AEM Formsでデータベースを再設定する場合、パラメーターがハードコードされているので接続に失敗します。 （FORMS-19568、FORMS-17621）

* ユーザーが部分的に自動でセットアップする方法を使用して MySQL 8.4 とAEM 6.5 をセットアップする場合、データベース接続テスト中に LiveCycle Configuration Manager （LCM）が必要な MySQL コネクタドライバーを認識せず、セットアップが失敗します。 （FORMS-19442）。

* JEE 環境で、JRE 11 上の JDBC 12.8.1 を使用して LCM を実行すると、非互換性の問題が原因でセットアップが失敗します。（FORMS-19276）。

* ユーザーがオンプレミスのAEMでタスクを開くと、AssignedUserProfile ではなく、Workspace開始アクションプロファイルが実行されます。 （FORMS-19065）。

* AEM JEE Process Manager で retryAction （long actionOid） メソッドを使用すると、予期しない動作が発生します。 （FORMS-18357）（FORMS-18187）。

* AEM Forms 6.5.21.0 で、PDFG 変換が次のエラーで失敗する：（FORMS-16851）（FORMS-14613）。

#### Forms の Captcha {#forms-captcha-6523}

* 送信エラーコードを 400 に更新することで、アダプティブフォームの reCAPTCHA アラートを改善しました。また、ログアラートを絞り込んで、タイムアウト、有効期限、ボット検出の失敗を区別し、トラブルシューティングの精度とシステムの可観測性を高めました。（FORMS-19240）
* AEM Forms で reCAPTCHA 統合を使用する際に、リソースリークの可能性を防ぎ、システムの安定性を向上させるために、`ReCaptchaConfigurationServiceImpl` で閉じられていない `ResourceResolver` インスタンスを閉じました。（FORMS-19242）
* `/conf/global` フォルダーに複数のエントリが存在する場合に、各フォームに正しい設定が連結されるようにすることで、AEM Form の CAPTCHA 設定処理を改善しました。設定コンテナが明示的に選択されていない場合に、誤った CAPTCHA 設定を意図せずに使用することを防ぎます。（FORMS-19239）

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

* Coral アラートバナーで、サービスパック 21 にアップグレードするとテキストの色が黒ではなく白く表示される問題を修正しました。正しいスタイルを適用し、インターフェイス全体でアラートメッセージの適切なコントラストと読みやすさを維持しました。（NPR-42359）
* JWT （JSON web トークン）の廃止に伴い、スマートタグ設定で OAuth 統合のサポートが追加されました。更新された認証方法を使用して、スマートタグ機能を維持します。（NPR-42296）

#### Apache Felix {#foundation-apachefelix-6523}

CRX のバイナリタイプのプロパティフィールドにプライベートファイルをアップロードする際に発生していた NullPointerException を修正し、サービスパック 16 で存在していた互換性を復元しました。サーバーエラーや証明書更新プロセスの中断を発生させずに、AEM Managed Services での安全なキーファイルアップロードワークフローを有効にします。（CQ-4359178）


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

* Service Pack 21 へのアップグレード後に HTML ページを読み込むと遅延やエラーが発生する、Apache Sling スクリプティングサービス間の OSGi 依存関係サイクルを解決しました。内部サービス参照を更新し、`SightlyScriptingEngineFactory` および関連コンポーネントに関与する循環依存関係を排除し、スクリプトエンジンの信頼性と起動動作を向上させました。（GRANITE-56808）
* Apache Sling の「JS スクリプトの使用」をアップデートし、起動時に積極的にページを読み込むのではなくオンデマンドでのみ読み込むようにしました。これにより、スレッドの競合が排除され、読み込み中にパブリッシュサーバーが応答しなくなるリスクが軽減されます。この変更により、スクリプトの早期解決によって発生するリソースのロックが防止されるため、高トラフィックのシナリオにおけるサーバーの安定性と応答時間が向上します。（GRANITE-56611）
* AEM オムニサーチで、入力フィールドのプレースホルダーがラベルとして正しく表示されず、視覚的な混乱を招く問題を修正しました。フィルターフィールド間でプレースホルダーが適切にレンダリングされ、一貫性のある、アクセスしやすいフォームの動作が維持されるようにします。（GRANITE-51791）
* コンテンツフラグメントモデルのエディターでマルチフィールド参照を使用する CFM （コンテンツフラグメントモデル）を 30 個を超えて選択した際にトリガーされる、サーバーエラーを解決しました。POST 操作をサポートするようにフィルター提案コンポーネントを強化しました。この機能により、コンテンツフラグメントの作成時に大規模な参照セットを適切に処理でき、大容量モデル設定の安定性が向上します。（GRANITE-57164）
* CFM でチェックボックスの近くをクリックすると、意図せずに状態が切り替わる問題を修正しました。クリックのアクティベーションをチェックボックス要素に限定するようにスタイルを更新し、ユーザーの誤操作を防ぎ、フォームの操作性とアクセシビリティを向上させました。（GRANITE-52384）


<!--
#### Integrations{#foundation-integrations-6523}

* A () -->


#### Jetty{#foundation-jetty-6523}

カスタムホストヘッダーを含む Dispatcher SSL 設定を使用している AEM のお客様に対する SNI 検証で、HTTPS 経由の API 呼び出しがブロックされる問題を修正しました。Jetty 設定の一部として SNI 検証を無効にするオプションを導入し、`mod_proxy` の実行が不可能な特定のリバースプロキシ設定との互換性を有効にします。（NPR-42614）


<!--
#### Localization{#foundation-localization-6523}

* A () -->

<!--
#### Oak {#foundation-oak-6523}

* A () -->


#### プラットフォーム{#foundation-platform-6523}

* タグがインラインで作成されたか標準のタグ作成方法を使用して作成されたかに関係なく、結合されたタグ値が常にアセット間で正しく表示されるようにすることで、一貫性のないタグの結合動作を修正しました。`EN:title` フィールドの残存値が結合されたタグの表示を上書きするのを防ぎます。（CQ-4358812）
* タグ編集ダイアログボックス内のタグ値における、アンパサンド文字のエンコーディングの繰り返しを修正しました。保存するたびに「&amp;」エンティティが追加されるのを防ぎ、編集間でタグ値がクリーンなまま一貫性が維持されるようにし、作成されたコンテンツの表示エラーを回避します。（CQ-4359048）
* WebSphere® 上で実行中の AEM 6.5 で、アダプティブフォームの送信時にメールが配信されない `ClassCastException` エラーを解決しました。この修正により、WebSphere® 環境で期待されるメールハンドラー設定に合わせて `com.sun.mail.handlers.text_plain` と `java.activation.DataContentHandler` の互換性が確保され、メール送信が成功します。（NPR-42500）
* インストールが失敗し、エラー応答が空の場合に AEM で明確なメッセージが表示されるようにすることで、パッケージマネージャーのエラー処理を改善しました。この修正により、サイレントエラーを防ぎ、パッケージのデプロイメント中により迅速にデバックできるようになります。（NPR-42375）

<!--
#### Security{#foundation-security-6523}

* A -->

<!--
#### Sling{#foundation-sling-6523}

* A () -->


#### 翻訳{#foundation-translation-6523}

「**言語コピーを更新**」を使用してワークフローのコンテンツフラグメントを更新する際にトリガーされる NullPointerException （NPE）の問題を修正しました。この修正により、翻訳参照に紐付けられたコンテンツを編集する際に、ワークフローが失敗した状態になったり、実行中の状態で停止したりすることがなくなります。（NPR-42115）

#### ユーザーインターフェイス{#foundation-ui-6523}

コンポーネント編集ダイアログボックスの「**完了**」や「**キャンセル**」など、Coral UI ダイアログボックスのボタンに欠落している `title` 属性を追加して、アクセシビリティを向上させ、自動検証を有効にします。ボタンがマークアップレンダリング全体で期待される属性を保持し、Selenium ベースの UI テストでエラーが発生しないようにします。（NPR-42412）

#### WCM{#foundation-wcm-6523}

サービスパック 19 以降を含む環境で「**言語コピーを更新**」を使用すると、翻訳ジョブにページが追加されなくなる問題を修正しました。翻訳ワークフローが期待どおりに実行され、手動の操作を行わなくても、言語コピー間でページを適切に転送できます。（CQ-4357929）

#### ワークフロー{#foundation-workflow-6523}

`EmailNotificationServiceProcessor` でホットフィックスのデプロイメント後に `getSegmentId` メソッドが `null` を返し、それが原因となってワークフローの処理中にメールトリガーが失敗する問題を修正しました。AEM インスタンス間のメール通知ワークフローをサポートするために、プロセッサーが必要な `SegmentInfo` 値を取得できるようにすることで、適切なセグメント ID 解決ロジックを復元します。（CQ-4359755）


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

AEM 6.5 で廃止または削除されたすべての機能の詳細なリストについては、[廃止および削除された機能](/help/release-notes/deprecated-removed-features.md/)を参照してください。

### SPA エディター {#spa-editor}

[SPA エディター](/help/sites-developing/spa-overview.md)は、AEM 6.5 のリリース 6.5.23 以降の新しいプロジェクトでは廃止されました。SPA エディターは、既存のプロジェクトでは引き続きサポートされますが、新しいプロジェクトには使用しないでください。

AEM でヘッドレスコンテンツの管理に推奨されるエディターは次のようになりました。

* ビジュアル編集用の[ユニバーサルエディター](/help/sites-developing/universal-editor/introduction.md)。
* フォームベース編集用の[コンテンツフラグメントエディター](/help/sites-developing/universal-editor/introduction.md)。

## 既知の問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **AEM 6.5.21 - 6.5.23 および AEM 6.5 LTS GA の JSP スクリプティングバンドルの問題**
AEM 6.5.21、6.5.22、6.5.23 および AEM 6.5 LTS GA には、既知の問題を含む `org.apache.sling.scripting.jsp:2.6.0` バンドルが付属しています。この問題は、通常、AEM インスタンスが多数の同時リクエストを処理する際の高負荷時に発生します。

  この問題が発生すると、`org.apache.sling.scripting.jsp:2.6.0` への参照と共に、次の例外のいずれかがエラーログに表示される場合があります。

   * `java.io.IOException: classFile.delete() failed`
   * `java.io.IOException: tmpFile.renameTo(classFile) failed`
   * `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
   * `java.io.FileNotFoundException`

  このエラーが発生した場合、回復する唯一の方法は、AEM インスタンスを再起動することです。

  Adobe カスタマーサポートに連絡し、このリリースノートを参照して解決してください。

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

### AEM Forms の既知の問題 {#known-issues-aem-forms-6523}

* お客様が Struts 2.x から 6.x にアップグレードする場合、特にチェックボックス・コンポーネントが false を返し、リスト *Integer* にバインドされている場合、より厳密なタイプ・チェックはサイレント・エラーを引き起こす可能性があります。 シリアル化の解除エラーを回避するには、この値の不一致を明示的に処理する必要があります。 （FORMS-20203）

* SUSE® Linux®（SLES 15 SP6 以降）サーバーで HTML から PDF への変換が失敗し、次のエラーが表示されます。

  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
その場合は、次の環境変数を設定して、サーバーを再起動します。
  `OPENSSL_CONF=/etc/ssl`

* AEM Forms JEE サービスパック 21（6.5.21.0）のインストール後、`<AEM_Forms_Installation>/lib/caching/lib` フォルダー配下に Geode JARs `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` の重複エントリが見つかった場合（FORMS-14926）、問題を解決するには、次の手順に従います。

   1. ロケーターが実行中の場合は、ロケーターを停止します。
   1. AEM サーバーを停止します。
   1. `<AEM_Forms_Installation>/lib/caching/lib` に移動します。
   1. `geode-*-1.15.1.2.jar` を除くすべての Geode パッチファイルを削除します。 `version 1.15.1.2` を含む Geode jar のみが存在することを確認します。
   1. 管理者モードでコマンドプロンプトを開きます。
   1. `geode-*-1.15.1.2.jar` ファイルを使用して Geode パッチをインストールします。

* ユーザーが保存された XML データを含むドラフトレターをプレビューしようとすると、一部の特定のレターが `Loading` 状態でスタックする。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （FORMS-14521）

* AEM Forms サービスパック 6.5.21.0 へのアップグレード後、`PaperCapture` サービスが、PDF に対して OCR（光学文字認識）処理を実行できない。このサービスでは、PDF やログファイルの形式で出力を生成しません。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （CQDOC-21680）

* ユーザーが AEM 6.5 Forms サービスパック 18 または 19 からサービスパック 20 または 21 にアップグレードした際、JSP コンパイルエラーが発生しました。 このエラーにより、アダプティブフォームを開いたり、作成したりすることができませんでした。 また、他の AEM インターフェイスでも問題が発生しました。 これらのインターフェイスには、ページエディター、AEM Forms UI、ワークフローエディター、システム概要 UI が含まれていました。（FORMS-15256）

  このような問題が発生した場合は、次の手順を実行して解決します。
   1. CRXDE のディレクトリ `/libs/fd/aemforms/install/` に移動します。
   1. `com.adobe.granite.ui.commons-5.10.26.jar` という名前のバンドルを削除します。
   1. AEM サーバーを再起動します。

* Forms アドオンを使用して AEM Forms サービスパック 20（6.5.20.0）にアップデートすると、資格情報に基づく認証を使用する従来の Adobe Analytics Cloud Service に依存する設定が機能しなくなります。この問題により、分析ルールが正しく実行されなくなりました。 ホットフィックスをダウンロードしてインストールするには、[Adobe Experience Manager Forms のホットフィックス](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)の記事を参照してください。 （FORMS-15428）
* インタラクティブ通信エージェント UI の印刷プレビューでは、すべてのフィールド値に通貨記号（ドル記号 $ など）が一貫して表示されません。 999 までの値の場合は表示されますが、1000 以上の値の場合は表示されません。 （FORMS-16557）
* インタラクティブ通信内でネストされたレイアウトフラグメントの XDP に対する変更は、IC エディターに反映されません。 （FORMS-16575）
* インタラクティブ通信エージェント UI の印刷プレビューでは、一部の計算値が正しく表示されません。 （FORMS-16603）
* 印刷プレビューでレターを表示すると、コンテンツが変更されます。 つまり、一部のスペースが表示されなくなり、特定の文字が `x` に置き換えられます。（FORMS-15681）
* ユーザーが WebLogic 14c インスタンスを設定すると、JBoss® で実行されている JEE 上の AEM Forms サービスパック 21（6.5.21.0）の PDFG サービスが、SLF4J ライブラリに関連するクラスローダーの競合により失敗します。エラーは次のように表示されます。（CQDOC-22178）：

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature.
  ```


## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、この [!DNL Experience Manager] 6.5 サービスパックリリースに含まれている OSGi バンドルとコンテンツパッケージのリストが記載されています。

* [Experience Manager 6.5.23.0](/help/release-notes/assets/65230-bundles.txt) に含まれている OSGi バンドルのリスト<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.23.0](/help/release-notes/assets/65230-packages.txt) に含まれているコンテンツパッケージのリスト<!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

これらの Web サイトは、お客様のみが利用できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/ja/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/ja/docs/experience-manager-65)
>* [アドビ製品アップデートの優先通知を購読](https://www.adobe.com/subscription/priority-product-update.html)
