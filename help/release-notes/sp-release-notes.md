---
title: '[!DNL Experience Manager] 6.5 サービスパックリリースノート'
description: 固有のリリースノート [!DNL Adobe Experience Manager] 6.5 サービスパック 10
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 0a35b26c5f790d67db55421b8f3e98e5ddb30528
workflow-type: tm+mt
source-wordcount: '4430'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5 サービスパックリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.10.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2021年8月26日（PT） |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## に含まれるもの [!DNL Adobe Experience Manager] 6.5.10.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.10.0には、2019 年 4 月の 6.5 リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善が含まれています。 サービスパックがにインストールされている [!DNL Adobe Experience Manager] 6.5.

に導入された主な機能および機能強化 [!DNL Adobe Experience Manager] 6.5.10.0は次のとおりです。

* **強化機能 [!DNL Content Fragment] モデルとエディター**:ネストされたを使用して、構造化コンテンツ用の複雑なモデルやカスタムモデルを作成できるようになりました。 [!DNL Content Fragment] モデル。 コンテンツ構造は、サブフラグメントとしてモデル化された基本要素にモジュール化されます。 上位レベルのフラグメントは、これらのサブフラグメントを参照します。 高度な検証ルールなどのデータタイプの強化により、 [!DNL Content Fragments]. この [!DNL Experience Manager] [!DNL Content Fragment] エディターは、一般的なエディターセッションでネストされたフラグメント構造をサポートします。たとえば、構造ツリー表示や、フラグメント階層を介したタブ付きパンくずナビゲーションなどの機能強化がおこなわれます。

* **の GraphQL API[!DNL Content Fragments]**:新しい GraphQL API は、構造化コンテンツを JSON 形式で配信する標準の方法です。 GraphQL クエリを使用すると、クライアントはエクスペリエンスをレンダリングする関連コンテンツ項目のみを要求できます。 このような選択により、クライアント側でのコンテンツ解析を必要とするコンテンツの過剰配信（HTTP REST API での可能性）が排除されます。 GraphQL スキーマは次から派生します。 [!DNL Content Fragment] モデルと API の応答は JSON 形式でおこなわれます。 In [!DNL Experience Manager] as a [!DNL Cloud Service], [GraphQL クエリが保持されます](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) キャッシュに適したGETリクエストを処理 ～ではまだ不可能だ [!DNL Experience Manager] 6.5.10.0.

* **階層の管理と今後のプレビュー**:ユーザーは、 [!DNL Experience Manager] ローンチに含まれるページの追加と削除の機能を含むローンチ。 この機能により、 [!DNL Experience Manager] 今後の公開をターゲットとするコンテンツバージョンを作成するためのローンチ。 [タイムワープ機能](/help/sites-authoring/working-with-page-versions.md#timewarp) ユーザーは、ローンチを将来のコンテンツステートとしてプレビューできます。

* **Connected Assets**: [!DNL Experience Manager] は [!DNL Connected Assets] 使用に対する機能 [!DNL Dynamic Media] 該当するコアコンポーネント内の画像。 「[Connected Assets の使用](/help/assets/use-assets-across-connected-assets-instances.md)」を参照してください。

* **アセットまたはレンディションをダウンロードするためのリンク共有オプション**:アセットとコレクションをリンクとして共有する場合、元のアセットのダウンロードを許可するか、レンディションのダウンロードを許可するか、共有リンクを使用して両方を許可するかを選択できます。 また、リンクを通じて共有されているアセットをダウンロードしたユーザーは、元のアセットのみ、レンディションのみ、またはその両方をダウンロードするオプションが使用できます。

* **生成されるサブアセットを制限**:管理者は、 [!DNL Experience Manager] は、PDF、PowerPoint、InDesign、キーノートファイルなどの複合アセットに対してを生成します。 詳しくは、 [複合アセットの管理](/help/assets/managing-linked-subassets.md#generate-subassets).

* **Camera Raw支援**:新しい [!DNL Camera Raw] をサポートするパッケージが利用可能です [!DNL Adobe Camera Raw] v10.4。詳しくは、 [を使用して画像を処理 [!DNL Camera Raw]](/help/assets/camera-raw.md).

* 組み込み型のリポジトリ (Apache Jackrabbit Oak) が1.22.8に更新されました。

* **アクセシビリティの強化**:

   * [!DNL Dynamic Media] では、ビューアに対して多くのアクセシビリティ強化を提供しています。 詳しくは、 [[!DNL Dynamic Media] 更新](#dynamic-media-65100).

   * Platform では、アクセシビリティがいくつか強化されています。 詳しくは、 [Platform の更新](#platform-65100).

* **ユーザーエクスペリエンスの強化**:

   * [!DNL Experience Manager] フォルダーの下にすべてのコンテンツモデルのリストを直接表示します。コンテンツ作成者はファイル構造内を移動する必要はありません。 この機能により、クリック数が少なくなり、オーサリングの効率が向上しました。

   * のパスフィールド [!DNL Sites] エディターを使用すると、作成者は次の場所からアセットをドラッグできます： [!DNL Content Finder].

* のサポートを追加しました。 `GuideBridge#getGuidePath` の API [!DNL AEM Forms].

* これで、Automated forms conversionサービスを [PDF formsをフランス語、ドイツ語、スペイン語、イタリア語、ポルトガル語の各言語で変換する](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html#language-specific-meta-model) アダプティブフォームに変換する

* **プロパティブラウザーのエラーメッセージ**：アダプティブフォームのプロパティブラウザーに、各プロパティに関するエラーメッセージを追加しました。これらのメッセージは、フィールドの許可値を理解するのに役立ちます。

* **リテラルオプションを使用して JSON タイプの変数の値を設定する機能をサポート**:リテラルオプションを使用して、AEM Workflow の変数設定手順で JSON 型変数の値を設定できます。 リテラルオプションを使用すると、文字列の形式で JSON を指定できます。

* [プラットフォームの更新](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] JEE 上では、次のプラットフォームのサポートが追加されました。
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

に導入されたすべての機能および機能強化の一覧については、 [!DNL Experience Manager] 6.5.10.0、 [の新機能 [!DNL Adobe Experience Manager] 6.5 サービスパック 10](new-features-latest-service-pack.md).

以下は、 [!DNL Experience Manager] 6.5.10.0リリース。

### [!DNL Sites] {#sites-65100}

* フォーカスは、 **[!UICONTROL デフォルト値]** 下のフィールド **[!UICONTROL プロパティ]** コンテンツフラグメントエディターのタブ (NPR-36992)。

* フィルタリング中 [!DNL Content Fragment] 指定したパスの下のモデル [!DNL Experience Manager] 検索では、 `cq:Template` のパスやノードを返す代わりに、 [!DNL Content Fragment] モデル (SITES-1453)。
* [!DNL Content Fragments] 戻る `null` をフォルダーのステータス (SITES-1157) として追加しました。
* [!DNL Experience Manager] ユーザーが無効にして有効にすることを許可しない [!DNL Content Fragment] モデル (SITES-1088)。
* ユーザーが移動、名前変更、または削除したとき [!DNL Content Fragments] ( 参照元の [!DNL Content Fragments] は自動的には更新されません (SITES-196)。
* あるページから別のページにコンポーネントを貼り付けると、JavaScript エラーが発生する (NPR-37030)。
* ページのプロパティがすばやく表示されると、別のページのページプロパティが開かれる (NPR-37025)。
* コンテンツフラグメントを使用すると、コンテンツフラグメントは自身を参照できます。 ピッカーが操作をサポートしていない (NPR-36993)。
* Service Pack 9 にアップグレードした後、一部のユーザーは、Experience Manager内でフォルダを移動できず、ログにエラーが表示されません (SITES-1481)。
* 編集モードでレイアウトコンテナ内のコンポーネントの幅を調整する際に、ちらつきが発生する (NPR-36961)。
* ローンチの昇格時に、昇格済みのローンチの変更が他のローンチに二重にロールアウトされます。 ユーザーがダブルロールアウトされたローンチを昇格すると、2 倍のコンテンツがソースページに反映される (NPR-36893)。
* [!DNL Experience Manager] 画像コアコンポーネントを使用してページに画像を追加する場合、または基盤画像コンポーネントを使用してサイズを変更する場合に、透明度を持つ一部の PNG 画像にグレーの境界線を追加する。(NPR-36879)
* [!DNL Experience Manager Sites] 多数のテンプレートを含む管理 UI で、ナビゲーションが遅くなる (NPR-36870)。
* リンクがカスタムサーブレットフィルターバンドルによって変更された場合、Web ページがレンダリングに失敗する (NPR-36857)。
* この `ContextHubImpl` メソッドは `ResourceResolver` それは閉じられていません。 長時間実行に関する警告メッセージが表示されます。 `ResourceResolver` また、サービスが予期しない結果を時々返す (NPR-36853)。
* ブループリントページのプロパティから単一のライブコピーを同期すると、その他のすべてのライブコピーも同期される (NPR-36829、NPR-36522)。
* XLS の MIME タイプのみを使用した場合、ファイルのアップロード機能が期待どおりに動作しない (NPR-36785)。
* パスケースとすべて大文字の単語を含む新しいタグは、内のタグフィールドに表示されません [!DNL Content Fragments] (NPR-36742)。
* 「単一のテキスト要素」オプション ( [!DNL Content Fragment] を指定すると、テキストが欠落し、リストとネストされたリストに関連する奇数の書式が作成される (NPR-36565)。
* 作成者がページ上の任意のコンポーネントに注釈を付け、そのコンポーネントを削除し、削除操作の取り消しを実行すると、サイトコンソールでそのページのタイムラインデータを表示しようとするとエラーが発生する。(NPR-36528)
* ページプロパティバルクエディターの [!UICONTROL 保存して閉じる] オプションは変更を保存するが、エディターを閉じない (NPR-36527)。
* ユーザーが新しいテキストコンポーネントをページにドラッグ&amp;ドロップしようとすると、そのコンポーネントが直ちに消える (NPR-36442)。
* ユーザーがスペース（システム上に存在しないタグ）を含むオンデマンドタグに入力し、Enter キーを押すと、そのタグがフィールドの下に表示されます。 ただし、 [!DNL Content Fragment] が保存され再び開かれた場合、オンデマンドタグは表示されない (NPR-36441)。
* インスタンスが Dispatcher 経由でアクセスされる場合、テンプレートは削除できない。(NPR-36385)
* ページを移動する際に、変更をレンダリングするには、ブラウザを手動で更新する必要がある (NPR-36381)。
* コンポーネントを選択する際に、Ctrl + X または Ctrl + C キー ( およびMacでは Command + X または Command + C キー ) を使用して切り取りまたはコピーできます。 別のコンポーネントをクリックしたときに、ツールバーで貼り付けることができますが、キーボード（Ctrl+V または Command+V）では貼り付けできません (NPR-36379)。
* ユーザーがはさみアイコンを使用してコンポーネントを切り取って別の場所に移動しようとすると、コンソールエラーが発生します。 また、1 つのコンポーネントのみ貼り付けると、移動される (NPR-36378)。
* [!DNL Experience Manager] には、WCM 上のインデックスや通知を含まないクエリがあり、パフォーマンスが低下する (NPR-36303)。
* 作成者が、削除された継承コンポーネントの継承を復元する場合、使用可能なオプションは、すべてのページコンテンツを同期することです。 継承が 1 つのコンポーネントでのみ復元された場合でも、コンテンツ作成者は完全なページを同期する必要があります。 完全な同期により、望ましくないコンテンツが同期される可能性がある (NPR-34456、CQ-4310183)。
* オーサーインスタンス上のコンポーネントのライブ使用では、すべての項目が表示されるわけではありません。 1,000 ページを超えるページで使用されているコンポーネントもありますが、レポートには約 40 ページしか表示されません (CQ-4323724)。
* 多数のサブページを含むサイト構造がある場合、列表示でのサブページの読み込みには、Experience Manager6.4.8.2 に比べて、Experience Manager6.5.8 での時間が長くなります (CQ-4322766)。
* 「ページをロールアウト」オプションで「すべて」が機能しない。(NPR-37070)
* ページの既存の v3 コンポーネントバージョンを開くと、ページのプロパティダイアログが開かず、 `NullPointerException` がログに記録されます (SITES-1830)。

### [!DNL Assets] {#assets-65100}

以下の問題を修正しました。 [!DNL Assets]:

* プロパティの値 `jcr:title` フォルダーを移動した後、パブリッシュインスタンス上ではが更新されません。 作成者内のフォルダーの名前を変更して再公開しても、 `jcr:title` パブリッシュインスタンスで同じプロパティ値を持つ (NPR-36369)。

* 2 つ以上のアセットを選択し、1 つ以上のメタデータフィールドが編集された場合、Safari ブラウザーでエラーコード 500 が表示されて保存操作が失敗する。(NPR-36413)

* 日付の形式が正しくないので、一括メタデータの読み込みに失敗する。(NPR-36428)

* 選択が [!UICONTROL プロパティ] メタデータを更新するページで、スキーマから多くのオプションが提供される場合、インターフェイスの応答が遅くなる (NPR-36430)。

* を使用した検索フィルター [!UICONTROL 有効期限ステータス] 述語が機能しない (NPR-36436)。

* の各種フィールドのポップアップメニュー [!UICONTROL フォルダーメタデータ] プロパティには、最後に選択された値が表示されない (NPR-36937、CQ-4314429)。

* ファイルとフォルダを検索する場合、フィルタを適用して選択する場合 [!UICONTROL ファイルとフォルダー]の場合、ファイルのみが表示されますが、フォルダーは表示されません (CQ-4319543、NPR-36627)。

* フォルダー内から同じコレクションが選択されている場合と、検索結果から選択されている場合で、ツールバーのオプションが異なる (NPR-36620)。

* この [!UICONTROL クイック公開] オプションが検索結果ページで使用できない (NPR-36904、CQ-4317748)。

* ユーザーが拡張子を指定せずにアセットのライブコピーを作成した場合、ダウンロード後にライブコピーファイルを使用できない (NPR-36903、CQ-4326305)。

* ユーザーが子フォルダーの所有者として追加されると、そのユーザーは親フォルダーの所有者権限も取得します。つまり、親フォルダーの他の子フォルダーの所有者権限も取得します。 また、ユーザーが親フォルダーを削除しようとしても、親フォルダーの所有者として削除されません。 (NPR-36801、CQ-4323737)。

* [!DNL Experience Manager] PowerPoint プレゼンテーションなどの複合アセットのサブアセットを作成しようとすると、メモリ不足の例外が生成されます (NPR-36668)。

* 公開済みのサイトページで既に使用されているアセットをユーザーが移動すると、公開するオプションが選択されていない場合でも、サイトページが再び公開されます (NPR-36636、CQ-4323500)。

* Apache Tika の MIME タイプ検出機能を使用する場合、 `AssetManager.createAsset` メソッドは、 `apache-tika-*.tmp` ファイルを一時ディレクトリに格納します。 この一時ファイルは、使用可能なすべての空きディスク領域を使用します (NPR-36545)。

* DRM で保護されているすべてのアセットがダウンロードされ、特定のアセットをダウンロードするためのユーザー選択が実行されません (CQ-4327422)。

* アセットを次にドラッグできません： `pathfield` ユーザーインターフェイス (NPR-36849) で確認。

* 列表示でアセットを選択すると、アセットの詳細パネルが表示されなくなる (NPR-36667)。

### [!DNL Dynamic Media] {#dynamic-media-65100}

**アクセシビリティの強化**

では、次のアクセシビリティの強化が利用できます。 [!DNL Dynamic Media Viewers].

* スクリーンリーダーが、プレースホルダーテキストを読み上げ、アセットをリンクダイアログとして共有する際に、電子メールアドレスを必須フィールドとして追加し、 [!UICONTROL このフィールドに入力してください] tooltip(CQ-4327761)

* スクリーンリーダーで、 [!UICONTROL 画像プリセットエディター] キーボードを使用してユーザーインターフェイスフィールドにアクセスする際に (CQ-4325677)。

* キーボードフォーカスがの検索タブに適切に移動するようになりました。 [!UICONTROL ビューアプリセット] のアセットピッカーのダイアログボックス [!UICONTROL リッチメディアタイプ] オプション (CQ-4324736) が表示されます。

* キーボードキーを使用してフォームモードで移動する場合、スクリーンリーダーは、の増分および減分オプションに対応するラベルを読み上げます。 [!UICONTROL 作成] タブ [!UICONTROL 画像プリセット] (CQ-4323900)。

* スクリーンリーダーで [!UICONTROL メールアドレスを検索して追加] アセットをリンクダイアログボックスとして共有するオプション (CQ-4323352)

* キーボードキーを使用してアセットを移動しても、ツールバーにキーボードフォーカスが保持される (CQ-4322037)。

* スクリーンリーダーで、新しく追加された [!UICONTROL 編集] 選択後のフィールド情報 [!UICONTROL 切り抜きを追加] オプションを [!UICONTROL レスポンシブ画像の切り抜き] オン [!UICONTROL 画像処理プロファイルを編集] ページ (CQ-4290734) に表示されます。

* オン [!UICONTROL 画像プリセットを編集] および [!UICONTROL インタラクティブビデオを作成] ページ、スクリーンリーダーで、見出しキーボードショートカットキーを使用してページを移動する際に、ページ見出しが適切に読み上げられるようになりました (CQ-4290730)(CQ-4290701)。

* スクリーンリーダーは、次のページを移動する際に、ランドマークキーと領域ショートカットキーを使用して、画面の様々な領域（右パネル領域、左パネル、アクションツールバー、ビューアツールバーのランドマーク、ズーム可能な画像のランドマークなど）を認識できるようになりました。

   * [!UICONTROL ビューアプリセットエディター] (CQ-4290729)

   * [!UICONTROL 画像セットエディター] (CQ-4290710)

   * [!UICONTROL インタラクティブビデオを作成] (CQ-4290702)。

* スクリーンリーダーが下向き矢印キーを使用して移動する際に、ビデオフレームの共有オプションの名前を読み上げるようになりました (CQ-4290728)。

* スクリーンリーダーで、 [!UICONTROL スプライト] および [!UICONTROL 背景] タブ [!UICONTROL 外観] タブ [!UICONTROL ビューアプリセットエディター] (CQ-4290727)。

* 編集するフィールドなどの必須フィールド [!UICONTROL 幅]、 [!UICONTROL 基本] タブ [!UICONTROL ビデオエンコーディングを編集] ページにアスタリスク記号 (*) が表示されるようになりました (CQ-4290725)。

* スクリーンリーダーで、 [!UICONTROL イメージプロファイル] ページ (CQ-4290723) に表示されます。

* Windows ユーザーは、 [!UICONTROL ビューアプリセットエディター] フォーカスが CSS エディターにあるとき (CQ-4290720)。

* オン [!UICONTROL 基本] タブ [!UICONTROL 画像プリセットを編集] フォームモードで移動する際に、スクリーンリーダーが様々な編集フィールドおよびオプションのラベルを読み上げるようになりました (CQ-4290717)。

* スクリーンリーダーが、アセットの詳細ページの左側のナビゲーションにあるユーザーインターフェイスオプションの役割と状態（選択または未選択）を読み上げるようになりました (CQ-4290709)。

* スクリーンリーダーで、状態（選択された、または選択されていない）を正しく読み上げ、画像のリンクが [!UICONTROL コンテンツ] タブ [!UICONTROL インタラクティブビデオを作成] ページ (CQ-4290707) に表示されます。

* スクリーンリーダーで、上の下向き矢印キーを使用して移動する際、ビデオタイムラインスケールで、様々なセグメントの名前、役割、状態を正しく読み上げるようになりました。 [!UICONTROL インタラクティブビデオを作成] ページ (CQ-4290706) に表示されます。

* スクリーンリーダーで、 [!UICONTROL インタラクティブビデオを作成] ページ (CQ-4290704) に表示されます。

* スクリーンリーダーで、 [!UICONTROL すべてのアセット] および [!UICONTROL すべてのコレクション] 移動時のオプション [!UICONTROL 公開] ページ (CQ-4290705) に表示されます。

* で（MP4 以外の）サポートされていないビデオ形式をアップロードしたとき [!UICONTROL インタラクティブビデオを作成] ページ、Experience Managerが表示され、エラーメッセージがアナウンスされる (CQ-4290700)。

* タイムラインスケールの数値（秒単位の時間）のコントラスト [!UICONTROL インタラクティブビデオを作成] ページが最小限の必要な明るさの比率を満たし、色の知覚が限られたユーザーが読みやすくなるようになりました (CQ-4290699)。

* スクリーンリーダーで、 [!UICONTROL 製品名] フィールド ( [!UICONTROL インタラクティブビデオを作成] ページ (CQ-4290697) に表示されます。

**修正された問題**

以下のバグ修正が、 [!DNL Dynamic Media].

* にビデオをアップロードしました [!DNL Experience Manager] 表示 `Process failed` 後 `dynamicmedia_scene7` 実行モードが有効で、同期が無効です (CQ-4327791)。

### Platform {#platform-65100}

このサービスパックでは、次の機能強化が提供されています。

* ユーザーがツリー表示で項目を選択すると、スクリーンリーダーは、上部に表示される選択とツールバーオプションを読み上げる (NPR-36504)。
* 明るさの比率が最小要求比 4.5:1 を満たすので、視覚の問題があるユーザーは、テキストや制御名の読みやすさが一部わかりやすくなります (NPR-36503)。
* ユーザーがカレンダーコントロールを使用する場合、スクリーンリーダーは、記述的な日付、月、曜日の情報をナレーションします。 ユーザーがカレンダーショートカットキーを使用すると、スクリーンリーダーが日付、月、年の変更をナレーションする (NPR-36498)。
* カスタム JavaScript を実行するためのサポートが提供されました `Clientlibs` 厳密なモードに準拠せずに ECMAScript 6 機能を使用する。 特に、 `emitUseStrict` フラグが `GCCScriptProcessor` (NPR-36411)。

このサービスパックには、次のバグ修正が含まれています。

* カスタムヘルスチェックは、スケジュールされたよりも頻繁に実行されます (NPR-36985)。
* この `Resourceresolver map` メソッドがエイリアスページに対して誤った結果を返す。(NPR-36767)
* [!DNL Experience Manager] 読み込みワークフローが原因で、起動が遅延する。(NPR-36615)

### 統合 {#integrations-65100}

* Experience Managerが応答しなくなるのは、プライマリ MongoDB ノードが別のノードに切り替わったときです (NPR-36566)。
* [!DNL Sling content distribution] コレクションメンバーの削除操作の実行時に失敗する。(NPR-36521、CQ-4323578)

### ユーザーインターフェイス {#user-interface-65100}

* この **[!UICONTROL 参照]** サイドパネルにアセットおよびサイトの参照が表示されない (GRANITE-35078、GRANITE-34892)。

### 翻訳プロジェクト {#translation-65100}

* 多言語翻訳プロジェクトの言語コピーの余分なサブページが削除される (NPR-36622)。

### ワークフロー {#workflow-65100}

* サーバーが不在メッセージを受け取ると、メモリアラートを報告し、応答を停止する (NPR-36768)。

### [!DNL Communities] {#communities-65100}

* コミュニティサイトページが `LoggedIn` 匿名のゲストユーザーの状態 (NPR-36908)。

* ページが **[!UICONTROL コミュニティ]** > **[!UICONTROL アイデア]** > **[!UICONTROL コメント]** ページのナビゲーションが機能しない (NPR-36541)。

<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65100}

*
-->

### [!DNL Forms] {#forms-65100}


>[!NOTE]
>
>* [!DNL Experience Manager Forms] では、予定されている [!DNL Experience Manager] サービスパックリリース日の 1 週間後にアドオンパッケージをリリースします。


[!DNL AEM 6.5.10.0 Forms] には、次のバグ修正が含まれています。

* インストール時 [!DNL AEM 6.5 Forms]に設定すると、次のサードパーティライブラリが自動的にインストールされます (CQDOC-18373)。
   * [!DNL Microsoft Visual C++ 2008 Service Pack 1 (x86)]
   * [!DNL Microsoft Visual C++ 2010 Service Pack 1 (x86)]

**アダプティブフォーム**

* アダプティブフォームのフィールド値に対して実行された検証が正常に完了した場合、 [!DNL AEM Forms] フォームデータモデルの呼び出しに失敗しました (CQ-4325491)。

* 翻訳プロジェクトに言語辞書を追加し、そのプロジェクトを開くと、 [!DNL AEM Forms] は次のエラーメッセージを表示します (CQ-4324933)。

   ```TXT
   Uncaught TypeError: Cannot read property 'PROJECT_LISTING_PATH' of undefined
   at openButtonClickHandler (clientlibs.js:245)
   at HTMLButtonElement.onclick (clientlibs.js:258)
   ```

* インストール後のパフォーマンスの問題 [!DNL AEM Forms] Service Pack 7(CQ-4326828)。

* 標準の HTML アップロードフィールドを含んだフォームを Apple iOS デバイスから送信すると、ファイルの内容が送信されず、送信先で 0 バイトのファイルを受信することがあります。Apple iOS 15.1 では、問題の修正が提供されています (CQ-4325361)。

**Correspondence Management**

* 内の文字の表示遅延 [!UICONTROL データ] タブやHTMLレターのプレビュー (NPR-37020) も表示される。

* テキストドキュメントフラグメントを編集しているとき、フラグメントを保存すると、新しい単語がHTMLタグとして表示される (NPR-36837)。

* ドラフトとして保存されているレターを表示できない (NPR-36816)。

* テキストドキュメントフラグメントを編集してレターをプレビューすると、AEM FormsはHTMLレタープレビューに式言語を表示します (CQ-4322331)。

* セルフサービスレターテンプレートを使用してデータをレンダリングする際に発生する問題 (NPR-37161)。


**インタラクティブコミュニケーション**

* タブ文字は、テキストドキュメントフラグメントの編集後にインタラクティブ通信のプレビューを印刷するたびに、2 つの単語間で重複します (NPR-37021)。

* [!DNL AEM Forms] 最大サイズ制限を超えるテキストドキュメントフラグメントを保存すると、エラーが表示される。(NPR-36874)

* インタラクティブ通信に画像を追加すると、その画像の後に追加の空のブロックが表示される (NPR-36659)。

* エディターですべてのテキストを選択すると、フォントテキストを Arial に変更できない (NPR-36646)。

* エディターで URL を作成し、変更をプレビューすると、URL テキストの代わりに黒い背景が表示される (NPR-36640)。

* エディターにテキストをコピーして貼り付ける際、ドキュメント内の箇条書き記号のフォントを Arial に変更する際に問題が発生する。(NPR-36628)

* テキストエディターでの箇条書きのインデントの問題 (NPR-36513)。

**デザイナー**

* 画面Readerが、マスターページ上のテキストラベルまたは動的PDFのサブフォームページに配置されたフローティングフィールドデータを読み取れませんでした (CQ-4321587)。

**ドキュメントサービス**

* XDP ファイルをPDFファイルに変換し、結果のPDFをアセンブリすると、PDFの生成に失敗し、次のエラーメッセージが表示されます。

   ```TXT
   Caused by: com.adobe.fd.assembler.client.AssemblerException$ClientException: Document is in a disposed state!
   ```

**Forms のワークフロー**

* AEM Forms Service Pack 8 にアップグレードした後、Workbench プロセスにフォームを送信できない (CQ-4325846)。

**HTML5 のフォーム**

* この `mfAllowAttachments` プロパティとして `True` CRX DE リポジトリで、 `dataXml` 送信時に破損するHTML5 フォーム (NPR-37035)。

* を使用して XDP をHTMLとしてレンダリングする場合 `dataXml`, [!DNL AEM Forms] が表示されます `Page Unresponsive` エラー (NPR-36631)。

### コマース {#commerce-65100}

* の値 **[!UICONTROL 公開者]** 表示されるフィールドが列表示で正しくない (NPR-36902)。
* カタログがロールアウトされると、新しい製品が誤って変更された製品としてマークされる (NPR-36666)。
* 削除された製品を再作成しても、製品ページは再作成されません (NPR-36665)。
* 変更されたページは更新されますが、対応するリンクされた製品は「カタログ」ロールアウトで更新されません (CQ-4321409、NPR-36422)。
* この **[!UICONTROL 後で公開]** および **[!UICONTROL 後で非公開にする]** ワークフローが機能しない (CQ-4327679)。

セキュリティ更新について詳しくは、 [[!DNL Experience Manager] セキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html).

## 6.5.10.0 のインストール {#install}

**設定要件と詳細情報**

* Experience Manager6.5.10.0にはExperience Manager6.5 が必要です。 [アップグレードドキュメント](/help/sites-deploying/upgrade.md) を参照してください。
* サービスパックのダウンロードは、Adobeで利用できます [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* MongoDB および複数のインスタンスを使用するデプロイメントで、パッケージマネージャーを使用して、いずれかのオーサーインスタンスにExperience Manager6.5.10.0をインストールします。

>[!NOTE]
>
>Adobeは、 [!DNL Adobe Experience Manager] 6.5.10.0パッケージ。

### サービスパックのインストール {#install-service-pack}

に Service Pack をインストールするには [!DNL Adobe Experience Manager] 6.5 インスタンスを使用するには、次の手順に従います。

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 Adobeでは、インスタンスの現在の稼動時間が長い場合に再起動を推奨します。

1. インストールする前に、スナップショットまたは新しいバックアップを作成します [!DNL Experience Manager] インスタンス。

1. 次の場所からサービスパックをダウンロードします。 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip).

1. パッケージマネージャーを開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。詳しくは、 [パッケージマネージャー](/help/sites-administering/package-manager.md).

1. パッケージを選択し、 **[!UICONTROL インストール]**.

1. S3 コネクタを更新するには、Service Pack のインストール後にインスタンスを停止し、既存のコネクタを install フォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。 詳しくは、 [Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。 Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを保証します。 通常、この問題は [!DNL Safari] ブラウザーは断続的に使用されますが、どのブラウザーでも発生する場合があります。

**自動インストール**

を自動的にインストールするには、次の 2 つの方法があります [!DNL Experience Manager] 6.5.10.0（作業中のインスタンス）:

A.パッケージをに配置します。 `../crx-quickstart/install` フォルダー（サーバーがオンラインで使用可能な場合） パッケージが自動的にインストールされます。

B. [パッケージマネージャーからの HTTP API](/help/sites-administering/package-manager.md#package-share). 用途 `cmd=install&recursive=true` ネストされたパッケージがインストールされるようにする。

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0では、Bootstrapのインストールはサポートされていません。

**インストールの検証**

1. 製品情報ページ (`/system/console/productinfo`) は、更新されたバージョン文字列を表示します `Adobe Experience Manager (6.5.10.0)` under [!UICONTROL インストール済み製品].

1. すべての OSGi バンドルは、 **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** OSGi コンソール (Web コンソールを使用： `/system/console/bundles`) をクリックします。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン1.22.3以降です (Web コンソールを使用： `/system/console/bundles`) をクリックします。

このリリースでの動作が認定されたプラットフォームについては、 [技術要件](/help/sites-deploying/technical-requirements.md).

### Adobe Experience Manager Formsアドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Experience Manager Formsを使用していない場合はスキップします。 Experience Manager Formsでの修正は、スケジュールされた週の後に、個別のアドオンパッケージを通じて配信されます [!DNL Experience Manager] Service Pack リリース。

1. Adobe Experience Manager Service Pack がインストールされていることを確認します。
1. [AEM Forms リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. Formsアドオンパッケージをインストールします。詳しくは、 [AEM Formsアドオンパッケージのインストール](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager6.5.10.0には、 [AEM Forms互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). 古いバージョンのAEM Forms互換性パッケージを使用していて、Experience Manager6.5.10.0にアップデートする場合は、Formsアドオンパッケージのインストール後に、最新バージョンのパッケージをインストールします。

### JEE でのAdobe Experience Manager Formsのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE 上のAdobe Experience Manager Formsの修正は、別のインストーラーを通じて提供されます。

JEE 上のExperience Manager Formsの累積インストーラーのインストールとデプロイ後の設定について詳しくは、 [リリースノート](jee-patch-installer-65.md).

>[!NOTE]
>
>JEE 上のExperience Manager Formsの累積インストーラーをインストールした後、最新のFormsアドオンパッケージをインストールし、次の場所からFormsアドオンパッケージを削除します。 `crx-repository\install` フォルダーを開き、サーバーを再起動します。


### UberJar {#uber-jar}

Experience Manager6.5.10.0の UberJar は、 [Maven 中央リポジトリ](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/).

Maven プロジェクトで UberJar を使用するには、 [UberJar の使用方法](/help/sites-developing/ht-projects-maven.md) およびは、プロジェクト POM に次の依存関係を含めます。

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.10</version>
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

## OSGi バンドルとコンテンツパッケージが含まれています {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントでは、に含まれる OSGi バンドルとコンテンツパッケージの一覧を示します。 [!DNL Experience Manager] 6.5.10.0:

* [Experience Manager6.5.10.0に含まれている OSGi バンドルの一覧](assets/65100_bundles.txt)

* [Experience Manager6.5.10.0に含まれているコンテンツパッケージの一覧](assets/65100_packages.txt)

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

