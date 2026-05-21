---
title: Dynamic Media の一般設定
description: Dynamic Media で一般設定を管理する方法を説明します。 ここで公開先サーバー名と公開元サーバー名を設定し、画像の上書きオプションを設定できます。 また、画像のアンシャープマスク用のデフォルトのアップロードオプションや、PostScript、Adobe Photoshop、PDF、Adobe Illustrator の各ファイルを処理する方法に関するアップロードオプションも用意されています。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: 55cc7c57-87a0-4bfb-b226-36d01d36849a
solution: Experience Manager, Experience Manager Assets
autotag-review: '2026-05-18T18:45:43.326Z'
TQID: 'https://experienceleague.adobe.com/MXCLWQOBsCl3DPKVPn-WjnPeu-NGnQtUn6EYueH7OfE'
product_v2: id: e14eb250-3c22-4a07-9061-a78112b2b826id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2: id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: d378ca77-2da1-4f39-ad92-1917fe974a38
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 2537
ht-degree: 85%

---

# Dynamic Media の一般設定

**[!UICONTROL Dynamic Media 一般設定]** は、次の場合にのみ使用できます。

* Scene7 モードで Dynamic Media を実行している。 詳しくは、 [Scene7 モードの Dynamic Media の有効化](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode)を参照してください。
* Adobe Experience Manager 6.5.11 以降に、*既存の* **[!UICONTROL Dynamic Media 設定]**（**[!UICONTROL クラウドサービス]**&#x200B;内）がある。 [Cloud Services での Dynamic Media 設定の作成](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)を参照してください。
* 自身が管理者権限を持つ Experience Manager システム管理者である。

Dynamic Media の一般設定は、経験豊富な web サイト開発者やプログラマーが使用することを目的としています。 Adobe Dynamic Mediaでは、これらの公開設定を変更するユーザーに、Adobe Experience Manager 上の Dynamic Media と基本的な画像技術に精通することをお勧めします。

アカウントの作成時に、会社に割り当てられているサーバーが Adobe Dynamic Media によって自動的に提供されます。 これらのサーバーは、web サイトとアプリケーションの URL 文字列を生成するのに使用されます。 これらの URL 呼び出しは、アカウントに固有です。

Dynamic Media の公開設定ページでは、Adobe Dynamic Media サーバーから web サイトやアプリケーションにアセットを配信する方法を決定するデフォルト設定を指定します。 設定が指定されていない場合、Adobe Dynamic Media サーバーは、Dynamic Media 公開設定ページで設定されたデフォルト設定に従ってアセットを配信します。

その他のオプションの設定タスクについては、[オプション - Dynamic Media のセットアップと設定 - Scene7 モードの設定](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)も参照してください。

>[!NOTE]
>
>Adobe Experience Manager で Dynamic Media Classic から Dynamic Media にアップグレードしますか？ Dynamic Media の一般設定ページおよび[公開設定](/help/assets/dm-publish-settings.md)ページには、Dynamic Media Classic アカウントから取得した値が事前に入力されています。 例外は、一般設定ページの&#x200B;**[!UICONTROL デフォルトのアップロードオプション]**&#x200B;領域にリストされているすべての値です。 これらの値はすでに Experience Manager に存在します。 そのため、Experience Manager ユーザーインターフェイスを介して 5 つのタブのいずれかで&#x200B;**[!UICONTROL デフォルトのアップロードオプション]**&#x200B;で行った変更は、Dynamic Media Classic ではなく Dynamic Media に反映されます。 一般設定ページと[公開設定](/help/assets/dm-publish-settings.md)ページの他のすべての設定と値は、Experience Manager の Dynamic Media Classic と Dynamic Media の間で維持されます。

**Dynamic Media の一般設定を指定するには：**

1. Experience Manager 作成者モードで、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。
1. 左側のパネルで「ツール」アイコンを選択し、**[!UICONTROL アセット]**／**[!UICONTROL Dynamic Media 一般設定]**&#x200B;に移動してください。
1. サーバーページで、**[!UICONTROL 公開先サーバー名]**&#x200B;と&#x200B;**[!UICONTROL 公開元サーバー名]**&#x200B;を設定し、5 つのタブを使用して、画像編集のデフォルトのアップロードオプション、および Postscript ファイル、Photoshop ファイル、PDF ファイル、Illustrator ファイルのデフォルトのアップロードオプションを構成します。

   * [サーバー](#server-general-setting)
   * [アプリケーションへのアップロード](#upload-to-application)
   * 「[画像編集](#image-editing-tab)」タブ
   * 「[PostScript](#postscript-tab)」タブ
   * 「[Photoshop](#photoshop-tab)」タブ
   * 「[PDF](#pdf-tab)」タブ
   * 「[Illustrator](#illustrator-tab)」タブ

   ![Dynamic Mediaの一般設定ページ](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media の一般設定ページ（**[!UICONTROL 画像編集]**タブが選択済み）*<br><br>

1. 作業が完了したら、ページの右上隅付近にある「**[!UICONTROL 保存]**」を選択してください。

## サーバー {#server-general-setting}

アカウントの作成時に、会社に割り当てられているサーバーが Adobe Dynamic Media によって自動的に提供されます。 これらのサーバーは、web サイトとアプリケーションの URL 文字列を生成するのに使用されます。 これらの URL 呼び出しは、アカウントに固有です。

| オプション | 説明 |
| --- | --- |
| **[!UICONTROL 公開先サーバー名]** | 必須。<br>名前はパスに`https://`を使用する必要があります。<br>このサーバーは、アカウントに固有のすべてのシステム生成 URL 呼び出しで使用されるライブ CDN（コンテンツ配信ネットワーク）サーバーです。 アドビテクニカルサポートから指示されない限り、このサーバー名は変更しないでください。 |
| **[!UICONTROL 公開元サーバー名]** | 必須。<br>このサーバーは品質保証テストにのみ使用されます。 Adobe テクニカルサポートから指示がない限り、このサーバー名を変更しないでください。 |

## アプリケーションへのアップロード {#upload-to-application}

* **[!UICONTROL 画像を上書き]**

  Adobe Dynamic Media は、2 つのファイルが同じ名前を持つことを許可しません。 各項目の Adobe Dynamic Media ID（画像名からファイル名拡張子を取り除いた部分）は一意である必要があります。 このルールのため、**[!UICONTROL アプリケーションにアップロード]**&#x200B;は上書き機能があります。 このオプションの正確な効果は、選択した「画像を上書き」オプションによって異なります。 これらのオプションは、置き換えるアセットのアップロード方法、つまり元のアセットを置き換えるか、重複させるかを指定します。 重複する画像の名前は `-1` に変更されます。 例：`chair.tif` の名前は `chair-1.tif` に変更されます。 これらのオプションは、元の画像とは別のフォルダーにアップロードされる画像や、元の画像と異なるファイル名拡張子（JPG、TIF、PNG など）を持つアセットに影響を与えます。

  >[!NOTE]
  >
  >Experience Manager との一貫性を維持するには、「画像を上書き」オプションの&#x200B;**[!UICONTROL 現在のフォルダーにあるベース名と拡張子が同じファイルを上書き]**&#x200B;を選択してください。

  | 「画像を上書き」オプション | 説明 |
  | --- | --- |
  | **[!UICONTROL 現在のフォルダーにあるベース名と拡張子が同じファイルを上書き]** | 新規 Dynamic Media アカウントのみで&#x200B;*デフォルト*。<br>このオプションは最も厳格な置換ルールです。 置き換え画像を元の画像と同じフォルダーにアップロードし、置き換え画像と元の画像のファイル名拡張子が同じになっている必要があります。 これらの要件が満たされない場合は、重複する画像が作成されます。<br>*Experience Manager との一貫性を維持するには、このオプションを選択してください*。 |
  | **[!UICONTROL 現在のフォルダーにあるベース名が同じファイルを拡張子に関わらず上書き]** | 置換画像を元の画像と同じフォルダーにアップロードする必要がありますが、ファイル名の拡張子は元の画像と異なることができます。 例えば、chair.tif は chair.jpg を置き換えます。 |
  | **[!UICONTROL 任意のフォルダーにあるベース名と拡張子が同じファイルを上書き]** | 置換画像のファイル名拡張子が元の画像と同じである必要があります（例えば、chair.jpg は chair.tif ではなく chair.jpg を置き換える必要があります）。 ただし、置換画像を、元の画像と別のフォルダーにアップロードできます。 更新された画像は新しいフォルダーにあり、元の場所のファイルはなくなります。 |
  | **[!UICONTROL 任意のフォルダーでベース名が同じファイルを拡張子に関わらず上書き]** | このオプションは、最も包括的な置換ルールです。 置換画像を、元の画像と別のフォルダーにアップロードでき、ファイル名拡張子が異なるファイルをアップロードして、元のファイルと置換することができます。 元のファイルが別のフォルダーにある場合、置換画像は、アップロード先の新しいフォルダーに存在します。 |

* **[!UICONTROL 切り抜きを保持]**

  既存の手動切り抜き定義の保存を制御します。

  Dynamic Media ビューアリファレンスガイドの [UploadPostJob ](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html?lang=ja) および [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html?lang=ja) の `preserveCrop` も参照してください。

## デフォルトのアップロードオプション {#default-upload-options}

### 「画像編集」タブ {#image-editing-tab}

このフィルターを使用すると、ダウンサンプリングされた最終的な画像に対するシャープフィルター効果を微調整できます。 効果の強さ、効果の半径（ピクセル単位）、無視されるコントラストのしきい値を制御するのに役立ちます。

アンシャープマスク効果では、Photoshop のアンシャープマスクフィルターと同じオプションが使用されます。 名前から連想される機能と違い、アンシャープマスクとはシャープニングフィルターのことです。

| アンシャープマスクオプション | 説明 |
| --- | --- |
| **[!UICONTROL 量]** | 必須。<br> エッジ ピクセルに適用されるコントラストの量を制御します。<br>この量は、効果の強さと考えることができます。 Dynamic Media と Adobe Photoshop での「アンシャープマスク」の量の値の主な違いは、Photoshop では量の範囲が 1%～500% である点です。 一方、Adobe Dynamic Mediaでは、値の範囲は `0.0` ～ `5.0` です。 Adobe Dynamic Media の値が 5.0 の場合、Photoshop のほぼ 500％ に相当します。値が 0.9 の場合は 90％ に相当します。 |
| **[!UICONTROL 半径]** | 必須。<br>効果の半径を制御します。<br>値の範囲は `0`〜`250` です。 効果は画像内の全ピクセルに切れ目なく続き、すべてのピクセルから全方向に放射されます。 半径の単位はピクセルです。 例えば、2000 x 2000 ピクセルの画像と 500 x 500 ピクセルの画像で同様のシャープなエフェクトを得るには、2000 x 2000 ピクセルの画像で 2 ピクセルの半径を設定します。 次に、500 x 500 ピクセルの画像上で 1 ピクセルの半径値を設定します。 ピクセル数の多い画像には大きい値を使用します。 |
| **[!UICONTROL しきい値]** | 必須。<br>しきい値は、アンシャープマスクフィルターが適用されたときに無視されるコントラストの範囲です。 このエフェクトは、このフィルターの使用中に画像に「ノイズ」が加わるのを防ぐために重要です。 値の範囲は `0`〜`255` で、グレースケール画像の明るさのステップ数です。 `0`=黒、`128`=50% グレー、`255`=白。<br>しきい値`12`を指定すると、肌のトーンの明るさにわずかなバリエーションが無視され、ノイズが加えられるのを防ぐことができますが、まつげと肌の間の部分など、コントラストの強い部分にはエッジ コントラストが加わります。<br>人の顔写真であれば、アンシャープマスクは画像のコントラストが強い部分に作用します。 例えば、まつ毛と肌の境目でコントラストが強く出る部分や、なめらかな肌そのものの部分などです。 なめらかな肌でも、明るさの値はわずかに変化しています。 しきい値を使用しないと、フィルターはこのような肌部分のピクセルのわずかな変化を強調します。 その結果、まつ毛のコントラストが強くなり、シャープさが強調され、ノイズのある望ましくない効果を生み出してしまいます。<br>しきい値は、この問題を解決するために導入されたもので、フィルターに対し、滑らかな肌のようにコントラストが大きく変化しないピクセルを無視するよう指示します。<br>先ほど示したファスナーのグラフィックで、ファスナーの横の生地に注目してください。 しきい値が低すぎてノイズを抑制できなかったので、画像ノイズが発生しています。 |
| **[!UICONTROL モノクロ]** | 画像の明るさ（強度）をアンシャープマスクする場合に選択します。<br>各カラーコンポーネントを個別にアンシャープマスクする場合は選択解除します。 |

[Adobe Dynamic Media および Image Server での画像のシャープニング](/help/assets/assets/sharpening_images.pdf)も参照してください。

### 「PostScript」タブ {#postscript-tab}

Adobe PostScript® ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択を行うことができます。

Adobe PostScript®（EPS）ファイルは、Adobe Dynamic Media で使用できます。 Adobe Dynamic Media には、アップロード時にこれらのファイルを設定するためのコマンドが用意されています。

PostScript（EPS）画像ファイルのアップロード時に、様々な方法でファイルをフォーマットできます。 ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択ができます。

| PostScript オプション | 説明 |
| --- | --- |
| **[!UICONTROL 処理]** | ラスタライズを選択して、ファイル内のベクターグラフィックスをビットマップ形式に変換します。 |
| **[!UICONTROL レンダリング済みの画像での透明背景の維持]** | ファイルの背景の透明度を維持します。 |
| **[!UICONTROL 解像度（ピクセル／インチ）]** | 解像度設定を決定します。 この設定により、ファイル内で 1 インチあたりに表示するピクセル数を決定します。 |
| **[!UICONTROL カラースペース]** | ・ **[!UICONTROL 自動的に検出]** - ファイルのカラースペースを保持します。<br>・ **[!UICONTROL RGBとして強制]** - RGBのカラースペースに変換します。<br>・ **[!UICONTROL CMYKとして強制]** - CMYKのカラースペースに変換します。<br>・ **[!UICONTROL グレースケールとして強制]** - グレースケールのカラースペースに変換します。 |

### 「Photoshop」タブ {#photoshop-tab}

Adobe® Photoshop® ファイルからのテンプレート作成、レイヤーの維持、レイヤーの命名方法の指定、テキストの抽出、テンプレートへの画像のアンカー方法の指定を行うことができます。

| Photoshop オプション | 説明 |
| --- | --- |
| **[!UICONTROL レイヤーを維持]** | PSD にレイヤーがある場合は、レイヤーを切り離して個別のアセットにします。 アセットレイヤーは PSD に関連付けられたまま維持されます。 詳細ビューで PSD ファイルを開き、レイヤーパネルを選択すると、これらを確認できます。 PSD ファイルでのレイヤーの表示と編集を参照してください。 |
| **[!UICONTROL テンプレートを作成]** | PSD ファイル内のレイヤーからテンプレートを作成します。 |
| **[!UICONTROL テキストを抽出]** | テキストを抽出して、ユーザーがビューア内でテキストを検索できるようにします。 |
| **[!UICONTROL レイヤーを背景サイズに拡大]** | 切り離した画像レイヤーのサイズを、背景レイヤーのサイズに拡大します。 |
| **[!UICONTROL レイヤーの名前]** | リッピングされた画像レイヤーのサイズを背景レイヤーのサイズに拡張します。<br>・ **[!UICONTROL レイヤー名]** - PSD ファイル内のレイヤー名の後に画像の名前を付けます。 例えば、元の PSD ファイルに Price Tag という名前のレイヤーがある場合、Price Tag という名前の画像になります。 ただし、PSD ファイル内のレイヤー名がデフォルトの Photoshop レイヤー名（背景、レイヤー 1、レイヤー 2 など）である場合、画像の名前は PSD ファイル内のレイヤー番号に従って付けられます。 <br>• **[!UICONTROL Photoshop とレイヤー番号]** - PSD ファイル内のレイヤー番号に従って画像の名前を付け、元のレイヤー名は無視します。 Photoshop ファイル名の後にレイヤー番号を付けたものが画像の名前になります。 例えば、`Spring Ad.psd`という名前のファイルの2番目のレイヤーは、Photoshopにデフォルト以外の名前が付いている場合でも`Spring Ad_2`という名前になります。<br>・ **[!UICONTROL Photoshopとレイヤー名]** - PSD ファイルの後にレイヤー名またはレイヤー番号が付いた画像に名前を付けます。 PSD ファイル内のレイヤー名がデフォルトの Photoshop レイヤー名である場合、レイヤー番号が使用されます。 例えば、`SpringAd` という名前の PSD ファイルに `Price Tag` という名前のレイヤーがある場合、`Spring Ad_Price Tag` という名前になります。 レイヤー 2 というデフォルト名のレイヤーは `Spring Ad_2` となります。 |
| **[!UICONTROL アンカー]** | PSD ファイルから生成されたレイヤー構成を使用して作成されるテンプレートにおいて、画像がどのようにアンカーされるのかを指定します。 デフォルトでは、アンカーは中央です。 中央のアンカーを使用すると、置換画像の縦横比に関係なく、置換画像で同じ領域をより適切に埋めることができます。 テンプレートを参照してパラメータ置換を使用する場合、この画像を置換する縦横比が異なる画像は、実質的に同じスペースを占有します。 アプリケーションでテンプレート内の割り当てられた領域を置換画像で埋める必要がある場合は、別の設定に変更してください。 |

### 「PDF」タブ {#pdf-tab}

ファイルのラスタライズ、検索単語とリンクの抽出、解像度の設定、カラースペースの選択を行うことができます。

| PDF オプション | 説明 |
| --- | --- |
| **[!UICONTROL 処理]** | ・ **[!UICONTROL なし]** - PDFの処理は完了していません。<br>・ **[!UICONTROL サムネール]** - PDF ファイルの各ページをリッピングし、サムネール画像に変換します。<br> • **[!UICONTROL ラスタライズ]** - PDF ファイルのページをリッピングし、ベクターグラフィックをビットマップイメージに変換します。 eCatalog を作成するには、このオプションを選択します。 |
| **[!UICONTROL 抽出]** | ・ **[!UICONTROL なし]** – 検索ワードまたはリンクがPDFから抽出されません。<br>・**[!UICONTROL 検索ワード]** - PDF ファイルから検索ワードを抽出して、eCatalog ビューアでキーワードで検索できるようにします。<br>・**[!UICONTROL リンク]** - PDF ファイルからリンクを抽出し、eCatalog ビューアで使用される画像マップに変換します。<br>・**[!UICONTROL 検索ワードとリンク]** - e ビューアで使用する両方の検索ワードとリンクを抽出抽出します。 |
| **[!UICONTROL 解像度（ピクセル／インチ）]** | 解像度設定を決定します。 この設定により、PDF ファイル内で 1 インチあたりに表示するピクセル数を決定します。 デフォルトは 150 です。 |
| **[!UICONTROL カラースペース]** | ・ **[!UICONTROL 自動検出]** - PDF ファイルのカラースペースを維持します。<br>・ **[!UICONTROL RGBとして強制]** - RGBのカラースペースに変換します。<br>・ **[!UICONTROL CMYKとして強制]** - CMYK カラースペースに変換します。<br>・ **[!UICONTROL グレースケールとして強制]** - グレースケールのカラースペースに変換します。 |

### 「Illustrator」タブ {#illustrator-tab}

Adobe Illustrator® ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択を行うことができます。

Adobe Dynamic Media で Adobe® Illustrator®（AI）ファイルを使用できます。 Adobe Dynamic Media には、アップロード時にこれらのファイルを設定するためのコマンドが用意されています。

Illustrator（AI）画像ファイルのアップロード時に、様々な方法でファイルをフォーマットできます。 ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択ができます。 PostScript ファイルと Illustrator ファイルをフォーマットするためのオプションは、アップロードジョブのオプションボックスの「PostScript」オプションおよび「Illustrator」オプションの下のアップロード画面で利用できます。


| 「Illustrator」オプション | 説明 |
| --- | --- |
| **[!UICONTROL 処理]** | ラスタライズを選択して、ファイル内のベクターグラフィックスをビットマップ形式に変換します。 |
| **[!UICONTROL レンダリング済みの画像での透明背景の維持]** | ファイルの背景の透明度を維持します。 |
| **[!UICONTROL 解像度（ピクセル／インチ）]** | 解像度設定を決定します。 この設定により、ファイル内で 1 インチあたりに表示するピクセル数を決定します。 |
| **[!UICONTROL カラースペース]** | ・ **[!UICONTROL 自動的に検出]** - ファイルのカラースペースを保持します。<br>・ **[!UICONTROL RGBとして強制]** - RGBのカラースペースに変換します。<br>・ **[!UICONTROL CMYKとして強制]** - CMYKのカラースペースに変換します。<br>・ **[!UICONTROL グレースケールとして強制]** - グレースケールのカラースペースに変換します。 |
