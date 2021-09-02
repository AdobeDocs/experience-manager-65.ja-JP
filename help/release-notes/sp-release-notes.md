---
title: '[!DNL Experience Manager] 6.5サービスパックリリースノート'
description: リリースノート（ [!DNL Adobe Experience Manager] 6.5 service pack 10固有）
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: f9b53df7d235fa6be2cee8c05071790114a91da1
workflow-type: tm+mt
source-wordcount: '4376'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5サービスパックリリースノート {#aem-service-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.10.0 |
| タイプ | Service Pack のリリース |
| 日付 | 2021 年 8 月 26 日 |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## [!DNL Adobe Experience Manager] 6.5.10.0に含まれる内容 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.10.0には、2019年4月の6.5リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善が含まれています。サービスパックは[!DNL Adobe Experience Manager] 6.5にインストールされています。

[!DNL Adobe Experience Manager] 6.5.10.0で導入された主な機能と機能強化は次のとおりです。

* **モデル [!DNL Content Fragment] とエディターの強化**:ネストされたモデルを使用して、構造化コンテンツ用の複雑なモデルおよびカスタムモデルを作成できるよう [!DNL Content Fragment] になりました。コンテンツ構造は、サブフラグメントとしてモデル化された基本要素にモジュール化されます。 上位レベルのフラグメントは、これらのサブフラグメントを参照します。 高度な検証ルールなどのデータタイプの強化により、[!DNL Content Fragments]を使用したコンテンツモデリングの柔軟性がさらに向上します。 [!DNL Experience Manager] [!DNL Content Fragment]エディターは、一般的なエディターセッションでネストされたフラグメント構造をサポートし、構造ツリー表示やフラグメント階層でのタブ付きパンくずナビゲーションなどの機能が強化されました。

* **次のためのGraphQL API[!DNL Content Fragments]**:新しいGraphQL APIは、構造化コンテンツをJSON形式で配信する標準の方法です。GraphQLクエリを使用すると、クライアントは、エクスペリエンスをレンダリングする関連コンテンツ項目のみを要求できます。 このような選択により、クライアント側でのコンテンツ解析を必要とするコンテンツの過剰配信（HTTP REST APIで使用可能）が排除されます。 GraphQLスキーマは[!DNL Content Fragment]モデルから派生し、API応答はJSON形式でおこなわれます。 [!DNL Experience Manager]では、[!DNL Cloud Service]として[GraphQLクエリが保持され、キャッシュに適したGETリクエストが処理されます。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) [!DNL Experience Manager] 6.5.10.0ではまだ可能ではありません。

* **階層の管理と今後のプレビュー**:ローンチのページの追加や削除機能を含む、ローンチのコン [!DNL Experience Manager] テンツ構造にアクセスするためのインターフェイスがユーザーに追加されました。この機能により、今後の公開をターゲットとしたコンテンツバージョンを作成する際に、[!DNL Experience Manager]ローンチの柔軟性が向上します。 [タイムワープ機能を使用す](/help/sites-authoring/working-with-page-versions.md#timewarp) ると、ユーザーはローンチを将来のコンテンツ状態としてプレビューできます。

* **Connected Assets**: [!DNL Experience Manager] は、適用可 [!DNL Connected Assets] 能なコアコンポーネン [!DNL Dynamic Media] トでの画像の使用に対して機能を拡張します。「[Connected Assets の使用](/help/assets/use-assets-across-connected-assets-instances.md)」を参照してください。

* **アセットやレンディションをダウンロードするためのリンク共有オプション**:アセットとコレクションをリンクとして共有する場合、元のアセットのダウンロードを許可するか、レンディションのダウンロードを許可するか、共有リンクを使用して両方を許可するかを選択できます。また、リンクを通じて共有されているアセットをダウンロードしたユーザーは、元のアセットのみ、レンディションのみ、またはその両方をダウンロードするオプションを使用できます。

* **生成されるサブアセットの制限**:管理者は、PDF、PowerPoint、InDesign、Keynoteファイルな [!DNL Experience Manager] どの複合アセットに対して生成されるサブアセットの数を制限できます。[複合アセットの管理](/help/assets/managing-linked-subassets.md#generate-subassets)を参照してください。

* **Camera Rawサポート**:v10.4をサ [!DNL Camera Raw] ポートする新しいパッケー [!DNL Adobe Camera Raw] ジが利用できます。 [を使用した画像の処 [!DNL Camera Raw]](/help/assets/camera-raw.md)理を参照してください。

* 組み込み型のリポジトリ(Apache Jackrabbit Oak)が1.22.8に更新されました。

* **アクセシビリティの強化**:

   * [!DNL Dynamic Media] では、ビューアのアクセシビリティが多く強化されています。[[!DNL Dynamic Media] 更新](#dynamic-media-65100)を参照してください。

   * Platformでは、アクセシビリティがいくつか強化されています。 [プラットフォームの更新](#platform-65100)を参照してください。

* **ユーザーエクスペリエンスの強化**:

   * [!DNL Experience Manager] は、フォルダーの下にすべてのコンテンツモデルのリストを直接表示します。コンテンツ作成者はファイル構造内を移動する必要はありません。この機能により、クリック数が少なくなり、オーサリングの効率が向上しました。

   * [!DNL Sites]エディターのパスフィールドを使用すると、作成者は[!DNL Content Finder]からアセットをドラッグできます。

* [!DNL AEM Forms]での`GuideBridge#getGuidePath` APIのサポートを追加しました。

* 自動フォーム変換サービスを使用して、[フランス語、ドイツ語、スペイン語の PDF フォームをアダプティブフォームに変換](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#language-specific-meta-model)できるようになりました。

* **プロパティブラウザーのエラーメッセージ**：アダプティブフォームのプロパティブラウザーに各プロパティのエラーメッセージが追加されました。これらのメッセージは、フィールドに使用できる値を理解するのに役立ちます。

* **リテラルオプションを使用してJSONタイプの変数の値を設定する機能**&#x200B;をサポートします。リテラルオプションを使用して、AEM Workflowの変数設定手順でJSONタイプの変数の値を設定できます。リテラルオプションを使用すると、文字列の形式で JSON を指定できます。

* **プラットフォームのアップデート**: [!DNL Adobe Experience Manager Forms] JEE上では、次のプラットフォームのサポートが追加されました。
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

[!DNL Experience Manager] 6.5.10.0で導入されたすべての機能と機能強化の一覧については、 [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md)の新機能を参照してください。[

[!DNL Experience Manager] 6.5.10.0リリースで提供された修正の一覧を次に示します。

### [!DNL Sites] {#sites-65100}

* コンテンツフラグメントエディターの「**[!UICONTROL プロパティ]**」タブの下の「**[!UICONTROL デフォルト値]**」フィールドに入力すると、フォーカスが別のフィールドに移動する(NPR-36992)。

* 指定されたパスの下の[!DNL Content Fragment]モデルをフィルタリングする際、[!DNL Experience Manager]検索は、[!DNL Content Fragment]モデル(SITES-1453)のパスとノードを返す代わりに、`cq:Template`を含むすべてのノードを返します。
* [!DNL Content Fragments] をフォ `null` ルダーのステータスとして返します(SITES-1157)。
* [!DNL Experience Manager] では、ユーザーはモデルの無効化と [!DNL Content Fragment] 有効化をおこなえません(SITES-1088)。
* ユーザーが[!DNL Content Fragments]やメディアアセットを移動、名前変更、削除した場合、参照されている[!DNL Content Fragments]は自動的には更新されません(SITES-196)。
* あるページから別のページにコンポーネントを貼り付けると、JavaScriptエラーが発生する(NPR-37030)。
* ページプロパティがすばやく表示されると、別のページのページプロパティが開く(NPR-37025)。
* コンテンツフラグメントを使用すると、コンテンツフラグメント自体を参照できます。 ピッカーが操作をサポートしていない(NPR-36993)。
* Service Pack 9にアップグレードした後、一部のユーザーがExperience Manager内のフォルダーを移動できず、ログにエラーが表示される(SITES-1481)。
* 編集モードでレイアウトコンテナ内のコンポーネントの幅を調整する際に、ちらつきが発生する(NPR-36961)。
* ローンチの昇格時に、昇格済みのローンチの変更が他のローンチに二重にロールアウトされます。 ユーザーがダブルロールアウトされたローンチを昇格すると、2倍のコンテンツがソースページに反映される(NPR-36893)。
* [!DNL Experience Manager] 画像コアコンポーネントを使用してページに画像を追加する場合、または基盤画像コンポーネントを使用してサイズを変更する場合に、透明性を持つ一部のPNG画像にグレーの境界線を追加します(NPR-36879)。
* [!DNL Experience Manager Sites] 多数のテンプレートを含む管理UIで、ナビゲーションが遅くなる(NPR-36870)。
* Service Pack 9にアップグレードすると、一部のコンポーネントがオーサリングされなくなります。 この問題では、[!DNL Sites]ユーザーが新しいページを作成できない(NPR-36857)。
* `ContextHubImpl`メソッドは、閉じられていない`ResourceResolver`を作成します。 長時間実行されている`ResourceResolver`に関する警告メッセージが表示され、サービスが予期しない結果を時々返す(NPR-36853)。
* ブループリントページのプロパティから1つのライブコピーを同期する際に、他のすべてのライブコピーも同期される(NPR-36829、NPR-36522)。
* XLSのMIMEタイプのみを使用する場合、ファイルのアップロード機能が期待どおりに動作しない(NPR-36785)。
* パスカルケースとすべて大文字の単語を含む新しいタグは、[!DNL Content Fragments]内のタグフィールドに表示されない(NPR-36742)。
* [!DNL Content Fragment]を追加すると、「単一のテキスト要素」オプションにより、テキストが欠落し、リストとネストされたリストに関連する奇数の書式が作成される(NPR-36565)。
* 作成者がページ上の任意のコンポーネントに注釈を付け、そのコンポーネントを削除し、削除操作で取り消しを実行すると、サイトコンソールでそのページのタイムラインデータを表示しようとするとエラーが発生する。(NPR-36528)
* ページプロパティバルクエディターの「[!UICONTROL 保存して閉じる]」オプションは変更を保存しますが、エディターは閉じません(NPR-36527)。
* ユーザーが新しいテキストコンポーネントをページにドラッグ&amp;ドロップしようとすると、そのコンポーネントが直ちに消える(NPR-36442)。
* スペースを含むオンデマンドタグ（システム上に存在しないタグ）にユーザーが入力してEnterキーを押すと、そのタグがフィールドの下に表示されます。 ただし、[!DNL Content Fragment]を保存して再び開くと、オンデマンドタグは表示されない(NPR-36441)。
* インスタンスがDispatcher経由でアクセスされる場合、テンプレートを削除できない。(NPR-36385)
* ページを移動する際に、変更をレンダリングするには、ブラウザーの手動更新が必要です(NPR-36381)。
* コンポーネントを選択する際に、Ctrl + XまたはCtrl + Cキー（Macの場合はCommand + XまたはCommand + Cキー）を使用して切り取りまたはコピーできます。 別のコンポーネントをクリックすると、ツールバーで貼り付けることができますが、キーボード（Ctrl + VまたはCommand + V）は貼り付けできません(NPR-36379)。
* ユーザーがはさみアイコンを使用してコンポーネントを切り取って別の場所に移動しようとすると、コンソールエラーが発生します。 また、1つのコンポーネントのみを貼り付けると、移動する(NPR-36378)。
* [!DNL Experience Manager] に、WCMまたは通知でインデックスのないクエリがある場合、パフォーマンスが低下する(NPR-36303)。
* 作成者が、削除された継承コンポーネントの継承を復元する場合、使用可能なオプションは、すべてのページコンテンツを同期することです。 継承が1つのコンポーネントでのみ復元された場合でも、コンテンツ作成者は完全なページを同期する必要があります。 完全な同期により、不要なコンテンツが同期される場合がある(NPR-34456、CQ-4310183)。
* オーサーインスタンス上のコンポーネントのライブ使用では、すべての回数が表示されるわけではありません。 1,000ページを超えるコンポーネントで使用されているコンポーネントもありますが、レポートには約40ページしか表示されません(CQ-4323724)。
* サブページが多いサイト構造の場合、列表示でのサブページの読み込みには、Experience Manager6.4.8.2に比べてExperience Manager6.5.8での時間が長くなります(CQ-4322766)。
* 「すべて」をオフにすると、「ページをロールアウト」オプションで「すべて」が機能しない(NPR-37070)。
* ページの既存のv3コンポーネントバージョンを開くと、ページのプロパティダイアログが開かず、`NullPointerException`がログに記録されます(SITES-1830)。

### [!DNL Assets] {#assets-65100}

[!DNL Assets]では、次の問題が修正されました。

* フォルダーを移動した後、パブリッシュインスタンス上でプロパティ`jcr:title`の値が更新されない。 オーサー内のフォルダーの名前を変更して再公開しても、パブリッシュインスタンス内の同じ`jcr:title`プロパティ値が更新されない(NPR-36369)。

* 2つ以上のアセットが選択され、1つ以上のメタデータフィールドが編集された場合、Safariブラウザーのエラーコード500で保存操作が失敗する。(NPR-36413)

* 日付の形式が正しくないため、一括メタデータの読み込みが失敗する。(NPR-36428)

* [!UICONTROL プロパティ]ページでメタデータを更新するように選択すると、スキーマが多くのオプションを提供する場合、インターフェイスの応答が遅くなる(NPR-36430)。

* [!UICONTROL 有効期限ステータス]述語を使用した検索フィルターが機能しない(NPR-36436)。

* [!UICONTROL フォルダーメタデータ]プロパティの様々なフィールドのポップアップメニューに、最後に選択された値が表示されない(NPR-36937、CQ-4314429)。

* ファイルとフォルダーを検索する際に、ユーザーがフィルターを適用し、「[!UICONTROL ファイルとフォルダー]」を選択した場合、ファイルのみが表示され、フォルダーは表示されません(CQ-4319543、NPR-36627)。

* フォルダー内から同じコレクションが選択されている場合と、検索結果から選択されている場合とで、ツールバーオプションが異なる。(NPR-36620)

* 「[!UICONTROL クイック公開]」オプションは、検索結果ページで使用できません(NPR-36904、CQ-4317748)。

* ユーザーが拡張子を指定せずにアセットのライブコピーを作成した場合、ダウンロード後にライブコピーファイルを使用できない(NPR-36903、CQ-4326305)。

* ユーザーが子フォルダーの所有者として追加されると、そのユーザーは親フォルダーの所有者権限も取得され、親の他の子フォルダーの所有者権限も取得されます。 また、ユーザーが親フォルダーを削除しようとしても、親フォルダーの所有者として削除されることはありません。 (NPR-36801、CQ-4323737)。

* [!DNL Experience Manager] PowerPointプレゼンテーションなどの複合アセットのサブアセットを作成しようとすると、メモリ不足例外が発生します(NPR-36668)。

* 公開済みのサイトページで既に使用されているアセットをユーザーが移動すると、公開するオプションが選択されていない場合でも、サイトページが再び公開される(NPR-36636、CQ-4323500)。

* Apache TikaのMIMEタイプ検出機能を使用する場合、`AssetManager.createAsset`メソッドを使用してアップロードされたアセットは、一時ディレクトリに`apache-tika-*.tmp`ファイルを残します。 この一時ファイルは、使用可能なすべての空きディスク領域を使用します(NPR-36545)。

* DRMで保護されたすべてのアセットがダウンロードされ、特定のアセットをダウンロードするためのユーザー選択は実行されません(CQ-4327422)。

* ユーザーインターフェイスの`pathfield`にアセットをドラッグできない。(NPR-36849)

* 列表示でアセットを選択すると、アセットの詳細パネルが表示されなくなる(NPR-36667)。

### [!DNL Dynamic Media] {#dynamic-media-65100}

**アクセシビリティの強化**

[!DNL Dynamic Media Viewers]では、次のアクセシビリティの強化を利用できます。

* スクリーンリーダーは、プレースホルダーテキストを読み上げ、リンクダイアログとして共有アセットの必須フィールドとして電子メールアドレスを検索して追加し、[!UICONTROL このフィールドに入力]ツールチップ(CQ-4327761)を読み上げます。

* スクリーンリーダーで、キーボードを使用してユーザーインターフェイスフィールドにアクセスする際に、[!UICONTROL 画像プリセットエディター]で様々なフィールドの名前と目的を正しく読み上げるようになりました(CQ-4325677)。

* [!UICONTROL リッチメディアタイプ]オプションのアセットピッカーから、[!UICONTROL ビューアプリセット]ダイアログボックスの「検索」タブにキーボードフォーカスが適切に移動するようになりました(CQ-4324736)。

* キーボードキーを使用してフォームモードで移動する場合、スクリーンリーダーは、[!UICONTROL 画像プリセット]の「[!UICONTROL 作成]」タブで、増分および減分オプションに対応するラベルを読み上げます(CQ-4323900)。

* スクリーンリーダーが、リンクダイアログボックスとしてアセットを共有する際に、「[!UICONTROL 電子メールアドレスを検索して追加]」オプションを読み上げるようになりました(CQ-4323352)。

* キーボードキーを使用してアセットを移動する際に、キーボードフォーカスがツールバーに保持される(CQ-4322037)。

* スクリーンリーダーは、[!UICONTROL 画像処理プロファイルを編集]ページの[!UICONTROL レスポンシブ画像切り抜き]内で「[!UICONTROL 切り抜き]を追加」オプションを選択した後、新しく追加された[!UICONTROL 編集]フィールド情報を読み上げるようになりました。(CQ-4290734

* [!UICONTROL 画像プリセットを編集]ページと[!UICONTROL インタラクティブビデオを作成]ページで、スクリーンリーダーが見出しキーボードショートカットキー(CQ-4290730)を使用してページを移動する際に、ページ見出しを適切に読み上げるようになりました(CQ-4290701)。

* スクリーンリーダーは、次のページを移動する際に、ランドマークキーと領域ショートカットキーを使用して、画面の様々な領域（右パネル領域、左パネル、アクションツールバー、ビューアツールバーのランドマーク、ズーム可能な画像のランドマークなど）を認識できるようになりました。

   * [!UICONTROL ビューアプリセットエディター] (CQ-4290729)

   * [!UICONTROL 画像セットエディター] (CQ-4290710)

   * [!UICONTROL インタラクティブビデオの作成] (CQ-4290702)。

* スクリーンリーダーは、下向き矢印キーを使用して移動する際に、ビデオフレームの共有オプションの名前を読み上げるようになりました(CQ-4290728)。

* スクリーンリーダーで、[!UICONTROL ビューアプリセットエディター]の「[!UICONTROL 外観]」タブの「[!UICONTROL Sprite]」タブと「[!UICONTROL 背景]」タブの様々なオプションの名前を読み上げるようになりました(CQ-4290727)。

* 必須フィールド（[!UICONTROL 幅]を編集するフィールドなど）が[!UICONTROL ビデオエンコーディングを編集]ページの「[!UICONTROL 基本]」タブに、アスタリスク記号(*)で表示されるようになりました(CQ-4290725)。

* スクリーンリーダーが、[!UICONTROL イメージプロファイル]ページのオプションのラベルを読み上げるようになりました(CQ-4290723)。

* Windowsユーザーは、CSSエディターにフォーカスがある場合、[!UICONTROL ビューアプリセットエディター]で、拡張されたCSSエディターから移動できるようになりました(CQ-4290720)。

* フォームモードで移動する際に、[!UICONTROL 「[!UICONTROL 画像プリセットを編集]」の「基本]」タブで、スクリーンリーダーが様々な編集フィールドおよびオプションのラベルを読み上げるようになりました(CQ-4290717)。

* スクリーンリーダーで、アセットの詳細ページの左側のナビゲーションにあるユーザーインターフェイスオプションの役割と状態（選択または未選択）を読み上げるようになりました(CQ-4290709)。

* スクリーンリーダーで、[!UICONTROL インタラクティブビデオを作成]ページの「[!UICONTROL コンテンツ]」タブで、状態（選択または未選択）と画像のリンク切り替えが正しく読み上げられるようになりました(CQ-4290707)。

* スクリーンリーダーで、[!UICONTROL インタラクティブビデオを作成]ページの下向き矢印キーを使用して移動する際に、ビデオタイムラインスケールの様々なセグメントの名前、役割、状態を正しくナレートできるようになりました(CQ-4290706)。

* スクリーンリーダーで、[!UICONTROL インタラクティブビデオを作成]ページ(CQ-4290704)のオプションを移動する際に、名前、役割、デフォルトの状態（選択済みまたは未選択）およびプロパティを読み上げるようになりました。

* スクリーンリーダーで、[!UICONTROL 公開]ページ(CQ-4290705)を移動する際に、「 [!UICONTROL すべてのアセット] 」および「 [!UICONTROL すべてのコレクション] 」オプションの名前、役割、デフォルトの状態（選択されているかどうか）を読み上げる。

* [!UICONTROL インタラクティブビデオを作成]ページにサポートされていないビデオ形式（MP4以外）をアップロードすると、Experience Managerがエラーメッセージを表示し、通知します(CQ-4290700)。

* [!UICONTROL インタラクティブビデオを作成]ページのタイムラインスケールの数値(時間（秒）)のコントラストが、最低限必要な輝度比を満たすようになり、色の知覚が限られたユーザーが簡単に読めるようになりました(CQ-4290699)。

* スクリーンリーダーは、[!UICONTROL インタラクティブビデオを作成]ページに移動する際に、「[!UICONTROL 製品名]」フィールドのラベルを読み上げるようになりました(CQ-4290697)。

**修正された問題**

[!DNL Dynamic Media]では、次のバグ修正を利用できます。

* `dynamicmedia_scene7`実行モードが有効になり、同期が無効になった後、[!DNL Experience Manager]に`Process failed`が表示されるようにビデオをアップロードしました(CQ-4327791)。

### プラットフォーム {#platform-65100}

このサービスパックでは、次の機能強化がおこなわれています。

* ユーザーがツリー表示で項目を選択すると、スクリーンリーダーは選択と、上部に表示されるツールバーオプションを読み上げる(NPR-36504)。
* 明度の比率が最小要件の4.5:1を満たすので、視覚に問題があるユーザーは、テキストやコントロール名の読みやすさがあります(NPR-36503)。
* ユーザーがカレンダーコントロールを使用する場合、スクリーンリーダーは、記述的な日付、月、曜日の情報をナレーションします。 ユーザーがカレンダーショートカットキーを使用すると、スクリーンリーダーが日付、月、年の変更をナレーションする(NPR-36498)。
* ECMAScript 6の機能を使用して、厳密なモードに準拠せずにカスタムJavaScript `Clientlibs`を実行するためのサポートが提供されました。 具体的には、`emitUseStrict`フラグを`GCCScriptProcessor`に追加する(NPR-36411)。

このサービスパックには、次のバグ修正が含まれています。

* カスタムヘルスチェックは、スケジュールよりも頻繁に実行されます(NPR-36985)。
* `Resourceresolver map`メソッドがエイリアスページに対して誤った結果を返す(NPR-36767)。
* [!DNL Experience Manager] ワークフローの読み込みが原因で起動が遅延する(NPR-36615)。

### 統合 {#integrations-65100}

* Experience Managerは、プライマリMongoDBノードが別のノードに切り替えると応答しなくなる(NPR-36566)。
* [!DNL Sling content distribution] コレクションメンバーの削除操作の実行時に失敗する(NPR-36521、CQ-4323578)。

### ユーザーインターフェイス {#user-interface-65100}

* **[!UICONTROL 参照]**&#x200B;サイドパネルには、アセットとサイトの参照が表示されません(GRANITE-35078、GRANITE-34892)。

### 翻訳プロジェクト {#translation-65100}

* マルチ翻訳プロジェクトの言語コピーの余分なサブページが削除される(NPR-36622)。

### ワークフロー {#workflow-65100}

* サーバーが不在メッセージを受け取ると、メモリアラートを報告し、応答を停止する(NPR-36768)。

### [!DNL Communities] {#communities-65100}

* コミュニティサイトページが、匿名のゲストユーザーに対して`LoggedIn`状態で開かれる(NPR-36908)。

* **[!UICONTROL コミュニティ]** / **[!UICONTROL アイデア]** / **[!UICONTROL コメント]**&#x200B;ページに複数のページが存在する場合、ページナビゲーションが機能しない(NPR-36541)。

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


**アダプティブフォーム**

* アダプティブフォームのフィールド値に対して実行された検証が正常に完了した場合、[!DNL AEM Forms]はフォームデータモデルの呼び出しに失敗します(CQ-4325491)。

* 翻訳プロジェクトに言語辞書を追加してからプロジェクトを開くと、[!DNL AEM Forms]にエラーメッセージが表示されます(CQ-4324933)。

   ```TXT
   Uncaught TypeError: Cannot read property 'PROJECT_LISTING_PATH' of undefined
   at openButtonClickHandler (clientlibs.js:245)
   at HTMLButtonElement.onclick (clientlibs.js:258)
   ```

* [!DNL AEM Forms] Service Pack 7をインストールした後のパフォーマンスの問題(CQ-4326828)。

**Correspondence Management**

* 「[!UICONTROL データ]」タブおよびHTMLレタープレビューでの文字表示の遅延(NPR-37020)。

* テキストドキュメントフラグメントを編集している場合、フラグメントを保存すると、新しい単語がHTMLタグとして表示される(NPR-36837)。

* ドラフトとして保存されたレターを表示できない(NPR-36816)。

* テキストドキュメントフラグメントを編集してレターをプレビューすると、AEM FormsはHTMLレタープレビューに式言語を表示します(CQ-4322331)。

* セルフサービスレターテンプレートを使用してデータをレンダリングする際の問題(NPR-37161)。


**インタラクティブコミュニケーション**

* テキストドキュメントフラグメントの編集後にインタラクティブ通信のプレビューを印刷するたびに、タブ文字が2つの単語間で重複する(NPR-37021)。

* [!DNL AEM Forms] 最大サイズ制限を超えるテキストドキュメントフラグメントを保存すると、エラーが表示される(NPR-36874)。

* インタラクティブ通信に画像を追加すると、画像の後に追加の空のブロックが表示される(NPR-36659)。

* エディターですべてのテキストを選択すると、フォントテキストをArialに変更できない(NPR-36646)。

* エディターでURLを作成し、変更をプレビューすると、URLテキストの代わりに黒い背景が表示される(NPR-36640)。

* テキストをエディターにコピー&amp;ペーストする際、ドキュメントで使用可能な箇条書きのフォントをArialに変更する際に問題が発生する。(NPR-36628)

* テキストエディターでの箇条書きのインデントの問題(NPR-36513)。

**デザイナー**

* 画面Readerが、マスターページ上のテキストラベルまたはダイナミックPDFのサブフォームページに配置されたフローティングフィールドデータを読み取れない(CQ-4321587)。

**ドキュメントサービス**

* XDPファイルをPDFファイルに変換し、結果のPDFをアセンブリすると、PDFの生成に失敗し、次のエラーメッセージが表示されます。

   ```TXT
   Caused by: com.adobe.fd.assembler.client.AssemblerException$ClientException: Document is in a disposed state!
   ```

**Forms のワークフロー**

* AEM Forms Service Pack 8にアップグレードした後、Workbenchプロセスにフォームを送信できない(CQ-4325846)。

**HTML5 のフォーム**

* CRX DEリポジトリで`mfAllowAttachments`プロパティの値を`True`に設定すると、HTML5フォームの送信時に`dataXml`が破損する(NPR-37035)。

* `dataXml`を使用してXDPをHTMLとしてレンダリングする場合、[!DNL AEM Forms]は`Page Unresponsive`エラーを表示します(NPR-36631)。

### コマース {#commerce-65100}

* 表示される&#x200B;**[!UICONTROL 「Published By]**」フィールドの値が列表示で正しくない。(NPR-36902)
* カタログがロールアウトされると、新しい製品が誤って変更された製品としてマークされる(NPR-36666)。
* 削除した製品を再作成しても、製品ページが再作成されない(NPR-36665)。
* 変更されたページは更新されますが、対応するリンクされた製品がカタログのロールアウトで更新されません(CQ-4321409、NPR-36422)。
* **[!UICONTROL 後で公開]**&#x200B;および&#x200B;**[!UICONTROL 後で非公開]**&#x200B;のワークフローは機能しません(CQ-4327679)。

セキュリティ更新について詳しくは、[[!DNL Experience Manager] セキュリティ速報ページ](https://helpx.adobe.com/security/products/experience-manager.html)を参照してください。

## 6.5.10.0 のインストール {#install}

**設定要件と詳細情報**

* Experience Manager6.5.10.0にはExperience Manager6.5が必要です。詳細な手順については、[アップグレードのドキュメント](/help/sites-deploying/upgrade.md)を参照してください。
* サービスパックのダウンロードは、Adobe[「Software Distribution」](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)で入手できます。
* MongoDBおよび複数のインスタンスを使用したデプロイメントで、パッケージマネージャーを使用して、いずれかのオーサーインスタンスにExperience Manager6.5.10.0をインストールします。

>[!NOTE]
>
>Adobeは、[!DNL Adobe Experience Manager] 6.5.10.0パッケージの削除またはアンインストールはお勧めしません。

### サービスパックのインストール {#install-service-pack}

[!DNL Adobe Experience Manager] 6.5インスタンスにService Packをインストールするには、次の手順に従います。

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 Adobeでは、インスタンスの現在の稼動時間が長い場合に再起動を推奨します。

1. インストールする前に、[!DNL Experience Manager]インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip)からサービスパックをダウンロードします。

1. パッケージマネージャーを開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

1. S3コネクタを更新するには、Service Packのインストール後にインスタンスを停止し、既存のコネクタをinstallフォルダーに用意されている新しいバイナリファイルで置き換えて、インスタンスを再起動します。 [Amazon S3データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャーUIのダイアログが終了することがあります。 Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデータバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認します。 通常、この問題は[!DNL Safari]ブラウザーで発生しますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.10.0を作業インスタンスに自動的にインストールする方法は2つあります。

A.サーバーがオンラインで使用可能になったら、 `../crx-quickstart/install`フォルダーにパッケージを配置します。 パッケージが自動的にインストールされます。

B.パッケージマネージャーの[HTTP APIを使用します。](/help/sites-administering/package-manager.md#package-share) `cmd=install&recursive=true`を使用して、ネストされたパッケージをインストールします。

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0は、Bootstrapのインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ(`/system/console/productinfo`)に、[!UICONTROL インストール済みの製品]の下に、更新されたバージョン文字列`Adobe Experience Manager (6.5.10.0)`が表示されます。

1. OSGiコンソール内のOSGiバンドルは、すべて&#x200B;**[!UICONTROL ACTIVE]**&#x200B;または&#x200B;**[!UICONTROL FRAGMENT]**&#x200B;です(Webコンソールを使用：`/system/console/bundles`)です。

1. OSGiバンドル`org.apache.jackrabbit.oak-core`は、バージョン1.22.3以降です(Webコンソールを使用：`/system/console/bundles`)です。

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

### Adobe Experience Manager Formsアドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Formsを使用していない場合はスキップします。 Experience ManagerFormsの修正は、スケジュールされた[!DNL Experience Manager] Service Packリリースの1週間後に、別のアドオンパッケージを通じて配信されます。

1. Adobe Experience Manager Service Packがインストールされていることを確認します。
1. [AEM Forms リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. [AEM Formsアドオンパッケージのインストール](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)の説明に従って、Formsアドオンパッケージをインストールします。

>[!NOTE]
>
>Experience Manager6.5.10.0には、[AEM Forms互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases)の新しいバージョンが含まれています。 古いバージョンのAEM Forms互換パッケージを使用し、Experience Manager6.5.10.0に更新する場合は、Formsアドオンパッケージのインストール後に、最新バージョンのパッケージをインストールします。

### JEEへのAdobe Experience Manager Formsのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE上のAdobe Experience Manager Formsの修正は、別のインストーラーを使用して提供されます。

JEE上のFormsExperience Manager用の累積インストーラーのインストールとデプロイ後の設定について詳しくは、[リリースノート](jee-patch-installer-65.md)を参照してください。

>[!NOTE]
>
>JEE上のFormsExperience Manager用の累積インストーラーをインストールしたら、最新のFormsアドオンパッケージをインストールし、`crx-repository\install`フォルダーからFormsアドオンパッケージを削除して、サーバーを再起動します。


### UberJar {#uber-jar}

Experience Manager6.5.10.0のUberJarは、[Maven Centralリポジトリ](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/)で入手できます。

MavenプロジェクトでUberJarを使用するには、[UberJar](/help/sites-developing/ht-projects-maven.md)の使用方法を参照し、プロジェクトPOMに次の依存関係を含めます。

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
>UberJarおよびその他の関連アーティファクトは、AdobeのパブリックMavenリポジトリ(`repo.adobe.com`)ではなく、Maven Centralリポジトリで使用できます。 メインのUberJarファイルの名前が`uber-jar-<version>.jar`に変更されます。 したがって、`dependency`タグには`apis`を値とする`classifier`はありません。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

[!DNL Experience Manager] 6.5.7.0で非推奨とマークされた機能の一覧を以下に示します。機能は、最初に廃止され、後で将来のリリースで削除されます。 別のオプションが提供されます。

機能または機能をデプロイメントで使用するかどうかを確認します。 また、別のオプションを使用するように実装を変更することを計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | **[!UICONTROL AEM Cloud Servicesオプトイン]**&#x200B;画面は廃止されました。Experience Manager6.5では[!DNL Experience Manager]と[!DNL Adobe Target]の統合が更新されているためです。この統合は、Adobe Target Standard APIをサポートしています。 APIは、Adobe IMSと[!DNL Adobe I/O]を介したAdobeを使用し、分析やパーソナライゼーション用に[!DNL Experience Manager]ページを実装するために、認証開始の役割の拡大をサポートしています。オプトインウィザードは、機能的に無関係です。 | 各[!DNL Experience Manager]クラウドサービスを使用して、システム接続、Adobe IMS認証、[!DNL Adobe I/O]統合を設定します。 |
| コネクタ | Experience Manager6.5では、Microsoft® SharePoint 2010およびMicrosoft® SharePoint 2013用のAdobeJCR Connectorが非推奨（廃止予定）となりました。 | 該当なし |

## 既知の問題 {#known-issues}

* [!DNL Microsoft Windows Server 2019]は[!DNL MySQL 5.7]と[!DNL JBoss EAP 7.1]をサポートしていないので、[!DNL Microsoft Windows Server 2019]は[!DNL AEM Forms 6.5.10.0]の自動インストールをサポートしていません。

* [!DNL Experience Manager]インスタンスを6.5から6.5.10.0バージョンにアップグレードする場合は、`error.log`ファイルで`RRD4JReporter`例外を表示できます。 この問題を解決するには、インスタンスを再起動します。

* [!DNL Experience Manager] 6.5 Service Pack 10または以前のService Packを[!DNL Experience Manager] 6.5にインストールすると、（`/var/workflow/models/dam`で作成された）アセットカスタムワークフローモデルのランタイムコピーが削除されます。
ランタイムコピーを取得するには、HTTP APIを使用して、カスタムワークフローモデルのデザイン時コピーをそのランタイムコピーと同期することをお勧めします。
   `<designModelPath>/jcr:content.generate.json`。

* ユーザーは、[!DNL Assets]の階層内のフォルダーの名前を変更し、ネストされたフォルダーを[!DNL Brand Portal]に公開できます。 ただし、[!DNL Brand Portal]では、ルートフォルダーが再公開されるまで、フォルダーのタイトルは更新されません。

* アダプティブフォームで初めてフィールドの設定を選択した場合、設定を保存するオプションはプロパティブラウザーに表示されません。 同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。

* Experience Manager6.5.x.xのインストール中に、次のエラーおよび警告メッセージが表示される場合があります。
   * 「Adobe Target統合がTarget Standard API（IMS認証）を使用してExperience Managerで設定されている場合、エクスペリエンスフラグメントをTargetに書き出すと、間違ったオファータイプが作成されます。 Target では、「エクスペリエンスフラグメント」/source「Adobe Experience Manager」タイプではなく、「HTML」/source「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MINなどの集計関数が使用されると、アダプティブフォームのサーバー側検証が失敗します(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューすると、Dynamic Mediaのインタラクティブ画像のホットスポットが表示されない。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :登録変更が完了するのを待機中のタイムアウトが未登録です。

## OSGiバンドルとコンテンツパッケージが含まれています {#osgi-bundles-and-content-packages-included}

以下のテキストドキュメントは、[!DNL Experience Manager] 6.5.10.0に含まれるOSGiバンドルとコンテンツパッケージの一覧です。

* [Experience Manager6.5.10.0に含まれているOSGiバンドルの一覧](assets/65100_bundles.txt)

* [Experience Manager6.5.10.0に含まれているコンテンツパッケージの一覧](assets/65100_packages.txt)

## 制限付きWebサイト {#restricted-sites}

これらのWebサイトは、お客様のみが利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [Adobeカスタマーケアへの問い合わせ方法](https://experienceleague.adobe.com/docs/customer-one/using/home.html)を参照してください。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5リリースノート](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [Adobe Priority 製品アップデート](https://www.adobe.com/subscription/priority-product-update.html)のサブスクリプションを購入する

