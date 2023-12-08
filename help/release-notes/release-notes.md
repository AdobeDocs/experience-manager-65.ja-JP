---
title: ' [!DNL Adobe Experience Manager]  6.5 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
mini-toc-levels: 4
exl-id: cac14ac1-9cda-46ae-8aa3-94674bb79157
source-git-commit: 1c3df6ea88f1dfbab5d9df2dcd4907e72829287a
workflow-type: tm+mt
source-wordcount: '4232'
ht-degree: 75%

---

# [!DNL Adobe Experience Manager] 6.5 の最新のサービスパックのリリースノート {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| バージョン | 6.5.19.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2023 年 12 月 07 日（木） <!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.19.0 の内容 {#what-is-included-in-aem-6519}

[!DNL Experience Manager] 6.5.19.0 には、2019年4月の 6.5 の初公開以降にリリースされた新しい機能、お客様から要望のあった主な機能強化、バグ修正およびパフォーマンスや安定性、セキュリティの向上が含まれています。[!DNL Experience Manager] 6.5 で[このサービスパックをインストール](#install)します。

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

## 主な機能および機能強化

このリリースの主な機能と機能強化は次のとおりです。

* Sites ページエディター／画像コンポーネントユーザーがリモート Assets Cloud Service からアセットを参照できるようにしました。（Sites-13448、Sites-13433）
* AEMでサーバー側の並べ替えがサポートされ、リスト表示でのプロジェクトのナビゲーションをより迅速におこなえるようになりました。 プロジェクトノードは、インターフェイスに表示される前に、ユーザが選択した列に基づいて並べ替えられます。

### [!DNL Forms]

* **新しいアダプティブフォームコアコンポーネント**：フォームのスケーラビリティを高めるために、縦並びのタブ、「利用条件」および「チェックボックス」が追加されました。
   * **[チェックボックスコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**：コアコンポーネントに基づくアダプティブFormsで、チェックボックスコンポーネントを含めることができるようになりました。 ユーザーは、特定のオプションの選択または選択解除を行い、バイナリ選択をおこなうことができます。 これは通常、小さなボックスとして表示され、クリックまたはタップすると、2 つの状態（チェック済みとオフ）を切り替えることができます。 このチェックボックスは、はい/いいえ、真/偽の選択肢を提示するために使用される一般的なフォーム要素です。

   * **[利用条件コンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**：コアコンポーネントに基づくアダプティブFormsで、利用条件コンポーネントを含めることができるようになりました。 フォーム作成者は、フォーム内に特定のセクションを導入できます。このセクションには、サービス、製品、プラットフォームの使用に関連する利用条件、または法的契約が表示されます。 このコンポーネントは、フォームを送信することで、同意するルール、規制、義務をユーザーに通知するように設計されています。

     ![垂直タブ、利用条件およびチェックボックスコンポーネント](/help/forms/using/assets/forms-components.png)

   * **[垂直タブコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**：コアコンポーネントに基づくアダプティブFormsで、フォームコンテンツをタブの縦並びのリストに整理でき、構造化されたナビゲーション可能なレイアウトが提供されるようになりました。 フォーム内で縦置きのタブを使用すると、ナビゲーションが簡単になり、フォームコンテンツの構成が改善され、特にフォームに複数のセクションや複雑な情報が含まれる場合に、ユーザーの操作性が向上します。

* **[64 ビット版のAEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**: 64 ビット版のAEM Forms Designer では、パフォーマンス、拡張性、メモリ管理の機能が強化され、フォーム作成エクスペリエンスが強化されます。 64 ビットアーキテクチャを使用すると、より大規模で複雑なプロジェクトに簡単に取り組むことができ、シームレスな設計ワークフローと最適化された効率を確保できます。 フォームデザインの機能を向上させ、この最先端リリースでAEM Forms Designer の将来を受け入れます。

* **[Microsoft® SharePointリストとのアダプティブFormsの接続](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**:AEM Formsは、フォームデータを直接SharePointリストに送信するための OOTB 統合機能を備えており、SharePointのリスト機能を使用できます。 Microsoft SharePointリストをフォームデータモデルのデータソースとして設定し、「フォームデータモデルを使用して送信」送信アクションを使用して、アダプティブフォームをSharePointリストに接続することができます。

* **[アダプティブフォームフラグメントのレコードのドキュメントプロパティの設定をサポート](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**：アダプティブフォームエディターで、アダプティブフォームフラグメントとそのフィールドを簡単にカスタマイズできるようになりました。

* **64 ビット XMLFM**:XMLFM の 64 ビット版では、パフォーマンス、拡張性、メモリ管理の改善が導入されています。 これは、サーバー側にデプロイされる最初の 64 ビットネイティブサービスです。 XMLFM 64 ビットは、32 ビット対応のメモリリソースに比べて、大幅に大きなメモリリソースにアクセスする固有の機能を備えているため、より大きなレンダリングワークロードのシームレスな処理を実現します。 このマイルストーンは、パフォーマンスの飛躍を表すだけでなく、AEM Formsサーバー内のネイティブサービスフレームワークに対する主な機能強化も導入します。 このアップデートでは、AEM Formsサーバーが 64 ビットのネイティブサービスをシームレスにサポートするように装備しています。


**非推奨（廃止予定）の機能**

* AEM の ActiveMQ は、非推奨（廃止予定）です。2 つの AEM パブリッシュインスタンス間の通信に ActiveMQ が使用されていました。アドビでは、現在ロードバランサーを使用することを推奨しています。

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## サービスパック 19 で修正された問題 {#fixed-issues}

### [!DNL Sites]{#sites-6519}

#### アクセシビリティ{#sites-accessibility-6519}

* AEM Sites ページで、ページを 200％拡大すると、参照レールの&#x200B;**[!UICONTROL 言語コピー]**&#x200B;と **[!UICONTROL CSV レポート]**&#x200B;のリンクが非表示になります。（SITES-11011）

#### 管理ユーザーインターフェイス{#sites-adminui-6519}

* AEM Screens チャネルの&#x200B;**[!UICONTROL プレビュー]**&#x200B;機能が機能しないか、ダッシュボードに表示されません。（SITES-15730）
* ページの移動操作中に、ユーザーインターフェイスに参照が表示されないにもかかわらず、参照が自動的に再公開されると表示されている場合、参照は再公開&#x200B;*されません*。（SITES-16435）
* Service Pack 16 または 17 を適用した AEM 6.5 では、「ワークフロー」列が有効なサイトのリスト表示で、その列の項目に基づいてリストを並べ替えることができません。並べ替えは実行されません。（SITES-15385）
* リダイレクトページテンプレートの場合、リダイレクトフィールドは必須になりました。ただし、必須フィールドの検証は、必須のリダイレクト値を指定せずにページを作成した場合と、リダイレクトページを作成できない場合の 2 つのシナリオでは適用されず、機能しません。キーボードショートカットを使用して移動する場合、検証は機能せず、フィールドが無効としてマークされている場合、検証は続行しません。（SITES-15903）
* 一部の&#x200B;**受信リンク**&#x200B;は、**参照**&#x200B;パネルに表示される数に含まれていませんでした。例えば、パネルには&#x200B;**受信リンク（6）**&#x200B;と表示されていましたが、実際には 9 つの受信リンクがありました。（SITES-14816）

#### クラシック UI{#sites-classicui-6519}

* SITES-15827 のホットフィックスをインストールすると、単語の間に空白があるダイアログボックスのタイトルが `" "` に置き換えられました。また、改行も削除されていました。（SITES-16089）
* エンコードされたダイアログボックスのタイトルでは、タイトルが二重にエンコードされるようになりました。（SITES-15841）
* AEM サーバーをサービスパック 6.5.16 から 6.5.17 に更新すると、クラシック UI ダイアログボックスのタイトルが二重にエンコードされるようになりました。（SITES-15634）

#### [!DNL Content Fragments]{#sites-contentfragments-6519}

* コンテンツフラグメントエディターに内部サーバーエラーメッセージが表示されます。（SITES-13550）
* NPR-41291 による `org.json` ライブラリの更新により、`cfm-impl` バンドルの `DefaultDataTypeConverter` でデータエラー変換が発生しました。データタイプの変換は、より柔軟に行う必要があります。（SITES-16473）
* 「コンテンツに互換性がないため、このコンテンツフラグメントのバージョンは現在のバージョンと比較できません」というエラーポップアップメッセージが表示されます。コンテンツフラグメントは比較できるはずですが、実際はそうではありません。（SITES-16317）
* アセットセレクターの JS URL を次から変更しました
  `https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js`
コピー先：
  `https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js`（SITES-16068）
* 新しい Polaris メタデータ API 応答スキーマを CFM-Polaris 統合に適応させます。（SITES-15166）
* 選択したコンテンツフラグメントが参照される場所に、すべてのコンテンツフラグメントをリストする必要があります。代わりに、コンテンツフラグメント参照パネルのアセット参照には 0（ゼロ）の参照が表示されます。（SITES-15036）

#### コアバックエンド{#sites-core-backend-6519}

* `StyleImpl` を改善します。（SITES-15164）
* WCM パイプラインの release/650 ブランチを改善し、そのモジュールの統合テストを実行できるようにします。（SITES-12938）

<!--#### Core Components{#sites-core-components-6519}

* A -->

#### Campaign 統合{#sites-campaign-integration-6519}

* 署名コンポーネント（`/apps/fpl/components/campaign/signature`）では、Link Externalizer が機能していませんでした。画像タグの上の HTML コメントを削除した場合、ドメインが画像ソースに追加されませんでした。この問題は、ステージング環境ではなく、実稼動環境の署名コンポーネントでのみ発生しました。（SITES-16120）

<!--#### Experience Fragments{#sites-experiencefragments-6519}

* A -->

#### 基盤コンポーネント（レガシー）{#sites-foundation-components-legacy-6519}

* Adobe Experience Manager（AEM）Sites 検索コンポーネントによりユーザーインターフェイスが破損します。（SITES-15087）

#### GraphQL クエリエディター{#sites-graphql-query-editor-6519}

* GraphQL エディターのユーザーインターフェイスでは、クエリの数が多い場合（例えば、25 を超える場合）、永続化されたクエリをすべてスクロールすることはできません。（SITES-16008）
* GraphQL Editor は、永続化されたクエリの公開ステータスを保存しません。 GraphQL エディターに非公開ボタンが表示されますが、永続クエリが公開されていることを示すアイコンは表示されません。ページを更新すると、永続クエリが公開されていないことがわかります。（SITES-15858）

#### ローンチ{#sites-launches-6519}

* 複数のページの編集中またはコンテンツの作成中に、`Oak0001` の競合が発生するので、リポジトリ内の変更は保存されません。このようなイベントでは再試行を実行するのが通常ですが、これは行われません。（SITES-14840）

#### MSM - ライブコピー{#sites-msm-live-copies-6519}

* MSM ロールアウトボタンは、タッチグラフィックユーザーインターフェイスでは機能しません。（SITES-16991）
* ライブコピーの作成時またはクスペリエンスフラグメントのロールアウト時に、エクスペリエンスフラグメント内でリンク参照が更新されません。（SITES-15460）

#### ページエディター{#sites-pageeditor-6519}

* Forms／テーマで、テーマエディターでテーマを開き、いくつかの変更を加えて保存し、「プレビュー」をクリックすると、読み込みアイコンが表示されますが、実際のプレビューは読み込まれません。（SITES-17164）
* ページコンソールのアセットタイプフィルターで、複数のドキュメントファイルタイプの選択が機能しません。1 つの特定のファイルタイプの結果が利用可能な場合でも、結果が見つかりません。その結果、作成者は複数のドキュメントをフィルタリングできなくなります。複数のドキュメントタイプを使用し、一度に 1 つずつフィルタリングする必要があります。（SITES-14047）
* AEM 6.5.17 および AEM 6.5.18 からインスタンスをアップグレードした後、ページエディター内で「**[!UICONTROL ページを公開]**」を選択すると、存在しない URL にリダイレクトされます。ユーザーは、公開ウィザードにリダイレクトされます。（SITES-15856）
* オペレーティングシステムのクリップボードからのペースト中の AEM のクリップボードからの冗長コピー。（SITES-15704）
* Assets で「**[!UICONTROL ドキュメント]**」を選択し、**[!UICONTROL Filtertype]** で「**[!UICONTROL Microsoft® Word]**」または「**[!UICONTROL Microsoft® Excel]**」を選択すると、両方のタイプのファイルが存在しても結果が表示されません。（SITES-14837）

### [!DNL Assets]{#assets-6519}

* 公開フォルダーを作成または保存すると、管理ダッシュボードに 3 つのグループが作成されます。（ASSETS-26700）
* 公開アセットを Experience Manager または Brand Portal に区別できません。（NPR-41320）
* 検索パネルでチェックボックスをオンにし、いずれかのチェックボックスをオフにすると、すべてのチェックボックスがオフになります。（ASSETS-26377）

#### [!DNL Dynamic Media]{#assets-dm-6519}

* アセットを AEM にアップロードすると、`update_asset` ワークフローがトリガーされます。ワークフローが完了することはありません。ワークフローインスタンスを見ると、ワークフローは製品のアップロード手順まで完了します。次の手順は、Scene7 のバッチアップロードです。ユーザーは、Dynamic Media Classic アプリからアセットが Scene7 にあることを確認できます。（ASSETS-30443）
* カスタムサーブレット（API エンドポイント）が正しくない Dynamic Media（Scene7）ファイル名を返します。これは、アセットが削除され、同じ名前のアセットに置き換えられる場合に発生します。カスタムサーブレットは古いDynamic Media（Scene7）ファイル名を返しますが、「jcr」API 呼び出しが正しいファイル名を返します。（ASSETS-29476）
* フォルダーレベルで同期がオフになった後でも、ログには「Scene7 ReplicateOnModifyListener」のトリガーが表示されます。`ReplicateOnModifyListener/Worker` では、Dynamic Media 以外のフォルダーアセットとコンテンツフラグメントの処理をスキップする必要があります。（ASSETS-26705）
* コントラストの高い白黒モードでドロップダウン要素（コンテンツのみ、表示、その他のオプション）にフォーカスが表示されない場合、視覚障害のあるユーザーは影響を受けます。（ASSETS-25759）
* ページ上のテキストの輝度コントラスト比が 4.5:1 未満の場合、視覚障害のあるユーザーは影響を受けます。（ASSETS-25756）
* スクリーンリーダーでは、データの送信後に表示されるポップアップメッセージのナレーションを行いません。（ASSETS-25755）
* ランドマーク／地域のショートカットキー `D/R` を使用して移動すると、スクリーンリーダーではページ（Dynamic Media、ビデオエンコードプロファイルの作成）内のランドマークを認識しません。（ASSETS-25752）
* スクリーンリーダーがランドマーク／領域のショートカットキーを使用して移動すると、ページ内の複数のランドマーク（Dynamic Media、インタラクティブビデオの作成）を認識できません `D/R`。（ASSETS-25750）
* スクリーンリーダー（NVDA／JAWS／ナレーター）がショートカットキーを使用して移動している間、**アセットを編集**&#x200B;ページのランドマークを認識しません `D/R`。（ASSETS-25744）
* ユーザーは空／偽の非同期ジョブメッセージを受け取りますが、接続されたアセットは正常に公開されます。（ASSETS-29342）

### [!DNL Forms]{#forms-6519}

#### [!DNL Adaptive Forms]

<!-- Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.19.0 Forms add-on package release is scheduled for Thursday, November 30, 2023. A list of Forms fixes and enhancements would be added to this section post the release.-->

<!--* Adding Access Control List for `fd-cloudservice` user to be able to read or update the Microsoft&reg; configurations under `cloudconfigs/microsoftoffice`. (FORMS-11142) -->

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6519}

* A -->

* ユーザーがアダプティブフォームにツールバーを追加すると、フォームコンテナラベルには、作成者がForms用に選択した優先言語に変更されないので、異常な動作が表示されます。 （FORMS-11371）
* AEM Forms Workspace では、ドロップダウンフィールドにより、UI の最初のオプションがデフォルトで選択されます。 （FORMS-11346）
* 5 文字のロケールを使用し、小数点記号がレター内で正しくレンダリングされない場合、AEMの言語設定は効果を示しません。 （FORMS-11344）
* ユーザーが Workbench プロセスを使用して XML 出力を生成する場合、一部のファイルで失敗します。 （FORMS-11314）
* ユーザーが英語以外の言語でレコードのドキュメント (DOR) のプレビューを生成した場合、そのレコードは機能しません。 （FORMS-11106）
* ユーザーが、JDK11 を使用して Linux に基づく OSGi インスタンスで PDFG を使用して一部の画像ファイルを変換しても、変換はおこなわれません。 （FORMS-11105）
* ユーザーがAEM Formsアドオンをインストールすると、AEM Sitesのコンテンツツリーパネルが壊れます。 （FORMS-10912）
* ユーザーが日付選択コンポーネントから NVDA スクリーンリーダーを使用して日付をコピーすると、正しく読み取れません。 (FORMS-10805) 
* Formsのルールエディターで、データ値タイプが Boolean の場合、ユーザーはラジオボタン/チェックボックスの値を設定できません。 （FORMS-10713）
* ユーザーがアダプティブフォームに追加した項目は、ドロップダウンリストの逆の順序で追加されます。 （FORMS-10456）
* ルールエディターでドロップダウンをクリアした場合、最初に指定した値は、値がクリアされていても表示されます。 (FORMS-9963) 
* ユーザーは、NVDA などのスクリーンリーダーを使用してフォームタイトルにアクセスできません。 (FORMS-8815) 
* ユーザーは、NVDA などのスクリーンリーダーを使用してフォームのサブタイトルにアクセスできません。 (FORMS-8814) 
* HTML フォームのページソースでは、アクセスキー属性が空で、機能しません。 (FORMS-5753) 
* Workspace についてダイアログでは、「Adobe Experience Manager - Forms」というテキストがテキストとして表示されます。 （FORMS-5748）

#### [!DNL Forms Designer]{#forms-designer-6519}

* ユーザーがスクリーンリーダーで非インタラクティブPDF formsを読み上げようとすると、一部のリスト項目が読み上げられず、スキップされません。 (LC-3921645) 
* ユーザーが編集可能フィールド内をタブで移動しても、一貫してすべてのPDFフォームフィールドを横断するわけではありません。 (LC-3921631) 
* Forms Designer でのタグ付けが正しい場合でも、PDFでタグの順序がランダムに変更されます。 (LC-3921313) 
* Adobe Acrobat ReaderまたはAdobe Acrobat DC のタグで、リストが正しく表示されません。 （LC-3921306）
* Forms Designer で正しく割り当てられた見出しレベルは、 `<P>` タグをAdobe Acrobatに追加します。 (LC-3921305) 
* テーブルでは、オブジェクトを割り当てた後にその ID を変更することはできません。 (LC-3921134) 
* 結合されたセルがテーブル内にある場合、AEM Forms Designer の複雑なテーブルで span（行と列）と scope を設定する GUI は使用できません。 (LC-3919532) 

### 基盤{#foundation-6519}

* 言語ルートレベルで言語コピーを作成しても、ページ内のパスは調整されません。言語コピーが言語ルートではなくその下のページに対して作成された場合でも、パスは正しく変更されました。（NPR-41364）
* 「相対的な日付の表示」ツールチップを閉じるには、キーボードの Esc キー（ESC）を押します。ユーザがユーザーインターフェイスの任意の部分を選択すると、ツールチップが閉じます。（NPR-41394）
* **ユーザーを編集**／**キーストア**&#x200B;で間違った秘密鍵ファイルを追加すると、ローカライズされていない文字列 `Something went wrong while adding the private key.` が発生します。（NPR-41366）
* アイコンは、AEM 6.5 環境の Microsoft® SharePoint と Microsoft® One Drive に必要です。（NPR-41354）
* 「UserId/Password mismatch」がローカライズされていません。 **セキュリティ**／**ユーザー**／**作成**&#x200B;ダイアログボックス内の文字列。（NPR-41245）
* ポップオーバーコードとイベントハンドラーが 2 回読み込まれ、ユーザーが作成した Coral3 ベースのユーザーインターフェイスが機能しなくなります。（NPR-41171）
* AEM Sites コンソールで「すべてを選択」を使用しても、選択解除が正しく機能しません。（NPR-41304）

<!--#### Content distribution{#foundation-content-distribution-6519}

* T -->

#### 統合{#integrations-6519}

* AEM メールキャンペーンの SMS リンクが正しく書き込まれていません。リンクには HTML アンカー要素が含まれています。（NPR-41211）
* アカウント設定画面で使用する文言では、新しい資格情報の種類を使用しないでください。（NPR-41210）
* Analytics レポート読み込みスケジューラーを `ManagedPollConfig` から Sling ジョブに移動します。2 つの異なるサイトに異なるレポートスイートを使用して、2 つの異なる分析フレームワークを接続すると、`ManagedPollConfig` はそのうちの 1 つだけをポーリングします。（NPR-41209）
* 値がデフォルトにリセットされても、以前に選択した期間ボタンは有効なままです。AEM のコンテンツインサイトダッシュボードでは、デフォルトで期間が週に設定され、コンテンツインサイトが週別データとして表示されます。現在、ユーザーが時間、日、月、年などの他の時間枠オプションを選択すると、選択した値に応じてデータが変更されます。ただし、値がリセットされた場合、デフォルトで表示される期間は週ですが、以前に選択した時間枠オプションが選択されたままになります。（NPR-41246）

#### Oak{#oak-6519}

* 非同期インデックス作成が遅延した場合に、AEM への書き込みレートを制限するバックポートユーティリティ。（NPR-40985）

#### プラットフォーム{#foundation-platform-6519}

* 角括弧で囲まれた QueryBuilder クエリが、誤って xpath に変換されます。（NPR-41298）

<!--#### Replication{#foundation-replication-6519}

* R -->

<!--#### Sling{#foundation-sling-6519}

* W -->

#### 翻訳プロジェクト{#foundation-translation-6519}

* ページ「A」の言語コピーを作成する際に、参照されるページ、エクスペリエンスフラグメント、コンテンツフラグメント、アセットの言語コピーが自動的に作成されます。また、新しいパスにあるページ「A」の新しく作成した言語コピーの参照は、ページ、エクスペリエンスフラグメント、コンテンツフラグメント、アセットのそれぞれで新しく作成した言語コピーに更新する必要があります。（NPR-41076）

<!--#### User interface{#foundation-ui-6519}

* A -->

<!--#### WCM{#wcm-6519}

* A -->

#### ワークフロー{#foundation-workflow-6519}

* インボックスでタスクを完了できません。タスクを完了してアクションを選択しようとすると、ドロップダウンメニューに「未定義」の値のみが表示されます。つまり、ユーザーは AEM 6.5.18 サービスパックを適用できません。（NPR-41402 および NPR-41473）
* インボックスでタスクを完了できません。zip ファイル、アセットレポート、移動（成功または失敗）またはアセットの有効期限に関するタスクを完了しようとすると、ドロップダウンリストに値が表示されません （「未定義」のみ）。（NPR-41305）
* ユーザーが&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／インスタンスを選択し、実行中のワークフローを選択してから「**[!UICONTROL ペイロードを表示]**」を選択すると、500 エラーページが表示されます。（NPR-41325）

## [!DNL Experience Manager] 6.5.19.0 のインストール{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.19.0 には [!DNL Experience Manager] 6.5 が必要です。手順について詳しくは、[アップグレードに関するドキュメント](/help/sites-deploying/upgrade.md)を参照してください。<!-- UPDATE FOR EACH NEW RELEASE -->
* サービスパックは、アドビの[ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip)からダウンロードできます。
* MongoDB と複数のインスタンスを含むデプロイメントでは、パッケージマネージャーを使用して、オーサーインスタンスの 1 つに [!DNL Experience Manager] 6.5.19.0 をインストールしてください。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> アドビでは、[!DNL Experience Manager] 6.5.19.0 パッケージを削除またはアンインストールすることを推奨しません。したがって、パッケージをインストールする前に、ロールバックする必要がある場合に備えて `crx-repository` のバックアップを作成する必要があります。<!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### [!DNL Experience Manager] 6.5 へのサービスパックのインストール{#install-service-pack}

1. インスタンスが更新モードの場合（インスタンスが以前のバージョンから更新された場合）、インストール前にインスタンスを再起動します。インスタンスの現在の稼動時間が長い場合、アドビは再起動することを推奨します。

1. インストールする前に、[!DNL Experience Manager] インスタンスのスナップショットまたは新しいバックアップを作成します。

1. 次の場所からサービスパックをダウンロードします。 [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.19.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. パッケージマネージャーを開き、「**[!UICONTROL パッケージをアップロード]**」を選択して、パッケージをアップロードします。詳しくは、[パッケージマネージャー](/help/sites-administering/package-manager.md)を参照してください。

1. パッケージを選択して、「**[!UICONTROL インストール]**」を選択します。

1. S3 コネクタを更新するには、サービスパックのインストール後にインスタンスを停止し、既存のコネクタをインストールフォルダーに用意されている新しいバイナリファイルに置き換えて、インスタンスを再起動します。[Amazon S3 データストア](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)を参照してください。

>[!NOTE]
>
>サービスパックのインストール中に、パッケージマネージャー UI のダイアログが終了することがあります。Adobeでは、エラーログが安定するのを待ってから、デプロイメントにアクセスすることをお勧めします。アップデーターバンドルのアンインストールに関連する特定のログが表示されるのを待ってから、インストールが成功したことを確認してください。この問題は、通常 [!DNL Safari] ブラウザーで発生しますが、どのブラウザーでも断続的に発生する場合があります。

**自動インストール**

[!DNL Experience Manager] 6.5.19.0 の自動インストールに使用できる方法は 2 つあります。<!-- UPDATE FOR EACH NEW RELEASE -->

* サーバーがオンラインで使用可能な場合、パッケージを `../crx-quickstart/install` フォルダーに配置します。パッケージが自動的にインストールされます。
* [パッケージマネージャーの HTTP API](/help/sites-administering/package-manager.md#package-share) を使用します。ネストされたパッケージがインストールされるように、`cmd=install&recursive=true` を使用します。

>[!NOTE]
>
>Experience Manager 6.5.19.0 では、Bootstrap のインストールをサポートしていません。<!-- UPDATE FOR EACH NEW RELEASE -->

**インストールの検証**

このリリースでの動作が認定されたプラットフォームについては、[技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

1. 製品情報ページ（`/system/console/productinfo`）の[!UICONTROL インストール済み製品]に、更新されたバージョン文字列 `Adobe Experience Manager (6.5.19.0)` が表示されます。<!-- UPDATE FOR EACH NEW RELEASE -->

1. すべての OSGi バンドルは、OSGi コンソールで **[!UICONTROL アクティブ]** または **[!UICONTROL フラグメント]** です（web コンソールを使用：`/system/console/bundles`）。

1. OSGi バンドル `org.apache.jackrabbit.oak-core` はバージョン 1.22.17 以降です（Web コンソールを使用：`/system/console/bundles`）。<!-- NPR-41292 for 6.5.19.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### [!DNL Experience Manager] Forms へのサービスパックのインストール{#install-aem-forms-add-on-package}

AEM Forms にサービスパックをインストールする手順については、[AEM Forms サービスパックのインストール手順](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)を参照してください。

>[!NOTE]
>
>[AEM 6.5 クイックスタート](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=ja)で使用できるアダプティブフォーム機能は、探索と評価のみを目的として設計されています。アダプティブフォームの機能には適切なライセンスが必要なので、実稼動環境で使用する場合は、AEM Forms の有効なライセンスを取得することが不可欠です。

### Experience Manager コンテンツフラグメント用の GraphQL インデックスパッケージのインストール{#install-aem-graphql-index-add-on-package}

GraphQL を使用しているお客様は、[Experience Manager コンテンツフラグメントと GraphQL インデックスパッケージ 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip) をインストールする必要があります。

これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。

このパッケージをインストールしないと、GraphQL クエリが遅くなったり失敗したりする場合があります。

>[!NOTE]
>
>このパッケージは、インスタンスごとに 1 度だけインストールします。サービスパックごとに再インストールする必要はありません。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.19.0 の UberJar は、[Maven Central リポジトリ](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.19/)で入手できます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Maven プロジェクトで UberJar を使用するには、[UberJar の使用方法](/help/sites-developing/ht-projects-maven.md)を参照し、プロジェクト POM に次の依存関係を含めます。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.19</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar およびその他の関連アーティファクトは、Adobe のパブリック Maven リポジトリー （`repo.adobe.com`） ではなく、Maven Central リポジトリーで入手できます。メインの UberJar ファイルの名前は、「`uber-jar-<version>.jar`」に変更されます。そのため `classifier` が存在せず、`apis` が値として `dependency` タグに使用されます。

## 廃止される機能および削除された機能{#removed-deprecated-features}

[廃止される機能および削除された機能](/help/release-notes/deprecated-removed-features.md/)を参照してください。

## 既知の問題{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->



* **Oak 関連**
サービスパック 13 以降で、永続性キャッシュに影響する次のエラーログが表示されるようになりました。

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  または

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  この例外を解決するには、次の手順を実行します。

   1. 次の 2 つのフォルダーを `crx-quickstart/repository/` から削除する

      * `cache`
      * `diff-cache`

   1. サービスパックをインストールするか、Experience Manager as a Cloud Serviceを再起動します。
`cache` および `diff-cache` の新しいフォルダーが自動的に作成され、`error.log` 内で `mvstore` に関連する例外は発生しなくなりました。

* コンテンツモデルのカスタム API 名を使用していた可能性のある GraphQL クエリを、代わりにコンテンツモデルのデフォルト名を使用するように更新してください。

* GraphQL クエリでは、`fragments` インデックスの代わりに `damAssetLucene` インデックスを使用する場合があります。このアクションは結果的に、GraphQL クエリが失敗するか、実行に非常に長い時間がかかる可能性があります。

  問題を修正するには、`damAssetLucene` では、`/indexRules/dam:Asset/properties` に次の 2 つのプロパティを含むように設定する必要があります。

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  インデックス定義を変更した後、インデックス再作成が必要です（`reindex` = `true`）。

  これらの手順を行うと、GraphQL クエリの実行が高速化されます。

* コンテンツフラグメント、サイト、ページのいずれかを移動、削除または公開しようとすると、バックグラウンドクエリが失敗したため、コンテンツフラグメント参照が取得される際に問題が発生します。つまり、この機能が動作しなくなります。
正しく動作させるには、インデックス定義ノード `/oak:index/damAssetLucene` に次のプロパティを追加する必要があります（インデックスの再作成は不要です）。

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* [!DNL Experience Manager] インスタンスを 6.5.0～6.5.4 から Java™ 11 の最新のサービスパックにアップグレードすると、`error.log` ファイルに `RRD4JReporter` 例外が表示されます。例外を停止するには、[!DNL Experience Manager] のインスタンスを再起動します。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* ユーザーは、[!DNL Assets] の階層内のフォルダーの名前を変更し、ネストされたフォルダーを [!DNL Brand Portal] に公開できます。ただし、ルートフォルダーが再公開されるまで、[!DNL Brand Portal] でフォルダーのタイトルは更新されません。

* [!DNL Experience Manager] 6.5.x.x のインストール中に、次のエラーや警告メッセージが表示される場合があります。
   * 「Target Standard API（IMS 認証）を使用して [!DNL Experience Manager] に Adobe Target 統合を設定する場合、エクスペリエンスフラグメントを Target に書き出すと、間違ったオファータイプが作成されます。Target では、「エクスペリエンスフラグメント」／ソース「Adobe Experience Manager」タイプではなく、「HTML」／ソース「Adobe Target Classic」タイプのオファーをいくつか作成します。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * SUM、MAX、MIN などの集計関数が使用される場合、アダプティブフォームのサーバー側検証が失敗します （CQ-4274424）。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - granite/operations/maintenance にメンテナンスウィンドウが見つかりません。
   * ショッパブルバナービューアでアセットをプレビューしている間、Dynamic Media インタラクティブ画像のホットスポットは表示されません。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`：登録状況を未登録に変更する処理が完了するのを待機中にタイムアウトになりました。

* AEM 6.5.15 以降、```org.apache.servicemix.bundles.rhino``` バンドルで提供される Rhino JavaScript Engine には、新しい巻上げ動作が追加されました。strict モード（```use strict;```）を使用するスクリプトでは、変数を正しく宣言する必要があります。宣言しない場合、変数は実行されず、代わりにランタイムエラーが発生します。

### AEM Forms の既知の問題

#### サポートされているプラットフォーム

* JDK 11.0.20 では、AEM Forms on JEE インストーラーのインストールをサポートしていません。AEM Forms on JEE インストーラーのインストールは、JDK 11.0.19 以前のバージョンのみがサポートしています。（FORMS-10659）

#### インストール

* JBoss® 7.1.4 プラットフォームで、Experience Manager 6.5.16.0 以降のサービスパックをインストールすると、`adobe-livecycle-jboss.ear` デプロイメントが失敗します。（CQ-4351522、CQDOC-20159）

<!-- 
* After upgrading to AEM Forms 6.5.18.0 JBoss&reg; Turnkey full installer environment on Windows Server 2022, when compiling Output client application code using Java&trade; 11, the following compilation error may occur:
  
  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  
  ```
  
  To resolve the issue, perform the following steps:
    1. Navigate to `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` and unzip `adobe-output-client.jar` to extract the `Manifest.mf` file.
    1. Update the `Manifest.mf` file by removing the entry `${clover.jar.name}` from the class-path attribute. 

        >[!NOTE]
        >
        > You can also use an in-place editing tool, for example, 7-zip, to update the `Manifest.mf` file.  

    1. Save the updated the `Manifest.mf` in the `adobe-output-client.jar` archive. 
    1. Save the modified `adobe-output-client.jar` file and rerun the setup. (CQDOC-20878) -->

* AEM サービスパック 6.5.19.0 フルインストーラーをインストールした後、JBoss® Turnkey を使用した JEE での EAR デプロイメントが失敗します。
問題を解決するには、設定マネージャーを実行する前に、`<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` ファイルを見つけて、すべての出現箇所について `Adobe_Adobe_JAVA_HOME` を `Adobe_JAVA_HOME` に更新します。（CQDOC-20803）

#### サーブレットフラグメント（AEM サービスパック 6.5.14.0 以前）のインストール

* AEM Service Pack 6.5.15.0以降にアップグレードし、AEMインスタンスが Tomcat 8.5.88 で動作している場合は、サーブレットフラグメントをインストールする必要があります *前* Service Pack 6.5.15.0以降のインストールを続行します。
* JBoss® EAP 7.4.0 で実行されているものを除き、すべてのアプリケーションサーバーのサーブレットフラグメントをインストールする必要があります。

**サーブレットフラグメントをインストールするには：**

1. [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)からサーブレットフラグメントをダウンロードします。
1. アプリケーションサーバーを起動します。
1. ログが安定するのを待ってから、バンドルの状態を確認します。
1. Web コンソールのバンドルを開きます。デフォルトの URL は `http://[Server]:[Port]/system/console/bundles` です。
1. 「**[!UICONTROL インストール]**」または「**[!UICONTROL 更新]**」を選択します。
1. ダウンロードしたフラグメントを選択します
   `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`
1. 「**[!UICONTROL インストール]**」または「**[!UICONTROL 更新]**」を選択します。
1. アプリケーションサーバーが安定するまで待ちます。
1. アプリケーションサーバーを停止します。

#### アダプティブフォーム

* アダプティブフォームを公開すると、変更していない場合でも、ポリシーを含むすべての依存関係が再公開されます。（FORMS-10454）
* アダプティブフォームでユーザーが初めてフィールドを設定する場合、設定を保存するオプションはプロパティブラウザーに表示されません。同じエディターでアダプティブフォームの他のフィールドを設定するように選択すると、問題が解決します。
* ユーザーが送信アクションを実行すると、送信は次のエラーで失敗します。
  ` javax.servlet.ServletException: java.lang.NoSuchMethodError`
問題を解決するには、 [JSP、Java、Sightly などの Sling スクリプトを再コンパイルします。](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=en#resolution). （FORMS-8542）


## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、[!DNL Experience Manager] 6.5.19.0 に含まれている OSGi バンドルとコンテンツパッケージのリストが記載されています。<!-- UPDATE FOR EACH NEW RELEASE -->

* [Experience Manager 6.5.19.0 に含まれている OSGi バンドルのリスト](/help/release-notes/assets/65190_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5.19.0 に含まれているコンテンツパッケージのリスト](/help/release-notes/assets/65190_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=ja)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 製品ページ](https://business.adobe.com/jp/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5 ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
>* [アドビ製品アップデートの優先通知に登録する](https://www.adobe.com/subscription/priority-product-update.html)
