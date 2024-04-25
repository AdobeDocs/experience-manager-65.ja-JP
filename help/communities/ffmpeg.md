---
title: コミュニティのための FFmpeg
description: Communities 用の FFmpeg のインストールおよび設定方法
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 3%

---

# コミュニティのための FFmpeg {#ffmpeg-for-communities}

## 概要 {#overview}

FFmpeg は、オーディオとビデオを変換してストリーミングするためのソリューションで、インストールすると、の適切なトランスコーディングに使用されます。 [ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video).

## FFmpeg のインストール {#installing-ffmpeg}

FFmpeg は、AEMをホストするサーバーにインストールする必要があります *作成者* インスタンス。

1. に移動 [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. お使いの環境（Macintosh、Windows、Linux）に合った最新バージョンの FFmpeg をダウンロードします。

   * 古いバージョンではセキュリティの脆弱性があるので、FFmpeg を最新の状態に保つことが重要です。

1. FFmpeg を OS の手順に従ってインストールします。

1. FFmpeg 実行ファイルがシステムパスに設定されていることを確認します。

   システム内の任意のディレクトリから FFmpeg を実行できるはずです。

   * 例えば、`ffmpeg -version` のように指定します。

## FFmpeg トランスコーディングサービスの設定 {#configure-ffmpeg-transcoding-service}

デフォルトでは、FFmpeg がインストールされている場合、に従って複数のレンディションが設定（トランスコーディング）されます [!UICONTROL DAM アセットの更新] ワークフロー定義。

トランスコードは CPU を大量に消費するので、ターゲットレンディションのリストを変更することをお勧めします。 ほとんどの場合、トランスコーディングは必要ありません。

を変更するには [!UICONTROL DAM アセットの更新] 以下の例では、ワークフローでトランスコーディングをオフにします。

* 管理者権限でオーサーインスタンスにログインします。
* グローバルナビゲーションから、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL ワークフロー]** > **[!UICONTROL モデル]**.
* を見つける **[!UICONTROL DAM アセットの更新]**.
* クラシック UI で編集用のワークフローをダブルクリックして開きます。

  結果の場所： [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* をダブルクリックします **[!UICONTROL FFmpeg トランスコーディング]** 手順を実行して、手順のプロパティダイアログにアクセスします。
* の下 **[!UICONTROL プロセス]** タブ：

   * **[!UICONTROL 引数]**：すべてのエントリをクリアしてトランスコーディングを無効にしますデフォルト値： `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

  ![configure-ffmpeg](assets/configure-ffmpeg.png)

* を選択 **[!UICONTROL OK]** を閉じるには `Step Properties` ダイアログ。

* を選択 **[!UICONTROL 保存]** を保存します `DAM Update Asset` ワークフロー。
