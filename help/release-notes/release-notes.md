---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: '"[!DNL Adobe Experience Manager] 6.5 リリース情報、新機能、インストール方法、および詳細な変更リストの概要を説明するノート。」'
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: a45d66dc2226dbe2879aa61d95cc5379dce882bb
workflow-type: tm+mt
source-wordcount: '3774'
ht-degree: 26%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.13.0 |
| タイプ | Service Pack リリース |
| 日付 | 2022年5月26日（PT） |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip) |

## [!DNL Experience Manager] 6.5.13.0 の内容 {#what-is-included-in-aem}

[!DNL Experience Manager] 6.5.13.0には、2019 年 4 月の 6.5 の初期リリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善が含まれています。 [このサービスパックをインストール](#install) オン [!DNL Experience Manager] 6.5.

[!DNL Adobe Experience Manager] 6.5.13.0 に導入された主な機能および機能強化は次のとおりです。

* アダプティブフォーム内で非表示の CAPTCHA を使用します。不明な CAPTCHA を使用して、疑わしいアクティビティが発生した場合にのみ CAPTCHA チャレンジを表示できるようになりました。 疑わしいアクティビティが見つからない場合、CAPTCHA チャレンジは表示されません。 これにより、チェックボックス要件を持たずに人間がフォームを完成させたかどうかを評価し、カスタマイズ作業を軽減し、エンドユーザーエクスペリエンスを向上させることができます。 (NPR-38500)

* REST エンドポイント用のフォームデータモデル後処理での応答ヘッダーの取得のサポートが追加されました。 (NPR-38275)

* これで、アダプティブフォームの翻訳ファイルを生成する際に、生成される XLIFF ファイルと、対応するアダプティブフォーム内のコンポーネントのシーケンスが同じテキストのシーケンスになります。 (NPR-37700)

* アダプティブフォームをローカライズして、ベース言語のテキストに小さな変更を加えた場合、他のすべての言語で完全な翻訳が見つからなくなります。 この問題は、 [!DNL Experience Manager] 6.5.13.0. (NPR-37189)

* Formsのアクセシビリティの改善：

   * スクリーンリーダーが、テーブルのヘッダーと本文を連続エンティティと接続エンティティとして認識できるようになりました。 スクリーンリーダーでテーブルを適切に移動するのに役立ちます。 (NPR-37139)
   * ダイアログが開くまでHTMLワークスペース内を移動しないようにするスクリーンリーダーのサポートを追加しました。 (NPR-37134)
   * Forms Designer で、ハイパーリンクの画面Readerテキストを指定する機能が追加されました。(NPR-36221)

次のバグ修正、主な機能、機能強化が [!DNL Experience Manager] 6.5.13.0:

<!-- The following issues are fixed in [!DNL Experience Manager] 6.5.13.0: -->

## [!DNL Assets] {#assets-6513}

* 読み取り専用のドロップダウンフィールドを編集しようとすると、ドロップダウン値が空にリセットされる。 (NPR-38389)
* ビデオファイルにオーディオがない場合、ユーザーはビデオ (.mp4) アセットを取り込めません。 DAM アセットの更新ワークフローが失敗し、エラーメッセージが反映されます。 (NPR-38116)
* アセットを移動ウィザードを使用してアセットを含むフォルダーを移動すると、ワークフローが失敗し、エラーメッセージが表示されます。 (NPR-38061)
* FFmpeg トランスコーディングワークフローが FLV ビデオプロファイルで失敗する。 （CQ-4343249）
* に更新した後 [!DNL Experience Manager] 6.5 SP10 の場合、アセットメタデータエディターが正しく動作していません。 （CQ-4341359）
* 検索フィルターを「公開」として適用して保存したスマートコレクションを開くと、検索フィルターが自動的に「非公開」に変わります。 （CQ-4341191）
* で言語を切り替える場合 **[!UICONTROL ユーザーの環境設定]**、ラベル **[!UICONTROL 並べ替え基準]**、ドロップダウンボタン、およびアセットホームページ上の並べ替えオプション内のその他のオプションは、選択した言語には反映されません。 （CQ-4339306）
* ルールを **[!UICONTROL メタデータスキーマ]**、 **[!UICONTROL 依存]** リストには、ドロップダウンのフィールドラベルが反映されません。 (ASSETS-9442)
* アセットのメタデータドロップダウンが無効になり、値が保持されない。 (ASSETS-8918)
* を使用してアセットを表示する場合 **[!UICONTROL 詳細]** オプション **[!UICONTROL 列]** ビュー、誤った注釈が表示されます。 (ASSETS-8851)
* 異なるバージョンで重複したアセットを作成する場合、それらのレンディションは生成されません。 (ASSETS-8607)

* 管理者以外のユーザーは、別のユーザーが既にチェックアウトしているアセットを公開できます。 (NPR-38128)
* ディメンショナルビューアは、Chrome 97 では機能しません。 （CQ-4340456）
* アセットのダウンロードボタンが、アセットの詳細ページに完全なメニューを表示しない。 （CQ-4336703）
* リンク共有を使用する場合、リンク共有ウィンドウの一部の文字列がローカライズされません。 （CQ-4330540）
* 「公開を管理」で項目を追加する場合、選択した項目の数を反映する文字列はローカライズされません。 （CQ-4330491）

### [!DNL Dynamic Media] {#dynamic-media-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Zero day exploit with the Java™ Spring Core Framework (CVE-2022-22963) impacting Experience Manager 6.5.12. (ASSETS-9031) -->
* AEM オーサーインスタンス上のDynamic Media Assets 用のトークンベースのセキュアプレビュー。 (ASSETS-4995)
* でDynamic Mediaの画像プリセットを作成する際 [!DNL Experience Manager]の場合、ユーザーインターフェイスで許可される最大値は 2000 x 2000 ピクセルに制限されます。 幅または高さの値を 2001 ピクセルに増やした場合、 **[!UICONTROL 保存]** 」ボタンが非アクティブになっている。 (ASSETS-5691)
* ユーザーは、特定のファイル形式がDynamic Mediaにアップロードされないようにすることができます。 (ASSETS-5693)
* アクセシビリティ — 画像プリセットユーザーインターフェイスの画像に Alt 属性が実装されていない場合、スクリーンリーダーに依存する視覚的に異なるユーザーが影響を受けます。 (ASSETS-9817)
* アクセシビリティ — スクリーンリーダーが、下向き矢印モードでに移動したときに、「タイムラインセグメント」と「アクション」タブに存在する画像に対して、ラベルのない画像を読み上げると、影響を受けます。 (ASSETS-5651)
* アクセシビリティ — （参照/カーソル）モードを使用して移動する際に、スクリーンリーダー (NVDA/JAWS) が、ビデオプレーヤーの「EmailLink」ダイアログボックスの「E メールを送信」ボタンの記述名（E メールを送信）を読み上げないので、スクリーンリーダーに影響が出ます。 (ASSETS-5641)
* アクセシビリティ — キーボードの Tab キーを使用して移動中に、画像セットエディターページの「元に戻す」ボタンを呼び出した後に表示される「やり直し」ボタンに、キーボードのフォーカスが移動しない。 (ASSETS-5582)
* アクセシビリティ — スクリーンリーダーに依存するユーザーは、「プロパティ」見出しの下にある画像セット画像に対して Alt 属性が提供されていないので、影響を受けます。 (ASSETS-5576)
* アクセシビリティ — スクリーンリーダーがの見出しの役割を読み上げない `Cannot save this set` テキスト `Cannot save this set` 警告：見出しショートカットキーを使用して移動中 `H`、および下向き矢印キー。 (ASSETS-5569)
* アクセシビリティ — スクリーンリーダーに依存するユーザーは、フォーム内を移動する影響を受けます。 NVDA が「幅と高さ」スピンコントロールのラベル情報を読み上げていない場合、フォームコントロールに関する情報を理解するのが困難です。 NVDA フォームモード「F」で移動する際に、レスポンシブ画像切り抜きヘッダーの下に存在するこれらのコントロール。 (ASSETS-5393)
* サイトでDynamic Mediaコンポーネントを追加した後、ページを公開した後、新しく追加されたDynamic Mediaアセットは、公開されたページにもプレビューページにも表示されません。 この問題は、画像とビデオの両方のアセットタイプで発生していました。 (ASSETS-9467)

## Commerce {#commerce-6513}

* 「everyone」には jcr:write があります `/content/usergenerated/etc/commerce/smartlists`. (NPR-35230)
* コマース製品のローカル並べ替えが機能しなくなりました。 （CQ-4343750）
* プロパティを変更した後、検索結果ページから製品をクイック公開できない。 （CQ-4343318）

## CRX {#crx-6513}

* 特殊文字が含まれる場合、パッケージをダウンロードすることはできません `+` パッケージ名に含まれます。 (NPR-38102)

## [!DNL Forms] {#forms-65130}

* 事前入力サービスを使用して、フラグメントを含むアダプティブフォームに入力し、フラグメントにリッチテキストをサポートする「テキスト」ボックスが含まれている場合、フォームは送信に失敗し、次のエラーが発生します。

   `[AF] [AEM-AF-901-004]: Encountered an internal error while submitting the form.` (NPR-38542)

* ラジオボタン、チェックボックス、ファイルアップロードの各コンポーネントが、ドイツ語から英語に正しく翻訳されていない問題を修正しました。 (NPR-38527)
* PDF417 バーコードエンコーディング： [!DNL Experience Manager] Formsはラジオボタングループに対して無効です。 (NPR-38525)
* アダプティブフォームの送信時に次のエラーが発生します。
   `WARN [10.172.114.236 [1650871578492] POST /lc/content/forms/af/public/DHS-3754-ENG/jcr:content/guideContainer.af.internalsubmit.jsp HTTP/1.1] com.adobe.aemds.guide.internal.impl.utils.SubmitDataCollector TemplateKey not found in merge json:cq:responsive` (NPR-38520)
* 「レコードのドキュメントから非表示のフィールドを除外」オプションは機能しません。 (NPR-38512)
* Formsコンテナコンポーネントを Sites ページに追加すると、ユーザーが別の Sites ページに移動できなくなり、 Sites ページがハングすることがあります。 問題が断続的に発生する。 (NPR-38506)
* 適用後、アダプティブFormsでテキストが重なり合う [!DNL Experience Manager] 6.5 サービスパック 11。 (NPR-38376、CQ-4342472)
* アダプティブフォームのパネルを新しいレスポンシブレイアウトに移動すると例外が発生する。 (NPR-38369)
* ECMASCRIPT 6 (ES6) のサポートがクライアントライブラリに対して有効になっていません ` /libs/fd/expeditor/clientlibs/view`. (NPR-38358)
* を使用する場合、 [!DNL Experience Manager] ヘブライ語で E メールを送信するワークフローで、ユーザーの最後に受け取った E メールに、ヘブライ語のテキストではなく疑問符 (??) が含まれる (NPR-38296)。
* ユーザーが次の項目からランダムにログアウトされる [!DNL Experience Manager] パブリッシュインスタンスとアダプティブフォームが送信に失敗する。 問題は、に表示されます。 [!DNL Experience Manager] Dispatcher を使用するインスタンス。 (NPR-38285)
* AdobeLaunch のルールで getFormDataString オプションを使用してアダプティブフォームデータを取得する場合、このオプションはアダプティブFormsデータを返しません。 (NPR-38283)
* [!DNL Experience Manager] 6.5 Formsの非推奨の java.acl.Group 関連 API と次のエラーメッセージが error.log ファイルに表示されます。
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)
* ドイツ語で作成されたFormsが、英語や他の言語に翻訳できなかった。 (NPR-38280)
* ローカライズ版のアダプティブフォームを使用する場合、対応するレコードのドキュメント (DoR) はローカライズされません。 (NPR-38235)
* 「電子メールを送信」ステップを使用して添付ファイルを電子メールと共に送信する場合、「ワークフロー」ステップで指定された名前が添付ファイルに保持されません。 (NPR-38216)
* レターの新しいバージョンが発行されると、ユーザーは以前のバージョンのレターのドラフトレターを開くことができません。 (NPR-38215、CQ-4342515)
* アダプティブフォームルールとして設定されたボタンのクリックでAEM Forms JEE サービス SOAP エンドポイントサービスメソッドを呼び出すと、SOAP サービスは次の例外で失敗します。
   `ERROR* [0:0:0:0:0:0:0:1 [1624362360493] POST /content/forms/af/testsoapwsdl/jcr:content/guideContainer.af.dermis HTTP/1.1] com.adobe.aemds.guide.addon expeditor.servlet.ExpEditorServiceManager Error while making web service related call java.lang.Exception: createSOAPParam: JSONException`
* PDFを XDP 形式に変換するためにcom.adobe.fd.pdfutility.services.PDFUtilityService#convertPDFtoXDP を使用すると、無効な XDP ファイルが返されます。 (NPR-38140、CQ-4342099)
* 複数のユーザーが Correspondence Management を使用して異なるレターを生成する場合、プレビュー時に、誤ったレターが一部のユーザーに表示されます。 (NPR-38134)
* SITES ページに埋め込まれるAEM Formsコンポーネントは、値が%で、W3CHTML検証時に無効な width 属性を使用します。 ユーザーの検証中に誤った解析エラーがHTMLしました。 (NPR-38124)
* アダプティブフォーム内の OOTB テーマのほとんどに対するラジオボタンおよびチェックボックス項目がタブ順序に含まれていない (NPR-38108)
* ワークフローの実行中にHTMLタグをコメントセクションに追加すると、そのHTMLタグがレンダリングされます。 (NPR-37591)
* 新しい XDP ファイルを含むレターを読み込んで発行すると、そのレターは発行インスタンスでプレビューできません。 ただし、同じ CMP ファイルを使用してレターが読み込まれて 2 回目に公開された場合、レターは正常にプレビューされます。 （CQ-4343599）
* データ準備プロパティが設定されたフォームが、HTMLWorkspace でレンダリングに失敗します。 （CQ-4343294）
* Forms 6.5 Designer で作成された静的PDF formsの場合、PDFアクセシビリティはエラーで失敗します `Tab order entry in page with annotations not set to "S"`. （CQ-4343117）
* AEMForms-6.5.0-0038(log4jv2.16) パッチを適用した後、OCR を使用して PDFG サービスを使用して画像をPDFに変換できない。 （CQ-4342450）
* バーコード SSCC-18 に正しくない値が表示される。 Formsサーバーは、バーコードの右側の値を省略します。 （CQ-4342400）
* Microsoft® Word ファイルをForms Designer に読み込めません。 ユーザーにエラーが発生しました `Word (version XP or onwards) could not be found on the machine`. （CQ-4342146）
* Forms 6.5 Designer で、Forms 6.1 Designer で作成したフォームを開き、テキストボックスを編集すると、段落の間隔が指定したスペースを超えます。 スペースに対する以前の設定はすべて削除され、テキストボックスの手動での再フォーマットが必要になります。 （CQ-4341899）
* ユーザはジョブの削除スケジューラにカスタム時間を設定できません。 （CQ-4339192）
* エンドポイント管理 UI の下の設定を更新できず、エラーが発生しました ` Uncaught ReferenceError: updateEndpoint_required is not defined`. （CQ-4331523）
* 無効なタグの場合、エラーメッセージの正常な処理が期待どおりに動作しません。 (NPR-38106および CQ-4337173)

>[!NOTE]
>
>* [!DNL Experience Manager Forms] では、[!DNL Experience Manager] サービスパックのリリース予定日の 1 週間後にアドオンパッケージをリリースします。


## Granite {#granite-6513}

* オムニサーチは、読み取り権限のないユーザーに対して結果を返します。 (NPR-38373)
* ES6 を有効にする対象 `/libs/granite/configurations/clientlibs/confbrowser`. (NPR-38300)

## 統合 {#integrations-6513}

* 非推奨の UserInfoServlet からの、Test および Target サービス上のリソースリゾルバーセッションのリーク。 (NPR-38112)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑13 ‑ HTTP Parameter Pollution in `com.day.cq.searchpromote.impl.servlet`. (NPR-38033) -->
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Analytics 2.0 IMS support added to Experience Manager 6.5. (NPR-37914) -->

## Oak - インデックス作成とクエリ {#oak-6513}

* 6.5.13.0の Oak バージョンが1.22.11に更新されました。 (NPR-38084) -->

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Create a CFP based on latest 6.5.12 and update Oak-related bundle versions. (NPR-38144) -->

## プラットフォーム {#platform-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * RTC : Universal XSS through cq-rewriter HtmlParser. (NPR-38064) -->
* のアップグレード依存関係 `org.apache.httpcomponents.httpclient` in [!DNL Experience Manager] 6.5. (NPR-37999)
* パスフィールドの候補が原因でオーサーの読み込みが高くなる。 （CQ-4341826）
* プロジェクトをカード表示からカレンダー表示に変更した場合、ユーザーはページを更新する必要があります。 （CQ-4340368）
* 権限の制限により、タグは失われます。 （CQ-4339543）
* パス選択の検索とフィルターで複数の問題が報告されましたが、機能しませんでした。 （CQ-4339402）
* 6.5 での DTM の使用を停止 — Omega Instrumentation 用に Launch に切り替え、Gainsight のサポートを追加します。 （CQ-4337809）
* 設定されている pathfield filter プロパティに基づいて、pathfield コンポーネントの検索機能を制限します。 （CQ-4309556）
* [!DNL Experience Manager] Platform 6.5:中国語のロケールの命名に関する修正。 （CQ-4308978）
* Omega Instrumentation の Launch に切り替えます。 (NPR-38377)
* [!DNL Experience Manager] Platform 6.5:中国語のロケールの命名に関する修正。 （CQ-4308978）

## レプリケーション {#replication-6513}

* ユーザーノードの公開がオーサーからパブリッシャーに失敗する。 (NPR-38005)

## [!DNL Sites] {#sites-6513}

### 管理者 {#sites-admin-6513}

* SP 12 で発生した、ページの移動時に問題が発生する問題を修正しました。 (SITES-5298)

### クラシックユーザインターフェイス {#sites-classicui-6513}

* RTE:新しい画像を既存の画像の上にドラッグすると、更新された画像が表示されません。 (NPR-38141)

<!-- version 2 of description above * Updated Image is not visible When a new image is dragged on top of an existing image the updated image is not visible in RTE - Classic UI. (NPR-38141) -->

### コンテンツフラグメント {#sites-contentfragments-6513}

* サブ設定でのコンテンツフラグメントモデルの作成をサポートします。 (NPR-38054)

<!-- version 2 of description above * The Configuration Manager now allows you to set the Content Fragment Model config on a sub-config folder. (NPR-38054) -->
* コンテンツフラグメントモデルで「一意のフィールド」検証を使用する際のパフォーマンスを向上させます。 (NPR-38142)

<!-- version 2 of description above * The unique field validation query is now fixed. (NPR-38142) -->
* コンテンツフラグメントモデルエディターを開く際の応答時間を改善します。 Assets で多数のフラグメントを使用している場合、を開くとエラーが発生することがあります。 (SITES-6284)

<!-- version 2 of description above * If the customer is trying to access the editor of the content fragment models, they get a query error because of too many fragments on the dam. (SITES-6284) -->
* コンテンツフラグメントモデルエディターでエラーが発生する可能性がある、6.5.11 から 6.5.12 に更新する際に発生した回帰を修正しました。 （SITES-5088 および SITES-4967）

<!-- version 2 of description above * Paths were getting deleted when AEM 6.5.12.0 was installed on existing 6.5.11.0 instance. (SITES-5088)
* Apple 6.5.10 system crashing when using CF model editor, due to erroneous feature toggle check. (SITES-4967) -->
* コンテンツフラグメントモデルエディターのユーザーインターフェイスのローカライゼーションを改善しました。 (NPR-38126)

<!-- version 2 of description above * Some strings in the Content Fragment Model editor are not localized. (NPR-38126) -->
* オーサーサーバーを Dispatcher と共に使用する場合に、コンテンツフラグメントエディターを閉じるとエラーが発生する可能性がある問題を修正しました。 (NPR-38205)

<!-- version 2 of description above * Update of Content Fragment references is returning an invalid JSON response via Dispatcher. (NPR-38205) -->
* RTE フィールドで検証が使用された場合に、モデルを保存できなかった問題を修正しました。 (NPR-38210)

<!--version 2 of description above * Content Fragment Model Rich Text Validation Prevents Blocks Saving a Content Fragment Model. (NPR-38210) -->
* コンテンツフラグメントの問題が発生し、ブール型プロパティで「タイトル」にフィールドテキストが表示されず、「プロパティ名」が表示されない。 (NPR-38244)
* Postmanを介してクエリ変数を使用して永続化クエリを実行中にエラーが発生しました。 (NPR-38251、NPR-38057)
<!--version 2 of description above * An unexpected error message is coming in Postman, when executing the graphQL persisted query having query variables. (NPR-38251) -->
* コンテンツフラグメントコンポーネント：「見出しを段落として処理」オプションの回帰 (6.5 SP7) が修正されました。 (NPR-38055)

<!--version 2 of description above * After applying SP11 to the Publish instance of AEM 6.5.6, the display result of the Content Fragment set in the published page changes. (NPR-38055) -->
* 6.5.11 で導入された、アセット検索エラーの原因となっていた問題を修正しました。 (SITES-4784)

<!--version 2 of description above * Adapt external index package to use selection Policy (fragment versus asset index). (SITES-4784) -->
* 使用 **[!UICONTROL 編集]** 検索結果から、 `Not Found` エラー。 (NPR-37810)

<!--version 2 of description above * When editing Content Fragment from the Assets Search Rail results page, it throws 'Not Found' error. (NPR-37810) -->

### ContentHub {#sites-contenthub-6513}

* ページをハードリフレッシュしないと、ContextHub UI モデルが正しくレンダリングされません。 (NPR-38212)

### 電子メールエディタ {#sites-emaileditor-6513}

* 電子メールコアコンポーネントの今後のリリースに対するサポートを有効にする [https://github.com/adobe/aem-core-email-components](https://github.com/adobe/aem-core-email-components). (NPR-38445および NPR-38204)

<!-- version 2 of description above * Allow new email templated under campaign and ambit. (NPR-38445) * The "Approve for Adobe Campaign" workflow was only running for pages which are of type or extending the resource types: "mcm/neolane/components/newsletter", "mcm/campaign/components/newsletter" and "mcm/campaign/components/campaign_newsletterpage". (NPR-38204) -->

### エクスペリエンスフラグメント {#sites-experiencefragments-6513}

* エクスペリエンスフラグメントの参照で「ページに移動」アクションを使用すると、間違ったページが開きます。 (NPR-38062)
* XF テンプレートから取得したレイアウトプロパティは、ページの横に表示されません。 (NPR-38214)
* XF 参照計算のパフォーマンスが向上しました。 (NPR-38269)

<!-- version 2 of description above * Job queue configuration is incorrect - The OSGi configuration for the reference updater job queue has not been ported back to 6.5. This issue leads to jobs being run in the main queue, which has a higher priority and allows more jobs to run in parallel. This flow can lead to CPU exhaustion. (NPR-38269) -->

### ページエディター {#sites-pageeditor-6513}

* で inlineEditing 機能や dropTarget 機能を持たないコンポーネントの取り消し機能を改善します。 `cq:editConfig`. (NPR-38361)

<!-- version 2 of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* を使用するコンポーネントの場合、「スタイルシステム」ドロップダウンが、コンポーネントのコンテキスト内ではなく、ページの先頭に配置されている可能性があります `cq:editConfig` &quot;afteredit:REFRESH_PAGE」と呼ばれます。 この問題は解決されました。 (NPR-38384)

<!-- version 2 of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig “afteredit: REFRESH_PAGE”. (NPR-38384) -->
* ネストされたレイアウトコンテナに追加すると、テキストコンポーネントの位置がずれています。 (NPR-38193)
* コンポーネントのスタイルシステム設定がない場合、空の「スタイル」タブが表示されていました。設定が存在しない場合、「 」タブが非表示になります。 (NPR-38218)
<!-- version 2 of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* プロパティ `useLegacyResponsiveBehaviour` は、認証済みの場合にのみ機能します。 (NPR-37996)
* jquery-ui を最新バージョンにアップグレードすると、エディターが機能しなくなっていました。 (SITES-5647)

### セキュリティ {#sites-security-6513}

* 特に、ユーザー数が+20 のグループで、ユーザーグループ管理ユーザーインターフェイスでユーザーを削除できない場合がありました。 (NPR-38041)

<!--version 2 of description above * Cannot remove users from user groups. (NPR-38041) -->

### SEO {#sites-seo-6513}

* Sitemap Generator と Canonical タグは、.html を使用しない URL のサポートを追加します。 (CIF-2647)
* noindex 設定を使用して代替言語を削除するサポートを追加しました。 (CIF-2496)
* ほぼ同じコンテンツを持つページのデフォルトの正規 URL を上書きするカスタム URL を提供するサポートを追加しました。 (CIF-2747)

### SPA Editor と SDK {#sites-spa-sdk-6513}

* 6.5.13 以降では、SPAエディターを使用して編集を行う前に、JCR でコンテナコンポーネントノードを作成する必要がなくなりました。 A `virtual container` は、SDK を介して保存する前に作成されます。 (SITES-5762)

<!-- version 2 of description above * Virtual container support - Adding a child component to a virtual container that is not yet present in the database implies the creation of a node to represent the container in content structure. (SITES-5762) -->

### テンプレートエディター {#sites-templateeditor-6513}

* 変更したテンプレートを公開しても、すべての依存関係が公開されない問題を修正しました。 (NPR-38274)

<!-- version 2 of description above * Template changes do not get published until you publish a page that uses that template. (NPR-38274) -->
* TemplatedResource valueMap は、ValueMap API ごとにディープ読み取りを許可する必要があります。 (NPR-38439)

## Sling {#sling-6513}

* でのメモリリーク `DiscoveryLiteDescriptor`. (NPR-38288)
* 更新 `sling-javax.activation` SLING-8777 の修正を含むバンドル。 (NPR-38077)
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Security issues reported under `org.apache.sling.scripting.jst`. (NPR-38067) -->

## 翻訳プロジェクト {#translation-6513}

* 参照先のページ/xf に対して複数のローンチが作成されました。 (NPR-38263)
* Service Pack 10 以降、翻訳プロジェクトにページを追加する動作を変更しました。 翻訳プロジェクトに新しく作成されたページが含まれていません [例：test-page-women-2] （新しく作成されたページの親を選択した場合） [新しく作成されたページが直接作成されていません]. (NPR-38256)
* 追加 `cq:isTranslationLaunch` プロパティを翻訳プロジェクトで作成しました。 (NPR-38224)
* アセットを含む参照元の XF を持つページに対して Launch が作成されます。 (NPR-38199)
* [!DNL Experience Manager] 翻訳メモリの更新が機能しません。 (NPR-38196)
* ES6 を有効にする対象 `/libs/cq/gui/components/projects/admin/translation/job/addcontent/clientlibs.js`. (NPR-38306)
* の翻訳用の最新の 18n パッケージ [!DNL Experience Manager] 6.5. （CQ-4339505）

## ユーザーインターフェイス {#ui-6513}

* 「スタート」ページ/「ツール」セクションで、 [!DNL Experience Manager] アイコン [!DNL Experience Manager] ナビゲーション画面がポップアップ表示されます。 (NPR-38417)
* ES6 を有効にする対象 `/libs/granite/ui/references/clientlibs/coral/references`. (NPR-38303)
* ES6 を有効にする対象 `/libs/granite/datavisualization/clientlibs/d3-3.x`. (NPR-38302)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑09 ‑ Persistent cross‑site scripting selecting paths in templates. (NPR-38301) -->
* タッチ UI の日付選択は、韓国語で表示されます。 (NPR-38079)
* 複数フィールドを含むオーサリングダイアログで、ラジオボタンの選択値をローズしてフィールドの順序を変更する。 (NPR-38063)

## WCM {#wcm-6513}

* [!DNL Experience Manager] MCM (Campaign) 6.5:中国語のロケールの命名に関する修正。 （CQ-4308973）
* com.day.cq.wcm.workflow.impl.WcmWorkflowServiceImpl.autoSubmitPageAfterModification の閉じられていない ResourceResolver (NPR-38286)

## インストール [!DNL Experience Manager] 6.5.13.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback -->

* [!DNL Experience Manager] 6.5.13.0が必要 [!DNL Experience Manager] 6.5. [アップグレードドキュメント](/help/sites-deploying/upgrade.md) を参照してください。
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からダウンロードできます。
* MongoDB および複数のインスタンスを使用したデプロイメントで、をインストールします。 [!DNL Experience Manager] 6.5.13.0を、いずれかのオーサーインスタンス上で、パッケージマネージャーを使用して実行します。

>[!NOTE]
>
>アドビは、[!DNL Experience Manager] 6.5.13.0 パッケージを削除またはアンインストールすることはお勧めしません。

### 次の場所に Service Pack をインストールします。 [!DNL Experience Manager] 6.5 {#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip)からサービスパックをダウンロードします。

1. パッケージマネージャーを開き、「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。詳しくは、 [パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。 [Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。 Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでもときどき発生する場合があります。

**自動インストール**

自動インストールに使用できる方法は 2 つあります [!DNL Experience Manager] 6.5.13.0.

* パッケージをに配置します。 `../crx-quickstart/install` フォルダー（サーバーがオンラインで使用可能な場合） パッケージが自動的にインストールされます。
* 以下を使用： [パッケージマネージャーからの HTTP API](/help/sites-administering/package-manager.md#package-share). ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>[!DNL Experience Manager] 6.5.13.0では、Bootstrapのインストールはサポートされていません。

**インストールの検証**

このリリースでの動作が認定されているプラットフォームについては、 [技術要件](/help/sites-deploying/technical-requirements.md).

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.13.0)` が表示されます。

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.3 以降です（web コンソールを使用：`/system/console/bundles`）。


### インストール [!DNL Experience Manager] Formsアドオンパッケージ {#install-aem-forms-add-on-package}

>[!NOTE]
>
>を使用していない場合はスキップ [!DNL Experience Manager] Forms。 の修正点 [!DNL Experience Manager] Formsは、スケジュールされた後 1 週間で、別のアドオンパッケージを通じて配信されます [!DNL Experience Manager] Service Pack リリース。

1. をインストール済みであることを確認します。 [!DNL Experience Manager] サービスパック。
1. [AEM Forms リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. Formsアドオンパッケージをインストールします。詳しくは、 [AEM Formsアドオンパッケージのインストール](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Experience Manager6.5 Formsでレターを使用する場合は、 [最新の AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### インストール [!DNL Experience Manager] JEE 上のForms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。の修正点 [!DNL Experience Manager] JEE 上のFormsは、別のインストーラーを使用して提供されます。

の累積インストーラーのインストールに関する情報 [!DNL Experience Manager] JEE 上のFormsとデプロイメント後の設定については、 [リリースノート](jee-patch-installer-65.md).

>[!NOTE]
>
>の累積インストーラーをインストールした後 [!DNL Experience Manager] JEE 上のForms、最新のFormsアドオンパッケージをインストールし、 `crx-repository\install` フォルダーを開き、サーバーを再起動します。

### UberJar {#uber-jar}

の UberJar [!DNL Experience Manager] 6.5.13.0は、 [Maven 中央リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/)(https://)。

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めてください。

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
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
| 統合 |  6.5 で **[!UICONTROL と]** の統合が更新されたことにより、[!DNL Experience Manager]AEM クラウドサービスのオプトイン[!DNL Adobe Target]画面は非推奨になりました。この統合では、Adobe Target Standard API をサポートしています。 [!DNL Experience Manager]API は、認証を使用してAdobe IMSし、 [!DNL Adobe I/O]. これは、Launch が実装に向けて果たすAdobeの役割の拡大を支援します [!DNL Experience Manager] 分析およびパーソナライゼーション用のページでは、オプトインウィザードは機能的に無関係です。 | システム接続、Adobe IMS 認証、 [!DNL Adobe I/O] 統合を各 [!DNL Experience Manager] クラウドサービスを通じて設定します。 |
| コネクタ | Microsoft® SharePoint 2010 およびMicrosoft® SharePoint 2013 用のAdobeJCR Connector は、次の用途で非推奨（廃止予定）となりました： [!DNL Experience Manager] 6.5. | 該当なし |

## 既知の問題 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

<!-- VULNERABILITY ISSUE - REMOVED MAY 23, 2022 AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * If you are using Content Fragments and GraphQL, Adobe recommends that you install the following packages on top of 6.5.12.0:

  * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip) (this hot fix replaces SP12, but can be installed on top of SP12) -->

* [GraphQL インデックスパッケージ 1.0.3 を使用したAEMコンテンツフラグメント](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* [!DNL Microsoft® Windows Server 2019] は [!DNL MySQL 5.7] および [!DNL JBoss® EAP 7.1] をサポートしていないので、[!DNL Microsoft® Windows Server 2019] は [!DNL AEM Forms 6.5.10.0] の自動インストールをサポートしていません。

* [!DNL Experience Manager] インスタンスを 6.5 から 6.5.10.0 バージョンにアップグレードする場合は、`error.log` ファイルで `RRD4JReporter` の例外を表示できます。この問題を解決するには、インスタンスを再起動します。

* [!DNL Experience Manager] 6.5 Service Pack 10 または以前の Service Pack を [!DNL Experience Manager] 6.5 にインストールすると、アセットのカスタムワークフローモデル（`/var/workflow/models/dam` に作成）のランタイムコピーが削除されます。
ランタイムコピーを取得するには、HTTP API を使用して、カスタムワークフローモデルの設計時コピーとランタイムコピーを同期させることをお勧めします。
   `<designModelPath>/jcr:content.generate.json`

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* アダプティブフォームでユーザーが初めてフィールドを設定する場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* のインストール中に、次のエラーと警告メッセージが表示される場合があります。 [!DNL Experience Manager] 6.5.x.x:
   * 「Adobe Target統合が [!DNL Experience Manager] Target Standard API（IMS 認証）を使用してエクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」/ ソース「Adobe Experience Manager」タイプではなく、「HTML」/ ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : 登録の変更が完了するのを待機中のタイムアウトが未登録になりました。

* コンテンツフラグメントまたは Sites/Pages のいずれかを移動/削除/公開しようとすると、バックグラウンドクエリが失敗したため、コンテンツフラグメント参照を取得する際に問題が発生する。つまり、機能が動作しません。
正しい操作を確実におこなうには、次のプロパティをインデックス定義ノードに追加する必要があります `/oak:index/damAssetLucene` （インデックスの再作成は不要）:

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## 含まれている OSGi バンドルとコンテンツパッケージ {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、[!DNL Experience Manager] 6.5.13.0 に含まれている OSGi バンドルとコンテンツパッケージの一覧が記載されています。

* [Experience Manager 6.5.13.0 に含まれている OSGi バンドルの一覧](/help/release-notes/assets/65130_bundles.txt)

* [Experience Manager 6.5.13.0 に含まれているコンテンツパッケージの一覧](/help/release-notes/assets/65130_packages.txt)

## 制限付き Web サイト {#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [Adobeカスタマーサポートに連絡](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [アドビ製品アップデートの優先通知に登録する](https://www.adobe.com/subscription/priority-product-update.html)

