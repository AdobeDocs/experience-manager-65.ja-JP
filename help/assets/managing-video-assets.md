---
title: ビデオアセットの管理
description: ' [!DNL Adobe Experience Manager] でビデオアセットをアップロード、プレビュー、注釈、公開します。'
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
source-git-commit: b0286341c1b643bd39a3009185c0d4c8d76ccba5
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 100%

---

# ビデオアセットの管理 {#manage-video-assets}

ビデオ形式は、組織のデジタルアセットの重要な部分です。[!DNL Adobe Experience Manager] は、ビデオアセットの作成後に、ビデオアセットのライフサイクル全体を管理するための充実した機能を提供しています。

[!DNL Adobe Experience Manager Assets] でビデオアセットを管理および編集する方法について説明します。FFmpeg トランスコーディングなどのビデオのエンコーディングとトランスコーディングは、[!DNL Dynamic Media] 統合を使用して行うことができます。

## ビデオアセットのアップロードとプレビュー {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] は、拡張子が MP4 のビデオアセットのプレビューを生成します。アセットの形式が MP4 でない場合は、FFmpeg パックをインストールしてプレビューを生成します。FFmpeg は、OGG タイプと MP4 タイプのビデオレンディションを作成します。これらのレンディションは、[!DNL Assets] ユーザーインターフェイスでプレビューできます。

1. デジタルアセットフォルダー（またはサブフォルダー）で、デジタルアセットを追加する場所に移動します。
1. アセットをアップロードするには、ツールバーの「**[!UICONTROL 作成]**」をクリックして、「**[!UICONTROL ファイル]**」を選択します。または、ユーザーインターフェイス上でファイルをドラッグします。詳しくは、[アセットのアップロード](manage-assets.md#uploading-assets)を参照してください。
1. カード表示でビデオをプレビューするには、ビデオアセットの「**[!UICONTROL 再生]**」![play option](assets/do-not-localize/play.png)オプションをクリックします。ビデオの一時停止や再生は、カード表示でのみ可能です。リスト表示では、[!UICONTROL 再生]および[!UICONTROL 一時停止]オプションを使用できません。

1. アセットの詳細ページでビデオをプレビューするには、カードの「**[!UICONTROL 編集]**」をクリックします。ビデオは、ブラウザーのネイティブなビデオプレーヤーで再生されます。再生、一時停止、音量の調節およびビデオの全画面表示を行うことができます。

   ![ビデオ再生コントロール](assets/video-playback-controls.png)

## 2 GB を超えるアセットをアップロードするための設定 {#configuration-to-upload-assets-that-are-larger-than-gb}

[!DNL Assets] ではファイルサイズの制限により、デフォルトで 2 GB を超えるアセットをアップロードすることはできません。ただし、この上限は CRXDE Lite を開き、`/apps` ディレクトリ配下にノードを作成することで上書きできます。ノードには、同じノード名とディレクトリ構造および類似した順序のノードプロパティが必要です。

大きなアセットをアップロードするには、[!DNL Assets] 設定に加えて、次の設定を変更します。

* トークンの有効期間を増やします。詳しくは、web コンソールの [!UICONTROL Adobe Granite CSRF サーブレット]を `https://[aem_server]:[port]/system/console/configMgr` で参照してください。詳しくは、[CSRF 保護](/help/sites-developing/csrf-protection.md)を参照してください。
* Dispatcher の設定で `receiveTimeout` を増やします。詳しくは、[Adobe Experience Manager Dispatcher の設定](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja#renders-options)を参照してください。

>[!NOTE]
>
>[!DNL Experience Manager] クラシックユーザーインターフェイスには、2 GB のファイルサイズ上限の制約がありません。また、サイズの大きなビデオでは、エンドツーエンドのワークフローが完全にはサポートされません。

ファイルサイズの制限を高めに設定するには、`/apps` ディレクトリで次の手順を実行します。

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL CRXDE Lite]** をクリックします。
1. CRXDE Lite で、`/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` に移動します。ディレクトリウィンドウを表示するには、「`>>`」をクリックします。
1. ツールバーで、「**[!UICONTROL ノードをオーバーレイ]**」をクリックします。または、コンテキストメニューの「**[!UICONTROL ノードをオーバーレイ]**」を選択します。
1. **[!UICONTROL ノードをオーバーレイ]**&#x200B;ダイアログで「**[!UICONTROL OK]**」をクリックします。

   ![ノードをオーバーレイ](assets/overlay-node-path.png)

1. ブラウザーを更新します。オーバーレイノード `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` が選択されます。
1. サイズ上限を必要なサイズに増やすには、「**[!UICONTROL プロパティ]**」タブで適切な値をバイト単位で入力します。例えば、サイズ制限を 30 GB に増やすには、`32212254720` という値を入力します。

1. ツールバーで「**[!UICONTROL すべて保存]**」をクリックします。
1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL 操作]**／**[!UICONTROL web コンソール]**&#x200B;をクリックします。
1. [!DNL Adobe Experience Manager] の [!UICONTROL web コンソールバンドル]ページで、表の「名前」列で **[!UICONTROL Adobe Granite ワークフロー外部プロセスジョブハンドラー]**&#x200B;を探してクリックします。
1. [!UICONTROL Adobe Granite ワークフロー外部プロセスジョブハンドラー]ページで、「**[!UICONTROL デフォルトタイムアウト]**」フィールドと「**[!UICONTROL 最大タイムアウト]**」フィールドの秒数を`18000`（5 時間）に設定します。「**[!UICONTROL 保存]**」をクリックします。
1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;をクリックします。
1. ワークフローモデルページで「**[!UICONTROL Dynamic Media エンコーディングビデオ]**」を選択し、「**[!UICONTROL 編集]**」をクリックします。
1. ワークフローページで、**[!UICONTROL Dynamic Media ビデオサービスのプロセス]**&#x200B;コンポーネントをダブルクリックします。
1. [!UICONTROL ステップのプロパティ]ダイアログボックスの「**[!UICONTROL 共通]**」タブにある「**詳細設定**」を展開します。
1. 「**[!UICONTROL タイムアウト]**」フィールドの値を `18000` に指定し、「**[!UICONTROL OK]**」をクリックして **[!UICONTROL Dynamic Media エンコーディングビデオ]**&#x200B;ワークフローページに戻ります。
1. ページ上部付近の [!UICONTROL Dynamic Media エンコーディングビデオ]ページのタイトルの下にある「**[!UICONTROL 保存]**」をクリックします。

## ビデオアセットを公開する {#publish-video-assets}

公開後、ビデオアセットを URL として Web ページに含めたり、アセットを直接埋め込んだりできます。詳しくは、[Dynamic Media アセットの公開](/help/assets/publishing-dynamicmedia-assets.md)を参照してください。

## ビデオアセットに注釈を付ける {#annotate-video-assets}

1. [!DNL Assets] コンソールから、アセットカードの「**[!UICONTROL 編集]**」を選択して、アセット詳細ページを表示します。
1. ビデオを再生するには、「**[!UICONTROL プレビュー]**」をクリックします。
1. ビデオに注釈を付けるには、「**[!UICONTROL 注釈]**」をクリックします。注釈がビデオ内の特定の時点（フレーム）に追加されます。注釈を付ける際に、キャンバスに描画して、その画像をコメントと一緒に含めることができます。コメントは自動保存されます。注釈ウィザードを終了するには、「**[!UICONTROL 閉じる]**」をクリックします。

   ![ビデオフレームに描画して注釈を付ける](assets/annotate-video.png)

1. ビデオ内の特定のポイントを探すには、**テキスト**&#x200B;フィールドに時刻（秒）を指定して、「**ジャンプ**」をクリックします。例えば、ビデオの最初の 20 秒をスキップするには、テキストフィールドに「20」と入力します。

   ![ビデオ内の時間をシークして、指定した秒数だけスキップする](assets/seek-in-video.png)

1. タイムラインで表示するには、注釈をクリックします。タイムラインから注釈を削除するには、「**[!UICONTROL 削除]**」をクリックします。

   ![注釈と詳細をタイムラインに表示](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Experience Manager Assets でのデジタルアセットの管理](/help/assets/manage-assets.md)
>* [Experience Manager Assets でのコレクションの管理](/help/assets/manage-collections.md)
>* [Dynamic Media ビデオドキュメント。](/help/assets/video.md)

