---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 3
source-git-commit: 72b3eaea279911569dbd6b9acf41527111e9e53c
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 44%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2023 年 2 月 23 日木曜日 <!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.16.0 の内容 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] 6.5.16.0 には、2019年4月の 6.5 リリースの公開当初にリリースされた新機能、お客様から要望のあった主な機能強化およびパフォーマンスや安定性、セキュリティの向上が含まれています。[このサービスパック](#install)を [!DNL Experience Manager] 6.5 にインストール<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Dynamic Mediaの主な改善点は次のとおりです。

Dynamic Mediaビデオ配信（CMAF を使用）でのアダプティブビットレートストリーミングに対して、新しいプロトコル DASH（HTTP 経由でのダイナミックアダプティブストリーミング）のサポートが開始されました。 [共通メディアアプリケーション形式] 有効 )。

* アダプティブストリーミング (DASH/HLS) により、エンドユーザーがビデオを視聴する際の操作性が向上します。
* DASH はアダプティブビデオストリーミングの国際標準プロトコルで、業界で広く採用されています。
* アジア太平洋およびヨーロッパ中東アフリカで間もなく提供される、北米で利用可能（サポートチケットを介して有効化）。

詳しくは、 [アカウントで DASH を有効にする](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* Connected Assets:リモート DAM の画像に対してスマート切り抜きオプションを有効にし、画像をフォルダーにアップロードし、フォルダーをローカルサイトに同期した場合、ローカルの Sites デプロイメントではフォルダーが開きません。 （NPR-39912）
* コレクションを名前で並べ替えると、リスト表示が適切に機能しない (ASSETS-19401)
* サイズの大きいメディアファイル (JPEG) がコレクションにアップロードされると、Experience Managerは応答を停止します。 （ASSETS-19387）
* コンテンツツリーペインでは、アセットの場所が適切にレンダリングされないので、表示されるアセット名が正しくありません。 （ASSETS-18870）
* リンクを使用してコレクションを共有する際、URL 内のデータが、カード表示とリスト表示のシャッフルで一致しません。 （ASSETS-18758）
* フォルダータイプに対してフィルターを使用してオムニサーチを実行すると、検索結果に一貫性がなくなります。 （ASSETS-18227）
* この `dam:size` プロパティがXMPの書き戻し後に更新されないので、誤った情報がから返されます。 `/platform/path/to/asset.jpg;resource=metadata` API （ASSETS-17631）
* すべてのリソースインスタンスで閉じられていないExperience Managerリゾルバーです。 （ASSETS-16904）
* アセットのバージョンを作成できません ( `create` および `modify` 権限。 （ASSETS-15956）
* この `move` アセットを別のポイントに移動する際に、ボタンがランダムに無効になります。 （ASSETS-14889）
* スクリーンリーダーは、見出しを識別できません。見出しタグ内ではテキストが定義されず、一般的なテキストとして定義されています。 （ASSETS-6924）
* 画像の下の代替テキストは必須ではありませんが、画像の下に表示されるテキストは、 `Type` 属性。 （ASSETS-6915）


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* フォーム要素にラベルが含まれていません。 NVDA や JAWS などのスクリーンリーダーでは、フォームラベル情報が正しくお知らせされません。 （CQ-4344078）
* ドロップダウンが `Escape` キーは、キーボードで使用される。 （CQ-4344077）
* 無効な入力が与えられた後にインラインエラー修正候補に表示される情報アイコン（「i」という文字）は、キーボードを使用してアクセスできません。 （CQ-4344076）
* `getManifestURI` JCR プロパティが次のように読み取られたので、null を返します。 `toString` の代わりに `getString`. （ASSETS-18674）
* SmartCrop ビデオコンポーネントが正しく動作していません。 コンポーネントは、ストリーミングではなく再生を実行しており、VTT 呼び出しが失敗し、404 エラーが発生します。 （ASSETS-18468）
* 選択 **[!UICONTROL プロパティ]** アセットのビューアページで、null ポインターの例外が発生する。 （ASSETS-18420）
* [!DNL Experience Manager] 次の機能を含む DASH ストリーミングのユーザインターフェイスが変更されました。
   * ビデオプロファイルエディターに「 CMAF (Common Media Application Format) 」フィールドが表示される。
   * ビデオのアップロードプロセスでは、CMAF フラグが送信されます。
   * オプション **[!UICONTROL auto]**, **[!UICONTROL hls]**、および **[!UICONTROL ダッシュ]** がビューアプリセットエディターの再生ドロップダウンリストで使用できるようになりました。 **[!UICONTROL 動作]** タブをクリックします。
（ASSETS-17428）
* ナビゲーションで、 **[!UICONTROL Assets]** > **[!UICONTROL ファイル]** > **[!UICONTROL 作成]** > **[!UICONTROL カルーセルセット]**&#x200B;の場合、画像アイコンは「スライド 1」のテキスト文字列と重なります。 （ASSETS-18578）
* 非公開のアセットが再び公開される。 （ASSETS-16428）
* Experience Manager作成者が読み込みの問題によりダウンし、合成アラートの作成を促すメッセージが表示されました。 （ASSETS-15937）
* Dynamic Mediaの一般設定ページに、未翻訳のエラーメッセージが表示されます `Failed to fetch data` が表示されます。 （ASSETS-15617）

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] 主な機能 {#forms-features-6516}

* [ヘッドレスアダプティブForms](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 開発者は、従来のグラフィカルユーザーインターフェイスを使用するのではなく、API を使用してアクセスし、操作できるインタラクティブフォームを作成、公開、管理できます。

* [アダプティブFormsコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) は、Adobe Experience Manager WCM コアコンポーネントの基盤上に構築された、24 個のオープンソースの BEM 準拠コンポーネントのセットです。 これらのコンポーネントはオープンソースで、開発者は、組織の特定のニーズに合わせて、これらのコンポーネントを簡単にカスタマイズおよび拡張できます。 カスタマイズする既存のスキルを持つすべてのユーザー [WCM コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) では、これらのコンポーネントを簡単にカスタマイズおよびスタイル設定できます。

* OSGi 上のReader拡張サービスに、Adobe Acrobat ReaderでのデータのインポートまたはエクスポートをおこなうPDFに対する使用権限のインポートとエクスポートを可能にする個別のオプションが追加されました。 （NPR-39909）

### [!DNL Forms] 修正 {#forms-fixes-6516}

* タスクの割り当て**手順を使用して割り当てられたタスクに関する通知を送信する場合、割り当てられた個人に 1 つではなく 2 つの電子メールが送信されます。 （NPR-40078）
* ユーザーがテーブルヘッダーを非表示にした場合、以前に設定した列幅が未設定になり、すべての列が同じ幅を保持します。 （NPR-40063）
* 管理者ユーザーのデフォルトのパスワードを `admin`、 `Prepare Adobe Experience Manager Server For DSC deployment` AEM Forms JEE Service Pack でエラーが発生したことを確認します。 (NPR-40062)、(NPR-39387)
* OutputService API と AssemblerService API が、PDFフォームをPDF/A に変換できない。(NPR-39990)
* AssemblerService はPDF/A にPDFを変換できません。ユーザーがPDFをPDF/A に変換すると、次のエラーが発生します。 `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. （NPR-39956）
* GuideSubmitServlet API 呼び出しのサーバー側検証が失敗した場合、クライアントに送信される応答ではエラーは返されません。 （NPR-39925）
* Windows サーバーでAEM 6.5.15.0 Service Pack にアップグレードした後、複数のエラーメッセージが表示され、電子メールサービスが機能しません。（NPR-39919）
* AEM 6.5.14.0にアップグレードし、importData サービスを使用してPDFを XML と結合すると、次のエラーが発生します。 `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.（NPR-39807）
* ユーザーが **ドキュメントセキュリティオフィス** 拡張機能では、次の問題が発生します。
   * Microsoft® Excel が頻繁にクラッシュします。
   * 保護されたドキュメントを開くと、 **ドキュメントセキュリティオフィス** 拡張機能がコンピューターにインストールされていると認識されません。 セキュリティ拡張機能をダウンロードしてインストールするようにユーザーに指示します。 （NPR-39768）
* ユーザーがAEM 6.5.15.0 Service Pack にアップグレードした後、PostScript から Pdf への変換が機能しない。 (NPR-39765)、(NPR-39764)
* アダプティブフォームを開いた後にツアー画面を開こうとすると、NullPointer 例外が発生して失敗します。`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:”` (NPR-39654)
* Windows では、ユーザーが高コントラストの黒の設定を有効にすると、HTML5 Formsコンテンツは、ブラウザーでHTMLプレビューとしてレンダリングされると不明瞭になります。 （NPR-39018）

## 統合 {#integrations-6516}

* AdobeSearch&amp;PromoteコードとExperience Manager6.5 から依存関係を削除。AdobeSearch&amp;Promoteは 2022 年 9 月にサービス終了に達しました。 詳しくは、 [AdobeSearch&amp;Promoteのサービス終了に関するお知らせ](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). （NPR-39706）

## [!DNL Sites] {#sites-6516}

* 現在 `cq-wcm-core` artifactory リリースに POM がありません。 （SITES-10983）
* ロールアウトプレビューアクションでは、作成するページのリストを表示しないでください。 (SITES-10355、CQ-4266213)
* MSM 分離後にロールアウトすると、分離されたページが再作成されます。 （SITES-9841）
* ローンチの作成がタイムアウトになっています。ユーザーは、読み込み画面でリクエストがタイムアウトするまでに、何分も待つ必要があります。 （SITES-9051）
* ロールアウトページユーザーインターフェイスに存在しない親ページのパスが表示されています。 成功メッセージ付きでページをロールアウトできますが、親ページがロールアウトされないので、子ページはロールアウトされません。 （SITES-8621）

### [!DNL Sites] - コアコンポーネント {#sites-core-components-6516}

* 電子メールページのリンク処理を一元化し、モデルのカスタマイズが不要になりました。 （SITES-9002）

### [!DNL Sites]  — 管理ユーザーインターフェイス {#sites-adminui-6516}

* CSV の書き出しで、選択したページの下にあるすべてのページが書き出されない。 （SITES-9390）

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* コンテンツフラグメントの JSON を印刷できません。 これは、コンテンツフラグメントのプレビューページを開いたときにGraphQLクエリを生成できないからです。 （SITES-8619）
* コンテンツフラグメントモデルエディターを再度開くと、 **[!UICONTROL 日時]** フィールドのタイプは、デフォルトで日付と時刻に設定されます。 （SITES-8401）

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* 許可されたテンプレートの下にテンプレートがリストされている場合でも、エクスペリエンスフラグメントを別のフォルダーに移動することはできません。 （SITES-8601）
* （SITES-7989）


### [!DNL Sites] - ページエディター {#sites-pageeditor-6516}

* オーサリングモードでのページレンダリングで多数の `TemplatedResourceImpl` オブジェクト。 （SITES-9350）


## Sling {#sling-6516}

* Experience Managerは起動時にデッドロックされます。 （NPR-39832）
* バニティーパスがExperience Managerのバージョンストレージに多数存在する場合、Experience Managerの開始に失敗します。 （NPR-38955）


## 翻訳プロジェクト {#translation-6516}

* In `MicrosoftTranslationServiceImpl`、クエリー文字列パラメーター `Category` が正しくありません。 （NPR-39828）
* 翻訳プロジェクトを作成すると、エラーが表示されます *マスターページリソースが存在しません*;翻訳プロジェクトは作成されません。 （NPR-39762）
* 人間の翻訳コネクタを使用する翻訳プロジェクトに期限を設定できません。 （NPR-39593）

## ユーザーインターフェイス {#ui-6516}

* より小さい解像度に変更すると、DatePicker が表示されず、AM/PM の選択が表示されず、表示も変更もされません。 （NPR-39948）
* js の縮小（JavaScript の最小化）を使用する場合、解析エラーが原因で縮小は処理されません。 （NPR-39650）
* タグフィールド (`/libs/cq/gui/components/coral/common/form/tagfield`) がタイムラインと競合しています。 （CQ-4350751）


## WCM {#wcm-6516}

* ロールアウトプレビューアクションでは、作成するページのリストを表示しないでください。 (CQ-4266213、SITES-10355)

## ワークフロー {#workflow-6516}

* から編集可能なワークフローモデルを手動で削除 `/conf` 編集可能なモデルを持たない、長持ちするランタイムモデルインスタンスを残します。 （CQ-4349365）


## [!DNL Experience Manager] 6.5.16.0 のインストール {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0 には [!DNL Experience Manager] 6.5 が必要です。手順について詳しくは、[アップグレードに関するドキュメント](/help/sites-deploying/upgrade.md)を参照してください。<!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.16.0 をインストールしてください。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.16.0 パッケージを削除またはアンインストールすることを推奨しません。 したがって、パッケージをインストールする前に、ロールバックする必要がある場合に備えて `crx-repository` のバックアップを作成する必要があります。<!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### [!DNL Experience Manager] 6.5 へのサービスパックのインストール {#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)からサービスパックをダウンロードします。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、「**[!UICONTROL パッケージをアップロード]**」を選択して、パッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、「**[!UICONTROL インストール]**」を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。[Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでもときどき発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.16.0. の自動インストールに使用できる方法は 2 つあります<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.16.0 では、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.16.0)` が表示されます。<!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.14 以降です（web コンソールを使用：`/system/console/bundles`）。<!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Service Pack のインストール [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

AEM Forms にサービスパックをインストールする手順については、[AEM Forms サービスパックのインストール手順](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)を参照してください。

### UberJar {#uber-jar}

[!DNL Experience Manager] 6.5.16.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/)で入手できます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>Experience Manager6.5.16.0では、UberJar のバージョン (6.5.15.0) は以前のリリースと同じです。


Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。メインの UberJar ファイルの名前は、「`uber-jar-<version>.jar`」に変更されます。ですので `classifier` がなく、値として `apis` を `dependency` タグに使用します。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

[!DNL Experience Manager] 6.5.7.0 で非推奨（廃止予定）とマークされた特徴と機能のリストは次のとおりです。 これらの機能は、最初は非推奨とマークされ、将来のリリースでは削除されます。別のオプションが提供されます。

デプロイメントでその特徴または機能を使用しているかどうかを確認します。また、別のオプションを使用するように、実装の変更を計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 |  6.5 で **[!UICONTROL と]** の統合が更新されたことにより、[!DNL Experience Manager]AEM クラウドサービスのオプトイン[!DNL Adobe Target]画面は非推奨になりました。この統合では、Adobe Target Standard API をサポートしています。 [!DNL Experience Manager]API は、Adobe IMS と [!DNL Adobe I/O Runtime] の認証方法を使用します。これは、Adobe Experience Platform Launch が分析およびパーソナライゼーション用に [!DNL Experience Manager] ページを構築する役割が増大していることをサポートするもので、オプトインウィザードは機能的に無関係です。 | システム接続、Adobe IMS 認証、 [!DNL Adobe I/O Runtime] 統合を各 [!DNL Experience Manager] クラウドサービスを通じて設定します。 |
| コネクタ | Microsoft® SharePoint 2010 および Microsoft® SharePoint 2013 用の Adobe JCR Connector は、[!DNL Experience Manager] 6.5 で非推奨になりました。 | 該当なし |

## 既知の問題 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* [GraphQL インデックスパッケージ 1.0.5 を使用した AEM コンテンツフラグメント](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
GraphQL を使用するユーザーは、このパッケージが必要です。このパッケージにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

* コンテンツモデルのカスタム API 名を使用していた可能性のある GraphQL クエリを、代わりにコンテンツモデルのデフォルト名を使用するように更新してください。

* GraphQLクエリでは、 `damAssetLucene` インデックス `fragments` 索引 その結果、GraphQLクエリが失敗するか、実行に非常に長い時間がかかる可能性があります。

   問題を修正するには、 `damAssetLucene` は、次の 2 つのプロパティを含むように設定する必要があります。

   * `contentFragment`
   * `model`

   インデックス定義を変更した後、インデックス再作成が必要です (`reindex` = `true`) をクリックします。

   これらの手順の後、GraphQLクエリの実行が高速化されます。

* [!DNL Microsoft®® Windows Server 2019] は [!DNL MySQL 5.7] および [!DNL JBoss®® EAP 7.1] をサポートしていないので、[!DNL Microsoft®® Windows Server 2019] は [!DNL AEM Forms 6.5.10.0] の自動インストールをサポートしていません。

* 以下をアップグレードする場合、 [!DNL Experience Manager] 6.5.0 ～ 6.5.4 から Java™ 11 の最新のサービスパックへのインスタンスが表示されます。 `RRD4JReporter` 例外 `error.log` ファイル。 例外を停止するには、のインスタンスを再起動します。 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* アダプティブフォームでユーザーが初めてフィールドを設定する場合、設定を保存するオプションはプロパティブラウザーに表示されません。同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* [!DNL Experience Manager] 6.5.x.x のインストール中に、次のエラーや警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して [!DNL Experience Manager] に Adobe Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」／ソース「Adobe Experience Manager」タイプではなく、「HTML」／ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 登録状況を未登録に変更する処理が完了するのを待機中にタイムアウトになりました。

* コンテンツフラグメントまたはサイトやページを移動／削除／公開しようとすると、コンテンツフラグメントの参照を取得する際にバックグラウンドクエリが失敗し、機能が動作しなくなるという問題があります。
正しく動作させるには、インデックス定義ノード `/oak:index/damAssetLucene` に次のプロパティを追加する必要があります（インデックスの再作成は不要です）。

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* AEM Formsでは、POP3 プロトコルはMicrosoft® Office 365 の電子メールエンドポイントでは機能しません。
* JBoss® 7.1.4 プラットフォームで、ユーザーがAEM 6.5.16.0 Service Pack をインストールしたとき、 `adobe-livecycle-jboss.ear` デプロイに失敗しました。

## 含まれている OSGi バンドルとコンテンツパッケージ {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、[!DNL Experience Manager] 6.5.16.0 に含まれている OSGi バンドルとコンテンツパッケージの一覧が記載されています。<!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.16.0 に含まれている OSGi バンドルの一覧](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.16.0 に含まれているコンテンツパッケージの一覧](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト {#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [アドビ製品アップデートの優先通知に登録する](https://www.adobe.com/subscription/priority-product-update.html)

