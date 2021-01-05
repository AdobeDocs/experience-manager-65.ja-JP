---
title: ビデオアセットの管理
description: ' [!DNL Adobe Experience Manager] でビデオアセットをアップロード、プレビュー、注釈、公開します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 58%

---


# ビデオアセットの管理  {#manage-video-assets}

ビデオ形式は、組織のデジタルアセットの重要な部分です。[!DNL Adobe Experience Manager] は、ビデオアセットの作成後に、ビデオアセットのライフサイクル全体を管理するための充実した機能を提供しています。

[!DNL Adobe Experience Manager Assets] でビデオアセットを管理および編集する方法について説明します。[!DNL Dynamic Media]統合を使用して、ビデオのエンコーディングとトランスコーディング（例えば、FFmpegトランスコーディング）を行うことができます。

## ビデオアセットのアップロードとプレビュー {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] は、拡張子が MP4 のビデオアセットのプレビューを生成します。アセットの形式がMP4でない場合は、FFmpegパックをインストールしてプレビューを生成します。 FFmpegは、OGGタイプとMP4タイプのビデオレンディションを作成します。 これらのレンディションは、[!DNL Assets] ユーザーインターフェイスでプレビューできます。

1. デジタルアセットフォルダー（またはサブフォルダー）で、デジタルアセットを追加する場所に移動します。
1. アセットをアップロードするには、ツールバーの「**[!UICONTROL 作成]**」をクリックして、「**[!UICONTROL ファイル]**」を選択します。または、ユーザーインターフェイス上でファイルをドラッグします。詳しくは、[アセットのアップロード](manage-assets.md#uploading-assets)を参照してください。
1. カード表示でビデオをプレビューするには、ビデオアセットの&#x200B;**[!UICONTROL 再生]** ![再生オプション](assets/do-not-localize/play.png)をクリックします。 ビデオの一時停止や再生は、カード表示でのみ可能です。リスト表示では、[!UICONTROL 再生]および[!UICONTROL 一時停止]オプションを使用できません。

1. アセットの詳細ページでビデオをプレビューするには、カードの&#x200B;**[!UICONTROL 編集]**&#x200B;をクリックします。 ビデオは、ブラウザーのネイティブなビデオプレーヤーで再生されます。再生、一時停止、音量の調節およびビデオの全画面表示をおこなうことができます。

   ![ビデオ再生コントロール](assets/video-playback-controls.png)

## 2 GB を超えるアセットをアップロードするための設定 {#configuration-to-upload-assets-that-are-larger-than-gb}

デフォルトでは、ファイルサイズの制限により、[!DNL Assets]では2 GBを超えるアセットはアップロードできません。 ただし、この上限は CRXDE Lite を開き、`/apps` ディレクトリ配下にノードを作成することで上書きできます。ノードには、同じノード名とディレクトリ構造および類似した順序のノードプロパティが必要です。

[!DNL Assets]設定に加えて、次の設定を変更し、大きなアセットをアップロードします。

* トークンの有効期間を増やします。Webコンソール(`https://[aem_server]:[port]/system/console/configMgr`)の「[!UICONTROL AdobeGranite CSRFサーブレット]」を参照してください。 詳しくは、[CSRF保護](/help/sites-developing/csrf-protection.md)を参照してください。
* Dispatcher の設定で `receiveTimeout` を増やします。詳しくは、[Adobe Experience Manager Dispatcher の設定](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options)を参照してください。

>[!NOTE]
>
>[!DNL Experience Manager] Classicユーザーインターフェイスには、2 GBのファイルサイズ制限はありません。 また、サイズの大きなビデオでは、エンドツーエンドのワークフローが完全にはサポートされません。

ファイルサイズの制限を高めに設定するには、`/apps` ディレクトリで次の手順を実行します。

1. [!DNL Experience Manager]で、**[!UICONTROL ツール]**/**[!UICONTROL 一般]**/**[!UICONTROL CRXDE Lite]**&#x200B;をクリックします。
1. CRXDE Lite で、`/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` に移動します。ディレクトリウィンドウを表示するには、`>>`をクリックします。
1. ツールバーで、**[!UICONTROL ノードをオーバーレイ]**&#x200B;をクリックします。 または、コンテキストメニューの「**[!UICONTROL ノードをオーバーレイ]**」を選択します。
1. 「**[!UICONTROL ノードをオーバーレイ]**」ダイアログで、「**[!UICONTROL OK]**」をクリックします。

   ![ノードをオーバーレイ](assets/overlay-node-path.png)

1. ブラウザーを更新します。オーバーレイノード `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` が選択されます。
1. サイズ上限を必要なサイズに増やすには、「**[!UICONTROL プロパティ]**」タブで適切な値をバイト単位で入力します。例えば、サイズ制限を 30 GB に増やすには、`32212254720` という値を入力します。

1. ツールバーで、「**[!UICONTROL すべて保存]**」をクリックします。
1. [!DNL Experience Manager]で、**[!UICONTROL ツール]**/**[!UICONTROL 操作]**/**[!UICONTROL Webコンソール]**&#x200B;をクリックします。
1. [!DNL Adobe Experience Manager] [!UICONTROL Web Console Bundles]ページの表の「Name」列の下で、**[!UICONTROL 「AdobeGranite Workflow External Process Job Handler]**」を探してクリックします。
1. [!UICONTROL AdobeGranite Workflow External Process Job Handler]ページで、**[!UICONTROL Default Timeout]**&#x200B;と&#x200B;**[!UICONTROL Max Timeout]**&#x200B;の両方のフィールドの秒を`18000` （5時間）に設定します。 「**[!UICONTROL 保存]**」をクリックします。
1. [!DNL Experience Manager]で、**[!UICONTROL ツール]**/**[!UICONTROL ワークフロー]**/**[!UICONTROL モデル]**&#x200B;をクリックします。
1. ワークフローモデルページで、「**[!UICONTROL ビデオをDynamic Mediaエンコード]**」を選択し、「**[!UICONTROL 編集]**」をクリックします。
1. ワークフローページで、**[!UICONTROL Dynamic Mediaビデオサービスプロセス]**&#x200B;コンポーネントを重複クリックします。
1. [!UICONTROL ステップのプロパティ]ダイアログボックスの「**[!UICONTROL 共通]**」タブにある「**詳細設定**」を展開します。
1. 「**[!UICONTROL タイムアウト]**」フィールドで値`18000`を指定し、「**[!UICONTROL OK]**」をクリックして&#x200B;**[!UICONTROL Dynamic Mediaエンコードビデオ]**&#x200B;ワークフローページに戻ります。
1. ページの上部近く、「[!UICONTROL Dynamic Mediaエンコードビデオ]」ページタイトルの下にある「**[!UICONTROL 保存]**」をクリックします。

## ビデオアセットを公開する {#publish-video-assets}

公開後、ビデオアセットを URL として Web ページに含めたり、アセットを直接埋め込んだりできます。詳しくは、[Dynamic Media アセットの公開](/help/assets/publishing-dynamicmedia-assets.md)を参照してください。

## ビデオアセットに注釈を付ける {#annotate-video-assets}

1. [!DNL Assets] コンソールから、アセットカードの「**[!UICONTROL 編集]**」を選択して、アセット詳細ページを表示します。
1. ビデオを再生するには、「**[!UICONTROL プレビュー]**」をクリックします。
1. ビデオに注釈を付けるには、「**[!UICONTROL 注釈]**」をクリックします。注釈がビデオ内の特定の時点（フレーム）に追加されます。注釈を付ける際に、キャンバスに描画して、その画像をコメントと一緒に含めることができます。コメントは自動保存されます。注釈ウィザードを終了するには、「**[!UICONTROL 閉じる]**」をクリックします。

   ![ビデオフレームの描画と注釈の追加](assets/annotate-video.png)

1. ビデオ内の特定のポイントを探すには、**テキスト**&#x200B;フィールドに時刻（秒）を指定して、「**ジャンプ**」をクリックします。例えば、ビデオの最初の 20 秒をスキップするには、テキストフィールドに「20」と入力します。

   ![ビデオ内の時間をシークして、指定された秒数だけスキップします](assets/seek-in-video.png)

1. タイムラインで表示するには、注釈をクリックします。タイムラインから注釈を削除するには、「**[!UICONTROL 削除]**」をクリックします。

   ![表示注釈とタイムライン内の詳細](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Experience Managerアセット内のデジタルアセットの管理](/help/assets/manage-assets.md)
>* [Experience Managerアセット内のコレクションの管理](/help/assets/manage-collections.md)
>* [Dynamic Media ビデオドキュメント。](/help/assets/video.md)

