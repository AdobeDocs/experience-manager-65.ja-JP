---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: '"[!DNL Adobe Experience Manager] 6.5 リリース情報、新機能、インストール方法、および詳細な変更リストの概要を説明するノート。」'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 9a3f26b6709461a911e833f7e340d11c759c7dae
workflow-type: tm+mt
source-wordcount: '3180'
ht-degree: 36%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.12.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2022年2月24日（PT） |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip) |

## [!DNL Adobe Experience Manager] 6.5.12.0 の内容 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.12.0 には、2019年4月の 6.5 リリースの公開以降にリリースされた新機能、お客様からリクエストされた主な機能強化およびパフォーマンス、安定性、セキュリティの向上が含まれています。サービスパックは [!DNL Adobe Experience Manager] 6.5 にインストールされています。

[!DNL Adobe Experience Manager] 6.5.12.0 に導入された主な機能および機能強化は次のとおりです。

* リモート DAM と Sites デプロイメント間の接続を設定すると、リモート DAM 上のアセットが Sites デプロイメントで使用できるようになります。 リモート DAM のアセットまたはフォルダーに対して、更新、削除、名前変更、移動の操作を実行できるようになりました。 更新は、少し遅れて、Sites デプロイメントで自動的に利用可能になる (NPR-37816)。

* ブループリント設定を必要とせずに、ライブコピーソースを複数のライブコピーにプッシュロールアウトできるようになりました (CQ-4259951)。
* ユーザーが同じパス上で誤って複数の非同期操作をトリガーするのを防ぐために、進行中の非同期操作のステータスがユーザーインターフェイスに表示されるようになりました (NPR-37611)。
* Analytics 2.0 API に対して、IMS ベースの認証のサポートが提供されます (CQ-4285474、NPR-37803、NPR-37701、NPR-37702、NPR-37703)。
* JSON オファータイプのエクスペリエンスフラグメントの API のサポート (NPR-37796)。
* IMS の削除オファー（エクスペリエンスフラグメント API）に対してオファーリクエストが提供されるようになりました。(NPR-37668)
* 組み込みリポジトリ (Apache Jackrabbit Oak) は、引き続き1.22.9にあります。

[!DNL Experience Manager] 6.5.12.0 リリースで提供される修正のリストは次のとおりです。

### [!DNL Sites] {#sites-65120}

[!DNL Sites] で、以下の問題を修正しました。

* 「基本」タブと「詳細」タブには左側に余白がないので、コンテンツフラグメントのプロパティのレイアウトは壊れます (SITES-4484)。
* 様々なサイトページで参照されるコンテンツフラグメントのバナーを閉じるオプションが機能しません。 このバナーは、コンテンツフラグメントが 1 つ以上のページで参照されていることをユーザーに通知します (SITES-4173)。
* 継承を元に戻すダイアログボックスで、チェックボックスが揃っていません (SITES-3514)。
* pageinfo.json サーブレットが LaunchManagerImpl.getLaunchStream(SITES-3489) で停止しているので、we-retail サイトと wknd サイトのテンプレートページは、コンポーネントが読み込まれず、構造オプションを使用できないので、壊れています。
* オーサー環境からパブリッシュ環境へのユーザーノードの公開が機能しない (NPR-38005)。
* 編集されたテンプレートを使用してエクスペリエンスフラグメントを作成しようとしても、初期ページのプロパティに対して行われた編集が表示されない (NPR-37962)。
* Experience Managerのページ移動操作が遅い (NPR-37961)。
* エクスペリエンスフラグメント翻訳が言語コピーパスへの参照を更新しない (NPR-37953)。
* レプリケーション権限を持たないユーザーは、ページがアクティベートされていない場合でも、ページを削除または移動できない (NPR-37936)。
* ランダムな org.apache.felix.metatype エラーがサーバーで発生する (NPR-37935)。
* サイト管理タッチユーザーインターフェイスの参照で、受信リンクが正しく表示されない (NPR-37934)。
* 翻訳ジョブでページを選択する際に、新しいページまたはアセットを追加するための起動パスが利用できない。(NPR-37912)
* ローンチの昇格時に、エクスペリエンスフラグメントに追加されたリストコンポーネント内の参照ページが、宛先ページに更新されない。(NPR-37886)
* オーサー環境にはユーザーインターフェイスに関する問題があります。例えば、編集モードのページタイトルが中央に配置されず、ポリシーエディター上で許可されるコンポーネントセレクターがあります。「グループ」チェックボックスはコンテナの幅全体を取り込むので、ラベルは次の行にレンダリングされる。(NPR-37878)
* [Platform] commons-httpclient の metatype.xml ファイルの xmlns:metatype のバージョン番号は、「http://www.osgi.org/xmlns/metatype/v1.2.0」ではなく「http://www.osgi.org/xmlns/metatype/v1.0.0」です (NPR-37865)。
* エラーが表示され、ページに移動しようとするとページが移動しない (NPR-37864)。
* [リッチテキストエディター] 画像をリッチテキストエディターでリスト項目として追加する際に、画像がクラシックユーザーインターフェイスでレンダリングされない (NPR-37835)。
* 作成者は、ダイアログでタグフィールドを使用する際に、設定されたルートパスの外にあるタグを適用できる。(NPR-37834)
* マルチフィールドがレイアウトコンテナで正しくレンダリングされず、エラーが発生する (NPR-37811)。
* ページエディターでコンポーネントレイアウトのサイズを変更しようとしても、モバイルレイアウトで機能しない (NPR-37805)。
* エクスペリエンスフラグメント翻訳で、言語コピーパスへの循環参照が更新されない。(NPR-37745)
* ページプロパティで cq-msm-lockable リッチテキストフィールドを使用しても、ページのロールアウト時にフィールドが無効にならず、作成者が変更できる。(NPR-37714)
* エクスペリエンスフラグメントをアクティブ化すると、パブリッシャーが多数のアクティベーション要求を Dispatcher に送信する (NPR-37707)。
* トポロジの変更時に、アセット処理の Sling ジョブがリセットされ、トポロジの変更時に進行中のジョブが無視される (NPR-37706)。
* MacOSの書き出しサイトとアセットの URL のユーザーが CSV に書き出す際に、引用符、クロス、ダッシュが CSV に書き出されない。(NPR-37698)
* SPAページテンプレートのレイアウトコンテナが、React SPAページの実行時に、テンプレートポリシーで定義されたカスタム CSS クラスを登録できない。(NPR-37697)
* コンテナ内のバックグラウンドを持つエクスペリエンスフラグメントでターゲティングを選択すると、背景画像が表示されない。(NPR-37662)
* エクスペリエンスフラグメントの翻訳ジョブが、そのエクスペリエンスフラグメントのすべてのコンポーネントを翻訳していない (NPR-37660)。
* エクスペリエンスフラグメントの翻訳と、エクスペリエンスフラグメントを含むページが、エクスペリエンスフラグメントリンクのローンチパスを更新しない。(NPR-37659)
* ファイルのアップロードウィジェットは、ファイルがアップロードされ、ダイアログが保存されたときに、ファイル名を表示しない (NPR-37634)。
* アセットを含むフォルダーを移動した場合、そのアセットのスケジュールされたアクティベーション（公開）がスケジュールされた時間にトリガーされない (NPR-37621)。
* [Platform] 外部リンクチェッカーダッシュボードで結果のレンダリングに失敗 [!DNL Adobe Experience Manager] WCM(NPR-37614)。
* エディターでタグを編集する際に、タグ名で大文字の文字が使用されている場合、コンテンツフラグメントエディターが正しく機能しない (NPR-37601)。
* クラシックユーザーインターフェイスエディターで、タッチユーザーインターフェイスの比較ビューにマークが表示されない (NPR-37588)。
* 間欠的な 500 エラーが、翻訳ジョブにエクスペリエンスフラグメントを追加する際に記録される (NPR-37587)。
* 作成者は、無効な日付ピッカーでも日付選択の日付を選択して使用できます (NPR-37583)。
* [Foundation] 作成者が、タッチユーザーインターフェイスのコンポーネントダイアログ構造の数値フィールドリソースタイプに、一部の小数値を入力できない。(NPR-37059)
* 以前のサービスパックのインストール時に libs フォルダー内のパスが削除される (NPR-36815)。
* [コマース] ルートフォルダーのアクティベートを解除しても、 [!DNL Experience Manager Commerce] コンソールまた、非アクティブ化時のルートフォルダーの子フォルダーの数が、ユーザーインターフェイスに誤って表示される (CQ-4338261)。
* [ローカリゼーションワークフロー] 列のカスタマイズとブランディングのカスタマイズの内容が、管理コントロールダイアログ ( [!DNL Adobe Experience Manager] インボックス (CQ-4334864)。
* [コミュニティ] グループメンバー用のテーブル内のコンテンツをクリックできません (CQ-4334404)。
* [Oak] コールドスタンバイ同期プロセスが機能せず、エラーをログに記録しています (CQ-4333868)。
* [Platform Foundation UI] [!DNL Experience Manager] ユーザーが選択すると、開始ページが再び表示されます [!DNL Adobe Experience Manager] アイコンが既に開始ページに表示されています (CQ-4317409)。
* （レプリケーション権限を持たない）ユーザーが（ページがアクティベートされていない場合でも）ページを削除または移動する場合、 `Page Subtree Activation Check` 設定で `Page Manager Factory` を有効にする必要がある (NPR-37936)。

### [!DNL Assets] {#assets-65120}

<!--
The following accessibility enhancements are available in [!DNL Assets]:

* enhancement 1
-->

[!DNL Assets] で、以下の問題を修正しました。

* アセットまたはフォルダー ( `single quote` （名前）「Connected Assets」で、参照パスが失敗し、例外として返される (NPR-37712)。
* アセットに透かしを追加する場合、ユーザーが定義した色に関係なく、透かしは常に黒で表示される (NPR-37720)。
* Connected Assets を使用する場合、管理者以外のユーザーが DAM リポジトリへのアクセスを制限されている場合でも、管理者以外のユーザーがアセットを検索できます (NPR-37644)。
* 一括編集を使用してアセットメタデータを更新する場合、ドロップダウンフィールドに適用された変更が保存されず、デフォルト値にリセットされる (NPR-37345)。
* フォルダーの削除に時間がかかりすぎて、全体的なパフォーマンスに影響する (NPR-37107)。
* メタデータスキーマでルールを適用すると、ユーザーはドロップダウンの完全な値を表示できません `Field Value` および `Field Choices` 値がテキストボックスより大きい場合 (CQ-4338074)。
* バージョン 6.5.10.0にアップグレードすると、アセットのプロパティページに不要なHTMLレンダリングメッセージが表示されます (CQ-4336994)。
* でのアセットの並べ替え `List View` は効果的に機能しません (CQ-4335298)。
* 共有リンクを使用してアセットを共有する場合は、アセットが別のフォルダーにダウンロードされます (CQ-4335000)。
* 検証時に [!DNL Experience Manager] `Inbox` 設定 `Share` および `Out of office` タブに未翻訳のコンテンツが反映されます (CQ-4334858)。

* 次の修正は、アセットプロパティのカスケードメタデータに関連しています。
   * 必須ドロップダウンは、複数値フィールドの各選択に対して複数のエラーメッセージを反映します (NPR-37859)。
   * 親フィールドの最後の選択のみが、依存する編集不可フィールドに対して保存される (NPR-37858)。
   * 依存するドロップダウン（複数値フィールド）は、選択した親ドロップダウンのデフォルト値を断続的に反映します (NPR-37791)。

### [!DNL Dynamic Media] {#dynamic-media-65120}

[!DNL Dynamic Media] で、以下の問題を修正しました。

* を含むフォルダーのアセット `renditions` のフォルダー名は、で同期されません `Dynamic Media` (CQ-4338428)。
* で画像プリセットを作成する場合 `tiff` 形式の場合、プリセットは作成されますが、形式は `jpeg` (CQ-4335985)。
* を変更する場合 `Progressive JPEG Scan` の値を指定すると、ドロップダウンの値は常ににリセットされます。 `auto`(CQ-4335971)。
* のビデオメタデータは表示されません `mxf` アセットのプロパティページのビデオ (CQ-4335499)。
* ビデオアセットを再処理すると、AVS（アダプティブビデオセット）とビデオレンディションがパブリッシュサーバーから非公開になります (CQ-4335461)。
* 生成されるPDFのサムネールは、実際のPDFの最初のページとは異なります。 画像の一部がサムネールに表示されません (CQ-4315554)。
* CDN 無効化は、 `companyName` および `companyRoot` が異なる (CQ-4339896)。

### ワークフロー {#workflows-65120}

* インボックス項目にフィルターを適用した場合、スクロールが期待どおりに機能しません (CQ-4333594)。

### [!DNL Forms] {#forms-65120}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] サービスパックリリース日の 1 週間後にアドオンパッケージをリリースします。


**アダプティブフォーム**

* アダプティブフォーム内のテキストコンポーネントにテーブルが含まれている場合、そのコンポーネントにコンテンツを貼り付けると、エディター内のテーブルが消去される (NPR-38078)。

* フォームは、保存されたフォームを開いた場合にのみツールバーを表示する (NPR-38060)。

* 取り消し操作がルールエディターに対して正しく動作しない (NPR-37973)。

* `getAemFormContainer` AEM Forms 6.5.10.0のインストール後に null ポインタを返す (NPR-37881)。

* アクセシビリティ — スクリーンリーダーは、フィールドをクリックした場合にのみ通知するのではなく、タブフォーカスがフィールドに移るとすぐに、テキストボックスの長い説明を通知する。(NPR-37855)

* テキストボックスに対して「リッチテキストを許可」プロパティを有効にすると、許可されている文字の長さの上限に問題が生じます (NPR-37825)。

* アダプティブフォーム内の任意のコンポーネントをコピーする際に CSS が発生する (NPR-37812)。

**フォームデータモデル**

* フォームデータモデルに接続されたアダプティブフォームの添付ファイルをデータベースに保存する際に問題が発生します (CQ-4338561)。

**インタラクティブコミュニケーション**

* 「参照」タブに、インタラクティブ通信内の参照が一覧表示されない (NPR-37995)。

**Document Services**

* Assembler が、期待どおりにフォントを埋め込まない (NPR-38056)。

* ワークベンチを使用してPDFを PDFA に変換できない (NPR-37879)。

* AEM 6.5.7.0 FormsからAEM 6.5.10.0 Formsにアップグレードした後の、PDFジェネレーターサービスの使用中に Office ドキュメントに関する問題 (NPR-37758)。

**Document Security**

* PDFの暗号化は、java バージョン 1.8.0_281 にアップグレードした後は機能しません (NPR-37716)。

**Foundation JEE**

* AEM 6.5.7.0 Formsのランダムな時間の経過後に、マルチスレッドPDFジェネレーターサービスのデッドロックが発生する (NPR-38053)。

* AEM Workbench バージョン 6.5.0.20210518.1.338459では、電子メールのスタートポイントを使用し、ユーザー名とパスワードを編集した場合、設定は保存されません (NPR-37967、CQ-4336081)。

* ログを保存すると、CPU 使用率が高くなり、サーバーの再起動が必要になる (NPR-37868)。

* `Gemfire.log` は `temp\adobejb_server1\Caching` AEM Forms-6.5.0-0038 のインストール後のフォルダー (CQ-4340237)。

* 次のエラーは、 `ConfigurationManager.sh` コマンド (CQ-4338323):

   ```TXT
     [root@localhost bin]# ./ConfigurationManager.sh 
     bash: ./ConfigurationManagerCLI.sh: /bin/sh^M: bad interpreter: No such file or directory
   ```

* RHEL8 上のAEM 6.5 Formsは、JBOSS EAP 7.3 および MySQL8(CQ-4331770) をサポートしていません。

**ワークフロー**

* AEM 6.5.10.0 Formsパブリッシュインスタンスのワークフローの一部として UTF-8 特殊文字を保存する際の問題 (NPR-37673)。

* ArrayList タイプと JSON サブタイプの変数を作成する際に問題が発生する (NPR-37600)。

* AEM 6.5.9.0 FormsおよびAEM 6.5.10.0 Formsのワークフローの「変数を設定」手順での XPath/Dot 表記ブラウザーの問題 (CQ-4336582)。

セキュリティ更新について詳しくは、[[!DNL Experience Manager] セキュリティ情報ページ](https://helpx.adobe.com/jp/security/products/experience-manager.html)を参照してください。

## 6.5.12.0 のインストール {#install}

**設定要件と詳細情報**

* Experience Manager 6.5.12.0 には Experience Manager 6.5 が必要です。詳しくは、[アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに Experience Manager 6.5.12.0 をインストールしてください。

>[!NOTE]
>
>アドビは、[!DNL Adobe Experience Manager] 6.5.12.0 パッケージを削除またはアンインストールすることはお勧めしません。

### サービスパックのインストール {#install-service-pack}

[!DNL Adobe Experience Manager] 6.5 インスタンスにサービスパックをインストールするには、次の手順に従ってください。

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip)からサービスパックをダウンロードします。

1. パッケージマネージャーを開き、「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。詳しくは、 [パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。 [Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。 Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでもときどき発生する場合があります。

**自動インストール**

実行中のインスタンスに [!DNL Experience Manager] 6.5.12.0 を自動的にインストールするには、次の 2 つの方法があります。

A. サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。パッケージが自動的にインストールされます。

B. [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Adobe Experience Manager 6.5.12.0では、Bootstrap のインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.12.0)` が表示されます。

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.3 以降です（web コンソールを使用：`/system/console/bundles`）。

このリリースでの動作が認定されたプラットフォームについては、 [技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

### Adobe Experience Manager Formsアドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Experience Manager Formsを使用していない場合はスキップします。 Experience Manager Formsでの修正は、スケジュールされた週の後に、個別のアドオンパッケージを通じて配信されます [!DNL Experience Manager] Service Pack リリース。

1. Adobe Experience Manager Service Pack がインストールされていることを確認します。
1. [AEM Forms リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. Formsアドオンパッケージをインストールします。詳しくは、 [AEM Formsアドオンパッケージのインストール](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### JEE でのAdobe Experience Manager Formsのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE 上のAdobe Experience Manager Formsの修正は、別のインストーラーを通じて提供されます。

JEE 上のExperience Manager Formsの累積インストーラーのインストールとデプロイ後の設定について詳しくは、 [リリースノート](jee-patch-installer-65.md).

>[!NOTE]
>
>JEE 上のExperience Manager Formsの累積インストーラーをインストールした後、最新のFormsアドオンパッケージをインストールし、次の場所からFormsアドオンパッケージを削除します。 `crx-repository\install` フォルダーを開き、サーバーを再起動します。

### UberJar {#uber-jar}

Experience Manager 6.5.12.0 の UberJar は、 [Maven Central リポジトリー](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.12/)で入手できます。

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めてください。

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.12</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。 メインの UberJar ファイルの名前は、「`uber-jar-<version>.jar`」に変更されます。ですので `classifier` がなく、値として `apis` を `dependency` タグに使用します。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

[!DNL Experience Manager] 6.5.7.0 で非推奨（廃止予定）とマークされた特徴と機能のリストは次のとおりです。 これらの機能は、最初は非推奨とマークされ、将来のリリースでは削除されます。別のオプションが提供されます。

デプロイメントでその特徴または機能を使用しているかどうかを確認します。 また、別のオプションを使用するように、実装の変更を計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | Experience Manager 6.5 で [!DNL Experience Manager] と [!DNL Adobe Target] の統合が更新されたことにより、**[!UICONTROL AEM クラウドサービスのオプトイン]**&#x200B;画面は非推奨になりました。この統合では、Adobe Target Standard API をサポートしています。 この API は、Adobe IMS と [!DNL Adobe I/O] による認証を使用し、Adobe Launch の高まる役割をサポートして、分析とパーソナライズ機能のために [!DNL Experience Manager] のページを構築できるようにします。オプトインウィザードは機能的に無関係です。 | システム接続、Adobe IMS 認証、 [!DNL Adobe I/O] 統合を各 [!DNL Experience Manager] クラウドサービスを通じて設定します。 |
| コネクタ | Microsoft® SharePoint 2010 および Microsoft® SharePoint 2013 用の Adobe JCR Connector は、Experience Manager 6.5 で非推奨になりました。 | 該当なし |

## 既知の問題 {#known-issues}

* コンテンツフラグメントと GraphQL を使用している場合は、6.5.12.0の上に次のパッケージをインストールすることをお勧めします。

   * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip)

   * [GraphQL インデックスパッケージ 1.0.3 を使用したAEMコンテンツフラグメント](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* [!DNL Microsoft Windows Server 2019] は [!DNL MySQL 5.7] および [!DNL JBoss EAP 7.1] をサポートしていないので、[!DNL Microsoft Windows Server 2019] は [!DNL AEM Forms 6.5.10.0] の自動インストールをサポートしていません。

* [!DNL Experience Manager] インスタンスを 6.5 から 6.5.10.0 バージョンにアップグレードする場合は、`error.log` ファイルで `RRD4JReporter` の例外を表示できます。この問題を解決するには、インスタンスを再起動します。

* [!DNL Experience Manager] 6.5 Service Pack 10 または以前の Service Pack を [!DNL Experience Manager] 6.5 にインストールすると、アセットのカスタムワークフローモデル（`/var/workflow/models/dam` に作成）のランタイムコピーが削除されます。
ランタイムコピーを取得するには、HTTP API を使用して、カスタムワークフローモデルの設計時コピーとランタイムコピーを同期させることをお勧めします。
   `<designModelPath>/jcr:content.generate.json`

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* アダプティブフォームでユーザーが初めてフィールドを設定する場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* Experience Manager 6.5.x.x のインストール中に、次のエラーや警告メッセージが表示される場合があります。
   * Target Standard API（IMS 認証）を使用して Experience Manager に Adobe Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」/ ソース「Adobe Experience Manager」タイプではなく、「HTML」/ ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 登録の変更が完了するのを待機中のタイムアウトが未登録になりました。

* コンテンツフラグメントまたは Sites/Pages のいずれかを移動/削除/公開しようとすると、バックグラウンドクエリが失敗したため、コンテンツフラグメント参照を取得する際に問題が発生する。つまり、機能が動作しません。
正しい操作を確実におこなうには、次のプロパティをインデックス定義ノードに追加する必要があります `/oak:index/damAssetLucene` （インデックスの再作成は不要） :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## 含まれている OSGi バンドルとコンテンツパッケージ {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、[!DNL Experience Manager] 6.5.12.0 に含まれている OSGi バンドルとコンテンツパッケージの一覧が記載されています。

* [Experience Manager 6.5.12.0 に含まれている OSGi バンドルの一覧](assets/65120_bundles.txt)

* [Experience Manager 6.5.12.0 に含まれているコンテンツパッケージの一覧](assets/65120_packages.txt)

## 制限付き Web サイト {#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* 詳しくは、 [アドビカスタマーサポートへのお問い合わせ方法](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)を参照してください。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [アドビ製品アップデートの優先通知に登録する](https://www.adobe.com/subscription/priority-product-update.html)

