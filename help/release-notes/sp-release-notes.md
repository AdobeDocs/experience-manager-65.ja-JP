---
title: '[!DNL Experience Manager] 6.5サービスパックリリースノート'
description: リリースノート（ [!DNL Adobe Experience Manager] 6.5 service pack 9に固有）
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: c59ec6e2429095c07c9b2d6bb83dad6ab4f80aa0
workflow-type: tm+mt
source-wordcount: '3837'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5サービスパックリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.9.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2021 年 5 月 27 日 |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip) |

## [!DNL Adobe Experience Manager] 6.5.9.0に含まれるもの {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.9.0には、2019年4月の6.5リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善が含まれています。サービスパックは[!DNL Adobe Experience Manager] 6.5にインストールされています。

[!DNL Adobe Experience Manager] 6.5.9.0で導入された主な機能と機能強化は次のとおりです。

* [!DNL Experience Manager Sites] Dynamic Media Foundationコンポーネントで、レスポンシブな画像プリセットまたはスマート切り抜きを使用する際に、高解像度のデバイス向けの最適化のオン/オフを切り替えることができるようになりました。

* パフォーマンスを向上させるために、`hidden=false`条件をJCRクエリから[!UICONTROL QueryBuilder]エバリュエーターに移動します。 変更後に非表示の述語が機能していることを確認するために、[!DNL Experience Manager]は非表示のフォルダーが表示されていないことを確認します。

* [!DNL Experience Manager Sites]ページで削除されたページとツリーを復元する機能。

* 新しいユーザーがメーラー設定サービスの更新トークンを使用してアクセストークンを更新する機能をサポートします。

* [メール設定サービスのSMTP XOAUTH2](/help/sites-administering/notification.md#setting-up-oauth) メカニズムのサポート。

* [!DNL MongoDB]バージョン4.2および4.4のサポート。

* 香港、マカオ、台湾に関連する名前の出現は、中国のロケールと地域の新しい命名規則に従って更新されます。

* [!DNL Experience Manager] [[!DNL Assets]](#assets-accessibility-6590)と[[!DNL Dynamic Media]](#accessibility-dm-6590)のアクセシビリティの強化。

* スマートイメージングDPR（デバイスピクセル比）とネットワーク帯域幅の最適化により、最高品質の画像を効率的に配信できます。（高解像度のディスプレイとネットワーク帯域幅の制限があるデバイス） 詳細とタイムラインについては、[スマートイメージングのFAQ](/help/assets/imaging-faq.md)を参照してください。

* [!DNL Dynamic Media] 配信(URL修`fmt` 飾子)は、次世代の画像形式AVIF（AV1画像形式）をサポートします。詳しくは、 [画像サービングとレンダリングAPI fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html)を参照してください。

* [!UICONTROL タスクの割り当て]ワークフローステップを使用して、グループに通知電子メールを送信する機能。

* ソースのインタラクティブ通信を変更した後に、インタラクティブ通信の下書きを取得する機能。

* [!DNL Experience Manager Forms]でreCAPTCHAサービスの読み込み、レンダリングおよび検証用のカスタムドメイン名を設定します。

* [!UICONTROL 「フォームデータモデルサービスを起動」]ワークフローステップの入力データの強化。

* [!DNL Experience Manager Forms]内のレコードのドキュメントテンプレートで複数のマスターページを使用できます。

* [!DNL Experience Manager Forms]のレコードのドキュメントで改ページをサポートします。

* 組み込み型のリポジトリ(Apache Jackrabbit Oak)が1.22.7に更新されました。

[!DNL Experience Manager] 6.5.9.0で導入された機能と機能強化の完全なリストについては、 [!DNL Adobe Experience Manager] 6.5サービスパック9](new-features-latest-service-pack.md)の新機能を参照してください。[

>[!NOTE]
>
>Service Pack 9以降、[!DNL Experience Manager]のお客様は、Java™ SEに準拠した標準規格に準拠したOpenJDKの[!DNL Azul Zulu]ビルドの配布を使用して、[!DNL Experience Manager]アプリケーションを開発および操作できます。
>[!DNL Azul Zulu] JDKのサポートは、[!DNL Experience Manager]のお客様へのAdobeによっても提供されます。
>[!DNL Azul Zulu] JDKの関連バージョンは、[Adobeソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)からダウンロードできます。
>oracleJava™テクノロジーの使用権は、Adobe別に配布され、2022年12月末までに期限が切れます。 [!DNL Experience Manager] のお客様は、この日までに最新のJDKの使用を計 [!DNL Azul Zulu] 画し、実装することをお勧めします。[!DNL Oracle Java™]テクノロジーと[!DNL Azul Zulu]テクノロジーの使用方法について詳しくは、関連する[FAQ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf?lang=en)を参照してください。

[!DNL Experience Manager] 6.5.9.0リリースで提供された修正の一覧を以下に示します。

### [!DNL Sites] {#sites-6590}

* 認証要件プロパティが有効な公開済みページがログインページにリダイレクトされず、404エラーメッセージが返される(NPR-36354)。

* ハイパーリンクを作成する際に、リンクを検索するオプションがテキストコンポーネントで機能しない(NPR-35849)。

* `com.day.cq.wcm.commons.ReferenceSearch` APIを使用してトラバーサルクエリがトリガーされます。 [!DNL Experience Manager]サーバーのパフォーマンスに影響を与えます(NPR-36407)。

* 別のサイズ変更されたレイアウトコンテナ内にネストされたレイアウトコンテナが子コンポーネントの列数を正しく表示しないため、これらのコンポーネントがグリッドに揃えられない(NPR-36359)。

* 外部リンクチェッカーは、有効な外部リンクを無効なリンクとして表示する(NPR-36289)。

* しばらくの間、参照パネルがエラーメッセージを表示し始める(NPR-36167)。

* コンポーネントを移動する際、自動的に作成されたparsysに`sling:resourceType`ノードがない(NPR-36165)。

* （ロールアウト設定[!UICONTROL Blueprintのアクティベーションで有効化]と[!UICONTROL ブループリントのアクティベーションで無効化]を使用して）ライブコピーを同期しようとすると、同期が失敗し、`NullPointerException`がログに記録されます(NPR-36127)。

* ユーザーがタグ（システムに存在しないタグ）の即席テキストを入力し、Enterキーを押すと、そのタグがフィールドの下に表示されますが、コンテンツフラグメントを保存して再び開くと、即席タグが消えます(NPR-36132)。

* インボックスに、非同期操作のステータスを表示するオプションがない(NPR-36104)。

* 継承を復元した後に、重複コンポーネントが作成される(NPR-36000)。

* `RemoteContentRenderingService`を使用する場合、`RemoteContentRendererRequestHandler.getRequest`へのリクエストには常に`ComponentExporter`のルートページが含まれますが、トラバーサルの深さとフィルタリングオプションセットに基づくルートモデルに含まれない場合は、要求されたページは含まれません。 SPAが応答をレンダリングするのに十分な情報を持つように、要求には常に要求されたページを含める必要がある(NPR-35961)。

* onTime/offTime項目が、期待されたonTime/offTimeでアクティブ化/非アクティブ化されない(NPR-35936)。

* `cq:lastModified`プロパティを持たないエクスペリエンスフラグメントを含むページを公開すると、`NullPointerException`が発生する(NPR-35914)。

* コンテナ内のコンポーネントのサイズを変更しようとすると、元のサイズに戻すことはできません。 コンポーネントのコンテナのサイズを小さくすると、元のサイズに戻すことはできない(NPR-35809)。

* エディターで、またはライブコピーの概要からトリガーされるロールアウトダイアログで、分離されたページ、休止されたページ、または作成されていないページのステータスアイコンが正しく表示されない(NPR-35691)。

* マスターの「ロールアウトページを無視する」および「サブページを無視する」チェックボックスのページプロパティに対するマルチサイトマネージャーのロールアウト(NPR-35634)。

* クラシックUIで使用可能な復元ツリー機能がタッチUIにない(CQ-4315352、CQ-4309415)。

* 継承を元に戻し、[!DNL Experience Manager Sites]ページのページをロールアウトする際の問題(NPR-36033)。

### [!DNL Assets] {#assets-6590}

[!DNL Assets]では、次のユーザーエクスペリエンスの強化がおこなわれました。

* [!UICONTROL 作成]、[!UICONTROL 変更]、[!UICONTROL 名前]のいずれかのパラメーターに基づいて並べ替えられていないアセットを表示するには、[!DNL Adobe Experience Manager]「[!UICONTROL 並べ替え]」オプション内に「[!UICONTROL なし]」オプションを用意します。 「[!UICONTROL なし]」オプションを選択すると、Assetsユーザーインターフェイス（カード、列およびインサイト表示）のアセットがJCRノードに存在するのと同じ順序になります(NPR-36356)。

* [!DNL Adobe Experience Manager]からのACP API応答で電子メールIDを小文字にするために、オプションの設定が導入されました。を使用します。 [!DNL Adobe Asset Link][!DNL Adobe Asset Link]パネルは、[!DNL Adobe Experience Manager]からACP API応答を使用します(CQ-4317704)。

[!DNL Adobe Experience Manager] 6.5.9.0では、次のアクセシビリ [!DNL Assets] ティの強化がおこなわれています。

以下のテキストとアイコンのコントラスト（背景と共に）が改善され、視覚や色の知覚が限られているユーザーが理解できるようになりました。

* [!UICONTROL プロパティ]ページのアセットタイトル(NPR-35967)。
* 様々な場所の[!UICONTROL Rating]セクションの星評価アイコン(NPR-36009)。
* アセットおよびフォルダーのカード表示のテキスト。(NPR-35966)
* [!UICONTROL タイムライン]ビューのプレースホルダーテキスト(NPR-35965)。
* アセット検索結果のアセット名(NPR-35964)。
* [!UICONTROL リンク共有]ダイアログのプレースホルダーテキスト(NPR-35963)。
* [!UICONTROL 設定を表示ダイアログの「リスト」オプショ]ンのメタデー [!UICONTROL タ]  、  ステータス [!UICONTROL 、その他] のテキスト(NPR-35910)。
*  グローバル検 [!UICONTROL 索で、] 場所と入力して検索プレースホルダーテキストを検索します(NPR-35909)。
* [!UICONTROL コンテンツツリー](NPR-35908)の下のアイコンを展開および折りたたみます。
* アセットフォルダーが表示されるページの[!UICONTROL アセット]テキスト(NPR-35905)。
* アセットの詳細ページの[!UICONTROL 概要]オプション内の[!UICONTROL アセットメタデータ]、[!UICONTROL 使用状況統計]のテキスト(NPR-35904)。
* アセットの詳細ページの[!UICONTROL properties]および[!UICONTROL edit]オプションのショートカットキーのテキスト(NPR-35904)。

[!DNL Adobe Experience Manager] 6.5.9.0では、次 [!DNL Assets] の問題が修正されました。

* [!UICONTROL フォルダーメタデータスキーマ]フォームのタグ選択要素内から作成されたタグは保存されません(NPR-36119)。

* 小さな楕円を使用してアセットに注釈を付けると、楕円は印刷バージョンの注釈の数と重なります(NPR-36114)。

* 列表示で、重複アセットがアップロードされたときに、[!DNL Experience Manager]が重複アセットの競合を確認するメッセージを表示しない場合があります(NPR-36048)。

* リンクを共有ダイアログが開いていていて、変更が行われていない場合、閉じるボタンをクリックして閉じない(NPR-36030)。

* 複数のアセットを選択してプロパティを更新すると、エラーが発生したり、選択が解除されたアセットのプロパティが更新されたりする(NPR-36002)。

* アセットのアップロード時に、アセットファイル名の先頭または末尾に空白が追加され、残りの文字がリポジトリ内の既存のアセットの名前と同じ場合、エラーを記録せずに既存のアセットが置き換えられる(NPR-36001)。

* アセットの詳細ページでビデオが再生されると、再生および一時停止オプションが機能しない(NPR-35999)。

* アセットを一括して非公開にすると、Brand Portalが要求URIが長すぎることを示すエラーを生成する(NPR-35954)。

* 注釈テキストが長いアセットを印刷すると、スペースが使用可能な場合でも注釈テキストがトリミングされる(NPR-35948)。

* 「次のページに移動」オプションは、カタログを作成ページの「テンプレートを選択」ビューでページを選択すると無効になります(CQ-4315462)。

* ビデオアセットでアセットの更新ワークフローが開始されると、ページが繰り返し更新されます(CQ-4313375)。

* DAMフォルダーを削除または移動できず、例外がログに記録される(NPR-35942)。

### [!DNL Dynamic Media] {#dynamic-media-6590}

[!DNL Adobe Experience Manager] 6.5.9.0では、次のアクセ [!DNL Assets] シビリティ強化がおこなわれま [!DNL Dynamic Media]した。

* [!UICONTROL 画像セット]エディターのキーボードキーを使用してアセットを追加するダイアログを開くと、次のようになります。
   * スクリーンリーダーは、ダイアログが開いたことを読み上げる。
   * キーボードフォーカスは、ダイアログを開くとダイアログに移動する。
   * ダイアログが閉じると、キーボードフォーカスが「アセットを追加」オプションに戻る(CQ-4312134)。

* ホットスポットエディターのキーボードキーを使用して、アセットのホットスポットを追加および編集できるようになりました(CQ-4305965)。

* キーボードキーを使用して、ホットスポット管理を使用して、ホットスポットにハイパーリンクを配置できるようになりました。 スクリーンリーダーのフォーカスがフィールドに移動して、URLパスを編集し、「選択ダイアログを開く」オプションを選択できるようになりました(CQ-4290735)。

* 画像セットエディターページのテキストとコントロールのコントラスト（背景）が改善され、視覚や色の知覚が制限されたユーザーが理解できるようになりました(CQ-4290733)。

* ビューアプリセットエディターでアセット共有オプションに移動し、キーボードキーを使用して展開された共有オプションを折りたためることができるようになりました(CQ-4290724)。

* キーボードキーを使用して、ビデオエンコーディングを編集ページの「基本」タブと「詳細」タブの情報アイコンと警告アイコンのツールチップに移動して表示できるようになりました(CQ-4290722)。

* スクリーンリーダーで、ビューアプリセットエディターの「外観」タブと「ビヘイビアー」タブの様々なフィールドに関する説明を読み上げるようになりました(CQ-4290721)。

* フォームモードで画像プリセットを編集ページに移動すると、スクリーンリーダーは様々なフィールドおよびコントロールの目的と名前をナレーションします(CQ-4290717)。

* アセットの詳細ページを移動する際に、スクリーンリーダーでビューア内の様々なオプションの目的が説明されるようになりました(CQ-4290716)。

* プレースホルダーテキストの（背景と共に）コントラストを強化し、アセットの詳細ページの「レンディションのすべてのレンディション」オプションを改善し、視覚や色の知覚が制限されたユーザーが理解できるようにしました(CQ-4290713)。

* 必須フィールドを示す視覚的なアスタリスクが画像セットエディターのアセットの「タイトル」フィールドに表示され、スクリーンリーダーがそのフィールドに必要な情報を読み上げるようになりました(CQ-4290712)。

* スクリーンリーダーは、アセットの詳細ページで、ビューア内の様々なインタラクティブオプションの目的にアクセスし、説明できるようになりました(CQ-4290708)。

[!DNL Dynamic Media]の既知のビデオ再生の問題：

* 

   <!-- CQDOC-18116 -->You cannot play video renditions from the asset's Details page on Experience Manager - Dynamic Media running in hybrid mode.

* 

   <!-- CQDOC-18116 -->You cannot stream videos on Experience Manager - Dynamic Media running in hybrid mode.

Adobe Experience Manager 6.5.9.0 Assetsの[!DNL Dynamic Media]に関する次の問題が修正されました。

* [!DNL Dynamic Media]が選択的にアクティブ化され、[default](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html?lang=en#troubleshoot-dm-config)によって無効化されている場合、カスタムのビューアプリセットとCSSが[!DNL Dynamic Media]に複製されない(NPR-36232)。

* アセットの詳細ページでビデオレンディションをプレビューしようとすると、ビデオの読み込みが遅くなる(CQ-4320122)。

* 重複アセット検出が有効な200個を超えるアセットをアップロードすると、ブラウザーページが応答しなくなり、低速になります(CQ-4319633)。

* ページのパノラマメディアコンポーネントにパノラマ画像アセットを追加すると、キャッチできない参照エラーが記録されます(CQ-4317666)。

* エクスペリエンスフラグメントを使用してインタラクティブメディアビューアを実装する場合、パブリッシャーからエクスペリエンスフラグメントが開かれず、エラーが記録されます(CQ-4317655)。

* [!UICONTROL 「動的メディアに公] 開」オプションは、プロパテ [!UICONTROL ィペ] ージのクイック公  開オプションでは使用できません(CQ-4317199)。

* 読み取り専用権限を持つサイト作成者は、アセットに対してスマート切り抜き機能を使用し、スマート切り抜きレンディションを編集できます(CQ-4316450)。

* [!DNL Dynamic Media]設定が有効になっていないフォルダーパスに対しては、[!DNL Dynamic Media]モードで[!DNL Experience Manager]インスタンスが設定されている場合でも、ビデオ注釈は機能しません(CQ-4314950)。

* アセットのタイトルに2バイト、2バイト、高ASCII、キリル、サロゲートペア、ヘブライ語、アラビア語、GB18030文字が含まれる場合、Dynamic Mediaに公開すると、アセットのタイトルに疑問符(?)が付きます。 (CQ-4311872).

### プラットフォーム {#platform-6590}

* ブループリントのサムネールを生成し、ライブコピーに対する変更をロールアウトすると、一部のフィールドの継承が機能しなくなります(CQ-4319517)。

* フォルダーを作成する際に、「Orderable」プロパティを選択し、20個を超えるアセットをフォルダーに追加すると、そのフォルダー内のすべてのアセットを選択するとカウントが正しく表示されません(CQ-4316243)。

* ページを更新すると、フォルダーまたはアセットの並べ替えに適切な結果が表示されません(CQ-4316200)。

* Handlebars JavaScriptライブラリがv4.7.7にアップグレードされました(NPR-36375)。

* パッケージマネージャー(NPR-35949)を使用して新しいコードパッケージをインストールしても、カスタムバンドルが更新されない。

* `resourceresolver` Slingバンドルが原因で`Sling:alias`クエリが失敗する(NPR-35335)。

* Experience ManagerでSSLを設定すると、コンテキストパスが削除される(NPR-35294)。

* 長時間実行セッションの後に`SegmentNotFound`例外が返される(NPR-36405)。

### 統合 {#integrations-6590}

* Cloud Servicesエクスペリエンスフラグメントの継承が有効なページプロパティを保存できない。(NPR-36107)

* IMSユーザーインターフェイスのページネーションと遅延読み込みが適切な結果を表示しない(NPR-36046)。

* A4T Target設定を作成し、レポートソースに[!DNL Adobe Analytics]を選択した場合、ドロップダウンリストにAdobe Target対応のレポートスイートが表示されません(NPR-36006)。

### プロジェクト {#projects-6590}

* プロジェクトパスに追加された余分なスラッシュ(`/`)が原因でプロジェクトへのJCRパスが解決されないので、プロジェクトのプロパティを保存できない。(NPR-36191)

### スクリーン {#screens-6590}

* [!DNL Experience Manager Screens] カスタムの2要素認証ハンドラーが使用されている場合、プレーヤーは認証できない(NPR-35854)。

### コマース {#commerce-6590}

* [!UICONTROL コマースカタログ]ウィザードで、列表示で40個を超える項目を読み込めません(CQ-4318379)。

### 翻訳プロジェクト {#translation-6590}

* `es`を`es_es`ページに再変換する際に、更新または上書きのオプションが表示されない(NPR-36170)。

* 人間による翻訳を含むプロジェクトに対して「自動承認」オプションが選択されている場合、ジョブステータスは`Unknown`と表示されます(NPR-35981)。

* ページを翻訳する際、[!DNL Experience Fragments]の参照パスは、宛先の[!DNL Experience Fragment]参照パスに更新されません(NPR-35911)。

* 親ページと子ページに変更を加え、翻訳用に親ページを送信すると、子ページも誤って翻訳される(NPR-35896)。

* 選択したページに対して同時翻訳プロジェクトが複数ある場合、「[!UICONTROL プロジェクトに移動]」オプションが最新の翻訳プロジェクトにリンクされない(NPR-35454)。

* [!DNL Dynamic Media]にアセットを公開すると、[!DNL Experience Manager]に非公開のタグに対して誤ったメッセージが表示されます(CQ-4315914、CQ-4315913)。

* 削除されたジョブを開くと、[!DNL Experience Manager]に誤ったメッセージが表示されます(CQ-4315910)。

### ワークフロー {#workflow-6590}

* インボックスで使用可能な項目に対して「完了」、「委任」、「開く」の各アクションをクリックした場合、これらのアクションを完了するための視覚的な手がかりはありません(NPR-36317)。

### [!DNL Communities] {#communities-6590}

* スパムフィルタリングでは、システムがJava™ヒープ領域の100%を消費し、Experience Managerサーバーが応答しなくなる(NPR-36316、NPR-36493)。
* フォーラムで、`SearchCommentSocialComponentListProvider`からのJCRセッションデータが漏れ出している(NPR-36235)。
* 特定のインボックスメッセージを開くと、不適切なページネーションおよびその他の問題が発生したすべてのメッセージが反映される(NPR-35917)。

### [!DNL Brand Portal] {#brandportal-6590}

* [!DNL Brand Portal]を使用して[!DNL Experience Manager Assets]を設定すると、アセットソーシング機能フラグが自動的に有効になる(NPR-36010)。

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] サービスパックリリース日の 1 週間後にアドオンパッケージをリリースします。
>* OSGiデプロイメント上の[!DNL Experience Manager Forms]用の[!DNL Azul Zulu]ビルドの[!DNL OpenJDK]を使用して、アプリケーションを開発および操作できるようになりました。


**アダプティブフォーム**

* 複数の翻訳辞書を生成する際の[!DNL Experience Manager Forms] 6.5.7.0での言語初期化の問題(NPR-36439)。
* アダプティブフォームフラグメントに添付ファイルを追加してフォームを送信すると、[!DNL Experience Manager Forms]は次のエラーメッセージを表示します(NPR-36195)。

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* 人間による翻訳を使用して辞書を更新し、アダプティブフォームをプレビューすると、変更が表示されない(NPR-36035)。

**インタラクティブコミュニケーション**

* インタラクティブ通信の印刷チャネルを使用して画像をアップロードし、編集すると、画像が表示されなくなる(NPR-36518)。

* テキストアセットを編集してプレースホルダーを入力すると、すべてのインタラクティブ要素がナビゲーションペインから削除される(NPR-35991)。

**ワークフロー**

* JBoss®上の[!DNL Experience Manager Forms]サービスのRESTエンドポイントを呼び出すと、[!DNL Experience Manager]に次のエラーメッセージが表示されます(NPR-36305)。

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**BackendIntegration**

* 読み取りサービスの引数をダッシュを含むリテラル値にバインド中にフォームデータモデルを保存できない(NPR-36366)。

**Document Security**

* GlobalSignに対して証明書とHSMを設定すると、 [!DNL Experience Manager Forms]は、LTVにタイムスタンプを追加する際に、`Unsuported Algorithm`および`Invalid TSA Certificate`エラーメッセージを表示します(NPR-36026、NPR-36025)。

**ドキュメントサービス**

* [!DNL Experience Manager Forms]と統合するための[!DNL Gibson]ライブラリの更新(NPR-36211)。

**Foundation JEE**

* AdminUIで「エンドポイント管理」を選択すると、 [!DNL Experience Manager Forms]に`endpoint registry failure`エラーメッセージが表示されます(CQ-4320249)。

セキュリティ更新について詳しくは、[[!DNL Experience Manager] セキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)を参照してください。

## 6.5.9.0 のインストール {#install}

**設定要件と詳細情報**

* Experience Manager6.5.9.0にはExperience Manager6.5が必要です。詳細な手順については、[アップグレードのドキュメント](/help/sites-deploying/upgrade.md)を参照してください。
* サービスパックのダウンロードは、Adobe[「Software Distribution」](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)で入手できます。
* MongoDBおよび複数のインスタンスを使用したデプロイメントで、パッケージマネージャーを使用して、いずれかのオーサーインスタンスにExperience Manager6.5.9.0をインストールします。

>[!NOTE]
>
>Adobeは、[!DNL Adobe Experience Manager] 6.5.9.0パッケージの削除またはアンインストールはお勧めしません。

### サービスパックのインストール {#install-service-pack}

[!DNL Adobe Experience Manager] 6.5インスタンスにService Packをインストールするには、次の手順に従います。

1. インスタンスが更新モードの場合（以前のバージョンから更新された場合）は、インストール前にインスタンスを再起動します。 Adobeでは、インスタンスの現在の稼動時間が長い場合に再起動を推奨します。

1. インストールする前に、[!DNL Experience Manager]インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip)からサービスパックをダウンロードします。

1. パッケージマネージャーを開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

1. S3コネクタを更新するには、Service Packのインストール後にインスタンスを停止し、既存のコネクタをinstallフォルダーに用意されている新しいバイナリファイルで置き換えて、インスタンスを再起動します。 [Amazon S3データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャーUIのダイアログが終了することがあります。 Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデータバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認します。 通常、[!DNL Safari]ではこのような処理が行われますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.9.0を作業インスタンスに自動的にインストールする方法は2つあります。

A.サーバーがオンラインで使用可能になったら、 `../crx-quickstart/install`フォルダーにパッケージを配置します。 パッケージが自動的にインストールされます。

B.パッケージマネージャーの[HTTP APIを使用します。](/help/sites-administering/package-manager.md#package-share) `cmd=install&recursive=true`を使用して、ネストされたパッケージをインストールします。

>[!NOTE]
>
>Adobe Experience Manager 6.5.9.0では、Bootstrapのインストールはサポートされていません。

**インストールの検証**

1. 製品情報ページ(`/system/console/productinfo`)に、[!UICONTROL インストール済みの製品]の下に、更新されたバージョン文字列`Adobe Experience Manager (6.5.9.0)`が表示されます。

1. OSGiコンソール内のOSGiバンドルは、すべて&#x200B;**[!UICONTROL ACTIVE]**&#x200B;または&#x200B;**[!UICONTROL FRAGMENT]**&#x200B;です(Webコンソールを使用：`/system/console/bundles`)です。

1. OSGiバンドル`org.apache.jackrabbit.oak-core`は、バージョン1.22.3以降です(Webコンソールを使用：`/system/console/bundles`)です。

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

### Adobe Experience Manager Formsアドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Formsを使用していない場合はスキップします。 Experience ManagerFormsの修正は、スケジュールされた[!DNL Experience Manager] Service Packリリースの1週間後に、別のアドオンパッケージを通じて配信されます。

1. Adobe Experience Manager Service Packがインストールされていることを確認します。
1. [AEM Forms リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. [AEM Formsアドオンパッケージのインストール](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)の説明に従って、Formsアドオンパッケージをインストールします。

>[!NOTE]
>
>Experience Manager6.5.9.0には、[AEM Forms互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases)の新しいバージョンが含まれています。 古いバージョンのAEM Forms互換性パッケージを使用し、Experience Manager6.5.9.0に更新する場合は、Formsアドオンパッケージのインストール後に、最新バージョンのパッケージをインストールします。

### JEEへのAdobe Experience Manager Formsのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE上のAdobe Experience Manager Formsの修正は、別のインストーラーを使用して提供されます。

JEE上のFormsExperience Manager用の累積インストーラーのインストールとデプロイ後の設定について詳しくは、[リリースノート](jee-patch-installer-65.md)を参照してください。

>[!NOTE]
>
>JEE上のFormsExperience Manager用の累積インストーラーをインストールしたら、最新のFormsアドオンパッケージをインストールし、`crx-repository\install`フォルダーからFormsアドオンパッケージを削除して、サーバーを再起動します。

### UberJar {#uber-jar}

Experience Manager6.5.9.0用のUberJarは、[Maven Centralリポジトリ](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.9-1.0/)で入手できます。

MavenプロジェクトでUberJarを使用するには、[UberJar](/help/sites-developing/ht-projects-maven.md)の使用方法を参照し、プロジェクトPOMに次の依存関係を含めます。

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.9-1.0</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJarおよびその他の関連アーティファクトは、AdobeのパブリックMavenリポジトリ(`repo.adobe.com`)ではなく、Maven Centralリポジトリで使用できます。 メインのUberJarファイルの名前が`uber-jar-<version>.jar`に変更されます。 したがって、`dependency`タグには`apis`を値とする`classifier`はありません。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

[!DNL Experience Manager] 6.5.7.0で非推奨とマークされた機能の一覧を以下に示します。機能は、最初に廃止され、後で将来のリリースで削除されます。 別のオプションが提供されます。

機能または機能をデプロイメントで使用するかどうかを確認します。 また、別のオプションを使用するように実装を変更することを計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | **[!UICONTROL AEMクラウドサービスのオプトイン]**&#x200B;画面は非推奨（廃止予定）となりました。 Experience Manager6.5でExperience ManagerとAdobe Targetの統合が更新され、AdobeIMSと[!DNL Adobe I/O]を介した認証を使用するAdobe Target Standard APIがサポートされるようになり、分析とパーソナライゼーション用のExperience Managerページを実装するためのAdobeLaunchの役割が増加しています。 | 各[!DNL Experience Manager]クラウドサービスを使用して、システム接続、AdobeIMS認証、および[!DNL Adobe I/O]統合を設定します。 |
| コネクタ | Experience Manager6.5では、Microsoft® SharePoint 2010およびMicrosoft® SharePoint 2013用のAdobeJCR Connectorが非推奨（廃止予定）となりました。 | 該当なし |

## 既知の問題 {#known-issues}

* [!DNL Experience Manager]インスタンスを6.5から6.5.9.0バージョンにアップグレードする場合は、`error.log`ファイルで`RRD4JReporter`例外を表示できます。 インスタンスを再起動して問題を解決します。

* [!DNL Experience Manager] 6.5 Service Pack 5または以前のService Packを[!DNL Experience Manager] 6.5にインストールすると、（`/var/workflow/models/dam`で作成された）アセットカスタムワークフローモデルのランタイムコピーが削除されます。
ランタイムコピーを取得するには、HTTP APIを使用して、カスタムワークフローモデルのデザイン時コピーをそのランタイムコピーと同期することをお勧めします。
   `<designModelPath>/jcr:content.generate.json`

* 階層内のフォルダーの名前が[!DNL Assets]で変更され、アセットを含むネストされたフォルダーが[!DNL Brand Portal]に公開された場合、ルートフォルダーが再公開されるまで、フォルダーのタイトルは[!DNL Brand Portal]で更新されません。

* アダプティブフォームで初めてフィールドの設定を選択した場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* Experience Manager6.5.x.xのインストール中に、次のエラーおよび警告メッセージが表示される場合があります。
   * 「Adobe Target統合がTarget Standard API（IMS認証）を使用してExperience Managerで設定されている場合、エクスペリエンスフラグメントをTargetに書き出すと、間違ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計関数が使用されると、アダプティブフォームのサーバー側検証が失敗します(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューすると、Dynamic Mediaのインタラクティブ画像のホットスポットが表示されない。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :登録変更が完了するのを待機中のタイムアウトが未登録です。

## OSGiバンドルとコンテンツパッケージが含まれています {#osgi-bundles-and-content-packages-included}

以下のテキストドキュメントは、[!DNL Experience Manager] 6.5.9.0に含まれるOSGiバンドルとコンテンツパッケージの一覧です。

* [Experience Manager6.5.9.0に含まれているOSGiバンドルの一覧](assets/6590_bundles.txt)

* [Experience Manager6.5.9.0に含まれているコンテンツパッケージの一覧](assets/6590_packages.txt)

## 制限付きWebサイト {#restricted-sites}

これらのWebサイトは、お客様のみが利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [Adobeカスタマーケアへの問い合わせ方法](https://experienceleague.adobe.com/docs/customer-one/using/home.html)を参照してください。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5リリースノート](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] 製品ページ](https://www.adobe.com/marketing/experience-manager.html)
* [[!DNL Experience Manager] 6.5ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
* [Adobe Priority 製品アップデート](https://www.adobe.com/subscription/priority-product-update.html)のサブスクリプションを購入する

