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
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

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

1. FFmpeg実行可能ファイルがシステムパスに設定されていることを確認します。

   システム内の任意のディレクトリからFFmpegを実行できるはずです。

   * for example, `ffmpeg -version`

## FFmpeg トランスコーディングサービスの設定 {#configure-ffmpeg-transcoding-service}

By default, when FFmpeg is installed, multiple renditions are configured (transcodings) as per the [!UICONTROL DAM Update Asset] workflow definition.

トランスコーディングは CPU を集中的に使用するので、対象レンディションのリストを変更することを推奨します。ほとんどの場合、トランスコードは必要ありません。

To modify the [!UICONTROL DAM Update Asset] workflow, and in this example, to turn off transcoding:

* 管理者権限を持つ作成者インスタンスにサインインします
* From global navigation: **[!UICONTROL Tools > Workflow > Models]**
* Locate **[!UICONTROL DAM Update Asset]**
* 重複キーを押しながらクリックして、編集用のワークフローをクラシックUIで開きます

   Resulting location: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Double-click the **[!UICONTROL FFmpeg transcoding]** step to access the Step Properties dialog
* Under the **[!UICONTROL Process]** tab:

   * **[!UICONTROL 歩調]**:トランスコードを無効にするすべてのエントリを消去します。初期設定値： `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* Select **[!UICONTROL OK]** to close the `Step Properties` dialog

* Select **[!UICONTROL Save]** to save the `DAM Update Asset` workflow

   （左上隅）

