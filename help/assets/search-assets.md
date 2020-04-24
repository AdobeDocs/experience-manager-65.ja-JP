---
title: Adobe Experience Managerでのデジタルアセットと画像の検索
description: フィルターパネルを使用して、Adobe Experience Managerで必要なアセットを検索する方法と、検索に表示されるアセットを使用する方法を説明します。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Adobe Experience Managerでのアセットの検索 {#search-assets-in-aem}

Adobe Experience Manager Assetsは、より高速なコンテンツ速度を実現するための堅牢なアセット検出方法を提供します。 標準搭載の機能とカスタム方法を使用して、シームレスでインテリジェントな検索を実現し、チームがタイム・トゥ・マーケティングを短縮します。 アセットの検索は、デジタルアセット管理システムの利用の中核を成します。用途は、クリエイティブ担当者によるさらなる利用、ビジネスユーザーやマーケティング担当者によるアセットの堅牢な管理、DAM 管理者による管理などです。Experience Manager Assetsのユーザーインターフェイスや他のアプリケーションやサーフェスを介して実行できる、シンプル、高度、カスタムの検索は、これらの使用例を満たすのに役立ちます。

Experience Manager Assetsでは、次の使用例がサポートされています。この記事では、これらの使用例の使用方法、概念、設定、制限およびトラブルシューティングについて説明します。

| アセットの検索 | 設定と管理 | 検索結果の操作 |
|---|---|---|
| [基本検索](#searchbasics) | [検索インデックス](#searchindex) | [結果の並べ替え](#sort) |
| [検索 UI について](#searchui) | [視覚検索または類似性検索](#configvisualsearch) | [アセットのプロパティとメタデータの確認](#checkinfo) |
| [検索候補](#searchsuggestions) | [必須メタデータ](#mandatorymetadata) | [ダウンロード](#download) |
| [検索結果および動作について](#searchbehavior) | [検索ファセットの変更](#searchfacets) | [メタデータの一括更新](#metadataupdates) |
| [検索ランキングおよびブースト](#searchrank) | [テキスト抽出](#extracttextupload) | [スマートコレクション](#collections) |
| [詳細検索：検索のフィルタリングと範囲](#scope) | [カスタム述語](#custompredicates) | [予期しない検索結果と検索に関連する問題のトラブルシューティング](#troubleshoot-unexpected-search-results-and-issues) |
| [他のソリューションやアプリから検索](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[Experience Managerデスクトップアプリケーション](#desktopapp)</li><li>[Adobe Stock 画像](#adobestock)</li><li>[Dynamic Media アセット](#dynamicmedia)</li></ul> |  |  |
| [アセットピッカー](#assetselector) |  |  |
| [制限事項](#limitations)と[ヒント](#tips) |  |  |
| [例を使った説明](#samples) |  |  |

Experience Manager Webインターフェイスの上部にあるOmnisearchフィールドを使用して、アセットを検索します。 Go to **[!UICONTROL Assets]** > **[!UICONTROL Files]** in Experience Manager , click search icon in top bar, enter search keyword, and press return. または、キーワードショートカット/（スラッシュ）を使用してOmnisearchフィールドを開きます。 場所：検索をDAMアセットに制限するために、アセットが事前に選択されています。 検索キーワードを入力すると、Experience Managerで開始に提案が表示されます。

フィルターパネルを使用して **** 、ファイルタイプ、ファイルサイズ、最終変更日、アセットのステータス、インサイトデータ、Adobe Stockのライセンスなど、様々なオプション（予測）に基づいて検索結果をフィルタリングし、検索結果を絞り込みます。 管理者は、検索ファセットを使用して、フィルターパネルをカスタマイズし、検索述部を追加または削除することができます。 [ [!UICONTROL フィルター] ]パネルの[ファイルタイプ]フィ [!UICONTROL ルタには] 、混在状態のチェックボックスがあります。 したがって、ネストされた述語（またはフォーマット）をすべて選択しない限り、第1レベルのチェックボックスは部分的にオンになります。

Experience Managerの検索機能では、コレクションの検索と、コレクション内のアセットの検索がサポートされています。 詳しくは、[コレクションの検索](/help/assets/managing-collections-touch-ui.md)を参照してください。

## 検索インターフェイスについて {#searchui}

検索インターフェイスと使用可能なアクションについて理解します。

![Experience Manager Assetsの検索結果インターフェイスを理解する](assets/aem_search_results.png)

*図：Experience Manager Assetsの検索結果インターフェイスを理解する*

**A.** 検索をスマートコレクションとして保存します。 **B.** フィルターまたは述部を使用して、検索結果を絞り込みます。 **C.ファイル** 、フォルダ、またはその両方を表示します。 **D：**「フィルター」をクリックすると、左側のパネルが開くまたは閉じます。**E：** DAM が検索場所になります。**F.** ユーザが指定した検索キーワードを含むOmnisearchフィールド。 **G.** 読み込まれた検索結果を選択します。 **H.** 検索結果の合計の中で表示された検索結果の数。 **私。** 検索 **Jを閉じる** カードの表示とリスト表示

### 動的検索ファセット {#dynamicfacets}

検索ファセット内で予想される検索結果の数は動的に更新されますが、この数を使用して、検索結果ページから目的のアセットをより迅速に見つけることができます。検索フィルターを適用する前であっても、予想されるアセット数は更新されます。フィルターに対して予想されるアセット数を確認すると、検索結果をすばやく効率的にナビゲートすることができます。For more info, see [Search assets in Experience Manager](search-assets.md).

![検索ファセットで検索結果をフィルタリングしない場合のアセット概数の表示](assets/asset_search_results_in_facets_filters.png)

*図：検索結果を検索ファセットでフィルタリングせずに、およその数のアセットを確認する*

## 検索結果および動作について {#searchbehavior}

### 基本的な検索用語と検索結果 {#searchbasics}

オムニサーチフィールドからキーワード検索を実行できます。キーワード検索では大文字と小文字が区別されず、（よく使用されるメタデータフィールド全体での）全文検索です。 複数のキーワードを検索する場合、キーワード間の初期設定の演算子は初期設定の検索で、アセ `AND` ットにスマートタグが付けら `OR` れている場合に検索が行われます。

結果は、最も近い一致を先頭に関連性の高い順に並べ替えられます。複数のキーワードがある場合は、メタデータに含まれるキーワードが多いアセットが、より関連性の高い結果になります。メタデータ内では、スマートタグとして表示されるキーワードは、他のメタデータフィールドに表示されるキーワードより高くランク付けされます。Experience Managerでは、特定の検索用語をより高い重み付けで表示。 Also, it is possible to [boost the rank](#searchrank) of a few targeted assets for specific search terms.

関連性の高いアセットをすばやく見つけるために、この機能豊富なインターフェイスには、フィルタリング、並べ替え、選択のメカニズムが用意されています。複数の条件に基づいて結果をフィルタリングし、検索されたアセットの数を様々なフィルター別に確認できます。または、オムニサーチフィールドのクエリを変更して検索を再実行することもできます。検索用語やフィルターを変更しても、その他のフィルターは依然として適用され、検索のコンテキストが保たれます。

結果が多数のアセットである場合、Experience Managerでは最初の100がカード表示に、200がリスト表示に表示されます。 ユーザがスクロールすると、読み込まれるアセットが増えます。 これは、パフォーマンスを向上させるためです。

>[!VIDEO](https://www.youtube.com/watch?v=LcrGPDLDf4o)

時には、予期しないアセットが検索結果に表示される場合があります。詳しくは、[予期しない検索結果](#troubleshoot-unexpected-search-results-and-issues)を参照してください。

Experience Managerでは様々なファイル形式を検索でき、検索フィルターはビジネス要件に合わせてカスタマイズできます。 DAMリポジトリで使用可能になっている検索オプションと、アカウントにどのような制限があるかについては、管理者に問い合わせてください。

### 強化されたスマートタグのある場合とない場合の結果 {#withsmarttags}

デフォルトでは、Experience Managerの検索では検索用語とAND句が結合されます。 例えば、「woman running」というキーワードを検索するとします。 メタデータに「woman」と「running」の両方のキーワードを含むアセットのみが、デフォルトで検索結果に表示されます。 特殊文字（ピリオド、アンダースコアまたはダッシュ）をキーワードと共に使用する場合も、同じ動作が保持されます。 次の検索クエリは同じ結果を返します。

* `woman running`
* `woman.running`
* `woman-running`

ただし、クエリは、メタ `woman -running` データを含まな `running` いアセットを返します。
Using smart tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. つまり、検索結果は、以下を組み合わせたものになります。

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* いずれかのキーワードでスマートタグ付けされたアセット（スマートタグの動作）

### 入力に応じて提示される検索候補 {#searchsuggestions}

キーワードの開始入力時に、Experience Managerによって検索キーワードや語句の候補が表示されます。 提案は、既存のアセットのメタデータに基づいて行われます。 Experience Managerは、検索に役立つすべてのメタデータフィールドのインデックスを作成します。 検索候補を提示するために、以下のいくつかのメタデータフィールドの値が使用されます。検索候補の提示をおこなう場合は、次のフィールドに適切なキーワードを入力することを検討してください。

* アセットのタグ（`jcr:content/metadata/cq:tags` にマッピングされます）
* アセットのタイトル（`jcr:content/metadata/dc:title` にマッピングされます）
* アセットの説明（`jcr:content/metadata/dc:description` にマッピングされます）
* JCR リポジトリ内でのタイトル。この値はアセットのタイトルにマッピングされる可能性があります（`jcr:content/jcr:title` にマッピングされます）
* JCR リポジトリ内での説明。この値はアセットの説明にマッピングされる可能性があります（`jcr:content/jcr:description` にマッピングされます）

複数の検索キーワードのサーチクエリを受け取る場合は、1つのキーワードのサーチクエリを選択せずに、引き続きすべてのキーワードを入力します。

![複数のキーワードを入力して、表示の提案をすべてに適合させる](assets/search_suggestionsmanykeywords.gif)

*図：複数のキーワードを入力して、表示の提案をすべてに適合させる*

### 検索ランキングおよびブースト {#searchrank}

メタデータフィールド内のすべての検索用語に一致する検索結果が最初に表示され、スマートタグ内の検索用語のいずれかに一致する検索結果はその後に表示されます。上記の例の場合、検索結果が表示される順序はおおよそ次のようになります。

1. 各種メタデータフィールド内の「`woman running`」に一致するもの。
1. スマートタグ内の「`woman running`」に一致するもの。
1. スマートタグ内の「`woman`」または「`running`」に一致するもの。

特定のアセットに対するキーワードの有効性を高めることで、キーワードに基づいた検索を強化できます。つまり、特定のキーワードを昇格させた場合、それらのキーワードに基づいて検索すると、それらのキーワードの対象となる画像が検索結果の最上部に表示されます。

1. Assets ユーザーインターフェイスから、アセットのプロパティページを開きます。「**[!UICONTROL 詳細]**」をクリックし、「**[!UICONTROL 検索キーワードに採用]**」の下の「**[!UICONTROL 追加]**」をクリックまたはタップします。
1. 「**[!UICONTROL 昇格を検索]**」ボックスで、画像検索時の強化の対象となるキーワードを指定し、「**[!UICONTROL 追加]**」をクリックまたはタップします。同じ方法で複数のキーワードを指定できます。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックまたはタップします。昇格したこのキーワードの対象となるアセットが、検索結果の上位に表示されます。

ターゲットを絞ったキーワードの検索結果で一部のアセットのランクを上げることで、この機能をうまく利用できます。以下の例（ビデオ）を参照してください。For detailed info, see [search in Experience Manager](https://helpx.adobe.com/experience-manager/kt/assets/using/search-feature-video-use.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*検索結果のランク付けの方法とランクへの影響について*

## 詳細検索 {#scope}

Experience Managerには、検索したアセットに適用されるフィルターなど、様々な方法が用意されており、目的のアセットをすばやく見つけることができます。 一般的に使用されるいくつかの方法を以下で説明します。[動作例](#samples)もいくつか以下に示します。

**ファイルまたはフォルダーの検索**：検索結果には、ファイル、フォルダーまたはその両方が表示されます。**[!UICONTROL フィルター]**&#x200B;パネルから、適切なオプションを選択できます。詳しくは、[検索インターフェイス](#searchui)を参照してください。

**フォルダー内のアセットの検索**：検索対象を特定のフォルダーに限定できます。**[!UICONTROL フィルター]**&#x200B;パネルで、フォルダーのパスを追加します。一度に 1 つのフォルダーのみ選択できます。

![フィルターパネルにフォルダーパスを追加して検索結果を特定のフォルダーに限定](assets/search_folder_select.gif)

*図：フォルダパネルにフォルダパスを追加して、検索結果をフォルダにフィルターする*

### 類似の画像の検索 {#visualsearch}

ユーザーが選択した画像と視覚的に類似した画像を検索するには、画像のカード表示またはツールバーから「**[!UICONTROL 類似を検索]**」オプションをクリックします。Experience Managerに、ユーザーが選択した画像に類似した、DAMリポジトリのスマートタグ付き画像が表示されます。 [類似性検索の設定方法](#configvisualsearch)を参照してください。

![カードのオプションを使用して類似の画像を検索する表示](assets/search_find_similar.png)

*図：カードのオプションを使用して類似の画像を検索する表示*

### Adobe Stock 画像 {#adobestock}

From within the Experience Manager user interface, users can search [Adobe Stock assets](/help/assets/aem-assets-adobe-stock.md) and license the required assets. オムニサーチバーに「`Location: Adobe Stock`」を追加します。また、フィルターパネルを使用して、ライセンス取得済みまたはライセンス未取得のアセットをすべて検索したり、Adobe Stock ファイル番号を使用して特定のアセットを検索したりすることもできます。

### Dynamic Media アセット {#dmassets}

**[!UICONTROL フィルター]**&#x200B;パネルから **[!UICONTROL Dynamic Media]**／**[!UICONTROL セット]**&#x200B;を選択して、Dynamic Media 画像をフィルタリングすることができます。画像セット、カルーセル、混在メディアセット、スピンセットなどのアセットがフィルタリングされて表示されます。

### メタデータフィールドの特定の値を使用した検索 {#gqlsearch}

タイトル、説明、作成者など、特定のメタデータフィールドの正確な値に基づいてアセットを検索できます。 GQL 全文検索機能では、メタデータ値が検索クエリと完全に一致するアセットのみを取得できます。プロパティの名前（author や title など）と値は、大文字と小文字が区別されます。

| メタデータフィールド | ファセット値と使用法 |
|---|---|
| タイトル | title:John |
| 作成者 | creator:John |
| 場所 | location:NA |
| 説明 | description:&quot;Sample Image&quot; |
| 作成ツール | creatortool:&quot;Adobe Photoshop CC 2015&quot; |
| 著作権の所有者 | copyrightowner:&quot;Adobe Systems&quot; |
| 投稿者 | contributor:John |
| 使用条件 | usageterms:&quot;CopyRights Reserved&quot; |
| 作成日 | created:YYYY-MM-DDTHH |
| 有効期限 | expires:YYYY-MM-DDTHH |
| オンタイム | ontime:YYYY-MM-DDTHH |
| オフタイム | offtime:YYYY-MM-DDTHH |
| 時間の範囲（有効期限、オンタイム、オフタイム） | facet field : lowerbound..upperbound |
| パス | /content/dam/&lt;folder name> |
| PDF タイトル | pdftitle:&quot;Adobe Document&quot; |
| 件名 | subject:&quot;Training&quot; |
| タグ | tags:&quot;Location And Travel&quot; |
| タイプ | type:&quot;image\png&quot; |
| 画像の幅 | width:lowerbound..upperbound |
| 画像の高さ | height:lowerbound..upperbound |
| 人 | person:John |

path、limit、size および orderby の各プロパティを他のプロパティと OR で結合することはできません。

ユーザー生成プロパティのキーワードは、プロパティエディターにおけるフィールドラベルからスペースを削除して小文字で表記したものです。

複雑なクエリの検索形式の例：

* 複数のファセットフィールドを持つアセットをすべて表示する（例：title=John Doe および creatortool=Adobe Photoshop）： `tiltle:"John Doe" creatortool : Adobe*`
* ファセット値が 1 語でなく文になっているアセットをすべて表示する（例：title=Scott Reynolds）：`title:"Scott Reynolds"`
* 1 つのプロパティに複数の値が指定されているアセットを表示する（例：title=Scott Reynolds または John Doe）：`title:"Scott Reynolds" OR "John Doe"`
* プロパティ値が特定の文字列で始まるアセットを表示する（例：title=Scott Reynolds）：`title:Scott*`
* プロパティ値が特定の文字列で終わるアセットを表示する（例：title=Scott Reynolds）：`title:*Reynolds`
* プロパティ値に特定の文字列が含まれるアセットを表示する（例：title=Basel Meeting Room）：`title:*Meeting*`
* 特定の文字列が含まれ、特定のプロパティ値を持つアセットを表示する（例：title=John Doe のアセットで文字列「Adobe」を検索する）：`*Adobe* title:"John Doe"`

## Search assets from other Experience Manager offerings or interfaces {#beyondomnisearch}

Adobe Experience Managerは、DAMリポジトリを他の様々なExperience Managerソリューションに接続して、デジタルアセットへのアクセスを高速化し、クリエイティブワークフローを効率化します。 アセットの検出は、参照または検索で始まります。異なるサーフェスやソリューションでも、検索の動作はほとんど同じです。検索方法の中には、ターゲットオーディエンス、使用例、ユーザーインターフェイスがExperience Managerソリューションによって異なるので、変更されるものもあります。 個々のソリューションの具体的な方法については、以下のリンクを参照してください。ここでは、一般に当てはまるヒントや動作について説明しています。

### Adobe Asset Link パネルからのアセットの検索 {#aal}

クリエイティブプロフェッショナルは、Adobe Asset Linkを使用して、サポートされているAdobe Creative Cloudアプリケーションから離れることなく、Experience Manager Assetsに保存されたコンテンツにアクセスできるようになりました。 また、Photoshop、Illustrator、InDesign などの Creative Cloud アプリ内のパネルを使用して、アセットをシームレスに参照、検索、チェックアウトおよびチェックインすることができます。また、Asset Link を使用すると、視覚的に類似した結果を検索できます。ビジュアル検索の表示結果は、Adobe Sensei の機械学習アルゴリズムを活用しており、見た目に類似した画像を見つけやすくなっています。詳しくは、[Adobe Asset Link を使用したアセットの検索と参照](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)を参照してください。

### Experience Managerデスクトップアプリでのアセットの検索 {#desktopapp}

クリエイティブプロフェッショナルは、デスクトップアプリを使用して、Experience Manager Assetsをローカルデスクトップ（WindowsまたはMac OS）で簡単に検索および利用できるようにします。 クリエイティブは、Mac FinderまたはWindowsエクスプローラーで目的のアセットを簡単に表示し、デスクトップアプリケーションで開いてローカルで変更し、Experience Managerに保存し、リポジトリで新しいバージョンを作成して変更を反映させることができます。 1 つ以上のキーワード、ワイルドカード * および ？、AND 演算子を使用した基本検索がサポートされています。[デスクトップアプリケーションでのアセットの参照、検索、プレビュー](https://docs.adobe.com/content/help/ja-JP/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)を参照してください。

### Brand Portal でのアセットの検索 {#brandportal}

マーケティング担当者や事業部門のユーザーは、Brand Portal を使用して、承認済みのデジタルアセットを、広範な社内チーム、パートナーおよび販売店と効率的かつ安全に共有します。詳しくは、[Brand Portal でのアセットの検索](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html)を参照してください。

### Adobe Stock 画像の検索 {#adobestock-1}

ユーザーは、Experience Managerユーザーインターフェイス内からAdobe Stockアセットを検索し、必要なアセットのライセンスを取得できます。 オムニサーチフィールドに「`Location: Adobe Stock`」を追加します。また、**[!UICONTROL フィルター]**&#x200B;パネルを使用して、ライセンス取得済みまたはライセンス未取得のアセットをすべて検索したり、Adobe Stock ファイル番号を使用して特定のアセットを検索したりすることもできます。See [manage Adobe Stock images in Experience Manager](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Dynamic Media アセットの検索 {#dynamicmedia}

**[!UICONTROL フィルター]**&#x200B;パネルから **[!UICONTROL Dynamic Media]**／**[!UICONTROL セット]**&#x200B;を選択して、Dynamic Media 画像をフィルタリングすることができます。画像セット、カルーセル、混在メディアセット、スピンセットなどのアセットがフィルタリングされて表示されます。Web ページの作成時に、作成者はコンテンツファインダー内でセットを検索できます。セットのフィルターは、ポップアップメニューで使用できます。

### Web ページ作成時のコンテンツファインダーでのアセットの検索 {#contentfinder}

作成者は、コンテンツファインダーを使用して関連アセットを DAM リポジトリで検索し、作成中の Web ページで使用できます。作成者は、接続されたアセット機能を使用して、リモートのExperience Managerデプロイメントで使用可能なアセットを検索することもできます。 作成者は、これらのアセットをローカルのExperience ManagerデプロイメントのWebページで使用できます。 See [use remote assets](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### コレクションの検索 {#collections}

Experience Managerの検索機能では、コレクションの検索と、コレクション内のアセットの検索がサポートされています。 詳しくは、[コレクションの検索](/help/assets/managing-collections-touch-ui.md)を参照してください。

## アセットピッカー {#assetselector}

アセット選択を使用すると、DAMアセットを特別な方法で検索、フィルタリングおよび参照できます。 Asset Picker is available at `https://[aem-server]:[port]/aem/assetpicker.html`. この機能を使用して、選択したアセットのメタデータを取得できます。 アセットタイプ（画像、ビデオ、テキスト）や選択モード（単一選択または複数選択）など、サポートされているリクエストパラメーターを使用して、アセットセレクターを起動できます。これらのパラメーターは、特定の検索インスタンスのアセットピッカーのコンテキストを設定し、選択範囲全体を通してそのまま残ります。

The asset Picker uses the HTML5 `Window.postMessage` message to send data for the selected asset to the recipient. アセットピッカーは、参照モードでのみ機能し、Omnisearch結果ページでのみ機能します。

URLに次のリクエストパラメーターを渡して、特定のコンテキストでアセットピッカーを起動できます。

| 名前 | 値 | 例 | 目的 |
|---|---|---|---|
| resource suffix (B) | URL のリソースサフィックスとしてのフォルダーパス：[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | To launch the asset Picker with a particular folder selected, for example with the folder `/content/dam/we-retail/en/activities` selected, the URL should be of the form: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | アセットセレクターの起動時に特定のフォルダーを選択する必要がある場合、そのフォルダーをリソースサフィックスとして渡します。 |
| mode | single、multiple | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | 複数モードでは、アセットセレクターを使用して、いくつかのアセットを同時に選択できます。 |
| mimetype | アセットの MIME タイプ（`/jcr:content/metadata/dc:format`）（ワイルドカードもサポートされています） | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png)</li></ul> | MIME タイプに基づいてアセットをフィルタリングするために使用します |
| dialog | true、false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | アセットセレクターを Granite ダイアログとして開くには、これらのパラメーターを使用します。このオプションは、Granite パスフィールドを使用してアセットセレクターを起動し、pickerSrc URL として設定する場合にのみ適用できます。 |
| assettype (S) | images、documents、multimedia、archives | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | 渡された値に基づいてアセットタイプをフィルタリングするには、このオプションを使用します。 |
| root | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | アセットセレクターのルートフォルダーを指定するには、このオプションを使用します。この場合、アセットセレクターを使用すると、ルートフォルダーの下の子アセット（直接／間接）のみを選択できます。 |

To access the asset Picker interface, go to `https://[aem_server]:[port]/aem/assetpicker`. 目的のフォルダーに移動して、1 つまたは複数のアセットを選択します。または、オムニサーチボックスから目的のアセットを検索し、必要に応じてフィルターを適用して選択します。

![アセットピッカーでのアセットの参照と選択](assets/assetpicker.png)

*図：アセットピッカーでアセットを参照して選択します。*

## 制限事項 {#limitations}

Experience Manager Assetsの検索機能には、次の制限があります。

* 検索クエリの先頭にスペースを入れないでください。スペースを入れると、検索が機能しません。
* Experience Manager may continue to show the search term after you select properties of an asset from searched results and then cancel the search. <!-- (CQ-4273540) -->
* フォルダーまたはファイルとフォルダーを検索する場合、どのパラメーターでも検索結果を並べ替えることはできません。
* Omnisearchバーに何も入力しないでReturnキーを押すと、Experience Managerはファイルのみのリストを返し、フォルダーは返しません。 キーワードを使用せずに特定のフォルダーを検索した場合、Experience Managerは結果を返しません。
* 検索ペー **[!UICONTROL ジの右上隅にある]** 「すべて選択」オプションを使用して、検索したアセットを選択します。 Experience Managerでは、最初に100個のアセットがカード表示で、200個のアセットがリスト表示で表示されます。 検索結果をスクロールすると、読み込まれるアセットが増えます。 読み込まれたアセットより多くのアセットを選択できます。 選択したアセットの数が、検索結果ページの右上隅に表示されます。 選択範囲に対して操作を行うことができます。例えば、選択したアセットのダウンロード、選択したアセットのメタデータプロパティの一括更新、選択したアセットのコレクションへの追加などが可能です。 表示されている数より多くのアセットが選択されている場合は、選択したすべてのアセットにアクションが適用されるか、ダイアログに適用されたアセットの数が表示されます。 読み込まれなかったアセットにアクションを適用するには、すべてのアセットが明示的に選択されていることを確認します。

ビジュアル検索または類似検索には、次の制限事項があります。

* ビジュアル検索は、より大きなリポジトリで最も有効に機能します。良好な結果を得るために最低限必要な画像数はありませんが、画像の数が少ないと、一致の精度が大きなリポジトリの場合ほど良くない可能性があります。
* モデルを変更したり、Experience Managerをトレーニングして類似の画像を見つけることはできません。 例えば、一部のアセットにスマートタグを追加または削除しても、モデルは変更されません。それらのアセットは、視覚的に類似した検索結果から除外されます。

次のシナリオでは、検索機能のパフォーマンスに制限がある場合があります。

* カードの表示は、検索結果を表示するリスト表示と比較して、読み込み時間が短くなりました。

## 検索のヒント {#tips}

* アセットのレビューステータスを監視する場合は、該当するオプションを使用して、承認されているアセットまたは承認待ちのアセットを検索します。
* 様々な Creative アプリから取得した使用状況の統計に基づいて、サポートされるアセットを検索するには、インサイトの述語を使用します。使用状況データが、使用状況スコア、インプレッション数、クリック数およびメディアチャネルでグループ化され、アセットがカテゴリ別に表示されます。
* 「すべて選択」 **[!UICONTROL チェックボックスを使用し]** 、検索したアセットを選択します。 Experience Managerでは、最初に100個のアセットがカード表示で、200個のアセットがリスト表示で表示されます。 検索結果をスクロールすると、読み込まれるアセットが増えます。 読み込まれたアセットより多くのアセットを選択できます。 選択したアセットの数が、検索結果ページの右上隅に表示されます。 選択範囲に対して操作を行うことができます。例えば、選択したアセットのダウンロード、選択したアセットのメタデータプロパティの一括更新、選択したアセットのコレクションへの追加などが可能です。 表示されている数より多くのアセットが選択されている場合は、選択したすべてのアセットにアクションが適用されるか、ダイアログに適用されたアセットの数が表示されます。 読み込まれなかったアセットにアクションを適用するには、すべてのアセットが明示的に選択されていることを確認します。
* 必須メタデータを含んでいないアセットを検索する場合は、[必須メタデータ](#mandatorymetadata)を参照してください。
* 検索では、すべてのメタデータフィールドが使用されます。12 の検索などの一般的な検索では通常、多数の結果が返されます。より良い結果を得るには、（一重引用符ではなく）二重引用符を使用するか、特殊文字のない単語に番号が続いている（例：*shoe12* など）ようにします。
* 全文検索では、- や ^ などの演算子をサポートしています。これらの文字を文字列リテラルとして検索するには、検索式を二重引用符で囲みます。例えば、「Notebook - Beauty」ではなく、「&quot;Notebook - Beauty&quot;」と指定します。
* 検索結果が多すぎる場合は、[検索範囲](#scope)を制限して、目的のアセットを絞り込みます。これは、特定のファイルタイプ、特定の場所、特定のメタデータなど、目的のアセットを検索する良い方法がある程度わかっている場合に最も効果的です。

* **タグ付け**：タグを使用すると、アセットを分類して参照や検索をより効率的におこなえるようになります。タグ付けは、適切な分類を他のユーザーやワークフローに伝播するうえで役に立ちます。Experience Managerのオファー方法を使用すると、Adobe Senseiの人為的にインテリジェントなサービスを使用して、アセットに自動的にタグ付けし、使用状況やトレーニングでアセットをより効率的にタグ付けできます。 この機能がアカウントで有効な場合は、アセットを検索する際にスマートタグが考慮されます。これは組み込みの検索機能と連携して機能します。[検索動作](#searchbehavior)を参照してください。検索結果の表示順序を最適化するには、選択した一部のアセットの[検索ランキングを上げる](#searchrank)ことができます。

* **インデックス作成**：インデックスが作成されたメタデータおよびアセットのみが検索結果に返されます。検索範囲とパフォーマンスを向上させるには、適切なインデックス作成をおこない、ベストプラクティスに従ってください。詳しくは、[インデックス作成](#searchindex)を参照してください。

## 検索の例 {#samples}

ユーザーが指定したとおりの語句を含んだアセットを検索するには、キーワードを二重引用符で囲みます。

![引用符がある場合とない場合の検索動作](assets/search_with_quotes.gif)

*図：検索動作（引用符付き）と引用符なし*

**アスタリスクワイルドカードを使用した検索**：検索の範囲を広げるには、検索語の前後にアスタリスクを使用して任意の数の文字に一致するようにします。例えば、アスタリスクを付けずに「run」を検索しても、（メタデータ内も含め）検索語のバリエーションを含んだアセットは返されません。アスタリスクは任意の数の文字に置き換わります。以下に例を示します。

* `run`：キーワード「run」を含んだアセットを返します。
* `run*`：「running」、「run」、「runaway」などを含んだアセットを返します。
* `*run`：「outrun」、「rerun」などを含んだアセットを返します。
* `*run*`：可能なあらゆる組み合わせを含んだアセットを返します。

![アセット検索でのアスタリスクワイルドカードの使用例](assets/search_with_asterisk_run.gif)

*図：例を使用したアセット検索でのアスタリスクワイルドカードの使用例*

**疑問符ワイルドカードを使用した検索**：検索の範囲を広げるには、1 つ以上の「?」文字を使用して正確な数の文字に一致するようにします。例えば、次の例では、

* `run???` クエリはどのアセットとも一致しません。

* `run????` クエリは、`run` の後に 4 文字がある単語 `running` と一致します。

* `??run` クエリは、`run` の前に 2 文字がある単語 `rerun` と一致します。

![アセット検索での疑問符ワイルドカードの使用例](assets/search_with_questionmark_run.gif)

*図：例を使用したアセット検索での疑問符ワイルドカードの使用例*

**キーワードの除外**：ダッシュを使用すると、キーワードを含まないアセットを検索できます。例えば、`running -shoe` クエリでは、`running` を含み `shoe` を含まないアセットを返します。同様に、`camp -night` クエリでは`camp` を含み `night` を含まないアセットを返します。なお、`camp-night` クエリの場合は、`camp` と `night` の両方を含むアセットを返すので、注意してください。

![ダッシュを使用して、除外されたキーワードを含まないアセットを検索する](assets/search_dash_exclude_keyword.gif)

*図：ダッシュを使用して、除外されたキーワードを含まないアセットを検索する*

## 検索機能に関連するタスクの設定と管理 {#configadmin}

### 検索インデックスの設定 {#searchindex}

アセットの検出は、メタデータを含むDAMコンテンツのインデックス作成に依存します。 迅速で正確なアセットの検出は、最適化されたインデックス作成と適切な設定に依存しています。 「検索インデ [ックス](/help/assets/performance-tuning-guidelines.md#search-indexes)」、「Oakクエリとインデ [ックス作成](/help/sites-deploying/queries-and-indexing.md)」、「ベストプラクティス [」を参照してください](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

### 視覚検索または類似性検索 {#configvisualsearch}

ビジュアル検索ではスマートタグを使用し、Experience Manager 6.5.2.0以降が必要です。 スマートタグ機能を設定した後、次の手順に従います。

1. Experience Manager CRXDEのノードで、 `/oak:index/lucene` 次のプロパティと値を追加し、変更を保存します。

   * `costPerEntry` 値を持つタイプ `Double` のプロパティ `10`。

   * `costPerExecution` 値を持つタイプ `Double` のプロパティ `2`。

   * `refresh` 値を持つタイプ `Boolean` のプロパティ `true`。
   この設定により、適切なインデックスからの検索が可能になります。

1. Luceneインデックスを作成するには、CRXDEで、次のタ `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`イプのノードを作 `imageFeatures` 成しま `nt-unstructured`す。 ノード `imageFeatures` 内で、

   * 値を追加持つタイ `name` プのプロパテ `String``jcr:content/metadata/imageFeatures/haystack0`ィ。

   * の値追加を持つタ `nodeScopeIndex` イプのプロパティで `Boolean``true`す。

   * の値追加を持つタ `propertyIndex` イプのプロパティで `Boolean``true`す。

   * 値を追加持つタイ `useInSimilarity` プのプロパテ `Boolean``true`ィ。
   変更内容を保存します。

1. の値を `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` 持つタ `similarityTags` イプのプロパテ `Boolean` ィにアクセスし、追加しま `true`す。
1. スマートタグをExperience Managerリポジトリのアセットに適用します。 スマート [タグの設定方法を参照してください](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)。
1. CRXDEのnodeで、プ `/oak-index/damAssetLucene` ロパティをに設 `reindex` 定します `true`。 変更内容を保存します。
1. （オプション）検索フォームをカスタマイズした場合は、ノードをにコ `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` ピーしま `/conf/global/settings/dam/search/facets/assets/jcr:content/items`す。 すべての変更を保存します。

関連情報については、Experience Managerでのス [マートタグの理解と](https://helpx.adobe.com/experience-manager/kt/assets/using/smart-tags-feature-video-understand.html) 、スマートタ [グの管理方法を参照してください](/help/assets/managing-smart-tags.md)。

### 必須メタデータ {#mandatorymetadata}

ビジネスユーザー、管理者またはDAMライブラリは、ビジネスプロセスが機能するための必須の必須メタデータとして、一部のメタデータを定義できます。 様々な理由で、既存のアセットや一括で移行されたアセットなど、一部のアセットにこのメタデータが欠落している可能性があります。 メタデータがないか無効なアセットが検出され、インデックス付きのメタデータプロパティに基づいてレポートされます。 設定するには、必須のメタデータを [参照してくださ](/help/assets/metadata-schemas.md#define-mandatory-metadata)い。

### 検索ファセットの変更 {#searchfacets}

検出の速度を向上させるために、Experience Manager Assetsオファーは検索ファセットを検索し、これを使用して検索結果をフィルタリングできます。 フィルターパネルには、デフォルトでいくつかの標準ファセットが含まれています。 管理者は、フィルターパネルをカスタマイズして、組み込み述語を使用してデフォルトのファセットを変更できます。 Experience Managerには、組み込みの述語の適切なコレクションと、ファセットをカスタマイズするエディターが用意されています。 検索ファセ [ットを参照](/help/assets/search-facets.md)。

### アセットのアップロード時のテキストの抽出 {#extracttextupload}

ユーザーがPSDやPDFファイルなどのアセットをアップロードする際に、アセットからテキストを抽出するようにExperience Managerを設定できます。 Experience Managerは、抽出されたテキストのインデックスを作成し、抽出されたテキストに基づいてこれらのアセットを検索するのに役立ちます。 See [upload assets](/help/assets/managing-assets-touch-ui.md#uploading-assets).

### 検索結果をフィルタするカスタム述語 {#custompredicates}

述部は、ファセットの作成に使用されます。 管理者は、事前設定の述語を使用して、フィルターパネルの検索ファセットをカスタマイズできます。 これらの述語は、オーバーレイを使用してカスタマイズできます。 「カスタム述 [部の作成」を参照してくださ](/help/assets/searchx.md)い。

デジタルアセットは、次の1つ以上のプロパティに基づいて検索できます。 これらのプロパティの一部に適用されるフィルターは、デフォルトで使用でき、他のフィルターの一部は、カスタム作成して他のプロパティに適用できます。

| 検索フィールド | 検索プロパティの値 |
|---|---|
| MIME タイプ | 画像、ドキュメント、マルチメディア、アーカイブ、その他 |
| 最終変更 | 時間、日、週、月、年 |
| ファイルサイズ | 小、中、大 |
| 公開ステータス | 公開済みまたは非公開 |
| 承認ステータス | 承認または却下 |
| 向き | 水平方向、垂直方向、四角形 |
| スタイル | カラーまたは白黒 |
| ビデオの高さ | 最小値と最大値として指定。値はビデオレンディションのメタデータにのみ保存されます。 |
| ビデオの幅 | 最小値と最大値として指定。値はビデオレンディションのメタデータにのみ保存されます。 |
| ビデオ形式 | DVI、Flash、MPEG4、MPEG、OGG Theora、QuickTime、Windows Media。値は、ソースビデオのメタデータとレンディションに保存されます。 |
| ビデオコーデック | x264。値はビデオレンディションのメタデータにのみ保存されます。 |
| ビデオビットレート | 最小値と最大値として指定。値はビデオレンディションのメタデータにのみ保存されます。 |
| オーディオコーデック | Libvorbis、Lame MP3、AACエンコーディング。 値はビデオレンディションのメタデータにのみ保存されます。 |
| オーディオビットレート | 最小値と最大値として指定。値はビデオレンディションのメタデータにのみ保存されます。 |

## アセット検索結果の操作 {#aftersearch}

条件に一致する検索済みアセットが表示されたら、これらの検索結果に対して、次の典型的タスクやアクションを実行できます。

* メタデータプロパティなどの情報を表示する。
* 1 つ以上のアセットをダウンロードする。
* デスクトップアクションを使用してデスクトップアプリケーションでアセットを開く。
* スマートコレクションを作成する。

### 検索結果の並べ替え {#sort}

検索結果を並べ替えると、必要なアセットをすばやく見つけることができます。検索結果の並べ替えはリスト表示で機能し、**[!UICONTROL フィルター]**&#x200B;パネルで「**[!UICONTROL [ファイル](#searchui)]**」を選択した場合のみおこなえます。Experience Manager Assetsでは、サーバー側での並べ替えを使用して、フォルダー内のすべてのアセット（数量）や検索フォルダーの結果をすばやく並べ替えることができます。クエリ サーバー側の並べ替えにより、クライアント側の並べ替えよりも高速で正確な結果が得られます。

リスト表示では、任意のフォルダー内のアセットを並べ替える場合と同じように、検索結果を並べ替えることができます。並べ替えは、「名前」、「タイトル」、「ステータス」、「ディメンション」、「サイズ」、「評価」、「使用状況」、「作成日」、「変更日」、「発行日」、「ワークフロー」、「チェックアウト済み」の各列で行われます。

並べ替え機能の制限事項については、[制限事項](#limitations)を参照してください。

### アセットの詳細情報の確認 {#checkinfo}

検索したアセットの詳細情報を検索結果ページで確認できます。

アセットのすべてのメタデータを表示するには、アセットを選択し、ツールバーの「**[!UICONTROL プロパティ]**」をクリックします。

アセットへのコメントやアセットのバージョン履歴を確認するには、アセットをクリックして大きいサイズのプレビューを開きます。左側のパネルでタイムラインを開き、「**[!UICONTROL コメント]**」または「**[!UICONTROL バージョン]**」を選択します。また、コメントやバージョンなどのタイムラインアクティビティを時系列順に並べ替えることもできます。

![検索アセットのタイムラインエントリの並べ替え](assets/sort_timeline_search_results.gif)

*図：検索アセットのタイムラインエントリの並べ替え*

### 検索したアセットのダウンロード {#download}

フォルダーから通常のアセットをダウンロードする場合と同じように、検索したアセットとそのレンディションをダウンロードできます。検索結果から 1 つ以上のアセットを選択し、ツールバーの「**[!UICONTROL ダウンロード]**」をクリックします。

### メタデータプロパティの一括更新 {#metadataupdates}

複数アセットの共通のメタデータフィールドに対して一括更新をおこなうことができます。検索結果から、1 つ以上のアセットを選択します。ツールバーの「**[!UICONTROL プロパティ]**」をクリックし、必要に応じてメタデータを更新します。完了したら、「**[!UICONTROL 保存して閉じる]**」をクリックします。更新されたフィールド内の既存のメタデータが上書きされます。

For the assets that are available in a single folder or a collection, it is easier to [update the metadata in bulk](/help/assets/managing-multiple-assets.md) without using the search functionality. 複数のフォルダーをまたぐアセットや共通の条件に一致するアセットについては、検索を通じてメタデータを一括更新するほうが手軽です。

### スマートコレクション {#collections-1}

コレクションとは、様々な場所から得られるアセットを含むことができる順序付きアセットセットです。これが可能なのは、コレクションにはこれらのアセットへの参照のみが含まれるからです。コレクションには次の 2 つのタイプがあります。

* アセット、フォルダーおよび他のコレクションの静的な参照リスト
* 検索条件に基づいてコレクション内のアセットが決まる動的リスト（スマートコレクション）。

検索条件に基づいて、スマートコレクションを作成できます。**[!UICONTROL フィルター]**&#x200B;パネルで「**[!UICONTROL ファイル]**」を選択し、「**[!UICONTROL スマートコレクションを保存]**」をクリックします。詳しくは、[コレクションの管理](/help/assets/managing-collections-touch-ui.md)を参照してください。

## 予期しない検索結果や問題のトラブルシューティング {#troubleshoot-unexpected-search-results-and-issues}

| エラー、問題、症状 | 考えられる理由 | 問題の修正または理解 |
|---|---|---|
| メタデータがないアセットを検索する際に誤った結果が生じる | 必須のメタデータがないアセットを検索すると、Experience Managerで有効なメタデータを持つ一部のアセットが表示される場合があります。 結果は、インデックス付きのメタデータプロパティに基づいています。 | メタデータの更新後、アセットメタデータの正しい状態を反映するために、インデックスの再作成が必要です。 詳しくは、[必須メタデータ](metadata-schemas.md#define-mandatory-metadata)を参照してください。 |
| 検索結果が多すぎます | 部分一致検索パラメータ。 | 検索範囲の制限 [を検討します](#scope)。 スマートタグを使用すると、予想以上に多くの検索結果が得られる場合があります。 スマートタ [グを使用した検索動作を参照してくださ](#withsmarttags)い。 |
| 関連のない、または一部関連の検索結果 | スマートタグを使用した検索動作の変更。 | スマートタ [グ付け後の検索の変化を理解します](#withsmarttags)。 |
| アセットのオートコンプリートの提案なし | 新しくアップロードされたアセットのインデックスはまだ作成されていません。 Omnisearchバーで検索キーワードを入力した場合、メタデータは開始候補としてすぐには使用できません。 | Experience Manager Assetsは、タイムアウト期間（デフォルトで1時間）が経過するまで待ってから、バックグラウンドジョブを実行し、新しくアップロードまたは更新されたすべてのアセットのメタデータのインデックスを作成し、そのメタデータを提案のリストに追加します。 |
| 検索結果はありません | <ul><li>クエリに一致するアセットが存在しない。</li><li>検索クエリの前に空白を追加。</li><li>サポートされていないメタデータフィールドに、検索しているキーワードが含まれている。</li><li>アセットにオンタイムとオフタイムが設定されていて、アセットのオフタイム時に検索がおこなわれた。</li></ul> | <ul><li>別のキーワードを使用して検索します。 または、（スマート）タグ付けを使用して検索結果を改善します。</li><li>これは[既知の制限事項](#limitations)です。</li><li>すべてのメタデータフィールドが検索の際に考慮されるわけではありません。詳しくは、[検索範囲](#scope)を参照してください。</li><li>後で検索するか、必要なアセットのオン/オフのタイミングを変更します。</li></ul> |
| 検索フィルター/述語が使用できません | <ul><li>検索フィルターが設定されていない。</li><li>ログインできません。</li><li>（考えにくい）検索オプションは、使用している展開でカスタマイズされません。</li></ul> | <ul><li>検索のカスタマイズが使用可能かどうかを管理者に問い合わせて確認してください。</li><li>管理者に問い合わせて、お使いのアカウントにカスタマイズを使用する権限/権限があるかどうかを確認してください。</li><li>管理者に問い合わせて、使用しているExperience Manager Assetsデプロイメントで使用可能なカスタマイズを確認します。</li></ul> |
| 視覚的に類似した画像を検索する場合、期待される画像が見つからない | <ul><li>画像はExperience Managerでは使用できません。</li><li>画像のインデックスが作成されません。 通常、最近アップロードされた日時。</li><li>画像にスマートタグが付いていません。</li></ul> | <ul><li>Experience Manager追加 Assetsの画像。</li><li>リポジトリのインデックスを再作成するには、管理者に問い合わせてください。 また、適切なインデックスを使用していることを確認します。</li><li>管理者に問い合わせて、関連アセットのスマートタグを付けます。</li></ul> |
| 視覚的に類似した画像を検索する場合、無関係な画像が表示されます | ビジュアル検索の動作。 | Experience Managerには、可能な限り多くの関連するアセットが表示されます。 関連性の低い画像がある場合は、結果には追加されますが、検索のランキングは低くなります。検索結果を下にスクロールするにつれて、検索されたアセットの一致精度と関連性が低くなります。 |
| 検索結果を選択して操作する場合、検索されたすべてのアセットは操作されません。 | 「すべ [!UICONTROL て選択] 」オプションでは、カード表示の最初の100件の検索結果と、リスト表示の最初の200件の検索結果のみが選択されます。 |  |

>[!MORELIKETHIS]
>
>* [Experience Manager検索導入ガイド](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [複数値およびタグ検索述語の詳細設定](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/search-feature-video-use.html)
>* [スマート翻訳検索の設定](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

