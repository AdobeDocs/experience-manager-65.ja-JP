---
title: '[!DNL Adobe Experience Manager] 6.5 以前のサービスパックリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 サービスパックのリリースノート'
contentOwner: AK
mini-toc-levels: 2
exl-id: aeed49a0-c7c2-44da-b0b8-ba9f6b6f7101
source-git-commit: 99d38dddbcd06fecb82c744d446b9cef981e0781
workflow-type: tm+mt
source-wordcount: '23168'
ht-degree: 13%

---

# 以前のサービスパックに含まれていたホットフィックスと機能パック {#hotfixes-and-feature-packs-included-in-previous-service-packs}

## [!DNL Adobe Experience Manager] 6.5.9.0 {#experience-manager-6590}

[!DNL Adobe Experience Manager] 6.5.9.0 には、2019 年 4 月の 6.5 リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善が含まれています。サービスパックは [!DNL Adobe Experience Manager] 6.5 にインストールされています。

[!DNL Adobe Experience Manager] 6.5.9.0 で導入された主な機能と機能強化は次のとおりです。

* [!DNL Experience Manager Sites] Dynamic Media Foundation コンポーネントで、レスポンシブな画像プリセットまたはスマート切り抜きを使用する際に、高解像度のデバイス向けの最適化のオン/オフを切り替えることができるようになりました。

* パフォーマンスを向上させるために、`hidden=false` 条件を JCR クエリから [!UICONTROL QueryBuilder] エバリュエーターに移動します。 変更後に非表示の述語が機能していることを確認するために、[!DNL Experience Manager] は非表示のフォルダーが表示されていないかどうかを確認します。

* [!DNL Experience Manager Sites] ページで削除されたページとツリーを復元する機能。

* 新しいユーザーがメーラー設定サービスの更新トークンを使用してアクセストークンを更新できるようになりました。

* [メール設定サービスの SMTP XOAUTH2](/help/sites-administering/notification.md#setting-up-oauth) メカニズムのサポート。

* [!DNL MongoDB] バージョン 4.2 および 4.4 のサポート。

* 香港、マカオ、台湾に関連する名前の発生件数は、中国のロケールと地域の新しい命名規則に従って更新されます。

* [!DNL Experience Manager] [[!DNL Assets]](#assets-accessibility-6590) および [[!DNL Dynamic Media]](#accessibility-dm-6590) のアクセシビリティの強化。

* スマートイメージング DPR(Device Pixel Ratio) とネットワーク帯域幅の最適化により、最高品質の画像を効率的に配信できます。（高解像度のディスプレイとネットワーク帯域幅の制限があるデバイス） 詳細とタイムラインについては、[ スマートイメージングの FAQ](/help/assets/imaging-faq.md) を参照してください。

* [!DNL Dynamic Media] 配信 (URL 修`fmt` 飾子 ) は、次世代の画像形式 AVIF（AV1 画像形式）をサポートします。詳しくは、[ 画像のサービングとレンダリング API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html) を参照してください。

* [!UICONTROL  タスクの割り当て ] ワークフローステップを使用して、通知電子メールをグループに送信できます。

* ソースのインタラクティブ通信を変更した後に、インタラクティブ通信の下書きを取得する機能。

* [!DNL Experience Manager Forms] で reCAPTCHA サービスの読み込み、レンダリングおよび検証のためのカスタムドメイン名を設定します。

* [!UICONTROL 「フォームデータモデルサービスを起動」] ワークフローステップの入力データの強化。

* [!DNL Experience Manager Forms] 内のレコードのドキュメントテンプレートで複数のマスターページを使用できます。

* [!DNL Experience Manager Forms] のレコードのドキュメントで改ページをサポートします。

* 組み込み型のリポジトリ (Apache Jackrabbit Oak) が1.22.7に更新されます。

[!DNL Experience Manager] 6.5.9.0 で導入された機能と機能強化の完全なリストについては、[ [!DNL Adobe Experience Manager] 6.5 Service Pack 9](new-features-latest-service-pack.md) の新機能を参照してください。

>[!NOTE]
>
>Service Pack 9 以降、[!DNL Experience Manager] のお客様は、Java™ SE に準拠した標準規格に準拠した OpenJDK の [!DNL Azul Zulu] ビルドの配布を使用して、[!DNL Experience Manager] アプリケーションを開発および操作できます。
>[!DNL Azul Zulu] JDK のサポートは、[!DNL Experience Manager] のお客様へのAdobeによっても提供されます。
>[!DNL Azul Zulu] JDK の関連バージョンは、[Adobeソフトウェア配布 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) からダウンロードできます。
>oracleJava™テクノロジーの使用権は、Adobe別に配布され、2022 年 12 月末までに期限が切れます。 [!DNL Experience Manager] のお客様は、この日までに最新の JDK の使用を計 [!DNL Azul Zulu] 画および実装することをお勧めします。[!DNL Oracle Java™] テクノロジーと [!DNL Azul Zulu] テクノロジーの使い方について詳しくは、関連する [FAQ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf) を参照してください。

[!DNL Experience Manager] 6.5.9.0 リリースで提供された修正の一覧を次に示します。

### [!DNL Sites] {#sites-6590}

* 認証要件プロパティが有効な公開済みページがログインページにリダイレクトされず、404 エラーメッセージが返される (NPR-36354)。

* ハイパーリンクを作成する際に、リンクを検索するオプションがテキストコンポーネントで機能しない (NPR-35849)。

* `com.day.cq.wcm.commons.ReferenceSearch` API を使用してトラバーサルクエリがトリガーされます。 [!DNL Experience Manager] サーバのパフォーマンスに影響を与える (NPR-36407)。

* 別のサイズ変更されたレイアウトコンテナ内にネストされたレイアウトコンテナが子コンポーネントの列数を正しく表示しないため、これらのコンポーネントがグリッドに揃えられない (NPR-36359)。

* 外部リンクチェックは、有効な外部リンクを無効なリンクとして表示する (NPR-36289)。

* しばらくの間、参照パネルがエラーメッセージを表示し始める (NPR-36167)。

* コンポーネントを移動する際に、自動的に作成された parsys に `sling:resourceType` ノードがない (NPR-36165)。

* （ロールアウト設定 [!UICONTROL Blueprint のアクティベーションでアクティブ化 ] と [!UICONTROL  ブループリントのアクティベーションで非アクティブ化 ] を使用して）ライブコピーの同期を試みると、同期が失敗し、`NullPointerException` がログに記録されます (NPR-36127)。

* ユーザーがタグ（システムに存在しないタグ）の即興テキストを入力し、Enter キーを押すと、そのタグがフィールドの下に表示されますが、コンテンツフラグメントが保存されて再び開くと、即興のタグが消えます (NPR-36132)。

* インボックスに、非同期操作のステータスを表示するオプションがない (NPR-36104)。

* 継承を復元した後に、重複コンポーネントが作成される (NPR-36000)。

* `RemoteContentRenderingService` を使用する場合、`RemoteContentRendererRequestHandler.getRequest` への要求には常に `ComponentExporter` のルートページが含まれますが、トラバーサルの深さとフィルタリングオプションセットに基づいてルートモデルに含まれていない場合は、要求されたページは含まれません。 応答をレンダリングするのに十分な情報をSPAが持つように、要求には常に要求されたページを含める必要がある (NPR-35961)。

* onTime/offTime 項目が、期待された onTime/offTime でアクティブ化/非アクティブ化されない (NPR-35936)。

* `cq:lastModified` プロパティを持たないエクスペリエンスフラグメントを含むページを公開すると、`NullPointerException` が発生する (NPR-35914)。

* コンテナ内のコンポーネントのサイズを変更しようとすると、元のサイズに戻すことはできません。 コンポーネントのコンテナのサイズを小さくすると、元のサイズに戻すことはできません (NPR-35809)。

* エディターまたはライブコピーの概要からトリガーされるロールアウトダイアログで、分離されたページ、休止されたページ、作成されていないページのステータスアイコンが正しく表示されない (NPR-35691)。

* マルチサイトマネージャーのロールアウト（マスターのページプロパティでロールアウトページとサブページを無視するチェックボックスをオンにする）(NPR-35634)。

* クラシック UI で使用可能な復元ツリー機能がタッチ UI に表示されません (CQ-4315352、CQ-4309415)。

* 継承を元に戻し、[!DNL Experience Manager Sites] ページをロールアウトする際の問題 (NPR-36033)。

### [!DNL Assets] {#assets-6590}

[!DNL Assets] では、次のユーザーエクスペリエンスの強化がおこなわれました。

* [!UICONTROL  作成 ]、[!UICONTROL  変更 ]、[!UICONTROL  名前 ] のいずれかのパラメーターに基づいて並べ替えられていないアセットを表示するには、[!DNL Adobe Experience Manager][!UICONTROL 「] で並べ替え」オプション内に [!UICONTROL 「なし」] オプションを用意します。 「[!UICONTROL  なし ]」オプションを選択すると、Assets ユーザーインターフェイス（カード、列およびインサイト表示）のアセットが JCR ノードに存在するのと同じ順序になります (NPR-36356)。

* [!DNL Adobe Experience Manager] からの ACP API 応答で電子メール ID を小文字にするために、オプションの設定が導入されました。を使用するのは、 [!DNL Adobe Asset Link] ユーザーの ID にすべての文字が小文字で含まれていない場合、アセットをチェックインできないからです。 [!DNL Adobe Asset Link] パネルは、[!DNL Adobe Experience Manager] からの ACP API 応答を使用します (CQ-4317704)。

[!DNL Assets] では、次のアクセシビリティの強化がサービスパック 9 の一部として利用できます。

以下のテキストとアイコンのコントラスト（背景付き）が改善され、視覚や色の知覚が限られたユーザーが理解できるようになりました。

* [!UICONTROL  プロパティ ] ページのアセットタイトル (NPR-35967)。
* 様々な場所の [!UICONTROL  評価 ] セクションの星評価アイコン (NPR-36009)。
* アセットおよびフォルダーのカード表示のテキスト。(NPR-35966)
* [!UICONTROL  タイムライン ] ビューのプレースホルダーテキスト (NPR-35965)。
* アセット検索結果のアセット名 (NPR-35964)。
* [!UICONTROL  リンク共有 ] ダイアログのプレースホルダーテキスト (NPR-35963)。
* [!UICONTROL 設定を表示ダイアログの「リス]ト」オプションのメタデー [!UICONTROL タ]、  ステータス  、その他  のテキスト (NPR-35910)。
*  グローバル検 [!UICONTROL 索で場所と] 入力して、プレースホルダーテキストを検索します (NPR-35909)。
* [!UICONTROL  コンテンツツリー ] の下のアイコンを展開および折りたたむ (NPR-35908)。
* アセットフォルダーが表示されるページの [!UICONTROL  アセット ] テキスト (NPR-35905)。
* アセットの詳細ページの [!UICONTROL  概要 ] オプション内の [!UICONTROL  アセットのメタデータ ]、[!UICONTROL  使用状況の統計 ] のテキスト (NPR-35904)。
* アセットの詳細ページの [!UICONTROL properties] および [!UICONTROL edit] オプションのショートカットキーのテキスト (NPR-35904)。

[!DNL Assets] では、次のバグ修正がサービスパック 9 の一部として利用できます。

* [!UICONTROL  フォルダーメタデータスキーマ ] フォームのタグ選択要素内で作成されたタグは保存されません (NPR-36119)。

* 小さな楕円を使用してアセットに注釈を付けると、楕円は印刷バージョンの注釈の数と重なります (NPR-36114)。

* 列表示では、重複アセットがアップロードされたときに、[!DNL Experience Manager] が重複アセットの競合を確認するメッセージを表示しない場合があります (NPR-36048)。

* リンクを共有ダイアログが開いていていて、変更が行われていない場合、閉じるボタンをクリックして閉じない (NPR-36030)。

* 複数のアセットを選択してプロパティを更新すると、エラーが発生したり、選択解除されたアセットのプロパティが更新されたりする (NPR-36002)。

* アセットのアップロード時に、アセットファイル名の先頭または末尾に空白が追加され、残りの文字がリポジトリ内の既存のアセットの名前と同じ場合、既存のアセットはエラーを記録せずに置き換えられる (NPR-36001)。

* アセットの詳細ページでビデオが再生されると、再生および一時停止オプションが機能しない (NPR-35999)。

* アセットを一括して非公開にすると、要求 URI が長すぎることを示すエラーがBrand Portalによって生成される (NPR-35954)。

* 注釈テキストが長いアセットを印刷すると、スペースが使用可能な場合でも注釈テキストがトリミングされる (NPR-35948)。

* 「次のページに移動」オプションは、カタログを作成ページの「テンプレートを選択」ビューでページを選択すると無効になります (CQ-4315462)。

* ビデオアセットでアセットの更新ワークフローが開始されると、ページが繰り返し更新されます (CQ-4313375)。

* DAM フォルダーを削除または移動できず、例外がログに記録される (NPR-35942)。

### [!DNL Dynamic Media] {#dynamic-media-6590}

[!DNL Adobe Experience Manager] 6.5.9.0 では、[!DNL Dynamic Media] で次のアクセシビリティの強化が利用できます。

* [!UICONTROL  画像セット ] エディターのキーボードキーを使用してアセットを追加するダイアログを開くと、次のようになります。
   * スクリーンリーダーは、ダイアログが開いたことを読み上げます。
   * キーボードフォーカスは、開くとダイアログに移動する。
   * ダイアログを閉じると、キーボードフォーカスが「アセットを追加」オプションに戻る (CQ-4312134)。

* ホットスポットエディターのキーボードキーを使用して、アセットのホットスポットを追加および編集できるようになりました (CQ-4305965)。

* キーボードキーを使用して、ホットスポット管理を使用して、ホットスポットにハイパーリンクを配置できるようになりました。 スクリーンリーダーのフォーカスがフィールドに移動して、URL パスを編集し、「選択ダイアログを開く」オプションに移動するようになりました (CQ-4290735)。

* 画像セットエディターページのテキストとコントロールのコントラスト（背景付き）が改善され、視覚や色の知覚が制限されたユーザーが理解できるようになりました (CQ-4290733)。

* ビューアプリセットエディターでアセット共有オプションに移動し、キーボードキーを使用して展開された共有オプションを折りたたむことができるようになりました (CQ-4290724)。

* キーボードキーを使用して、ビデオエンコーディングを編集ページの「基本」タブと「詳細」タブの情報アイコンと警告アイコンのツールチップに移動して表示できるようになりました (CQ-4290722)。

* スクリーンリーダーで、ビューアプリセットエディターの「外観」タブと「動作」タブの様々なフィールドに関する説明を読み上げるようになりました (CQ-4290721)。

* フォームモードで画像プリセットを編集ページに移動する際に、スクリーンリーダーは、様々なフィールドおよびコントロールの目的と名前をナレーションします (CQ-4290717)。

* アセットの詳細ページを移動する際に、スクリーンリーダーでビューア内の様々なオプションの目的が説明されるようになりました (CQ-4290716)。

* プレースホルダーテキストの（背景と共に）コントラスト ( アセットの詳細ページの「レンディションのすべてのレンディション」オプションが改善され、視覚や色の知覚が限られたユーザーが理解できるようになりました (CQ-4290713)。

* 必須フィールドを示す視覚的なアスタリスクが画像セットエディターのアセットの「タイトル」フィールドに表示され、スクリーンリーダーがそのフィールドに必要な情報を読み上げるようになりました (CQ-4290712)。

* スクリーンリーダーは、アセットの詳細ページで、ビューア内の様々なインタラクティブオプションの目的にアクセスし、ナレーションできるようになりました (CQ-4290708)。

Adobe Experience Manager 6.5.9.0 Assets の修正 [!DNL Dynamic Media] の次の問題：

* [default](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html#troubleshoot-dm-config) によって [!DNL Dynamic Media] が選択的にアクティベートされ無効になっている場合、カスタムのビューアプリセットと CSS が [!DNL Dynamic Media] に複製されない (NPR-36232)。

* アセットの詳細ページでビデオレンディションをプレビューしようとすると、ビデオの読み込みが遅くなる (CQ-4320122)。

* 重複アセット検出が有効な 200 個を超えるアセットをアップロードすると、ブラウザーページが応答しなくなり、低速になります (CQ-4319633)。

* パノラマ画像アセットをページのパノラマメディアコンポーネントに追加すると、キャッチできない参照エラーが記録されます (CQ-4317666)。

* エクスペリエンスフラグメントを使用してインタラクティブメディアビューアを実装する場合、エクスペリエンスフラグメントはパブリッシャーから開かれず、エラーが記録されます (CQ-4317655)。

* [!UICONTROL 「動的メディアに公] 開」オプションは、プロパテ [!UICONTROL ィページ] のクイック公  開オプションでは使用できません (CQ-4317199)。

* 読み取り専用の権限を持つサイト作成者は、アセットに対してスマート切り抜き機能を使用し、スマート切り抜きレンディションを編集できます (CQ-4316450)。

* [!DNL Dynamic Media] 設定が有効になっていないフォルダーパスに対しては、[!DNL Dynamic Media] モードで [!DNL Experience Manager] インスタンスが設定されている場合でも、ビデオ注釈は機能しません (CQ-4314950)。

* アセットのタイトルに 2 バイト、2 バイト、高 ASCII、キリル、サロゲートペア、ヘブライ語、アラビア語、GB18030文字が含まれている場合、Dynamic Mediaに公開すると、アセットのタイトルに疑問符 (?) が付きます。 (CQ-4311872).

>Dynamic Media *Experience Manager6.5.9.0 のみ* の既知のビデオ再生の問題：
>
>* 

   <!-- CQDOC-18116 -->You cannot play video renditions from the asset's Details page on Experience Manager - Dynamic Media running in hybrid mode.
>* 

   <!-- CQDOC-18116 -->You cannot stream videos on Experience Manager - Dynamic Media running in hybrid mode.


### Platform {#platform-6590}

* ブループリントのサムネールを生成し、ライブコピーに対する変更をロールアウトする場合、一部のフィールドの継承は機能しません (CQ-4319517)。

* フォルダーを作成する際に、「Orderable」プロパティを選択し、20 個を超えるアセットをフォルダーに追加すると、そのフォルダー内のすべてのアセットを選択した場合、カウントが正しく表示されません (CQ-4316243)。

* ページを更新すると、フォルダーまたはアセットの並べ替えに適切な結果が表示されません (CQ-4316200)。

* Handlebars JavaScript ライブラリが v4.7.7 にアップグレードされました (NPR-36375)。

* パッケージマネージャー (NPR-35949) を使用して新しいコードパッケージをインストールしても、カスタムバンドルが更新されない。

* `resourceresolver` Sling バンドルが原因で `Sling:alias` クエリが失敗する (NPR-35335)。

* Experience Manager(NPR-35294) で SSL を設定すると、コンテキストパスが削除される。

* 長時間実行されたセッションの後に `SegmentNotFound` 例外が返される (NPR-36405)。

### 統合 {#integrations-6590}

* Cloud Servicesエクスペリエンスフラグメントの継承が有効なページプロパティを保存できない。(NPR-36107)

* IMS ユーザーインターフェイスのページネーションと遅延読み込みで適切な結果が表示されない (NPR-36046)。

* A4T Target 設定を作成し、レポートソースに [!DNL Adobe Analytics] を選択した場合、ドロップダウンリストでAdobe Target対応のレポートスイートは使用できません (NPR-36006)。

### プロジェクト {#projects-6590}

* プロジェクトの JCR パスが、プロジェクトパスに追加された余分なスラッシュ (`/`) によって解決されないので、プロジェクトのプロパティを保存できません。(NPR-36191)

### スクリーン {#screens-6590}

* [!DNL Experience Manager Screens] カスタムの 2 要素認証ハンドラーが使用されている場合、プレーヤーは認証できない (NPR-35854)。

### Commerce {#commerce-6590}

* [!UICONTROL  コマースカタログ ] ウィザードで、列表示で 40 個を超える項目を読み込めませんでした (CQ-4318379)。

### 翻訳プロジェクト {#translation-6590}

* `es` を `es_es` ページに再変換する際に、更新または上書きのオプションが表示されない (NPR-36170)。

* 人間による翻訳を含むプロジェクトに対して自動承認オプションが選択されると、ジョブのステータスが `Unknown` と表示されます (NPR-35981)。

* ページを翻訳する際に、[!DNL Experience Fragments] の参照パスが宛先の [!DNL Experience Fragment] 参照パスに更新されない (NPR-35911)。

* 親ページと子ページに変更を加え、翻訳のために親ページを送信すると、子ページも誤って翻訳されます (NPR-35896)。

* 選択したページに対して同時翻訳プロジェクトが複数ある場合、「[!UICONTROL  プロジェクトに移動 ]」オプションが最新の翻訳プロジェクトにリンクされない (NPR-35454)。

* [!DNL Dynamic Media] にアセットを公開すると、[!DNL Experience Manager] に非公開のタグに間違ったメッセージが表示されます (CQ-4315914、CQ-4315913)。

* 削除されたジョブを開くと、[!DNL Experience Manager] に誤ったメッセージが表示されます (CQ-4315910)。

### ワークフロー {#workflow-6590}

* [ 完了 ]、[ 委任 ]、または [ 開く ] をクリックして、インボックスで使用可能な項目に対して [ 操作の完了 ] をクリックした場合、これらの操作を完了する視覚的な手がかりはありません (NPR-36317)。

### [!DNL Communities] {#communities-6590}

* スパムフィルタリングでは、システムが Java™ヒープ領域の 100%を消費し、Experience Managerサーバーが応答しなくなる (NPR-36316、NPR-36493)。
* フォーラムで、`SearchCommentSocialComponentListProvider` からの JCR セッションデータが漏洩している (NPR-36235)。
* 特定のインボックスメッセージを開くと、不適切なページネーションおよびその他の問題が発生するすべてのメッセージが反映される (NPR-35917)。

### [!DNL Brand Portal] {#brandportal-6590}

* [!DNL Brand Portal] を使用して [!DNL Experience Manager Assets] を設定すると、アセットソーシング機能フラグが自動的に有効になる (NPR-36010)。

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] サービスパックリリース日の 1 週間後にアドオンパッケージをリリースします。


**アダプティブフォーム**

* 複数の翻訳辞書を生成する際の [!DNL Experience Manager Forms] 6.5.7.0 での言語初期化の問題 (NPR-36439)。
* アダプティブフォームフラグメントに添付ファイルを追加してフォームを送信すると、[!DNL Experience Manager Forms] は次のエラーメッセージを表示します (NPR-36195)。

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* 人間による翻訳を使用して辞書を更新し、アダプティブフォームをプレビューすると、変更内容が表示されない (NPR-36035)。

**インタラクティブコミュニケーション**

* インタラクティブ通信の印刷チャネルを使用して画像をアップロードし、編集すると、画像が表示されなくなる (NPR-36518)。

* テキストアセットを編集してプレースホルダーを入力すると、すべてのインタラクティブ要素がナビゲーションペインから削除される (NPR-35991)。

**ワークフロー**

* JBoss®で [!DNL Experience Manager Forms] サービスの REST エンドポイントを呼び出すと、[!DNL Experience Manager] に次のエラーメッセージが表示されます (NPR-36305)。

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**BackendIntegration**

* 読み取りサービスの引数をダッシュを含むリテラル値にバインド中に、フォームデータモデルを保存できない。(NPR-36366)

**Document Security**

* GlobalSign に対して証明書と HSM を設定すると、 [!DNL Experience Manager Forms] は、LTV にタイムスタンプを追加する際に、 `Unsuported Algorithm` と `Invalid TSA Certificate` のエラーメッセージを表示します (NPR-36026、NPR-36025)。

**ドキュメントサービス**

* [!DNL Experience Manager Forms] との統合のために [!DNL Gibson] ライブラリを更新しました (NPR-36211)。

**Foundation JEE**

* AdminUI で「エンドポイント管理」を選択すると、 [!DNL Experience Manager Forms] に `endpoint registry failure` エラーメッセージが表示されます (CQ-4320249)。

セキュリティ更新の詳細については、[[!DNL Experience Manager]  セキュリティ速報ページ ](https://helpx.adobe.com/security/products/experience-manager.html) を参照してください。

### Experience Manager6.5.9.0 の既知の問題 {#known-issues-6590}

* [!DNL Experience Manager] インスタンスを 6.5 から 6.5.10.0バージョンにアップグレードする場合は、`error.log` ファイルで `RRD4JReporter` 例外を表示できます。 この問題を解決するには、インスタンスを再起動します。

* [!DNL Experience Manager] 6.5 Service Pack 5 または以前の Service Pack 5 を [!DNL Experience Manager] 6.5 にインストールした場合、（`/var/workflow/models/dam` で作成された）アセットのカスタムワークフローモデルのランタイムコピーが削除されます。
ランタイムコピーを取得するには、HTTP API を使用して、カスタムワークフローモデルのデザイン時コピーをそのランタイムコピーと同期することをお勧めします。
   `<designModelPath>/jcr:content.generate.json`。

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。 ただし、[!DNL Brand Portal] では、ルートフォルダーが再公開されるまで、フォルダーのタイトルは更新されません。

* アダプティブフォームで初めてフィールドの設定を選択した場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* Experience Manager6.5.x.x のインストール中に、次のエラーと警告メッセージが表示される場合があります。
   * 「Adobe Target統合が Target Standard API（IMS 認証）を使用してExperience Managerで設定されている場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用されると、アダプティブフォームのサーバー側検証が失敗します (CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューすると、Dynamic Mediaのインタラクティブ画像のホットスポットが表示されない。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :登録変更が完了するのを待機中のタイムアウト。

## [!DNL Adobe Experience Manager] 6.5.8.0 {#experience-manager-6580}

[!DNL Adobe Experience Manager] 6.5.8.0 には、2019 年 4 月の 6.5 リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善が含まれています。サービスパックは [!DNL Adobe Experience Manager] 6.5 にインストールされています。

[!DNL Adobe Experience Manager] 6.5.8.0 で導入された主な機能と機能強化は次のとおりです。

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* [Connected Assets 機能 ](/help/assets/use-assets-across-connected-assets-instances.md) を使用する場合、そのアセットを使用するすべての [!DNL Sites] ページのリストを表示できるようになりました。 アセットへのこれらの参照は、アセットの [!UICONTROL  プロパティ ] ページで使用できます。 これにより、管理者、マーケターおよびライブラリ担当者は、アセットの使用状況を完全に把握でき、トラッキング、管理、ブランドの一貫性を向上できます。

* Web ページで参照されているアセットを削除すると、[!DNL Experience Manager] [ に警告 ](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references) が表示されます。 参照元のアセットを強制的に削除するか、アセットの [!DNL Properties] ページに表示される参照を確認して変更することができます。 参照をクリックすると、ローカルページとリモートページが開きます。 [!DNL Sites]

* [!UICONTROL  名前 ]、[!UICONTROL  最終変更日、] および [!UICONTROL  最終ロールアウト日 ] のプロパティを使用して、ロールアウトに使用できるライブコピーページを並べ替えます。

* 組み込み型のリポジトリ (Apache Jackrabbit Oak) が1.22.6に更新されました。 <!-- TBD: Mention the version -->

[!DNL Experience Manager] 6.5.8.0 で導入された機能と機能強化の完全なリストについては、[ [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md) の新機能を参照してください。

[!DNL Experience Manager] 6.5.8.0 リリースで提供された修正の一覧を次に示します。

### [!DNL Sites] {#sites-6580}

* ページがブループリントに移動されても、リンク先は更新されない (NPR-35724)。
* Tizen ベースのプレーヤーが、特定のブラウザーで認証に失敗する場合があります。 この問題は、samesite=none 属性をサポートしないブラウザーで発生します (NPR-35589)。
* ロックが解除されたレスポンシブコンテナに許可されているコンポーネントが表示されない (NPR-35565)。
* 新しく追加されたページのライブコピーを作成すると、言語マスターは各ドメインに対して 2 つのコピーを作成します (NPR-35545)。
* `org.apache.felix.scr.impl.ComponentRegistry` タイマーが原因で多数のスレッドがブロックされた場合、SCR コンポーネントレジストリのデッドロック。 その結果、[!DNL Experience Manager] は無限に応答を停止します (GRANITE-33125,FELIX-6252)。
* サイドレールで特定のアセットを検索すると、結果には、検索されなかった一部のアセットが含まれます (NPR-35524)。
* あるExperience Managerインスタンスに対して SSL を有効にすると、コンテキストパスが削除される (NPR-35477)。
* リストを作成し、最初の要素にテキストを追加し、2 番目の要素にテーブルを追加し、テーブル内にリストを追加すると、親リストがゆがむ (NPR-35465)。
* 連続するリスト項目で異なるプラグインを使用すると、リスト項目に <br> タグが追加される (NPR-35464)。
* リストが 2 つの段落の間に配置されている場合、リストにテーブルを追加できない (NPR-35356)。
* AEMインスタンスをAEM 6.3 からAEM 6.5 にアップグレードすると、アップグレードインスタンスの起動に時間がかかります (NPR-35323)。
* 角括弧 () を含むAEMアセットを複製する場合。 この名前では、レプリケーションが失敗します (GRANITE-27004、NPR-35315)。
* 見出しをリッチテキストエディターに追加すると、段落ボタンが無効になる (NPR-35256)。
* 既存のリストに項目を追加すると、後続の折りたたみ可能なリストまたはトグルリストが削除されます (NPR-35206)。
* 「ページをロールアウト」オプションを選択すると、使用可能なすべてのライブコピーを含むダイアログボックスが表示され、自動ロールアウトが実行されます。 ページのライブコピーは、ユーザーの操作を行わずにすべての地域にロールアウトされます (NPR-35138)。
* 「子を含める」オプションを使用する場合、「公開を管理」オプションですべてのページがリストされるわけではありません。 22 ページのみが表示される (NPR-35086)。
* ポリシーが編集されると、テキストコンポーネントはポリシーの変更を保持しない (NPR-35070)。
* 番号付きリストの一部の項目をインデントする場合、すべての項目は同じ番号を保持しますが、同じインデントを持つ項目に対しては、1 から始める番号を付ける必要があります (CQ-4313011)。
* 縮小化を有効にすると、どのページやコンポーネントも編集できなくなります。 問題は、AEM 6.5 Service Pack 7 のインストール後に発生しました (CQ-4311133)。
* オムニサーチおよびアセットフィルターが、無関係な結果または結果を返す (CQ-4312322、NPR-35793)。
* 複数のページがクライアントライブラリに同時にアクセスする場合、HTMLライブラリマネージャーはクライアントライブラリの読み込みに失敗します。 これにより、ページの誤ったレンダリングが発生する (NPR-35538)。
* [!DNL Experience Manager] で SSL を設定すると、コンテキストパスが自動的に削除されます (NPR-35294)。
* パッケージマネージャーがログアウトオプションをクリックした後、ユーザーをログアウトしない (NPR-35160)。

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0 では、次の問 [!DNL Assets] 題が修正され、次の機能強化がおこなわれました。

* 以前のバージョンのアセットを復元すると、OSGi コンソールで DamEvent.Type RESTORED イベントがトリガーされません (NPR-35789)。
* `IndexWriter.merge` スマー `OutOfMemoryError` トタグ機能が大きなとインデックスを `/oak:index/lucene` 作成す `/oak:index/ntBaseLucene` るので、エラーが発生する。(NPR-35651)
* マルチバイト文字を含む [!UICONTROL  アセットの投稿 ] タイプのフォルダーを名前に保存しようとすると、エラーメッセージが表示される (NPR-35605)。
* カスケードメタデータサブタイプフィールドを使用すると、誤った「このフィールドに入力してください」エラーが発生する (NPR-35643)。
* 既存のアセットを [!DNL Assets] ユーザーインターフェイスにドラッグして新しいバージョンを作成した場合、メタデータの変更は永続的ではありません (NPR-34940)。
* カスケードメニュー用のルールをメタデータスキーマエディタで作成する場合、「[!UICONTROL  依存オン ]」オプションは同じ名前を繰り返す (NPR-35596)。
* [!UICONTROL  アセット管理者の検索レール ] を編集した後、類似性検索が機能しない (NPR-35588)。
* フォルダー内で、左側のレールの「[!UICONTROL  フィルター ]」をクリックしてアセット検索を開くと、[!UICONTROL  ステータス ]/[!UICONTROL  チェックアウト ]/[!UICONTROL  チェックアウト ] が機能しません (NPR-35530)。
* アセットのすべてのスマートタグを削除して変更を保存しようとしても、タグは削除されません。 ただし、ユーザーインターフェイスは、変更が保存されたことを示す (NPR-35519)。
* 順序指定可能なフォルダーのリスト表示で、アセットの並べ替えや並べ替えができない。(NPR-35516)
* デフォルトのメタデータスキーマを編集すると、アセットの [!UICONTROL  プロパティ ] ページのタグフィールドがテキストフィールドに変わります。 この変更により、ユーザーがオンデマンドタグを追加することを認識できなくなり、タグがリポジトリに文字列として保存される (NPR-35478)。
* アセットをダウンロードする際に、有効な電子メールアドレスが指定されていない名前を指定した場合、ダウンロードオプションは使用できません。 ただし、ダウンロードダイアログの別のオプションが選択されている場合、このボタンは有効になるが、電子メールは送信されない (NPR-35365)。
* ユーザーは、[!DNL Adobe InDesign] でアセットを編集した後、アセットをチェックインできず、権限の不足に関するエラーを受け取る (NPR-35341)。
* Handlebars JavaScript ライブラリが v4.7.6 にアップグレードされました (NPR-35333)。
* 一括メタデータ編集を開始し、単一の項目が選択されるまで項目の選択を解除すると、メタデータエディターインターフェイスが期待どおりに動作しなくなる (NPR-35144)。
* `assets.html` ページ内からクリックしても、グローバルナビゲーションで正しいコンソールが開かない (CQ-4312311)。
* [!DNL Assets] は、RGBレンディションを持つRGBのアセットレンディションを表示しません (CQ-4310190)。
* メニューの [!UICONTROL  関連付け ] オプションが [!UICONTROL  プロパティ ] ページに正しく表示されません (CQ-4310188)。
* アセットの検索やスマートコレクションの作成に、ドキュメントのファイルタイプフィルターを使用した場合、コレクションへのアクセス時にフィルターは適用されません。 代わりに、すべてのタイプのアセットが検索に表示されます (NPR-35759)。
* [!DNL Assets] ユーザーインターフェイスから Lightbox にアセットをドラッグして追加することはできません (NPR-35901)。
* 名前の競合を解決した後に既存のアセットの新しいバージョンが作成されると、元のアセットのメタデータが上書きされます (CQ-4313594)。
* 検索フィルターまたは述語を使用してアセット検索をフィルタリングする場合は、アセットを開いて表示または編集し、検索結果ページに戻ると、フィルターは機能しません。 検索されたすべてのアセットが、フィルタリングされずに表示される (NPR-35913)。

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* RESS 画像プリセットの「 URL 」オプションは、アセットの詳細ページで有効になっています。 動的レンディションセクションで RESS 画像プリセットが選択されている場合、アセットの詳細ページで URL と RESS の両方のオプションを使用できるようになりました。 （CQ-4311241）
* インタラクティブメディアコンポーネント — 選択的公開設定で [!DNL Experience Manager] を持つユーザーがいる場合、インタラクティブビデオは機能しません (CQ-4311054)。
* フォルダー間でアセットを移動する場合、API を介した [!DNL Experience Manager] と [!DNL Dynamic Media–Scene7] の同期は非常に遅くなります (CQ-4310001)。
* オムニサーチを使用すると、ログのサイズが大幅に増加します (CQ-4309153)。
* 選択的同期が有効で、アセットが同期フォルダーにコピー（移動なし）されると、期待どおりに同期されません (CQ-4307122)。
* DM に自動公開されるアップロード済みアセットの場合、ステータスに「AEMで公開済み」と表示されません。 また、「Dynamic Mediaの公開ステータス」列に正しい公開ステータスが表示されません (CQ-4306415)。
* アセットが [!DNL Experience Manager] で公開され、アクティベーション時に [!DNL Dynamic Media] に公開するように設定されている場合、 `scene7FileStatus` メタデータの値は期待どおりに更新されません (CQ-4308269)。
* ビデオプロファイルの編集時に、[!DNL Experience Manager] にはビデオプリセットに設定された高さとビットレートの値が表示されません。 フィールドは空白で表示されます (CQ-4311828)。

### [!DNL Commerce] {#commerce-6580}

* コマースのすべての製品のカスタムタグを作成できない (CQ-4310682)。

* 製品アセットの参照の更新により、ProductAssetListener スレッドが JCR へのコミットを完了するまで、レプリケーションスレッドが待機状態になる (NPR-35269)。

### Platform {#platform-6580}

* タブのない Coral タブ表示コンポーネントを使用し、基盤バリデーターをトリガーすると、次のエラーが発生します (NPR-35636)。

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* 名前にコンマが含まれるノードの SCD 転送レプリケーションが、削除イベントで失敗する (NPR-35191)。

* AEM 6.5.7 にアップグレードすると、ビルドが失敗し始めます。 理由は、古いバージョンが uber-jar に埋め込まれているか、jackson-core がないからです (GRANITE-33006)。

### ユーザーインターフェイス {#ui-6580}

* アセットコンソールで、フォルダー内のドキュメントのカード表示からリスト表示に切り替えると、並べ替えが適切に機能しない (NPR-35842)。

* テキストコンポーネント内のテキストをハイパーリンクすると、検索機能に適切な結果が表示されない (NPR-35849)。

* 値が必須とマークされた非表示フィールドに指定されていない場合、コンポーネントの保存がブロックされます (NPR-35219)。

### 統合 {#integrations-6580}

* IMS テナント ID と Target クライアントコードに異なる値を使用すると、 [!DNL Experience Manager] と [!DNL Adobe Target] の統合に失敗します (NPR-35342)。

### 翻訳プロジェクト {#translation-6580}

* [!DNL Experience Manager] で翻訳ジョブを書き出すまたは読み込む際の問題 (NPR-35259)。

### Campaign {#campaign-6580}

* タッチ UI で標準のテンプレートを使用してキャンペーンページを作成し、ページのプロパティダイアログの「 E メール」タブを開くと、件名および本文フィールドのパーソナライゼーション変数が無効のままになります (CQ-4312388)。

### [!DNL Communities] {#communities-6580}

* ページ構造をコミュニティグループに追加すると、パンくずリストの [!UICONTROL Group] タイトルが、最初の [!UICONTROL Page] のタイトルに変更されます (NPR-35803)。
* モデレーターとは異なり、標準コミュニティメンバーはドラフト投稿にアクセスして編集できません (NPR-35339)。
* `DSRPReindexServlet` によるアクセス制御とサービス拒否が壊れ、インデックス作成が完了するまでコミュニティサイトが停止します (NPR-35591)。
*  を [!UICONTROL  管理者 ] フィールドから削除しても、実際にはバックエンドからは削除されません (NPR-35592、NPR-35611)。
* [!UICONTROL  メッセージを作成 ] コンポーネントは、入力したテキストが部分一致の場合、結果を返しません (NPR-35666)。

* **[!UICONTROL タグを追加]** を選択して新しいブログにタグを追加しようとすると、パフォーマンスに影響が出たり遅くなったりする場合があります。 パフォーマンスを向上させるには、[cqTagLucene-0.0.1.zip hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip) をインストールします。

### [!DNL Brand Portal] {#brandportal-6580}

* [!UICONTROL  アセット投稿 ] タイプのフォルダーにメンバーを追加すると、ユーザーインターフェイスに「[!UICONTROL  ユーザーまたはグループを追加 ]」と表示されます。ただし、Brand Portalのアクティブなユーザーのみがサポートされ、グループはサポートされません。(NPR-35332)

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] サービスパックリリース日の 1 週間後にアドオンパッケージをリリースします。

**アダプティブフォーム**

* 繰り返し可能な行を持つ表を、アダプティブフォーム内に複数のインスタンスを持つ繰り返し可能なパネルに挿入すると、その表は常にパネルの最初のインスタンスに追加される。(NPR-35635)

* アダプティブフォームでタブフォーカスが CAPTCHA コンポーネントを 1 回正常に検証した後に再度 CAPTCHA コンポーネントに到達すると、[!DNL Experience Manager Forms] に `Provide Captcha phrase to proceed` エラーメッセージが表示される (NPR-35539)。

**インタラクティブコミュニケーション**

* 翻訳済みのフォームを送信すると、送信メッセージは英語で表示され、適切な言語に翻訳されません (NPR-35808)。

* 添付された XDP またはドキュメントフラグメントに非表示の条件を含めると、インタラクティブ通信の読み込みに失敗する (NPR-35745)。

**Correspondence Management**

* レターを編集する際、条件を持つモジュールの読み込みに時間がかかる (NPR-35325)。

* 左側のナビゲーションパネルから、レターに含まれていないアセットを選択し、次のアセットを選択した場合、青いハイライトは、以前に選択したアセットから削除されません (NPR-35851)。

* レター内のテキストフィールドを編集すると、[!DNL Experience Manager Forms] に `Text Edit Failed` エラーメッセージが表示されます (CQ-4313770)。

**ワークフロー**

* iOSの [!DNL Experience Manager Forms] モバイルアプリケーションでアダプティブフォームを開こうとすると、アプリケーションは応答を停止します (CQ-4314825)。

* HTMLワークスペースの [!UICONTROL To-do] タブにHTML文字が表示される (NPR-35298)。

**XMLFM**

* Output Service を使用して XML ドキュメントを生成する場合、一部の XML ファイルに対して `OutputServiceException` エラーが発生します (CQ-4311341、CQ-4313893)。

* 箇条書きの最初の文字に上付き文字プロパティを適用すると、箇条書きのサイズが小さくなります (CQ-4306476)。

* Output Service を使用して生成されたPDF formsには、境界線が含まれません (CQ-4312564)。

**デザイナー**

* [!DNL Experience Manager Forms] Designer で XDP ファイルを開くと、designer.log ファイルが XDP ファイルと同じフォルダーに生成されます (CQ-4309427、CQ-4310865)。

**HTML5 のフォーム**

* [!DNL iOS 14.1 or 14.2] に対して [!DNL Safari] Web ブラウザーでアダプティブフォームのチェックボックスをオンにすると、追加のフィールドが表示されない (NPR-35652)。

**Forms Management**

* XDP ファイルの CRX リポジトリへの一括アップロードが正常に完了したことを示す確認メッセージが表示されない (NPR-35546)。

**Document Security**

* AdminUI の [!UICONTROL  ポリシー ] を編集オプションに関して複数の問題が報告された (NPR-35747)。

### Experience Manager6.5.8.0 の既知の問題 {#known-issues-6580}

* [!DNL Experience Manager] インスタンスを 6.5 から 6.5.8.0 バージョンにアップグレードする場合は、`error.log` ファイルで `RRD4JReporter` 例外を表示できます。 インスタンスを再起動して問題を解決します。

* [!DNL Experience Manager] 6.5 Service Pack 5 または以前の Service Pack 5 を [!DNL Experience Manager] 6.5 にインストールした場合、（`/var/workflow/models/dam` で作成された）アセットのカスタムワークフローモデルのランタイムコピーが削除されます。
ランタイムコピーを取得するには、HTTP API を使用して、カスタムワークフローモデルのデザイン時コピーをそのランタイムコピーと同期することをお勧めします。
   `<designModelPath>/jcr:content.generate.json`。

* [!UICONTROL  ルールの定義 ] ダイアログを使用して、[!UICONTROL AdobeメタデータスキーマFormsエディター ] と [!UICONTROL  メタデータスキーマFormsエディター ] でカスケードルールを編集および作成する際に問題が発生した場合は、フォルダーカスタマーサポートにお問い合わせください。 作成および保存済みのルールは、期待どおりに動作しています。

* 階層内のフォルダーの名前が [!DNL Experience Manager Assets] に変更され、アセットを含むネストされたフォルダーが [!DNL Brand Portal] に公開された場合、そのフォルダーのタイトルは、ルートフォルダーが再び公開されるまで [!DNL Brand Portal] で更新されません。

* アダプティブフォームで初めてフィールドの設定を選択した場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* [!UICONTROL Connected assets configuration] ウィザードがインストール後に 404 エラーメッセージを返した場合は、パッケージマネージャーを使用して `cq-remotedam-client-ui-content` パッケージと `cq-remotedam-client-ui-components` パッケージを手動で再インストールします。

* Experience Manager6.5.x.x のインストール中に、次のエラーと警告メッセージが表示される場合があります。
   * 「Adobe Target統合が Target Standard API（IMS 認証）を使用してExperience Managerで設定されている場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用されると、アダプティブフォームのサーバー側検証が失敗します (CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューすると、Dynamic Mediaのインタラクティブ画像のホットスポットが表示されない。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :登録変更が完了するのを待機中のタイムアウト。

## [!DNL Adobe Experience Manager] 6.5.7.0 {#experience-manager-6570}

[!DNL Adobe Experience Manager] 6.5.7.0 は、2019 年 4 月の 6.5 リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善を含む重要なアップデートです。サービスパックは [!DNL Adobe Experience Manager] 6.5 にインストールされています。

[!DNL Adobe Experience Manager] 6.5.7.0 で導入された主な機能と機能強化には、以下が含まれます。

* ページの移動および MSM ロールアウトを非同期操作として実行すると、実行時のパフォーマンスに与える影響を軽減できます。

* ユーザーは、カード表示と列表示でデジタルアセットを並べ替えることができます。

* [!DNL Assets] およびで [!DNL Dynamic Media] は、複数のアクセシビリティ強化をおこないます。この機能強化は、キーボードナビゲーション、スクリーンリーダーの使用、類似の支援テクノロジー (AT) の使用に関連しています。 [[!DNL Assets] enhancements](#assets-6570) および [[!DNL Dynamic Media] enhancements](#dynamic-media-6570) を参照してください。

* [フォームデータモデルの HTTP クライアント](../../help/forms/using/configure-data-sources.md#fdm-http-client-configuration) 設定を使用して、パフォーマンスを最適化します。

* [レイアウトモードで各コンポーネントのリセ](../../help/forms/using/resize-using-layout-mode.md#resize-components) ットオプションを使用できる

* [!DNL Experience Manager] 6.5 Service Pack 7 Formsにより、次の点でパフォーマンスが向上しました。

   * アダプティブフォームを送信する際に、サーバー上でフィールド値を検証する。

   * [!DNL Automated Forms Conversion service] を使用してPDFフォームをアダプティブフォームに変換する。

* [!DNL Experience Manager Forms] での [!DNL Microsoft SQL Server] 2019 のサポート。

* [!DNL Microsoft] SQL Server 2016 OSGi デプロイメントの高可用性のための常時稼動可用性グループのサポート。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.22.5 に更新しました。

[!DNL Experience Manager] 6.5.7.0 で導入された機能と機能強化の完全なリストについては、[ [!DNL Adobe Experience Manager] 6.5 Service Pack 7 の新機能 ](new-features-latest-service-pack.md) を参照してください。

[!DNL Experience Manager] 6.5.7.0 リリースで提供された修正の一覧を次に示します。

### [!DNL Sites] {#sites-6570}

* ページの [!UICONTROL  タイムラップ ] オプションを開き、「タイムライン」サイドレールオプションを開いたまま、[!UICONTROL  サイト ] コンソールに移動すると、`Failed to Load` エラーが発生します (NPR-34951)。

* [!UICONTROL  タイムラップ ] オプションは、選択した日付と時間範囲の画像を表示しない (NPR-34951)。

* フィルターがコンテンツフラグメントを含むページから `getHeader()` を呼び出すと、`java.lang.AbstractMethodError` エラーが発生します (NPR-34942)。

* ページのパスに複数のコンテンツサブ文字列が含まれている場合、プレビューがレンダリングに失敗し、バージョン比較関数も失敗する (NPR-34740)。

* コンポーネントの `String` タイプラベルプロパティに数値を設定すると、コンポーネントを削除して、削除操作を取り消すことができます。 ただし、削除を取り消した後、ラベルプロパティが `String` から `Long` に変更されます (NPR-34739)。

* 次の例外は、ロックされたレイアウトを持つテンプレートをページに基づいてエクスペリエンスフラグメントを追加する際に発生します (NPR-34632)。

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.apache.sling.api.SlingException: Cannot get DefaultSlingScript: org.mozilla.javascript.EcmaError: TypeError: Cannot call method "getChildren" of null
   ```

* フォルダーを移動すると、トラバーサルの問題が発生し、次のエラーが発生する (NPR-34554)。

   ```TXT
   org.apache.sling.api.SlingException: Cannot get DefaultSlingScript. org.apache.jackrabbit.oak.query.RuntimeNodeTraversalException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped
   ```

* 新しいアセットを作成、公開、新しい場所に移動すると、`Request to complete move operation` ワークフローが作成され、「中止」状態になります。 新しいアセットをアップロードし、`move` 操作を実行すると、保留状態の `Request to complete move operation` ワークフローが作成される。(NPR-34543)

* エクスペリエンスフラグメントを [!DNL Experience Manager] 6.5.2 環境から [!DNL Target] Standard に書き出すと、Workspace プロパティが [!DNL Target] Standard(NPR-34557) で使用できないので、API 呼び出しが失敗します。

* [!UICONTROL 「] を公開」オプションが表示されなくなるので、[!UICONTROL 「公開を管理」] オプションを使用してページを公開できません (NPR-34542)。

* テキストにスタイルを追加すると、`<div>` タグがテキストに追加され、そのスタイルをテキストに適用できなくなる (NPR-34531)。

* ポップアップメニューで項目を選択して必要なファイルを更新した場合、他のメニューの必須フィールドが空のため、ダイアログ値の保存は許可されない (NPR-34529)。

* カスタムテンプレートからページを作成してブループリント階層内に移動すると、そのページから先に削除されたコンポーネントがライブコピー階層内のページに表示され始める (NPR-34527)。

* 記事のスタイルがコンテンツに適用されると、そのコンテンツを削除できなくなる (NPR-34486)。

* エクスペリエンスフラグメントのすべてのライブコピーとコピーが、同じ [!DNL Adobe Target] オファー ID を指している (NPR-34469)。

* 箇条書きリスト項目は、番号付きリストに加えて表示されます (NPR-34455)。

* 「ソースと比較」オプションで、ソースページとページの編集バージョンの違いが表示されない (NPR-34285)。

* ページを削除すると、バージョン管理の詳細は設定できなくなります (NPR-34159)。

* ユーザーが「[!UICONTROL  選択範囲を開く ]」ダイアログオプションを選択すると、キーボードフォーカスがページにある非表示のコントロールに移動します (CQ-4307779、CQ-4293601)。

* オーサー環境で公開済みのフォルダーを移動しても、パブリッシュインスタンス上のフォルダーのパスはそれに応じて更新されません (CQ-4305144)。

* ユーザーが「[!UICONTROL  すべてを選択 ]」オプションで `Enter` キーを選択した場合、キーボードフォーカスは「[!UICONTROL  コントロールを作成 ]」オプションに移動しません (CQ-4293599)。

* `Esc` キーを選択した場合、フォーカスは親コントロールに復元されません (CQ-4293593、CQ-4293590)。

* [!DNL Sites] UI およびコアコンポーネントの WCAG 準拠を改善しました (CQ-4293448)。

*  このペ  ージでは Zoom および Scale 関数 [!DNL Sites Editor] が無効になっています (CQ-4282353)。

* 「右に回転」オプションを使用すると、スクリーンリーダーは現在の回転または反転状態のナレーションを停止します (CQ-4282128)。

* 「完了」および「設定をキャンセル」ダイアログボタンには、多数のタブストップがあります (CQ-4274601)。

* 同じレベルで同じ名前のページを移動することは許可されない (NPR-35041)。

* 「消去 (x) 」オプションを選択した後、キーボードフォーカスが [!UICONTROL  フィルター ] フィールドに移動しない (CQ-4293581)。

* [!DNL Experience Manager] 6.5.6.0 にアップグレードすると、継承された段落システムの動作が変更され、正しく動作しない (NPR-35117)。

* キーボードユーザーは、[!DNL AEM Sites] ページの [!UICONTROL  アクション ] セクションを選択した後、タブフォーカスを適切な順序に移動できない (CQ-4307786)。

* コンテンツフラグメントの編集時に、RTE ツールバーのリンクターゲットメニューリストでオプションを選択すると、コンテンツフラグメント作成者ダイアログがちらつき始めます (CQ-4305532)。

* キーボードユーザーは、下向き矢印キーを使用して [!UICONTROL  コンポーネントを追加 ] ドロップダウンリストのオプションを選択できない (CQ-4295097)。

* [!DNL Sites] ページの「[!UICONTROL  アセット ]」タブでカレンダーメニューから日付を選択しても、タブのフォーカスが適切な順序に移ることはありません (CQ-4293600)。

* サイトページの編集時に使用できる「リンク」オプションまたは「テキスト」オプションを削除した後も、キーボードユーザーの次のオプションまたは前のオプションにタブフォーカスが移動しない (CQ-4293597)。

* キーボードユーザーは、使用可能なオプションを表示して `Esc` キーを押した後で、[!UICONTROL  アクション ] セクションの「その他のオプション」にタブフォーカスを戻すことができない (CQ-4293592)。

* [!UICONTROL  編集 ] モードで画像の [!UICONTROL  回転 ] オプションを有効にすると、タブフォーカスが回転に留まらず、キーボードユーザーの [!UICONTROL  やり直し ] オプションに移動します (CQ-4293587)。

* 「[!UICONTROL  リンクとアクション ]」タブにある「[!UICONTROL  選択範囲を開く ]」ダイアログで、「[!UICONTROL  キャンセル ]」オプションの後に、タブフォーカスがページ内の非表示の要素に移動します (CQ-4293579)。

* キーボードユーザーが画像を編集する際に、[!UICONTROL 「完了」] オプションに移動し、Enter キーを押しても、スクリーンリーダーが完了を読み上げない (CQ-4282351)。

* [!UICONTROL  リンクおよびアクション ] ダイアログで使用できる「上へ移動」および「下へ移動」オプションは、スクリーンリーダーおよびキーボードユーザーは使用できません (CQ-4281120)。

* [!UICONTROL  プロパティ ] ページで「閉じる」(X) オプションに移動した後、キーボードユーザーがタブフォーカスを復元できない (CQ-4293581、NPR-34653)。

### [!DNL Assets] {#assets-6570}

[!DNL Adobe Experience Manager] 6.5.7.0 では、次の問 [!DNL Assets] 題が修正され、次の機能強化がおこなわれました。

* このリリースでは、[!DNL Experience Manager Assets] のアクセシビリティに関する次の機能強化がおこなわれています。詳しくは、[ [!DNL Assets]](/help/assets/accessibility.md) のアクセシビリティ機能を参照してください。

   * キーボードを使用してタイムラインを移動する場合、`Esc` キーは、「[!UICONTROL  すべて表示 ]」オプションを折りたたみ、フォーカスを失うことはありません (CQ-4293598)。
   * キーボードの Tab キーを使用してナビゲートする際、追加したタグから最後のタグを削除した後、タグフィールドにフォーカスが保持される (NPR-35109)。
   * [!DNL Experience Manager] コンポーネントに、スクリーンリーダーが使用する名前、役割、値に関する適切な情報が含まれるようになりました (NPR-34255)。
   * 「種類/サイズ」コンボボックス、「リンク」コンボボックス、「言語」コンボボックス、または「テキスト」編集ボックスを削除すると、キーボードフォーカスが次または前のユーザーインターフェイス要素、またはより関連性の高いユーザーインターフェイス要素に戻ります (CQ-4293585)。
   * オプションの上にポインターを置くと、「選択」や「ダウンロード」などのヒントが表示されます。拡大鏡を使用している場合は、これらのヒントが原因でファイルのサムネールが表示されないことがあります。`Escape` キーを使用してオプションを削除した後に、フォーカスを保持できるようになりました。(CQ-4293554).
   * ページに表示されているグリッドからグリッドセルを選択すると、フォーカスが画面に表示されるアクションバーに移動します (CQ-4282127)。
   * [!DNL Experience Manager] ホームページ内のすべてのソリューションへのリンクに視覚的なヒント（下線と山形のアイコン）が表示されるので、ビジュアルユーザーは通常のテキストとリンクを区別できます (CQ-4282072)。

* 次のユーザーエクスペリエンスの強化は、[!DNL Assets] でおこなわれます。

   * カード表示と列表示でのアセットの並べ替えを有効にする (NPR-35097)。

* 6.5 にアップグレードした後、Assets HTTP API を使用して JSON ファイルが生成された場合、ファイルで使用されているエンコーディングに問題があります (NPR-35129)。

* コレクションを作成する権限が与えられていない（「コレクションを作成」オプションは使用できない）グループのユーザーは、URL `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/collections/createcollectionwizard.html/content/dam/collections?contentPath=/content/dam/collections` に直接アクセスしてコレクションを作成できます (NPR-35115)。

* 名前順に並べ替えられたアセットは、大文字と小文字が区別されて並べ替えられます。 これにより、検索結果で順番に表示される大文字と小文字に基づいて、2 つの異なる並べ替えリストが作成される (NPR-35068)。

* コンテンツフラグメントがエディターで開かれると、警告メッセージ (`Invalid value specified for a metadata property`) がエラーログに記録されます (NPR-35012)。

* 管理者権限を持たないユーザーは、[Experience Manager] デスクトップアプリケーションを使用して、期限切れアセットを編集できます。 (NPR-34993).

* 同じアセットを Assets ユーザーインターフェイスにドラッグして新しいバージョンを作成した場合、メタデータの変更が永続的におこなわれない (NPR-34940)。

* コレクションの編集時に、ユーザーはコレクションのタイトルを削除して、変更を正常に保存できる (NPR-34889)。

* 重複画像をアップロードすると、削除オプションが表示されます。 「削除」を選択すると、画像をアップロードできます。 DAM アセットの更新ワークフローもトリガーされます (NPR-34744)。

* [!DNL Adobe Asset Link] を [!DNL Adobe InDesign] と共に使用する場合、検索結果にはフォルダーやコレクションは含まれず、アセットのみが含まれます (NPR-34699、CQ-4303666)。

* カード表示にカーソルを合わせると、カードで使用可能なクイックアクションに（自動的に）フォーカスした結果、画面がスクロールする (NPR-34514)。

* 複数のアセットのプロパティを一括編集する際に、「[!UICONTROL  保存 ]」オプションを選択すると、Bulk Editor の表示が閉じて、メインの [!DNL Assets] ページにリダイレクトされます。 この動作は、[!UICONTROL 「保存して閉じる」] オプションの動作と同じで、予期しない動作です (NPR-34546)。

* 保存後、スマートコレクションに正しいユーザーインターフェイス設定が表示されません。 クエリは正しく保存されるが、インターフェイスには常に最後に追加されたオプションの述語が表示される (NPR-34539)。

* [!DNL Experience Manager] にアセットを追加すると、名前空間のないメタデータが読み込まれない (NPR-34530)。

* フォルダー上のアセットをドラッグして移動すると、ユーザーインターフェイスに「[!UICONTROL Lightbox にドロップ ]」および「[!UICONTROL  コレクションにドロップ ]」というオプションも表示されます。 移動操作がキャンセルされても、ユーザインターフェイスに後者の 2 つのオプションが引き続き表示される (NPR-34526)。

* シンボル `%>` がコレクションページに表示される (NPR-34499)。

* 列表示では、[!DNL Assets] は、すべてのアセットが表示される前に、上下にスクロールすると、重複するフォルダーおよびアセット名を表示します (NPR-34464)。

* 公開フォルダーを作成した直後にプライベートフォルダーを作成した場合、公開フォルダーはプライベートフォルダー設定を使用する (NPR-34415)。

* カード表示では、カードはアルファベット順に表示されず、カードはアルファベット順に並べ替えられない (NPR-34234)。

* カスケードルールを再度開いても、ユーザーインターフェイスで選択内容が維持されない (CQ-4301452)。

#### [!DNL Dynamic Media] {#dynamic-media-6570}

* [!DNL Dynamic Media] のアクセシビリティに関する次の機能強化がおこなわれました (CQ-4290306)。 詳しくは、 [!DNL Dynamic Media]](/help/assets/accessibility-dm.md) の [ アクセシビリティ機能を参照してください。

   * スクリーンリーダー（JAWS、ナレーター）は、「埋め込みサイズ」メニューオプションのメニュー項目の名前、役割、状態をナレーションします (CQ-4290927)。
   * ユーザーは、`Tab` キーを使用して E メールリンクダイアログを移動できます (CQ-4290926)。
   * ビデオエンコーディングプロファイルを作成するワークフローは、スクリーンリーダーの機能強化を考えると、より使いやすくなります (CQ-4290623、CQ-4290622)。
   * `Tab` キーを使用して移動する場合、フォーカスはワークフロー内の適切なユーザーインターフェイス要素に移動し、インタラクティブビデオを作成します (CQ-4290621、CQ-4290620、CQ-4290619)。
   * 公開、アセットを編集、スマート切り抜きを編集、画像セットエディターの各ページが、Web 標準に準拠するように改善されました。支援テクノロジー (AT) のユーザーが、これらのページを簡単に移動し、画像の切り抜きなどのアクションを実行できるようになりました (CQ-4290617、CQ-4290616、CQ-4290613、CQ-4290612、CQ-4290610、CQ-4290614)。
   * ビューアが改善され、ユーザーがキーボードを使用して移動できるようになりました (CQ-4290615)。
   * キーボードおよびスクリーンリーダーのユーザーは切り抜き機能を使用できます (CQ-4290609)。
   * キーボードユーザーは、ホットスポットをより適切に管理できます (CQ-4290604、CQ-4290603)。

* 会社名とフォルダー名が同じ場合、 [!DNL Experience Manager] でリモートイメージセットを編集できない (NPR-31340)。

* [!DNL Dynamic Media] 画像にホットスポットを追加した後、または [!DNL Dynamic Media] ビデオまたは [!DNL Experience Fragment] を画像付きで編集した後に、出力をプレビューしようとすると、z-index の順序が正しくありません (CQ-4307267)。

* [!DNL Dynamic Media] 混在メディアセットが再処理されると同期が失敗します (CQ-4307184)。

* [!DNL Dynamic Media] への自動同期が設定されているフォルダーにアセットが移動されると、そのアセットは同期されません (CQ-4307122)。

* [!DNL Dynamic Media] ビデオがネイティブのHTML5 ビデオコントロールでiOSデバイスで再生されない (CQ-4306977、CQ-4306727)。

* スマート切り抜きが適用されている画像をダウンロードできない (CQ-4304558)。

* フォルダーをDynamic Mediaに選択的に公開できない (CQ-4304526)。

* [!DNL Experience Manager] からビデオファイルを非公開にしても、設定済みのScene7デプロイメントからアダプティブビデオセットを非公開にしないでください (CQ-4304405)。

* パノラマメディアコンポーネントにパノラマ画像アセットを追加し、ページを更新すると `Uncaught ReferenceError: $ is not defined` エラーが発生します (CQ-4302810)。

* [!UICONTROL  ビューアプリセットエディター ] で、[!UICONTROL PanoramicImage/PanoramicImage_VR] プリセットを編集する際に、`PanoramicView` コンポーネントで `PANORAMICVIEW_AUTOROTATE` 修飾子のラベルを使用できません (CQ-4302443)。

* ビデオが MixedMediaSet の最初でない場合、ビデオキャプションは表示されません (CQ-4298161)。

* iPhone モバイルデバイスのHTML5 eCatalog ビューアで、ページをめくったりページをめくったりすることはできません (CQ-4296611)。

* モバイルデバイスでスウォッチをスクロールすると、スウォッチが表示領域の右と外に数秒間スクロールしてから、ビューに戻ります (CQ-4296439)。

* ビューアプリセットのマスターレコードを作成すると、CSS とアートワークは公開されず、ビューアプリセットのみが公開されます (CQ-4262205)。

* [!UICONTROL  インタラクティブビデオ/画像 ] コンポーネント内の特定のホットスポットのエクスペリエンスフラグメントをリンクしようとしても、選択したエクスペリエンスフラグメントのパスは表示されません。 代わりに、パスフィールドから空の値を返します (NPR-35146、CQ-4298136)。

* IVV エディターでエクスペリエンスフラグメントをプレビューできない (CQ-4308560)。

* ホットスポットを画像に追加してエクスペリエンスフラグメントを選択する場合、エクスペリエンスフラグメントのサブフォルダーとバリエーションを選択できません (CQ-4307455)。

* アップロード後に、画像以外のアセットが公開済みとして表示されない (CQ-4306415)。

#### [!DNL Experience Manager] 3D アセット {#three-d-assets-6570}

* `DAM CQ MIME Type` サービスによって、誤った MIME タイプが 3D アセットに適用され、誤ったレンダリングがおこなわれる (NPR-34731)。

### [!DNL Commerce] {#commerce-6570}

* コマース製品コレクションのユーザーインターフェイスで、1 つのコレクション内に 15 個を超える製品がリストされない (NPR-34502)。

### Platform {#platform-6570}

* HTTPS を介した HTTP セッションが無効化されない (NPR-35083)。
* ユーザーインターフェイスから日次または週次のメンテナンスタスクを開始すると、`NullPointerException` が返される。(NPR-34953)
* W3C バリデーターが、準拠しているクライアントライブラリ JavaScript ファイルに関する警告を報告する (NPR-34898)。
* `AudienceOmniSearchHandler` 関数は、廃止されたインデックスを使用します (NPR-34870)。
* Experience Managerからサインアウトしても、Cookie が消去されない (NPR-34743)。
* `TagManager` API の `findByTitle` 関数は、タグ名に特殊文字が含まれている場合には機能しません (NPR-34357)。
* ユーザー同期パッケージを読み込むプロセスが失敗する (NPR-34399)。
* `ariaLabel` および `ariaLabelledby` プロパティのサポートを `Coral.Masonry` コンポーネントに追加しました (GRANITE-29962)。
* 最新のコアコンポーネントパッケージをインストールした後、コンテンツフラグメントを含むページで Dispatcher キャッシュが更新されない (CQ-4306788)。
* ローカライズされたタグ名が引用符 (`"`) で囲まれていると、ユーザーインターフェイスに正しく表示されません (CQ-4305439)。

### ユーザーインターフェイス {#ui-6570}

* コンポーネントプロパティの [!UICONTROL 「] へのリンク」フィールドに、指定した文字列と一致しないオートコンプリート候補が表示されます (NPR-34865)。

* 2 日間に分散する毎日のメンテナンスウィンドウをスケジュールすると、AEMに次のエラーメッセージが表示される (NPR-35280)。

   ```TXT
   ERROR The start time must precede (be less than) the end time
   ```

### 統合 {#integrations-6570}

* 既存の [!DNL Adobe Launch] 設定の編集に失敗する (NPR-35045)。
* IMS 設定と [!DNL Adobe Target Standard] 環境を使用している場合、[!DNL Experience Fragments] を [!DNL Adobe Target] に書き出すことはできません (NPR-34555)。
* フォルダーから [!UICONTROL  オーディエンス ] ページに移動すると、[!UICONTROL  作成 ] オプションが [!UICONTROL  オーディエンス ] ページに表示される (NPR-35151)。

### Sling {#sling-6570}

* デフォルトのログインヘルスチェックは、存在しないユーザーの資格情報を検証します (NPR-34686)。

### 翻訳プロジェクト {#translation-6570}

* [!DNL Experience Manager] で翻訳プロジェクトをキャンセルしても、キャンセルするリクエストは翻訳プロバイダーに送信されません (NPR-34433)。

### [!DNL Communities] {#communities-6570}

* 製品内の不公平な用語のすべてのインスタンスは、受け入れられた同等のものに置き換えられます (NPR-34311)。
* [!DNL Google+] がソーシャル共有オプションのリストから削除される (NPR-33877)。

### [!DNL Brand Portal] {#brandportal-6570}

* [!UICONTROL  リスト表示 ] でのアセットの選択に対してユーザーインターフェイスが応答しない (NPR-34728)。

### [!DNL Forms] {#forms-6570}

>[!NOTE]
>
>[!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] サービスパックリリース日の 1 週間後にアドオンパッケージをリリースします。

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack には、の修正が含まれていませ [!DNL Forms]ん。別の [!DNL Forms] アドオンパッケージを使用して配信されます。 さらに、JEE 上の [!DNL Experience Manager Forms] の修正を含む累積インストーラーがリリースされました。 詳しくは、「 [AEM Formsアドオンのインストール ](#install-aem-forms-add-on-package) 」および「 [JEE へのAEM Formsのインストール ](#install-aem-forms-jee-installer) 」を参照してください。

**アダプティブフォーム**

* [!DNL Experience Manager] サービスパック 6 を適用した後、クラシック UI を使用してアダプティブフォームを編集できない (NPR-35126)。

* PDFをアダプティブフォームに変換する場合、タブ付きレイアウト上のフォームデータモデルを使用して、入れ子になったパネルの値を設定することはできません。 また、コードエディターを使用してラジオボタングループの値を静的な配列で動的に設定する際に問題が発生する (NPR-35062)。

* アダプティブフォームのテキストフィールドコンポーネントに日本語の文字を入力する場合、最大 35 文字を超える文字を指定できます (NPR-35039)。

* アダプティブフォームは、フォームの送信後に表示される **[!UICONTROL ありがとう]** ページに、`owner` や `status` などの不要なパラメーターを表示します (NPR-34989)。

* [!UICONTROL  添付ファイル ] コンポーネントの [!UICONTROL  ファイルの選択 ] ダイアログに、サポートされていないファイルタイプと、アダプティブフォームの送信中にエラーが発生する選択が表示されます (NPR-34970)。

* フォームの前にテキストを含む [!DNL Experience Manager Sites] ページにアダプティブフォームを挿入すると、カーソルのフォーカスは、フォームの前のテキストではなく、直接フォームに移動する (NPR-34947)。

* [!UICONTROL 「データを使用し] てプレビュー」オプションを選択した場合に、 [!DNL Experience Manager] 6.2 データの XML ファイルを使用してアダプティブフォームに事前に入力すると、適切に動作しない (NPR-35087)。

* アダプティブフォームのデータディクショナリを更新しても、アダプティブフォームがキャッシュされた値を返すので、フォームは変換されません (NPR-34845)。

* キャッシュの無効化が原因で、フラグメントのアダプティブフォームへの読み込みに時間がかかる。(NPR-34567)

* タブナビゲーションが、アダプティブフォームのスクリーンリーダーに対して適切に機能しない (NPR-34544)。

**Correspondence Management**

* フロート型を含む数値データを持つ XML タグの値をドラフトとして保存できない (NPR-35050)。

* ES3 からアセットを移行する場合、アセットには編集不可の 2 つのデフォルト条件が含まれます (NPR-34972)。

* レター内のデータディクショナリを編集すると、「[!UICONTROL  貸したコンテンツ ]」セクションに、有用な情報ではなく、回転する長方形が表示されます (NPR-34853)。

**インタラクティブコミュニケーション**

* [!DNL Forms] アドオンパッケージのインストール後に使用できるインタラクティブ通信のロールアウト設定名は、標準のロールアウト設定名と重複します (NPR-34976)。

**Document Security**

* 新しい Document Security ポリシーを保存すると、Experience Manager Formsに `Relative validity period is required` エラーメッセージが表示されます (NPR-34679)。

* Document Security でPDF2.0 ドキュメントを保護できない (CQ-4305851)。

セキュリティ更新について詳しくは、[Experience Managerセキュリティ速報ページ ](https://helpx.adobe.com/security/products/experience-manager.html) を参照してください。

## [!DNL Adobe Experience Manager] 6.5.6.0 {#experience-manager-6560}

Adobe Experience Manager 6.5.6.0 は、2019 年 4 月の **6.5 リリースの一般リリース (GA) 以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善を含む重要なアップデートです。**&#x200B;これは、Adobe Experience Manager 6.5 の上にインストールできます。

Adobe Experience Manager 6.5.6.0 で導入された主な機能および機能強化には、次が含まれます。

* [!UICONTROL  クイック公開 ] ウィザードまたは [!UICONTROL  公開を管理 ] ウィザードを使用して、[!DNL Experience Manager] または [!DNL Dynamic Media] にアセットを選択的に公開または非公開にする。

* [!DNL Dynamic Media] ユーザーインターフェイスを使用して、キャッシュされたコンテンツをコンテンツ配信ネットワーク (CDN) を無効にします。

* Brand PortalからExperience Manager Assetsへのアセット投稿フォルダーの公開が、プロキシサーバーを通じてサポートされるようになりました。

* [!DNL Experience Manager Assets] 内のプライベートフォルダーを削除すると、自動生成されたプライベートフォルダーのグループがクリーンアップされるようになりました。

* ビデオ [!UICONTROL  ビューア ] プリセットエディターの修飾子の説明を [!DNL Dynamic Media] で更新しました。

* [!DNL Dynamic Media] コネクタのステータスを反映する新しい会社設定が追加されました。

* 以前のDynamic Mediaの `Rasterize` から `test` と `aiprocess` のデフォルトオプションが `Thumbnail` に更新され、サムネールのみを作成して、ページ抽出とキーワード抽出をスキップする必要があるようになりました。

* [クライアントでのアダプティブフォームの事前入力](../../help/forms/using/prepopulate-adaptive-form-fields.md#prefill-at-client)

* [双方向 SSL 実装のサーバー上の RESTful API とフォームデータモデルを統合](../../help/forms/using/configure-data-sources.md)。

* [翻訳済みアダプティブフォームページのキャッシュ機能が強化されました](../../help/forms/using/configure-adaptive-forms-cache.md)。

* automated forms conversionサービス ](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=ja) での [Adobe Signテキストタグのサポート。

* [[!DNL Automated Forms Conversion service] を使用して、色付きのフォームをアダプティブフォームに変換 ](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html) できます。

* SMB 2 および SMB 3 プロトコルのサポート。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.22.4 に更新しました。

Experience Manager6.5.6.0 で導入された機能と機能強化の完全なリストについては、「 [Adobe Experience Manager 6.5 Service Pack 6 の新機能 ](new-features-latest-service-pack.md) 」を参照してください。

[!DNL Experience Manager] 6.5.6.0 リリースで提供された修正の一覧を次に示します。

### [!DNL Sites] {#sites-6560}

* [!DNL Sites] または [!DNL Screens] で、プロジェクトを選択し、[!UICONTROL [ パブリケーションの管理 ]] をクリックします。 ユーザーインターフェイスエラーが原因で、[!UICONTROL  公開を管理 ] ウィザードを進めることができません。 特に、「[!UICONTROL  公開 ]」オプションは機能しません (NPR-34099)。
* 「[!UICONTROL  継承をキャンセル ]」または「[!UICONTROL  継承を無効にする ]」オプションを選択解除した後、iParsys（継承された段落システム）の位置は、元のデフォルトの位置に戻りません (NPR-34097)。
* `RolloutConfigManagerFactoryImpl` がロールアウト設定を読み込めない場合、見つからない設定の読み込みは試行されません。 キャッシュされた設定を返す (NPR-34092)。
* テキストコアコンポーネントで、ソースHTMLの編集オプションを使用した後、`em` タグのクラスが削除される (NPR-34081)。
* Experience Manager6.3.3 からExperience Manager6.5.3 にアップグレードした後、ロールアウトプロセスに時間がかかり、ロールアウトがタイムアウトエラーで失敗する (NPR-34049)。
* `htmlwriter` は属性値をエンコードしません。 XF マークアップに存在するマークアップは、デコードされた属性値（`&#34` ではなく `"`）で書き出されます。 これにより、XF を使用する Visual Experience Composer で、ターゲット側で問題が発生します (NPR-34048)。
* [!DNL Experience Manager Sites] 内のページを移動する際に、理由を持つバージョン作成の失敗をキャプチャするためのログ機能を強化する (NPR-34014)。
* [!DNL Rich Text Editor] で、すべてのテキストが削除されると、段落タグも削除されます (NPR-33976)。
* （クラシック UI で）`siteadmin` ページを開くか更新すると、`New` メニューのオプションが無効になります (NPR-33949)。

   ![クラシック UI で見つからないメニューの問題を示すスクリーンショット](assets/33949_missing_menu.png)

* [!DNL Content Fragment] は `ContentFragmentUsePojo` で失敗するので、`TemplatedResource` として使用できません (NPR-33911)。
* 同期移動操作と非同期移動操作は、同時転送が原因でエラーが発生する可能性があります。 ページ移動操作は、非同期移動にのみ制限されます。 これにより、ページの同時移動が妨げられる (NPR-33875)。
* [!UICONTROL オーサ] ーインスタンスからパブリッシュインスタンスにコンテンツをレプリケートする「Publication」操作を管理すると失敗し、JavaScript エラーが発生する (NPR-33872)。
* 複数のページまたはアセットを選択してバージョンを作成する場合、新しいバージョンは、最後に選択されたページまたはアセットに対してのみ作成される (NPR-33866)。
* ライブコピーを含むブループリントページを別のフォルダーに移動します。 元のフォルダーに移動すると、移動操作がエラーなく失敗する (NPR-33864)。
* 移動アクションを使用して [!DNL Sites] コンソールで Web ページの名前を変更すると、ウィザードの最後の手順で、重なり合う 2 つのダイアログが表示されます (NPR-33831)。

   ![重複する移動ダイアログの NPR-33831の問題を示すスクリーンショット](assets/33831_rename_dialog.png)

* コピーおよび貼り付け操作中に、コピー上の `cq:acLinks` および `cq:acUUID` プロパティが削除されます (NPR-33794)。[!DNL Adobe Campaign]
* 別の親ライブコピーの子ページでロールアウトを試みると、[!DNL Experience Manager] によってヌルポインタ例外が生成される (NPR-33676)。
* レイアウトコンテナをコピーして再度ページに貼り付けると、レイアウトコンテナ内の [!DNL RTE] コンポーネントが表示されなくなります。 [!DNL RTE] コンポーネントは編集できませんが、ページの更新時に表示されます (NPR-33662)。
* 異なるブレークポイント（中、大）に対してレイアウトコンポーネントのサイズを変更する場合、レイアウトが期待どおりに動作しない (NPR-33608)。
* [!DNL RTE] のインライン編集モードでは、画像をドラッグしてもテキストコンポーネントに対しては機能しない (NPR-33602)。
* ブループリントページ内に、ページ名と同じ名前のコンポーネントを作成できます。 ロールアウト中は、`_msm_moved` が末尾に付いて、コンポーネントの名前を変更します。 コンポーネントが [!UICONTROL  段落システム ] の最後に移動されます (NPR-33535)。
* 多くのページやアセットで offTime または onTime が設定されている場合、リソースが大量に消費され、起動時とシャットダウン時にシステムの速度が低下します (NPR-33482)。
* `/content/experience-fragment` の CRUD 権限を持つユーザーがフォルダーを削除できない (NPR-33436)。
* [!DNL Experience Fragments] セクションの親フォルダーで、[!UICONTROL Adobe Target書き出し形式 ] のオプションとして [!UICONTROL HTMLと JSON] を選択できます。 この親フォルダーのサブフォルダーに対して、同じプロパティがタッチ操作対応 UI に表示されます。 ただし、CRXDE では、`cq:adobeTargetExportFormat` の場合、`html,json` を表示する代わりに、HTMLだけを表示します (NPR-33423)。
* ページエイリアスの公開または非公開はサポートされていません。 他の場合に要求されるオプションを削除します (NPR-33415)。
* [!DNL Experience Manager] 内の別の場所に、特定のタグを移動できます。 また、移動前と移動後に、異なるページに適用することもできます。 ページのプロパティを編集する際に、タグが同じであっても、タグが編集用に表示されない (NPR-33353)。
* 複数のレイアウトコンテナを含むテンプレートからレイアウトコンテナが削除された場合、ページテンプレートが正しくレンダリングされない。(NPR-33347)
* テンプレートエディターで、`/content/` の下の100000ページ以上で使用されているテンプレートを削除してみます。 エラーメッセージが表示されずにエラーが表示される (NPR-33312)。
* `PageRedirectServlets` が URL フラグメントまたはアンカーの後にクエリ文字列を配置するので、アンカーを含む [!DNL Experience Manager] ページへのリダイレクトはオーサーインスタンスで機能しません。(NPR-34288)
* `/content/campaign` の下にブランドを作成すると、キャンペーンを作成できない構造になります。 [!UICONTROL 「Create ] Brandoption」を選択すると、「Create」オプションがないので、オファーとアクティビティを作成する機能を持たずに、新しく作成されたブラン    ドがそのまま残ります (NPR-34113)。
* ページの [!DNL Live Copy] を休止すると、エディターモードで確認できるように、で継承が解除されます。 ページプロパティで、継承を表すアイコンが誤って、継承が存在し、壊れていないことを示す (NPR-34017)。
* 多数の参照を持つページは非同期で移動できず、移動操作が失敗する場合があります (CQ-4297969)。
* URL 内に `/` 文字を含む Web ページが、オーサリング中に応答しなくなります。 オーサリング中にコンポーネントを追加すると、CPU 使用率が増加し、ブラウザーの応答が停止します (CQ-4295749)。
* 参照モードでは、NVDA は「タイプ/サイズ」メニューオプションから選択した値を読み上げません。 選択した要素に視覚的なフォーカスがない。 スクリーンリーダーに依存するユーザーは、参照モードを使用できません (CQ-4294993)。
* Web ページの作成時に、ユーザーは [!UICONTROL  コンテンツページ ] テンプレートを選択できます。 「[!UICONTROL  ソーシャルメディア ]」タブで、「[!UICONTROL  優先 XF バリエーション ]」を選択します。 NVDA 参照モードでエクスペリエンスフラグメントを選択する場合、ユーザーはキーボードキーを使用できません (CQ-4292669)。
* ハンドルバーライブラリを、より安全な v4.7.3 に更新しました (NPR-34484)。
* [!DNL Experience Manager Sites] コンポーネントの複数のクロスサイトスクリプティングインスタンス (NPR-33925)。
* 新しいフォルダーを作成する際のフォルダー名フィールドに、保存されたクロスサイトスクリプティングに対する脆弱性がある (GRANITE-30094)
* [!UICONTROL  ウェルカム ] ページの検索結果とパス完了テンプレートが、クロスサイトスクリプティングに対して脆弱である (NPR-33719、NPR-33718)。
* 非構造化ノードでバイナリプロパティを作成すると、バイナリプロパティダイアログでクロスサイトスクリプティングがおこなわれる (NPR-33717)。
* CRX DE インターフェイスで [!UICONTROL  アクセス制御テスト ] オプションを使用する場合のクロスサイトスクリプティング (NPR-33716)。
* ユーザ入力は、クライアントに情報を送信する際に、様々なコンポーネントに対して適切にエンコードされない (NPR-33695)。
* カレンダー表示でのクロスサイトスクリプティング (Experience Managerインボックスの場合 )(NPR-33545)。
* `childrenlist.html` で終わる URL は、404 応答ではなくHTMLページを表示します。 このような URL は、クロスサイトスクリプティングに対して脆弱です (NPR-33441)。


### [!DNL Assets] {#assets-6560}

**Experience Manager Assetsのアクセシビリティの強化**

* キーボードキーを使用して、[!UICONTROL  参照 ] アセットのリストのインタラクティブユーザーインターフェイスオプションにアクセスし、フォーカスできるようになりました (NPR-34115)。

* スクリーンリーダーが、検索ページ上の述語の意図されたアクションを通知するようになった (NPR-34104)。

* 検索ページと検索結果ページに、スクリーンリーダーユーザーをより深く理解できるよう、より多くの情報が表示されるようになりました (NPR-34093)。

* スクリーンリーダーが、アセット [!UICONTROL  プロパティ ] ページの「[!UICONTROL  基本 ]」タブで選択したタグを削除するオプションを読み上げるようになりました (NPR-33972)。

* リスト表示の各行の要素が、スクリーンリーダーによって同じ行の要素としてアナウンスされるようになった (NPR-33932)。

* `Tab` キーを使用して移動する際のユーザーフォーカスが、バージョンプレビューの閉じるオプションに移動するようになった (NPR-33863)。

* オムニサーチが閉じられた後、ユーザーのフォーカスが検索アイコンに移動するようになった (NPR-33705)。

* キーボードキーを使用してナビゲーションした場合、操作可能なユーザーインターフェイスオプションの視覚的なフォーカスが目立ち、コントラストが強化されました。 キーボードユーザーは、フォーカスされた領域を識別できる (NPR-33542)。

* キーボードを使用したドラッグ機能が、スクリーンリーダーの参照モードで [!UICONTROL  メタデータスキーマエディター ] で動作するようになりました (CQ-4296326)。

* リンク共有ダイアログで、参照モードで移動する際に、スクリーンリーダーに次の操作を行います。

   * ダイアログが読み込まれるとすぐに、テーブル情報を読み上げない。

   * リストに表示されているすべての自動候補に移動できます。

   * 「[!UICONTROL  電子メールアドレスを追加/検索 ]」に対して表示される自動候補を読み上げます (CQ-4294232)。

* `Esc` キーを使用してカード表示からクイックアクションアイコンを削除しても、最後にフォーカスされた項目からキーボードフォーカスが削除されなくなりました (CQ-4293554)。

* ユーザーインターフェイスのインタラクティブオプションの場合、スクリーンリーダーがアイコンのリテラル名ではなく目的を読み上げるようになりました (CQ-4272943)。

* キーボードフォーカスが [!UICONTROL  フライアウト ]、[!UICONTROL InlineZoom]、[!UICONTROL Shoppable_Banner]、[!UICONTROL Zoom_dark]、[!UICONTROL Zoom_light]、[!UICONTROL ZoomVertical_dark アセットの詳細 [!UICONTROL [!DNL Dynamic Media] のビューア ] でキーボードの Tab キーを使用して移動する際の、a11/> および [!UICONTROL ZoomVertical_light] オプション (CQ-4290605)。]

* [!UICONTROL アセットのプ] ロパティページの「保存して閉じる」オ  プションが、キーボードキーを使用してアクセスできるようになりました (NPR-34107)。

* ログインページのユーザー名とパスワードの組み合わせが正しくないことによるエラーメッセージが、エラーが発生するたびにスクリーンリーダーによって通知されるようになりました (NPR-33722)。

* [!DNL Experience Manager] ヘッダーセクションで、参照モードで移動すると、スクリーンリーダーが次の情報を通知するようになりました。

   * [!UICONTROL  オムニサーチで ] を検索するには、自動編集した候補を入力します。

   * [!UICONTROL  ソリューション ]、[!UICONTROL  ヘルプ ]、[!UICONTROL  インボックス ]、[!UICONTROL  ユーザー ] の各オプションで、展開または折りたたまれた状態。

   * 「[!UICONTROL  ヘルプ ]」オプションの下の「[!UICONTROL  ヘルプを検索 ]」フィールドに検索文字列を入力すると表示される [!UICONTROL  ヘルプ ] の検索ステータスメッセージ。

   ![ヘッダーのヘルプメニュー](assets/Help_aem_header.png)

   *図： [!UICONTROL ヘルピンヘルプメ] ニューを  検索します。*

   * 誤った値が [!UICONTROL 「[!UICONTROL  ユーザー ]」オプションの下の「] として動作」フィールドに入力され、フォーカスが正しくテキストフィールドに移動すると、エラーメッセージが表示される (NPR-33804)。

   ![ヘッダーのユーザーメニュー](assets/User_aem_header.png)

   *図： [!UICONTROL ヘッダーの] ユーザーメニュ  ーのフィールドとして実行します。*

* ユーザーは、次のウィンドウ内のキーボードを使用してフォーカスを変更できるようになりました。

   * [!UICONTROL リンク共有ダイアログの「電子メ] ールアドレス [!UICONTROL を検索/] 追加」フィールド

   * [!UICONTROL フォルダープロパティの「] 権限」タブの「閉じられたユーザーグループ [!UICONTROL 」の下に、ユーザーまたはグループフィールドを追加しま] す    (NPR-34452)。

**Experience Manager Assetsで修正された問題**

[!DNL Adobe Experience Manager] 6.5.6.0 で [!DNL Assets] は、次の問題を修正しました。

* 注釈がアセットのタイムラインから選択されても、ハイライト表示されない (CQ-4302422)。

* [!DNL Adobe InDesign] テンプレートを使用して作成したマーケティングコラテラルアセット（パンフレット、チラシ、名刺など）のプレビューに、改行と段落区切りが表示されない (NPR-34268)。

* テキスト抽出と、アップロードされたPDFファイルの全文検索が機能しない (NPR-34164)。 この問題を解決するには、Service Pack 6 をインストールした後に [!DNL sAdobe Experience Manager] デプロイメントを再起動します。

* 複数ページのアセットのタイムラインで、アセットを参照する際に、特定のサブアセットに固有の注釈を表示する代わりに、すべてのサブアセットに適用された注釈を表示する (NPR-34100)。

* フォルダーに JavaScript、CSS または JSON ファイル形式のリソースが含まれている場合、「 [!UICONTROL  公開を管理 ] 」オプションを使用してアセットフォルダーが公開されない (NPR-34090)。

* オムニサーチで適用されたタグまたはフィルターの選択を解除または削除すると、検索クエリが複数回実行され、検索時間が長くなる (NPR-34078)。

* （フォルダー内のアセット上の）ワークフローが進行中または保留中の場合、カード表示では、ワークフローが完了または終了するまでページが再読み込みされます。 したがって、作成者は、下にスクロールする必要があるフォルダー内のアセットを操作できません (NPR-33986)。

* ユーザーが公開済みのアセットを新しい場所に移動すると、「[!UICONTROL  再公開 ]」オプションの選択を解除しても、アセットが再公開されます。 これにより、多数の孤立したアセットがパブリッシュインスタンス上に配置されます。 ただし、デフォルトの動作では、公開済みのアセットに対する移動操作によって自動的に非公開になります。このアセットは、アセットの移動時に作成者が「[!UICONTROL  再公開 ]」オプションを選択した場合に再公開されます (NPR-33934)。

* コレクション内のアセットの [!UICONTROL HTMLを移動 ] ページでは、[!UICONTROL  調整/再公開 ] オプションなど、すべてのアセットコンテンツが読み込まれるわけではありません。 したがって、ユーザーは移動操作を完了できない (NPR-33860)。

* アセットを移動し、移動したアセットの名前とタイトルに特殊文字を追加すると、そのアセットの新しい場所に（同じ名前の）追加のフォルダーが作成されます (NPR-33826)。

*  ダウンロードダイアログで「Emailoption」が選択さ  れている場合、アセットのダウ  ンロードボタンが無効になる (NPR-33730)。

* アセットに対して一括操作（一括メタデータ編集など）を実行すると、「要求 —URI が長すぎます」というエラーが表示される (NPR-33723)。

* [!UICONTROL Add through JSON path] 機能で [!UICONTROL Folder Metadata Schema Form Editor] によって [!UICONTROL Dropdown] フィールドに生成された選択肢を選択または削除できない (NPR-33712)。

* アセットが [!DNL desktop app] または [!DNL Adobe Asset Link] の [!UICONTROL 「開く ] 」オプションを使用して更新され、[!DNL Adobe Experience Manager] に同期された場合、アセットの静的レンディションは更新されません (CQ-4296279)。

* 列表示では、一連のアセットの移動操作によって、[!UICONTROL 「フィルター ]」オプションを使用する前に選択したアセットも移動されます。 「[!UICONTROL Filter]」オプションを使用すると、前の選択が選択解除されることに注意してください (NPR-34018)。

* 名前に特殊文字が含まれるアセットの検索候補で、特殊文字の前にバックスラッシュが追加される。(NPR-33834)

* [!UICONTROL  フォルダーメタデータスキーマフォーム ] でドロップダウンのルールを作成すると、ユーザーは [!UICONTROL  フィールドの選択肢 ] 列の値を選択できません (CQ-4297530)。

* [!DNL Experience Manager] 6.5 Service Pack 5 または以前のバージョンを [!DNL Experience Manager] 6.5 にインストールすると、（`/var/workflow/models/dam` で作成された）アセットのカスタムワークフローモデルの実行時コピーが削除されます (NPR-34532)。 ランタイムコピーを取得するには、HTTP API を使用して、ワークフローモデルのデザイン時コピーとランタイムコピーを同期します。
   `<designModelPath>/jcr:content.generate.json`。

**Dynamic Mediaで修正された問題**

* ユーザーがビデオプロファイルの作成後に編集時にエンコーディング設定を定義した場合、スマート切り抜き設定はビデオプロファイルから削除されます (CQ-4299177)。

* ユーザーがアセットの詳細ページのサイドレールオプション（例：[!UICONTROL  概要 ]、[!UICONTROL  タイムライン ]、[!UICONTROL  ビューア ]）を切り替えると、ページの読み込み時にアセットがちらつく (NPR-34235)。

* 再処理ジョブで次の問題が発生しました。

   * ジョブ ID が再処理ジョブによって返されたジョブハンドルにありません。

   * ビデオログのジョブを再処理する際に、フルパスではなくファイル名のみを使用します。

   * 再処理ジョブには、アセットタイプを静的に設定するオプションはありません。

   * `ExcludeFromAVS` オプションが指定されていません (CQ-4298401)。

* 画像プロファイルが複数（例えば、11）の縦横比を持つフォルダーに追加されると、スマート切り抜き機能がエラーで失敗する (NPR-34082)。

* Dynamic Media Scene7(CQ-4299727) で設定された [!UICONTROL  ツール ] 内の [!UICONTROL 「ワークフロー ]」タブの [!UICONTROL  ワークフローアーカイブ ] ページをスクロールすると、DAM アセットの更新ワークフローがトリガーされます。[!DNL Adobe Experience Manager]

* [!UICONTROL  ビューアプリセットエディター ] の [!UICONTROL 「ビヘイビアー ]」タブのシンボルがローカライズされません (CQ-4299026)。

* メインビューでは、ビューアがレスポンシブモードの場合、画像が正しくないレイアウトで表示され、ビューアに収まりません (CQ-4298293)。

* [!UICONTROL Adobe Experience Manager] の画像プリセットに対する変更がScene7 Publishing System に同期されない (CQ-4299713)。

### [!DNL Commerce] {#commerce-6560}

* アセットが移動されたときに、製品からのアセットへのリンクがリファクタリングされない (NPR-34098)。

### Platform {#platform-6560}

* アップグレードされたExperience Managerインスタンスの診断ツールを使用してログをダウンロードできない。(NPR-34336)
* `cq-wcm-api` 基盤パッケージの特定のバージョンへの依存関係が原因で、アップグレードが失敗します (CQ-4300520)。
* デフォルトエージェント（パブリッシュ）設定の「 **[!UICONTROL 接続タイムアウト]** 」と「 **[!UICONTROL ソケットタイムアウト]** 」のデフォルト値が指定されていません (NPR-33707)。
* `/etc/map.publish` 下のマッピング設定の更新がサイトページに反映されない (NPR-34015)。
* [API リファレンス](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html) ドキュメントには、パッケージのドキュメ `com.day.cq.tagging` ントは含まれていません (CQ-4295864)。

### ユーザーインターフェイス {#ui-6560}

* オフロードするブラウザーインターフェイスにすべてのジョブトピックが表示されない (NPR-34308)。
* [ 設定ブラウザー ](/help/sites-administering/configurations.md) のインターフェイスにすべての設定が表示されない (NPR-33644)。
* 別のユーザーとして実行するユーザーを検索する際に `Esc` キーを押すと、ユーザーリストの代わりに **[!UICONTROL User]** ダイアログが閉じます (NPR-34084)。

### 統合 {#integrations-6560}

* 長い名前のアクティビティは [!DNL Adobe Target] と同期されない (NPR-34254)。

* 新しいAdobeの起動設定を作成する際にプロパティを選択すると、次のエラーメッセージが表示される。(NPR-33947)

   ```javascript
   GET http://hostname:Port/libs/cq/dtm-reactor/content/configurations/createcloudconfigwizard/jcr:content/body/items/form/items/wizard/items/general/items/fixedcolumns/items/container/items/general/items/property/data.html?query=&start=0&end=25&imsConfigurationId=Adobe%20Launch&companyId=&_charset_=utf-8 400 (Bad Request)
   ```

### 翻訳プロジェクト {#translation-6560}

* ユーザーの `authorizableID` に特殊文字が含まれている場合、翻訳プロジェクトは作成されません (NPR-33828)。

### Sling {#sling-6560}

* ヘルスチェックとパターン検出には、重複する機能があります。 その結果、ヒースチェックが製品から削除されます (NPR-33928)。

### WCM {#wcm-6560}

* 基盤コンポーネント — 基盤画像コンポーネントをページに追加して画像を参照する場合、 `Undo` 操作は機能しません (NPR-34516)。

* ページ移動操作を使用できません (CQ-4303028)。

### [!DNL Communities] {#communities-6560}

* ソーシャルメディアで投稿を共有すると、古いオプションGoogle+が表示される (NPR-33877)。

* コミュニティメンバーが、グループテンプレートや他のグループ機能の設定を変更できない。(NPR-33530)

* 画像のハイパーリンクタグがフォーラム投稿で正しく生成されない (NPR-33464)。

* アクセシビリティのエラーは、コミュニティ割り当て機能で識別されます (NPR-33442)。

* 管理コンソールを通じて追加されたコミュニティグループの既存のユーザーは、コミュニティグループコンソールで変更を加えると、ユーザーリストから削除されます (NPR-34315)。

* `TagFilterServlet` は、潜在的に機密データを漏れる (NPR-33868)。

<!--
* Tag filters are vulnerable to sensitive information disclosure (NPR-33868).
-->

### [!DNL Forms] {#forms-6560}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack には、の修正が含まれていませ [!DNL Forms]ん。別の [!DNL Forms] アドオンパッケージを使用して配信されます。 さらに、JEE 上の [!DNL Experience Manager Forms] の修正を含む累積インストーラーがリリースされました。 詳しくは、「 [AEM Formsアドオンのインストール ](#install-aem-forms-add-on-package) 」および「 [JEE へのAEM Formsのインストール ](#install-aem-forms-jee-installer) 」を参照してください。

[!DNL Experience Manager Forms] 6.5.6.0 アドオンパッケージのインストール後：

* [!DNL Experience Manager Forms] インスタンスを停止します。

* `bcpkix-1.51`、`bcmail-1.51`、および `bcprov-1.51` の JAR ファイルを `crx-repository\launchpad\ext` ディレクトリから削除します。

* `sling.properties` ファイルから ` sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider` プロパティを削除します。

* [!DNL Experience Manager Forms] インスタンスを再起動します。

**アダプティブフォーム**

* 見つからないアダプティブフォームフラグメントがある場合、そのアダプティブフォームがレンダリングに失敗する (NPR-34302)。

* アダプティブフォームフィールドのヘルプコンテンツの説明に段落HTMLタグが表示される (NPR-34116)。

* 「**[!UICONTROL サーバーで再検証]**」プロパティを選択すると、アダプティブフォームは送信に失敗します (NPR-33876)。

* **[!UICONTROL REST エンドポイントへの送信]** 送信アクションは、アダプティブフォームでは機能しません (CQ-4299044)。

* アクセシビリティ：必須フィールドの添付ファイルをアップロードせずにアダプティブフォームを送信しようとしても、フォーカスが添付フィールドに自動的に移動することはありません (CQ-4298065)。

* アダプティブフォームの表に行を追加する場合、「**[!UICONTROL 上に追加]**」および「**[!UICONTROL 下に追加]**」の各オプションでは、適切な結果が表示されません (CQ-4297511)。

* [!UICONTROL  値のコミット ] スクリプトが正しくトリガーされず、アダプティブフォームでデータが失われます (CQ-4296874)。

* 日付選択が、ローカライズされたアダプティブフォームに対して正しく機能しない (NPR-34333)。

* ファイル名にアンダースコアまたはスペースが含まれている場合、そのファイルをアダプティブフォームに添付することはできません (CQ-4301001)。

* ネストされた繰り返し可能なパネルの回数が親より多い場合、ネストされた繰り返し可能なパネルの発生回数がすべて事前入力に失敗する (NPR-33666)。

* アダプティブフォームには、いくつかのオープンリソースリゾルバーがあります。 これらは送信エラーを引き起こします。 この問題は断続的に発生します (CQ-4299407)。

* フィールド設定を初めて開いたときに、プロパティアイコンが表示されません (CQ-4296284)。

* アダプティブフォームの送信時に、`afPath`、`afSubmissionTime`、`signers` などの送信メタデータを編集できます。 この問題を解決するために、クライアント側のフォーム送信データからメタデータ値が削除されます。 ユーザーは `FormSubmitInfo` オブジェクトを使用して、これらの値をサーバーから取得できます (NPR-33654)。

* ユーザー入力は、クライアントに情報を送信する際に、[!DNL Forms] コンポーネントに対して適切にエンコードされない (NPR-33611)。

**ワークフロー**

* ワークフローの承認者が添付ファイルをアップロードすると、添付ファイルの名前が `undefined` に変更されます (NPR-33699)。

* [!DNL Experience Manager] ワークフローのパージ操作が失敗し、次のエラーメッセージが表示される (NPR-33575)。

   `java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory`

* [!DNL Experience Manager Forms] フォーム [!DNL Windows] の送信後、のアプリが応答を停止する (NPR-34409)。

* AEM Service Pack をインストールすると、項目の **To Do** リストがリンクとして表示されません。 **To Do** 項目のテキストには、HTMLタグが含まれます (NPR-34317)。

**インタラクティブコミュニケーション**

* ネストされた繰り返し可能なコンポーネントを含むテキストドキュメントフラグメントを含めると、インタラクティブ通信の保存に失敗する (NPR-34095)。

**Correspondence Management**

* データディクショナリ値を含むテキストドキュメントフラグメントを変更すると、エージェント UI が応答を停止する (NPR-33930)。

* [!DNL Microsoft Word] ドキュメントからレターのテキストドキュメントフラグメントにコンテンツをコピー&amp;ペーストすると、フォーマットの問題が発生する (NPR-33536)。

**ドキュメントサービス**

* Output サービスとFormsサービスを使用して XDP ファイルからPDFファイルを生成すると、テキストが欠落し、重複する結果になります (NPR-34237、CQ-4299331)。

* HTMLファイルをPDFに変換する場合、 `MaxReuseCount` 属性は設定できません (NPR-33470)。

* Reader拡張のインタラクティブ機能を含むPDFファイルをダウンロードする場合、[!DNL Adobe Reader] を使用してPDFファイルに添付ファイルを追加することはできません (NPR-33729)。

**Document Security**

* [!DNL Experience Manager] Service Pack をインストールした後、PDFファイル内の HSM ベースの証明書を使用して署名操作を実行できない。(NPR-34310)

**デザイナー**

* Designer バージョン 6.5.x で XForms を開けない (CQ-4295322)。

* Designer を開くと、ようこそ画面に誤った年が表示されます (CQ-4295289)。

* [!DNL Acrobat DC] をサーバーにインストールすると、「**[!UICONTROL フォームを配布]**」オプションは非アクティブになります (CQ-4296304)。

セキュリティ更新について詳しくは、[Experience Managerセキュリティ速報ページ ](https://helpx.adobe.com/security/products/experience-manager.html) を参照してください。

## [!DNL Adobe Experience Manager] 6.5.5.0 {#experience-manager-6550}

Adobe Experience Manager 6.5.5.0 は、2019 年 4 月の **6.5 リリースの一般リリース (GA) 以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善を含む重要なアップデートです。**&#x200B;これは、Adobe Experience Manager 6.5 の上にインストールできます。

[!DNL Adobe Experience Manager] 6.5.5.0 で導入された主な機能と機能強化には、次のものが含まれます。

* 匿名でのCRXDE Liteへのアクセスは許可されていません。 代わりに、ユーザーはログイン画面に移動します。 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) を使用した開発を参照してください。

* [!DNL Adobe Experience Manager] インボックスに表示する列名をカスタマイズします。

* ページエディター、コアコンポーネント、RTE、管理者ユーザーインターフェイスなど、Experience ManagerWeb コンテンツ管理 (WCM) の様々な領域でのアクセシビリティを改善しました。

* [!DNL Interactive Communication] をドラフトとして保存します。

* JEE 上のExperience Manager Formsでの [!DNL Oracle WebLogic 12] のサポート。

* [!DNL Adobe Experience Manager Assets] ユーザーインターフェイスフローの例外処理を改善しました。

* Dynamic Media Scene7の公開 URL を取得するには、新しいメソッド `getRemoteAssetPublishURL` が `com.day.cq.dam.api.s7dam.scene7.ImageUrlApi` インターフェイスに追加されます。

* [Web コンテ](#assets-6550) ンツアクセシビリ [!DNL Adobe Experience Manager Assets] ティガイドライン (WCAG) に準拠したアクセシビリティの強化。

* Adobe Experience Manager内からパッケージ共有の統合を削除しました。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.22.3 に更新しました。

Experience Manager6.5 Service Pack 5 で導入された主な機能の一覧については、 [Adobe Experience Manager 6.5 Service Pack 5 の新機能 ](new-features-latest-service-pack.md) を参照してください。

[!DNL Experience Manager] 6.5.5.0 リリースで提供された修正の一覧を次に示します。

### [!DNL Sites] {#sites-6550}

* Experience Manager Sitesには、エイリアスからページを公開または非公開にするオプションが用意されています。 このオプションが機能しない (NPR-33415)。
* 複数のテンプレートを含むテンプレートからレイアウトコンテナを削除すると、そのテンプレートが正しくレンダリングされない (NPR-33347)。
* Experience Manager Sitesページが、複数のライブコピーを含む大きなコンテンツセットの一部である場合、ページのバージョン履歴プレビューを読み込めない (NPR-33311)。
* 「移動」コマンドを使用してExperience Manager Sitesページの名前を変更すると、ページタイトルは更新されない (NPR-33264)。
* 列表示を通じてページを移動すると、列が消える (NPR-33216)。
* 言語コピーのローカルコンポーネントの名前がブループリントのコンポーネントの名前と同じで、コンポーネントがブループリントからロールアウトされる場合、ローカルコンポーネントの名前に「 `_msm_moved` 」は追加されません (NPR-33208)。
* ページリダイレクトサーブレットは、ResourceType が `cq:Page` でない場合に、Experience Manager Sitesの URLに.html を追加します (NPR-33176)。
* サブツリーを貼り付ける場合、対応するサブページを貼り付けるかどうかを決定するオプションはありません (NPR-33149)。
* コンポーネントのライブ使用の結果数は 49 に制限されます (NPR-33058)。
* スキーマにコンテンツフラグメントをベースにし、そのフラグメントに必須のテキスト領域またはパスフィールドが含まれている場合、コンテンツフラグメントの保存に失敗する (NPR-33007)。
* デフォルトのエクスペリエンスフラグメントコンポーネントを使用してカスタムコンポーネントを作成し、Experience Manager Sitesページで使用すると、Experience Managerにカスタムコンポーネントの参照（使用状況）が表示されない。(NPR-32852)
* 多数の参照を含むフォルダーの名前を変更すると、そのフォルダーへの参照の多くは更新されない (NPR-32765)。
* ソース編集オプションを有効にすると、インラインのフルスクリーンオプションに使用できるようになりますが、リッチテキストエディターの編集ダイアログやフルスクリーンオプションには引き続き表示されません (NPR-32763)。
* 複数フィールドがあり、ブループリントのページプロパティに必須フィールド（ドロップダウンやパスフィールドなど）が含まれている場合、そのような複数フィールドを含むページをロールアウトすると、ライブコピーのページプロパティは保存されません (NPR-32751)。
* スクリーンリーダーは、見出し構造を使用してページを移動できません。 さらに、「Components」タブのラベルが正しくない (NPR-32648)。
* ページネーションが開始すると、エクスペリエンスフラグメントピッカーがすべての項目を読み込まない (NPR-32605)。
* ライブコピーの読み取り、変更、作成および削除をおこなう作成者権限は取り消されます。 各作成者は、ブループリント内でページを移動する読み取りおよび変更権限を明示的に提供する必要がありました (NPR-32550)。
* Adobe Analyticsとの統合があるページの Launch をコンテンツ作成者が作成できない (NPR-32548)。
* ユーザーが同期を使用して継承を再開すると、親ページのライブコピーがブループリントと同期せず、誤ったステータスが表示される (NPR-32500)。
* Experience Manager Sitesエディターページの読み込みに 15 秒以上かかる (NPR-32413)。
* 一部のフィールドで、「継承をキャンセル」オプションが表示されない。(NPR-32362)
* エクスペリエンスフラグメントコンポーネントのパスを選択し、「選択ダイアログを開く」チェックボックスを選択した場合、パスブラウザーで選択されたパスに移動しない (NPR-32308)。
* Experience Manager6.2 からExperience Manager6.5 にアップグレードすると、静的テンプレートの Parsys コンポーネントが正しく表示されません。 Parsys コンポーネントの高さが 0 に設定され、その中のコンポーネントが表示されない (NPR-33663)。
* ユーザーがレイアウトコンテナを同じページにコピーして貼り付けると、レイアウトコンテナ内のコンポーネントが表示されない (NPR-33648)。
* Dispatcher のヘルスチェックで、ログファイルに `Invalid cookie header` 警告メッセージが表示される (NPR-33629)。
* PreferencesServlet に XSS が反映された (NPR-33438)。
* 匿名ユーザーは、CRXDE Lite機能にアクセスできます (GRANITE-27790)。

### [!DNL Assets] {#assets-6550}

>[!IMPORTANT]
>
>[!DNL Experience Manager desktop app] の Windows ユーザーは、[ デスクトップアプリケーションバージョン 2.0.3.2](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html#what-is-new) にアップグレードして、[!DNL Adobe Experience Manager 6.5.5.0] インスタンス上の DAM リポジトリにアクセスすることをお勧めします。 デスクトップアプリケーションバージョン 2.0.2 を使用して [!DNL Adobe Experience Manager] 6.5.5.0 インスタンスの DAM リポジトリーにアクセスする際に問題が発生する可能性があるので、

**Experience Manager Assetsのアクセシビリティの強化**

* [!UICONTROL  コメント ] リストにキーボードフォーカスを移し、アセットの [!UICONTROL  タイムライン ] パネルの [!UICONTROL  新しいバージョン ] の下に [!UICONTROL  バージョンコメントを作成 ] するクリック可能なオプションが追加されました。(NPR-33424)

* アセットの「[!UICONTROL  設定を表示 ]」オプションにアクセスし、キーボードキーを使用して [!UICONTROL  設定を表示 ] ダイアログの設定を変更できるようになりました (NPR-33420)。

* コンボボックスのリストボックスポップアップ（異なるページの様々なフィールド）に、スクリーンリーダーがアナウンスできるオプションのリストとしてエントリが表示されるようになりました (NPR-33516)。

* 並べ替え可能なヘッダーの並べ替え機能（リスト表示、[!UICONTROL  タイムライン ] 表示、[!UICONTROL  公開を管理 ] ページ）が、スクリーンリーダーによって通知され、列ヘッダーの並べ替えコントロールにキーボードを使用してアクセスできる。(NPR-32979)

* コメントカード、バージョン更新、コンボボックス、メニューの山形アイコンなどのクリック可能な要素に焦点を当て、キーボードを使用して操作できるようになりました (NPR-33514)。

* [!UICONTROL  インサイトビュー ] のインサイトアイコン（使用方法、インプレッション数、クリック数）の機能（またはアクションの目的）が、スクリーンリーダーによって正しくアナウンスされるようになりました。(NPR-33513)

* 読み取り専用フォームフィールド（例えば、アセット [!UICONTROL  プロパティ ] の [!UICONTROL 「基本」タブ ] の無効なフィールド）が、キーボードを使用してフォーカスできるようになりました (NPR-33493、CQ-4273031)。

* 様々な入力フィールドのラベルが、テキストの入力時に消えたプレースホルダーラベルだけでなく、永続的なラベル（したがってアクセス可能）になりました (NPR-33475)。

* 異なる見出しレベル（ページタイトルやセクション見出しなど）が、スクリーンリーダーユーザーに対して異なるレベルの見出しとして認識されるようになりました (NPR-33471)。

* リンクやオプション（アセットページのヘッダーとズームオプション、フォルダーナビゲーションオプション）などのインタラクティブなユーザーインターフェイス要素が、キーボードを使用してアクセスできるようになりました (NPR-33468、CQ-4271412)。

* [!UICONTROL  公開を管理 ] ページの [!UICONTROL  オプション ]、[!UICONTROL  スコープ ]、[!UICONTROL  ワークフロー ] の進行状況インジケーターが、タブではなく、進行状況インジケーターとして正しく読み上げられるようになりました。(NPR-33416)

* アセット [!UICONTROL  プロパティ ] またはカード表示の「[!UICONTROL  詳細 ]」タブの「[!UICONTROL  評価 ]」セクションなど、星評価アイコンの色は、視覚が限られ、色の知覚がないユーザーに対して適切なコントラストが表示されるように変更される。(NPR-33414)

* アセットの詳細ページの [!UICONTROL  コメント ] フィールドの横にある山形の上向き矢印が、キーボードキーを使用してアクセスできるようになりました (NPR-33397)。

* アセット [!UICONTROL  プロパティ ] と左側のパネルのナビゲーション（アセットのユーザーインターフェイス）の [!UICONTROL  タグ ] ダイアログの展開状態と折りたたみ状態が、スクリーンリーダーによって正しく通知されるようになりました。(NPR-33396)

* [!DNL Adobe Experience Manager] Assets 上のすべての参照済みページのタイトルが一意になりました (NPR-33343)。

* ツリー構造内を移動する際に、ツリー表示コントロールの様々な要素がスクリーンリーダーによって正しく通知されるようになった (NPR-33304)。

* アセットの詳細ページの [!UICONTROL  タイムライン ] 表示の異なるバージョンのアセットに、キーボードキーを使用してアクセスできるようになりました (NPR-33283)。

* オムニサーチコンボボックスに表示される検索候補の名前が、検索機能の使用時にスクリーンリーダーによって通知されるようになった (NPR-33280)。

* クリック可能な要素と [!UICONTROL [!UICONTROL  リンク ] に移動 ] が、スクリーンリーダーによってクリック可能な要素としてアナウンスされるようになりました (NPR-33278)。

* [!UICONTROL  共有リンク ] ダイアログのテーブル構造情報（行 1、セル 1、テーブルなど）は、ダイアログが開いたときに、スクリーンリーダーによってアナウンスされなくなる (NPR-33268)。

* 様々なコンボボックス要素の目的（アセットのプロパティの「基本」タブで「パス」フィールドや「選択ダイアログを開く」オプションなど）が、スクリーンリーダーによって正しく読み上げられるようになりました。(NPR-33235)

* リスト表示テーブルの行が選択可能な情報が、キーボードフォーカスがあるときにスクリーンリーダーユーザーに伝えられるようになりました。 ポインターが行の上に置かれると、スクリーンリーダーは情報を読み上げる (NPR-33234)。

* [!UICONTROL  プロパティ ] の [!UICONTROL  基本 ] タブの [!UICONTROL  タグ ] フィールドの下の選択した各タグを削除するオプション（[!UICONTROL x] を含む）が、スクリーンリーダーでアクセスできるようになりました。(NPR-33206)

* カレンダーの日付選択が、スクリーンリーダーユーザーと目の見えるキーボードユーザーによって、キーボードを使用してフォーカスでき、操作可能になりました (NPR-33200)。

* リスト表示とカード表示を切り替える切り替えで、（表示の調整という）機能がスクリーンリーダーに正しく表示されるようになりました (NPR-33069)。

* 左側のパネルのメニューにアクセスできるようになりました。 メニューを拡張する機能と目的は、スクリーンリーダーによって適切にアナウンスされる (NPR-33068)。

* リストボックスやその他の多くのユーザーインターフェイス要素が、目の見えないスクリーンリーダーユーザーがアクセスできるようになり、それらに関する次の情報がスクリーンリーダーによって通知されるようになりました (NPR-33040)。

   * フォームを送信する前に、要素に対してユーザー入力が必要かどうか。
   * 要素が編集できないかどうか。
   * ウィジェットが選択されているかどうか。

* フィルターのサイドバーを開くオプションが、キーボードを使用してアクセスできるようになりました (NPR-32842、CQ-4273018)。

* リスト表示の列ヘッダーのチェックボックスコントロールがアクセス可能になり、コントロールを使用する目的がスクリーンリーダーによって通知されるようになった (NPR-32722、NPR-33005)。

* カレンダー日付選択の時間 (HH) および分 (mm) フィールドのラベルは、プレースホルダーラベルではなく永続的なラベルになり、ユーザーがこれらのフィールドにテキストを入力したときに消えなくなりました (NPR-32720)。

* （ベルのアイコンをクリックした後に表示される）通知のリンクテキストが、スクリーンリーダーユーザーに通知され、各リンクにアクセスする際にタブを使用する (NPR-32645)。

* [!UICONTROL 「]インサイト [!UICONTROL 」のアセットカードで、「]」、「 [!UICONTROL ダウンロード]」、「 [!UICONTROL プロパティ] 」、「その他のアクション」の各オプションを選択しま  す。これで、キーボードを使用してアクセスできるようになりました。(NPR-32609)

* 目に見えないコンテンツ（検索結果のヘッダーメニューバーの内容など）が、キーボードを使用してアクセスしたときに、スクリーンリーダーによってアナウンスされなくなった (NPR-32606)。

* カレンダー日付選択で次の月と前の月に移動するコントロールのラベルの目的が、スクリーンリーダーによってアナウンスされるようになった (NPR-32604)。

* 星評価アイコンが、キーボードキーを使用して、フォーカス可能で操作可能になった (NPR-32513)。

* ビデオのボリュームを制御する機能に、（ボリュームスライダにフォーカスする）タブと（ボリュームを調整する）矢印キーを介して、キーボードでアクセスできるようになりました (NPR-32065)。

* ファイルサイズフィルターの下限 ([!UICONTROL From]) と上限 ([!UICONTROL To]) の入力フィールドの目的が、目の見えないスクリーンリーダーユーザーに対して通知されるようになりました。(NPR-32064)

* [!UICONTROL  作成と翻訳 ] フォームの [!UICONTROL  言語 ] メニューが、参照モードでスクリーンリーダーにアクセスできるようになりました (CQ-4293906)。

* [!UICONTROL  参照 ] パネルに、次の機能強化を適用してアクセスできるようになりました (NPR-33261、CQ-4293798)。

   * 参照モードで、スクリーンリーダーのフォーカスが、「[!UICONTROL  サイト参照 ]」、「[!UICONTROL  アセット参照 ]」、「[!UICONTROL  コピー ]」、「[!UICONTROL  フォーム参照 ]」の下の非表示の複数行編集フィールドに移動しなくなりました。

   * スクリーンリーダーが、[!UICONTROL  サイト参照 ] および [!UICONTROL  言語コピー ] 要素の役割を読み上げるようになりました。

   * ブラウズモードでのスクリーンリーダーのフォーカスは、意味のある順序で様々な要素に移行する。

* [!UICONTROL メタデータスキ] ーマエディターページとその要素がキーボードを使用してアクセスできるようになり、スクリーンリーダーに適するようになりました (CQ-4290962、CQ-4272953)。

* 選択したタグを削除する `X` 記号の目的が、選択したタグの数と共にスクリーンリーダーによって通知されるようになりました (CQ-4273017)。

* スクリーンリーダーを使用する目の見えないユーザーが混乱するのを防ぐため、装飾用のアイコンと画像はスクリーンリーダーで無視されるようになりました (CQ-4272944)。

**Experience Manager Assetsで修正された問題**

[!DNL Adobe Experience Manager] 6.5.5.0 Assets では、次の問題を修正しました。

*  コレクション内 [!UICONTROL のア] セットに対するワークフローダイアログの作成の開始オプションが無効になっているので、ワークフローがトリガーされない。(NPR-32471)

* メタデータスキーマでカスケードポップアップを使用する場合、（子ドロップダウンから）アポストロフィを含むドロップダウンオプションを選択して保存すると、選択したアポストロフィオプションが、アセット [!UICONTROL  プロパティ ] を再び開いた後に消える。(NPR-32649)

* [!UICONTROL アセットインサイ] トの同期ジョブは停止し、次のエントリに移動する代わりに（Analytics 側で）無効なエントリが検出された場合に失敗します (NPR-32674)。

* パノラマビューアのモバイルブラウザーでは、モーションセンサーがデフォルトで無効になっているので、ジャイロスコープは機能しません (CQ-4272937)。

* [!UICONTROL 6.5.1] に 6.5.3 をインストールすると、Connected Assets の設定ウィザードが 404 エラーで動作しない (NPR-32730)。

* XMPの書き戻しプロセス中、すべてのカスタム名前空間メタデータプロパティは、設定された名前空間プレフィックスとは異なり、カスタム名前空間プレフィックスを ns2 に変更します (NPR-32748)。

* 遅延読み込みがトリガーされず、通知インボックスからタスクを確認するために選択したときに 100 個のアセットのみが表示される (NPR-32750)。

* `NullPointerException` は、新しく作成されたユーザープロファイル (SAML/SSO) でノードの環境設定が見つからないことが原因で発生します。このエラーは、新しくログインしたユーザーが [!DNL Adobe Experience Manager Stock] 統合を使用できないようにします (NPR-32777)。

* 10,000 個を超えるアセットを含むスマートコレクションを開くと、ログにトラバーサル警告が表示される (NPR-32980)。

* Dynamic Media Scene7実行モードで動作している [!DNL Adobe Experience Manager] でアセットを別のフォルダーに移動すると、アセット名が小文字に変更される (NPR-32995)。

* 検索結果からプロパティに移動した後、検索結果に戻って削除した後で、検索されたアセットを削除することはできない (NPR-32998)。

*  「アセットを移動」インターフェイスで宛先フォルダーを選 [!UICONTROL 択する] と、次のオプションが無効のままになる。(NPR-33356)

*  親ノード（単一の子フォルダーが表示される）を選択してから子フォルダーを選択すると、Nextoption が有効にならない。(NPR-33275)

* 読み取り、作成、変更などの他の権限が付与されている場合でも、削除権限を持つAdobeの Asset Link(AAL) でチェックインおよびチェックアウト権限が無効になっている (NPR-33272)。

* スマート切り抜きレンディションは、アセットのダウンロードダイアログで使用できない (NPR-33167)。

* スマート切り抜きプロファイルを持つフォルダーの下でPDFのレンディションレールを開くと、ログに例外が記録されます (CQ-4294201)。

* Dynamic Media Scene7実行モードとのExperience Manager時に [!UICONTROL Dynamic Media同期モード ] がデフォルトで無効になっている場合、画像プリセットは公開されません (CQ-4294200)。

* 一括アップロード中のアセット処理が停止し、ワークフローインスタンスに DAM 更新アセットのスタックインスタンスが表示される (CQ-4293916)。

* Experience ManagerでのDynamic Media設定の作成は機能しますが、ユーザーインターフェイスで「保存」を選択しても何も起こりません (CQ-4292442)。

* F4V ビデオアセットのプレビューが、Safari/Macでのプログレッシブ再生で機能しない (CQ-4289844)。

* 親フォルダー内のアセットをスマート切り抜きする際に、名前にドット `.` 文字が含まれる追加のフォルダーが作成されます (CQ-4289337)。

* サムネールが壊れ、ビデオのコピー時にビデオ処理バナーが表示されない (CQ-4284125)。

* ディメンショナルビューアで、空のカメラビューを持つ一部のモデルに対して、Firefox で空のサムネールが誤って表示される (CQ-4283447)。

* 6.5.5.0 で修正されたパフォーマンスの問題は次のとおりです (CQ-4279206)。

   * 大きなバイナリをDynamic Media Image Processing Server にアップロードするには、時間がかかりすぎます。

   * Dynamic Media Scene7アーキテクチャが原因で、Experience Managerのサムネール生成時間が長くなりました。

* Dynamic Media Scene7の移行に関する問題が、大量のアセットを持つお客様に発生する (CQ-4279206)。

* `setVideo` を使用すると、ビデオ 360 ビューアのレイアウトが壊れ、`video= modifier` を使用するとビデオが下にシフトします (CQ-4263201)。

* SDL パッケージのインストール中にExperience Managerメッセージが表示される (NPR-33175)。

* Experience Managerの SSRF 脆弱性 (NPR-33435)。

### Platform {#platform-6550}

* `/etc/maps` の下に `sling:match` マップエントリが作成された場合、[!DNL Sling] フィルターは呼び出されません (NPR-33362)。
* [!DNL Apache Lucene] のセグメント化障害が原因でExperience Managerがクラッシュする (NPR-32988)。
* [!DNL Jackson] コアパッケージがExperience Manageruberjar ファイルに見つからない (NPR-32848)。
* CRXDE Liteが、ノードの `jcr:primaryType` プロパティに対する読み取り権限を持たないユーザーのコンテンツを読み込まない。(NPR-32611)
* [!DNL Granite] メンテナンスタスクスケジューラーは、Experience Managerデプロイメント中に再初期化が頻繁におこなわれすぎます (CQ-4294627)。
* SQL クエリが長時間（例えば 7 時間）実行されると、Experience Managerは応答を停止する (NPR-33044)。

### ユーザーインターフェイス {#ui-6550}

* ラジオボタンの選択がマルチフィールドで保持されない (NPR-33309)。
* 遅延読み込み制限がリスト表示で機能しない (NPR-33124)。
* 一致がない場合、オムニサーチ結果ページにメッセージが表示されない (NPR-32974)。
* オムニサーチフィルターは、`/content` ノード以下にあるすべての一致を返し、選択された場所を無視する (NPR-32849)。

### 統合 {#integrations-6550}

* Adobe Targetコンポーネントを含むページが公開されると、内部キャッシュがクリアされる (NPR-33162)。
* Adobe Targetとの統合は [!DNL Windows Internet Explorer] 11 では機能しません (NPR-33111)。
* Adobe Targetを設定する際に、レポートソースを選択すると、「[!UICONTROL  会社 ]」と「[!UICONTROL  レポートスイート ]」のフィールドが表示されない (NPR-32502)。
* [!DNL Adobe I/O] を使用して [!DNL Experience Fragments] を書き出す場合、ソース製品などのメタデータはAdobe Targetに書き出されない (NPR-32159)。
* ローカルのExperience Manager管理グループの権限を持つ IMS ユーザーは、IMS 設定を作成または変更できない。(NPR-33045)
* Adobeの起動設定ページにすべてのレコードが表示されない (NPR-33011)。
* JavaScript エラーが原因で、content-authors グループのユーザーがAdobe Targetコンポーネントのプロパティを編集できない。(NPR-32996)
* JSON のクロスサイトスクリプティング (NPR-32744)。

### 翻訳プロジェクト {#translation-6550}

* 翻訳されたタグは、サードパーティのExperience Managerサービスから翻訳に読み込まれません (NPR-33154)。
* 翻訳設定ページに、翻訳に使用されたものとは異なる翻訳プロバイダーが表示される (NPR-32971)。
* 既存の翻訳プロジェクトにエクスペリエンスフラグメントフォルダーを追加すると、新しいプロジェクトが作成されます (NPR-32843)。
* 翻訳ジョブの実行時にログに `NullPointerException` エラーが表示される (NPR-32628)。

### WCM {#wcm-6550}

* ページエディター — [!DNL Sites] ページエディターでは、キーボードのみのユーザーが、ヘッダーで使用可能なすべてのオプションを使用してタブフォーカスを移動する代わりに、メインコンテンツにスキップすることはできません (CQ-4293883)。
* ページエディター — Well コンポーネントを使用し、保存したデータを含むパネルが、[!DNL Chrome] および [!DNL Firefox] バージョンで更新されたので表示されません (CQ-4292995)。
* MSM — ページからコンポーネントを削除しても、公開済みバージョンのページからはコンポーネントは削除されません (CQ-4292360)。

### [!DNL Brand Portal] {#assets-brand-portal-6550}

* [!DNL Brand Portal] から公開済みのメタデータスキーマを削除すると、エラーが発生します (CQ-4292063)。
* 管理者がAdobe開発者コンソールを通じてBrand Portalで [!DNL Experience Manager Assets] 6.5.4 を設定した場合、[!DNL Brand Portal] ユーザーは、投稿フォルダーのアセットを [!DNL Brand Portal] から [!DNL Experience Manager] に公開できません (NPR-33046)。
* 親フォルダーの重複レプリケーションが競合の原因となる (NPR-33001)。

### [!DNL Communities] {#communities-6550}

* クイック編集メニューオプションを使用してモデレートコンソールのカードを削除できない (NPR-33117)。
* [!UICONTROL  アクティビティストリーム ] ページへのアクセス時にエラーが発生する (NPR-33146)。
* オーサーインスタンスで削除されたグループが、すべてのパブリッシュインスタンスから削除されない (NPR-33199)。
* 作成者は、新しいグループを作成した後、 [!DNL Internet Explorer] 11 の [!UICONTROL  コミュニティグループ ] セクションにリダイレクトされない (NPR-33205)。
* メッセージインボックス内のExperience Managerにアクセスしても、メッセージのステータスは読み取りに変わらない (NPR-32764)。
* [!DNL Communities] グループを編集してサムネール画像を変更しても、グループサムネール画像は更新されない (NPR-32599)。
* ユーザーがコミュニティ内の別のユーザーに電子メールを送信できない (NPR-32598)。
* 送信されたブログは、ユーザーがページを更新するまで表示されない (NPR-32391)。
* ユーザー生成コンテンツ (UGC) の通知と購読のバージョンを作成する際に、ソースページの ID が正しく保存されません (CQ-4279355、CQ-4289703)。
* クロスサイトスクリプティングの問題 (NPR-33203)。

### ワークフロー {#workflow-6550}

* 左側のレールの [!UICONTROL  タイムライン ] オプションの読み込みに予想以上の時間がかかる (NPR-32851)。
* Experience Managerインスタンスを再起動した後、コレクションのレビュータスクの電子メールに、誤ったペイロードリンクが含まれる (NPR-32774)。

### [!DNL Forms] {#forms-6550}

>[!NOTE]
>
>Experience Managerサービスパックには [!DNL Forms] の修正が含まれていません。 別の Forms アドオンパッケージを使用して配布されます。さらに、JEE 上のAEM Formsの修正を含む累積インストーラーがリリースされました。 詳しくは、「 [Experience Manager Formsアドオンのインストール ](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 」および「 [JEE へのExperience Manager Formsのインストール ](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer) 」を参照してください。

* Correspondence Management:ターゲット領域内のアセットの順序は、文字を送信した後でシャッフルする (NPR-33359、NPR-33153)。
* アダプティブForms:ユーザーがアダプティブフォームを編集すると、[!UICONTROL  ページ情報 ] メニューの「[!UICONTROL  ワークフローを開始 ]」オプションが機能しない (NPR-33004)。
* アダプティブForms:ユーザーが複数の添付ファイルを含むアダプティブフォームを保存できない。(NPR-32997)
* アダプティブForms:アダプティブフォームでパネルレイアウトを変更すると、エラーが発生します (CQ-4293880)。
* アダプティブForms:アダプティブフォームの辞書の文字列に新しい行が追加され、`&#xa;` 文字が辞書に追加される (NPR-33266)。
* アダプティブFormsのアクセシビリティ：ユーザーがアダプティブフォームをHTMLフォームとしてプレビューする場合、「[!UICONTROL  手書き署名 ]」フィールドがタブフォーカスを保持できない (NPR-33159)。
* アダプティブFormsのアクセシビリティ：アダプティブフォームの送信時に表示されるエラーメッセージが `aria-describedBy` 属性にリンクされない。(NPR-33071)
* アダプティブFormsのアクセシビリティ：アダプティブフォーム内で必須とマークされたフィールドが、ARIA アクセシビリティスキーマで必須属性を「True」に設定していない。(NPR-33070)
* PDFG サービス：ユーザーがテキストファイルをPDFに変換すると、日本語の文字が正しくレンダリングされない (NPR-33238)。
* PDFG サービス：`CreatePDF` 操作で、PDFファイルをPDFOCR 形式に変換できない (NPR-32994)。
* PDFG サービス：PDF変換が [!DNL OpenOffice] ドキュメントの 200 番目のインスタンスで失敗する (NPR-32766)。
* バックエンドの統合：無効な状態が正しくないため、更新トークンの有効期限が切れると、フォームデータモデルの要求が失敗する。(NPR-33169)
* デザイナー：スクリーンリーダーは、XDP ファイルで定義されているカスタムタブ順序の代わりに、デフォルトの地理的順序に基づいてタブ順序を実行する (NPR-32160)。
* デザイナー：タグ付けオプションが有効な場合、生成されたPDF出力でサブフォームの境界線が消える (NPR-32778)。
* GuideSOMProviderServlet(NPR-32700) と共に XSS を格納。

## Adobe Experience Manager 6.5.4.0 {#experience-manager-6540}

Adobe Experience Manager 6.5.4.0 は、新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善を含む重要なアップデートです。2019 年 4 月の 6.5 リリース（a0/>a4 月 **）の一般リリース以降にリリースされました。**&#x200B;これは、Adobe Experience Manager 6.5 の上にインストールできます。

Adobe Experience Manager 6.5.4.0 で導入された主な機能および機能強化には、次のものが含まれます。

* Adobe Experience Manager Assets は、[!DNL Adobe I/O] コンソールを通じてBrand Portalで設定されるようになりました。

* 新しい「[ 印刷可能な出力を生成 ](../forms/using/aem-forms-workflow-step-reference.md)」手順が、Adobe Experience Manager Formsのワークフローで使用できるようになりました。

* [アダプティブフォー](../forms/using/resize-using-layout-mode.md) ムおよびインタラクティブ通信のレイアウトモードで複数列をサポート。

* HTML5 フォームでの [ リッチテキスト ](../forms/using/designing-form-template.md) のサポート。

* [Experience Manager Assetsのアクセ](new-features-latest-service-pack.md#accessibility-enhancements) シビリティの強化。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.10.8 に更新しました。

* `content/dam` で利用可能なコンテンツをすべて同期する代わりに、選択的なコンテンツサブツリーを *Dynamic Media - Scene7モード* に同期できるようになりました。

* SOAP Web サービスとのフォームデータモデルの統合で、要素の選択グループまたは属性がサポートされるようになりました。

* SOAP 入力または出力と複雑なデータ構造で、動的グループ置換がサポートされるようになりました。

最新のサービスパックで導入された機能と主な特徴の一覧については、[Adobe Experience Manager 6.5 サービスパックの新機能 ](new-features-latest-service-pack.md) を参照してください。

### Sites {#sites-fixes}

* Adobe Experience Manager Sitesページの URL にコロン (`:`) またはパーセンテージ記号 (`%`) が含まれている場合、ブラウザーは応答を停止し、CPU 使用スパイクが発生します (NPR-32369、NPR-31918)。

* Experience Manager Sitesページを編集用に開き、コンポーネントをコピーした場合、一部のプレースホルダーで貼り付け操作が使用できない。(NPR-32317)

* 公開を管理ウィザードを開くと、コアコンポーネントにリンクされたエクスペリエンスフラグメントが、公開済み参照のリストに表示されない。(NPR-32233)

* タッチ UI のライブコピーの概要が、クラシック UI よりもレンダリングに時間がかかる (NPR-32149)。

* サーバー時間とマシン時間が異なるタイムゾーンにある場合、スケジュールされた公開時間はタッチ UI でサーバー時間を表示するのに対して、クラシック UI ではマシン時間が表示される (NPR-32077)。

* Experience Manager Sitesが URL のサフィックスを持つページを開けない (NPR-32072)。

* ユーザーがコンテンツフラグメントを編集すると、削除されたバリエーションのコンテンツフラグメントが復元される (NPR-32062)。

* ユーザーは、必須フィールドに情報を入力せずにコンテンツフラグメントを保存できます (NPR-31988)。

* kernel.js と ui.js は、事前にコンパイルまたはキャッシュされません。 ページのレンダリングにさらに時間がかかる (NPR-31891)。

* PageEventAuditListener が有効な場合、コミットキューの長さが長くなります。 これは、一括公開、ナビゲーション、一括アセット移動など、多くの操作のパフォーマンスに影響を与えます (NPR-31890)。

* エクスペリエンスフラグメントがドラッグされると、応答時間が長くなる (NPR-31878)。

* レスポンシブグリッドのプレースホルダーで「コンポーネントをここにドラッグ」オプションを選択すると、GETリクエストが送信され、リクエストが HTTP 403 エラーになる (NPR-31845)。

* 同じフォルダー内のコンテンツを移動すると、ページ移動オプションが無効になる (NPR-31840)。

* 編集可能テンプレートの構造モードでは、レイアウトコンテナの許可されたコンポーネントリストに正しくない結果が表示されます。 デザインダイアログを持つコンポーネントのみがレイアウトコンテナに表示される (NPR-31816)。

* ページにユーザーに対する読み取り専用権限がある場合、「プロパティを開く」オプションは sites.html に表示されるが、editor.html には表示されない (NPR-31770)。

* ユーザーが「作成」ボタンをクリックすると、ページオプションが使用できない (NPR-31756)。

* OOTB（標準）デザインインポーターコンポーネントを含むAdobeキャンペーンでキャンペーンを同期できない。(NPR-31728)

* 箇条書きリストを番号付きリストに変更しようとすると、リストの最初の 2 つの項目のみが変更されます (NPR-31636)。

* ページが作成解除され、子ノードが選択されても、選択ダイアログには初期ノードが表示されます。 ページを作成し、ユーザーが「参照」をクリックすると、ページは、作成したノードではなくルートノードにリダイレクトされる (NPR-31618)。

* ビュー設定ダイアログボックスが、インボックスカスタマイズワークフロー機能 (NPR-32503および NPR-32492) に対して正しく機能しない。

* インボックスを使用してワークフロー情報を表示すると、エラーメッセージが表示されます (CQ-4282168)。

### Assets {#assets-6540-enhancements}

* アセット収集ページのトリガーワークフローへのボタンが無効になっている (NPR-32471)。

* Dynamic Media Scene7設定を使用してExperience Manager内でアセットを別のフォルダーに移動すると、名前のないフォルダーが SPS(Scene7 Publishing System) に作成される (NPR-32440)。

* 「すべて選択」を使用して、公開済みアセットを含むフォルダーにすべてのアセットを移動するアクションが失敗し、エラーが発生する (NPR-32366)。

* ${extension} を持つアセットのレンディションの生成に失敗しました (NPR-32294)。

* バージョン履歴 URL は、アセットのプロパティページの「参照元」フィールドに表示される。(NPR-31889)

* DAM からダウンロードした ZIP ファイルを WinZip を使用して開くことができない (NPR-32293)。

* フォルダー設定を開くと、元の権限が更新され、フォルダーのタイトルやサムネール画像が変更されて保存される (NPR-32292)。

* スケジュールされたアクティベーションのカレンダーアイコンが、アクティベーションの日時が後でスケジュールされているアセットの「ステータス」列（DAM アセットリストのクラシック UI）に表示されない (NPR-32291)。

* スニペットテンプレートを使用したスニペットの作成で、スニペット作成プロセス中にコレクションの検索でエラーが発生する (NPR-32290)。

* 検索フィルターから複数のタグが選択されると、複数の検索クエリが実行される。(NPR-32143)

* ファイル名に 50 文字を超えるアセットがアップロードされると、Experience Manager Assets UI にファイル名が切り捨てられて表示される (NPR-32054)。

* Adobe Stockのチェックボックスツリーのレベル 2 のチェックボックスが選択されている場合、フィルターパネルのすべてのチェックボックスは、最初と 2 番目のチェックボックスがオフになっているときにオフになります (NPR-31919)。

* オムニサーチファセットを使用したファイルおよびフォルダー検索で例外が発生する (NPR-31872)。

* 依存関係ルールが対応するメタデータスキーマフォームに設定されている場合、メタデータエディターでの必須フィールド選択のフィールドハイライトが、必須フィールドを選択した後でも削除されない。(NPR-31834)

* （タグ階層からの）リーフレベルタグの完全な名前が、アセットのプロパティページに表示されない (NPR-31820)。

* Safari ブラウザーでアセットのプロパティページから back コマンドを使用するとエラーが発生する (NPR-31753)。

* タッチ UI 検索（オムニサーチを通じて実行）の結果ページが自動的にスクロールアップし、ユーザーのスクロール位置が失われる (NPR-31307)。

* PDFアセットのアセットの詳細ページに、Dynamic Media Scene7実行モードで実行されているExperience Managerで「コレクションに追加」ボタンと「レンディションを追加」ボタン以外のアクションボタンが表示されない (CQ-4286705)。

* Scene7のバッチアップロード処理では、アセットの処理に時間がかかりすぎます (CQ-4286445)。

* ユーザーがDynamic Mediaクライアントのセットエディターで変更を加えていない場合、「保存」ボタンを押しても、リモートセットは読み込まれません (CQ-4285690)。

* サポートされている 3D モデルがExperience Managerに取り込まれる場合、3D アセットのサムネールは情報を提供しません (CQ-4283701)。

* スマート切り抜きビデオビューアプリセットの未処理のステータスが、プリセット名の横のバナーテキストに 2 回表示されます (CQ-4283517)。

* 3D ビューアでプレビューしたアップロード済み 3D モデルのコンテナの高さが、アセットの詳細ページで誤って表示される (CQ-4283309)。

* カルーセルエディターが、Experience ManagerDynamic Mediaハイブリッドモードで IE 11 で開かれない (CQ-4255590)。

* Chrome および Safari ブラウザーで、ダウンロードダイアログの電子メールドロップダウンでキーボードフォーカスが動かない (NPR-32067)。

* Experience Managerで DM クラウド設定を追加しようとすると、「すべてのコンテンツを同期」チェックボックスがデフォルトで有効になりません (CQ-4288533)。

### Foundation UI {#foundation-ui-6540}

* フィルターパネルを使用してアセットを検索する際、既存のフィルターフィールドに留まる代わりに、前のフィルターフィールドに移動します (NPR-32538)。

* プラットフォームタグ付け：タグフィールドに入力してタグを検索すると、ルート境界の外にあるタグが表示され、タグフィールドの `rootPath` プロパティが適用されない (NPR-31895)。

* プラットフォーム UI:テキストフィールドに無効なパスが追加されると、パスブラウザーが壊れる (NPR-31884)。

* 通知が、ページ選択のスティッキーメニューの背後に隠れる (NPR-31628)。

### Platform {#platform-sling-6540}

* (HTL) アンダースコアは、URL のパスセクションのコロンを置き換えます (NPR-32231)。

### プロジェクト {#projects-6540}

* ユーザーがサブフォルダーにプロジェクトを作成する権限を持っている場合でも、「作成」ボタンがユーザーに表示されない。(NPR-31832)

### プロジェクトの翻訳 {#projects-translation-6540}

* `Apache Sling JSP Script Handler` で「トリムスペース」オプションが有効になっていると、翻訳プロジェクトの作成によって UI が壊れる (NPR-32154)。

* 翻訳するタグが翻訳プロジェクトに追加されると、UI のエラーとエラーログのヌルポイント例外が発生する (NPR-31896)。

### 統合 {#integrations-6540}

* Launch ライブラリ URL の生成は、Launch API の `path` 値と `library_name` 値のみに基づいており、`library_path` 値に基づいていない (NPR-31550)。

* LiveFyre 関連項目の処理中にエラーメッセージが表示されます (FYR-12420)。

* ReportSuitesServlet が SSRF に対して脆弱である。（NPR-32156）

### WCM テンプレートエディター {#wcm-template-editor-6540}

* 編集可能テンプレートの構造モードで、レイアウトコンテナで許可されたコンポーネントリストにリンクボタンコンポーネントが表示されません (CQ-4282099)。

### WCM ページエディター {#wcm-page-editor-6540}

* オーバーレイを選択し、レスポンシブグリッドコンポーネントをここにドラッグすると、エラーが発生します (CQ-4283342)。

### キャンペーンターゲティング {#campaign-targeting-6540}

* Target クラウドの設定が失敗し、「get mboxes request failed」というエラーが表示されます (CQ-4279880)。

### Brand Portal {#assets-brand-portal-6540}

* Brand PortalユーザーがExperience Manager6.5.4 の [!DNL Adobe I/O] にアップグレードすると、投稿フォルダーのアセットを [!DNL Assets] に公開できない (CQDOC-15655)。 Experience Manager6.5.4 の即時修正をおこなうには、[ ホットフィックス ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) をダウンロードして、オーサーインスタンスにインストールすることをお勧めします。

* メタデータスキーマポップアップ値がアセットのプロパティに表示されない (CQ-4283287)。

* メタデータサブスキーマに、アセットプロパティの MIME タイプに基づくタブが表示されません (CQ-4283288)。

* 非公開メタデータスキーマが、バックエンドでスキーマが削除されてもエラーメッセージを入力する。

* 公開済みアセットのプレビュー画像が表示されない (CQ-4285886)。

* 名前に一重引用符が含まれているアセットを公開または非公開にできない (CQ-4272686)。

* 複数のアセットのダウンロード中に利用条件が表示されない (CQ-4281224)。

* セキュリティに関する小さな脆弱性を解消。

### Communities {#communities-6540}

* 「メンバーの作成」フォームが空白のページとして表示される (NPR-31997)。

* ユーザーがオーサーインスタンスで Analytics レポートを表示できない (NPR-30913)。

### Oak — インデックス作成とクエリ {#oak-indexing-6540}

* Tika パーサーで解析が失敗し、クラスが見つからないエラーが発生した場合、JPEGイメージを含む MS Word および MS Excel ドキュメントが表示される (NPR-31952)。

### Forms {#forms-6540}

>[!NOTE]
>
>Experience Managerサービスパックには、Experience Manager Formsの修正は含まれていません。 別の Forms アドオンパッケージを使用して配布されます。さらに、JEE 上のAdobe Experience Manager Formsの修正を含む累積インストーラーがリリースされました。 詳しくは、「 [Experience Manager Formsアドオンのインストール ](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 」および「 [JEE へのExperience Manager Formsのインストール ](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer) 」を参照してください。

* Correspondence Management:後処理ワークフローに送信した後、レターに余分な文字が表示される (NPR-32626)。

* Correspondence Management:レターは、後処理ワークフローに送信した後、テキストコンポーネントとしてドロップダウンプレースホルダーを表示する (NPR-32539)。

* Correspondence Management:レターテンプレートで定義されたデフォルト値は、プレビューモードで表示されない。(NPR-32511)

* モバイルForms:送信ボタンは、HTMLバージョンで XDP フォームをレンダリングする際に、サイズが拡張されて表示される。(NPR-32514)

* ドキュメントサービス：Service Pack 2 を適用した後のレターおよびその他のページの URL アクセスの問題 (NPR-32508、NPR-32509)。

* ドキュメントサービス：サーバー上のトランザクション数が特定の制限を超えると、PDF変換のHTMLが失敗し、ファイルタイプ設定が [!DNL Forms] サーバーから削除されます (NPR-32204)。

* アダプティブForms:ブラウザーアクセシビリティツールが、WCAG2 レベル AA ガイドライン (NPR-32312、NPR-32309、CQ-4285439) に従ってアダプティブフォーム内のエラーを報告する。

* アダプティブForms:Chrome ブラウザーのアクセシビリティツールが、ベストプラクティスの失敗を報告する (NPR-32310)。

* アダプティブForms:Experience Manager Sitesページに埋め込まれたアダプティブフォームの設定時に翻訳の問題が発生する (NPR-32168)。

* Workbench:「Get Error Properties」操作をPDFUtilities サービスに使用すると、PDFメッセージが表示される。(NPR-32150)

* Document Security:保護されたPDFファイルをオフラインで開く際に、DisableGlobalOfflineSynchronizationData オプションが True に設定されている場合に失敗する (NPR-32078)。

* デザイナー：タグ付けオプションが有効な場合、生成されたPDF出力でサブフォームの境界線が消える (NPR-32547、NPR-31983、NPR-31950)。

* デザイナー：表内に結合されたセルがある場合、出力サービスを使用して XDP フォームから変換された出力PDFファイルのアクセシビリティテストが失敗します (CQ-4285372)。

* Foundation JEE:Experience Manager Formsサーバーがクラスターから切断された場合、キャッシュの問題によってサーバーへの再接続が妨げられます (NPR-32412)。

## Adobe Experience Manager 6.5.3.0 {#experience-manager-6530}

[!DNL Adobe Experience Manager] 6.5.3.0 は、パフォーマンス、安定性、セキュリティ、お客様向けの主要な修正および 2019 年 4 月の 6.5 リリースの一般リリース以降にリリースされた機能強化を含む重要なリリ **ースです**。[!DNL Adobe Experience Manager] 6.5 の上にインストールできます。

この Service Pack リリースの主な特徴は次のとおりです。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.10.6 に更新しました。

* [!DNL Experience Manager Assets] は、Deflate64 アルゴリズムを使用して作成された ZIP アーカイブをサポートするようになりました。

* 作成日（並べ替え可能）の新しい列が DAM リスト表示およびリスト表示のアセット検索結果に追加されました。

* 名前列に基づくアセットの並べ替えが、リスト表示で有効になりました。

* [!DNL Dynamic Media] では、スマート切り抜きビデオアセットをサポートするようになりました。スマート切り抜きは、シーンの焦点に従ってフレームを移動しながらビデオを再切り抜く機械学習主導の機能です。

* [!DNL Dynamic Media] は、スマートイメージングをサポートします。

* [[!DNL Experience Manager] ワークフローで不在 ](../forms/using/configure-out-of-office-settings.md) 環境設定を設定できます。

* [[!DNL Experience Manager] ワークフロー内の他のユーザーと受信ボックスまたは受信ボックス項目 ](../forms/using/configure-shared-queues-osgi.md) を共有する機能。

* [ バッチモードでインタラクティブ通信を生成する機能 ](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

* ContextHub にバンドルされている jQuery のバージョンを 3.4.1 に更新しました。

### Assets {#assets-6530-enhancements}

**製品の機能強化**

* [!DNL Experience Manager Assets] は、Deflate64 アルゴリズムを使用して作成された ZIP アーカイブをサポートするようになりました (NPR-27573)。

* 作成日の新しい列（並べ替え可能）が DAM リスト表示およびリスト表示のアセット検索結果に追加される。(NPR-31312)

* リスト表示では、ユーザーは [!UICONTROL  名前 ] 列を使用してアセットのリストを並べ替えることができます (NPR-31299)。

* GLB、GLTF、OBJ、STL の各ファイルは、DAM の [!UICONTROL Asset Details] ページでプレビューできます (CQ-4282277)。

* `ReplicationOnModifyListener` のチャンクアップロード中に、チャンクノードに対してイベ [!DNL Dynamic Media] ントがトリガーされます (CQ-4281279)。

* [!DNL Dynamic Media] では、スマート切り抜きビデオアセットをサポートするようになりました。スマート切り抜きは、シーンの焦点に従ってフレームを移動しながらビデオを再切り抜く機械学習主導の機能です (CQ-4278995)。

* [!DNL Dynamic Media] は、スマートイメージング (CQ-4222249) をサポートしています。

* クエリパラメーターが要求で渡された場合、検索または参照ビューが Foundation ピッカーのデフォルトビューとして設定される (NPR-31601)。

**安定性および**

* 一部のPDFドキュメントのメタデータが更新されず、タイトルが変更されてもPDFに保存されない (NPR-31629)。

* ファイル名にプラス文字 (`+`) が含まれるアセットでは、アセットの共有が機能しない。(NPR-31547)

* デフォルトの検索フォーム「アセット管理者の検索レール」での編集が期待どおりに機能しない (NPR-31502)。

* アセットビューでオムニサーチを使用してアセットを検索する場合、候補が表示されない。(NPR-31496)

* 同じアセットが別のユーザーによって別のコレクションで参照される場合、参照先のアセットが別の場所に移動されても、コレクション内のアセット参照は更新されない。(NPR-31486)

* 重複した IPTC タグがアセットメタデータに追加される (NPR-31328)。

* フィルターレールから検索がトリガーされた場合、検索結果カウントが正確に更新されない (NPR-31316)。

* ファイルタイプフィルターで第 2 レベルのチェックボックスの選択を解除すると、すべてのチェックボックスがオフになり、検索バーのテキストが選択または選択解除されたプロパティと同期しない (NPR-31287)。

* すべてのメンバー（ユーザー/グループ）をフォルダーの「メンバー」セクションから削除することはできません。すべてのユーザーを削除しようとすると、ログインしたユーザーがリストに追加される (NPR-31171)。

* ファイル名にプラス記号 (`+`) が付いているアセットは削除できない (NPR-31162)。

* フォルダーを選択する際にトップメニューに表示される「作成」ドロップダウンメニューが、作成オプションとして「フォルダー」を表示しない (NPR-30877)。

* パスの ACL がユーザーに適用されている場合、作成/FileUpload アクション項目が見つからない (NPR-30840)。`jcr:removeChildNodes``jcr:removeNode`

* 特定の mp4 アセットがアップロードされると、DAM ワークフローが古い状態になり、残りのすべてのワークフローが古い状態になる (NPR-30662)。

* メモリ不足エラーは、（数 GB の）大きなPDFファイルが DAM にアップロードされ、そのサブアセットが処理されると発生します (NPR-30614)。

* アセットの一括移動が失敗し、警告メッセージが表示される (NPR-30610)。

* [!DNL Dynamic Media]-Scene7モードで動作する [!DNL Experience Manager] で、アセットを別のフォルダーに移動する際に、アセット名を小文字に変更する (NPR-31630)。

* Scene7の会社名と同じ名前のフォルダーに存在する画像に関して、リモート画像セットの編集中にエラーが発生する (NPR-31340)。

* [!DNL Dynamic Media] 参照を含むアセットが公開されない (NPR-31180)。

* [!DNL Dynamic Media]7-Scene7モードから [!DNL Dynamic Media Classic] へのアップロードが完了するのに時間がかかりすぎる (NPR-31048)。

* 画像アセットに追加されたホットスポットが、アセットの詳細ページのインタラクティブ画像ビューアに表示されない。(NPR-30979)

* [!DNL Experience manager Assets] 内のアセットに対して実行されたアクションがScene7に渡されると、巨大な Sling ジョブが作成され、処理バナーが再び表示される。(NPR-30947)

* アセットの言語コピーの作成時に競合が発生し、アセットがScene7にアップロードされない。(NPR-30932)

* [!DNL Dynamic Media] — ハイブリッドモードで実行される [!DNL Experience Manager] からダウンロードされた動的レンディションが壊れる（画像コンテンツタイプではなく、コンテンツが「画像が見つかりません」というテキストタイプのレンディション）(NPR-30876)。

* [!DNL Dynamic Media] Adobe Experience Managerで、から —Scene7モードに移行されたビデオのサムネールの生成に失敗しま [!DNL Dynamic Media Classic] す ( [!DNL Dynamic Media]CQ-4282011)。

* 別のScene7会社 ID を使用して、あるインスタンスから別のインスタンスにアセットを移行する際に IpsApiException が発生していた問題を修正しました (CQ-4280548)。

* サポートされている 3D モデルが [!DNL Experience Manager] に取り込まれる場合、3D アセットのサムネールは情報を提供しません (CQ-4283701)。

* 3D アセットのカメラビューが少ない場合、スクロールボタンがビューアに表示されます (CQ-4283322)。

* アセットの詳細ページの DimensionalViewer でプレビューされた、アップロードされた 3D モデルのコンテナの高さが正しくありません (CQ-4283309)。

* Internet Explorer 11 および Safari では、SmartCropVideoViewer でビデオを再生できません (CQ-4281422)。

* [!DNL Dynamic Media]-Scene7実行モードで実行されている [!DNL Experience Manager] で、複数のアセットを別のフォルダーに移動するための移動ボタンの使用が失敗する (CQ-4280384)。

* MIME タイプが MP4 以外の場合に、アセットの詳細でビデオがゆがんで表示される (CQ-4279704)。

* ビデオプロファイルを持つフォルダーに新しく取り込んだビデオは、エンコードの割合が 100%に達した後も処理状態のままです (CQ-4279389)。

* フォルダーからアセットを移動すると、理想的に必要な数よりも多くの Sling ジョブ (Scene7 API 呼び出し ) が作成されます (CQ-4278664)。

* DAM で画像セット（またはメディアセット）が作成され、適切な命名規則で名前が付けられている場合、画像セットの名前がScene7で小文字に変更されます (CQ-4281112)。

* Scene7 Migrator が誤ってパブリッシュ状態を設定する (CQ-4263492)。

* （オムニサーチを通じて）タッチ UI 検索を実行すると、結果ページが自動的に上にスクロールし、コンテンツフラグメント内でのユーザーのスクロール位置が失われます (CQ-4282898)。

* PDFファイルのインデックスが作成されず、内のコンテンツを検索できない (CQ-4278916)。

* エラー「グループがユーザーピッカーに表示されません：異なる `principalName` と `authorizableId` を持つ閉じられたユーザーグループを追加すると、「false が true になる」と予期されていました (CQ-4278177)。

* Assets UI の列表示に、特定のテナントの DAM ルートパスに関係なく、すべてのパスが表示されます (CQ-4278175)。

* アセットセレクターの検索が期待どおりに機能しない (CQ-4275886)。

* レンディションワークフローが失敗する (CQ-4271928)。

* DAM イベントのパージは、最新の (`maxSavedActivities`) イベントデータを削除し、前に作成したデータを保持します (NPR-31336)。

* タッチ UI 検索（オムニサーチを通じて実行）の結果ページが自動的にスクロールアップし、ユーザーのスクロール位置が失われる (NPR-31307)。

* タッチ UI ですべてを選択した後、一部の項目（フォルダー/個々のアセット）の選択を解除したときに、アクションバーとアセット数が更新されない。(NPR-31118)

* アセットのジョブの詳細をポーリングする際に、[!DNL Experience Manager] に例外が表示されます (CQ-4283569)。

### Sites

* ライブコピーの継承が壊れている場合、ライブコピーページには、ライブコピーリンクではなく言語コピーリンクが表示される。(NPR-30980)
* 新しいブループリントの場合、レコード数が 40 を超える場合、最初の 40 個のレコードのみが表示されます。 ブループリントに残りのレコードの空白行が表示される (NPR-31182)。
* ユーザーがメニューの description プロパティに日本語または韓国語の文字を追加すると、メニューに日本語および韓国語のテキストに対して歪んだ文字が表示される (NPR-31331)。
* リッチテキストエディター (RTE) では、埋め込まれたテーブルをリスト項目として挿入できません (NPR-30879)。
* 標準で、リッチテキストエディター (RTE) の基礎モード。 予期せず、インラインフォントサイズを要素に適用する (NPR-31284)。
* 左パネルフィールドにフォーカスし、キーボードショートカットを使用してコンテンツをペーストすると、左パネルフィールドからコピーされたコンテンツではなく、ページエディターのクリップボードのコンテンツがペーストされる。（NPR-31172）
* ユーザーがファイルのアップロードフィールドをマルチフィールドに追加すると、画像パスは、マルチフィールドノードではなく、コンポーネントノードに格納されます (NPR-30882)。
* `ResponsiveGridExporter` API は `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` インターフェイスを返しません。 `com.day.cq.wcm.foundation.model.impl` パッケージがプライベートパッケージとして宣言される (NPR-31398)。

<!-- Review: NPR-31398 has fixVersion as 6530. However, it is mentioned twice in 6530 and 6520 as fixed. 
Remove one mention of this fix.
-->

* 一部のエクスペリエンスフラグメントを含むページがエディター以外のモードで（`editor.html` プレフィックスと `wcmmode=disabled` のないオーサーモードまたはパブリッシャーモードで）開かれると、リクエストは HTTP ステータスエラーコード `500` で終了します (NPR-30743)。
* ユーザーはパスワードを変更してプロファイルページにアクセスできない (NPR-31161)。

### 検索とユーザーインターフェイス {#ui-interface-and-search}

* カード表示から検索結果ページのリスト表示に切り替えると、ページをスクロールできるまでに遅れが生じる (NPR-31286)。

* [!UICONTROL 「すべて ] を選択」チェックボックスが、[!DNL Sites] ユーザーインターフェイスのリスト表示で非表示になっている (NPR-31614)。

* 検索結果ページの [!UICONTROL Select All] カウントが正しくない (NPR-31120)。

* メタデータエディターに、存在しないタグが表示される (NPR-31119)。

### 翻訳 {#translation}

* 翻訳ジョブの「期限」オプションを選択すると、2 つのカレンダーポップアップが表示される。(NPR-31270)

### Platform

* Web コンソールの「MIME タイプ」オプションが機能しない (NPR-31108)。

* シングルサインオンを設定する際に、クライアント証明書が受け入れられない (NPR-31165)。

* Jetty ベースの HTTP サービスのバッファーサイズ設定でアップデートが保存されない。（NPR-30925）

* QueryBuilder で、xpath クエリで orderby `fn:name()` がサポートされるようになりました (NPR-31322)。

* [!DNL Experience Manager] 6.3 からのアップグレード時に、重複したアクティベーションツリーが作成される (NPR-31513)。

* 転送された要求は、Sling 認証中に設定された応答ヘッダーを保持しない (NPR-30013)。

* ピッカーコンポーネント内の検索が機能しない (NPR-31692)。

* Apache POI と Apache Tika バンドルのバージョンが異なるため、ZIP ファイルを [!DNL Experience Manager Communities] の投稿に添付するとエラーが表示される (NPR-31018)。

* `org.apache.sling.distribution.api` バンドルは設定マネージャーで非表示になっているので、カスタムバンドルでは使用できません (NPR-31720)。

### プロジェクト

* カレンダービューの切り替えが機能しない (NPR-31271)。

### Brand Portal {#assets-brand-portal-6530}

**製品の機能強化**

* [!DNL Experience Manager Assets] のアセットソーシングの読み込みワークフローが変更され、新しく作成されたアセットのみが [!DNL Brand Portal] から [!DNL Experience Manager] に取得され、レプリケーションを避けるために、NEW フォルダーに既に存在するアセットをスキップします (CQ-4278527)。

**安定性および**

* アセットソーシング機能で新しい投稿フォルダーを作成すると、誤ったアイコンが表示されます (CQ-4282825)。
* 新しい投稿フォルダーを作成すると、1 つまたは両方のサブフォルダー（NEW と SHARED）が投稿フォルダー内に表示されません (CQ-4282424)。
* ユーザーが投稿フォルダーの新しいアセットを [!DNL Brand Portal] 側から受け取った後で、 [!DNL Experience Manager] から [!DNL Brand Portal] に投稿フォルダーを再公開しようとすると、例外がスローされます (CQ-4279740)。
* 投稿フォルダー（ネストされたフォルダー）内に投稿フォルダーを作成することは、複雑さを避けるために禁止されています (CQ-4278391)。
* [!DNL Experience Manager]Admin Consoleから読み込まれた [!DNL Brand Portal] ユーザーリスト（.csv ファイル）のアップロード時に例外が発生する。 .csv ファイルの「Email」、「FirstName」、「LastName」の各フィールドのみが必須です (CQ-4278390)。

### Communities {#communities-6530}

**安定性および**

* グループを管理するクイックリンク（グループを開く/編集/公開/削除）がコミュニティ管理者（グループ管理/サイト管理）に表示されない (NPR-31627)。
* 送信されたブログは、ページが手動で更新/再読み込みされない限り表示されない (NPR-31599)。
* 「メンション」機能で使用される JCR クエリでは大文字と小文字が区別され、結果を返すのに時間がかかりすぎる (NPR-31475)。
* [!DNL Experience Manager] 6.5 UberJar ファイルが例外をスロー `cq-social-translation` し、6.5 UberJar フ [!DNL Experience Manager] ァイルにバンドルが存在しない (NPR-31186)。
* Jackson Databind ライブラリが、新しい脆弱性に対処するためにバージョン 2.9.9.3 に更新されました (NPR-30967)。
* アクティビティと通知タイトルに一貫性がない。（NPR-30941）
* [!DNL Communities] ブログでページネーションが正しく機能しない (NPR-30914)。
* [!DNL Experience Manager] オーサー環境に Analytics レポートが入力されず、空白のページが表示される (NPR-30913)。

### Oak {#oak}

* Lucene のインデックスの更新により、オーサーサーバーの速度が低下する (NPR-31548)。

### Forms {#forms-6530}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack には、の修正が含まれていませ [!DNL Experience Manager Forms]ん。別の Forms アドオンパッケージを使用して配布されます。さらに、JEE 上の [!DNL Experience Manager Forms] の修正を含む累積インストーラーがリリースされました。 詳しくは、「 [Experience Manager Formsアドオンのインストール ](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 」および「 [JEE へのExperience Manager Formsのインストール ](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer) 」を参照してください。

#### Forms アドオンパッケージ {#forms-add-on-package-6530}

**アダプティブフォーム**

* 文字列には、アダプティブフォームのローカライズ時に辞書のキーが含まれます (NPR-31110)。

**インタラクティブコミュニケーション**

* **MissingNode.toString()** は、Jackson ライブラリを2.10.0にアップグレードした後、不正確な結果を返します (NPR-31549)。

* テキストエディターが、Microsoft Word からコピーしたテキストからスペース文字をランダムに削除する (NPR-31113)。

**Correspondence Management**

* LiveCycleES4SP1 から [!DNL Experience Manager] 6.5 へのレターの移行中に、キャプションとツールチップが表示されない (NPR-31615)。

* **レターをドラフトとして保存する** 際に、テキストフローの書式設定でサポートされるエラーメッセージが表示されなくなりました (NPR-30463)。

**ワークフロー**

* CPU 使用率 100%が原因で OSGi ワークフローが失敗する (NPR-31233)。

**HTML5 のフォーム**

* XDP フォームの HTML5 プレビューを生成すると、サブフォームのインスタンス追加中にちらつきが表示される。（NPR-30909）

#### Forms on JEE インストーラー {#forms-jee-installer-6530}

**Forms - ドキュメントサービス**

* .NET プロジェクトで MTOM を使用する SOAP Web サービスが、AssemblerServiceClient 呼び出しおよび HtmlToPDF2 メソッドの例外を表示する (NPR-4281771)。

* AXIS 1.4 jar で見つかったセキュリティ脆弱性 2012-5784 および 2014-3596 と、[AXIS1.4.1 jar](https://helpx.adobe.com/jp/aem-forms/quick-fixes/6-5/jee-patch-0014.html) で提供された修正 (NPR-31015)。

**Foundation JEE**

* アクションの設定が、「Forms Workflow送信アクションを呼び出す」のプロセス名を読み込まない。(NPR-31478)

### 含まれている機能パック {#feature-packs-included-6530}

>[!NOTE]
>
>[!DNL Experience Manager Forms] をご利用のお客様は、[!DNL Experience Manager] Service Pack、累積 Fix Pack、または機能パックをインストールした後に、[!DNL Experience Manager Forms] アドオンパッケージをインストールする必要があります。

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* [!DNL Experience Manager] FormsでのOracle18c のサポート (NPR-29155)。

## Adobe Experience Manager 6.5.2.0 {#experience-manager-6520}

[!DNL Adobe Experience Manager] 6.5.2.0 は、パフォーマンス、安定性、セキュリティ、お客様向けの主要な修正および 2019 年 4 月の [!DNL Adobe Experience Manager] 6.5 の一般リリース以降にリリースされた機能強化を含む重要なリリ **ースです**。[!DNL Experience Manager] 6.5 の上にインストールできます。

この Service Pack リリースの主な特徴は次のとおりです。

* 組み込み型のリポジトリ（Apache Jackrabbit Oak）をバージョン 1.10.3 に更新しました。
* [!DNL Adobe Target] のユーザー定義ワークスペースにエクスペリエンスフラグメントを直接書き出せるようにする設定プロパティが追加されました。
* Assets ユーザーは、視覚的に類似した画像を検索できます。[!DNL Experience Manager] は、ユーザーが選択した画像に類似した、DAM リポジトリのスマートタグ付き画像を表示します。[ビジュアル検索](../assets/search-assets.md#visualsearch)を参照してください。

* Connected Assets 機能が強化されて、リモート DAM デプロイメントからドキュメントを取得できるようになりました。サイト作成者は、サポートされているドキュメントタイプをコンテンツファインダーで検索およびフィルタリングできるようになりました。リモートドキュメントは、Web ページのダウンロードコンポーネントに追加できます。[Connected Assets の使用](../assets/use-assets-across-connected-assets-instances.md)を参照してください。

* 複数値のオプションをサポートする MIME タイプが増え、Document タイプフィルタが強化されました。
* 外部の再処理ワークフローが導入されて、複数のリソースがサポートされるようになりました。
* レプリケーションにデフォルトのアセットフィルターを使用して、[!DNL Dynamic Media] のパフォーマンスを最適化しました。
* DMS7（Dynamic Media Scene7）の切り抜きおよび回転のアセット編集オプションが復活しました。
* VideoPlayer で読み込み時にビデオをミュートするオプションが実装されました。
* アセット UI の列表示にテナント固有のコンテンツのみ表示されるように修正しました。
* スタイルアコーディオンの変更が検索結果に反映されるように修正しました。

### Assets

**製品の機能強化**

* Connected Assets 機能が強化されて、リモート DAM デプロイメントからドキュメントを取得できるようになりました。サイト作成者は、サポートされているドキュメントタイプをコンテンツファインダーで検索およびフィルタリングできるようになりました。リモートドキュメントは、Web ページのダウンロードコンポーネントに追加できます。CQ-4270245 のホットフィックス. [Connected Assets の使用](/help/assets/use-assets-across-connected-assets-instances.md)を参照してください。

* [!DNL Experience Manager Assets] ユーザーは、視覚的に類似した画像を検索できます。[!DNL Experience Manager] は、ユーザーが選択した画像に類似した、DAM リポジトリのスマートタグ付き画像を表示します。[ビジュアル検索](../assets/search-assets.md#visualsearch)を参照してください。

**安定性および**

* ACP API で生成された URL およびフォルダーメタデータのアセットパスが URL エンコードされません。GRANITE-26198：CQ-4271814 のホットフィックス
* 名前にパーセント記号 (%) が含まれるフォルダーを使用してアーカイブを解凍すると、[!DNL Experience Manager Assets] インターフェイスを使用して開くことができません。 NPR-29989：CQ-4270467 のホットフィックス
* タッチ操作対応 UI:公開を管理ウィザードでは、post リクエスト本文のページの後に参照が追加され、ページの後にすべてのアセットが公開され、ページがレンダリングされると、パブリッシュインスタンス内の一部のアセットが失われます。 NPR-29985：CQ-4270724 のホットフィックス
* 名前に特殊文字（URI エンコードされる文字）を含む関連アセットに対して、アセットの関連付け解除機能が機能しません。NPR-30387：CQ-4274446 のホットフィックス
* コンテンツフラグメントを編集すると、間違ったユーザーでバージョンが作成されます。
* テナントベースのシステムで、コレクションの作成が途中で失敗します。NPR-30114：CQ-4272948 のホットフィックス
* アセット UI の列表示が現在のテナントの DAM ルートパスを無視して、すべてのテナント DAM パスにアクセスします。NPR-30636：CQ-4275481 のホットフィックス
* 挿入された画像を表示できてしまうので、制限されているファイルに対する警告ウィンドウ経由で、クロスサイトスクリプティング（XSS）攻撃を受ける可能性があります。NPR-30617：CQ-4270133 のホットフィックス
* マルチテナント：フォルダープロパティを保存するテナントは、成功プロンプトとエラーメッセージの両方を観察し、アクションが正常に実行されなかったことを示します。「プロパティを編集できません。権限が不十分です。」 ので、紛らわしくなります。NPR-30545：CQ-4275333 のホットフィックス
* アセットセレクターダイアログでアセットを選択できないので、関連ソース置換機能を使用してソースを更新できません。NPR-30502：CQ-4275029 のホットフィックス
* [!UICONTROL DAM アセット] ワークフローの更新 — 大きなサイズの mp4 ファイルのアップロード時に古い状態。NPR-30480：CQ-4271352 のホットフィックス
* ペイロードが空の場合、「レビュータスクを作成」機能が機能しないので、後続のレビュータスク関連アクションがすべて失敗します。NPR-30468：CQ-4274263 のホットフィックス
* Datapower によって Adobe スマートタグの接続に関する問題が発生する。NPR-30026：CQ-4269457 のホットフィックス
* Assets UI の列表示で、レールに残ったフィルターを開こうとするとエラーが発生します。NPR-30501：CQ-4273862 のホットフィックス
* アセットフォルダーの非公開のユーザーグループ（CUG）プロパティに LDAP から同期されたグループを追加した場合、グループの保存や取得がおこなわれません。NPR-30615：CQ-4274689 のホットフィックス
* フィルターの検索スタイルおよび方向フィールドのオートコンプリート値が検索クエリに適用されません。NPR-30620：CQ-4275724 のホットフィックス
* 名前にスペースや「&amp;」文字が含まれるフォルダーのアセット共有リンクで、一部のアセットに対して空白の灰色カードが表示されます。NPR-30557：CQ-4270187 のホットフィックス
* フォルダーメタデータスキーマフォームでデータ型が自動的に検出されないので、フォーム送信で関連するタイプヒントが作成されません。NPR-30599：CQ-4275227 のホットフィックス
* DMS7 のオーサリング UI で切り抜きと回転のアセット編集オプションが無効になっています。NPR-30118：CQ-4273221 のホットフィックス
* DMS7 構成の [!DNL Experience Manager] インスタンスで共有リンク機能が機能しない。 NPR-30080、NPR-30492：CQ-4273651 のホットフィックス
* [!DNL Dynamic Media]-Scene7コンポーネントをページに追加してからページを公開しても、dmscene7 設定が毎回トリガーされるわけではありません。 NPR-30641：CQ-4275962 のホットフィックス
* [!DNL Experience Manager] に IPSJobJournal を追加し、1 つの処理プロファイルにつき IPS(Intrusion Prevention Systems) ジョブを 1 つだけ作成しました。 NPR-30490：CQ-4273614 のホットフィックス
* [!DNL Dynamic Media]:デフォルトのフィルターを追加し、アセットをパブリッシュノードにレプリケートしな [!DNL Experience Manager] いようにしました。NPR-30538：CQ-4274678 のホットフィックス
* 外部の再処理ワークフローが導入されて、複数のリソースがサポートされ、フォルダーをペイロードとして使用できるようになりました。ワークフローには 2 つのステップがあります。次のステップへのメタデータマップを通じてハンドルなしでアセットを再処理するステップと、単一の IPS ジョブですべてのアセットをアセットハンドルなしで S7 に再アップロードするステップです。詳しくは、「[!DNL Dynamic Media]Cloud Servicesの設定」を参照してください。 NPR-30489：CQ-4272903 のホットフィックス
* 正しい CSV の後に間違った CSV をアップロードすると、正しい CSV が消去されます。CQ-4277694、CQ-4277814 のホットフィックス
* 削除する投稿フォルダーに固有のアイコンが間違っています。CQ-4277580 のホットフィックス
* 「アセット投稿」タブのユーザーピッカーでユーザーを選択しても、ユーザーの名前がテーブルに表示されず、プロパティページのユーザーの削除ダイアログに間違ったテキストが表示されます。CQ-4277875 のホットフィックス
* ユーザーピッカーでユーザーを選択して「追加」をクリックしても、投稿者をアセット投稿フォルダーに追加できません。CQ-4277824、CQ-4278087 のホットフィックス
* ユーザーピッカーで小文字のユーザー名による検索が機能しません。CQ-4277958、CQ-4277930 のホットフィックス
* 管理者以外のユーザーでも、アセット投稿フォルダーの新しいフォルダーにアセットを公開できます。CQ-4278200 のホットフィックス
* 投稿者をアセット投稿フォルダーに追加するオプションが dam-user（管理者以外）にありません。CQ-4278192 のホットフィックス
* アセット投稿フォルダーに「作成」ボタンが表示されます。CQ-4277560 のホットフィックス
* 検索クエリを関連度順に並べ替えると、[!DNL InDesign] ドキュメントと [!DNL InDesign] テンプレートが返されます。 CQ-4273864 のホットフィックス
* ユーザーのメール ID が大文字の場合、以前にチェックアウトしたアセットをチェックインできません。CQ-4276575 のホットフィックス
* 削除操作は、選択されているプリセットにのみ適用され、操作後に画面上のリストが自動的に更新されると、既に更新されている他のプリセットが表示されます。CQ-4261461 のホットフィックス
* [!DNL Dynamic Media] — ハイブリッドモードで [!DNL Dynamic Media]Cloud Servicesを設定すると、[!DNL Analytics] に複数の空のレポートスイートが作成され、[!DNL Experience Manager] にレポートスイート ID が保存されないので、レポートスイートが重複します。 CQ-4249780 のホットフィックス
* [!DNL Experience Manager] アセットの名前を重複した名前に変更すると、Scene7と同期できません。 CQ-4276763 のホットフィックス
* ユーザー生成コンテンツが検索フィルターパネルに正しく表示されません。CQ-4273875 のホットフィックス
* 類似検索オプションが TIFF 画像に使用できません。CQ-4278238 のホットフィックス
* VideoPlayer で読み込み時にビデオをミュートするオプションが実装されました。CQ-4266465 のホットフィックス
* ビューア — VideoViewer:poster=none は、外部ビデオを使用した場合に正しく機能しません。 CQ-4265536 のホットフィックス
* IE11 および MS Edge ブラウザーでビデオ再生中に待機アイコンが表示されます。CQ-4251539 のホットフィックス
* 3.8 SDK および 5.13 ビューアの README ファイルは更新されず、以前のリリースの情報が含まれています。 CQ-4273737 のホットフィックス
* コンテンツフラグメントが、変更を保存する前でもバージョン管理されます。NPR-30616：CQ-4273088 のホットフィックス
* サムネール処理で Asset#getMetadata(String) が Asset#getMetadataValueFromJcr(String) に置き換わります。NPR-30491：CQ-4273067 のホットフィックス
* jpg をアップロードすると、「ReplicateOnModifyWorker Replicating UPDATED」というメッセージがアセットごとに複数回表示され、パフォーマンスが低下します。
* 「アーカイブを抽出」機能を使用して zip アーカイブを解凍すると、名前やタイトルにパーセント（％）が含まれるフォルダーで問題が発生します。NPR-29990：CQ-4270467 のホットフィックス

### Sites {#sites-6520}

* ライブコピーの継承が壊れている場合、ライブコピーページには、ライブコピーリンクではなく言語コピーリンクが表示される。(NPR-30980)
* 新しいブループリントの場合、レコード数が 40 を超えると、最初の 40 個のレコードのみが表示されます。 ブループリントに残りのレコードの空白行が表示される (NPR-31182)。
* テキストコンポーネントのリッチテキストエディター (RTE) プラグインが、日本語および韓国語テキストに歪んだ文字を表示する (NPR-31331)。
* リッチテキストエディター (RTE) では、埋め込まれたテーブルをリスト項目として挿入できません (NPR-30879)。
* 初期設定のリッチテキストエディター (RTE) が、予期せず要素にインラインフォントサイズを適用する (NPR-31284)。
* ユーザーが左側のレールフィールドにフォーカスし、キーボードショートカットを使用してコンテンツを貼り付けると、左側のレールフィールドからコピーしたコンテンツではなく、ページエディターのクリップボードのコンテンツを貼り付ける (NPR-31172)。
* ユーザーがファイルのアップロードフィールドをマルチフィールドに追加すると、画像パスは、マルチフィールドノードではなく、コンポーネントノードに格納されます (NPR-30882)。
* `ResponsiveGridExporter` API は `com.day.cq.wcm.foundation.model.impl.export.AllowedComponentsExporter` インターフェイスを返しません。 `com.day.cq.wcm.foundation.model.impl` パッケージがプライベートパッケージとして宣言される (NPR-31398)。
* 一部のエクスペリエンスフラグメントを含むページがエディター以外のモードで（`editor.html` プレフィックスと `wcmmode=disabled` のないオーサーモードまたはパブリッシャーモードで）開かれると、リクエストは HTTP ステータスエラーコード 500 で終了します (NPR-30743)。

### WCM - ページエディター {#wcm-page-editor-6520}

**製品の機能強化**

* `EnhanceDocument` 複数値のオプションをサポートする MIME タイプが多いタイプフィルター。CQ-4270694 のホットフィックス

### コンテンツフラグメント管理 {#content-fragment-management-6520}

* コンテンツフラグメントモデル UI で使用されるクエリが非常に遅く、最終的にエラーになります。CQ-4270807 のホットフィックス

### UI - 基盤 {#ui-foundation}

* 特定のユーザーインターフェイス内でユーザーが「m」、「p」、「e」を使用できないようにするショートカットトリガー。NPR-30355：Granite-26346 のホットフィックス
* [!DNL Experience Manager Assets] 検索 UI を閉じても、左側のレールが「コンテンツの選択」にリセットされず、ユーザーは 2 回目のフィルターレールの開きを妨げられます。 NPR-30509：CQ-4274716 のホットフィックス
* マルチテナント環境：[!DNL Experience Manager Assets] UI のトップナビゲーションが利用できず、JavaScript エラーが発生します。 NPR-30104：Granite-26344 のホットフィックス

### 翻訳 {#translation-6520}

* 翻訳の問題 - 機械翻訳を使用して翻訳されているコンポーネントはごくわずかです。NPR-30079：CQ-4273764 のホットフィックス

### Platform {#platform-6520}

* [!DNL Experience Manager] のデフォルトメール送信者が TLS v1.2 を介してリモート SMTP サーバーにメールを送信できません。NPR-30476：GRANITE-26605 のホットフィックス

### プロジェクト {#projects-6520}

* フォルダー内のアセットを削除した後でも、dam:folderThumbnailPaths 値が更新されず、古いサムネールが表示されます。NPR-30424：CQ-4273667 のホットフィックス
* 「移動」オプションを完了しても、アセットのタイトルと名前が元のまま変更されません。NPR-30647：CQ-4276265 のホットフィックス

### Communities {#communities-6520}

* ユーザー同期診断がまったく機能しません。NPR-30004、NPR-29943：CQ-4270287、CQ-4271348 のホットフィックス

### Sling {#sling}

* インスタンスを 6.3.3.2 から 6.5 にアップグレードすると、OSGi 設定が重複します。NPR-30130：CQ-4274016 のホットフィックス

### 統合

* パブリッシュインスタンスを再起動するまで、カスタマイズされたコンテンツがインスタンス上で正しく表示されません。NPR-30377：CQ-4273706 のホットフィックス
* Web サイトで Launch を設定すると、ライブラリアドレスの先頭にスラッシュ（/）が付加され、毎回手動の対応が必要になります。NPR-30694：CQ-4275501 のホットフィックス

### Forms {#forms-6520}

>[!NOTE]
>
>[!DNL Experience Manager] Service Pack には、の修正が含まれていませ [!DNL Experience Manager Forms]ん。別の [!DNL Forms] アドオンパッケージを使用して配信されます。 さらに、JEE 上の [!DNL Experience Manager Forms] の修正を含む累積インストーラーがリリースされました。 詳しくは、「 [Experience Manager Formsアドオンのインストール ](/help/release-notes/sp-release-notes.md#install-aem-forms-add-on-package) 」および「 [JEE へのExperience Manager Formsのインストール ](/help/release-notes/sp-release-notes.md#install-aem-forms-jee-installer) 」を参照してください。

[!DNL Experience Manager] 6.5.2.0 フォームの主な特徴は次のとおりです。

* [!DNL Experience Manager] Forms OSGi 用の `PDFFormRenderOptions` API の `RenderAtClient` に「自動」設定を追加しました。

#### Forms アドオンパッケージ

**バックエンドの統合**

* AWS ホスト型負荷分散 URL を使用してフォームデータモデルを設定できません。NPR-30123：CQ-4273359 のホットフィックス
* Web Service Definition Language(WSDL) を使用してフォームデータモデル (FDM) を作成すると、次のエラーメッセージ `Caused by: com.adobe.aem.dermis.exception.DermisException: java.lang.Exception: Unable to handle content type` が返されます。NPR-30477:CQ-4272921のホットフィックス

**Correspondence Management**

* 「通信作成 UI(CCR UI) レンディションが断続的に失敗し、コンソールに次のエラーが表示される：
   `- Uncaught Error: variable [object Object]is already known the letter`- NPR-30127

**インタラクティブコミュニケーション**

* フォームデータモデルで必須とマークされたフィールドが、「通信を作成」UI（CCR UI）で必要に応じて表示されます。NPR-30623：CQ-4274902 のホットフィックス

**Forms - ワークフロー**

* 監視フォルダーのマッピングされていない出力変数が原因で、呼び出しが失敗します。CQ-4264451 のホットフィックス

**HTML5 のフォーム**

* カスタムコードまたはプロジェクトを 2 回目にデプロイすると、ページはレンダリングされず、次のエラーが発生します。

   `org.apache.sling.scripting.sightly.SightlyException.`

   NPR-30539：CQ-4272509 のホットフィックス

* 参照モードで NonVisual Desktop Access を使用して HTML5 フォームを読み取る場合、Chrome ブラウザーがフォームデザインの各スケーラブルベクターグラフィック（SVG）の前に「グラフィック」を読み取る。NPR-30449：CQ-4274732 のホットフィックス

#### Forms JEE インストーラー

**Forms - Document Security**

* タイムスタンプ付きの署名を適用すると、次のエラーで失敗します：ALC-DSC-003-000 : com.adobe.idp.dsc.DSCInvocationException : 呼び出しエラー。NPR-30820：CQ-4275852 のホットフィックス

**Forms - ドキュメントサービス**

* 「SubmitURL」にアンパサンド (&amp;) が含まれている場合、`renderpdf` サーブレットにPOST要求が行われると、解析エラーがログに記録されます。 NPR-30865：CQ-4278232 のホットフィックス

**Forms - Foundation JEE**

* HTMLtoPDF サービスは、JMX コンソールに maxReuseCount を表示しません。 NPR-30134、NPR-30304：CQ-4273763 のホットフィックス
* [!DNL Experience Manager Forms] Workbench から Web サービスを呼び出して Web サービス接続を追加または編集すると、次のエラーが発生します。ClassNotFoundException org.apache.axis.message.SOAPBodyElement. NPR-30105：CQ-4273217 のホットフィックス

### 含まれている機能パック

>[!NOTE]
>
>[!DNL Experience Manager Forms] をご利用のお客様は、[!DNL Experience Manager] Service Pack、累積 Fix Pack、または機能パックをインストールした後に、[!DNL Experience Manager Forms] アドオンパッケージをインストールする必要があります。

#### Sites {#sites-feature-packs-included}

* [!DNL Adobe Target] のユーザー定義ワークスペースにエクスペリエンスフラグメントを直接書き出せるようにする設定プロパティが追加されました。 NPR-29189：CQ-4249782 のホットフィックス

#### Forms - ドキュメントサービス {#forms-document-services-1}

* [!DNL Experience Manager Forms] OSGi 用の `PDFFormRenderOptions` API の `RenderAtClient` に「自動」設定を追加しました。 NPR-30759：CQ-4278193 のホットフィックス

## Adobe Experience Manager 6.5.1.0 {#experience-manager-6510}

[!DNL Adobe Experience Manager] 6.5.1.0 は、パフォーマンス、安定性、セキュリティ、お客様向けの主要な修正および 2019 年 4 月の [!DNL Adobe Experience Manager] 6.5 の一般リリース以降にリリースされた機能強化を含む重要なリリ *ースです。* 6.5 の上にインストー [!DNL Experience Manager] ルできます。

この Service Pack リリースの主な特徴は次のとおりです。

* 追跡イベントに dynamic-UI-state をカスタム属性として含めることが可能になりました。
* [!DNL Dynamic Media]-Scene7モードでの 360 度ビデオアセットの配信のサポートが含まれました。
* リッチテキストエディターのスタイルプラグインを使用して、*日本語のワードラップ* 機能を有効にしました。 詳しくは、[ 日本語のワードラップの設定 ](/help/sites-administering/configure-rich-text-editor-plug-ins.md#jpwordwrap) を参照してください。

### Assets

* DAM DMGateway インターフェイスが更新されて、S3 マルチパートがサポートされるようになりました。NPR-29740：CQ-4226303 のホットフィックス
* [!DNL Experience Manager] 6.5 にアップグレードした後、レンディションプレビューが `Only empty tenantId is currently supported` エラーを生成する。NPR-29986:CQ-4272353のホットフィックス
* ジョブの削除を許可する削除ダイアログが表示されません。NPR-29720：CQ-4271074 のホットフィックス
* プロパティページにアセットタイトルを追加した後、ユーザーがページを閉じようとすると、[!DNL Experience Manager] によってプロパティページが再び開きます。 NPR-29627：CQ-4264929 のホットフィックス
* VersioningTimelineEventProvider は、nt:version タイプのノードと共にルートバージョンを提供する必要があります。GRANITE-26063 のホットフィックス
* DM-Scene7モードで 360 個の球形ビデオをアップロードして再生する機能を実装しました。 [!DNL Experience Manager]CQ-4265131 のホットフィックス
* ソースが編集されている場合、ライブコピーが間違ったステータスを取得します。CQ-4265451 のホットフィックス
* [!DNL Experience Manager Assets] に対するマルチサイトマネージャのサポートを有効にしました。 CQ-4271453、CQ-4268621、CQ-4257491 のホットフィックス
* [!DNL Experience Manager] インターフェイスには、現在のバージョンのアセットの追加エントリがタイムライン履歴に表示され、の最新のチェックインコメントが表示されま [!DNL Adobe Asset Link]す。CQ-4262864 のホットフィックス
* プロパティがない場合、コンテンツフラグメントタイムラインにエラーメッセージが表示されます。 CQ-4272560 のホットフィックス
* Scene 7 ビデオプレーヤーで全画面表示に拡大すると問題が発生します。CQ-4266700 のホットフィックス
* ZoomVerticalViewer：使用されている画像アセットが 1 つだけの場合に、パンボタンが表示されることがあります。CQ-4264795 のホットフィックス
* ライブコピーの子ノードを削除すると、liveRelationship の接続が解除される必要があります。CQ-4270395 のホットフィックス
* メタデータスキーマにグローバル設定のアイテムのみが含まれ、アクティブテナントのアイテムが欠落しています。URL の formPath 値が変更されても、デフォルト値に戻ります。NPR-29945：CQ-4262898 のホットフィックス
* [!DNL Brand Portal] に画像プリセットを公開すると、エラーコード 500 で失敗します。 NPR-29510：CQ-4268659 のホットフィックス

### Sites

* ロールアウト時に空のプロパティと複数のプロパティがブループリントから伝播されません。ブループリントを使用したライブコピーのリセットは、コンポーネントでは機能しません。NPR-29253：CQ-4264928、CQ-4264926、CQ-4267722 のホットフィックス
* CoralUI を `Multifield` と共に使用すると、`fileReferenceParameter` がマルチフィールドレベルではなくコンポーネントレベルに保存されます。 NPR-29537：CQ-4266129 のホットフィックス
* [!DNL Experience Manager] テキストコンポーネントとテキストエディターの日本語への機能強化。 NPR-29785：CQ-4265090 のホットフィックス
* タイムワープで復元されたページは、バージョン管理時に正しい画像を参照する必要があります。NPR-29431：CQ-4262638 のホットフィックス
* 親から子へのスタイルシステムノードの継承に関する問題。 NPR-29516：CQ-4270330 のホットフィックス
* [!DNL Facebook] 認証へのソーシャル投稿の設定中にエラーメッセージが表示されます。 NPR-29211：CQ-4266630 のホットフィックス
* コンテンツフラグメントにレンダリングされたサムネールに、日時フィールドの内部カレンダー表現が表示されます。NPR-29531：CQ-4269362 のホットフィックス
* Coral2 実装で「権限」タブを開いても、ボタンが表示されません。CQ-4269419 のホットフィックス

### コマース

* e コマースの遅延コンテンツ移行を実行すると、ConstraintViolationException が発生します。NPR-29247：CQ-4264383 のホットフィックス

### コンテンツフラグメント管理

* ドル `($)` および開き括弧 `({)` を含むコンテンツフラグメントを開く際に、解析エラーが発生しました。 CQ-4270266 のホットフィックス

### エクスペリエンスフラグメント

* [!DNL Experience Manager] エクスペリエンスフラグメントを [!DNL Adobe Target] に書き出します。 CQ-4265469 のホットフィックス
* Target へのエクスペリエンスフラグメントの書き出しが、スマート画像で失敗する。 CQ-4269606 のホットフィックス

* カード表示で Omnisearch を通じてエクスペリエンスフラグメントを移動しようとすると、行き詰まります。CQ-4263848 のホットフィックス

### WCM - ページエディター

* 無効なセレクターを使用すると、クロスサイトスクリプティング（XSS）が反映されます。CQ-4270397 のホットフィックス

### レプリケーション

* `cq/replication/components/agent` コンポーネントの出力でユーザー提供のデータがエスケープされないので、保存されたクロスサイトスクリプティング（XSS）の脆弱性がある。CQ-4266263 のホットフィックス

### ワークフロー

* ダイアログ参加者のカレンダーピッカーフィールドが機能しません。NPR-29727：CQ-4270423 のホットフィックス

### WCM - SPA エディター

* 事前にレンダリングされたコンテンツをリモートエンドポイントから取得できるようになりました。CQ-4270238 のホットフィックス
* サーバー側でレンダリングされた SPA テンプレートページを開くと、ログに警告が記録されます。CQ-4270238 のホットフィックス

### WCM - MSM

* [!DNL Experience Manager] 6.4.3 にアップグレードすると、Multi-Site Manager の展開に時間がかかります。 CQ-4271410 のホットフィックス

### 統合

* BrightEdge 認証情報が失敗し、接続エラーが発生します。NPR-29168：CQ-4265872 のホットフィックス

* [!DNL Experience Manager] 起動設定を編集および保存しようとすると、例外メッセージが表示されます。 NPR-29176：CQ-4265782／CQ-4266153 のホットフィックス

### ユーザーインターフェイス

* Foundation の追跡 API で特定のイベントを追跡中に、dynamic-UI-state をカスタム属性として追跡できるようになりました。GRANITE-26283 のホットフィックス
* 送信ボタンに追跡機能を設定できません。GRANITE-26326 のホットフィックス
* ウィザードで、送信ボタンに追跡機能を設定できません。NPR-29995、NPR-30025：CQ-4264289 のホットフィックス

### Communities

* メンバープロフィールページのドロップダウンに新しいバッジを整列配置できません。NPR-29381：CQ-4267987 のホットフィックス
* モデレーター権限のない訪問者とメンバーが、URL を貼り付けて未承認または承認待ちの投稿を表示できます。NPR-29724：CQ-4271124、CQ-4271441 のホットフィックス
* コミュニティにユーザーがログインする際、応答時間が長くなり、最大 40〜50 秒かかる場合があります。NPR-29677：CQ-4269444 のホットフィックス

### レプリケーション

* レプリケーションエージェントコンポーネントは、権限のないユーザーに機密情報が開示される脆弱性の影響を受けやすくなっています。NPR-29611：Granite-25070 のホットフィックス

* [!DNL Brand Portal] へのレプリケーションごとに、OAuth 中のセッションリーク。 NPR-30001：Granite-26196 のホットフィックス

### プロジェクト

* [!DNL Experience Manager] オーサー/content/dam/mac フォルダーから [!DNL Brand Portal] に [!DNL Experience Manager Assets] を公開しても機能しません。 NPR-29819：CQ-4271118 のホットフィックス

### Platform

* キャッシュの無効化時に HtmlLibraryManager が crx-quickstart の内容をすべて削除します。NPR-29863：Granite-26197 のホットフィックス

### Felix

* Java11\を使用している場合、メモリ使用量の詳細はシステムコンソールに表示されません。 NPR-29669

### Forms

[!DNL Experience Manager Forms] 6.5.1.0 の主なハイライトは次のとおりです。

* OSGi のみ：Output とForms Service に新しい属性 `PAGECOUNT` が追加されました。

* OSGI のみ：Formsサービスを使用した静的PDFファイルの作成がサポートされました。
* 管理者およびルートユーザーに対して XMLForm.exe の権限が有効になりました。
* Dynamics オンプレミス統合で ADFS v3.0 がサポートされるようになりました。

#### Forms アドオンパッケージ

**バックエンド統合**

* 保護された Web サービス定義言語（WSDL）の取得に失敗します。NPR-29944：CQ-4270777 のホットフィックス
* [!DNL Experience Manager Forms] がIBM WebSphere にインストールされると、SOAP に基づくフォームデータモデルの作成に失敗します。 CQ-4251134 のホットフィックス
* Microsoft Dynamics オンプレミス統合で Active Directory Federation Services（ADFS）v3.0 がサポートされるようになりました。CQ-4270586 のホットフィックス
* データソースのタイトルが変更されても、更新されたタイトルがフォームデータモデルに表示されません。CQ-4265599 のホットフィックス
* エンティティまたは属性の名前にハイフンまたはスペースが含まれている場合、式はそのようなエンティティや属性を評価できません。 CQ-4225129 のホットフィックス

* プリミティブ文字列出力にコロンが存在する場合、誤った出力が見られます。 CQ-4260825 のホットフィックス

* REST API 出力からコンテンツが想定されない場合でも、フォームデータモデルの呼び出し操作でエラーが発生します。CQ-4268828 のホットフィックス

**アダプティブフォーム**

* 遅延読み込み中にアダプティブフォームフラグメントに新しいインスタンスを追加できません。NPR-29818：CQ-4269875 のホットフィックス
* 検証コンポーネントが「レコードのドキュメント」テンプレートのエラーを記録または表示しません。CQ-4272999 のホットフィックス
* アダプティブフォームのレイアウトエディターを無効にできるようになりました。CQ-4270810 のホットフィックス
* [!DNL Experience Manager] 6.5 でアダプティブFormsの検証手順を復元しました。CQ-4269583のホットフィックス

* アダプティブフォームフィールドの検証が失敗すると、[!DNL Adobe Sign] が壊れます。 CQ-4269463 のホットフィックス
* [!DNL Experience Manager Forms] インスタンスに 20 を超えるアダプティブフォームフラグメントがあり、すべてのフォームフラグメントの名前が同じ文字列で始まる場合、検索では、作成されたフラグメントは 1 つも返されないか、最近の 20 個しか返されません。 CQ-4264414、CQ-4264914 のホットフィックス

* サイズの大きいデータセットで Adaptive Formsアプリを使用する場合のパフォーマンスの問題。. CQ-4235310 のホットフィックス

* 匿名アカウントでパブリッシュインスタンスにアクセスすると、GuideRuntime スクリプトを読み込めません。CQ-4268679 のホットフィックス

**Forms - インタラクティブコミュニケーション**

* インタラクティブコミュニケーションテンプレートで、許可されたコンポーネントのリストにヘッダーおよびフッターコンポーネントが表示されません。CQ-4237895 のホットフィックス
* 画像フィールドを含んだインタラクティブコミュニケーション印刷テンプレートを作成すると、グラフのタイトルが空白に設定されます。CQ-4264772 のホットフィックス
* グラフの線の色が削除されると、未定義に設定されます。CQ-4264762 のホットフィックス
* 変更の同期を維持を実行すると、ドキュメントフラグメントで行われたレイアウトレイヤーの変更が消えます。 CQ-4266054 のホットフィックス
* テキストフィールドにバインドされたドキュメントフラグメント内部のフォームデータモデル要素で、継承アイコンが表示されずに、バインディングが可能になっています。CQ-4261089 のホットフィックス
* 印刷チャネルレンダリング API に、データを API のパラメーターとして渡すオプションがありません。CQ-4263540 のホットフィックス
* バインドの種類が「テキストフラグメント」から「なし/文字列フィールド/変数のデータモデルオブジェクト」に変更された場合、「エージェントで編集可能」チェックボックスがオフになっているので、エージェントの設定は表示されません。 CQ-4261953 のホットフィックス
* エージェント UI の送信時に、生成される Web データ JSON ファイルに、継承がキャンセルされた連結されていないフィールドの情報が格納されます。 CQ-4265621 のホットフィックス

**Forms - ワークフロー**

* アダプティブフォームアプリのアウトボックスからフォームを再送信すると、データが失われます。NPR-28345：CQ-4260929 のホットフィックス
* 非可変ケースの場合、保存中にドキュメントが閉じられません。CQ-4269784 のホットフィックス
* アダプティブフォームアプリでは、Microsoft Windows 8.1 のサポートを終了しました。CQ-4265274 のホットフィックス
* 2 MB を超える画像をフィールドレベルの添付ファイルとして Android 版の [!DNL Experience Manager Forms] アプリでフォームに添付すると、アプリがクラッシュします。 CQ-4265578 のホットフィックス

* タスクの割り当てでインタラクティブコミュニケーション印刷チャネルの事前入力オプションを有効にしました。CQ-4265577 のホットフィックス
* タスクの割り当て先グループのメンバーになるまで、共有タスクを表示できません。CQ-4248733 のホットフィックス
* Windows では、アダプティブフォームアプリでの JEE アプリケーションの保存または送信がブロックされます。CQ-4268704 のホットフィックス
* フォームデータモデル変数に関連付けられているフォームデータモデルが表示されません。CQ-4266554 のホットフィックス
* 変数サポートを使用したドキュメント署名のステータス変数がサポートされていません。CQ-4266312 のホットフィックス
* ウムラウト文字が含まれていると、ワークスペースからの送信に失敗します。CQ-4263172 のホットフィックス
* アップグレードされたセットアップで、ワークフローを編集用に開くと、監視フォルダーのユーザーインターフェイス（UI）にワークフロー名ではなくエラーが表示されます。CQ-4238579 のホットフィックス

**Forms - 管理**

* xsd または schema.json 以外の拡張子のファイルがアップロードされると、アップロードがおこなわれず、エラーメッセージも生成されません。CQ-4266716 のホットフィックス

**Forms - Correspondence Management**

* [!DNL Experience Manager Forms] 6.5 通信を作成 UI(CCR UI) で、6.3 で作成された通信を開けま [!DNL Experience Manager Forms] せん。CQ-4266392のホットフィックス
* DDE データ型が数値型の場合、XDP の Sum 関数が機能しません。CQ-4227403 のホットフィックス
* アセットの公開時にアセットの最終変更時刻が更新されないので、メモリ内キャッシュの無効化ロジックを更新する必要があります。CQ-4250465 のホットフィックス
* DD およびレターのドキュメントフラグメントを公開できません。CQ-4272893 のホットフィックス

#### Forms JEE インストーラー

**PDF Generator**

* 64 ビット JDK では CAD ファイルから PDF への変換が失敗します。NPR-29924、NPR-29925：CQ-4272113 のホットフィックス
* HTML から PDF への変換の名前が PhantomJS から WebToPDF に変わりました。NPR-29933：CQ-4234545 のホットフィックス
* zip ファイルを PDF に変換中にエラーが発生します。CQ-4268628 のホットフィックス

**Forms - Designer**

* [!DNL Experience Manager Forms Designer] を使用して作成された静的PDFで完全なアクセシビリティチェックが実行されると、プライマリ属性が見つからないため、言語言語チェックが失敗します。 CQ-4272923、CQ-4271002 のホットフィックス

**Forms - Document Security**

* ハードウェアセキュリティモジュール (HSM) を使用したデジタル署名が、Java 11 および Java 8\上の OSGi Linux で機能しない。 NPR-29838：CQ-4270441 のホットフィックス
* ハードウェアセキュリティモジュール（HSM）を使用したデジタル署名が、JEE Linux およびサポートされているすべてのアプリサーバー（JBoss および Websphere）で機能しません。NPR-29839：CQ-4266721 のホットフィックス
* PAdES（PDF Advanced Electronic Signatures）を使用して PDF の署名を検証すると、InvalidOperationException が発生します。NPR-29842：CQ-4244837 のホットフィックス
* Office 2019\の Document Security Extension サポートを追加しました。 CQ-4254369、CQ-4259764 のホットフィックス

**Forms - ドキュメントサービス**

* PDFは、PDF/A-1b とフォームフィールドの変換に Appearance Dict がない。 NPR-29940：CQ-4269618 のホットフィックス

* OSGi:レンダリング中に生成されたページ数を特定できません。 NPR-28922：CQ-4270870 のホットフィックス
* [!DNL Experience Manager Forms OSGi] のFormsサービスを使用した静的PDFファイルのサポートを有効にしました。 NPR-28572：CQ-4270869 のホットフィックス
* XMLForm.exe の権限を変更できません。NPR-29828、NPR-29237：CQ-4267080 のホットフィックス
* [!DNL Experience Manager Forms] サーバーの出力モジュールで作成された静的PDFは、作成されたドキュメントの言語で言語属性/タグを設定しません。 NPR-27332：CQ-4271002 のホットフィックス

**Forms - Foundation JEE**

* 最終成果物で pdfg_srt を使用できないと、インストーラーが失敗します。NPR-29854：CQ-4270137 のホットフィックス
* LCBackupMode.sh が機能しません。NPR-29840：CQ-4269424 のホットフィックス
* WebSphere のユーザーインターフェイス（UI）から UDP ポート参照を削除する必要があります。CQ-4264782 のホットフィックス

### 含まれている機能パック

#### Assets — 含まれる

* [!DNL Experience Manager Assets] に対するマルチサイトマネージャのサポートを有効にしました。 詳しくは、[MSM for Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/reuse-assets-using-msm.html) を使用したアセットの再利用を参照してください。 NPR-29199：CQ-4259922 のホットフィックス

#### Sites — 含まれる

* [!DNL Experience Manager] エクスペリエンスフラグメントを [!DNL Adobe Target] に書き出します。 詳しくは、[ エクスペリエンスフラグメントリンク書き換えプロバイダー —HTML](https://helpx.adobe.com/experience-manager/6-5/help/sites-developing/experience-fragments.html#TheExperienceFragmentLinkRewriterProviderHTML) を参照してください。 CQ-4265469 のホットフィックス

#### Forms - Document Services — 同梱

* OSGi のみ：Output とForms Service に新しい属性 PAGECOUNT が追加されました。 NPR-28922：CQ-4270870 のホットフィックス
* OSGi のみ：Formsサービスを使用した静的PDFファイルの作成がサポートされました。 NPR-28572：CQ-4270869 のホットフィックス
* 管理者およびルートユーザーに対して XMLForm.exe の権限が有効になりました。NPR-29237：CQ-4267080 のホットフィックス

### OSGi バンドルとコンテンツパッケージ

次のテキストドキュメントは、[!DNL Experience Manager] 6.5.1.0 に含まれている OSGi バンドルとコンテンツパッケージの一覧です

[!DNL Experience Manager] 6.5.1.0 に含まれている OSGi バンドルの一覧

[ファイルを入手](assets/6_5-bundle-list.txt)

[!DNL Experience Manager] 6.5.1.0 に含まれているコンテンツパッケージの一覧

[ファイルを入手](assets/6_5-content-package-list.txt)
