---
title: ビデオコンポーネントの設定
seo-title: ビデオコンポーネントの設定
description: ビデオコンポーネントの設定方法について説明します。
seo-description: ビデオコンポーネントの設定方法について説明します。
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
translation-type: tm+mt
source-git-commit: 44dbabeeea4e4e8d17cc69a2d8ea791c98be2bd2
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 35%

---


# ビデオコンポーネントの設定 {#configure-the-video-component}

[ビデオコンポーネント](/help/sites-authoring/default-components-foundation.md#video) を使用すると、あらかじめ定義されたOOTB（標準搭載）ビデオ要素をページに配置できます。

For proper transcoding to occur, your administrator must [Install FFmpeg and configure AEM](#install-ffmpeg) separately. HTML5 要素と共に使用するために[ビデオプロファイルを設定](#configure-video-profiles)することもできます。

## ビデオプロファイルの設定 {#configure-video-profiles}

HTML5 要素に使用するビデオプロファイルの定義が必要になる場合があります。ここで選択したものは順番に使用されます。アクセスするには、[デザインモード](/help/sites-authoring/default-components-designmode.md)（クラシック UI のみ）を使用して「**[!UICONTROL プロファイル]**」タブを選択します。

![chlimage_1-317](assets/chlimage_1-317.png)

You can also configure the design of the video components and parameters for [!UICONTROL Playback], [!UICONTROL Flash], and [!UICONTROL Advanced].

## FmpegのインストールとAEMの設定 {#install-ffmpeg}

The Video Component relies on the third-party open-source product FFmpeg for proper transcoding of videos that can be downloaded from [https://ffmpeg.org/](https://ffmpeg.org/). FFmpegをインストールした後、特定のオーディオコーデックと特定のランタイムオプションを使用するようにAEMを設定する必要があります。

**お使いのプラットフォーム用にFFmpegをインストールするには**:

* **Windows の場合：**

   1. `ffmpeg.zip` というコンパイル済みバイナリをダウンロードします。
   1. フォルダーに解凍します。
   1. Set the system environment variable `PATH` to `<*your-ffmpeg-locatio*n>\bin`
   1. AEM を再起動します。

* **Mac OS X：**

   1. Install Xcode ([https://developer.apple.com/technologies/tools/xcode.html](https://developer.apple.com/technologies/tools/xcode.html))
   1. XQuartz/X11 をインストールします。
   1. Install MacPorts ([https://www.macports.org/](https://www.macports.org/))
   1. コンソールで次のコマンドを実行し、指示に従います。

      `sudo port install ffmpeg`

      `FFmpeg` は、AEMがコマンドラインから取得 `PATH` できるようにに設定する必要があります。

* **OS X 10.6 用のコンパイル済みバージョンの使用：**

   1. コンパイル済みバージョンをダウンロードします。
   1. Extract it to the `/usr/local` directory.
   1. ターミナルから、次を実行します。

      `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`

**AEMを設定するには**:

>[!NOTE]
>
>これらの手順は、コーデックをさらにカスタマイズする必要がある場合にのみ必要です。

1. Web ブラウザーで [!UICONTROL CRXDE Lite] を開きます。([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
2. Select the `/libs/settings/dam/video/format_aac/jcr:content` node and ensure that the node properties are as follows:

   * audioCodec：

      ```
       aac
      ```

   * customArgs:

      ```
       -flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8
      ```

3. To customize the configuration, create an overlay in `/apps/settings/` node and move the same structure under `/conf/global/settings/` node. It cannot be edited in `/libs` node. 例えば、パスをオーバーレイするに `/libs/settings/dam/video/fullhd-bp`は、で作成し `/conf/global/settings/dam/video/fullhd-bp`ます。

   >[!NOTE]
   >
   >変更が必要なプロパティだけでなく、プロファイルノード全体をオーバーレイ／編集してください。そのようなリソースは SlingResourceMerger 経由で解決されません。

4. いずれかのプロパティを変更した場合は、「**[!UICONTROL すべて保存]**」をクリックします。

>[!NOTE]
>
>OOTBワークフローモデルは、AEMインスタンスをアップグレードする際に保持されません。 OOTBワークフローモデルを編集する前に、そのモデルをコピーすることをお勧めします。 For example, copy the OOTB [!UICONTROL DAM Update Asset] model before editing the FFmpeg Transcoding step in the [!UICONTROL DAM Update Asset] model to pick video-profile names that existed before the upgrade. Then, you can overlay the `/apps` node to let AEM retrieve the custom changes to the OOTB model.

