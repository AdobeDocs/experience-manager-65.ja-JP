---
title: Search digital assets and images in [!DNL Adobe Experience Manager].
description: Learn how to find the required assets in [!DNL Adobe Experience Manager] by using Filters panel, and how to use the assets that show up in search.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 5599e0d4a3e52a4ad98b776b9178722c7ac47cbc
workflow-type: tm+mt
source-wordcount: '5968'
ht-degree: 51%

---


# Search assets in [!DNL Adobe Experience Manager] {#assets-search-in-aem}

[!DNL Adobe Experience Manager Assets] は、高いコンテンツ速度を達成するのに役立つ堅牢なアセット検出方法を提供します。 標準搭載の機能とカスタム方法を使用し、シームレスでインテリジェントな検索機能により、チームのタイム・トゥ・マーケティングの時間を短縮できます。 アセットの検索は、デジタルアセット管理システムの利用の中核を成します。用途は、クリエイティブ担当者によるさらなる利用、ビジネスユーザーやマーケティング担当者によるアセットの堅牢な管理、DAM 管理者による管理などです。Simple, advanced, and custom searches that you can perform via [!DNL Assets] user interface or other apps and surfaces help fulfill these use cases.

[!DNL Experience Manager Assets] は次の使用例をサポートしています。ここでは、これらの使用例での使用法、概念、設定、制限事項、トラブルシューティングについて説明します。

| アセットの検索 | 設定と管理 | 検索結果の操作 |
|---|---|---|
| [基本検索](#searchbasics) | [検索インデックス](#searchindex) | [結果の並べ替え](#sort) |
| [検索 UI について](#searchui) | [視覚的または類似性検索](#configvisualsearch) | [アセットのプロパティとメタデータの確認](#checkinfo) |
| [検索候補](#searchsuggestions) | [必須メタデータ](#mandatorymetadata) | [ダウンロード](#download) |
| [検索結果および動作について](#searchbehavior) | [検索ファセットの変更](#searchfacets) | [メタデータの一括更新](#metadataupdates) |
| [検索ランキングおよびブースト](#searchrank) | [テキスト抽出](#extracttextupload) | [スマートコレクション](#collections) |
| [詳細検索：検索のフィルタリングと範囲](#scope) | [カスタム述語](#custompredicates) | [予期しない検索結果と検索に関連する問題のトラブルシューティング](#troubleshoot-unexpected-search-results-and-issues) |
| [他のソリューションおよびアプリから検索](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[Experience Managerデスクトップアプリ](#desktopapp)</li><li>[Adobe Stock 画像](#adobestock)</li><li>[Dynamic Media アセット](#dynamicmedia)</li></ul> |  |  |
| [アセットセレクター](#assetpicker) |  |  |
| [制限事項](#limitations)と[ヒント](#tips) |  |  |
| [例を使った説明](#samples) |  |  |

Search for assets using the Omnisearch field at the top of the [!DNL Experience Manager] web interface. Go to **[!UICONTROL Assets]** > **[!UICONTROL Files]** in [!DNL Experience Manager], click search in top bar, enter search keyword, and press return. または、キーワードショートカット/（スラッシュ）を使用して、Omnisearchフィールドを開きます。 `Location:Assets` が事前に選択されており、DAM アセットの検索に制限されています。[!DNL Experience Manager] 開始が検索キーワードを入力する際に、サーチクエリを表示します。

[ **[!UICONTROL フィルター]** ]パネルを使用して、ファイルタイプ、ファイルサイズ、最終変更日、アセットのステータス、インサイトデータ、Adobe Stockライセンスなど、様々なオプション（述語）に基づいて検索結果をフィルタリングし、検索範囲を絞り込みます。 管理者は、フィルターパネルをカスタマイズし、検索ファセットを使用して検索予測を追加または削除できます。 [!UICONTROL フィルターパネルの] ファイルの種類 [!UICONTROL (File Type] )フィルターには、混在状態のチェックボックスがあります。 したがって、すべてのネストされた述語（またはフォーマット）を選択しない限り、第1レベルのチェックボックスは部分的にチェックされます。

[!DNL Experience Manager] 検索機能では、コレクションの検索とコレクション内のアセットの検索をサポートしています。詳しくは、[コレクションの検索](/help/assets/managing-collections-touch-ui.md)を参照してください。

## 検索インターフェイスについて {#searchui}

検索インターフェイスと使用可能なアクションについて理解します。

![Experience Managerアセットの検索結果インターフェイスを理解する](assets/aem_search_results.png)

*図：検索結果インターフェースを理解 [!DNL Experience Manager Assets] する。*

**A.** 検索をスマートコレクションとして保存します。 **B.検索結果を絞り込むための** フィルターまたは予測。 **C.** ファイル、フォルダ、またはその両方を表示する。 **D：**「フィルター」をクリックすると、左側のパネルが開くまたは閉じます。**E：** DAM が検索場所になります。**F.** Omnisearchフィールドにユーザが入力する検索キーワードを入力。 **G.** 、ロードされた検索結果を選択します。 **H.** 検索結果の合計中に表示された検索結果の数 **I.検索****** J.を閉じます。カードの表示とリストの表示を切り替えます。

### 動的検索ファセット {#dynamicfacets}

検索ファセット内で予想される検索結果の数は動的に更新されますが、この数を使用して、検索結果ページから目的のアセットをより迅速に見つけることができます。検索フィルターを適用する前であっても、予想されるアセット数は更新されます。フィルターに対して予想されるアセット数を確認すると、検索結果をすばやく効率的にナビゲートすることができます。For more info, see [Search assets in Experience Manager](search-assets.md).

![検索ファセットで検索結果をフィルタリングしない場合のアセット概数の表示](assets/asset_search_results_in_facets_filters.png)

*図：検索結果を検索ファセットでフィルタリングせずに、およそのアセット数を確認します。*

## 検索結果および動作について {#searchbehavior}

### 基本的な検索用語と検索結果 {#searchbasics}

オムニサーチフィールドからキーワード検索を実行できます。キーワード検索は、大文字と小文字が区別されません。また、（よく使用されるメタデータフィールド全体にわたる）フルテキスト検索です。 複数のキーワードを検索する場合、キーワード間のデフォルトの演算子は初期設定の検索 `AND` で、アセットにスマートタグが付けら `OR` れたときに使用されます。

結果は、最も近い一致を先頭に関連性の高い順に並べ替えられます。複数のキーワードがある場合は、メタデータに含まれるキーワードが多いアセットが、より関連性の高い結果になります。メタデータ内では、スマートタグとして表示されるキーワードは、他のメタデータフィールドに表示されるキーワードより高くランク付けされます。[!DNL Experience Manager] では、特定の検索用語に、より高い重みを付けることができます。Also, it is possible to [boost the rank](#searchrank) of a few targeted assets for specific search terms.

関連性の高いアセットをすばやく見つけるために、この機能豊富なインターフェイスには、フィルタリング、並べ替え、選択のメカニズムが用意されています。複数の条件に基づいて結果をフィルタリングし、検索されたアセットの数を様々なフィルター別に確認できます。または、オムニサーチフィールドのクエリを変更して検索を再実行することもできます。検索用語やフィルターを変更しても、その他のフィルターは依然として適用され、検索のコンテキストが保たれます。

結果が多数のアセットの場合、カード表示に最初の100が [!DNL Experience Manager] 表示され、リスト表示に200が表示されます。 ユーザがスクロールすると、読み込まれるアセットが増えます。 これは、パフォーマンスを向上させるためです。 表示されるアセット [数のデモビデオをご覧ください](https://www.youtube.com/watch?v=LcrGPDLDf4o)。

時には、予期しないアセットが検索結果に表示される場合があります。詳しくは、[予期しない検索結果](#troubleshoot-unexpected-search-results-and-issues)を参照してください。

[!DNL Experience Manager] では様々なファイル形式を検索でき、ビジネス要件に合わせて検索フィルターをカスタマイズできます。DAMリポジトリで使用できる検索オプションと、アカウントにどのような制限があるかについては、管理者に問い合わせてください。

### 強化されたスマートタグのある場合とない場合の結果 {#withsmarttags}

By default, [!DNL Experience Manager] search combines the search terms with an AND clause. 例えば、「woman running」というキーワードを検索するとします。 メタデータにwomanとrunningの両方のキーワードを含むアセットのみが、初期設定で検索結果に表示されます。 キーワードに特殊文字（ピリオド、アンダースコアまたはダッシュ）を使用する場合も、同じ動作が保持されます。 以下の検索クエリは同じ結果を返します。

* `woman running`
* `woman.running`
* `woman-running`

ただし、クエリは、メタデータを含まないアセット `woman -running``running` を返します。
Using smart tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using smart tags also appear in such a search query. つまり、検索結果は、以下を組み合わせたものになります。

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* いずれかのキーワードでスマートタグ付けされたアセット（スマートタグの動作）。

### 入力に応じて提示される検索候補 {#searchsuggestions}

When you start typing keywords, [!DNL Experience Manager] suggests the possible search keywords or phrases. サーチクエリは、既存のアセットのメタデータに基づいて作成されます。 [!DNL Experience Manager] では、検索に役立つすべてのメタデータフィールドのインデックスを作成します。検索候補を提示するために、以下のいくつかのメタデータフィールドの値が使用されます。検索候補の提示をおこなう場合は、次のフィールドに適切なキーワードを入力することを検討してください。

* アセットのタグ（`jcr:content/metadata/cq:tags` にマッピングされます）
* アセットのタイトル（`jcr:content/metadata/dc:title` にマッピングされます）
* アセットの説明（`jcr:content/metadata/dc:description` にマッピングされます）
* JCR リポジトリ内でのタイトル。この値はアセットのタイトルにマッピングされる可能性があります（`jcr:content/jcr:title` にマッピングされます）
* JCR リポジトリ内での説明。この値はアセットの説明にマッピングされる可能性があります（`jcr:content/jcr:description` にマッピングされます）

複数の検索キーワードに対するサーチクエリを受け取るには、1つのキーワードにサーチクエリを選択せずに、すべてのキーワードを入力し続けます。

![複数のキーワードを入力して、すべてに適した表示の提案を行います。](assets/search_suggestionsmanykeywords.gif)

*図：サーチクエリには複数の表示を入力し、それらすべてに適したキーワードを入力します。*

### 検索ランキングおよびブースト {#searchrank}

メタデータフィールド内のすべての検索用語に一致する検索結果が最初に表示され、スマートタグ内の検索用語のいずれかに一致する検索結果はその後に表示されます。上記の例の場合、検索結果が表示される順序はおおよそ次のようになります。

1. 各種メタデータフィールド内の「`woman running`」に一致するもの。
1. スマートタグ内の「`woman running`」に一致するもの。
1. スマートタグ内の「`woman`」または「`running`」に一致するもの。

特定のアセットに対するキーワードの有効性を高めることで、キーワードに基づいた検索を強化できます。つまり、特定のキーワードを昇格させた場合、それらのキーワードに基づいて検索すると、それらのキーワードの対象となる画像が検索結果の最上部に表示されます。

1. From the [!DNL Assets] user interface, open the properties page for the asset. Click **[!UICONTROL Advanced]** and click **[!UICONTROL Add]** under **[!UICONTROL Elevate for search keywords]**.
1. In the **[!UICONTROL Search Promote]** box, specify a keyword for which you want to boost the search for the image and then click **[!UICONTROL Add]**. 同じ方法で複数のキーワードを指定できます。
1. 「**[!UICONTROL 保存して閉じる]**」をクリックします。昇格したこのキーワードの対象となるアセットが、検索結果の上位に表示されます。

ターゲットを絞ったキーワードの検索結果で一部のアセットのランクを上げることで、この機能をうまく利用できます。以下の例（ビデオ）を参照してください。For detailed info, see [search in Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/search-and-discovery/search.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*検索結果のランク付けの方法とランクへの影響について*

## 詳細検索 {#scope}

[!DNL Experience Manager] には、検索したアセットに適用されるフィルターなど、目的のアセットをすばやく見つけるのに役立つ様々な方法が用意されています。一般的に使用されるいくつかの方法を以下で説明します。[動作例](#samples)もいくつか以下に示します。

**ファイルまたはフォルダーの検索**：検索結果には、ファイル、フォルダーまたはその両方が表示されます。**[!UICONTROL フィルター]**&#x200B;パネルから、適切なオプションを選択できます。詳しくは、[検索インターフェイス](#searchui)を参照してください。

**フォルダー内のアセットの検索**：検索対象を特定のフォルダーに限定できます。**[!UICONTROL フィルター]**&#x200B;パネルで、フォルダーのパスを追加します。一度に 1 つのフォルダーのみ選択できます。

![フィルターパネルにフォルダーパスを追加して検索結果を特定のフォルダーに限定](assets/search_folder_select.gif)

*図：フォルダーパネルにフィルターーパスを追加して、検索結果をフォルダーに制限する。*

### 類似の画像を検索 {#visualsearch}

ユーザーが選択した画像と視覚的に類似した画像を検索するには、画像のカード表示またはツールバーから「**[!UICONTROL 類似を検索]**」オプションをクリックします。[!DNL Experience Manager] は、ユーザーが選択した画像に類似した、DAM リポジトリのスマートタグ付き画像を表示します。[類似性検索の設定方法](#configvisualsearch)を参照してください。

![カード表示のオプションを使用して類似の画像を検索する](assets/search_find_similar.png)

*図：カード表示のオプションを使用して、類似した画像を検索します。*

### Adobe Stock 画像 {#adobestock}

From within the [!DNL Experience Manager] user interface, users can search [Adobe Stock assets](/help/assets/aem-assets-adobe-stock.md) and license the required assets. オムニサーチバーに「`Location: Adobe Stock`」を追加します。また、フィルターパネルを使用して、ライセンス取得済みまたはライセンス未取得のアセットをすべて検索したり、Adobe Stock ファイル番号を使用して特定のアセットを検索したりすることもできます。

### Dynamic Media アセット {#dmassets}

**[!UICONTROL フィルター]**&#x200B;パネルから **[!UICONTROL Dynamic Media]**／**[!UICONTROL セット]**&#x200B;を選択して、Dynamic Media 画像をフィルタリングすることができます。画像セット、カルーセル、混在メディアセット、スピンセットなどのアセットがフィルタリングされて表示されます。

### メタデータフィールドの特定の値を使用した検索 {#gqlsearch}

タイトル、説明、作成者など、特定のメタデータフィールドの正確な値に基づいてアセットを検索できます。 GQL 全文検索機能では、メタデータ値が検索クエリと完全に一致するアセットのみを取得できます。プロパティの名前（author や title など）と値は、大文字と小文字が区別されます。

| メタデータフィールド | ファセット値と使用法 |
| ----------------------------------------- | ------------------------------------- |
| タイトル | title:John |
| 作成者 | creator:John |
| 場所 | location:NA |
| 説明 | description:&quot;Sample Image&quot; |
| 作成ツール | creatortool:&quot;Adobe Photoshop CC 2020&quot; |
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

プロパティ `path`、、 `limit`、およびは、 `size`演算子を他のプロパティと組み合わせることはで `orderby``OR` きません。

ユーザー生成プロパティのキーワードは、プロパティエディターにおけるフィールドラベルからスペースを削除して小文字で表記したものです。

複雑なクエリの検索形式の例：

* 複数のファセットフィールドを持つアセットをすべて表示する（例：title=John Doe および creatortool=Adobe Photoshop）： `title:"John Doe" creatortool:Adobe*`
* ファセット値が 1 語でなく文になっているアセットをすべて表示する（例：title=Scott Reynolds）：`title:"Scott Reynolds"`
* 1 つのプロパティに複数の値が指定されているアセットを表示する（例：title=Scott Reynolds または John Doe）：`title:"Scott Reynolds" OR "John Doe"`
* プロパティ値が特定の文字列で始まるアセットを表示する（例：title=Scott Reynolds）：`title:Scott*`
* プロパティ値が特定の文字列で終わるアセットを表示する（例：title=Scott Reynolds）：`title:*Reynolds`
* プロパティ値に特定の文字列が含まれるアセットを表示する（例：title=Basel Meeting Room）：`title:*Meeting*`
* 特定の文字列が含まれ、特定のプロパティ値を持つアセットを表示する（例：title=John Doe のアセットで文字列「Adobe」を検索する）：`*Adobe* title:"John Doe"`

## Search assets from other [!DNL Experience Manager] offerings or interfaces {#beyondomnisearch}

[!DNL Adobe Experience Manager] では、DAMリポジトリを他の様々な [!DNL Experience Manager] ソリューションに接続して、デジタルアセットへの迅速なアクセスを提供し、クリエイティブワークフローを合理化します。 アセットの検出は、参照または検索で始まります。異なるサーフェスやソリューションでも、検索の動作はほとんど同じです。Some search methods change as the target audience, the use cases, and the user interface vary across the [!DNL Experience Manager] solutions. 個々のソリューションの具体的な方法については、以下のリンクを参照してください。ここでは、一般に当てはまるヒントや動作について説明しています。

### Adobe Asset Link パネルからのアセットの検索 {#aal}

Using Adobe Asset Link, the creative professionals can now access content stored in [!DNL Experience Manager Assets], without leaving the supported Adobe Creative Cloud apps. Creatives can seamlessly browse, search, check out, and check in assets using the in-app panel in the [!DNL Adobe Creative Cloud apps]: [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], and [!DNL Adobe InDesign]. また、Asset Link を使用すると、視覚的に類似した結果を検索できます。ビジュアル検索の表示結果は、Adobe Sensei の機械学習アルゴリズムを活用しており、見た目に類似した画像を見つけやすくなっています。詳しくは、[Adobe Asset Link を使用したアセットの検索と参照](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)を参照してください。

### Search assets in [!DNL Experience Manager] desktop app {#desktopapp}

Creative professionals use the desktop app to make the [!DNL Experience Manager Assets] easily searchable and available on their local desktop (Win or Mac). Creatives can easily reveal the desired assets in Mac Finder or Windows Explorer, opened in desktop applications, and changed locally - the changes are saved back to [!DNL Experience Manager] with a new version created in the repository. The application supports basic searches using one or more keywords, `*` and `?` wildcards, and `AND` operator. [デスクトップアプリケーションでのアセットの参照、検索、プレビュー](https://docs.adobe.com/content/help/ja-JP/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)を参照してください。

### Search assets in [!DNL Brand Portal] {#brandportal}

マーケティング担当者や事業部門のユーザーは、Brand Portal を使用して、承認済みのデジタルアセットを、広範な社内チーム、パートナーおよび販売店と効率的かつ安全に共有します。詳しくは、[Brand Portal でのアセットの検索](https://docs.adobe.com/content/help/ja-JP/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html)を参照してください。

### 画像の検索 [!DNL Adobe Stock] {#adobestock-1}

From within the [!DNL Experience Manager] user interface, users can search Adobe Stock assets and license the required assets. オムニサーチフィールドに「`Location: Adobe Stock`」を追加します。また、**[!UICONTROL フィルター]**&#x200B;パネルを使用して、ライセンス取得済みまたはライセンス未取得のアセットをすべて検索したり、Adobe Stock ファイル番号を使用して特定のアセットを検索したりすることもできます。See [manage Adobe Stock images in Experience Manager](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Dynamic Media アセットの検索 {#dynamicmedia}

**[!UICONTROL フィルター]**&#x200B;パネルから **[!UICONTROL Dynamic Media]**／**[!UICONTROL セット]**&#x200B;を選択して、Dynamic Media 画像をフィルタリングすることができます。画像セット、カルーセル、混在メディアセット、スピンセットなどのアセットがフィルタリングされて表示されます。Web ページの作成時に、作成者はコンテンツファインダー内でセットを検索できます。セットのフィルターは、ポップアップメニューで使用できます。

### Web ページ作成時のコンテンツファインダーでのアセットの検索 {#contentfinder}

作成者は、コンテンツファインダーを使用して関連アセットを DAM リポジトリで検索し、作成中の Web ページで使用できます。作成者は、接続されたアセット機能を使用して、リモート [!DNL Experience Manager] デプロイメントで使用可能なアセットを検索することもできます。 作成者は、これらのアセットをローカル [!DNL Experience Manager] デプロイメントのWebページで使用できます。 See [use remote assets](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### コレクションの検索 {#collections}

[!DNL Experience Manager] 検索機能では、コレクションの検索とコレクション内のアセットの検索をサポートしています。詳しくは、[コレクションの検索](/help/assets/managing-collections-touch-ui.md)を参照してください。

## アセットセレクター {#assetpicker}

>[!NOTE]
>
>Asset selector was called [asset picker](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) in prior versions of [!DNL Adobe Experience Manager].

アセットセレクターを使用すると、DAMアセットを特別な方法で参照、検索およびフィルターできます。 を使用して、 [!DNL Experience Manager] インスタンス内のアセットセレクターを起動でき `https://[aem-server]:[port]/aem/assetpicker.html`ます。 このURLは、アセットセレクターを参照モードで開きます。 サポートされているリクエストパラメーターをサフィックスとして使用します。例えば、 `mode` （1つまたは複数の選択範囲）や、 `viewmode` （画像、ビデオ、テキスト）、およびを使用 `assettype``mimetype`します。 これらのパラメーターは、特定の検索インスタンスに対してアセットセレクターのコンテキストを設定し、選択範囲全体を通してそのまま残ります。 この機能を使用して、選択したアセットのメタデータを取得することもできます。

アセットセレクターは、HTML5 `Window.postMessage` メッセージを使用して、選択したアセットのデータを受信者に送信します。ブラウズモードで、Omnisearch結果ページでのみ機能します。

次の要求パラメーターをURLに渡して、特定のコンテキストでアセットセレクターを起動します。

| 名前 | 値 | 例 | 目的 |
|---|---|---|---|
| resource suffix (B) | URL のリソースサフィックスとしてのフォルダーパス：[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | To launch the asset selector with a particular folder selected, for example with the folder `/content/dam/we-retail/en/activities` selected, the URL should be of the form: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | アセットセレクターの起動時に特定のフォルダーを選択する必要がある場合、そのフォルダーをリソースサフィックスとして渡します。 |
| mode | single、multiple | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | 複数モードでは、アセットセレクターを使用して、いくつかのアセットを同時に選択できます。 |
| dialog | true、false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | アセットセレクターを Granite ダイアログとして開くには、これらのパラメーターを使用します。このオプションは、Granite パスフィールドを使用してアセットセレクターを起動し、pickerSrc URL として設定する場合にのみ適用できます。 |
| root | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/アクティビティ) | アセットセレクターのルートフォルダーを指定するには、このオプションを使用します。この場合、アセットセレクターを使用すると、ルートフォルダーの下の子アセット（直接／間接）のみを選択できます。 |
| viewmode | 検索を |  | assettypeパラメータとmimetypeパラメータを使用して、検索モードでアセットセレクターを起動するには |
| assettype | images、documents、multimedia、archives | <ul><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=images](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=multimedia](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=archives](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;assettype=archives)</li></ul> | 渡された値に基づいてアセットタイプをフィルタリングするには、このオプションを使用します。 |
| mimetype | アセットの MIME タイプ（`/jcr:content/metadata/dc:format`）（ワイルドカードもサポートされています） | <ul><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=image/png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?viewmode=search&amp;mimetype=*presentation&amp;mimetype=*png)</li></ul> | MIME タイプに基づいてアセットをフィルタリングするために使用します |

アセットセレクターインターフェイスにアクセスするには、`https://[aem_server]:[port]/aem/assetpicker` に移動します。目的のフォルダーに移動して、1 つまたは複数のアセットを選択します。または、オムニサーチボックスから目的のアセットを検索し、必要に応じてフィルターを適用して選択します。

![アセットセレクターでアセットを参照して選択します](assets/assetpicker.png)

*図：アセットセレクターでアセットを参照し、選択します。*

## 制限事項 {#limitations}

The search capability in [!DNL Experience Manager Assets] has the following limitations:

* 検索クエリの先頭にスペースを入れないでください。スペースを入れると、検索が機能しません。
* [!DNL Experience Manager] は、検索結果からアセットのプロパティを選択し、検索をキャンセルした後も、検索語を引き続き表示する場合があります。 <!-- (CQ-4273540) -->
* フォルダーまたはファイルとフォルダーを検索する場合、どのパラメーターでも検索結果を並べ替えることはできません。
* If you press return without typing anything in Omnisearch bar, [!DNL Experience Manager] returns a list of only files and not folders. If you search specifically for folders without using a keyword, [!DNL Experience Manager] does not return any results.
* 検索ページの右上隅にある「すべて **[!UICONTROL 選択]** 」オプションを使用して、検索したアセットを選択します。 [!DNL Experience Manager] 最初は、100アセットをカード表示で、200アセットをリスト表示で表示します。 検索結果をスクロールすると、読み込まれるアセットが増えます。 読み込まれたアセットより多くのアセットを選択できます。 選択したアセットの数が、検索結果ページの右上隅に表示されます。 選択範囲に対して操作を実行できます。例えば、選択したアセットのダウンロード、選択したアセットのメタデータプロパティの一括更新、選択したアセットのコレクションへの追加などが可能です。 表示されている数よりも多くのアセットが選択されている場合は、選択したすべてのアセットにアクションが適用されるか、ダイアログにアセットが適用されている数が表示されます。 読み込まれなかったアセットにアクションを適用するには、すべてのアセットが明示的に選択されていることを確認します。

ビジュアル検索または類似検索には、次の制限事項があります。

* ビジュアル検索は、より大きなリポジトリで最も有効に機能します。良好な結果を得るために最低限必要な画像数はありませんが、画像の数が少ないと、一致の精度が大きなリポジトリの場合ほど良くない可能性があります。
* You cannot change the model or train [!DNL Experience Manager] to find similar images. 例えば、一部のアセットにスマートタグを追加または削除しても、モデルは変更されません。それらのアセットは、視覚的に類似した検索結果から除外されます。

次のシナリオでは、検索機能のパフォーマンスに制限がある場合があります。

* カード表示の読み込み時間は、検索結果を表示するリスト表示と比較して高速です。

## 検索のヒント {#tips}

* アセットのレビューステータスを監視する場合は、該当するオプションを使用して、承認されているアセットまたは承認待ちのアセットを検索します。
* 様々な Creative アプリから取得した使用状況の統計に基づいて、サポートされるアセットを検索するには、インサイトの述語を使用します。使用状況データが、使用状況スコア、インプレッション数、クリック数およびメディアチャネルでグループ化され、アセットがカテゴリ別に表示されます。
* 「 **[!UICONTROL Select All]** 」チェックボックスを使用して、検索したアセットを選択します。 [!DNL Experience Manager] 最初は、100アセットをカード表示で、200アセットをリスト表示で表示します。 検索結果をスクロールすると、読み込まれるアセットが増えます。 読み込まれたアセットより多くのアセットを選択できます。 選択したアセットの数が、検索結果ページの右上隅に表示されます。 選択範囲に対して操作を実行できます。例えば、選択したアセットのダウンロード、選択したアセットのメタデータプロパティの一括更新、選択したアセットのコレクションへの追加などが可能です。 表示されている数よりも多くのアセットが選択されている場合は、選択したすべてのアセットにアクションが適用されるか、ダイアログにアセットが適用されている数が表示されます。 読み込まれなかったアセットにアクションを適用するには、すべてのアセットが明示的に選択されていることを確認します。
* 必須メタデータを含んでいないアセットを検索する場合は、[必須メタデータ](#mandatorymetadata)を参照してください。
* 検索では、すべてのメタデータフィールドが使用されます。12 の検索などの一般的な検索では通常、多数の結果が返されます。より良い結果を得るには、（一重引用符ではなく）二重引用符を使用するか、特殊文字のない単語に番号が続いている（例：*shoe12* など）ようにします。
* 全文検索では、 — や^などの演算子を使用できます。 これらの文字を文字列リテラルとして検索するには、検索式を二重引用符で囲みます。例えば、「Notebook - Beauty」ではなく、「&quot;Notebook - Beauty&quot;」と指定します。
* 検索結果が多すぎる場合は、[検索範囲](#scope)を制限して、目的のアセットを絞り込みます。これは、特定のファイルタイプ、特定の場所、特定のメタデータなど、目的のアセットを検索する良い方法がある程度わかっている場合に最も効果的です。

* **タグ付け**:タグを使用すると、閲覧や検索が効率的に行えるアセットを分類できます。 タグ付けは、適切な分類を他のユーザーやワークフローに伝播するうえで役に立ちます。[!DNL Experience Manager] では、使用状況データやトレーニングでアセットのタグ付けを絶えず改善する、Adobe Sensei の AI サービスを活用して、アセットに自動的にタグを付ける手段を提供しています。この機能がアカウントで有効な場合は、アセットを検索する際にスマートタグが考慮されます。これは組み込みの検索機能と連携して機能します。[検索動作](#searchbehavior)を参照してください。検索結果の表示順序を最適化するには、選択した一部のアセットの[検索ランキングを上げる](#searchrank)ことができます。

* **インデックス作成**：インデックスが作成されたメタデータおよびアセットのみが検索結果に返されます。検索範囲とパフォーマンスを向上させるには、適切なインデックス作成をおこない、ベストプラクティスに従ってください。詳しくは、[インデックス作成](#searchindex)を参照してください。

* 検索結果から特定のアセットを除外するには、Luceneインデックスで `excludedPath` プロパティを使用します。

## 検索の例 {#samples}

ユーザーが指定したとおりの語句を含んだアセットを検索するには、キーワードを二重引用符で囲みます。

![引用符がある場合とない場合の検索動作](assets/search_with_quotes.gif)

*図：検索動作（引用符の有無）*

**アスタリスクワイルドカードを使用した検索**：検索の範囲を広げるには、検索語の前後にアスタリスクを使用して任意の数の文字に一致するようにします。例えば、アスタリスクを付けずに「run」を検索しても、（メタデータ内も含め）検索語のバリエーションを含んだアセットは返されません。アスタリスクは任意の数の文字に置き換わります。例：

* `run`：キーワード「run」を含んだアセットを返します。
* `run*`：「running」、「run」、「runaway」などを含んだアセットを返します。
* `*run`：「outrun」、「rerun」などを含んだアセットを返します。
* `*run*`：可能なあらゆる組み合わせを含んだアセットを返します。

![アセット検索でのアスタリスクワイルドカードの使用例](assets/search_with_asterisk_run.gif)

*図：例を使用して、アセット検索でアスタリスクワイルドカードを使用する例を示します。*

**疑問符ワイルドカードを使用した検索**：検索の範囲を広げるには、1 つ以上の「?」文字を使用して正確な数の文字に一致するようにします。例えば、次の例では、

* `run???` クエリはどのアセットとも一致しません。

* `run????` クエリは、`run` の後に 4 文字がある単語 `running` と一致します。

* `??run` クエリは、`run` の前に 2 文字がある単語 `rerun` と一致します。

![アセット検索での疑問符ワイルドカードの使用例](assets/search_with_questionmark_run.gif)

*図：例を使用して、アセット検索で疑問符ワイルドカードを使用する例を示します。*

**キーワードの除外**：ダッシュを使用すると、キーワードを含まないアセットを検索できます。例えば、`running -shoe` クエリでは、`running` を含み `shoe` を含まないアセットを返します。同様に、`camp -night` クエリでは `camp` を含み `night` を含まないアセットを返します。The query `camp-night` returns assets that contain both `camp` and `night`.

![ダッシュを使用して、除外されたキーワードを含まないアセットを検索する](assets/search_dash_exclude_keyword.gif)

*図：ダッシュを使用して、除外されたキーワードを含まないアセットを検索します。*

## 検索機能に関連する設定および管理タスク {#configadmin}

### 検索インデックスの設定 {#searchindex}

アセットの検出は、メタデータを含むDAMコンテンツのインデックス作成に依存しています。 迅速で正確なアセット検出は、最適化されたインデックス作成と適切な設定に依存しています。 「 [検索インデックス](/help/assets/performance-tuning-guidelines.md#search-indexes)」、「 [oakクエリとインデックス作成](/help/sites-deploying/queries-and-indexing.md)」、「 [ベストプラクティス」を参照してください](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

検索結果から特定のアセットを除外するには、Luceneインデックスで `excludedPath` プロパティを使用します。

### 視覚的または類似性検索 {#configvisualsearch}

ビジュアル検索ではスマートタグが使用され、6.5.2.0 [!DNL Experience Manager] 以降が必要です。 スマートタグ機能を設定したら、次の手順に従います。

1. CRXDEの [!DNL Experience Manager]`/oak:index/lucene` ノードで、次のプロパティと値を追加し、変更を保存します。

   * `costPerEntry` 値を持つタイプ `Double` のプロパティ `10`。
   * `costPerExecution` 値を持つタイプ `Double` のプロパティ `2`。
   * `refresh` 値を持つタイプ `Boolean` のプロパティ `true`。

   この設定では、適切なインデックスからの検索が可能です。

1. Luceneインデックスを作成するには、CRXDEで、タイプの名前 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`のノード `imageFeatures` を作成 `nt-unstructured`します。 ノード `imageFeatures` で、

   * 値を持つタイプの追加 `name` プロパティ `String` で `jcr:content/metadata/imageFeatures/haystack0`す。
   * の値を持つタイプの追加 `nodeScopeIndex` プロパティで `Boolean``true`す。
   * の値を持つタイプの追加 `propertyIndex` プロパティで `Boolean``true`す。
   * 値を持つタイプの追加 `useInSimilarity` プロパティ `Boolean` で `true`す。

   変更内容を保存します。

1. の値 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` を使用して、タイプの `similarityTags` プロパティ `Boolean` にアクセスして追加し `true`ます。
1. リポジトリ内のアセットにスマートタグを適用し [!DNL Experience Manager] ます。 スマートタグの設定 [方法を参照してください](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)。
1. CRXDEの `/oak-index/damAssetLucene` nodeで、 `reindex` プロパティをに設定し `true`ます。 変更内容を保存します。
1. （オプション）検索フォームをカスタマイズした場合は、に `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` ノードをコピーし `/conf/global/settings/dam/search/facets/assets/jcr:content/items`ます。 変更内容を保存します。

関連情報については、「Experience Managerのスマートタグ [について](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-feature-video-use.html) 」および「スマートタグの管理 [方法](/help/assets/enhanced-smart-tags.md)」を参照してください。

>[!CAUTION]
>
>Luceneのインデックス作成が終了した場合 [!DNL Adobe Experience Manager]は、スマートタグに基づく検索が期待どおりに動作しません。

### 必須メタデータ {#mandatorymetadata}

ビジネスユーザー、管理者またはDAMライブラリは、いくつかのメタデータを、ビジネスプロセスが機能するための必須のメタデータとして定義できます。 既存のアセットや一括移行されたアセットなど、様々な理由で、一部のアセットにこのメタデータがない場合があります。 メタデータがないか無効なアセットは、インデックス付きメタデータプロパティに基づいて検出され、報告されます。 設定するには、 [必須メタデータを参照してください](/help/assets/metadata-schemas.md#define-mandatory-metadata)。

### 検索ファセットの変更 {#searchfacets}

検出の速度を向上させるために、 [!DNL Experience Manager Assets] オファーは検索結果をフィルタリングできるファセットを検索します。 フィルターパネルには、デフォルトでいくつかの標準ファセットが含まれています。 管理者は、フィルターパネルをカスタマイズして、組み込みの述部を使用してデフォルトのファセットを変更できます。 [!DNL Experience Manager] には、組み込みの述語の適切なコレクションと、ファセットをカスタマイズするエディターが用意されています。 「 [検索ファセット](/help/assets/search-facets.md)」を参照してください。

### アセットのアップロード時にテキストを抽出 {#extracttextupload}

PSDファイルやPDFファイルなど [!DNL Experience Manager] のアセットをアップロードする際に、アセットからテキストを抽出するように設定できます。 [!DNL Experience Manager] は、抽出されたテキストのインデックスを作成し、抽出されたテキストに基づいてこれらのアセットを検索しやすくします。 See [upload assets](/help/assets/managing-assets-touch-ui.md#uploading-assets).

テキスト抽出がデプロイメントにとってリソースを大量に消費する大きすぎる場合は、テキスト抽出を [無効にすることを検討](https://helpx.adobe.com/experience-manager/kb/Disable-binary-text-extraction-to-optimize-Lucene-indexing-AEM.html)します。

### 検索結果をフィルターするカスタム述語 {#custompredicates}

述部は、ファセットの作成に使用されます。 管理者は、事前設定された述部を使用して、フィルターパネルの検索ファセットをカスタマイズできます。 これらの述部は、オーバーレイを使用してカスタマイズできます。 「カスタム述部の [作成](/help/assets/searchx.md)」を参照してください。

デジタルアセットは、次のプロパティのうち1つ以上に基づいて検索できます。 これらのプロパティの一部に適用されるフィルターは、デフォルトで使用できます。また、その他のフィルターの一部は、カスタム作成して他のプロパティに適用できます。

| 検索フィールド | 検索プロパティの値 |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
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

Experience Managerで検索したアセットを使用して、次の操作を実行できます。

* メタデータプロパティなどの情報を表示する。
* 1 つ以上のアセットをダウンロードする。
* デスクトップアクションを使用してデスクトップアプリケーションでアセットを開く。
* スマートコレクションを作成する。

### 検索結果の並べ替え {#sort}

検索結果を並べ替えて、必要なアセットをより迅速に見つけ出す。 You can sort the search results in list view and only when you select **[[!UICONTROL Files]](#searchui)** from the **[!UICONTROL Filters]** panel. [!DNL Experience Manager Assets] では、サーバー側の並べ替え機能を使用して、フォルダー内のすべてのアセット（どれだけ多くても対応可能）や検索クエリの結果をすばやく並べ替えます。サーバー側の並べ替えにより、クライアント側の並べ替えよりも高速で正確な結果が得られます。

リスト表示では、任意のフォルダー内のアセットを並べ替える場合と同じように、検索結果を並べ替えることができます。並べ替えは、「名前」、「タイトル」、「ステータス」、「寸法」、「サイズ」、「評価」、「使用状況」、「作成日」、「変更日」、「公開日」、「ワークフロー」、「チェックアウト済み」の各列でおこなわれます。

並べ替え機能の制限事項については、[制限事項](#limitations)を参照してください。

### アセットの詳細情報の確認 {#checkinfo}

検索したアセットの詳細情報を検索結果ページで確認できます。

アセットのすべてのメタデータを表示するには、アセットを選択し、ツールバーの「**[!UICONTROL プロパティ]**」をクリックします。

アセットへのコメントやアセットのバージョン履歴を確認するには、アセットをクリックして大きいサイズのプレビューを開きます。左側のパネルでタイムラインを開き、「**[!UICONTROL コメント]**」または「**[!UICONTROL バージョン]**」を選択します。また、コメントやバージョンなどのタイムラインアクティビティを時系列順に並べ替えることもできます。

![検索アセットのタイムラインエントリの並べ替え](assets/sort_timeline_search_results.gif)

*図：検索アセットのタイムラインエントリを並べ替えます。*

### 検索したアセットのダウンロード {#download}

フォルダーから通常のアセットをダウンロードする場合と同じように、検索したアセットとそのレンディションをダウンロードできます。検索結果から 1 つ以上のアセットを選択し、ツールバーの「**[!UICONTROL ダウンロード]**」をクリックします。

### メタデータプロパティの一括更新 {#metadataupdates}

複数アセットの共通のメタデータフィールドに対して一括更新をおこなうことができます。検索結果から、1 つ以上のアセットを選択します。ツールバーの「**[!UICONTROL プロパティ]**」をクリックし、必要に応じてメタデータを更新します。完了したら、「**[!UICONTROL 保存して閉じる]**」をクリックします。更新されたフィールド内の既存のメタデータが上書きされます。

For the assets that are available in a single folder or a collection, it is easier to [update the metadata in bulk](/help/assets/metadata.md) without using the search functionality. 複数のフォルダーをまたぐアセットや共通の条件に一致するアセットについては、検索を通じてメタデータを一括更新するほうが手軽です。

### スマートコレクション {#smart-collections}

コレクションとは、様々な場所から得られるアセットを含むことができる順序付きアセットセットです。これが可能なのは、コレクションにはこれらのアセットへの参照のみが含まれるからです。コレクションには次の 2 つのタイプがあります。

* アセット、フォルダーおよび他のコレクションの静的な参照リスト
* 検索条件に基づいてコレクション内のアセットが決まる動的リスト（スマートコレクション）。

検索条件に基づいて、スマートコレクションを作成できます。**[!UICONTROL フィルター]**&#x200B;パネルで「**[!UICONTROL ファイル]**」を選択し、「**[!UICONTROL スマートコレクションを保存]**」をクリックします。詳しくは、[コレクションの管理](/help/assets/managing-collections-touch-ui.md)を参照してください。

## 予期しない検索結果や問題のトラブルシューティング {#troubleshoot-unexpected-search-results-and-issues}

| エラー、問題、症状 | 考えられる理由 | 問題の修正または理解 |
|---|---|---|
| メタデータが見つからないアセットを検索する場合に、誤った結果が返される。 | When searching for assets that are missing the mandatory metadata, [!DNL Experience Manager] may display some assets that have valid metadata. 結果は、インデックス付きメタデータプロパティに基づきます。 | メタデータが更新された後、アセットメタデータの正しい状態を反映するために、再インデックス化が必要です。 詳しくは、[必須メタデータ](metadata-schemas.md#define-mandatory-metadata)を参照してください。 |
| 検索結果が多すぎます。 | 部分一致検索パラメータ。 | 検索の [範囲を制限することを検討](#scope)。 スマートタグを使用すると、予想以上に多くの検索結果が得られる場合があります。 「スマートタグを使用した [検索動作](#withsmarttags)」を参照してください。 |
| 検索結果が無関係か、一部関連している。 | スマートタグによって検索動作が変わります。 | スマートタグ付け後の検索 [の変更について理解し](#withsmarttags)ます。 |
| アセットに対するオートコンプリートの提案はありません。 | 新しくアップロードしたアセットのインデックスはまだ作成されていません。 開始がOmnisearchバーで検索キーワードを入力した場合、そのメタデータは提案としてすぐには使用できません。 | [!DNL Assets] では、タイムアウト期間（デフォルトは 1 時間）が経過してから、新しくアップロードまたは更新されたすべてのアセットのメタデータにインデックスを付けるバックグラウンドジョブを実行し、その後でメタデータを候補のリストに追加します。 |
| 検索結果はありません. | <ul><li>クエリに一致するアセットが存在しません。 </li><li> 検索クエリの前に空白が追加されました。 </li><li> サポートされていないメタデータフィールドに、検索したキーワードが含まれています。</li><li> アセットのオフタイム中に行われた検索。 </li></ul> | <ul><li>別のキーワードを使用した検索。 または、スマートタグ付け検索または類似性検索を使用して、検索結果を改善します。 </li><li>[既知の制限](#limitations)。</li><li>すべてのメタデータフィールドが検索対象と見なされません。 詳しくは、[検索範囲](#scope)を参照してください。</li><li>後で検索するか、必要なアセットのオンタイムとオフタイムを変更します。</li></ul> |
| 検索フィルターまたは述語が使用できません。 | <ul><li>検索フィルターが設定されていない。</li><li>ログインに使用できません。</li><li>（おそらく）検索オプションは、使用しているデプロイメントに合わせてカスタマイズされません。</li></ul> | <ul><li>検索のカスタマイズが使用可能かどうかを管理者に問い合わせて確認してください。</li><li>管理者に問い合わせて、お使いのアカウントに、カスタマイズを使用する権限または権限があるかどうかを確認してください。</li><li>管理者に問い合わせて、使用している [!DNL Assets] 展開で使用可能なカスタマイズを確認してください。</li></ul> |
| 視覚的に類似した画像を検索する場合、期待された画像が見つかりません。 | <ul><li>では画像を使用できません [!DNL Experience Manager]。</li><li>画像のインデックスが作成されていません。 通常、最近アップロードされた日時。</li><li>画像にスマートタグは付きません。</li></ul> | <ul><li>追加画像を [!DNL Assets]。</li><li>リポジトリのインデックスを再作成するには、管理者に問い合わせてください。 また、適切なインデックスを使用していることを確認してください。</li><li>管理者に問い合わせて、関連アセットのスマートタグを付けます。</li></ul> |
| 視覚的に類似した画像を検索する場合、無関係な画像が表示されます。 | 視覚検索の動作。 | [!DNL Experience Manager] では、関連する可能性のあるアセットをできるだけ多く表示します。関連性の低い画像がある場合は、結果には追加されますが、検索のランキングは低くなります。検索結果を下にスクロールするにつれて、検索されたアセットの一致精度と関連性が低くなります。 |
| 検索結果を選択して操作する場合、検索されたすべてのアセットは操作されません。 | 「す [!UICONTROL べて選択] 」オプションを選択した場合は、カード表示で最初に100件の検索結果が選択され、リスト表示で最初に200件の検索結果が選択されます。 |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 検索導入ガイド](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [検索結果を高めるための詳細設定](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [スマート翻訳検索の設定](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

