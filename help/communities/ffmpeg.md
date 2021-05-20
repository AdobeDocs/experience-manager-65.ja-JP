---
title: コミュニティのための FFmpeg
seo-title: コミュニティのための FFmpeg
description: コミュニティのための FFmpeg をインストールおよび設定する方法
seo-description: コミュニティのための FFmpeg をインストールおよび設定する方法
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Administrator
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 43%

---

# コミュニティのための FFmpeg  {#ffmpeg-for-communities}

## 概要 {#overview}

FFmpeg は、オーディオとビデオの変換およびストリーミングのためのソリューションです。インストールすると、[ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video)の適切なトランスコーディングと AEM Communities のイネーブルメント 能に使用できます。

FFmpeg は、オーサー環境で、アップロードしたイネーブルメントリソースのメタデータを取得したり、イネーブルメントリソースの一覧に表示するサムネイルを生成するときに使用します。

## FFmpeg のインストール  {#installing-ffmpeg}

FFmpeg は AEM *オーサー*&#x200B;インスタンスをホストしているサーバーにインストールする必要があります。

1. [https://www.ffmpeg.org](https://www.ffmpeg.org/)に移動します。
1. お使いの環境（Macintosh、WindowsまたはLinux）向けの最新バージョンのFFmpegをダウンロードします。

   * 古いバージョンのセキュリティの脆弱性により、FFmpegを最新の状態に保つことが重要です。

1. OS の手順に従って FFmpeg をインストールします。

1. FFmpeg実行可能ファイルがシステムパスに設定されていることを確認します。

   システム内の任意のディレクトリからFFmpegを実行できるはずです。

   * （例：`ffmpeg -version`）。

## FFmpeg トランスコーディングサービスの設定 {#configure-ffmpeg-transcoding-service}

デフォルトでは、FFmpegがインストールされると、[!UICONTROL DAMアセットの更新]ワークフロー定義に従って複数のレンディションが設定（トランスコーディング）されます。

トランスコーディングは CPU を集中的に使用するので、対象レンディションのリストを変更することを推奨します。ほとんどの場合、トランスコードは必要ありません。

[!UICONTROL DAMアセットの更新]ワークフローを変更し、この例でトランスコーディングをオフにするには、次のようにします。

* 管理者権限でオーサーインスタンスにログインします。
* グローバルナビゲーションから、**[!UICONTROL ツール]** / **[!UICONTROL ワークフロー]** / **[!UICONTROL モデル]**&#x200B;に移動します。
* **[!UICONTROL DAM Update Asset]**&#x200B;を探します。
* ダブルクリックして、編集用のワークフローをクラシックUIで開きます。

   結果の場所：[http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* **[!UICONTROL FFmpegトランスコーディング]**&#x200B;の手順をダブルクリックして、ステップのプロパティダイアログにアクセスします。
* 「**[!UICONTROL プロセス]**」タブで、次の操作を実行します。

   * **[!UICONTROL 引数]**:トランスコーディングを無効にするには、すべてのエントリをクリアします。デフォルト値：  `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 「**[!UICONTROL OK]**」を選択して、`Step Properties`ダイアログを閉じます。

* 「**[!UICONTROL 保存]**」を選択して、`DAM Update Asset`ワークフローを保存します。
