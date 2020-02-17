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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# コミュニティのための FFmpeg {#ffmpeg-for-communities}

## 概要 {#overview}

FFmpeg は、オーディオとビデオの変換およびストリーミングのためのソリューションです。インストールすると、[ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video)の適切なトランスコーディングと AEM Communities のイネーブルメント 能に使用できます。

FFmpeg は、オーサー環境で、アップロードしたイネーブルメントリソースのメタデータを取得したり、イネーブルメントリソースの一覧に表示するサムネイルを生成するときに使用します。

## FFmpeg のインストール {#installing-ffmpeg}

FFmpeg は AEM *オーサー*&#x200B;インスタンスをホストしているサーバーにインストールする必要があります。

1. Go to [https://www.ffmpeg.org](https://www.ffmpeg.org/)
1. 特定の環境用（Macintosh、Windows または Linux）の FFmpeg の最新バージョンをダウンロードします。

   * 古いバージョンにはセキュリティ脆弱性があるので、FFmpeg を最新の状態に保つことが重要です。

1. OS の手順に従って FFmpeg をインストールします。

1. システムパスにFFmpeg実行可能ファイルが設定されていることを確認します。

   システム内の任意のディレクトリからFFmpegを実行できるはずです。

   * for example, `ffmpeg -version`

## FFmpeg トランスコーディングサービスの設定 {#configure-ffmpeg-transcoding-service}

デフォルトでは、FFmpeg をインストールすると、DAM アセットの更新のワークフロー定義どおりに複数のレンディションが設定されます（トランスコーディング）。

トランスコーディングは CPU を集中的に使用するので、対象レンディションのリストを変更することを推奨します。ほとんどの場合、トランスコードは必要ありません。

DAM アセットの更新のワークフローを変更するには（この例ではトランスコーディングをオフにするには）、次のようにします。

* 管理者権限で作成者インスタンスにサインインします
* From global navigation: **[!UICONTROL Tools > Workflow > Models]**
* Locate **[!UICONTROL DAM Update Asset]**
* ダブルクリックして、編集用のワークフローをクラシックUIで開きます

   Resulting location: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Double-click the **[!UICONTROL FFmpeg transcoding]** step to access the Step Properties dialog
* Under the **[!UICONTROL Process]** tab:

   * **[!UICONTROL 歩調]**:すべてのエントリを消去して、トランスコードのデフォルト値を無効にします。 `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* Select **[!UICONTROL OK]** to close the `Step Properties` dialog

* Select **[!UICONTROL Save]** to save the `DAM Update Asset` workflow

   （左上隅）

