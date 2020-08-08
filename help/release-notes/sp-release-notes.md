---
title: Adobe Experience Manager6.5サービスパックリリースノート
description: Adobe Experience Manager 6.5 Service Pack 5 固有のリリースノート
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ca965d8495c0460b2b6bc5e08d8818b91f9fcdee
workflow-type: tm+mt
source-wordcount: '4531'
ht-degree: 7%

---


# Adobe Experience Manager6.5サービスパックリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.5.0 |
| 型 | Service Pack のリリース |
| 日付 | 2020年6月4日 |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Adobe Experience Manager6.5.5.0に含まれるもの {#what-s-included-in-aem}

Adobe Experience Manager6.5.5.0は、2019 **年4月のGAリリース(GA)以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの向上を含む重要なアップデートで**&#x200B;す。 Adobe Experience Manager6.5の上に設置できます。

Adobe Experience Manager6.5.5.0で導入された主な機能および機能強化には、次のものが含まれます。

* Adobe Experience Manager受信トレイに表示する列名をカスタマイズします。

* ページエディター、コアコンポーネント、RTE、管理者ユーザーインターフェイスなど、Experience ManagerWebコンテンツ管理(WCM)の様々な領域でのアクセシビリティが向上しました。

* をドラフト [!DNL Interactive Communication] として保存します。

* JEE [!DNL Oracle WebLogic 12] 上のExperience ManagerFormsのサポート。

* ユーザーインターフェイスフローでの例外処理を改善 [!DNL Adobe Experience Manager Assets] しました。

* ダイナミックメディアScene7の公開URLを取得するために、インター `getRemoteAssetPublishURL``com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` フェイスに新しいメソッドが追加されました。

* [アクセシビリティの強化](#assets-6550) (Webコンテンツアクセシビリティガイドライン(WCAG) [!DNL Adobe Experience Manager Assets] に準拠)

* パッケージ共有の統合がAdobe Experience Manager内から削除されました。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.22.3 に更新しました。

機能の完全なリスト、主な特徴、Experience Manager6.5 Service Pack 5で導入された主な機能については、「Adobe Experience Manager6.5 Service Pack 5 [の新機能](new-features-latest-service-pack.md) 」を参照してください。

6.5.5.0リリースでの修正のリスト [!DNL Experience Manager] を次に示します。

### [!DNL Sites] {#sites-6550}

* Experience Managerサイトには、エイリアスからページを公開または非公開にするオプションがあります。 このオプションは機能しません(NPR-33415)。
* 複数のテンプレートを含むテンプレートからレイアウトコンテナを削除すると、そのテンプレートは正しくレンダリングされません(NPR-33347)。
* Experience Managerサイトページが、複数のライブコピーが設定された大きなコンテンツの一部である場合、ページバージョン履歴プレビューの読み込みに失敗します(NPR-33311)。
* 「移動」コマンドを使用してExperience Managerサイトページの名前を変更すると、ページタイトルは更新されません(NPR-33264)。
* 列表示内でページを移動すると、列は表示されなくなります(NPR-33216)。
* 言語コピーのローカルコンポーネントの名前が、ブループリントのコンポーネントの名前と同じで、そのコンポーネントがブループリントからロールアウトされる場合、ローカルコンポーネントの名前に用語 `_msm_moved` が追加されない(NPR-33208)。
* Page Redirectサーブレットは、Experience ManagerサイトのURLに.htmlを追加します。このサイトのURLでは、ResourceTypeは追加されません `cq:Page` (NPR-33176)。
* サブツリーを貼り付ける場合、対応するサブページを貼り付けるかどうかを決定するオプションはありません(NPR-33149)。
* コンポーネントのライブ使用の結果の数は、49個に制限されます(NPR-33058)。
* スキーマに基づくコンテンツフラグメントのベースとなり、そのコンテンツに必須のテキスト領域またはパスフィールドが含まれている場合、コンテンツフラグメントは保存されません(NPR-33007)。
* デフォルトのエクスペリエンスフラグメントコンポーネントを使用してカスタムコンポーネントを作成し、Experience Managerサイトページで使用する場合、Experience Managerにはカスタムコンポーネント(NPR-32852)の参照（使用）が表示されません。
* 多数の参照を持つフォルダーの名前を変更すると、そのフォルダーへの多くの参照は更新されません(NPR-32765)。
* ソース編集オプションを有効にすると、インラインのフルスクリーンオプションで使用できるようになりますが、リッチテキストエディターの編集ダイアログおよびフルスクリーンオプションでは使用できなくなります(NPR-32763)。
* 複数のフィールドがあり、そのフィールドに設計図のページプロパティに必須のフィールド（ドロップダウンやパスフィールドなど）が含まれている場合、そのような複数のフィールドを含むページをロールアウトすると、ライブコピーのページプロパティは保存されません(NPR-32751)。
* スクリーンリーダーは、見出し構造を使用してページを移動することはできません。 さらに、「Components（コンポーネント）」タブのラベルが誤っています(NPR-32648)。
* ページ番号の開始では、エクスペリエンスフラグメントピッカーはすべての項目を読み込みません(NPR-32605)。
* ライブコピーを読み取り、変更、作成および削除する作成者権限は失効します。 各発言者は、Blueprint内でページを移動するための読み取り権限と変更権限を明示的に提供する必要がありました(NPR-32550)。
* Adobe Analytics(NPR-32548)と統合されているページでは、コンテンツ作成者は「起動」を作成できません。
* ユーザーが同期による継承を再開すると、親ページのライブコピーは青写真と同期せず、誤ったステータスを表示します(NPR-32500)。
* Experience Managerサイトのエディターページの読み込みに15秒以上かかる(NPR-32413)。
* 一部のフィールドでは、「継承をキャンセル」オプションが表示されません(NPR-32362)。
* エクスペリエンスフラグメントコンポーネントのパスを選択し、「選択ダイアログを開く」チェックボックスを選択した場合、パスブラウザー(NPR-32308)で選択されたパスに移動しません。
* Experience Manager6.2からExperience Manager6.5にアップグレードした場合、静的テンプレートのParsysコンポーネントが正しく表示されません。 Parsysコンポーネントの高さは0に設定され、その中のコンポーネントは表示されません(NPR-33663)。
* ユーザーがレイアウトコンテナをコピーして同じページに貼り付けた場合、レイアウトコンテナのコンポーネントは表示されません(NPR-33648)。
* ディスパッチャーの正常性チェックで、ログファイルに `Invalid cookie header` 警告メッセージが表示されます(NPR-33629)。
* PreferencesServlet(NPR-33438)でXSSが反映されている。
* 匿名ユーザーは、CRX DE Liteの機能(GRANITE-27790)にアクセスできます。

### [!DNL Assets] {#assets-6550}

**Experience Managerアセットのアクセシビリティの強化**

* 「 [!UICONTROL Comments] リスト」と「クリック可能」オプションにキーボードフォーカスを移し、「アセットのTimeline [!UICONTROL パネルで新しいバージョン] を作成(NPR33424)」の下の  「バージョンコメントを作成」に移動できるようになりました。

* アセットの「 [!UICONTROL 表示設定] 」オプションに移動し、キーボードキーを使用して [!UICONTROL 表示設定] (NPR-33420)ダイアログの設定を変更できるようになりました。

* コンボボックスのリストボックスポップアップ（異なるページの様々なフィールド）に、スクリーンリーダーがアナウンスできるオプションのリストとしてエントリが表示されるようになりました(NPR-33516)。

* 並べ替え可能なヘッダー(リスト表示、 [!UICONTROL タイムライン、およびパブリケーション] 表示の  管理ページ)の並べ替え機能が、スクリーンリーダーによって通知され、列ヘッダーの並べ替えコントロールがキーボード(NPR-32979)を使用してアクセスできるようになりました。

* コメントカード、バージョン更新、コンボボックス、メニューの山形アイコンなどのクリック可能な要素は、注目し、キーボード(NPR-33514)を使用して操作できるようになりました。

* インサイト表示のインサイトアイコン（使用方法、インプレッション数およびクリック数）の機能（またはアクションの目的）が、スクリーンリーダー  (NPR-33513)によって正しくアナウンスされるようになりました。

* Read-only form fields (for example disabled fields on [!UICONTROL Basic tab] of asset [!UICONTROL Properties]) are now focusable using keyboard (NPR-33493, CQ-4273031).

* 様々な入力フィールドのラベルが、テキストの入力時に消えたプレースホルダーラベルだけでなく、永続的なラベル（アクセス可能）になりました。(NPR-33475)

* 異なる見出しレベル（ページタイトルやセクションの見出しなど）が、スクリーンリーダーユーザーに対して異なるレベルの見出しとして認識されるようになりました(NPR-33471)。

* リンクやオプション（アセットページのヘッダーやズームオプション、フォルダーナビゲーション）などのインタラクティブなユーザーインターフェイス要素は、キーボード(NPR-33468、CQ-4271412)を使用してアクセスできるようになりました。

* [ [!UICONTROL ワークフロー]、[]範囲 、および[] ]の各進行状況インジケータは、タブ(NPR-33416)ではなく、スクリーンリーダーによって正しく読み上げられるようになりました。

* 星評価アイコンの色(アセットのプ [!UICONTROL ロパティの「] 詳細」タブやカードの表示の「 [!UICONTROL Rating] 」セクションなど)は、視覚が限られ、色の知覚がないユーザーに対しては、適切なコントラストが表示されるように変更されます(NPR-33414)。

* アセットの詳細ページの [!UICONTROL コメント] フィールドの横にある山形の上向き矢印が、キーボードキーを使用してアクセスできるようになりました(NPR-33397)。

* アセットのプ [!UICONTROL ロパティ] と左側のナビゲーション（アセットのユーザーインターフェイス上）のタグ [!UICONTROL (Tags] )ダイアログの展開状態と折りたたまれた状態が、スクリーンリーダー(NPR-33396)によって正しく通知されるようになりました。

* Titles of all the browsed pages on [!DNL Adobe Experience Manager] Assets are now unique (NPR-33343).

* ツリー構造をナビゲートする際に、ツリー表示コントロールの様々な要素がスクリーンリーダー(NPR-33304)によって正しく通知されるようになりました。

* アセットの詳細ページの [!UICONTROL Timeline] 表示にあるアセットの異なるバージョンが、キーボードキーを使用してアクセスできるようになりました(NPR-33283)。

* Omnisearchコンボボックスに表示される検索候補の名前が、検索機能を使用する際にスクリーンリーダーによって通知されるようになりました(NPR-33280)。

* スクリーンリーダーは、クリッ [!UICONTROL ク可能な要素と「] 参照」パネルの「リンクへ移動 [!UICONTROL 」をクリック可能な要素としてアナウンスします] (NPR-33278)。

* 共有リンクダイアログのテーブル構造情報（行1、セル1、テーブルなど）は、ダイアログが開いたときに、スクリ [!UICONTROL ーンリーダーによって通知されなくなりました] (NPR-33268)。

* 様々なコンボボックス要素（パスフィールドや、アセットのプロパティの「基本」タブで選択ダイアログを開くオプションなど）の目的が、スクリーンリーダー(NPR-33235)によって正しく通知されるようになりました。

* リスト表示テーブルの行が選択可能であるという情報が、キーボードフォーカスがある場合に、スクリーンリーダーユーザーに通信されるようになりました。 ポインタが行に合わさると、スクリーンリーダーは情報を読み上げます(NPR-33234)。

* Options (having [!UICONTROL x]) to remove each of the selected tags below the [!UICONTROL Tags] field in [!UICONTROL Basic] tab of [!UICONTROL Properties] are now accessible to screen readers (NPR-33206).

* カレンダーの日付選択は、スクリーンリーダーユーザーや視覚力のあるキーボードユーザーがキーボードを使用して、フォーカスでき、アクションを実行できるようになりました(NPR-33200)。

* リスト表示とカード表示を切り替える切り替え機能が、(表示の調整)スクリーンリーダー(NPR-33069)に正しく公開されるようになりました。

* 左側のレールのメニューにアクセスできるようになりました。 スクリーンリーダー(NPR-33068)は、メニューの拡張の機能と目的を適切に発表する。

* リストボックスや他の多くのユーザインターフェイス要素が、目の見えないスクリーンリーダーユーザーにアクセスできるようになり、スクリーンリーダー(NPR-33040)がそれらに関する次の情報を発表します。

   * フォームを送信する前に要素に対してユーザー入力が必要かどうか。
   * 要素を編集できないかどうか。
   * ウィジェットが選択されているかどうか。

* フィルターサイドバーを開くオプションに、キーボード(NPR-32842、CQ-4273018)を使用してアクセスできるようになりました。

* リスト表示の列見出しのチェックボックスコントロールがアクセス可能になり、コントロールの使用目的がスクリーンリーダー(NPR-32722、NPR-33005)によって通知されるようになりました。

* カレンダーの日付選択で時間(HH)と分(mm)のフィールドのラベルは、プレースホルダーラベルではなく永久的なラベルになり、これらのフィールドにユーザーがテキストを入力しても表示されなくなりました(NPR-32720)。

* （ベルのアイコンをクリックした後に表示される）通知のリンクテキストが、スクリーンリーダーのユーザーに通知されるようになりました。このユーザーはタブを使用して各リンクにアクセスします(NPR-32645)。

* [!UICONTROL アセットカードの「]」、「 [!UICONTROL ダウンロード]」、「 [!UICONTROL プロパティ]」 [!UICONTROL 、「その他のアクション」の各オプションを選択します(] Insights表示「npr」内)。現在は、キーボード(DPS-32609)を使用してアクセスできます。

* キーボード(NPR-32606)を使用してアクセスした場合に、視覚的に非表示にされたコンテンツ（検索結果上のヘッダーメニューバーのコンテンツなど）が、スクリーンリーダーによって通知されなくなりました。

* カレンダーの日付選択で、コントロールのラベルを次の月と前の月に移動する目的が、スクリーンリーダーによって通知されるようになりました(NPR-32604)。

* 星レーティングのアイコンが、キーボードキーを使用してフォーカスでき、アクションを実行できるようになりました(NPR-32513)。

* ビデオのボリュームを制御する機能に、（ボリュームスライダーにフォーカスするために）タブと、（ボリュームを調整するために）キーボードの(NPR-32065)矢印キーを通してアクセスできるようになりました。

* ファイルサイズフィルターの下限([!UICONTROL 送信者])と上限(宛先)の入力フィールドの目的が、近視眼的なスクリーンリーダーユーザーに対して通知されるようになりました(NPR-32064)。

* 「 [!UICONTROL 作成と翻訳] 」フォームの「 [!UICONTROL 言語] 」メニューにブラウズモードでアクセスできるようになりました。(CQ-4293906)

* 次の機能強化により、 [!UICONTROL References] パネルにアクセスできるようになりました(NPR-33261、CQ-4293798)。

   * ブラウズモードで、スクリーンリーダーのフォーカスが、「 [!UICONTROL サイト参照]」、「 [!UICONTROL アセット参照]」、「コピー」 [!UICONTROL 、「] フォーム参照」の各セクションの非表示の複数行編集フィールドに移動することはなくなりました。

   * スクリーンリーダーは、 [!UICONTROL サイト参照] &amp; [!UICONTROL 言語コピーの要素の役割を読み上げるようになりました] 。

   * ブラウズモードでのスクリーンリーダーのフォーカスは、意味のある順序で様々な要素に移動します。

* [!UICONTROL メタデータスキーマエディター] ページとその要素にキーボードを使用してアクセスできるようになり、スクリーンリーダーに使いやすくなりました。(CQ-4290962、CQ-4272953)

* 選択したタグを削除する `X` 記号の目的が、選択したタグの数と共にスクリーンリーダーによって通知されるようになりました。(CQ-4273017)

* スクリーンリーダーを使用する近視眼的なユーザーが混乱しないように、装飾用のアイコンと画像がスクリーンリーダーで無視されるようになりました。(CQ-4272944)

**Experience Managerアセットで修正された問題**

[!DNL Adobe Experience Manager] 6.5.5.0 Assetsには、次の問題の修正が含まれています。

* [!UICONTROL コレクション内のアセットに対して「ワークフローを] 作成 [!UICONTROL 」ダイアログの「開始] 」オプションが無効になっているので、ワークフローがトリガーされません(NPR-32471)。

* メタデータスキーマでカスケーディングポップアップを使用する場合、（子のドロップダウンから）アポストロフィを含むドロップダウンオプションを選択して保存すると、アセットの [!UICONTROL プロパティ] (NPR-32649)を再度開いた後に、選択されたアポストロフィオプションが消えます。

* [!UICONTROL 「アセットインサイトの同期ジョブ] 」は、（Analytics側で）次のエントリ(NPR-32674)に移動する代わりに無効なエントリが見つかると停止し、失敗します。

* パノラマビューアのモバイルブラウザでは、モーションセンサーがデフォルトで無効になっているので、ジャイロは機能しません。(CQ-4272937)

* [!UICONTROL Connected Assets Configuration] （接続済みアセットの設定）ウィザードが、6.5.1(NPR-32730)に6.5.3をインストールした場合に、404エラーで動作しない。

* XMPの書き戻し処理中に、すべてのカスタム名前空間のメタデータプロパティで、カスタム名前空間のプレフィックスが、設定された名前空間のプレフィックス(NPR-32748)ではなくns2に変更されます。

* 遅延読み込みはトリガーされず、通知インボックス(NPR-32750)からタスクを確認するように選択した場合は、100アセットのみが表示されます。

* `NullPointerException` は、新しく作成されたユーザープロファイル(SAML/SSO)でノードの環境設定が見つからないために表示されます。 このエラーは、新しくログインしたユーザーが [!DNL Adobe Experience Manager Stock] 統合(NPR-32777)を使用するのを防ぎます。

* 10,000を超えるアセットを含むスマートコレクションを開くと、ログ内でトラバーサルの警告が観察されます(NPR-32980)。

* ダイナミックメディアScene7ランモード(NPR-32995)で [!DNL Adobe Experience Manager] 作業中にアセットを別のフォルダーに移動すると、アセット名が小文字に変更されます。

* 検索されたアセットは、検索結果からそのプロパティに移動した後で検索結果に戻って削除した後は削除できません(NPR-32998)。

* [!UICONTROL 「次へ] 」オプションは、「アセットを [!UICONTROL 移動] 」インターフェイスで移動先フォルダーを選択した場合に無効のままです(NPR-33356)。

* [!UICONTROL 親ノード（子フォルダーが1つ表示されるノード）を選択した後で子フォルダーを選択すると] (NPR-33275)、次のオプションは有効になりません。

* 読み取り、作成、または変更などの他の権限が付与されている場合でも、削除権限を持つAdobeのアセットリンク(AAL)では、チェックインおよびチェックアウトの権限が無効になります(NPR-33272)。

* スマート切り抜きレンディションは、アセットのダウンロードダイアログ(NPR-33167)では使用できません。

* スマート切り抜きプロファイルを含むフォルダーの下のPDFのレンディションパネルを開くログ(CQ-4294201)で例外が発生する。

* ダイナミックメディアScene7実行モード(CQ-4294200)とのExperience Manager時に [!UICONTROL ダイナミックメディア同期モード] がデフォルトで無効になっている場合、画像プリセットは公開されません。

* バルクアップロード中のアセット処理が停止し、ワークフローインスタンスにDAM更新アセットのスタックインスタンスが表示される(CQ-4293916)。

* Experience Managerでのダイナミックメディア設定の作成は機能しますが、ユーザーインターフェイスで「保存」を選択しても何も起こりません。(CQ-4292442)

* Safari/Macでのプログレッシブ再生でF4Vビデオアセットのプレビューが機能しない(CQ-4289844)。

* 親フォルダー内にあるアセットの名前にドット(.)文字が含まれたアセットをスマート切り抜き時に、追加のフォルダーが作成されます。(CQ-4289337) `.`

* サムネールが破損し、ビデオのコピー時にビデオ処理バナーが表示されません。(CQ-4284125)

* Firefoxで、空のカメラ表示を持つ一部のモデルについて、ディメンションビューアに空のサムネールが誤って表示される場合があります。(CQ-4283447)

* 6.5.5.0で修正されたパフォーマンスの問題は次のとおりです(CQ-4279206)。

   * 大きなバイナリをダイナミックメディア画像処理サーバーにアップロードするには、時間がかかり過ぎます。

   * ダイナミックメディアScene7アーキテクチャが原因で、Experience Manager時のサムネールの生成時間が長くなりました。

* 大量のアセットを持つお客様の場合、Dynamic MediaのScene7移行の問題が失敗する(CQ-4279206)。

* ビデオ360ビューワのレイアウトが使用され `setVideo` ると壊れ、使用時にビデオが下に移動し `video= modifier` ます(CQ-4263201)。

* Experience ManagerSDLパッケージ(NPR-33175)のインストール中にエラーメッセージが表示されます。

* Experience ManagerのSSRF脆弱性(NPR-33435)。

### プラットフォーム {#platform-6550}

* マップエントリが [!DNL Sling]`sling:match``/etc/maps` (NPR-33362)の下に作成された場合、フィルターは呼び出されません。
* (NPR-32988)を使用したセグメント化障害によるExperience Managerのクラッシュ [!DNL Apache Lucene] 。
* [!DNL Jackson] コアパッケージがExperience Manageruberjarファイルに見つかりません(NPR-32848)。
* CRXDE Liteは、ノードの `jcr:primaryType` プロパティ(NPR-32611)の読み取り権限を持たないユーザー向けにコンテンツを読み込みません。
* [!DNL Granite] メンテナンスタスクスケジューラーは、Experience Managerデプロイメント中に再初期化する頻度が高すぎます(CQ-4294627)。
* SQLクエリが長時間（例えば7時間）実行されると、Experience Managerは応答を停止します(NPR-33044)。

### ユーザーインターフェイス {#ui-6550}

* ラジオボタンの選択がマルチフィールド(NPR-33309)で保持されない。
* 遅延読み込みの制限は、リスト表示(NPR-33124)では機能しません。
* 一致がない場合、Omnisearchの結果ページにメッセージが表示されません(NPR-32974)。
* Omnisearchフィルタは、 `/content` nodeの下のすべての一致を返し、選択された場所(NPR-32849)は無視されます。

### 統合 {#integrations-6550}

* Adobe Targetコンポーネントを含むページが公開されると、内部キャッシュはクリアされます(NPR-33162)。
* Adobe Targetとの統合は11では機能しません(NPR-33111) [!DNL Windows Internet Explorer] 。
* Adobe Targetの設定時に、 [!UICONTROL 会社] と [!UICONTROL レポートスイート] (NPR-32502)の各フィールドはレポートソースの選択時に表示されません。
* AdobeI/O [!DNL Experience Fragments] を使用して書き出す場合、「Source Product」などのメタデータはAdobe Targetに書き出されません(NPR-32159)。
* ローカルExperience Managerの管理者グループに属する権限のあるIMSユーザーは、IMS設定を作成または変更できません(NPR-33045)。
* Adobeの起動の設定ページに、すべてのレコードが表示されるわけではありません(NPR-33011)。
* content-authorsグループのユーザーは、JavaScriptエラー(NPR-32996)が原因で、Adobe Targetコンポーネントのプロパティを編集できません。
* JSONのクロスサイトスクリプティング(NPR-32744)。

### 翻訳プロジェクト {#translation-6550}

* 翻訳済みのタグは、サードパーティの翻訳サービス(NPR-33154)からExperience Managerに読み込まれません。
* 翻訳設定ページに、翻訳に使用されたものとは異なる翻訳プロバイダーが表示されます(NPR-32971)。
* 既存の翻訳プロジェクトにエクスペリエンスフラグメントフォルダーを追加すると、新しいプロジェクトが作成されます(NPR-32843)。
* 翻訳ジョブの実行時にログに `NullPointerException` エラーが表示されます(NPR-32628)。

### WCM {#wcm-6550}

* ページエディタ — [!DNL Sites] ページエディタでは、キーボードのみのユーザーが、ヘッダーにあるすべてのオプションを介してタブフォーカスを移動する代わりに、メインコンテンツにスキップすることはできません。(CQ-4293883)
* ページエディター — 十分なコンポーネントを使用し、保存されたデータを含むパネルは、 [!DNL Chrome] およびの [!DNL Firefox] バージョン(CQ-4292995)での更新のため表示されません。
* MSM — ページからコンポーネントを削除しても、ページの公開バージョンからはコンポーネントは削除されません(CQ-4292360)。

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* Removing a published metadata schema from [!DNL Brand Portal] results in an error (CQ-4292063).
* 管理者がAdobe開発者コンソールを使用してBrand Portalを使用して6.5.4を設定した場合、ユー [!DNL Experience Manager Assets] ザは貢献度フォルダーのアセットをから [!DNL Brand Portal][!DNL Brand Portal][!DNL Experience Manager] (NPR-33046)に公開できません。
* 競合の原因となる親フォルダーの重複レプリケーション(NPR-33001)。

### [!DNL Communities] {#communities-6550}

* クイック編集メニューオプション(NPR-33117)を使用して、モデレートコンソールでカードを削除することはできません。
* [!UICONTROL アクティビティストリーム] ページ(NPR-33146)へのアクセス時にエラーが発生します。
* オーサーインスタンスで削除されたグループは、すべての発行インスタンス(NPR-33199)から削除されません。
* 作成者は、新しいグループを作成した後、11の [!UICONTROL コミュニティグループ][!DNL Internet Explorer] (NPR-33205)セクションにリダイレクトされません。
* Experience Managerの受信トレイでメッセージにアクセスしても、メッセージのステータスは読み取り(NPR-32764)に変更されません。
* グループを編集してサムネール画像を変更しても、グループサムネール画像は更新されません(NPR-32599)。 [!DNL Communities]
* ユーザは、コミュニティ内の別のユーザに電子メールを送信できません(NPR-32598)。
* 送信されたブログは、ユーザがページを更新するまで表示されません(NPR-32391)。
* ユーザー生成コンテンツ(UGC)の通知と購読のバージョンを作成すると、ソースページの誤ったIDが保存されます(CQ-4279355、CQ-4289703)。
* クロスサイトスクリプティングの問題(NPR-33203)。

### ワークフロー {#workflow-6550}

* 左側のレールの「 [!UICONTROL タイムライン] 」オプションの読み込みに、予想以上に時間がかかります(NPR-32851)。
* Experience Managerインスタンスを再起動した後、コレクションのレビュータスクの電子メールに、正しくないペイロードリンク(NPR-32774)が含まれます。

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Managerサービスパックには、の修正が含まれていません [!DNL Forms]。 別の Forms アドオンパッケージを使用して配布されます。さらに、JEE上のAEM Formsの修正を含む累積インストーラーがリリースされました。 For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Correspondence Management:レターを送信した後、ターゲット領域内のアセットの順序が変化する(NPR-33359、NPR-33153)。
* アダプティブForms:ユーザーがアダプティブフォームを編集すると、 [!UICONTROL ページ開始] ( [!UICONTROL Page Information] )メニューの「情報のワークフロー」オプションが機能しません(NPR-33004)。
* アダプティブForms:複数の添付ファイルが含まれるアダプティブフォームを保存できません(NPR-32997)。
* アダプティブForms:アダプティブフォームでパネルレイアウトを変更するとエラーが発生します(CQ-4293880)。
* アダプティブForms:アダプティブフォームの辞書の文字列に対する新しい行で、 `&#xa;` 文字が辞書(NPR-33266)に追加されます。
* アダプティブForms:ユーザーがアダプティブフォームをHTMLフォームとしてプレビューした場合、「 [!UICONTROL Scribble Signature] 」フィールドはタブのフォーカスを保持できません(NPR-33159)。
* アダプティブForms:アダプティブフォームの送信時に表示されるエラーメッセージは、 `aria-describedBy` 属性(NPR-33071)にリンクされません。
* アダプティブForms:アダプティブフォームで必須とマークされたフィールドのARIAアクセシビリティスキーマ(NPR-33070)では、必須属性が「True」に設定されていません。
* PDFGサービス：ユーザーがテキストファイルをPDFに変換すると、日本語の文字は正しくレンダリングされません(NPR-33238)。
* PDFGサービス： `CreatePDF` 操作は、PDFファイルをPDF OCR形式(NPR-32994)に変換できません。
* PDFGサービス：ドキュメントの200番目のインスタンス(NPR-32766)のPDF変換は失敗し [!DNL OpenOffice] ます。
* BackendIntegration:非アクティブな状態が正しくないために更新トークンの期限が切れると、フォームデータモデルの要求は失敗します(NPR-33169)。
* Designer:スクリーンリーダーは、XDPファイルで定義されているカスタムタブ順序の代わりに、デフォルトの地理的順序に基づいてタブ順序を実行します(NPR-32160)。
* Designer:タグ付けオプションを有効にすると、生成されたPDF出力でサブフォームの境界線が非表示になります(NPR-32778)。
* GuideSOMProviderServlet(NPR-32700)に格納されたXSS。

## Install 6.5.5.0 {#install}

**セットアップ要件**

* AEM 6.5.5.0 requires AEM 6.5. See [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* Service Packのダウンロードは、Adobe [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)(SDM)で入手できます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.5.5.0 をインストールしてください。
* インストールする前に、AEMインスタンスのスナップショットまたは新規バックアップを作成します。
* インストールする前にインスタンスを再起動してください。これは、インスタンスがまだ更新モードになっている場合（インスタンスが以前のバージョンから更新されたばかりの場合）にのみ必要ですが、インスタンスが長期間実行されていた場合にはお勧めします。

>[!NOTE]
>
>Adobeでは、Adobe Experience Manager6.5.5.0パッケージの削除またはアンインストールはお勧めしません。

### サービスパックのインストール {#install-service-pack}

既存のAdobe Experience Manager6.5インスタンスにService Packをインストールするには、次の手順を実行します。

1. Service Packを [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip)（ソフトウェア配布）からダウンロードします。

1. Open Package Manager and click **[!UICONTROL Upload Package]** to upload the package. 使用方法について詳しくは、 [パッケージマネージャーを参照してください](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/contentmanagement/package-manager.html)。

1. Select the package and click **[!UICONTROL Install]**.

>[!NOTE]
>
>Service Packのインストール中に、Package Manager UIのダイアログが閉じることがあります。 Adobeでは、エラーログが安定するのを待ってからデプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。 Typically, this happens on [!DNL Safari] but can intermittently happen on any browser.

**自動インストール**

作業インスタンスにAdobe Experience Manager6.5.5.0を自動的にインストールするには、次の2つの方法があります。

A.サーバーがオンラインで使用可能になったら、パッケージを `../crx-quickstart/install` フォルダーに配置します。 パッケージが自動的にインストールされます。

B. Package Managerの [HTTP APIを使用します](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html)。 ネストされたパッケージ `cmd=install&recursive=true` がインストールされるようにを使用します。

>[!NOTE]
>
>Adobe Experience Manager6.5.5.0は、Bootstrapのインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ(`/system/console/productinfo`)の「インストール済み製品 `Adobe Experience Manager (6.5.5.0)` 」に、更新済みのバージョン文字列が表示され ます。

1. All OSGi bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: `/system/console/bundles`).

1. The OSGI bundle `org.apache.jackrabbit.oak-core` is version 1.22.3 or higher (Use Web Console: `/system/console/bundles`).

このリリースで動作が確認されたプラットフォームについて詳しくは、 [技術要件を参照してください](/help/sites-deploying/technical-requirements.md)。

### Adobe Experience Manager Formsアドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>AEM Forms を使用していない場合はスキップしてください。Adobe Experience Manager Formsの修正は、別のアドオンパッケージを通じて提供されています。

1. Adobe Experience ManagerService Packがインストールされていることを確認します。
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### JEEへのAdobe Experience Manager Formsのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE上のAdobe Experience Manager Formsの修正は、別のインストーラーを使用して提供されています。

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes for patch 0014](https://helpx.adobe.com/jp/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

Experience Manager6.5.5.0のUberJarは、 [AdobeパブリックMavenリポジトリで使用できます](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/)。

MavenプロジェクトでUberJarを使用するには、UberJarの使用 [方法を参照し](/help/sites-developing/ht-projects-maven.md) 、プロジェクトPOMに次の依存関係を含めます。

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.5</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

この節では、AEM 6.5.5.0で非推奨としてマークされている機能と機能に関するリストを示します。今後のリリースで削除される予定の機能は、非推奨となる最初に設定され、代わりに使用するオプションがあります。

お客様は、現在の導入で機能を利用しているかどうかを確認し、別のオプションを使用するように導入を変更する計画を立てることをお勧めします。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | AEM **[!UICONTROL クラウドサービスのオプトイン画面は非推奨です]** 。 AEM 6.5で更新されたAEMとターゲットの統合により、AdobeIMSとI/Oを介した認証を使用するTarget Standard APIがサポートされ、AEMページの解析とパーソナライゼーションの実装でAdobe開始の役割が増加しているため、オプトインウィザードは機能的に無関係になりました。 | 各AEMクラウドサービスを介して、システム接続、AdobeIMS認証、AdobeI/O統合を設定します。 |
| コネクタ | AEM 6.5では、JCR Connector for Microsoft SharePoint 2010およびMicrosoft SharePoint 2013のAdobeが非推奨です。 | 該当なし |

## 既知の問題 {#known-issues}

* 6.5.5.0と11をインストールする場合は、Service Packのインストール後にサーバーを再起動し [!DNL Experience Manager][!DNL Java] ます。 Service Pack [!DNL Java] 8をインストールする場合は、再起動は必要ありません。

* If a folder in the hierarchy is renamed in [!DNL Experience Manager Assets] and the nested folder containing an asset is published to [!DNL Brand Portal], the title of the folder is not updated in [!DNL Brand Portal] until the root folder is published again.

* AEM 6.5.5.0のインストール時に、バージョン83のアップデートが原因でパッケージの構築に問題が発生して [!DNL Chrome] います。 問題を解決するには、 [!DNL Internet Explorer] およびなどの他の利用可能なブラウザー、 [!DNL Firefox]またはAEM標準のパッケージインストールオプションを使用します。 この問題はAEM 6.5.5.0のインストール後に解決されます。

* AEMの既定のメール送信者を使用してリモートSMTPサーバーに電子メールを送信できません。TLS v1.2を使用した通信のみが可能です。バンドルを削除し、更新して問題 `javax.mail:mail:1.5.0-b01` を解決し `system/console` てください。

* ユーザーがアダプティブフォームで初めてフィールドを設定することを選択した場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドの設定を選択すると、問題が解決します。

* インストール後に [!UICONTROL 接続されたアセットの設定] (Connected Assets Configuration `cq-remotedam-client-ui-content` )ウィザードが404エラーメッセージを返す場合は、Package Managerを使用して、パッケージ `cq-remotedam-client-ui-components` とパッケージを手動で再インストールします。

* AEM 6.5.x.xのインストール中に、次のエラーおよび警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して AEM に Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計機能が使用されると、アダプティブフォームのサーバー側検証に失敗します。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ダイナミックメディアのインタラクティブ画像のホットスポットは、買い物かご可能なバナービューアでアセットをプレビューすると表示されません。

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

AEM 6.5.5.0に含まれるOSGiバンドルとコンテンツパッケージに関する次のテキストドキュメントリストです。

* [AEM 6.5.5.0 に含まれている OSGi バンドルの一覧](assets/6550_bundles.txt)

* [AEM 6.5.5.0 に含まれているコンテンツパッケージの一覧](assets/6550_packages.txt)

## Restricted sites {#restricted-sites}

以下のサイトは既存ユーザーのみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [カスタマーサポート](https://docs.adobe.com/content/help/en/customer-one/using/home.html)へのお問い合わせサポートポータルへのアクセスについて詳しくは、「サポートポータル [へのアクセス](https://helpx.adobe.com/jp/experience-manager/kb/accessing-aem-support-portal.html)」を参照してください。

>[!MORELIKETHIS]
>
>* [AEM 6.5 リリースノート](/help/release-notes/release-notes.md)
>* [AEM 製品ページ](https://www.adobe.com/marketing/experience-manager.html)
>* [AEM 6.5 ドキュメント](https://helpx.adobe.com/jp/support/experience-manager/6-5.html)
>* [Adobe優先度の製品アップデートの購読](https://www.adobe.com/subscription/priority-product-update.html)

