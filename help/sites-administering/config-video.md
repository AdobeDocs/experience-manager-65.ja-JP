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
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 19%

---

# ビデオコンポーネントの設定  {#configure-the-video-component}

[ビデオコンポーネント](/help/sites-authoring/default-components-foundation.md#video)を使用すると、事前定義済みの標準(OOTB)ビデオアセットをページに配置できます。

適切なトランスコーディングを行うために、管理者はFFmpegを個別にインストールします。 [FFmpegのインストールとAEM](#install-ffmpeg)の設定を参照してください。 管理者は、HTML5要素で使用するビデオプロファイル](#configure-video-profiles)を[設定することもできます。

>[!CAUTION]
>
>この基盤コンポーネントは廃止されました。Adobeでは、代わりに、[コアコンポーネント埋め込みコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html)を利用することをお勧めします。

>[!CAUTION]
>
>このコンポーネントは、プロジェクトレベルのカスタマイズが必要な場合は、すぐに使用できる状態では機能しなくなりました。

## ビデオプロファイルの設定 {#configure-video-profiles}

HTML5要素を使用するには、ビデオプロファイルを定義します。 ここで選ばれたものは順番に使われます。 アクセスするには、[デザインモード](/help/sites-authoring/default-components-designmode.md)（クラシックUIのみ）を使用し、「**[!UICONTROL プロファイル]**」タブを選択します。

![chlimage_1-317](assets/chlimage_1-317.png)

このダイアログから、ビデオコンポーネントのデザインと、[!UICONTROL 再生]、[!UICONTROL Flash]、[!UICONTROL 詳細]のパラメーターを設定することもできます。

## FFmpegをインストールし、AEM {#install-ffmpeg}を設定します。

ビデオコンポーネントは、ビデオのトランスコードにサードパーティのオープンソース製品FFmpegを使用します。 [https://ffmpeg.org/](https://ffmpeg.org/)からダウンロードしました。 FFmpegをインストールした後、特定のオーディオコーデックと特定のランタイムオプションを使用するようにAEMを設定します。

**Windows**&#x200B;にFFmpegをインストールするには、次の手順に従います。

1. コンパイル済みバイナリを`ffmpeg.zip`としてダウンロードします。
1. フォルダーのアーカイブを解除します。
1. システム環境変数`PATH`を&lt;*your-ffmpeg-location*`\bin`に設定します。
1. AEM を再起動します。

**Mac OS X**&#x200B;にFFmpegをインストールするには、次の手順に従います。

1. [developer.apple.com/xcode](https://developer.apple.com/xcode/)で入手可能なXcodeをインストールします。
1. [XQuartz](https://www.xquartz.org)でインストールして、[X11](https://support.apple.com/ja-jp/HT201341)を取得します。
1. [www.macports.org](https://www.macports.org/)で入手可能なMacPortsをインストールします。
1. コンソールで`sudo port install ffmpeg`コマンドを実行し、画面の指示に従います。 `FFmpeg`実行可能ファイルのパスが`PATH`システム変数に追加されていることを確認します。

**Mac OS X 10.6**&#x200B;にFFmpegをインストールするには、次の手順に従います。

1. コンパイル済みバージョンをダウンロードします。
1. `/usr/local`ディレクトリにアーカイブを解除します。
1. コンソールで、`sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`を実行します。 必要に応じてパスを変更します。

**AEM**&#x200B;を設定するには、次の手順に従います。

>[!NOTE]
>
>これらの手順は、コーデックをさらにカスタマイズする必要がある場合にのみ必要です。

1. Web ブラウザーで [!UICONTROL CRXDE Lite] を開きます。[http://localhost:4502/crx/de](http://localhost:4502/crx/de)にアクセスします。
2. `/libs/settings/dam/video/format_aac/jcr:content`ノードを選択し、ノードのプロパティが次のようになっていることを確認します。

   * `audioCodec` マウントされる `aac`.
   * `customArgs` マウントされる `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. 設定をカスタマイズするには、`/apps/settings/`ノードにオーバーレイを作成し、`/conf/global/settings/`ノードの下に同じ構造を移動します。 `/libs`ノードでは編集できません。 例えば、パス`/libs/settings/dam/video/fullhd-bp`をオーバーレイするには、`/conf/global/settings/dam/video/fullhd-bp`にパスを作成します。

   >[!NOTE]
   >
   >変更が必要なプロパティだけでなく、プロファイルノード全体をオーバーレイ／編集してください。そのようなリソースは SlingResourceMerger 経由で解決されません。

4. いずれかのプロパティを変更した場合は、「**[!UICONTROL すべて保存]**」をクリックします。

>[!NOTE]
>
>デフォルトの(OOTB)ワークフローモデルに対する変更は、AEMインスタンスをアップグレードしても保持されません。 Adobeでは、変更したワークフローモデルを編集する前にコピーすることをお勧めします。 例えば、[!UICONTROL DAMアセットの更新]モデルのFFmpegトランスコーディング手順を編集する前に、OOTB [!UICONTROL DAMアセットの更新]モデルをコピーして、アップグレード前に存在したビデオプロファイル名を選択します。 次に、`/apps`ノードをオーバーレイして、AEMがOOTBモデルに対するカスタムの変更を取得できるようにします。
