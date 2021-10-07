---
title: '[!DNL Experience Manager] 6.5 サービスパックリリースノート'
description: リリースノート（ [!DNL Adobe Experience Manager] 6.5 Service Pack 10 固有）
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 99d38dddbcd06fecb82c744d446b9cef981e0781
workflow-type: tm+mt
source-wordcount: '4392'
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

## [!DNL Adobe Experience Manager] 6.5.10.0に含まれるもの {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.10.0には、2019 年 4 月の 6.5 リリースのリリース以降にリリースされた新機能、お客様からリクエストされた主な機能強化、パフォーマンス、安定性、セキュリティの改善が含まれています。サービスパックは [!DNL Adobe Experience Manager] 6.5 にインストールされています。

[!DNL Adobe Experience Manager] 6.5.10.0で導入された主な機能と機能強化は次のとおりです。

* **拡張モ [!DNL Content Fragment] デルとエディター**:ネストされたモデルを使用して、構造化コンテンツ用の複雑なモデルやカスタムモデルを作成できるよう [!DNL Content Fragment] になりました。コンテンツ構造は、サブフラグメントとしてモデル化された基本要素にモジュール化されます。 上位のフラグメントは、これらのサブフラグメントを参照します。 高度な検証ルールなど、データタイプの機能強化が増えると、[!DNL Content Fragments] を使用したコンテンツモデリングの柔軟性がさらに向上します。 [!DNL Experience Manager] [!DNL Content Fragment] エディターは、共通のエディターセッションでネストされたフラグメント構造をサポートし、構造ツリー表示やフラグメント階層でのタブ付きパンくずナビゲーションなどの機能が強化されました。

* **GraphQL API( 以下[!DNL Content Fragments]**&#x200B;の ):新しい GraphQL API は、構造化コンテンツを JSON 形式で配信する標準の方法です。GraphQL クエリを使用すると、クライアントは、エクスペリエンスをレンダリングする関連するコンテンツ項目のみを要求できます。 このように選択すると、クライアント側でのコンテンツ解析を必要とするコンテンツの過剰配信（HTTP REST API で使用可能）が排除されます。 GraphQL スキーマは [!DNL Content Fragment] モデルから派生し、API 応答は JSON 形式でおこなわれます。 [!DNL Experience Manager] では、[!DNL Cloud Service] として [GraphQL クエリは ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) 保持され、キャッシュに適したGETリクエストを処理します。 [!DNL Experience Manager] 6.5.10.0ではまだ可能ではありません。

* **階層の管理と将来のプレビュー**:ローンチのページの追加や削除機能を含む、ローンチのコン [!DNL Experience Manager] テンツ構造にアクセスするためのインターフェイスが追加されました。この機能により、[!DNL Experience Manager] ローンチの柔軟性が高まり、今後の公開をターゲットとしたコンテンツバージョンを作成できます。 [タイムワープ機能を使用す](/help/sites-authoring/working-with-page-versions.md#timewarp) ると、ユーザーはローンチを将来のコンテンツ状態としてプレビューできます。

* **Connected Assets**: [!DNL Experience Manager] は、適用可 [!DNL Connected Assets] 能なコアコンポーネ [!DNL Dynamic Media] ントでの画像の使用に対して機能を拡張します。「[Connected Assets の使用](/help/assets/use-assets-across-connected-assets-instances.md)」を参照してください。

* **アセットまたはレンディションをダウンロードするためのリンク共有オプション**:アセットとコレクションをリンクとして共有する場合、元のアセットのダウンロードを許可するか、レンディションのダウンロードを許可するか、共有リンクを使用して両方を許可するかを選択できます。また、リンクを通じて自分と共有されているアセットをダウンロードしたユーザーは、元のアセットのみ、レンディションのみ、またはその両方をダウンロードするオプションが表示されます。

* **生成されるサブアセットの制限**:管理者は、PDF、PowerPoint、InDesign、Keynote ファイルな [!DNL Experience Manager] ど、複合アセットに対して生成されるサブアセットの数を制限できます。[ 複合アセットの管理 ](/help/assets/managing-linked-subassets.md#generate-subassets) を参照してください。

* **Camera Rawサポート**:新しいパッ [!DNL Camera Raw] ケージが利用でき、 [!DNL Adobe Camera Raw] v10.4 をサポートします。 [を使用した画像 [!DNL Camera Raw]](/help/assets/camera-raw.md)の処理を参照してください。

* 組み込み型のリポジトリ (Apache Jackrabbit Oak) が1.22.8に更新されます。

* **アクセシビリティの強化**:

   * [!DNL Dynamic Media] では、ビューアのアクセシビリティが多く強化されています。[[!DNL Dynamic Media]  更新 ](#dynamic-media-65100) を参照してください。

   * Platform では、アクセシビリティがいくつか強化されています。 [ プラットフォームの更新 ](#platform-65100) を参照してください。

* **ユーザーエクスペリエンスの強化**:

   * [!DNL Experience Manager] は、フォルダーの下にすべてのコンテンツモデルのリストを直接表示します。コンテンツ作成者はファイル構造内を移動する必要はありません。この機能により、クリック数が少なくなり、オーサリングの効率が向上しました。

   * [!DNL Sites] エディターのパスフィールドを使用すると、作成者は [!DNL Content Finder] からアセットをドラッグできます。

* [!DNL AEM Forms] に `GuideBridge#getGuidePath` API のサポートを追加しました。

* automated forms conversionサービスを使用して、アダプティブフォームに [PDF formsをフランス語、ドイツ語、スペイン語、イタリア語、ポルトガル語の各言語に変換できるようになりました。](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html#language-specific-meta-model)

* **プロパティブラウザーのエラーメッセージ**：アダプティブフォームのプロパティブラウザーに各プロパティのエラーメッセージが追加されました。これらのメッセージは、フィールドに使用できる値を理解するのに役立ちます。

* **リテラルオプションを使用して JSON タイプの変数の値を設定する機能**&#x200B;をサポートします。リテラルオプションを使用して、AEM Workflow の変数設定手順で JSON タイプの変数の値を設定できます。リテラルオプションを使用すると、文字列の形式で JSON を指定できます。

* [プラットフォームのアップデート](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] JEE 上では、次のプラットフォームのサポートが追加されました。
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

[!DNL Experience Manager] 6.5.10.0で導入されたすべての機能と機能強化の一覧については、 [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md) の新機能を参照してください。[

[!DNL Experience Manager] 6.5.10.0リリースで提供された修正の一覧を次に示します。

### [!DNL Sites] {#sites-65100}

* コンテンツフラグメントエディターの「**[!UICONTROL プロパティ]**」タブの下の「**[!UICONTROL デフォルト値]**」フィールドに入力すると、フォーカスが別のフィールドに移動する (NPR-36992)。

* 指定されたパスで [!DNL Content Fragment] モデルをフィルタリングする際、[!DNL Experience Manager] 検索は、[!DNL Content Fragment] モデル (SITES-1453) のみのパスとノードを返す代わりに、`cq:Template` を含むすべてのノードを返します。
* [!DNL Content Fragments] をフォ `null` ルダーのステータスとして返します (SITES-1157)。
* [!DNL Experience Manager] では、ユーザーはモデルの無効化と [!DNL Content Fragment] 有効化をおこなえません (SITES-1088)。
* ユーザーが [!DNL Content Fragments] やメディアアセットを移動、名前変更、削除した場合、参照されている [!DNL Content Fragments] は自動的には更新されません (SITES-196)。
* あるページから別のページにコンポーネントを貼り付けると、JavaScript エラーが発生する (NPR-37030)。
* ページのプロパティがすばやく表示されると、別のページのページプロパティが開かれる (NPR-37025)。
* コンテンツフラグメントを使用すると、コンテンツフラグメント自体を参照できます。 ピッカーが操作をサポートしていない (NPR-36993)。
* Service Pack 9 にアップグレードした後、一部のユーザーはExperience Manager内でフォルダを移動できず、ログにエラーが表示される (SITES-1481)。
* 編集モードでレイアウトコンテナ内のコンポーネントの幅を調整する際に、ちらつきが発生する (NPR-36961)。
* ローンチを昇格すると、昇格されたローンチの変更が他のローンチに二重にロールアウトされます。 ユーザーがダブルロールアウトされたローンチを昇格すると、2 倍のコンテンツがソースページに反映される (NPR-36893)。
* [!DNL Experience Manager] 画像コアコンポーネントを使用してページに画像を追加する場合、または基盤画像コンポーネントを使用してサイズを変更する場合に、透明性を持つ一部の PNG 画像にグレーの境界線を追加します (NPR-36879)。
* [!DNL Experience Manager Sites] テンプレートの数が多い管理 UI で、ナビゲーションが遅くなる (NPR-36870)。
* Service Pack 9 にアップグレードすると、一部のコンポーネントのオーサリングが妨げられます。 この問題により、[!DNL Sites] ユーザーが新しいページを作成できない (NPR-36857)。
* `ContextHubImpl` メソッドは、閉じられていない `ResourceResolver` を作成します。 長時間実行される `ResourceResolver` に関する警告メッセージが表示され、サービスが予期しない結果を時々返す (NPR-36853)。
* ブループリントページのプロパティから 1 つのライブコピーを同期すると、他のすべてのライブコピーも同期される (NPR-36829、NPR-36522)。
* XLS の MIME タイプのみを使用した場合、ファイルのアップロード機能が期待どおりに動作しない (NPR-36785)。
* パスケースとすべて大文字の単語を含む新しいタグは、[!DNL Content Fragments] 内のタグフィールドに表示されない (NPR-36742)。
* [!DNL Content Fragment] を追加すると、「単一のテキスト要素」オプションにより、テキストが欠落し、リストとネストされたリストに関連する奇数の書式が作成される (NPR-36565)。
* 作成者がページ上の任意のコンポーネントに注釈を付け、そのコンポーネントを削除し、削除操作で取り消しを実行すると、サイトコンソールでそのページのタイムラインデータを表示しようとするとエラーが発生する。(NPR-36528)
* ページプロパティバルクエディターの「[!UICONTROL  保存して閉じる ]」オプションは変更を保存しますが、エディターは閉じません (NPR-36527)。
* ユーザーが新しいテキストコンポーネントをページにドラッグ&amp;ドロップしようとすると、そのコンポーネントが直ちに消える (NPR-36442)。
* スペース（システムに存在しないタグ）を含むオンデマンドタグにユーザーが入力して Enter キーを押すと、そのタグがフィールドの下に表示されます。 ただし、[!DNL Content Fragment] を保存して再び開くと、オンデマンドタグは表示されない (NPR-36441)。
* インスタンスが Dispatcher 経由でアクセスされる場合、テンプレートは削除できません (NPR-36385)。
* ページを移動する際に、変更をレンダリングするには、ブラウザーを手動で更新する必要がある (NPR-36381)。
* コンポーネントを選択する際に、Ctrl + X または Ctrl + C(Macの Command + X または Command + C) を使用して切り取りまたはコピーできます。 別のコンポーネントをクリックすると、ツールバーで貼り付けることができますが、キーボード（Ctrl + V または Command + V）では貼り付けできません (NPR-36379)。
* ユーザーがはさみアイコンを使用してコンポーネントを切り取って別の場所に移動しようとすると、コンソールエラーが発生します。 また、1 つのコンポーネントのみを貼り付けると、移動する (NPR-36378)。
* [!DNL Experience Manager] に、WCM または通知でインデックスのないクエリがある場合、パフォーマンスが低下する (NPR-36303)。
* 作成者が、削除された継承コンポーネントの継承を復元する場合、使用可能なオプションは、すべてのページコンテンツを同期することです。 継承が 1 つのコンポーネントでのみ復元された場合でも、コンテンツ作成者はページ全体を同期する必要があります。 完全な同期を行うと、不要なコンテンツが同期される場合がある (NPR-34456、CQ-4310183)。
* オーサーインスタンス上のコンポーネントのライブ使用では、すべてのオカレンスが表示されるわけではありません。 1,000 ページを超えるページで使用されているコンポーネントもありますが、レポートには約 40 ページしか表示されません (CQ-4323724)。
* サブページが多数あるサイト構造の場合、列表示でのサブページの読み込みには、Experience Manager6.4.8.2 に比べて、Experience Manager6.5.8 での時間が長くなります (CQ-4322766)。
* 「すべて」をオフにすると、「ページをロールアウト」オプションが機能しない (NPR-37070)。
* ページの既存の v3 コンポーネントバージョンを開くと、ページのプロパティダイアログが開かず、`NullPointerException` がログに記録されます (SITES-1830)。

### [!DNL Assets] {#assets-65100}

[!DNL Assets] では、次の問題が修正されました。

* フォルダーを移動した後、パブリッシュインスタンスでプロパティ `jcr:title` の値が更新されない。 オーサーインスタンス内のフォルダーの名前を変更して再公開しても、パブリッシュインスタンス内の同じ `jcr:title` プロパティ値は更新されません (NPR-36369)。

* 2 つ以上のアセットを選択し、1 つ以上のメタデータフィールドが編集された場合、Safari ブラウザーのエラーコード 500 で保存操作が失敗する。(NPR-36413)

* 日付の形式が正しくないため、一括メタデータの読み込みが失敗する (NPR-36428)。

* [!UICONTROL  プロパティ ] ページでメタデータを更新するように選択すると、スキーマが多くのオプションを提供する場合、インターフェイスの応答が遅くなる (NPR-36430)。

* [!UICONTROL  有効期限ステータス ] 述語を使用した検索フィルターが機能しない (NPR-36436)。

* [!UICONTROL  フォルダーメタデータ ] プロパティの様々なフィールドのポップアップメニューに、最後に選択した値が表示されない (NPR-36937、CQ-4314429)。

* ファイルとフォルダーを検索する際に、フィルターを適用し、「[!UICONTROL  ファイルとフォルダー ]」を選択した場合、ファイルのみが表示され、フォルダーは表示されません (CQ-4319543、NPR-36627)。

* フォルダー内で同じコレクションが選択されている場合と、検索結果から選択されている場合で、ツールバーのオプションが異なる (NPR-36620)。

* 「[!UICONTROL  クイック公開 ]」オプションは、検索結果ページで使用できません (NPR-36904、CQ-4317748)。

* ユーザーが拡張子を指定せずにアセットのライブコピーを作成した場合、ダウンロード後にライブコピーファイルを使用できない (NPR-36903、CQ-4326305)。

* ユーザーが子フォルダーの所有者として追加されると、そのユーザーは親フォルダーの所有者権限を取得します。つまり、親の他の子フォルダーの所有者権限を取得します。 また、ユーザーが削除を試みても、親フォルダーの所有者として削除されることはありません。 (NPR-36801、CQ-4323737)。

* [!DNL Experience Manager] PowerPoint プレゼンテーションなどの複合アセットのサブアセットを作成しようとすると、メモリ不足の例外が発生します (NPR-36668)。

* 公開済みのサイトページで既に使用されているアセットをユーザーが移動すると、公開するオプションが選択されていない場合でも、サイトページが再び公開されます (NPR-36636、CQ-4323500)。

* Apache Tika の MIME タイプ検出機能を使用する場合、`AssetManager.createAsset` メソッドを使用してアップロードされたアセットは、一時ディレクトリに `apache-tika-*.tmp` という名前の一時ファイルを残します。 この一時ファイルは、使用可能なすべての空きディスク領域を使用します (NPR-36545)。

* DRM で保護されたすべてのアセットがダウンロードされ、特定のアセットをダウンロードするためのユーザー選択に従いません (CQ-4327422)。

* ユーザーインターフェイスの `pathfield` にアセットをドラッグできない。(NPR-36849)

* 列表示でアセットを選択すると、アセットの詳細パネルが表示されなくなる (NPR-36667)。

### [!DNL Dynamic Media] {#dynamic-media-65100}

**アクセシビリティの強化**

[!DNL Dynamic Media Viewers] では、次のアクセシビリティの強化が利用できます。

* スクリーンリーダーは、プレースホルダーテキストを読み上げ、アセットを共有する際に必須フィールドとして電子メールアドレスを検索して追加し、[!UICONTROL  このフィールドに入力 ] ツールチップ (CQ-4327761) を読み上げます。

* スクリーンリーダーが、キーボードを使用してユーザーインターフェイスフィールドにアクセスする際に、[!UICONTROL  画像プリセットエディター ] で、様々なフィールドの名前と目的を正しく読み上げるようになりました (CQ-4325677)。

* [!UICONTROL  リッチメディアタイプ ] オプションのアセットピッカーから、[!UICONTROL  ビューアプリセット ] ダイアログボックスの「検索」タブにキーボードフォーカスが適切に移動するようになりました (CQ-4324736)。

* キーボードキーを使用してフォームモードで移動する場合、スクリーンリーダーは、[!UICONTROL  画像プリセット ] の「[!UICONTROL  作成 ]」タブで、増減オプションに対応するラベルを読み上げます (CQ-4323900)。

* スクリーンリーダーが、アセットをリンクダイアログボックスとして共有する際に、「[!UICONTROL  電子メールアドレスを検索して追加 ]」オプションを読み上げるようになりました (CQ-4323352)。

* キーボードキーを使用してアセットを移動する際に、ツールバーのキーボードフォーカスが保持される (CQ-4322037)。

* スクリーンリーダーは、[!UICONTROL  画像処理プロファイルを編集 ] ページの [!UICONTROL  レスポンシブ画像切り抜き ] 内で [!UICONTROL  切り抜き ] を追加オプションを選択した後、新しく追加した [!UICONTROL  編集 ] フィールド情報を読み上げるようになりました。(CQ-4290734)

* [!UICONTROL  画像プリセットを編集 ] ページと [!UICONTROL  インタラクティブビデオを作成 ] ページで、スクリーンリーダーが見出しキーボードショートカットキーを使用してページを移動する際に、ページ見出しを適切に読み上げるようになりました (CQ-4290730)(CQ-4290701)。

* スクリーンリーダーは、次のページを移動する際に、ランドマークキーと領域ショートカットキーを使用して、画面の様々な領域（右パネル領域、左パネル、アクションツールバー、ビューアツールバーのランドマーク、ズーム可能な画像のランドマークなど）を認識できるようになりました。

   * [!UICONTROL ビューアプリセットエディター] (CQ-4290729)

   * [!UICONTROL 画像セットエディター] (CQ-4290710)

   * [!UICONTROL インタラクティブビデオの作成] (CQ-4290702)。

* スクリーンリーダーは、下向き矢印キーを使用して移動する際に、ビデオフレームの共有オプションの名前を読み上げるようになりました (CQ-4290728)。

* スクリーンリーダーは、[!UICONTROL  ビューアプリセットエディター ] の [!UICONTROL  外観 ] タブの [!UICONTROL Sprite] タブと [!UICONTROL  背景 ] タブで、様々なオプションの名前を読み上げるようになりました (CQ-4290727)。

* [!UICONTROL  ビデオエンコーディングを編集 ] ページの [!UICONTROL  基本 ] タブで、[!UICONTROL  幅 ] を編集するフィールドなどの必須フィールドに、アスタリスク記号 (*) が付きます (CQ-4290725)。

* スクリーンリーダーが、[!UICONTROL  イメージプロファイル ] ページのオプションのラベルを読み上げるようになりました (CQ-4290723)。

* Windows ユーザーは、CSS エディターにフォーカスがある場合、[!UICONTROL  ビューアプリセットエディター ] で、拡張された CSS エディターから移動できるようになりました (CQ-4290720)。

* フォームモードで移動する際、[!UICONTROL 「[!UICONTROL  画像プリセットを編集 ]」の「 基本 ]」タブで、スクリーンリーダーが様々な編集フィールドおよびオプションのラベルを読み上げるようになりました (CQ-4290717)。

* スクリーンリーダーが、アセットの詳細ページの左側のナビゲーションで、ユーザーインターフェイスオプションの役割と状態（選択または未選択）を読み上げるようになりました (CQ-4290709)。

* スクリーンリーダーで、状態（選択された、選択されていない）を正しく読み上げ、画像のリンクを切り替えるように、 [!UICONTROL  インタラクティブビデオを作成 ] ページ (CQ-4290707) の「[!UICONTROL  コンテンツ ]」タブを開きます。

* スクリーンリーダーが [!UICONTROL  インタラクティブビデオを作成 ] ページの下向き矢印キーを使用して移動する際に、ビデオタイムラインスケールで様々なセグメントの名前、役割、状態を正しくナレーションできるようになりました (CQ-4290706)。

* スクリーンリーダーは、[!UICONTROL  インタラクティブビデオを作成 ] ページ (CQ-4290704) でオプションを移動する際に、名前、役割、デフォルトの状態（選択済みまたは未選択）およびプロパティを読み上げるようになりました。

* スクリーンリーダーで、[!UICONTROL  公開 ] ページ (CQ-4290705) を移動する際に、「 [!UICONTROL  すべてのアセット ] 」および「 [!UICONTROL  すべてのコレクション ] 」オプションの名前、役割、デフォルトの状態（選択または未選択）を読み上げるようになりました。

* [!UICONTROL  インタラクティブビデオを作成 ] ページにサポートされていないビデオ形式（MP4 以外）をアップロードすると、Experience Managerがエラーメッセージを表示して通知します (CQ-4290700)。

* [!UICONTROL  インタラクティブビデオを作成 ] ページのタイムラインスケールの数値（時間）のコントラストが、最低限必要な輝度比を満たすようになり、色の知覚が限られたユーザーが読みやすくなりました (CQ-4290699)。

* スクリーンリーダーは、[!UICONTROL  インタラクティブビデオを作成 ] ページを移動する際に、「[!UICONTROL  製品名 ]」フィールドのラベルを読み上げるようになりました (CQ-4290697)。

**修正された問題**

[!DNL Dynamic Media] では、次のバグ修正を利用できます。

* `dynamicmedia_scene7` 実行モードが有効になり、同期が無効になった後、[!DNL Experience Manager] に `Process failed` が表示されるようにビデオをアップロードしました (CQ-4327791)。

### Platform {#platform-65100}

このサービスパックでは、次の機能強化が提供されています。

* ユーザーがツリー表示で項目を選択すると、スクリーンリーダーは選択を読み上げ、上部に表示されるツールバーオプションを読み上げる (NPR-36504)。
* 明るさの比率が最小必要比 4.5:1 を満たすので、視覚に問題があるユーザーは、テキストや制御名の読みやすさがあります (NPR-36503)。
* ユーザーがカレンダーコントロールを使用する場合、スクリーンリーダーは、説明的な日付、月、平日の情報をナレーションします。 ユーザーがカレンダーショートカットキーを使用すると、スクリーンリーダーが日付、月、年の変更をナレーションする (NPR-36498)。
* 厳密なモードに従わずに ECMAScript 6 機能を使用してカスタム JavaScript `Clientlibs` を実行するためのサポートが提供されました。 具体的には、`emitUseStrict` フラグが `GCCScriptProcessor` に追加される (NPR-36411)。

このサービスパックには、次のバグ修正が含まれています。

* カスタムヘルスチェックは、スケジュールよりも頻繁に実行されます (NPR-36985)。
* `Resourceresolver map` メソッドがエイリアスページに対して誤った結果を返す (NPR-36767)。
* [!DNL Experience Manager] ワークフローの読み込みが原因で起動が遅延する (NPR-36615)。

### 統合 {#integrations-65100}

* Experience Managerは、プライマリ MongoDB ノードが別のノードに切り替えると応答しなくなる (NPR-36566)。
* [!DNL Sling content distribution] コレクションメンバーの削除操作の実行時に失敗する (NPR-36521、CQ-4323578)。

### ユーザーインターフェイス {#user-interface-65100}

* **[!UICONTROL 参照]** サイドパネルには、アセットとサイトの参照が表示されません (GRANITE-35078、GRANITE-34892)。

### 翻訳プロジェクト {#translation-65100}

* マルチ翻訳プロジェクトの言語コピーの余分なサブページが削除される (NPR-36622)。

### ワークフロー {#workflow-65100}

* サーバーが不在メッセージを受け取ると、メモリアラートを報告し、応答を停止する (NPR-36768)。

### [!DNL Communities] {#communities-65100}

* コミュニティサイトページが、匿名のゲストユーザーに対して `LoggedIn` 状態で開かれる (NPR-36908)。

* **[!UICONTROL コミュニティ]**/**[!UICONTROL アイデア]**/**[!UICONTROL コメント]** ページに複数のページがある場合、ページナビゲーションは機能しません (NPR-36541)。

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

* [!DNL AEM 6.5 Forms] をインストールすると、次のサードパーティライブラリが自動的にインストールされます (CQDOC-18373)。
   * [!DNL Microsoft Visual C++ 2008 Service Pack 1 (x86)]
   * [!DNL Microsoft Visual C++ 2010 Service Pack 1 (x86)]

**アダプティブフォーム**

* アダプティブフォームのフィールド値に対して実行された検証が正常に完了すると、[!DNL AEM Forms] はフォームデータモデルの呼び出しに失敗します (CQ-4325491)。

* 翻訳プロジェクトに言語辞書を追加してからプロジェクトを開くと、[!DNL AEM Forms] にエラーメッセージが表示されます (CQ-4324933)。

   ```TXT
   Uncaught TypeError: Cannot read property 'PROJECT_LISTING_PATH' of undefined
   at openButtonClickHandler (clientlibs.js:245)
   at HTMLButtonElement.onclick (clientlibs.js:258)
   ```

* [!DNL AEM Forms] Service Pack 7 のインストール後のパフォーマンスの問題 (CQ-4326828)。

**Correspondence Management**

* 「[!UICONTROL  データ ]」タブおよびHTML文字プレビューでの文字の表示遅延 (NPR-37020)。

* テキストドキュメントフラグメントを編集しているとき、フラグメントを保存すると、新しい単語がHTMLタグとして表示される (NPR-36837)。

* ドラフトとして保存されたレターを表示できない (NPR-36816)。

* テキストドキュメントフラグメントを編集してレターをプレビューすると、AEM FormsはHTMLレタープレビューに式言語を表示します (CQ-4322331)。

* セルフサービスレターテンプレートを使用してデータをレンダリングする際に発生する問題 (NPR-37161)。


**インタラクティブコミュニケーション**

* テキストドキュメントフラグメントの編集後にインタラクティブ通信のプレビューを印刷するたびに、タブ文字が 2 つの単語間で重複する (NPR-37021)。

* [!DNL AEM Forms] 最大サイズ制限を超えるテキストドキュメントフラグメントを保存すると、エラーが表示される (NPR-36874)。

* インタラクティブ通信に画像を追加すると、画像の後に追加の空のブロックが表示される (NPR-36659)。

* エディターですべてのテキストを選択すると、フォントテキストを Arial に変更できない (NPR-36646)。

* エディターで URL を作成し、変更をプレビューすると、URL テキストの代わりに黒の背景が表示される (NPR-36640)。

* テキストをエディターにコピー&amp;ペーストすると、ドキュメントで使用可能な箇条書きのフォントを Arial に変更する際に問題が発生する (NPR-36628)。

* テキストエディターでの箇条書きのインデントの問題 (NPR-36513)。

**デザイナー**

* 画面Readerが、マスターページまたは動的PDFのサブフォームページのテキストラベル内に配置されたフローティングフィールドデータを読み取れない (CQ-4321587)。

**ドキュメントサービス**

* XDP ファイルをPDFファイルに変換し、結果のPDFをアセンブリすると、PDFの生成に失敗し、次のエラーメッセージが表示されます。

   ```TXT
   Caused by: com.adobe.fd.assembler.client.AssemblerException$ClientException: Document is in a disposed state!
   ```

**Forms のワークフロー**

* AEM Forms Service Pack 8 にアップグレードした後、Workbench プロセスにフォームを送信できない (CQ-4325846)。

**HTML5 のフォーム**

* CRX DE リポジトリで `mfAllowAttachments` プロパティの値を `True` に設定すると、HTML5 フォームの送信時に `dataXml` が破損する (NPR-37035)。

* `dataXml` を使用して XDP をHTMLとしてレンダリングすると、[!DNL AEM Forms] は `Page Unresponsive` エラーを表示します (NPR-36631)。

### Commerce {#commerce-65100}

* 表示される **[!UICONTROL 「Published By]**」フィールドの値が列表示で正しくない。(NPR-36902)
* カタログがロールアウトされると、新しい製品が誤って変更された製品としてマークされる (NPR-36666)。
* 削除した製品を再作成しても、製品ページは再作成されません (NPR-36665)。
* 変更されたページは更新されますが、対応するリンクされた製品がカタログのロールアウトで更新されません (CQ-4321409、NPR-36422)。
* **[!UICONTROL 後で公開]** および **[!UICONTROL 後で非公開]** ワークフローは機能しません (CQ-4327679)。

セキュリティ更新の詳細については、[[!DNL Experience Manager]  セキュリティ速報ページ ](https://helpx.adobe.com/security/products/experience-manager.html) を参照してください。

## 6.5.10.0 のインストール {#install}

**要件の設定と詳細情報**

* Experience Manager6.5.10.0にはExperience Manager6.5 が必要です。詳細な手順については、[ アップグレードに関するドキュメント ](/help/sites-deploying/upgrade.md) を参照してください。
* サービスパックのダウンロードは、Adobe[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) で入手できます。
* MongoDB および複数のインスタンスを使用するデプロイメントで、パッケージマネージャーを使用して、いずれかのオーサーインスタンスにExperience Manager6.5.10.0をインストールします。

>[!NOTE]
>
>Adobeは、[!DNL Adobe Experience Manager] 6.5.10.0パッケージの削除またはアンインストールはお勧めしません。

### サービスパックのインストール {#install-service-pack}

[!DNL Adobe Experience Manager] 6.5 インスタンスに Service Pack をインストールするには、次の手順に従います。

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。 Adobeでは、インスタンスの現在の稼動時間が長い場合に再起動を推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. [ ソフトウェア配布 ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) からサービスパックをダウンロードします。

1. パッケージマネージャーを開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。詳しくは、[ パッケージマネージャー ](/help/sites-administering/package-manager.md) を参照してください。

1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

1. S3 コネクタを更新するには、Service Pack のインストール後にインスタンスを停止し、既存のコネクタを install フォルダーに指定された新しいバイナリファイルに置き換えて、インスタンスを再起動します。 [Amazon S3 データストア ](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector) を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。 Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。 アップデータバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが正常に完了することを確認します。 通常、この問題は [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.10.0を作業インスタンスに自動的にインストールするには、次の 2 つの方法があります。

A.サーバーがオンラインで使用可能になったら、パッケージを `../crx-quickstart/install` フォルダーに配置します。 パッケージが自動的にインストールされます。

B.パッケージマネージャーの [HTTP API を使用します。](/help/sites-administering/package-manager.md#package-share) `cmd=install&recursive=true` を使用して、ネストされたパッケージをインストールします。

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0は、Bootstrapのインストールをサポートしていません。

**インストールの検証**

1. 製品情報ページ (`/system/console/productinfo`) に、[!UICONTROL  インストール済みの製品 ] の下に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.10.0)` が表示されます。

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL ACTIVE]** または **[!UICONTROL FRAGMENT]** です (Web コンソールを使用：`/system/console/bundles`) です。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` は、バージョン1.22.3以降です (Web コンソールを使用：`/system/console/bundles`) に置き換えます。

このリリースでの動作が認定されたプラットフォームについては、[ 技術要件 ](/help/sites-deploying/technical-requirements.md) を参照してください。

### Adobe Experience Manager Formsアドオンパッケージのインストール {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Experience Manager Formsを使用していない場合はスキップします。 Experience Manager Formsの修正は、スケジュールされた [!DNL Experience Manager] Service Pack のリリースから 1 週間後に、個別のアドオンパッケージを通じて配信されます。

1. Adobe Experience Manager Service Pack がインストールされていることを確認します。
1. [AEM Forms リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)のリストから、使用しているオペレーティングシステムに対応する Forms アドオンパッケージをダウンロードします。
1. 「[AEM Formsアドオンパッケージのインストール ](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)」の説明に従って、Formsアドオンパッケージをインストールします。

>[!NOTE]
>
>Experience Manager6.5.10.0には、[AEM Forms互換性パッケージ ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases) の新しいバージョンが含まれています。 古いバージョンのAEM Forms互換性パッケージを使用し、Experience Manager6.5.10.0に更新する場合は、Formsアドオンパッケージのインストール後に、最新バージョンのパッケージをインストールします。

### JEE へのAdobe Experience Manager Formsのインストール {#install-aem-forms-jee-installer}

>[!NOTE]
>
>JEE で AEM Forms を使用していない場合はスキップします。JEE 上のAdobe Experience Manager Formsの修正は、別のインストーラーを使用して提供されます。

JEE 上のExperience Manager Formsの累積インストーラーのインストールとデプロイ後の設定について詳しくは、[ リリースノート ](jee-patch-installer-65.md) を参照してください。

>[!NOTE]
>
>JEE 上のExperience Manager Formsの累積インストーラーをインストールした後、最新のFormsアドオンパッケージをインストールし、`crx-repository\install` フォルダーからFormsアドオンパッケージを削除して、サーバーを再起動します。


### UberJar {#uber-jar}

Experience Manager6.5.10.0の UberJar は、[Maven Central リポジトリ ](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/) で入手できます。

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法 ](/help/sites-developing/ht-projects-maven.md) を参照し、プロジェクトの POM に次の依存関係を含めます。

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
>UberJar およびその他の関連アーティファクトは、Adobeのパブリック Maven リポジトリ (`repo.adobe.com`) ではなく、Maven Central リポジトリで使用できます。 メインの UberJar ファイルの名前が `uber-jar-<version>.jar` に変更されます。 したがって、`dependency` タグには `apis` を値として持つ `classifier` はありません。

## 非推奨（廃止予定）の機能 {#removed-deprecated-features}

[!DNL Experience Manager] 6.5.7.0 で非推奨とマークされた機能の一覧を以下に示します。機能は、最初に廃止され、後で将来のリリースで削除されます。 別のオプションが提供されます。

機能または機能をデプロイメントで使用するかどうかを確認します。 また、別のオプションを使用するように実装を変更することを計画します。

| 領域 | 機能 | 代替手段 |
|---|---|---|
| 統合 | **[!UICONTROL AEM Cloud Services オプトイン]** 画面は廃止されました。Experience Manager6.5 では [!DNL Experience Manager] と [!DNL Adobe Target] の統合が更新されています。この統合は、Adobe Target Standard API をサポートしています。 API は、Adobe IMSと [!DNL Adobe I/O] を介した認証を使用し、Adobeの起動の役割が広がり、分析やパーソナライゼーション用に [!DNL Experience Manager] ページを実装できるようになっています。オプトインウィザードは機能的に無関係です。 | 各 [!DNL Experience Manager] クラウドサービスを介して、システム接続、Adobe IMS認証、および [!DNL Adobe I/O] 統合を設定します。 |
| コネクタ | Microsoft® SharePoint 2010 およびMicrosoft® SharePoint 2013 用のAdobeJCR Connector は、Experience Manager6.5 で非推奨（廃止予定）となりました。 | 該当なし |

## 既知の問題 {#known-issues}

* [!DNL Microsoft Windows Server 2019] は [!DNL MySQL 5.7] および [!DNL JBoss EAP 7.1] をサポートしていないので、[!DNL Microsoft Windows Server 2019] は [!DNL AEM Forms 6.5.10.0] の自動インストールをサポートしていません。

* [!DNL Experience Manager] インスタンスを 6.5 から 6.5.10.0バージョンにアップグレードする場合は、`error.log` ファイルで `RRD4JReporter` 例外を表示できます。 この問題を解決するには、インスタンスを再起動します。

* [!DNL Experience Manager] 6.5 Service Pack 10 または以前の Service Pack を [!DNL Experience Manager] 6.5 にインストールした場合、（`/var/workflow/models/dam` で作成された）アセットのカスタムワークフローモデルのランタイムコピーが削除されます。
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

## OSGi バンドルとコンテンツパッケージが含まれています {#osgi-bundles-and-content-packages-included}

次のテキストドキュメントは、[!DNL Experience Manager] 6.5.10.0に含まれている OSGi バンドルとコンテンツパッケージの一覧です。

* [Experience Manager6.5.10.0に含まれている OSGi バンドルの一覧](assets/65100_bundles.txt)

* [Experience Manager6.5.10.0に含まれているコンテンツパッケージの一覧](assets/65100_packages.txt)

## 制限付き Web サイト {#restricted-sites}

これらの Web サイトは、お客様のみが利用できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [ カスタマーサポートへの問い合わせ方法 ](https://experienceleague.adobe.com/docs/customer-one/using/home.html) を参照してください。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5 リリースノート](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [Adobe Priority 製品アップデート](https://www.adobe.com/subscription/priority-product-update.html)のサブスクリプションを購入する

