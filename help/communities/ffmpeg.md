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

FFmpeg は、オーディオとビデオを変換してストリーミングするためのソリューションで、インストールする場合は [ ビデオアセット ](../../help/sites-authoring/default-components-foundation.md#video) の適切なトランスコードに使用されます。

## FFmpeg のインストール {#installing-ffmpeg}

FFmpeg は、AEM（オーサー *インスタンスをホストするサーバーにインストールする必要* あります。

1. [https://www.ffmpeg.org](https://www.ffmpeg.org/) に移動します。
1. お使いの環境（Macintosh、Windows、Linux）に合った最新バージョンの FFmpeg をダウンロードします。

   * 古いバージョンではセキュリティの脆弱性があるので、FFmpeg を最新の状態に保つことが重要です。

1. FFmpeg を OS の手順に従ってインストールします。

1. FFmpeg 実行ファイルがシステムパスに設定されていることを確認します。

   システム内の任意のディレクトリから FFmpeg を実行できるはずです。

   * 例えば、`ffmpeg -version` のように指定します。

## FFmpeg トランスコーディングサービスの設定 {#configure-ffmpeg-transcoding-service}

デフォルトでは、FFmpeg がインストールされている場合、[!UICONTROL DAM アセットの更新 &#x200B;] ワークフロー定義に従って複数のレンディションが設定（トランスコーディング）されます。

トランスコードは CPU を大量に消費するので、ターゲットレンディションのリストを変更することをお勧めします。 ほとんどの場合、トランスコーディングは必要ありません。

[!UICONTROL DAM アセットの更新 &#x200B;] ワークフローを変更するには、この例では、トランスコーディングをオフにします。

* 管理者権限でオーサーインスタンスにログインします。
* グローバルナビゲーションから、**[!UICONTROL ツール]**/**[!UICONTROL ワークフロー]**/**[!UICONTROL モデル]** に移動します。
* **[!UICONTROL DAM アセットの更新]** を見つけます。
* クラシック UI で編集用のワークフローをダブルクリックして開きます。

  結果の場所：[http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* **[!UICONTROL FFmpeg トランスコーディング]** ステップをダブルクリックして、ステップのプロパティダイアログにアクセスします。
* 「**[!UICONTROL プロセス]**」タブで以下を実行します。

   * **[!UICONTROL 引数]**：すべてのエントリをクリアしてトランスコーディングを無効にしますデフォルト値：`profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

  ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 「**[!UICONTROL OK]**」を選択して、`Step Properties` のダイアログを閉じます。

* 「**[!UICONTROL 保存]**」を選択して、`DAM Update Asset` のワークフローを保存します。
