---
title: AEM 6.5 Service Pack リリースノート
description: Adobe Experience Manager 6.5 Service Pack 4 固有のリリースノート
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 4bda1be676ab357c68b541dbd41f108f274dd2d7

---


# Adobe Experience Manager 6.5 Service Packリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | **Adobe Experience Manager 6.5** |
|---|---|
| バージョン | 6.5.4.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2020年3月5日 |
| ダウンロード URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/AEM-6.5.4.0-Service-Pack), [Software Distribution（ベータ版）](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.4.zip) |

## Adobe Experience Manager 6.5.4.0の機能 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.4.0は、2019年4月のGAリリース(GA)以降にリリースされた、新機能、お客様から要望のあった機能強化、パフォーマンス、安定性、セキュリティの向上を含む重要なアップデート **です**。 Adobe Experience Manager (AEM) 6.5の上にインストールできます。

AEM 6.5.4.0で導入された主な機能と強化された機能の一部を次に示します。

* AEM Assetsは、Adobe I/Oコンソールを通じてBrand Portalで設定されるようになりました。

* AEM Formsワークフローで [「印刷可能な出力を生成](../forms/using/aem-forms-workflow-step-reference.md) 」の新しい手順が使用できるようになりました。

* [アダプティブフォームと](../forms/using/resize-using-layout-mode.md) Interactive Communicationsのレイアウトモードの複数列のサポート。

* HTML5フォー [ムでのリッチ](../forms/using/designing-form-template.md) ・テキストのサポート。

* [Experience Manager Assetsのアクセシビリティ](new-features-latest-service-pack.md#accessibility-enhancements) が強化されました。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.10.8 に更新しました。

* 選択したコンテンツサブツリーを、で使用可能なすべての *ものではなく、ダイナミックメディア* - Scene7モードに同期できるようになりまし `content/dam`た。

* SOAP Webサービスとのフォームデータモデルの統合で、要素の選択グループまたは属性がサポートされるようになりました。

* SOAPの入力または出力と複雑なデータ構造で、動的グループの置換がサポートされるようになりました。

以前のAEM 6.5サービスパックで導入された機能、主な特長、主な機能の完全なリストについては、 [Adobe Experience Manager 6.5 Service Pack 4の新機能を参照してください](new-features-latest-service-pack.md)。

### Sites {#sites-fixes}

* AEMサイトページのURLにコロン(:)が含まれる場合)または割合記号(%)を使用すると、基になるブラウザーが応答を停止し、CPUサイクルがスパイクを示します(NPR-32369、NPR-31918)。

* AEMサイトページを編集用に開き、コンポーネントをコピーした場合、一部のプレースホルダー(NPR-32317)では貼り付け操作が使用できないままになります。

* パブリケーションの管理ウィザードを開くと、コアコンポーネントにリンクされたエクスペリエンスフラグメントが、公開された参照のリスト(NPR-32233)に表示されません。

* タッチ操作対応UIのライブコピーの概要は、Classic UIよりもレンダリングに時間がかかります(NPR-32149)。

* サーバー時間とマシン時間が異なるタイムゾーンにある場合、スケジュールされた公開時間はタッチUIでサーバー時間を表示し、クラシックUIではマシン時間を表示します(NPR-32077)。

* AEM Sitesは、URLにサフィックスが付いたページを開けません(NPR-32072)。

* ユーザがコンテンツフラグメントを編集すると、削除されたコンテンツフラグメントが復元される(NPR-32062)。

* ユーザーは、必須フィールドに情報を入力しないで、コンテンツフラグメントを保存できます(NPR-31988)。

* kernel.jsとui.jsは事前にコンパイルまたはキャッシュされません。 ページのレンダリングにさらに時間がかかります(NPR-31891)。

* PageEventAuditListenerが有効な場合、コミットキューの長さが長くなります。 これは、バルク投稿、ナビゲーション、バルクアセットの移動など、多くの操作のパフォーマンスに影響を与えます(NPR-31890)。

* エクスペリエンスフラグメントをドラッグすると、応答時間が長くなります(NPR-31878)。

* レスポンシブグリッドのプレースホルダーで「Drag component here」オプションを選択すると、GETリクエストが送信され、リクエストの結果HTTP 403エラーが発生します(NPR-31845)。

* 同じフォルダー内のコンテンツを移動すると、ページ移動オプションが無効になります(NPR-31840)。

* 編集可能なテンプレートの構造モードでは、レイアウトモードで許可されたコンポーネントリストに誤った結果がコンテナされて表示されます。 レイアウトコンテナ(NPR-31816)には、デザインダイアログを持つコンポーネントのみが表示されます。

* ページにユーザーの読み取り専用権限がある場合、「プロパティを開く」オプションはsites.htmlには表示されますが、editor.htmlには表示されません(NPR-31770)。

* ユーザーが「作成」ボタンをクリックすると、ページオプションは使用できません(NPR-31756)。

* OOTB（初期設定）デザインインポーターコンポーネント(NPR-31728)を含むAdobeキャンペーンのキャンペーンを同期できない。

* 箇条書きのリストを番号付きリストに変更しようとすると、リストの最初の2項目のみが変更されます(NPR-31636)。

* ページの作成が解除され、子ノードが選択された場合、選択ダイアログには初期ノードが表示されます。 ページが作成され、ユーザーが参照をクリックすると、ページは作成されたノードではなくルートノードにリダイレクトされます(NPR-31618)。

* 表示設定ダイアログボックスが、受信トレイのカスタマイズワークフロー機能（NPR-32503およびNPR-32492）で正しく機能しません。

* インボックス(CQ-4282168)を使用してワークフロー情報を表示中に、エラーメッセージが表示されます。

### アセット {#assets-6540-enhancements}

* アセット収集ページでワークフローをトリガーするボタンが無効になっています(NPR-32471)。

* Dynamic Media Scene7設定(NPR-32440)を使用してExperience Managerでアセットを別のフォルダに移動すると、名前の付いていないフォルダがSPS(Scene7 Publishing System)に作成されます。

* 「すべて選択」を使用して、公開済みアセットを含むフォルダーにすべてのアセットを移動する操作は、エラーで失敗します(NPR-32366)。

* ${extension}を含むアセットのレンディションの生成に失敗しました(NPR-32294)。

* バージョン履歴のURLは、アセットのプロパティページの「参照元」フィールドの下に表示されます(NPR-31889)。

* DAMからダウンロードしたZIPファイルをWinZip(NPR-32293)を使用して開くことができない。

* フォルダーの元の権限は、「フォルダーの設定」を開いてフォルダーのタイトルまたはサムネール画像を変更し、保存した場合に更新されます(NPR-32292)。

* スケジュールされたアクティベーションのカレンダーアイコンが、アクティベーションが後の日時にスケジュールされているアセットの「ステータス」列（DAMアセットリストのクラシックUI）に表示されない(NPR-32291)。

* スニペットテンプレートを使用したスニペットの作成で、スニペットの作成プロセス(NPR-32290)中にコレクションの検索でエラーが発生する。

* 複数の検索クエリは、検索フィルターから複数のタグが選択されると実行されます(NPR-32143)。

* ファイル名が50文字を超えるアセットがアップロードされると、Experience Manager Assets UIでファイル名が切り捨てられて表示される(NPR-32054)。

* Adobe Stockのチェックボックスツリーのレベル2のチェックボックスが選択されている場合、フィルターパネルのすべてのチェックボックスは、最初と2番目のチェックボックスがクリアされたときにクリアされます(NPR-31919)。

* Omnisearchファセットを使用したファイルとフォルダーの検索で例外が発生する(NPR-31872)。

* 対応するメタデータスキーマフォーム(NPR-31834)で依存関係ルールが設定されている場合、メタデータエディターでの必須フィールド選択のフィールドのハイライト表示が、必須フィールドの選択後も削除されません。

* （タグ階層からの）リーフレベルタグの完全な名前は、アセットのプロパティページに表示されません(NPR-31820)。

* Safariブラウザーのアセットのプロパティページで「back」コマンドを使用するとエラーが発生する(NPR-31753)。

* タッチUI検索（Omnisearchを通じて行われる）の結果ページは、自動的に上にスクロールし、ユーザーのスクロール位置が失われます(NPR-31307)。

* PDFアセットのアセットの詳細ページに、Dynamic Media Scene7の実行モードで実行されるExperience Managerの「コレクションへ」と「レンディションへ」のボタンを除き、アクションボタンが表示されません。(CQ-4286705)

* Scene7のバッチアップロード処理では、アセットの処理に時間がかかりすぎます(CQ-4286445)。

* ユーザがダイナミックメディアクライアントのセットエディタで変更を行っていない場合、「保存」ボタンを押してもリモートセットは読み込まれません。(CQ-4285690)

* 3Dアセットのサムネールは、サポートされている3DモデルがAEMに取り込まれた場合には情報とはなりません(CQ-4283701)。

* スマート切り抜きビデオビューアのプリセットが未処理の状態で、バナーテキストにプリセット名と共に2回表示されます(CQ-4283517)。

* 3Dビューアでプレビューしたアップロードされた3Dモデルのコンテナの高さが、アセットの詳細ページで正しくない場合がある(CQ-4283309)。

* Experience ManagerダイナミックメディアハイブリッドモードのIE 11でカルーセルエディターが開かない(CQ-4255590)。

* ChromeおよびSafariブラウザー(NPR-32067)のダウンロードダイアログの「電子メール」ドロップダウンで、キーボードフォーカスが動かなくなる。

* AEMにDMクラウド設定を追加しようとすると、「すべてのコンテンツを同期」チェックボックスがデフォルトで有効になりません(CQ-4288533)。

### Foundation UI {#foundation-ui-6540}

* フィルターパネル(NPR-32538)を使用してアセットを検索する際に、マウスコントロールが既存のフィルターフィールドにとどまらず、前のフィルターフィールドに移動します。

* プラットフォームのタグ付け：タグフィールドにタグを入力して検索すると、ルート境界の外側にあるタグが表示され、タグフィールドのプ `rootPath` ロパティは無視されます(NPR-31895)。

* プラットフォームUI:テキストフィールドに無効なパスが追加された場合、パスブラウザーが中断する(NPR-31884)。

* ページ選択時に、通知が共通メニューの背後に隠れる(NPR-31628)。

### プラットフォーム {#platform-sling-6540}

* (HTL)アンダースコアは、URL(NPR-32231)のパスセクションのコロンを置き換えます。

### プロジェクト {#projects-6540}

* 作成ボタンは、サブフォルダーにプロジェクトを作成する権限を持っている場合でも、ユーザーに表示されません(NPR-31832)。

### プロジェクトの翻訳 {#projects-translation-6540}

* (NPR-32154)で「スペースをトリミング」オプションがアクティブな場合、翻訳プロジェクトを作成す `Apache Sling JSP Script Handler` るとUIが壊れます。

* 翻訳対象のタグが翻訳プロジェクトに追加されると、UIのエラーとエラーログのNullポイント例外が観察される(NPR-31896)。

### 統合 {#integrations-6540}

* 起動ライブラリのURL生成は、起動API `path` の `library_name` 値と値のみに基づき、値に基づい `library_path` てはいません(NPR-31550)。

* LiveFyre関連の項目の処理中にエラーメッセージが表示されます(FYR-12420)。

### WCMテンプレートエディター {#wcm-template-editor-6540}

* 編集可能なテンプレートの構造モードで、レイアウトコンテナで許可されたコンポーネントのリストにリンクボタンコンポーネントが表示されない(CQ-4282099)。

### WCM Page Editor {#wcm-page-editor-6540}

* オーバーレイを選択し、レスポンシブグリッドの「ドラッグ」コンポーネントを選択すると、エラーが発生する(CQ-4283342)。

### Campaign Targeting {#campaign-targeting-6540}

* ターゲットクラウドの設定が失敗し、エラーget mboxリクエストが失敗しました。(CQ-4279880)

### Brand Portal {#assets-brand-portal}

* Brand Portalユーザーは、AEM 6.5.4上のAdobe I/Oにアップグレードする際に、貢献度フォルダーのアセットをAEM Assetsに公開できません(CQDOC-15655)。

   この問題は、次のサービスパックAEM 6.5.5で修正されます。

   AEM 6.5.4の即時修正を行うには、ホットフィックスをダウンロードし [て作成者インスタンス](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) にインストールすることをお勧めします。


* メタデータスキーマのドロップダウン値がアセットのプロパティに表示されない(CQ-4283287)。

* メタデータのサブスキーマで、アセットのプロパティのMIMETYPEに基づくタブが表示されません。(CQ-4283288)

* 非公開メタデータスキーマが、バックエンドでスキーマが削除されてもエラーメッセージを入力する。

* プレビューの画像が公開済みアセットに表示されない(CQ-4285886)。

* 名前に一重引用符を含むアセットを発行または非公開できない(CQ-4272686)。

* 複数のアセットのダウンロード中に利用条件が表示されない(CQ-4281224)。

* セキュリティに関する小さな脆弱性を解消。

### Communities {#communities}

* 「メンバーの作成」フォームが空白のページ(NPR-31997)として表示される。

* ユーザーが、作成者インスタンス(NPR-30913)でAnalyticsレポートの表示を実行できない。

### Oak — インデックス作成とクエリ {#oak-indexing-6540}

* JPEGドキュメントを含むMS WordおよびMS Excel画像（Tikaパーサーで解析した場合、解析に失敗し、クラスが見つかりません）のエラーが表示される(NPR-31952)。

### Forms {#forms-6530}

>[!NOTE]
>
>AEM サービスパックには、AEM Forms の修正は含まれません。別の Forms アドオンパッケージを使用して配布されます。さらに、JEE上のAEM Formsの修正を含む累積インストーラーがリリースされました。 For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Correspondence Management:後処理ワークフロー(NPR-32626)に送信した後、レターに余分な文字が表示されます。

* Correspondence Management:レターは、後処理ワークフロー(NPR-32539)に送信した後、テキストコンポーネントとしてドロップダウンプレースホルダーを表示します。

* Correspondence Management:レターテンプレートで定義されているデフォルト値は、プレビューモード(NPR-32511)では表示されません。

* Mobile Forms:HTMLバージョン(NPR-32514)でXDPフォームをレンダリングする際、送信ボタンのサイズが拡張されて表示されます。

* ドキュメントサービス：Service Pack 2(NPR-32508、NPR-32509)を適用した後のLettersおよびその他のページのURLアクセスの問題。

* ドキュメントサービス：サーバー上のトランザクションの数が特定の制限を超えると、HTMLからPDFへの変換は失敗し、ファイルタイプの設定がAEM Formsサーバー(NPR-32204)から削除されます。

* アダプティブフォーム：WCAG2 Level AAのガイドライン(NPR-32312、NPR-32309、CQ-4285439)に従って、ブラウザーのアクセシビリティツールがアダプティブフォームでエラーを報告します。

* アダプティブフォーム：Chromeブラウザーのアクセシビリティツールが、ベストプラクティスの失敗を報告します(NPR-32310)。

* アダプティブフォーム：AEMサイトページに埋め込まれたアダプティブフォームの設定中に、翻訳の問題が発生する(NPR-32168)。

* Workbench:PDF Utilitiesサービス(NPR-32150)で「Get PDF Properties」操作を使用しているときに、エラーメッセージが表示されます。

* ドキュメントセキュリティ：DisableGlobalOfflineSynchronizationDataオプションがTrueに設定されている場合、保護されたPDFファイルをオフラインで開くことができない(NPR-32078)。

* Designer:タグ付けオプションが有効な場合、生成されたPDF出力(NPR-32547、NPR-31983、NPR-31950)でサブフォームの境界線が消えます。

* Designer:表に結合されたセルがある場合、アクセシビリティテストは、出力サービスを使用してXDPフォームから変換された出力PDFファイルに対して失敗します。(CQ-4285372)

* Foundation JEE:AEM Formsサーバーがクラスターから切断された場合、キャッシュの問題によりサーバーに再接続できなくなります(NPR-32412)。

## Install 6.5.4.0 {#install}

**セットアップ要件**

* AEM 6.5.4.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* サービスパックは AEM 6.5 インスタンスから直接アクセスできるパッケージ共有からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.5.4.0 をインストールしてください。
* サービスパックをインストールする前に、AEM インスタンスのスナップショットまたは新規バックアップを必ず作成します。
* インストールする前にインスタンスを再起動してください。これは、インスタンスがまだ更新モードになっている場合（インスタンスが以前のバージョンから更新されたばかりの場合）にのみ必要ですが、インスタンスが長期間実行されていた場合にはお勧めします。

>[!CAUTION]
>
>AEM 6.5.4.0 パッケージを削除またはアンインストールすることはお勧めしません。

### パッケージ共有による Service Pack のインストール {#install-service-pack-via-package-share}

既存の AEM 6.5 インスタンスに Service Pack をインストールするには、次の手順を実行します。

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.4.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/AEM-6.5.4.0-Service-Pack).

1. パッケージマネージャーを使用してダウンロードしたパッケージをインストールします。

>[!NOTE]
>
>**6.5.4.0 のインストール中に、パッケージマネージャー UI のダイアログが途中で終了することがあります。**
>
>そのため、エラーログが安定するのを待ってから、インスタンスにアクセスすることをお勧めします。ユーザーは、アップデーターバンドルのアンインストールに関連する特定のログを待ってから、インストールが正常に行われることを確認する必要があります。 通常は、Safari で発生しますが、任意のブラウザーで断続的に発生する可能性があります。

**自動インストール**

実行中のインスタンスに AEM 6.5.4.0 を自動的にインストールするには、次の 2 つの方法があります。

A.パッケージを。.*サーバーがオンラインで使用可能な間、* /crx-quickstart/installフォルダーを作成します。 パッケージは自動的にインストールされます。

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.4.0 では、ブートストラップインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ(/system/console/ productinfo)の「インストール済み製品」に、更新されたバージョン文字列 `Adobe Experience Manager, Version 6.5.4.0` が表示されます。

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. OSGIバンドルorg.apache.jackrabbit.oak-coreはバージョン1.10.6以降です(Use Web Console:/system/console/bundles)。

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>AEM Forms を使用していない場合はスキップしてください。AEM Forms の修正は、個別のアドオンパッケージを介して配信されます。

>[!NOTE]
>
>AEM 6.5.4.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). 古いバージョンのAEM Forms互換性パッケージを使用し、AEM 6.5.4.0にアップデートする場合は、Formsアドオンパッケージのインストール後に、最新バージョンのAEM Forms互換性パッケージをインストールします。

1. AEM Service Pack がインストールされていることを確認してください。
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE上のAEM Formsに関する修正は、別のインストーラーを使用して提供されます。

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0011](https://helpx.adobe.com/jp/aem-forms/quick-fixes/6-5/jee-patch-0011.html).

#### Workbench インストーラー

これはフルインストーラーなので、パッチバージョンよりもファイルサイズが大きくなります。新しいWorkbenchをインストールする前に、以前のバージョンのWorkbenchをアンインストールします。

### UberJar {#uber-jar}

The UberJar for AEM 6.5.4.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4/).

**com.fasterxml.jackson.core.asyncパッケージを含む、6.5.4.0の更新されたUberJarバージョンは、** Adobe Public Mavenリポジトリで入手できます [](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4-1.0/)。

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.4</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

この節では、AEM 6.5.4.0で非推奨とマークされた機能に関するリストを説明します。今後のリリースで削除される予定の機能は、まず非推奨に設定され、別のオプションを使用するようになります。

お客様は、現在の導入で機能を利用しているかどうかを確認し、別のオプションを使用するように実装を変更する計画を立てることをお勧めします。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. AEMとターゲットの統合がAEM 6.5で更新され、Adobe IMSとI/Oを介した認証を使用するターゲット標準APIがサポートされるようになりました。また、Adobe Launchの役割が増え、分析とパーソナライゼーションのためのAEMページの実装が増えています。 | 各AEMクラウドサービスを介したシステム接続、Adobe IMS認証、Adobe I/O統合の設定 |

## 既知の問題 {#known-issues}

* 接続さ **れたアセットの設定** ウィザードがインストール後に404エラーメッセージを返す場合は、Package Managerを使用して、 **cq-remotedam-client-ui-content** および **** cq-remotedam-client-ui-componentsパッケージを手動で再インストールします。
* AEM 6.5.x.xのインストール中に、次のエラーメッセージと警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して AEM に Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * com.adobe.granite.maintenance.impl.TaskScheduler : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計機能が使用されると、アダプティブフォームのサーバー側の検証に失敗します。 CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

次のドキュメントには、AEM 6.5.4.0 に含まれている OSGi バンドルとコンテンツパッケージの一覧が記載されています。

AEM 6.5.4.0 に含まれている OSGi バンドルの一覧

[ファイルを入手](assets/6540_bundles.txt)

AEM 6.5.4.0 に含まれているコンテンツパッケージの一覧

[ファイルを入手](assets/6540_packages.txt)

## Restricted sites {#restricted-sites}

以下のサイトは既存ユーザーのみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [カスタマーサポート](https://daycare.day.com/public/contact.html)へのお問い合わせサポートポータルへのアクセスについて詳しくは、「サポートポ [ータルへのアクセス](https://helpx.adobe.com/jp/experience-manager/kb/accessing-aem-support-portal.html)」を参照してください。

>[!MORE 気に入った]
>
>* [AEM 6.5 リリースノート](/help/release-notes/release-notes.md)
>* [AEM 製品ページ](https://www.adobe.com/solutions/web-experience-management.html)
>* [AEM 6.5 ドキュメント](https://helpx.adobe.com/jp/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

