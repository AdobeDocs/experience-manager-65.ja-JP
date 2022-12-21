---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: リリース情報、新機能、インストール方法、詳細な変更リストを見つけます。 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 38227a66-f2a9-4909-9297-1eced4ed6e8c
source-git-commit: 9b7321d7fbac46966876540b4ad9355ce33ab54e
workflow-type: tm+mt
source-wordcount: '3974'
ht-degree: 28%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.15.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2022年11月24日（PT） <!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.15.0 の内容 {#what-is-included-in-aem-6515}

[!DNL Experience Manager] 6.5.15.0には、2019 年 4 月の 6.5 の初期リリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、バグ修正、パフォーマンス、安定性、セキュリティの改善が含まれています。 [このサービスパックをインストール](#install) オン [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6515}

* アセット内でのアセットの移動に失敗した場合でも、Experience Managerの名前は変更できます。 （NPR-38753）
* アセットを [!UICONTROL リスト表示]の場合、一部のタイトルが欠落しています。 （CQ-4345746）
* スクリーンリーダーが [!UICONTROL 関連付け] ボタンをクリックします。 （ASSETS-6938）
* スクリーンリーダーが、フォルダーのリストが含まれるアセットナビゲーションページでフォルダーアイコンを誤って検出しました。 （ASSETS-6936）
* コレクションをコピーする際に、画像に空のがない `alt` attribute または role=&quot;presentation&quot;を設定します。 その結果、画像はスクリーンリーダーユーザに公開される。 （ASSETS-6932）
* アセットへの注釈の追加中に表示されるテキストには、4 つの:5:1 のコントラスト比（背景色と比較） （ASSETS-6931）
* アセットのプロパティページの「IPTC」タブで、ページの幅を調整すると、ページの内容が正しく収まらず、横方向にスクロールします。 （ASSETS-6929）
* アセットをフィルターすると、 [!UICONTROL 分] および [!UICONTROL 最大] フィールドは、値の入力後に非表示になります。 （ASSETS-6925）
* Experience Managerコレクションでは、スクリーンリーダーは [!UICONTROL 電子メール] フィールドに値を入力します。 （ASSETS-6923）
* 要素に注釈を付ける際に、代替テキストが見つかりません。 （ASSETS-6922）
* 日付選択フィールドに「時間」と「分」のテキストが記述されている場合、テキストエラーメッセージは表示されません。 エラーは、赤の色を使用してのみ識別されます。 (ASSETS-6852、ASSETS-6921、ASSETS-6920、ASSETS-6907)
* の代替テキスト `[role='img']` 「ファイル」フィルターが見つかりません。 （ASSETS-6919）
* のスクリーンリーダーに関する誤ったお知らせ [!UICONTROL 作成] サブメニュー。 （ASSETS-6916）
* Experience Managerコレクションで、削除ボタン `X` スクリーンリーダーに読み上げるためのテキストがありません。 （ASSETS-6912）
* Experience Managerで Color Contrast Analyzer を使用する場合、カレンダーウィジェットの日付選択で現在の日付と選択した日付を区別することはできません。 隣接する色と正反対に、少なくとも 3:1 のコントラスト比を欠いています。 （ASSETS-6911）
* Experience Managerファイルで、次のいずれかのオプションを選択します。 [!UICONTROL スケジュール] 「公開を管理」のラジオボタン。ラジオボタンのオプション名と状態は、スクリーンリーダーによって通知されます。 ただし、 **スケジュール** ラベルは通知されません。 (ASSETS-6908、ASSETS-6906)
* 並べ替えアイコンに代替テキストがありません。 （ASSETS-6904）
* アセットプロパティページで、フィールド名 `Person` 「 IPTC 拡張」タブのラベルは、スクリーンリーダーによって通知されません。 スクリーンリーダーは、編集可能で現在は空白のフィールドのみを読み上げ、ラベル名は読み上げません。 (ASSETS-6903、ASSETS-6848)
* 注釈ツールは、キーボードを使用して表示できません。 マウスを使用して、注釈ツールを表示する画像を描画します。 （ASSETS-6899）
* Experience Managerコレクションで、 **詳細** 「 」タブに、境界と隣接する色の間に間違ったコントラスト比が表示されます。 （ASSETS-6895）
* アセットの編集中に一部の要素の ARIA 属性値が正しくありません。 （ASSETS-6894）
* ワークフローの作成中、スクリーンリーダーで見出しが正しく識別されない。 （ASSETS-6892）
* コレクションのコピー時に、「画像をSVG」削除ボタン `X` role=&quot;img&quot;を使用した場合、role=&quot;presentation&quot;がありません。 その結果、画像はスクリーンリーダーユーザに公開される。 （ASSETS-6890）
* 内 **基本** タブ内のアセットのプロパティを編集する場合、スクリーンリーダーで「タグ」フィールドの展開状態や折りたたみ状態が適切に読み上げられない。 （ASSETS-6889）
* この **基本** 「 」タブ（アセットのプロパティ）には、重複した ID を持つページが含まれます。 （ASSETS-6888）
* ワークフローの作成時にタイトルを定義するテキストフィールドのラベルは、テキストボックスに値を指定すると表示されなくなります。 （ASSETS-6887）
* リンクを共有している受信者のリストは、見出しを含むデータテーブルとして表示されますが、スクリーンリーダーユーザーにとって、意味的にはデータテーブルとして識別されません。 （ASSETS-6886）
* に空のフィールドを表すエラーメッセージは表示されません `Add Email Address` フィールドに入力します。 エラーは色でのみ表示されます。 (ASSETS-6885、ASSETS-6843)
* プレースホルダーテキスト、パス、代替テキストの背景色と比較して、コントラスト比が 4.5:1 以上ありません。 (ASSETS-6884、ASSETS-6865)
* スマートコレクションの保存中に一部の ARIA 属性の値が無効になりました。 （ASSETS-6882）
* スマートコレクションを保存すると、一部のラベルがスクリーンリーダーに適切に関連付けられません。 （ASSETS-6881）
* アセットプロパティの「 IPTC 」タブでは、スクリーンリーダーはキーワードフォームフィールドのラベルを読み上げません。 （ASSETS-6879）
* Experience Managerコレクションで、 [!UICONTROL 電子メール] 「 」フィールドが必須フィールドとして識別されず、値を指定しない場合、エラーメッセージは表示されません。 （ASSETS-6877）
* Experience Managerファイルで、 **リンク共有** 画面が `Add Email Address`. エラーは、色の使用でのみ識別されます。 (ASSETS-6876、ASSETS-6875)
* [!UICONTROL 切り抜きとマップ] アセットの編集中に、オプションにプログラム名が付かない。 （ASSETS-6874）
* フィルターテキストには、背景色と比較して 4.5:1 の契約比率が不足しています。 （ASSETS-6873）
* メインナビゲーションページのフォルダー名のテキストの背景色と比較した場合、コントラストの比率が 4.5:1 ではありません。 （ASSETS-6872）
* を実行中に [!UICONTROL コピー] コレクションの操作、 **[!UICONTROL ユーザーを追加]** コンボボックスのフォームコントロールが、その表示可能なラベルと正しく関連付けられていません。 （ASSETS-6870）
* スクリーンリーダーが [!UICONTROL 作成] ボタンサブメニューオプション （ASSETS-6869）
* 「範囲」、「ワークフロー」および「タイムゾーン」オプションの背景色と比較した場合、コントラスト比は 4.5:1 ではありません。 （ASSETS-6868）
* スクリーンリーダーが、 **タイムライン** 列。 （ASSETS-6864）
* スマートコレクションの保存中に、一部の ARIA ロールの子要素が見つかりません。 （ASSETS-6862）
* アセットを共有する際には、次の用に ARIA 属性が必要です： `Search/Add Email Address` フィールドが指定されていません。 （ASSETS-6860）
* この **マップ** キーボードを使用してダイアログボックスを表示することはできません。 代わりに、マウスをクリックしてマップダイアログボックスを表示する必要があります。 （ASSETS-6859）
* アセットプロパティページの「基本」タブに、一部の ARIA ロールの子要素が見つかりません。 （ASSETS-6858）
* アセットプロパティの「 IPTC 」タブで使用できる空のテキスト入力フィールドのコントラスト比は、隣接する色と比較して 3:1 ではありません。 (ASSETS-6854、ASSETS-6847)
* 「 **タイムライン** セクションがスクリーンリーダーで誤って検出される。 （ASSETS-6850）
* スクリーンリーダーが、アセットのプロパティの「基本」タブにある「レビューステータス」コンボボックスが読み取り専用フィールドであると認識しません。 （ASSETS-6849）
* スクリーンリーダーで、「Select All」チェックボックスと「Annotation」チェックボックスのラベルが適切に読み上げられない。 （ASSETS-6846）
* キーボードフォーカスが `About Adobe Experience Manager` オプションは **ヘルプを表示** メニュー （ASSETS-6845）
* スクリーンリーダーは、カード表示のキーボード矢印キーを使用してフォルダーのリスト内を移動する際に、選択したフォルダーを正しく読み上げることができない。 （ASSETS-6844）
* PDFをExperience Managerにアップロードする際、メモリ使用量は常に増加しています。 （ASSETS-16889）
* ワークフローで.ZIP ファイルを Assets 内のフォルダー名に変換しても、.ZIP ファイル名の大文字と小文字は区別されません。 （ASSETS-16712）
* Brand PortalからExperience Manager6.5 に切り替えた場合、初めてフィルターを適用した際に、ユーザーの述語フィルターに適切な結果が表示されません。 （ASSETS-15932）
* ビデオに注釈を付けることができません。 （ASSETS-15217）
* **公開を管理** 複製アクセス権のないユーザーのオプションが表示されなくなり、 `READ` および `WRITE` ～へのアクセス `ETC` および `VAR`. （ASSETS-15007）
* 複数の参照を持つアセットの場合、プロパティページの読み込み時間が長くなります。 （ASSETS-14182）
* Brand Portalから画像を非公開にすると、Experience ManagerはDynamic Mediaから画像を非公開にするので、ライブ Web サイトには画像が表示されません。 （ASSETS-14118）
* Dynamic Mediaのスマート切り抜きカードで XSS の問題が発生しました。 (ASSETS-14212、ASSETS-14208、ASSETS-13704)
* Dynamic Mediaのビューアプリセットで XSS 問題が発生する。 （ASSETS-13822）
* AEMで DM アセットをプレビューする際に、ユーザーアクセスを検証します。 （CQ-4314757）


## Commerce {#commerce-6515}

* ストアページの作成に失敗し、カタログのロールアウトプロセス全体を停止しました。 （CQ-4347181）

## [!DNL Forms] {#forms-6515}

### 主な特長 {#keyfeatures}

* AEM Forms Designer が [スペイン語ロケール](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja). (LC-3920051)
* これで、 [Microsoft® Office 365 メールサーバープロトコル（SMTP および IMAP）で認証するための OAuth2](/help/forms/using/oauth2-support-for-mail-service.md). （NPR-35177）
* 次の設定が可能です。 [サーバーで再検証](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-an-adaptive-form/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br) プロパティを true に設定すると、サーバー側のレコードのドキュメントから除外する非表示フィールドが識別されます。 （NPR-38149）
* AEM Forms Designer には、Visual C++ 2019 再頒布可能パッケージ (x86) の 32 ビット版が必要です。  （NPR-36690）

### 修正 {#fixes}

* アダプティブフォームの data-disabled プロパティを切り替えても、ラジオボタンとチェックボックスグループの外観は変わりません。 （NPR-39368）
* アダプティブフォームが翻訳されると、一部の翻訳が失われ、正しく表示されません。 （NPR-39367）
* ページのプロパティを「非表示」に設定した場合、そのページはフォームセットから削除されません。 （NPR-39325）
* レコードのドキュメントでは、ページの最後に動的な脚注セクションは存在しません。 （NPR-39322）
* アダプティブフォーム用にレコードのドキュメントが生成された場合、ラジオボタンとチェックボックスで垂直方向の配置のみが許可されます。 ユーザーは、ラジオボタンとチェックボックスの水平方向の配置を設定できません。 （NPR-39321）
* Correspondence Management をデプロイした後、複数のユーザーがフォームにアクセスしようとすると、org.apache.sling.i18n.impl.JcrResourceBundle.loadPotentialLanguageRoots がボトルネックになり、スレッドの大部分が突き刺されます。 多くの場合、フォームのページリクエストの読み込みには、サーバーの読み込みが非常に少ない場合でも、1 分以上かかりました。 （NPR-39176、CQ-4347710）
* アダプティブフォームで、遅延読み込みされたアダプティブフォームフラグメントでリッチテキストフィールドを使用すると、次のエラーが発生します。
   * コンテンツを編集したり、「リッチテキスト」フィールドに何も追加したりすることはできません。
   * リッチテキストに適用された表示パターンが適用されない。 
   * 最小フィールド長に関するエラーメッセージは、フォームの送信時には表示されません。
   * このリッチテキストフィールドの内容は、生成された submit-XML に複数回含まれます。 （NPR-39168）
* アダプティブフォームで日付選択オプションを使用すると、値を正しい形式に変換できません。 （NPR-39156）
* アダプティブフォームをHTMLフォームとしてプレビューしている間、一部のサブフォームが親フォームと重なるので、正しくレンダリングされません。 （NPR-39046）
* パネルに非表示のテーブルがあり、アダプティブフォームが表形式ビューを使用してレンダリングされている場合、最初のタブのフィールドが正しく表示されません。 （NPR-39025）
* この `Body` 標準 (OOTB) テンプレートのタグが見つかりません。 (NPR-39022)
* レコードのドキュメントは、アダプティブフォームの言語で生成されません。 常に英語で生成されます。 （NPR-39020）
* アダプティブフォームに複数のパネルが含まれ、一部のパネルでは標準の **添付ファイル** コンポーネント、 `Error occurred while draft saving` エラーが発生します。 （NPR-38978）
* 条件 `=` アダプティブフォームのチェックボックス、ドロップダウンリスト、ラジオボタンフィールドで署名が使用され、レコードのドキュメントが生成されます。 `=` 生成されたレコードのドキュメントには署名が表示されません。（NPR-38859）
* 6.5.11.0サービスパックのアップグレード後に、通知バッチ処理エラーの数が複数回増加しています。 （NPR-39636）
* テストデータを指定しないと、Correspondence Management レターがエージェント UI に読み込まれません。 （CQ-4348702）
* IBM® WebSphere®を使用してデプロイされたAEM FormsからAEM Forms Service Pack 14(SP14) を適用すると、データベースの初期化中にブートストラップが失敗し、 `java.lang.NoClassDefFoundError:org/apache/log4j/Logger` エラーが発生しました。（NPR-39414）
* OSGi サーバー上のAEM Form で、Document Service API を使用してPDFを認証すると、次のエラーで失敗します。com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException:AEM-DSS-311-003 （NPR-38855）
* ユーザーがAEM 6.3 Formsでレターをレンダリングするためにラッパーサービスを使用しようとすると、 `java.lang.reflect.UndeclaredThrowableException` エラーが発生しました。 （CQ-4347259）
* XDP がHTML5 フォームとしてレンダリングされる場合、アダプティブフォーム内のオブジェクトの配置に関係なく、マスターページのコンテンツが最初にレンダリングされます。 （CQ-4345218）
* 宛先サーバーでのアプリケーションの設定は、ソースサーバーで定義された設定に変更されます ( **読み込み完了時に設定を上書き** アプリケーションのインポート時にオプションがオンになっていません。 （NPR-39044）
* ユーザーが Configuration Manager を使用してコネクタ設定を更新しようとすると、失敗します。（CQ-4347077）
* ユーザーが管理者ユーザーのデフォルトのパスワードを変更した後に JEE 上のAEM Forms パッチを実行しようとすると、例外が発生します `com.adobe.livecycle.lcm.core.LCMException[ALC-LCM-200-003]: Failed to whitelist the classes` 発生します。 （CQ-4348277）
* AEM Designer では、チェックボックスを含む表のセルに、キャプションのないフォームフィールドが配置されます。(LC-3920410)
* ユーザーがAEM Forms Designer でヘルプを開こうとすると、正しく表示されません。 （CQ-4341996）

## [!DNL Sites] {#sites-6515}

* Experience Manager Sites Launchs コンソールが空白で表示されていました。 （NPR-39188）
* 参照を含むページをページの移動中にアクティベートする必要がある場合、参照は調整されませんでした。 （NPR-39061）
* レイアウトコンテナが親コンテナで非表示になっていない場合、レイアウトの変更がネストされたコンテナ内のすべてのコンポーネントに適用されるわけではありません。 （NPR-39041）
* 320 ピクセルの幅で、コンテンツが他のコンテンツと重複しなくなりました。 （SITES-8885）
* ダイアログボックスを閉じた後にフォーカスが追加されました。 （SITES-8885）

### アクセシビリティ {#access-6515}

<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The scrollable region of the Page Editor did not have keyboard access. (SITES-2936) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The color input field of the Page Editor is not labeled or visible on the screen. (SITES-2925) -->
<!-- REMOVED FROM TOTAL RELEASE CANDIDATE LIST * The iframe in the Page Editor is missing a title attribute; it must have an accessible name. (SITES-2894) -->
* この **[!UICONTROL 注釈]** ボタンにアクセシビリティ名がありません。 （SITES-2892）
* ACTIVE ユーザインターフェイスコンポーネントの状態 (**[!UICONTROL 切り取り]**, **[!UICONTROL コピー]**, **[!UICONTROL 貼り付け]**, **[!UICONTROL コンポーネントを挿入]**, **[!UICONTROL グループ]**&#x200B;など ) には、内側または外側の隣接する背景との間に、3～1 個以上の明るさのコントラスト比がありません。 (SITES-8889、SITES-8756、SITES-8885)
* ステータスメッセージは自動的には通知されませんでした。 (SITES-8889、SITES-8756、SITES-8885)
* テキストコンテンツのコントラスト比が 4.5:1 を欠いています。 (SITES-8756、SITES-8885)
* リンクまたはボタンのテキストに、ホバー時またはフォーカス時のコントラスト比が 4.5:1 でない。 (SITES-8756、SITES-8885)

### [!DNL Content Fragments] {#sites-contentfragments-6515}

* GraphQLは例外を発生します。 例えば、コンテンツフラグメントからバリエーションタグを取得することはできません。 「electric」という名前のバリエーションはありません。 この問題は、 `getVariationTags` 例外を発生させる既存のバリエーション以外のバリエーションの場合。 （SITES-8898）
* リスト表示でのタイトルの順序の並べ替え（昇順と降順の両方）、A、C、B の順序でタイトルの順序を並べ替えます (SITES-7585)
* コンテンツフラグメントのバリエーションにタグ付けのサポートを追加しました。 （SITES-8168）
* 不要な Odin 固有のコードをExperience Manager6.5 で特定および削除しました。 （SITES-3574）
* コンテンツフラグメントエディターのユーザーインターフェイスから言語コピーフラグメントを公開すると、関連する参照が英語フォルダーの下で公開されていました。 （NPR-39182）
* 日付フィールドに日付が事前入力されています。 （NPR-39124）
* ラジオボタンオプションを選択すると、タグが 2 回目に表示されなくなりました。 （NPR-39071）

### 流体 XP {#sites-fluidxp-6515}

* クライアントライブラリの ES6 コンパイルサポートを有効にする `/libs/cq/gui/components/siteadmin/admin/restoretree/clientlibs/restoretree.js`. （NPR-39067）
* 検証が行われるのは、例えば **[!UICONTROL 必須]** が選択されていません。 （NPR-39063）
* どちらでも **[!UICONTROL コピー]** または **[!UICONTROL ライブコピー]** タスク、 `cq:targetMetadata` 情報が誤って複製されていました。 この機能により、Experience Manager内の 2 つ以上のエクスペリエンスフラグメントが、Target で書き出された同じオファーを指すようになっていました。 （NPR-38970）
* ツリーの復元操作の後、メッセージ `Un-publication pending. #0 in the queue` は、最初に公開されたことのないページのユーザーインターフェイスに表示されます。 （NPR-38847）

### ページエディター {#sites-pageeditor-6515}

* 取り消しで、コンポーネントに追加されたテキストに対する最後の変更が削除されませんでした。 代わりに、ページが更新されると、コンポーネント全体が削除されます。 （SITES-8597）
* アップグレード `jquery-ui` を最新バージョンに変更すると、ページエディターが正しく機能しなくなっていました。 （NPR-38596）
* 320 ピクセルの幅で、コンテンツが他のコンテンツと重複しなくなりました。 （SITES-8756）
* ダイアログを閉じた後にフォーカスが追加されました (SITES-8756)

## Sling {#sling-6515}

* `Repoinit` では、プリンシパル名に空白が含まれるグループの作成または管理がサポートされていませんでした。これは、グループ名が文字列として扱われ、引用符の引用をサポートしていなかったためです。 (SLING-10952)
* ログに誤ってエラーメッセージや例外が入力されていました。 （NPR-39024）

## 翻訳プロジェクト {#translation-6515}

* プロジェクトパネルで、更新済み言語コピーの翻訳ジョブに宛先ページが追加されていました。ソースページは更新されませんでした。 （NPR-39278）
* 翻訳プロジェクト内のすべてのページのプレビューを生成する際に、翻訳プロセスが失敗していました。 （NPR-39059）
* 言語ロケールが存在しない場合、イベントの参照ルールが設定されているときに、その言語ロケールがロケールフォルダに作成されます。 （NPR-39054）

## ユーザーインターフェイス {#ui-6515}

* JavaScript エラーはファイル内で発生します `multifield.js` コンテンツフラグメントモデルエディターおよびコンテンツフラグメントエディターのコンテンツフラグメントモデルの特定のフィールドの場合 （NPR-39350）

## ワークフロー {#workflow-6515}

* Experience Manager6.5.11 で正常に実行されたExperience Managerの 6.5.13 で、一貫して実行されていなかった問題を修正しました。 （NPR-39023）

## [!DNL Experience Manager] 6.5.15.0 のインストール {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.15.0が必要 [!DNL Experience Manager] 6.5. [アップグレードドキュメント](/help/sites-deploying/upgrade.md) を参照してください。 <!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.15.0 をインストールしてください。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
>Adobeでは、 [!DNL Experience Manager] 6.5.15.0パッケージ。 したがって、パックをインストールする前に、 `crx-repository` 戻す必要がある場合に備えて <!-- UPDATE FOR EACH NEW RELEASE -->

### [!DNL Experience Manager] 6.5 へのサービスパックのインストール {#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)からサービスパックをダウンロードします。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、「 **[!UICONTROL パッケージをアップロード]** をクリックしてパッケージをアップロードします。 詳しくは、 [パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択し、「 」を選択します。 **[!UICONTROL インストール]**.

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。[Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでもときどき発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.15.0. の自動インストールに使用できる方法は 2 つあります<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager6.5.15.0では、Bootstrapのインストールはサポートされていません。 <!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ (`/system/console/productinfo`) は、更新されたバージョン文字列を表示します `Adobe Experience Manager (6.5.15.0)` under [!UICONTROL インストール済み製品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン1.22.13以降です (Web コンソールを使用： `/system/console/bundles`) をクリックします。 <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

>[!NOTE]
>
>最新の [AEMサービスパック (6.5.15.0)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip)（フラグメントサーブレットの前） `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` JEE 上のAEM Forms環境の場合、CRX/bundle と開始ページにサービス使用不可エラーが表示されます。 [ここをクリック](/help/forms/using/aem-service-pack-installation-solution.md) をクリックして、トラブルシューティングの手順を確認します。

### [!DNL Experience Manager] Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager] Forms を使用していない場合はスキップしてください。

<!-- 
Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.
-->

1. をインストール済みであることを確認します。 [!DNL Experience Manager] サービスパック。
1. [AEM Forms リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. [AEM Forms アドオンパッケージのインストール](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)の記載どおりに Forms アドオンパッケージをインストールします。
1. Experience Manager6.5 Formsでレターを使用する場合は、 [最新の AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja).

### JEE 上の [!DNL Experience Manager] Forms のインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE 上の [!DNL Experience Manager] Forms の修正は別のインストーラーを介して配布されます。

JBoss EAP 7.4.0 以外の任意のアプリケーションサーバーを使用する JEE 上のすべてのAEM Forms環境で、次の手順を実行します。

1. の累積インストーラーをインストールします。 [!DNL Experience Manager] JEE 上のFormsとデプロイメント後の設定については、 [リリースノート](jee-patch-installer-65.md).

1. のインストール [org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) サーブレットフラグメントを生成し、アプリケーションサーバーが安定するのを待ちます。—>
1. インストール [AEM 6.5.15.0 service pack](#install-service-pack).
1. のインストール [最新のFormsアドオンパッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)、 Formsアドオンパッケージを `crx-repository\install` フォルダーを開き、サーバーを再起動します。

### UberJar {#uber-jar}

の UberJar [!DNL Experience Manager] 6.5.15.0は、 [Maven 中央リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven プロジェクトで UberJar を使用するには、 [UberJar の使用方法](/help/sites-developing/ht-projects-maven.md) およびは、プロジェクト POM に次の依存関係を含めます。 <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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

* [GraphQL インデックスパッケージ 1.0.5 を使用したAEMコンテンツフラグメント](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
このパッケージは、GraphQLを使用しているお客様に必要です。これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

* [!DNL Microsoft® Windows Server 2019] は [!DNL MySQL 5.7] および [!DNL JBoss® EAP 7.1] をサポートしていないので、[!DNL Microsoft® Windows Server 2019] は [!DNL AEM Forms 6.5.10.0] の自動インストールをサポートしていません。

* [!DNL Experience Manager] インスタンスを 6.5 から 6.5.10.0 バージョンにアップグレードする場合は、`error.log` ファイルで `RRD4JReporter` の例外を表示できます。この問題を解決するには、インスタンスを再起動します。

* [!DNL Experience Manager] 6.5 Service Pack 10 または以前の Service Pack を [!DNL Experience Manager] 6.5 にインストールすると、アセットのカスタムワークフローモデル（`/var/workflow/models/dam` に作成）のランタイムコピーが削除されます。
ランタイムコピーを取得するには、HTTP API を使用して、カスタムワークフローモデルの設計時コピーとランタイムコピーを同期させることをお勧めします。
   `<designModelPath>/jcr:content.generate.json`

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* アダプティブフォームでユーザーが初めてフィールドを設定する場合、設定を保存するオプションはプロパティブラウザーに表示されません。同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* [!DNL Experience Manager] 6.5.x.x のインストール中に、次のエラーや警告メッセージが表示される場合があります。
   * 「Adobe Target統合が [!DNL Experience Manager] Target Standard API（IMS 認証）を使用してエクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」/「Adobe Experience Manager」タイプの代わりに、「HTML」/「Adobe Target Classic」タイプのオファーを複数作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :登録の変更が未登録に完了するのを待機中にタイムアウトが発生しました。

* コンテンツフラグメントまたはサイトやページを移動／削除／公開しようとすると、コンテンツフラグメントの参照を取得する際にバックグラウンドクエリが失敗し、機能が動作しなくなるという問題があります。
正しい操作を確実におこなうには、次のプロパティをインデックス定義ノードに追加する必要があります `/oak:index/damAssetLucene` （インデックスの再作成は不要）:

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## 含まれている OSGi バンドルとコンテンツパッケージ {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントでは、に含まれる OSGi バンドルとコンテンツパッケージの一覧を示します。 [!DNL Experience Manager] 6.5.15.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.15.0 に含まれている OSGi バンドルの一覧](/help/release-notes/assets/65150_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.15.0 に含まれているコンテンツパッケージの一覧](/help/release-notes/assets/65150_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト {#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [アドビ製品アップデートの優先通知に登録する](https://www.adobe.com/subscription/priority-product-update.html)

