---
title: '[!DNL Experience Manager] 6.5 サービスパックリリースノート'
description: 固有のリリースノート [!DNL Adobe Experience Manager] 6.5 サービスパック 11
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: f2ccc77393e7fc1f53f9976076ec3c66c3f74189
workflow-type: tm+mt
source-wordcount: '3728'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] 6.5 サービスパックリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.11.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2021 年 11 月 25 日（PT） |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip) |

## に含まれるもの [!DNL Adobe Experience Manager] 6.5.11.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.11.0には、2019 年 4 月の 6.5 リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善が含まれています。 サービスパックがにインストールされている [!DNL Adobe Experience Manager] 6.5.

に導入された主な機能および機能強化 [!DNL Adobe Experience Manager] 6.5.11.0は次のとおりです。

* 複数行テキストデータタイプのマルチフィールドサポートを追加しました。

* ユーザーがバックグラウンドで現在実行中の非同期ジョブを認識し、同じパスで複数の非同期操作をトリガーしないようにする機能強化。

* SEO 用のサイトマップの自動生成は、 [SEO インデックスパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip). サイトマップ、代替 URL、ロボットメタタグなどを [!DNL Core Components].

* ユーザーエクスペリエンスが改善され、フォルダー内に存在するアセットの数が表示されます。1 つのフォルダー内のアセットが 1000 個を超える場合、[!DNL Assets] には「1000+」と表示されます。

* カード表示と列表示で並べ替えオプションをレンダリングできるようになりました。

* これで、 [!DNL Dynamic Media] を設定することで、 [!DNL Dynamic Media Classic] デスクトップアプリケーション。 詳しくは、 [Dynamic Mediaの一般設定](/help/assets/dm-general-settings.md).

* これで、 [!DNL Dynamic Media] を設定して、 [!DNL Dynamic Media Classic] デスクトップアプリケーション。 詳しくは、 [Dynamic Media Publish Setup の設定](/help/assets/dm-publish-settings.md).

* 組み込み型のリポジトリ (Apache Jackrabbit Oak) が1.22.9に更新されました。

以下は、 [!DNL Experience Manager] 6.5.11.0リリース。

### [!DNL Sites] {#sites-65110}

GraphQL を使用してコンテンツフラグメントを使用し、拡張されたコンテンツフラグメントモデルとエディター機能を使用してヘッドレスコンテンツ配信にアクセスするには、 [インデックス定義パッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.0.0.zip)、次の非同期AEMインデックス定義のインデックスを再作成します。

* /oak:index/assetPrefixNodename

* /oak:index/fragments

* /oak:index/graphqlConfig


以下の問題を修正しました。 [!DNL Sites]:

* コンテンツフラグメントを作成するためのテンプレートが、コンテンツフラグメントの作成時に表示されない (SITES-3365)。

* 正規表現および [!UICONTROL ユニーク] フィールドオプションがで機能しない [!UICONTROL appsUrl] モデルがコンテンツフラグメントエディター (SITES-1823) に反映されます。

* 設定は、 `/apps/system` をノードにする `/libs` 以前のサービスパック (SITES-3203) をインストールする場合。

* 以前のサービスパック (SITES-3151) のインストールで、コンテンツフラグメントを使用する機能が通常どおり機能しない。

* 並べ替えはでは機能しません [!UICONTROL コンテンツフラグメントモデル] コンソール (SITES-2722)。

* GraphiQL はモデル（スキーマ）を読み込んでいないので、エンドポイント JSON(SITES-2428) でエラーが発生しています。

* 列挙フィールドタイプ ( [!UICONTROL コンテンツフラグメントモデル] は、 [!UICONTROL コンテンツフラグメントモデルエディター] (SITES-2391)。

* タグのデータ型は、特定のデータ型 (SITES-2390) をサポートしていません。

* [!UICONTROL コンテンツフラグメント REST API] は、古いタグ値 (SITES-2386) を書き出しています。

* コンテンツフラグメントエディター (SITES-2341) でパンくずリストの矢印が正しく配置されない。

* 大きなデータセットでは、コンテンツフラグメント参照の検索が遅い (SITES-2147)。

* [!UICONTROL CopyUrl] オプションが [!UICONTROL コンテンツフラグメントエディター] (SITES-2007)。

* 関連するモデルと共にコンテンツフラグメントが公開され、モデルが制動の変更を導入した場合、警告は表示されません (SITES-1988)。

* コンテンツフラグメントモデルの URL 編集は、コンテンツフラグメントモデルの編集の使用例 (SITES-1980) によって異なります。

* インラインを使用して、同じタイトルを持つ 2 つのコンテンツフラグメントを作成する場合 [!UICONTROL 新しいコンテンツフラグメント] アクションを呼び出すと、ウィザードは同じフラグメントパスを返します (SITES-1978)。

* オートコンプリートが [!UICONTROL コンテンツフラグメントモデル] 検索ファセット (SITES-1976)

* コンテンツフラグメントにネストされたフラグメントの巨大な階層が含まれている場合、 [!UICONTROL コンテンツフラグメントエディター] サイドパネル (SITES-1974) を読み込むと、応答しなくなります。

* フラグメントピッカーパスのグローバル検索が機能しません (SITES-1973)。

* コンテンツフラグメントの移動時に参照が更新される (SITES-1897)。

* ページを作成するオプションがカード表示と列表示に表示されない (NPR-37549)。

* ローンチページ上のコンポーネントを並べ替える際に、ローンチの昇格時にコンポーネントの並べ替えが保持されない (NPR-37539)。

* リスト内のすべての項目を選択するオプションがロールアウトページで機能しない (NPR-37443)。

* 複数のページをスケジュールに沿ってアクティベートすると、 `wcm-workflow-service` ユーザー (NPR-37417)。

* サイトコンソールのフォルダーの移動操作が失敗し、「選択した項目のローンチ情報を取得できませんでした」というエラーメッセージが表示される (NPR-37340)。

* ブループリントのサムネールを生成し、ライブコピーにロールアウトする場合、ライブコピーのサムネール後のタブの継承が壊れる (NPR-37190)。

* ライブコピーを表示するフィルターの述語で、すべてのライブコピーが表示されない (NPR-37126)。

* レプリケーションイベントが、作成者でレプリケーションイベントハンドラーが呼び出されたときに、削除の対象としてマークされたすべての親ページと子ページのリストを返さない (NPR-37123)。

* 複数の値を持つプロパティをバルクエディターで保存する場合、コンマ区切りの文字列が配列の最初の要素として保存される (NPR-37089)。

* コンポーネントのレイアウトのサイズ変更がモバイルレイアウトで機能しない (NPR-37086)。

* ロールアウト設定を追加した後、ページプロパティを保存すると、ライブコピーレベルで新しいノードが誤って作成される (NPR-37084)。

* ユーザーは、新しいマスターページ (SITES-3442) のページプロパティを使用してライブコピーを作成したり、ロールアウトしたりできません。

* タグは、タイトルとクローズオプションの代わりにタグ名を表示しますが、プロパティレベルで継承がキャンセルされた場合に、タグプロパティが正しく機能しないため、タグが完全に削除されません (NPR-36831)。

* すべての項目の選択を解除するオプションが機能せず、ライブコピーのリストが表示されるページのテーブルの最初の行とヘッダーが重なる (NPR-37070)。

* ワークフローで使用されるカスタムダイアログで、ダイアログの検証を試みると、Experience Managerが失敗し、ブラウザーコンソールにエラーが表示されます (GRANITE-35049)。

では、次のアクセシビリティの強化が利用できます。 [!DNL Adobe Experience Manager Sites]:

* スクリーンリーダーで、 [!UICONTROL サイト参照] および [!UICONTROL 言語コピー] オプション (SITES-1791)。

* ブラウザーモードのフォーカスの順序が、ユーザーインターフェイスの様々なオプションで順番に移動するようになりました (SITES-1791)。

* スクリーンリーダーは、選択されたツリー項目が選択された状態であるかどうかを読み上げ、また、アクション領域が表示されたことをユーザーに通知するようになりました (SITES-2109)。

* スクリーンリーダーで、ページの選択フィルターまたは検索時に読み込みインジケーターが表示された場合に、読み込みが通知されるようになりました (SITES-1790)。

* スクリーンリーダーで、 [!UICONTROL フィルター] オプションの場合、左側のパネルに検索結果が返されない (SITES-1599)。

* 参照モードで移動する場合、スクリーンリーダーは、Enter キーが押されたときに、コンテンツページの役割と、ページの選択状態を読み上げる (SITES-1579)。

* 次の場合にスクリーンリーダーが読み上げられるようになりました [!UICONTROL メモ追加] オプションが選択されている (SITES-1573)。

* フォームフィールドにプレースホルダーとは別の視覚的なラベルが追加され、スクリーンリーダーユーザーがフィールド値の入力時に適切にガイドされるようになりました (SITES-1258)。

### [!DNL Assets] {#assets-65110}

では、次のアクセシビリティの強化が利用できます。 [!DNL Assets]:

* カード表示の [!DNL Assets] リポジトリ、使用時 `Tab` フォーカスをフォーカス時にクイックアクションを開く最初の項目に移動するためのキー。スクリーンリーダーは、フォーカスされた項目の名前を読み上げます。
* In [!DNL Dynamic Media] [!UICONTROL ビューアプリセットエディター]「シャドウの色」と「境界線の色」が存在しない場合、「無効」プロパティを使用して入力が無効になります。 キーボードユーザーが入力にフォーカスできず、スクリーンリーダーがコントロールの状態を無効と発表しない。
* In [!DNL Dynamic Media]新しいビデオエンコーディングプロファイルを作成するためのインターフェイスで、 [!UICONTROL スマート切り抜き率] オプションにはアクセシビリティのラベルが付いているので、スクリーンリーダーが適切に読み上げます。

* これで、 [!DNL Experience Manager Assets] キーボードを使用して。

以下の問題を修正しました。 [!DNL Assets]:

* コントリビューターグループのユーザーが DAM アセットリポジトリーに移動すると、例外として `POST` コレクションを作成するためのリクエストがトリガーされます。 この `POST` リクエストが失敗し、ログにエラーが反映される (NPR-37171)。

* ネストされたフォルダー構造を持つブループリントのライブコピーを作成する場合、ソースフォルダーの変更されたプロパティがライブコピーフォルダー内で更新されない (NPR-37449)。

* 複数のアセットを選択し、メタデータフィールドの値を変更する場合、アセットを保存しても値は保持されません。 また、メタデータの変更は適用されない (NPR-37341)。

* 複数のアセットを選択してプロパティを変更すると、カスタムプロパティ（ドロップダウン）の値がデフォルト値によって上書きされる (NPR-36437)。

* パンフレット、チラシおよびInDesignテンプレートに対して誤ったPDFレンディションが生成される (NPR-36433)。

* の保存 [!DNL Adobe Target] とのアクティビティ [!DNL Experience Manager] ターゲティングモードが失敗する場合、 [!DNL Adobe Analytics] レポート指標が参照される。(NPR-37167)

* 大文字と小文字が混在するドメイン名を使用して電子メールで送信されたユーザーがアセットをチェックアウトすると、そのアセットは、 [!DNL Asset Link] (CQ-4329266)。

<!-- Add 
* [!DNL Adobe Asset Link] is not able to access the digital assets even when the [!DNL Creative Cloud] and [!DNL Experience Management] entitlements are provided by two different organizations. -->

* ページにアップロード時に生成されたカスタムメタデータを含むビデオを追加すると、名前空間が登録されている場合でも、不明な名前空間に関するエラーが表示されます (CQ-4331471)。

* In [!DNL Assets]、 [!DNL Launcher] が無効になっている場合、手動でトリガーしたときにメタデータの書き戻しが機能しません (CQ-4329082)。

### [!DNL Dynamic Media] {#dynamic-media-65110}

以下のバグ修正が、 [!DNL Dynamic Media]:

* でアセットが更新されていません [!DNL Dynamic Media] でアセットのバージョンを復元する際 [!DNL Experience Manager] (NPR-37421)。

* 公開PDFファイルに ECatalog が公開されない (CQ-4329886)。

* コンポーネントが標準のプリセットを使用している場合に、公開したページを開くと 3D アセットが読み込まれない (CQ-4329205)。

* 大規模なPDFの場合のリポジトリアセット処理の問題 (CQ-4328711)。

* PDF処理エラーが [!DNL Experience Manager] ～で失敗した場合に [!DNL Scene7] (CQ-4331145)。

* ユーザーは、.MOV アセットのデフォルトのメタデータプロパティを表示できません (CQ-4332546)。

* .MXF ビデオファイルをにアップロードできません [!DNL Dynamic Media] using [!DNL Experience Manager] (CQ-4329709)。

* カスタム会社ルートが設定されている場合に、アップロードの問題が発生します (CQ-4332800)。

* In [!DNL Experience Manager] を含むカスタムランチャーの設定 `ActivationModel` ワークフローの際に、Experience Managerファイルのアップロード時のメモリの問題が原因でPDFがクラッシュします。 (CQ-4330512).

* でのパフォーマンスの問題 `DamEventRecorder` (CQ-4334072)。

* ショッパブルビデオのハイパーリンク (linked-URL) に特殊文字が含まれている場合、ターゲット URL はビューアによってエンコードされ、誤った製品ページとして表示されます (CQ-4331639)。

* ビデオプロファイルページで、ページの読み込み時にユーザーがビデオプロファイルを選択すると、ツールバーのオプションが消えます (CQ-4308521)。

* JCR 同時書き込みによる DM アセット処理の失敗 (CQ-4333489)。

* ユーザーのビデオプロファイルルートにビデオプロファイルのルートノードで定義されたカスタムアクセスポリシーがある場合、ビデオプロファイルページへのアクセスに失敗します (CQ-4332941)。

* ズーム可能な画像で、ショートカットキー (「+」、「 — 」) または「Esc」キーを使用すると、スクリーンリーダーのフォーカスがトラップされます (CQ-4290719)。

* ユーザーがフォームモードのショートカットキー (「F」) をクリックしても、スクリーンリーダーは [!UICONTROL 埋め込みサイズ] メニューボタン [!UICONTROL 埋め込みを取得] コードダイアログボックス (CQ-4290929) に表示されます。

* キーボードナビゲーションを使用して E メールリンクポップアップウィンドウを開く場合、「宛先」フィールドと「送信者」フィールドのユーザーインターフェイスに表示されるエラー候補は説明的ではありません (CQ-4290930)。

* E メールリンクダイアログボックスに移動する際、スクリーンリーダーが、下向き矢印とフォームモードのショートカットキー (「F」) を使用して、新しく追加された編集フィールドのラベル情報を読み上げない (CQ-4290934)。

* E メールリンクダイアログボックスに移動する際に、スクリーンリーダーに「宛先」および「送信者」必須フィールドの視覚的なアスタリスク (*) が反映されない (CQ-4290935)。

* ユーザーは、ショートカットキー (「D」、「R」) を使用してランドマークと領域を識別できません (CQ-4312118)。

<!-- Anuj to check if this section is required or not. We have an enh. in CIF area that is mentioned. It is added above and not part of this bug fix section.
-->

### コマース {#commerce-65110}

* を使用する場合、 [!UICONTROL 後で公開] オプションの場合、ユーザーインターフェイスにステータスが [!UICONTROL 公開保留中] (CQ-4334229)。

* フォルダーを非公開にしても、そのフォルダーの製品は完全に非公開にならず、公開者から製品が削除されますが、オーサーインスタンスにはまだ存在します (CQ-4332731)。

### Platform {#platform-65110}

* ユーザーが複数フィールドオプションの並べ替えアイコンをクリックすると、スクロールバーがユーザーインターフェイスに表示されなくなります (CQ-4331100)。

* アップグレード後、ユーザーがワークスペースログインコンテナコンポーネントを開くと、ダイアログボックスのヘッダーがユーザーインターフェイスに表示されなくなります (CQ-4316173)。

### 統合 {#integrations-65110}

* の保存 [!DNL Adobe Target] とのアクティビティ [!DNL Experience Manager] ターゲティングモードが失敗する場合、 [!DNL Adobe Analytics] レポート指標が参照される。(NPR-37167)

### プロジェクト {#projects-65110}

* からアップグレードする場合 [!DNL Experience Manager] 6.5.8.0 からバージョン 6.5.9.0 へのインストールは、のプロパティを上書きします。 `/content/dam/projects`. フォルダーの割り当て済みのメタデータスキーマとプロパティをデフォルトにリセットする (NPR-37124)。

### ユーザーインターフェイス {#user-interface-65110}

* モデルを表すフォルダーアイコンが正しくない (NPR-37176)。

* ユーザーがパスフィールドブラウザーを使用して検索または閲覧を実行すると、誤ったノードが表示される (NPR-37175)。

* パブリッシュインスタンスでは、受信リクエストが数分間ブロックされる (NPR-37169)。

* カスタムワークフローのダイアログボックスで multifield プロパティを追加すると、ダイアログボックスの処理に失敗し、ユーザーがダイアログボックスを閉じることができない (NPR-37075)。

### 翻訳プロジェクト {#translation-65110}

* 翻訳ローンチの自動昇格が例外で失敗する (NPR-37528)。

* エクスペリエンスフラグメントの翻訳が、URL の言語コピーの参照を更新しない (NPR-37522)。

* 言語ルート構造のパスと一致しないパスにエクスペリエンスフラグメントが作成された場合、そのページを翻訳プロジェクトに追加すると、空白のエラーメッセージが表示される (NPR-37425)。

* エクスペリエンスフラグメントを含むページ（英語）が変更され、翻訳用に送信されると、翻訳済みのエクスペリエンスフラグメントが英語コンテンツで上書きされます (NPR-37283)。

* 翻訳プロバイダーフィルターが適切に機能しない (NPR-37186)。

* エクスペリエンスフラグメントとアコーディオンコンポーネントが、サンプルサイトコンテンツ用に標準で翻訳されない (NPR-37170)。

* へのアップグレード後 [!DNL Experience Manager] 6.5.9.0 では、翻訳プロジェクトにページを追加すると、空のエラーメッセージが表示される (NPR-37105)。

* ローンチ内でページを追加する場合、類似の名前を持つ翻訳ページがプロジェクトに含まれません (NPR-37082)。

* トランスレーターインターフェイスを使用してフォーム辞書を.xliff ファイルとして書き出す場合、書き出されたファイルのフィールド順序が正しくない (NPR-37048)。

* 翻訳プロジェクトから親ページをロールアウトすると、言語固有の子ページが削除される (NPR-36998)。

* 翻訳プロジェクトを作成する際に、ページを循環的に参照することでローンチがトリガーし、エラーが発生します (CQ-4332982)。

* 翻訳されたエクスペリエンスフラグメントとページ内のエクスペリエンスフラグメントリンクに、ローンチ参照が含まれる。(NPR-37649)

### Sling {#sling-65110}

* 新しいパッケージをアップロードすると、MapEntries マップ内のメモリエイリアスが削除される (NPR-37067)。

### ワークフロー {#workflow-65110}

* `Deactivate` メソッド `InboxOmniSearchHandler` ヌルポインタ例外を表示する (NPR-37533)。

### [!DNL Communities] {#communities-65110}

* ユーザーがページ、 `Post` 操作が失敗し、エラーコード 500 が表示される (NPR-37156)。

* アプリケーションをデプロイする際に、SyncManager の長時間の実行セッションが原因で、セグメントが見つからない例外が発生する。(NPR-37351)

* ユーザーがフォーラムディスカッション投稿でスレッドの返信を表示できない。(NPR-37083)




<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65110}

*

-->

### [!DNL Forms] {#forms-65110}


>[!NOTE]
>
>* [!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] サービスパックリリース日の 1 週間後にアドオンパッケージをリリースします。


**アダプティブフォーム**

* アクセシビリティ — `Wizard` アダプティブフォームのパネルのレイアウトで、ナビゲーションボタンに Aria のラベルと役割がない (NPR-37613)。

* アダプティブフォームの日付フィールドでの検証が、期待どおりに動作しない (NPR-37556)。

* チェックボックスコンポーネントとラジオボタンコンポーネントのラベルテキストが長い場合、テキストが適切に収まらない (NPR-37294)。

* AEM Formsコンテナコンポーネントの「ありがとうございます」メッセージにスタイル設定の変更を適用した場合、その変更がソースアダプティブフォームに複製されない (NPR-37284)。

* の値の違い `Switch` ユーザーインターフェイスおよびバックエンドのコンポーネント (NPR-37268)。

* キーボードキーを使用して `Submit` オプションを選択し、 `Enter` キーを押すと、アダプティブフォームを複数回送信できます (CQ-4333993)。

* 添付ファイルコンポーネントの削除操作が期待どおりに動作しない (NPR-37376)。

* 各種言語に変換されるアダプティブフォームで、フィールドのラベルが 1,000 文字を超えると、辞書はラベルの翻訳を取得できません (CQ-4329290)。

**ドキュメントサービス**

* Assembler サービスの使用中にエラーが表示される (NPR-37606)。

   ```TXT
     500 Internal Server Error
   ```

* ドキュメントの添付ファイルが Assembler サービスに渡されると、次の例外が表示される (NPR-37582)。

   ```TXT
     com.adobe.livecycle.assembler.client.ProcessingException: ⁪: Failed to execute the DDX
   ```

* PDFドキュメントをPDFA/1BPDFドキュメントに変換した後、データから閉じ丸括弧が欠落する (NPR-37608)。

**HTML5 のフォーム**

* AEM 6.5.10.0をインストールすると、XDP フォームのHTMLプレビューが機能しない (NPR-37503、CQ-4331926)。

* 様々な言語でPDF formsをHTML5 フォームに移行する際に、テキストが重なる問題が発生する (NPR-37173)。

**レター**

* レターを送信し、HTMLビューで再度開くと、テキストドキュメントフラグメントの位置が変わる (NPR-37307)。

**Forms のワークフロー**

* 埋め込みコンテナワークフローの場合、 `Notify on Complete of Container Workflow` オプション (NPR-37280)。

**Foundation JEE**

* AEM 6.5 Forms Service Pack 9 のインストール後、CRX リポジトリの URL は使用できなくなります (NPR-37592)。


セキュリティ更新について詳しくは、 [[!DNL Experience Manager] セキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html).

## 6.5.11.0 のインストール {#install}

**設定要件と詳細情報**

* Experience Manager6.5.11.0にはExperience Manager6.5 が必要です。 [アップグレードドキュメント](/help/sites-deploying/upgrade.md) を参照してください。
* サービスパックのダウンロードは、Adobeで利用できます [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* MongoDB および複数のインスタンスを使用するデプロイメントで、パッケージマネージャーを使用して、いずれかのオーサーインスタンスにExperience Manager6.5.11.0をインストールします。

>[!NOTE]
>
>Adobeは、 [!DNL Adobe Experience Manager] 6.5.11.0パッケージ。

### サービスパックのインストール {#install-service-pack}

に Service Pack をインストールするには [!DNL Adobe Experience Manager] 6.5 インスタンスを使用するには、次の手順に従います。

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 Adobeでは、インスタンスの現在の稼動時間が長い場合に再起動を推奨します。

1. インストールする前に、スナップショットまたは新しいバックアップを作成します [!DNL Experience Manager] インスタンス。

1. 次の場所からサービスパックをダウンロードします。 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip).

1. パッケージマネージャーを開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。詳しくは、 [パッケージマネージャー](/help/sites-administering/package-manager.md).

1. パッケージを選択し、 **[!UICONTROL インストール]**.

1. S3 コネクタを更新するには、Service Pack のインストール後にインスタンスを停止し、既存のコネクタを install フォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。 詳しくは、 [Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。 Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを保証します。 通常、この問題は [!DNL Safari] ブラウザーは断続的に使用されますが、どのブラウザーでも発生する場合があります。

**自動インストール**

を自動的にインストールするには、次の 2 つの方法があります [!DNL Experience Manager] 6.5.11.0（作業中のインスタンス）:

A.パッケージをに配置します。 `../crx-quickstart/install` フォルダー（サーバーがオンラインで使用可能な場合） パッケージが自動的にインストールされます。

B. [パッケージマネージャーからの HTTP API](/help/sites-administering/package-manager.md#package-share). 用途 `cmd=install&recursive=true` ネストされたパッケージがインストールされるようにする。

>[!NOTE]
>
>Adobe Experience Manager 6.5.11.0では、Bootstrapのインストールはサポートされていません。

**インストールの検証**

1. 製品情報ページ (`/system/console/productinfo`) は、更新されたバージョン文字列を表示します `Adobe Experience Manager (6.5.11.0)` under [!UICONTROL インストール済み製品].

1. すべての OSGi バンドルは、 **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** OSGi コンソール (Web コンソールを使用： `/system/console/bundles`) をクリックします。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン1.22.3以降です (Web コンソールを使用： `/system/console/bundles`) をクリックします。

このリリースでの動作が認定されたプラットフォームについては、 [技術要件](/help/sites-deploying/technical-requirements.md).

<!-- 

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

Experience Manager6.5.11.0の UberJar は、 [Maven 中央リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.11/).

Maven プロジェクトで UberJar を使用するには、 [UberJar の使用方法](/help/sites-developing/ht-projects-maven.md) およびは、プロジェクト POM に次の依存関係を含めます。

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.11</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobeのパブリック Maven リポジトリ (`repo.adobe.com`) をクリックします。 メインの UberJar ファイルの名前がに変更されます。 `uber-jar-<version>.jar`. だから、 `classifier`を `apis` 値として、 `dependency` タグを使用します。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

以下に、で非推奨とマークされた機能のリストを示します。 [!DNL Experience Manager] 6.5.7.0.機能は、最初は非推奨とマークされ、後で将来のリリースで削除されます。 別のオプションが提供されます。

デプロイメントで機能または機能を使用しているかどうかを確認します。 また、別のオプションを使用するように実装を変更することを計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | この **[!UICONTROL AEM クラウドサービスのオプトイン]** 次の理由で、screen は非推奨（廃止予定）となりました： [!DNL Experience Manager] および [!DNL Adobe Target] 統合は、Experience Manager6.5 で更新されました。この統合は、Adobe Target Standard API をサポートしています。 API は、Adobe IMSと [!DNL Adobe I/O] そして、Adobe・ローンチが実装する役割の拡大を支援 [!DNL Experience Manager] 分析およびパーソナライゼーション用のページでは、オプトインウィザードは機能的に無関係です。 | システム接続、Adobe IMS認証、および [!DNL Adobe I/O] 各 [!DNL Experience Manager] クラウドサービス。 |
| コネクタ | Microsoft® SharePoint 2010 およびMicrosoft® SharePoint 2013 用のAdobeJCR Connector は、Experience Manager6.5 で非推奨（廃止予定）となりました。 | 該当なし |

## 既知の問題 {#known-issues}

* AEM 6.5 Service Pack 11 をインストールし、ステータス ZIP ファイルをダウンロードしようとすると、Experience Managerは破損したファイルをダウンロードします。 ダウンロードとインストール [AEM Sites SEO インデックスパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip) をAEMインスタンス上でクリックしてから、ZIP ファイルをダウンロードして問題を解決してください。

* 形式 [!DNL Microsoft Windows Server 2019] はをサポートしていません [!DNL MySQL 5.7] および [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] の自動インストールはサポートされていません [!DNL AEM Forms 6.5.10.0].

* アップグレードする場合は、 [!DNL Experience Manager] 6.5 から 6.5.10.0バージョンのインスタンスは、 `RRD4JReporter` 例外 `error.log` ファイル。 この問題を解決するには、インスタンスを再起動します。

* 次をインストールした場合： [!DNL Experience Manager] 6.5 Service Pack 10 または以前の Service Pack ( [!DNL Experience Manager] 6.5：アセットのカスタムワークフローモデルのランタイムコピー ( `/var/workflow/models/dam`) が削除されました。
ランタイムコピーを取得するには、HTTP API を使用して、カスタムワークフローモデルのデザイン時コピーをそのランタイムコピーと同期することをAdobeにお勧めします。
   `<designModelPath>/jcr:content.generate.json`

* ユーザーは、 [!DNL Assets] ネストされたフォルダーをに公開します。 [!DNL Brand Portal]. ただし、フォルダーのタイトルは [!DNL Brand Portal] ルートフォルダーが再公開されるまで。

* アダプティブフォームで初めてフィールドを設定する場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* Experience Manager6.5.x.x のインストール中に、次のエラーと警告メッセージが表示される場合があります。
   * 「Adobe Target統合が Target Standard API（IMS 認証）を使用してExperience Managerで設定されている場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用されている場合、アダプティブフォームのサーバー側検証が失敗します (CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューすると、Dynamic Mediaのインタラクティブ画像のホットスポットが表示されない。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :登録の変更が完了するのを待機中のタイムアウトが未登録になりました。

* コンテンツフラグメントまたは Sites/Pages のいずれかを移動/削除/公開しようとすると、バックグラウンドクエリが失敗するので、コンテンツフラグメント参照が取得される際に問題が発生する。つまり、機能は動作しません。
正しい操作を行うには、次のプロパティをインデックス定義ノードに追加する必要があります `/oak:index/damAssetLucene` （インデックスの再作成は不要） :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## OSGi バンドルとコンテンツパッケージが含まれています {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントでは、に含まれる OSGi バンドルとコンテンツパッケージの一覧を示します。 [!DNL Experience Manager] 6.5.11.0:

* [Experience Manager6.5.11.0に含まれている OSGi バンドルの一覧](assets/65110_bundles.txt)

* [Experience Manager6.5.11.0に含まれているコンテンツパッケージの一覧](assets/65110_packages.txt)

## 制限付き Web サイト {#restricted-sites}

これらの Web サイトは、のお客様のみが利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* 詳しくは、 [カスタマーサポートへの問い合わせAdobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 リリースノート](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [Adobe Priority 製品アップデート](https://www.adobe.com/subscription/priority-product-update.html)のサブスクリプションを購入する

