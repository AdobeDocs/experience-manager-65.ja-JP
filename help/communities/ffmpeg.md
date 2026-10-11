---
title: コミュニティのための FFmpeg
description: コミュニティ用にFFmpegをインストールして設定する方法
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 3%
---
# コミュニティのための FFmpeg {#ffmpeg-for-communities}

## 概要 {#overview}

FFmpegは、オーディオおよびビデオを変換およびストリーミングするためのソリューションであり、インストール時に、[&#x200B; ビデオアセット &#x200B;](../../help/sites-authoring/default-components-foundation.md#video)の適切なトランスコードに使用されます。

## FFmpegのインストール {#installing-ffmpeg}

FFmpegは、AEM *author* インスタンスをホストするサーバーにインストールする必要があります。

1. [https://www.ffmpeg.org](https://www.ffmpeg.org/)に移動します。
1. 特定の環境（Macintosh、Windows、またはLinux）に対応した最新バージョンのFFmpegをダウンロードします。

   * 古いバージョンのセキュリティ脆弱性により、FFmpegを最新の状態に保つことが重要です。

1. OSの指示に従ってFFmpegをインストールします。

1. FFmpeg実行可能ファイルがシステムパスに設定されていることを確認します。

   システム内の任意のディレクトリからFFmpegを実行できるはずです。

   * 例えば、`ffmpeg -version` のように指定します。

## FFmpeg トランスコーディングサービスの設定 {#configure-ffmpeg-transcoding-service}

デフォルトでは、FFmpegがインストールされると、[!UICONTROL DAM アセットの更新] ワークフロー定義に従って複数のレンディションが設定（トランスコード）されます。

トランスコードはCPUを多用するので、ターゲットレンディションのリストを変更することをお勧めします。 ほとんどの場合、トランスコードは必要ありません。

[!UICONTROL DAM アセットの更新] ワークフローを変更し、この例では、トランスコードをオフにするには：

* オーサーインスタンスに管理者権限でログインします。
* グローバルナビゲーションから、**[!UICONTROL ツール]** > **[!UICONTROL ワークフロー]** > **[!UICONTROL モデル]**&#x200B;に移動します。
* **[!UICONTROL DAM アセットの更新]**&#x200B;を探します。
* ダブルクリックして、クラシック UIで編集用のワークフローを開きます。

  結果の場所：[http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 「**[!UICONTROL FFmpeg トランスコード]**」ステップをダブルクリックして、「ステップのプロパティ」ダイアログにアクセスします。
* 「**[!UICONTROL プロセス]**」タブの下：

  * **[!UICONTROL 引数]**：すべてのエントリをクリアして、トランスコードを無効にします。既定値：`profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

  ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 「**[!UICONTROL OK]**」を選択して、`Step Properties` ダイアログを閉じます。

* 「**[!UICONTROL 保存]**」を選択して、`DAM Update Asset` ワークフローを保存します。
