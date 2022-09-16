---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: リリース情報、新機能、インストール方法、詳細な変更リストを見つけます。 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: 48f898a774d2ddd6d2c31f6a4107c71e4032cfc2
workflow-type: tm+mt
source-wordcount: '3281'
ht-degree: 38%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession&cid=a915e87c-369a-480c-9daf-d13efc766798 -->

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.14.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2022年8月25日（PT） <!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.14.0 の内容 {#what-is-included-in-aem-6514}

[!DNL Experience Manager] 6.5.14.0には、2019 年 4 月の 6.5 の初期リリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、バグ修正、パフォーマンス、安定性、セキュリティの改善が含まれています。 [このサービスパックをインストール](#install) オン [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_

* Added support for password reset for Dynamic Media Classic users within Experience Manager. (ASSETS-10298) -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6514}

* タグファイルのタグを追加または表示できませんでしたPDFファイル。 （NPR-38452）
* Connected Assets を設定し、設定を保存し、設定ページを再度開いて、既に保存されている設定をテストすると、テスト接続が失敗します。 （NPR-38507）
* ユーザー ID が数値のユーザーをコレクションに追加できない。 （NPR-38538）
* Experience Managerは、オーサーインスタンスにインストールされた FFmpeg を処理できません。 （NPR-38568）
* PDFの処理が `NoClassDefFoundError` エラーメッセージ。 （NPR-38741）
* 次のアセットレポートを作成する際に、「カスタム列」の下の「追加」ボタンが正しく表示されません： `de_DE` ロケール。 （ASSETS-10641）
* 重複アセットを Digital Asset Management リポジトリーにアップロードすると、Experience Managerが重複アセットを検出して削除するオプションを提供すると、元のアセットもリポジトリから削除されます。 （ASSETS-10826）
* Experience Managerで複数フィールドに特殊文字を指定すると、フォルダーメタデータが正しく保存されません。 （ASSETS-10721）
* クリックするまでアセットのプロパティを保存できません **[!UICONTROL 保存して閉じる]** 2 回。 （ASSETS-12040）
* スクリーンリーダーは、 `Relate` 」ボタンをクリックします。 ただし、 `Relate` ボタンにはサブメニューも含まれ、展開したり折りたたんだりできます。 （ASSETS-6938）
* 必須の ARIA（アクセス可能なリッチインターネットアプリケーション）属性 `aria-expanded` 対象 `role="combo box"` が見つかりません。 （ASSETS-6928）
* カード表示のメインファイルナビゲーション領域で、テキストコンテンツ **[!UICONTROL 並べ替え基準]** の背景色とのコントラスト比が 4.5:1 以上ではありません。 （ASSETS-6926）
* Experience Managerが識別されません **[!UICONTROL ワークフローモデルを選択]** ワークフローモデルを作成する際に、必須フィールドとしてドロップダウンリストを選択します。 （ASSETS-6871）

>[!NOTE]
>
>2022 年 9 月 1 日から、新しいExperience Manager Assets On-Premise のお客様はスマートコンテンツサービスを利用できなくなります。 この機能を既に有効にしている既存のオンプレミスおよび Adobe Managed Services のお客様は、影響を受けません。

### [!DNL Dynamic Media] {#dynamic-media-6514}

* Experience Manager内でのDynamic Media Classicユーザーのパスワードリセットのサポートを追加しました。 （ASSETS-10298）
* 透明な背景を持つ画像に対して生成されたスマート切り抜きは、白の背景を持ちます。 （ASSETS-13148）
* Dynamic MediaはEPSファイルのサムネールを生成しません。 （ASSETS-10959）
* アップロードパラメーターがないので、Dynamic Mediaアカウントにアセットをアップロードできません。 （ASSETS-13165）
* 127 文字を超える名前のアセットをDynamic Mediaにアップロードすることを許可します。 （ASSETS-9991）
* Experience Manager6.5.14.0でのDynamic Mediaビューアの JavaScript ES6(ECMAScript 6) の有効化 （NPR-38393）
* Dynamic Mediaでのオプションの設定 **[!UICONTROL 一般設定]** および **[!UICONTROL 公開設定]** は、管理者以外のユーザーがアクセスできないようにする必要があります。 （ASSETS-8628）
* Dynamic Media **[!UICONTROL 一般設定]** 設定済みのアップロードパラメーターがページに正しく表示されません。 （ASSETS-10245）
* Experience Managerのユーザーインターフェイスで、セットの作成/更新に失敗した場合に失敗メッセージが表示されない。 （ASSETS-10264）
* 編集可能テンプレートのコンテナの 1 つに保存済みポリシーを適用してDynamic Mediaコンポーネントを追加できない。 （ASSETS-11044）
* 誤ったジョブハンドルを持つアセットに対して「 Dynamic Mediaアセットを再処理」ワークフローを実行した後、アセットがDynamic Mediaアカウントにアップロードされない。 (ASSETS-12084、ASSETS-9877)
* スクリーンリーダーユーザーは、 `title` 属性が次に対して指定されていません： `<frame>` および `<iframe>` 内 **[!UICONTROL 入力して検索]** ダイアログボックス （ASSETS-5483）
* スクリーンリーダーで、関連する、意味のある `alt=` の値は、の下に存在する複数の画像に対して指定する必要があります **[!UICONTROL Assets]** 見出しを左側のペインに表示します。 （ASSETS-5644）
* スクリーンリーダーが読み取れない **[!UICONTROL ミュート]** および **[!UICONTROL ミュート解除]** ボタンをクリックします。Dynamic Mediaコンポーネントを使用したビデオの （ASSETS-10169）

## Commerce {#commerce-6514}

* コマース製品は列ヘッダーを使用して並べ替えられず、次を使用しています _リモート_ 並べ替えモード；代わりに、コマース製品は、列ヘッダーを _ローカル_ 並べ替えモード。 (CQ-4343750、NPR-38498)



## [!DNL Forms] {#forms-6514}

<!--

>[!NOTE]
>
> Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

>[!NOTE]
>
>* [!DNL Experience Manager Forms] releases the add-on packages one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages will release Thursday, September 1, 2022. In addition, a list of Forms fixes and enhancements will also be added to this section.

-->

* ファイルがマルチパネルアダプティブフォームに添付され、アダプティブフォームのドラフトが保存されると、エラーが発生します。 （NPR-38978）
* ユーザーが AdobePDF 設定で createPDF2 Java API を使用してRGBプロファイルを CMYK プロファイルに変換した場合、このオプションは Java API では機能しません。 このオプションは、スタンドアロンの DistillerClient アプリケーションで正常に機能します。 （NPR-38858、CQ-4346181）
* AEM 6.5 Forms Service Pack 12(6.5.12.0) をインストールすると、AEM Workflows の「タスクの割り当て」手順で、タスクを閉じる以外のすべてのオプションが使用できなくなります。 （NPR-38743）
* レコードのドキュメント (DoR) では、テーブルの一部の値が切り捨てられます。 （NPR-38657）
* データ XML を使用した FormSet のプレビュー時に、XDP にフローティングフィールドが含まれている場合、FormSet のプレビュー時にはデータは表示されませんが、「プレビューPDF」オプションを使用するとデータが表示されます。
* アダプティブFormsでは、ラジオボタンとチェックボックスがタブ順に表示されません。 （NPR-38645）
* を使用する場合、 `Summary Step` フォームの送信後に翻訳済みアダプティブフォームのレコードのドキュメント (DoR) を生成する場合、はローカライズされた言語に翻訳されません。 （NPR-38567）
* AEM Workflow ステップの「再試行を無効にする」オプションが期待どおりに動作しません。 この問題は断続的に発生します。（NPR-38547）
* リッチテキストフィールドを含むアダプティブフォームが送信されると、 `an Internal Error while Submitting a Form` エラーが発生しました。 フォームを送信する前にユーザーがリッチテキストフィールドにフォーカスを移した場合、エラーは発生しません。 （NPR-38542）
* エラー `sling-default-3-AdobeSignRefreshTokenScheduleJob com.adobe.forms.foundation.oauth.model.OAuthConfigSlingModel Refresh Token not present for: /conf/gws-eform/cashlite/settings/cloudconfigs/fdm/cashlite/jcr:content occurs` がログに記録されます。 （NPR-38541）
* ユーザーがアダプティブフォームにPDFをアップロードすると、AEM Formsサーバーが応答しなくなります。 （NPR-38398）
* OSGi サーバー上のAEM Formsで、Document Service API を使用してPDFを認証すると、次のエラーで失敗します。com.adobe.fd.signatures.truststore.errors.exception.CredentialRetrievalException:AEM-DSS-311。 （CQ-4346252）
* 下書きレターを送信すると、 `Could not upload asset from xml input` エラーが発生しました。 機能には影響しません。 ドラフトを開くと、レターは正しくレンダリングされます。 (CQ-4345979、CQ-4344418)
* 日付がドイツ形式で入力され、 `Preview with Data` オプションをレターに使用した場合、「日付」フィールドはレンダリングされません。 （CQ-4345783）
* Web ポータルを構築し、データに基づいてバーコードを生成する場合、一部のバーコードが正しくデコードされません。 （CQ-4345743）
* PDFへの PostScript 変換で、出力ドキュメントが期待どおりの色でレンダリングされなかった問題を修正しました。 （CQ-4345074）
* リソースリゾルバは、断続的な送信エラーを引き起こし、1 回の送信で同じスタックトレースが複数回表示されます。 （CQ-4344764）
* ユーザーは、 `cmDataUrl` パラメーター。 下書きは初めて正常に開きます。 問題は、以降の試行で発生し始めます。 （CQ-4344418）
* ユーザーが `&` シンボルを使用してインタラクティブ通信 (IC) を読み込むと、対応する IC の下書きが読み込めなくなる。 （CQ-4343969）
* AEM Forms Designer でスタイルオプションを使用して PCL ファイルを生成する場合、生成されたファイルには指定のスタイルが適用されません。 （CQ-4339573）
* ページ数が 15 を超える場合、動的 XDP フォームからアダプティブフォームへの自動変換が失敗します。 これは、ページ数が 15 未満の場合に正常に機能します。 （NPR-35337）
* 「お気に入りに追加」オプションを使用した場合でも、スクリーンリーダーに切り替える状態は示されません。 （NPR-37137）
* フォームデータモデルでは、データベースベースベースに基づくフォームデータモデルの小数点以下の値は、金額と小額の金額データ型用に切り捨てられます。. (CQDOC-19509)
* Workspace でワークフローのナビゲーションリンクを選択した場合、HTMLリンクが選択されていることは示されません。 （NPR-37138）
* 手書き署名機能は、アクセシビリティガイドラインに対応していません。 （NPR-37596）
* AEM Formsは log4j 1.x を使用します。log4j 1.x のサポートが提供終了になりました。 （NPR-38273）
* MSSQL データベースをフォームデータモデルのデータソースとして使用し、値を取得する場合、取得値の小数以降の数値は切り捨てられます。 （CQ-4346190）
* Forms 6.5 Designer で、Forms 6.1 Designer で作成したフォームを開き、テキストボックスを編集すると、段落の間隔が指定したスペースを超えます。スペースに対する以前の設定がすべて削除され、テキストボックスの手動での再フォーマットが必要になります。（CQ-4341899）
* バーコード SSCC-18 に正しくない値が表示されます。Forms サーバーが、バーコードの右側の値を省略します。（CQ-4342400）
* Forms 6.5 Designer で作成された静的 PDF フォームの場合、PDF アクセシビリティが次のエラーで失敗します。`Tab order entry in page with annotations not set to "S"`（CQ-4343117）
* Forms Designer で、ハイパーリンクの画面Readerテキストを指定する機能が追加されました。（NPR-36221）
* 非 XFA アダプティブフォームに繰り返し可能なパネルを追加し、非 XFA フォーム内の繰り返し可能なパネルの数が 15 を超える場合、新しいインスタンスを追加するのに最大 7 ～ 8 秒かかる場合があります。 （NPR-37346）

## 統合 {#integrations-6514}

* JavaScript ES6 （ECMAScript6 モード以降）コンパイルのサポートを `/libs/cq/analytics/widgets.js` ライブラリ。 （NPR-38433）
* JavaScript ES6 （ESMAScript6 モード以上）コンパイルのサポートを `/libs/cq/testandtarget/clientlibs/testandtarget/util.js` ライブラリ。 （NPR-38435）
* コンテンツが多いほど、 `/content/campaigns`を呼び出す時間が長いほど、 `targeteditor.html` (`/libs/cq/personalization/touch-ui/content/targeteditor.html`) は、ページエディターを開いたときに取得されます。 （NPR-38663）

## プラットフォーム {#platform-6514}

* パッケージマネージャにログオンして更新をデプロイできません。 （NPR-38646）
* アセットのタグピッカーユーザーインターフェイスでは、タグは作成された順序で表示されます。 ただし、タグが多数ある場合、並べ替えできないので、タグの表示と管理は困難です。 （CQ-4344279）
* ユーザーが管理者または **[!UICONTROL 次のユーザーとして動作]** フィールドに入力します。 （CQ-4345288）
* スマートコレクションでは、保存済みの検索結果を使用してフィルタリングする際に、すべてのアセットが表示されていました。 （CQ-4345326）
* 次の場合、選択されたアセットの数が正しく表示されません。 **[!UICONTROL コレクションに追加]** when **[!UICONTROL すべてを選択]** が選択されている。 （CQ-4345424）
* 例外メッセージが **[!UICONTROL 次のユーザーとして動作]** グループまたは存在しないユーザーを含むフィールド。 （CQ-4346098）

## [!DNL Sites] {#sites-6514}

* Experience Managerを 6.5.12.0から 6.5.13.0にアップグレード中に予期しないパスが削除されました。 （NPR-38532）

### アクセシビリティ {#access-6514}

* Experience Manager Sitesで、 **[!UICONTROL 表示形式を切り替え、表示設定を調整する]** ボタンをクリックし、「 **[!UICONTROL リスト表示]**、 **[!UICONTROL ドラッグ&amp;ドロップ]** ボタンにアクセス可能な名前がありません。 (SITES-2863、NPR-38760)
* スクリーンリーダーは、次のようなアクセス可能な名前を読み上げる必要があります。 `Show description for Archive` または `Show description for mini shopping cart`. ただし、現在アクセス可能な名前は `Info Circle button show description` 対象 _すべて_ ツールチップ情報ボタン （SITES-3104）
* `cq:editConfig` で inlineEditing 機能や dropTarget 機能を持たないコンポーネントの取り消し機能が向上しました。（NPR-38361） <!-- version 2 (old) of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* 「スタイルシステム」ドロップダウンが、コンポーネントのコンテキスト内ではなく、ページの先頭に配置されている場合があります ( `cq:editConfig` &quot;afteredit:REFRESH_PAGE」と呼ばれます。 (NPR-38384) <!-- version 2 (old) of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig "afteredit: REFRESH_PAGE". (NPR-38384) -->
* ネストされたレイアウトコンテナに追加すると、テキストコンポーネントの位置がずれます。（NPR-38193）
* コンポーネントのスタイルシステム設定がない場合、空の「スタイル」タブが表示されていました。 設定が存在しない場合、「 」タブが非表示になりました。 (NPR-38218) <!-- version 2 (old) of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* プロパティ `useLegacyResponsiveBehaviour` が、認証済みの場合にのみ機能します。（NPR-37996）

### [!DNL Content Fragments] {#sites-contentfragments-6514}

* コンテンツフラグメント列挙フィールドの検証では、コンテンツフラグメントが初めて読み込まれる際に問題が発生します。 （SITES-7140）
* コンテンツフラグメントエディターのリッチテキストエディターで Campaign パーソナライゼーションフィールドを追加する必要がある。 （NPR-38526）
* コンテンツフラグメントエディターで新しいコンテンツフラグメントを作成または編集する場合、Dispatcher を介して、コンテンツフラグメントモデルは保存されません。 さらに、コンテンツフラグメントエディターが閉じられず、エラーがブラウザーログに表示されます。 （NPR-38691）
* 永続的なクエリ検証エラー。 （NPR-38523）
* コンテンツフラグメントダイアログボックスで、 **[!UICONTROL プロパティ]**、 **[!UICONTROL コンテンツフラグメント]** フィールドは、選択ポップアップに保存されたパスを保持しません。 （NPR-38632）
* コンテンツフラグメントモデルを作成し、ドロップダウンタイプの列挙フィールドを追加する場合、 _`is required`_失敗しました。 （NPR-38237）

### コアコンポーネント {#sites-corecomponents-6514}

* 新しいページ電子メールコンポーネントを使用して、編集中にクラシックユーザーインターフェイスに強制的に移動させないでください。 `/etc`. （NPR-38648）

### ページエディター {#sites-pageeditor-6514}

* ユーザーが目的の列数にコンポーネントのサイズを変更できない。 （NPR-38688）

### テンプレートエディター {#sites-templateeditor-6514}

* 見つかりません **[!UICONTROL 削除]** および **[!UICONTROL 切り取り]** 編集可能テンプレートのメニューバーのボタン `cq:actions` プロパティがカスタマイズされました。 （NPR-38521）
* コンポーネントに別のコンポーネントが含まれている場合は、テンプレート構造内のコンポーネントを削除できません。 **[!UICONTROL 削除]** ボタンがメニューバーに表示されない。 （NPR-38585）

## Sling {#sling-6514}

* 実稼動環境でのオープンファイル数が増加したのは、モジュールのメモリリークが原因でした `DiscoveryLiteDescriptor` in `org.apache.sling.discovery.commons`、バージョン 1.0.20。 （NPR-38288）
* Experience Manager: **[!UICONTROL 運用]** > **[!UICONTROL 診断]**&#x200B;を選択すると、 **[!UICONTROL ステータス ZIP をダウンロード]** > **[!UICONTROL ダウンロード]**. （NPR-38514）

## 翻訳プロジェクト {#translation-6514}

* 親ページの参照として追加されたサブページのローンチが、 `isDeep` プロパティが `false`. （NPR-38531）

## ユーザーインターフェイス {#ui-6514}

* を使用する場合 **[!UICONTROL すべてを選択]** > **[!UICONTROL クイック公開]**、Experience Managerがすべてのアセットを公開していなかった、またはで公開されるアセットの数が表示されていた問題を修正しました。 **[!UICONTROL カード]** 表示または **[!UICONTROL リスト]** 表示 （NPR-38546）
* 以下に、選択したアセットの数が正しく表示されません。 **[!UICONTROL コレクションに追加]** in **[!UICONTROL すべてを選択]** ケース。 （NPR-38633）
* 無効になったユーザーは、引き続きコレクションやプロジェクトに追加できます。 （NPR-38651）
* 検索フォームを保存せずにフィルターを削除すると、エラーが発生します。 （NPR-38698）
* ユーザーのセッションは `ModifiableValueMap` 直接のグループメンバーシップを確立するためのグループのインスタンス。 （NPR-38710）

## ワークフロー {#workflow-6514}

* JavaScript ES6 （ESMAScript6 モード以上）コンパイルのサポートを `/libs/cq/inbox/gui/components/inbox/clientlibs/commons.js` ライブラリ。 （NPR-38304）
* ワークフローが実行され、プロセスステップが完了した後、同じコメントが複数回繰り返されます。 （NPR-38364）

## [!DNL Experience Manager] 6.5.14.0 のインストール {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.14.0が必要 [!DNL Experience Manager] 6.5. [アップグレードドキュメント](/help/sites-deploying/upgrade.md) を参照してください。 <!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.14.0 をインストールしてください。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!NOTE]
>
>Adobeは、 [!DNL Experience Manager] 6.5.14.0パッケージ。 <!-- UPDATE FOR EACH NEW RELEASE -->

### [!DNL Experience Manager] 6.5 へのサービスパックのインストール {#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.14.0.zip)からサービスパックをダウンロードします。 <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、「 **[!UICONTROL パッケージをアップロード]** をクリックしてパッケージをアップロードします。 詳しくは、 [パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択し、「 」を選択します。 **[!UICONTROL インストール]**.

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。[Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでもときどき発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.14.0. の自動インストールに使用できる方法は 2 つあります<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager6.5.14.0では、Bootstrapのインストールはサポートされていません。 <!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ (`/system/console/productinfo`) は、更新されたバージョン文字列を表示します `Adobe Experience Manager (6.5.14.0)` under [!UICONTROL インストール済み製品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン1.22.12以降です (Web コンソールを使用： `/system/console/bundles`) をクリックします。 <!-- NPR-38747 -->

### [!DNL Experience Manager] Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>[!DNL Experience Manager] Forms を使用していない場合はスキップしてください。

<!-- 

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

-->

1. サービスパックがインストールされていることを確認してください。[!DNL Experience Manager]
1. [AEM Forms リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. [AEM Forms アドオンパッケージのインストール](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)の記載どおりに Forms アドオンパッケージをインストールします。
1. Experience Manager6.5 Formsでレターを使用する場合は、 [最新の AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### JEE 上の [!DNL Experience Manager] Forms のインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE 上の [!DNL Experience Manager] Forms の修正は別のインストーラーを介して配布されます。

JEE 上の [!DNL Experience Manager] Forms の累積インストーラーのインストールとデプロイメント後の設定について詳しくは、[リリースノート](jee-patch-installer-65.md)を参照してください。

>[!NOTE]
>
>JEE 上の [!DNL Experience Manager] Forms の累積インストーラーをインストールした後、最新の Forms アドオンパッケージをインストールし、`crx-repository\install` フォルダーから Forms アドオンパッケージを開き、サーバーを再起動します。

### UberJar {#uber-jar}

の UberJar [!DNL Experience Manager] 6.5.13.0は、 [Maven 中央リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>Experience Manager6.5.14.0では、UberJar のバージョン (6.5.13.0) は以前のリリースと同じであることに注意してください。

Maven プロジェクトで UberJar を使用するには、 [UberJar の使用方法](/help/sites-developing/ht-projects-maven.md) およびは、プロジェクト POM に次の依存関係を含めます。 <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。メインの UberJar ファイルの名前は、「`uber-jar-<version>.jar`」に変更されます。ですので `classifier` がなく、値として `apis` を `dependency` タグに使用します。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

[!DNL Experience Manager] 6.5.7.0 で非推奨（廃止予定）とマークされた特徴と機能のリストは次のとおりです。 これらの機能は、最初は非推奨とマークされ、将来のリリースでは削除されます。別のオプションが提供されます。

デプロイメントでその特徴または機能を使用しているかどうかを確認します。また、別のオプションを使用するように、実装の変更を計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 |  6.5 で **[!UICONTROL と]** の統合が更新されたことにより、[!DNL Experience Manager]AEM クラウドサービスのオプトイン[!DNL Adobe Target]画面は非推奨になりました。この統合では、Adobe Target Standard API をサポートしています。 [!DNL Experience Manager]API は、Adobe IMS と [!DNL Adobe I/O Runtime] の認証方法を使用します。これは、Adobe Experience Platform Launch が分析およびパーソナライゼーション用に [!DNL Experience Manager] ページを構築する役割が増大していることをサポートするもので、オプトインウィザードは機能的に無関係です。 | システム接続、Adobe IMS 認証、 [!DNL Adobe I/O Runtime] 統合を各 [!DNL Experience Manager] クラウドサービスを通じて設定します。 |
| コネクタ | Microsoft® SharePoint 2010 および Microsoft® SharePoint 2013 用の Adobe JCR Connector は、[!DNL Experience Manager] 6.5 で非推奨になりました。 | 該当なし |

## 既知の問題 {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

* [GraphQL インデックスパッケージ 1.0.5 を使用したAEMコンテンツフラグメント](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
このパッケージは、GraphQL を使用するお客様に必要です。これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

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

次のテキストドキュメントでは、に含まれる OSGi バンドルとコンテンツパッケージの一覧を示します。 [!DNL Experience Manager] 6.5.14.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.14.0 に含まれている OSGi バンドルの一覧](/help/release-notes/assets/65140_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.14.0 に含まれているコンテンツパッケージの一覧](/help/release-notes/assets/65140_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト {#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [アドビ製品アップデートの優先通知に登録する](https://www.adobe.com/subscription/priority-product-update.html)

