---
title: AEM 6.5 Service Pack リリースノート
description: Adobe Experience Manager 6.5 Service Pack 5 固有のリリースノート
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d51577195e969ff8af31be49159ff575e3654cc9
workflow-type: tm+mt
source-wordcount: '4476'
ht-degree: 11%

---


# Adobe Experience Manager 6.5 Service Packリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | **Adobe Experience Manager 6.5** |
|---|---|
| バージョン | 6.5.5.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2020年6月4日 |
| ダウンロード URL | [パッケージ共有](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/AEM-6.5.5.0-Service-Pack)、 [ソフトウェア配布 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) |

## Adobe Experience Manager 6.5.5.0の機能 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.5.0は、2019 **年4月のGAリリース(GA)以降にリリースされた主な機能、お客様からリクエストされた機能強化、パフォーマンス、安定性、セキュリティの向上を含む重要なアップデートで**&#x200B;す。 Adobe Experience Manager (AEM) 6.5にインストールできます。

AEM 6.5.5.0で導入された主な機能および機能強化には、次のものが含まれます。

* AEMインボックスに表示する列名のカスタマイズ

* ページエディター、コアコンポーネント、RTE、管理者ユーザーインターフェイスなど、AEM Webコンテンツ管理(WCM)の様々な領域でのアクセシビリティの向上。

* 対話型通信を下書きとして保存する。

* JEE上 [!DNL Oracle WebLogic 12] のAEM Formsのサポート。

* ア [!DNL Adobe Experience Manager] セットユーザーインターフェイスのフローでの例外処理が改善されました。

* Dynamic Media Scene7の公開URL `getRemoteAssetPublishURL` を取得するための新しいメソッドがインター `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` フェイスに追加されました。

* [Webコンテンツアクセシビリティガイドライン](#assets-6550-changes) (WCAG)に準拠した [!DNL Adobe Experience Manager] アセットのアクセシビリティの強化。

* Adobe Experience Managerとのパッケージ共有の統合が削除されました。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.22.3 に更新しました。

AEM 6.5 Service Pack 5で導入された機能、主な特長、主な機能の完全なリストについては、Adobe Experience Manager 6.5 Service Pack 5の新機能を参照して [ください](new-features-latest-service-pack.md) 。

6.5.5.0リリースでの修正のリスト [!DNL Experience Manager] を次に示します。

### Sites {#sites-6550}

* AEMサイトには、エイリアスからページを公開または非公開するオプションが用意されています。 このオプションは機能しません(NPR-33415)。
* 複数のテンプレートを含むテンプレートからレイアウトコンテナを削除すると、そのテンプレートは正しくレンダリングされません(NPR-33347)。
* AEMサイトページが複数のライブコピーを持つ大きなコンテンツセットに含まれている場合、ページバージョン履歴プレビューの読み込みに失敗します(NPR-33311)。
* 「移動」コマンドを使用してAEMサイトページの名前を変更する場合、ページタイトルは更新されません(NPR-33264)。
* 列表示内でページを移動すると、列は表示されなくなります(NPR-33216)。
* 言語コピーのローカルコンポーネントの名前が、ブループリントのコンポーネントの名前と同じで、コンポーネントがブループリントからロールアウトされる場合、ローカルコンポーネントの名前に_msm_movedという用語は追加されません(NPR-33208)。
* Page Redirectサーブレットは、.htmlをAEMサイトのURLに追加します。このURLでは、ResourceTypeがcq:Pageではありません(NPR-33176)。
* サブツリーを貼り付ける場合、対応するサブページを貼り付けるかどうかを決定するオプションはありません(NPR-33149)。
* コンポーネントのライブ使用の結果の数は、49個に制限されます(NPR-33058)。
* スキーマに基づくコンテンツフラグメントのベースとなり、そのコンテンツに必須のテキスト領域またはパスフィールドが含まれている場合、コンテンツフラグメントは保存されません(NPR-33007)。
* 既製のエクスペリエンスフラグメントコンポーネントを使用してカスタムコンポーネントを作成し、それをAEMサイトページで使用する場合、AEMはカスタムコンポーネント(NPR-32852)の参照（使用）を表示しません。
* 多数の参照を持つフォルダーの名前を変更すると、そのフォルダーへの多くの参照は更新されません(NPR-32765)。
* ソース編集オプションを有効にすると、インラインのフルスクリーンオプションで使用できるようになりますが、リッチテキストエディターの編集ダイアログおよびフルスクリーンオプションでは使用できなくなります(NPR-32763)。
* 複数フィールドがあり、そのフィールドに青写真のページプロパティに必須のフィールド（ドロップダウンやパスフィールドなど）が含まれている場合、そのような複数フィールドを含むページをロールアウトすると、ライブコピーのページプロパティは保存されません。 (NPR-32751)
* スクリーンリーダーは、見出し構造を使用してページを移動することはできません。 さらに、「Components（コンポーネント）」タブのラベルが誤っています(NPR-32648)。
* ページ番号の開始では、エクスペリエンスフラグメントピッカーはすべての項目を読み込みません(NPR-32605)。
* ライブコピーを読み取り、変更、作成および削除する作成者権限は失効します。 各発言者は、Blueprint内でページを移動するための読み取り権限と変更権限を明示的に提供する必要がありました(NPR-32550)。
* Adobe Analytics(NPR-32548)と統合されているページで、コンテンツ作成者が「起動」を作成できません。
* ユーザーが同期による継承を再開すると、親ページのライブコピーは青写真と同期せず、誤ったステータスを表示します(NPR-32500)。
* AEMサイトのエディターページの読み込みに15秒以上かかる(NPR-32413)。
* 一部のフィールドでは、「継承をキャンセル」オプションが表示されません(NPR-32362)。
* エクスペリエンスフラグメントコンポーネントのパスを選択し、「選択ダイアログを開く」チェックボックスを選択した場合、パスブラウザー(NPR-32308)で選択されたパスに移動しません。
* AEM 6.2からAEM 6.5にアップグレードした場合、静的テンプレートのParsysコンポーネントが正しく表示されません。 Parsysコンポーネントの高さは0に設定され、その中のコンポーネントは表示されません。 (NPR-33663).
* ユーザーがレイアウトコンテナをコピーして同じページに貼り付けた場合、レイアウトコンテナのコンポーネントは表示されません(NPR-33648)。
* ディスパッチャーの正常性チェックで、ログファイルに `Invalid cookie header` 警告メッセージが表示されます(NPR-33629)。

### Assets {#assets-6550-changes}

**Experience Managerアセットのアクセシビリティの強化**

* 「 [!UICONTROL Comments] リスト」と「クリック可能」オプションにキーボードフォーカスを移し、「アセットのTimeline [!UICONTROL パネルで新しいバージョン] を作成(NPR33424)」の下の  「バージョンコメントを作成」に移動できるようになりました。

* アセットの「 [!UICONTROL 表示設定] 」オプションに移動し、キーボードキーを使用して [!UICONTROL 表示設定] (NPR-33420)ダイアログの設定を変更できるようになりました。

* コンボボックス（異なるページ上の様々なフィールド）のリストボックスドロップダウンに、スクリーンリーダーがアナウンスできるオプションのリストとしてエントリが表示されるようになりました。(NPR-33516)

* 並べ替え可能なヘッダー(リスト表示、 [!UICONTROL タイムライン、およびパブリケーション] 表示の  管理ページ)の並べ替え機能が、スクリーンリーダーによって通知され、列ヘッダーの並べ替えコントロールがキーボード(NPR-32979)を使用してアクセスできるようになりました。

* クリック可能な要素（コメントカード、バージョン更新、コンボボックス、メニューの山形アイコンなど）は、キーボード(NPR-33514)を使用して、フォーカス可能でアクション可能になりました。

* インサイト表示のインサイトアイコン（使用方法、インプレッション数およびクリック数）の機能（またはアクションの目的）が、スクリーンリーダー  (NPR-33513)によって正しくアナウンスされるようになりました。

* 読み取り専用のフォームフィールド(例えば、アセットの [!UICONTROL プロパティの「] 基本」タブの無効なフィールド )が、キーボード(NPR-33493、CQ-4273031)を使用してフォーカスできるようになりました。

* 様々な入力フィールドのラベルが、テキストの入力時に消えたプレースホルダーラベルだけでなく、永続的なラベル（アクセス可能）になりました。(NPR-33475)

* 異なる見出しレベル（ページタイトルやセクションの見出しなど）が、スクリーンリーダーユーザーに対して異なるレベルの見出しとして認識されるようになりました(NPR-33471)。

* リンクやオプション（アセットページのヘッダーやズームオプション、フォルダーナビゲーション）などのインタラクティブなユーザーインターフェイス要素は、キーボード(NPR-33468、CQ-4271412)を使用してアクセスできるようになりました。

* [ [!UICONTROL ワークフロー]、[]範囲 、および[] ]の各進行状況インジケータは、タブ(NPR-33416)ではなく、スクリーンリーダーによって正しく読み上げられるようになりました。

* 星評価アイコンの色(アセットのプ [!UICONTROL ロパティの「] 詳細」タブやカードの表示の「 [!UICONTROL Rating] 」セクションなど)は、視覚が限られ、色の知覚がないユーザーに対しては、適切なコントラストが表示されるように変更されます(NPR-33414)。

* アセットの詳細ページの [!UICONTROL コメント] フィールドの横にある山形の上向き矢印が、キーボードキーを使用してアクセスできるようになりました(NPR-33397)。

* アセットのプ [!UICONTROL ロパティ] と左側のナビゲーション（アセットのユーザーインターフェイス上）のタグ [!UICONTROL (Tags] )ダイアログの展開状態と折りたたまれた状態が、スクリーンリーダー(NPR-33396)によって正しく通知されるようになりました。

* ア [!DNL Adobe Experience Manager] セットの閲覧されたすべてのページのタイトルが一意になりました(NPR-33343)。

* ツリー構造をナビゲートする際に、ツリー表示コントロールの様々な要素がスクリーンリーダー(NPR-33304)によって正しく通知されるようになりました。

* アセットの詳細ページの [!UICONTROL Timeline] 表示にあるアセットの異なるバージョンが、キーボードキーを使用してアクセスできるようになりました(NPR-33283)。

* Omnisearchコンボボックスに表示される検索候補の名前が、検索機能を使用している間、スクリーンリーダーによってアナウンスされるようになりました(NPR-33280)。

* スクリーンリーダーは、クリッ [!UICONTROL ク可能な要素と「] 参照」パネルの「リンクへ移動 [!UICONTROL 」をクリック可能な要素としてアナウンスします] (NPR-33278)。

* 共有リンクダイアログのテーブル構造情報（行1、セル1、テーブルなど）は、ダイアログが開いたときに、スクリ [!UICONTROL ーンリーダーによって通知されなくなりました] (NPR-33268)。

* 様々なコンボボックス要素（パスフィールドや、アセットのプロパティの「基本」タブで選択ダイアログを開くオプションなど）の目的が、スクリーンリーダー(NPR-33235)によって正しく通知されるようになりました。

* リスト表示テーブルの行が選択可能であるという情報が、キーボードフォーカスがある場合に、スクリーンリーダーユーザーに通信されるようになりました。 この情報は、行上でマウスをポインターで移動すると(NPR-33234)、通知されます。

* ( [!UICONTROL xを含む)に設定した場合、]基本 [!UICONTROL タブのPropertiesNprの「] Tags [!UICONTROL (タグ] )」フィールドの下にある選択した各タグを削除するオプションが、スクリーンリーダー(NPR-33206)にアクセスできるようになりました。

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

* ファイルサイズフィルターの下限([!UICONTROL 送信者])と上限(宛先)の入力フィールドの目的が、近視眼的なスクリーンリーダーユーザー(NPR-32064)に対して通知されるようになりました。

* 「 [!UICONTROL 作成と翻訳] 」フォームの「 [!UICONTROL 言語] 」メニューにブラウズモードでアクセスできるようになりました。(CQ-4293906)

* 次の機能強化により、 [!UICONTROL References] パネルにアクセスできるようになりました(NPR-33261、CQ-4293798)。

   * ブラウズモードで、スクリーンリーダーのフォーカスが、「 [!UICONTROL サイト参照]」、「 [!UICONTROL アセット参照]」、「コピー」 [!UICONTROL 、「] フォーム参照」の各セクションの非表示の複数行編集フィールドに移動することはなくなりました。

   * スクリーンリーダーは、 [!UICONTROL サイト参照] &amp; [!UICONTROL 言語コピーの要素の役割を読み上げるようになりました] 。

   * ブラウズモードでのスクリーンリーダーのフォーカスは、意味のある順序で様々な要素に移動します。

* [!UICONTROL メタデータスキーマエディター] ページとその要素にキーボードを使用してアクセスできるようになり、スクリーンリーダーに使いやすくなりました。(CQ-4290962、CQ-4272953)

* 現在選択されているタグを削除するオプションの [!UICONTROL x] アイコンの目的も、選択されているタグの数と共に通知されます(CQ-4273017)。

* スクリーンリーダーを使用する目の見えないユーザーにとって混乱が生じないように、装飾的なアイコンと画像がスクリーンリーダーで無視されるようになりました。(CQ-4272944)

**Experience Manager Assetsで修正された問題**

[!DNL Adobe Experience Manager] 6.5.5.0 Assetsには、次の問題の修正が含まれています。

* [!UICONTROL コレクション内のアセットに対して「ワークフローを] 作成 [!UICONTROL 」ダイアログの「開始] 」オプションが無効になっているので、ワークフローがトリガーされません(NPR-32471)。

* メタデータスキーマでカスケーディングドロップダウンを使用している間、（子ドロップダウンから）アポストロフィを含むドロップダウンオプションを選択して保存すると、アセットの [!UICONTROL プロパティ] (NPR-32649)を再度開いた後に、選択されたアポストロフィオプションが消えます。

* [!UICONTROL 「アセットインサイトの同期ジョブ] 」は、（Analytics側で）次のエントリ(NPR-32674)に移動する代わりに無効なエントリが見つかると停止し、失敗します。

* パノラマビューアのモバイルブラウザでは、モーションセンサーがデフォルトで無効になっているので、ジャイロは機能しません。(CQ-4272937)

* [!UICONTROL Connected Assets Configuration] （接続済みアセットの設定）ウィザードが、6.5.1(NPR-32730)に6.5.3をインストールした場合に、404エラーで動作しない。

* XMPの書き戻し処理中に、すべてのカスタム名前空間のメタデータプロパティで、設定された名前空間プレフィックス(NPR-32748)ではなく、カスタム名前空間プレフィックスがns2に変更されます。

* 遅延読み込みはトリガーされず、通知インボックス(NPR-32750)からタスクを確認するように選択した場合は、100アセットのみが表示されます。

* `NullPointerException` は、新しく作成されたユーザープロファイル(SAML/SSO)でノードの環境設定が見つからないために表示されます。 このエラーは、新しくログインしたユーザーが [!DNL Adobe Experience Manager Stock] 統合(NPR-32777)を使用するのを防ぎます。

* 10,000を超えるアセットを含むスマートコレクションを開くと、ログ内でトラバーサルの警告が観察されます(NPR-32980)。

* Dynamic Media Scene7 runmode(NPR-32995)で [!DNL Adobe Experience Manager] 作業中にアセットを別のフォルダに移動すると、アセット名が小文字に変更されます。

* 検索されたアセットは、検索結果からそのプロパティに移動した後で検索結果に戻って削除した後は削除できません(NPR-32998)。

* [!UICONTROL 「次へ] 」オプションは、「アセットを [!UICONTROL 移動] 」インターフェイスで移動先フォルダーを選択した場合に無効のままです(NPR-33356)。

* [!UICONTROL 親ノード（子フォルダーが1つ表示されるノード）を選択した後で子フォルダーを選択すると] (NPR-33275)、次のオプションは有効になりません。

* 削除権限を持つユーザーに対しては、Adobe Asset Link(AAL)でチェックインおよびチェックアウトの権限が無効になります。読み取り、作成、変更などの他の権限が許可されている場合も同様です(NPR-33272)。

* スマート切り抜きレンディションは、アセットのダウンロードダイアログ(NPR-33167)では使用できません。

* スマート切り抜きプロファイルを含むフォルダーの下のPDFのレンディションパネルを開くログ(CQ-4294201)で例外が発生する。

* ダイナミックメディアシンクモード  (CQ-4294200)がダイナミックメディアScene7実行モードを持つAEMでデフォルトでダイナミックメディア同期モードが無効になっている場合、画像プリセットは公開されません。

* バルクアップロード中のアセット処理が停止し、ワークフローインスタンスにDAM更新アセットのスタックインスタンスが表示される(CQ-4293916)。

* AEMでのダイナミックメディア設定の作成は機能しますが、ユーザーインターフェイスで「保存」を選択しても何も起こりません。(CQ-4292442)

* Safari/Macでのプログレッシブ再生で、f4vビデオアセットのプレビューが機能しない(CQ-4289844)。

* 親フォルダー内にあるアセットの名前にドット(.)文字が含まれたアセットをスマート切り抜き時に、追加のフォルダーが作成されます。(CQ-4289337) `.`

* サムネールが破損し、ビデオのコピー時にビデオ処理バナーが表示されません。(CQ-4284125)

* Firefoxで、空のカメラ表示を持つ一部のモデルについて、ディメンションビューアに空のサムネールが誤って表示される場合があります。(CQ-4283447)

* 6.5.5.0で修正されたパフォーマンスの問題は次のとおりです(CQ-4279206)。

   * 大きなバイナリをダイナミックメディア画像処理サーバーにアップロードするには、時間がかかり過ぎます。

   * Dynamic Media Scene7アーキテクチャにより、AEMでのサムネールの生成時間が長くなりました。

* 大量のアセットを持つお客様のDynamic Media Scene7への移行に失敗する問題(CQ-4279206)。

* ビデオ360ビューワのレイアウトが使用され `setVideo` ると壊れ、使用時にビデオが下に移動し `video= modifier` ます(CQ-4263201)。

* AEM SDLパッケージ(NPR-33175)のインストール中にエラーメッセージが表示されます。

### プラットフォーム {#platform-6550}

* マップエントリが [!DNL Sling]`sling:match``/etc/maps` (NPR-33362)の下に作成された場合、フィルターは呼び出されません。
* (NPR-32988)を使用したセグメント化障害により、AEMがクラッシュ [!DNL Apache Lucene] する。
* [!DNL Jackson] コアパッケージがAEM uber jarファイル(NPR-32848)に見つかりません。
* CRXDE Liteは、ノードの `jcr:primaryType` プロパティに対するREAD権限を持たないユーザーのコンテンツを読み込みません(NPR-32611)。
* [!DNL Granite] メンテナンスタスクスケジューラーは、AEMデプロイメントの間、再初期化の頻度が高すぎます(CQ-4294627)。
* SQLクエリが7時間など長い時間実行されると、AEMは応答を停止します(NPR-33044)。

### ユーザーインターフェイス {#ui-6550}

* ラジオボタンの選択がマルチフィールド(NPR-33309)で保持されない。
* 遅延読み込みの制限は、リスト表示(NPR-33124)では機能しません。
* 一致がない場合、Omnisearchの結果ページにメッセージが表示されません(NPR-32974)。
* Omnisearchフィルタは、 `/content` nodeの下のすべての一致を返し、選択された場所(NPR-32849)は無視されます。

### 統合 {#integrations-6550}

* Adobeターゲットコンポーネントを含むページが公開されると、内部キャッシュはクリアされます(NPR-33162)。
* アドビのターゲットとの統合は11(NPR-33111)では機能しま [!DNL Windows Internet Explorer] せん。
* Adobeターゲットの設定時に、会社ソース(NPR-32502)の選択時に [!UICONTROL レポート] と [!UICONTROL レポートスイート] の各フィールドが表示されません。
* Adobe I/Oを使用してエクスペリエンスフラグメントを書き出す場合、「ソース製品」などのメタデータはAdobeターゲット(NPR-32159)に書き出されません。
* ローカルのAEM管理者グループに属する権限のあるIMSユーザーは、IMS設定を作成または変更できません(NPR-33045)。
* Adobe Launchの設定ページにすべてのレコードが表示されるわけではありません(NPR-33011)。
* JavaScriptエラー(NPR-32996)が原因で、content-authorsグループのユーザーはAdobeターゲットコンポーネントのプロパティを編集できません。

### 翻訳プロジェクト {#translation-6550}

* 翻訳済みのタグは、サードパーティの翻訳サービス(NPR-33154)からAEMに読み込まれません。
* 翻訳設定ページに、翻訳に使用されたものとは異なる翻訳プロバイダーが表示されます(NPR-32971)。
* 既存の翻訳プロジェクトにエクスペリエンスフラグメントフォルダーを追加すると、新しいプロジェクトが作成されます(NPR-32843)。
* 翻訳ジョブの実行時にログに `NullPointerException` エラーが表示されます(NPR-32628)。

### WCM {#wcm-6550}

* ページエディタ — [!DNL Sites] ページエディタでは、キーボードのみのユーザーが、ヘッダーにあるすべてのオプションを介してタブフォーカスを移動する代わりに、メインコンテンツにスキップすることはできません。(CQ-4293883)
* ページエディター — 十分なコンポーネントを使用し、保存されたデータを含むパネルは、 [!DNL Chrome] およびの [!DNL Firefox] バージョン(CQ-4292995)での更新のため表示されません。
* MSM — ページからコンポーネントを削除しても、ページの公開バージョンからはコンポーネントは削除されません(CQ-4292360)。

### Brand Portal {#assets-brand-portal-6550}

* 公開済みのメタデータスキーマをから削除すると、エラー [!DNL Brand Portal] が発生します(CQ-4292063)。
* 管理者がAdobe Developer Consoleを使用してBrand Portalを使用して [!DNL Experience Manager Assets] 6.5.4を設定した場合、ユー [!DNL Brand Portal] ザーは、貢献度フォルダーのアセットをからに発行でき [!DNL Brand Portal] ません [!DNL Experience Manager]。 (NPR-33046).
* 競合の原因となる親フォルダーの重複レプリケーション(NPR-33001)。

### Communities {#communities-6550}

* クイック編集メニューオプション(NPR-33117)を使用して、モデレートコンソールでカードを削除することはできません。
* [!UICONTROL アクティビティストリーム] ページ(NPR-33146)へのアクセス時にエラーが発生します。
* オーサーインスタンスで削除されたグループは、すべての発行インスタンス(NPR-33199)から削除されません。
* 作成者は、新しいグループを作成した後、11の [!UICONTROL コミュニティグループ][!DNL Internet Explorer] (NPR-33205)セクションにリダイレクトされません。
* AEMのインボックスでメッセージにアクセスしても、メッセージのステータスは読み取り(NPR-32764)に変更されません。
* グループを編集してサムネール画像を変更しても、グループサムネール画像は更新されません(NPR-32599)。 [!DNL Communities]
* ユーザは、コミュニティ内の別のユーザに電子メールを送信できません(NPR-32598)。
* 送信されたブログは、ユーザがページを更新するまで表示されません(NPR-32391)。
* ユーザー生成コンテンツ(UGC)の通知と購読のバージョンを作成すると、ソースページの誤ったIDが保存されます(CQ-4279355、CQ-4289703)。

### ワークフロー {#workflow-6550}

* 左側のレールの「 [!UICONTROL タイムライン] 」オプションの読み込みに、予想以上に時間がかかります(NPR-32851)。
* AEMインスタンスを再起動した後、コレクションのレビュータスクの電子メールに、誤ったペイロードリンクが含まれます(NPR-32774)。

### Forms {#forms-6550}

>[!NOTE]
>
>AEM サービスパックには、AEM Forms の修正は含まれません。別の Forms アドオンパッケージを使用して配布されます。さらに、JEE上のAEM Formsの修正を含む累積インストーラーがリリースされました。 For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Correspondence Management: レターを送信した後、ターゲット領域内のアセットの順序が変化する(NPR-33359、NPR-33153)。
* アダプティブフォーム： ユーザーがアダプティブフォームを編集すると、 [!UICONTROL ページ開始] ( [!UICONTROL Page Information] )メニューの「情報のワークフロー」オプションが機能しません(NPR-33004)。
* アダプティブフォーム： 複数の添付ファイルが含まれるアダプティブフォームを保存できません(NPR-32997)。
* アダプティブフォーム： アダプティブフォームでパネルレイアウトを変更するとエラーが発生します(CQ-4293880)。
* アダプティブフォーム： アダプティブフォームの辞書の文字列に対する新しい行で、 `&#xa;` 文字が辞書(NPR-33266)に追加されます。
* アダプティブフォームのアクセシビリティ： ユーザーがアダプティブフォームをHTMLフォームとしてプレビューした場合、「 [!UICONTROL Scribble Signature] 」フィールドはタブのフォーカスを保持できません(NPR-33159)。
* アダプティブフォームのアクセシビリティ： アダプティブフォームの送信時に表示されるエラーメッセージは、 `aria-describedBy` 属性(NPR-33071)にリンクされません。
* アダプティブフォームのアクセシビリティ： アダプティブフォームで必須とマークされたフィールドのARIAアクセシビリティスキーマ(NPR-33070)では、必須属性が「True」に設定されていません。
* PDFGサービス： ユーザーがテキストファイルをPDFに変換すると、日本語の文字は正しくレンダリングされません(NPR-33238)。
* PDFGサービス： `CreatePDF` 操作は、PDFファイルをPDF OCR形式(NPR-32994)に変換できません。
* PDFGサービス： ドキュメントの200番目のインスタンス(NPR-32766)のPDF変換は失敗し [!DNL OpenOffice] ます。
* BackendIntegration: 非アクティブな状態が正しくないために更新トークンの期限が切れると、フォームデータモデルの要求は失敗します(NPR-33169)。
* Designer: スクリーンリーダーは、XDPファイルで定義されているカスタムタブ順序の代わりに、デフォルトの地理的順序に基づいてタブ順序を実行します(NPR-32160)。
* Designer: タグ付けオプションを有効にすると、生成されたPDF出力でサブフォームの境界線が非表示になります(NPR-32778)。

## Install 6.5.5.0 {#install}

**セットアップ要件**

* AEM 6.5.5.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* サービスパックは AEM 6.5 インスタンスから直接アクセスできるパッケージ共有からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用してオーサーインスタンスの 1 つに AEM 6.5.5.0 をインストールしてください。
* インストールする前に、AEMインスタンスのスナップショットまたは新規バックアップを作成します。
* インストールする前にインスタンスを再起動してください。これは、インスタンスがまだ更新モードになっている場合（インスタンスが以前のバージョンから更新されたばかりの場合）にのみ必要ですが、インスタンスが長期間実行されていた場合にはお勧めします。

>[!NOTE]
>
>AEM 6.5.5.0 パッケージを削除またはアンインストールすることはお勧めしません。

### サービスパックのインストール {#install-service-pack}

既存の AEM 6.5 インスタンスに Service Pack をインストールするには、次の手順を実行します。

1. 「 [Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/AEM-6.5.5.0-Service-Pack) 」または「 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.5.zip) 」リンクをクリックして、パッケージをダウンロードします。

1. パッ [ケージマネージャーを開き](http://localhost:4502/crx/packmgr/index.jsp) 、「パッケージを **アップロード** 」をクリックしてパッケージをアップロードします。

1. パッケージ名を選択し、「 **インストール**」をクリックします。

>[!NOTE]
>
>**6.5.5.0 のインストール中に、パッケージマネージャー UI のダイアログが途中で終了することがあります。**
>
>そのため、エラーログが安定するのを待ってから、インスタンスにアクセスすることをお勧めします。ユーザーは、アップデーターバンドルのアンインストールに関連する特定のログを待ってから、インストールが正常に行われることを確認する必要があります。 通常は、Safari で発生しますが、任意のブラウザーで断続的に発生する可能性があります。

**自動インストール**

実行中のインスタンスに AEM 6.5.5.0 を自動的にインストールするには、次の 2 つの方法があります。

A. Place the package into `../crx-quickstart/install ` folder while the server is available online. パッケージは自動的にインストールされます。

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use `cmd=install&recursive=true` - so the nested packages  are  installed.

>[!NOTE]
>
>AEM 6.5.5.0 では、ブートストラップインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ(/system/console/ productinfo)の「インストール済み製品」に、更新済みのバージョン文字列 `Adobe Experience Manager, Version 6.5.5.0` が表示されます。

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. The OSGI bundle `org.apache.jackrabbit.oak-core` is on version 1.10.6 or higher (Use Web Console: `/system/console/bundles`).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>AEM Forms を使用していない場合はスキップしてください。AEM Forms の修正は、個別のアドオンパッケージを介して配信されます。

1. AEM Service Pack がインストールされていることを確認してください。
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE上のAEM Formsに関する修正は、別のインストーラーを使用して提供されます。

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0014](https://helpx.adobe.com/jp/aem-forms/quick-fixes/6-5/jee-patch-0014.html).

### UberJar {#uber-jar}

The UberJar for AEM 6.5.5.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.5/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

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

この節では、AEM 6.5.5.0で非推奨とマークされている機能に関するリストを紹介します。今後のリリースで削除される予定の機能は、非推奨となる最初に設定され、代わりの使用方法が用意されています。

お客様は、現在の導入で機能を利用しているかどうかを確認し、別のオプションを使用するように導入を変更する計画を立てることをお勧めします。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. AEMとターゲットの統合がAEM 6.5で更新され、Adobe IMSとI/Oを介した認証を使用するターゲット標準APIがサポートされるようになりました。また、分析とパーソナライゼーションのためのAEMページの実装が増えているため、オプトインウィザードは機能的に無関係です。 | 各AEMクラウドサービスを介したシステム接続、Adobe IMS認証、Adobe I/O統合の設定 |

## 既知の問題 {#known-issues}

* 6.5.5.0と11をインストールする場合は、Service Packのインストール後にサーバーを再起動し [!DNL Experience Manager][!DNL Java] ます。 Service Pack [!DNL Java] 8をインストールする場合は、再起動は必要ありません。

* 階層内のフォルダーの名前がに変更され、アセットを含むネストされたフォルダーがにパブリッシュされる場合 [!DNL Experience Manager Assets] 、ルートフォルダーが再度パブリッシュされ [!DNL Brand Portal][!DNL Brand Portal] るまで、フォルダーのタイトルはで更新されません。

* バージョン83の更新により、 [!DNL chrome] パッケージの構築で問題が発生しています。 この問題を解決するには、 [!DNL Internet Explorer] およびなどの他の利用可能なブラウザー、 [!DNL Firefox]またはAEM標準のパッケージインストールオプションを使用します。

* AEM既定のメール送信者を使用してリモートSMTPサーバーに電子メールを送信できません。TLS v1.2を使用した通信のみが可能です。バンドルを削除し、更新し `javax.mail:mail:1.5.0-b01` て問題を解決し `system/console` てください。

* ユーザーがアダプティブフォームで初めてフィールドを設定することを選択した場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドの設定を選択すると、問題が解決します。

* インストール後に [!UICONTROL 接続されたアセットの設定] (Connected Assets Configuration `cq-remotedam-client-ui-content` )ウィザードが404エラーメッセージを返す場合は、Package Managerを使用して、パッケージ `cq-remotedam-client-ui-components` とパッケージを手動で再インストールします。

* AEM 6.5.x.xのインストール中に、次のエラーおよび警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して AEM に Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計機能が使用されると、アダプティブフォームのサーバー側検証に失敗します。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

AEM 6.5.5.0に含まれるOSGiバンドルとコンテンツパッケージに関する次のテキストドキュメントリストを参照してください。

* [AEM 6.5.5.0 に含まれている OSGi バンドルの一覧](assets/6550_bundles.txt)

* [AEM 6.5.5.0 に含まれているコンテンツパッケージの一覧](assets/6550_packages.txt)

## Restricted sites {#restricted-sites}

以下のサイトは既存ユーザーのみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [カスタマーサポート](https://docs.adobe.com/content/help/en/customer-one/using/home.html)へのお問い合わせサポートポータルへのアクセスについて詳しくは、「サポートポータル [へのアクセス](https://helpx.adobe.com/jp/experience-manager/kb/accessing-aem-support-portal.html)」を参照してください。

>[!MORELIKETHIS]
>
>* [AEM 6.5 リリースノート](/help/release-notes/release-notes.md)
>* [AEM 製品ページ](https://www.adobe.com/solutions/web-experience-management.html)
>* [AEM 6.5 ドキュメント](https://helpx.adobe.com/jp/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

