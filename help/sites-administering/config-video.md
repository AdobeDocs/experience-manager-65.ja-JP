---
title: ビデオコンポーネントの設定
description: Adobe Experience Manager のビデオコンポーネントを使用して、事前定義された標準提供ビデオアセットをページに配置する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 83%

---

# ビデオコンポーネントの設定 {#configure-the-video-component}

この [ビデオコンポーネント](/help/sites-authoring/default-components-foundation.md#video) 定義済みですぐに使用できるビデオアセットをページに配置できます。

適切なトランスコードを行うために、管理者が FFmpeg を個別にインストールします。詳しくは、[FFmpeg のインストールと AEM の設定](#install-ffmpeg)を参照してください。HTML5 要素と共に使用する場合、管理者は[ビデオプロファイルの設定](#configure-video-profiles)も実施してください。

>[!CAUTION]
>
>この基盤コンポーネントは廃止されました。代わりに、[コアコンポーネント埋め込みコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html?lang=ja)を利用することをお勧めします。

>[!CAUTION]
>
>このコンポーネントは、広範なプロジェクトレベルのカスタマイズをしない限り、標準搭載の状態では使用できなくなりました。

## ビデオプロファイルの設定 {#configure-video-profiles}

HTML 5 要素を使用するには、ビデオプロファイルを定義します。ここで選択したものは順番に使用されます。アクセスするには、[デザインモード](/help/sites-authoring/default-components-designmode.md)（クラシック UI のみ）を使用し、「**[!UICONTROL プロファイル]**」タブを選択します。

![chlimage_1-317](assets/chlimage_1-317.png)

このダイアログから、ビデオコンポーネントのデザインや、[!UICONTROL 再生]、[!UICONTROL Flash]、[!UICONTROL 詳細]のパラメーターを設定することもできます。

## FFmpeg のインストールと AEM の設定 {#install-ffmpeg}

ビデオコンポーネントは、ビデオのトランスコーディングにサードパーティのオープンソース製品 FFmpeg を使用します。[https://ffmpeg.org/](https://ffmpeg.org/) からダウンロードします。FFmpeg をインストールした後、特定のオーディオコーデックと特定のランタイムオプションを使用するように AEM を設定します。

FFmpeg を **Windows** にインストールするには、次の手順を実行します。

1. `ffmpeg.zip` というコンパイル済みバイナリをダウンロードします。
1. アーカイブをフォルダーに解凍します。
1. システム環境変数 `PATH` を *ご利用の ffmpeg- の場所*`\bin`に設定します。
1. AEM を再起動します。

FFmpeg を **macOS X** にインストールするには、次の手順に従います。

1. [developer.apple.com/xcode](https://developer.apple.com/xcode/) で入手可能な Xcode をインストールします。
1. [XQuartz](https://www.xquartz.org) で入手可能な [X11](https://support.apple.com/ja-jp/100724) をインストールします。
1. [www.macports.org](https://www.macports.org/) で入手可能な MacPorts をインストールします。
1. コンソールで `sudo port install ffmpeg` コマンドを実行し、画面上の指示に従って操作します。`FFmpeg` 実行ファイルのパスが `PATH` システム変数に追加されていることを確認します。

FFmpeg を **macOS X 10.6** にインストールするには、事前にコンパイルされたバージョンを使用して、次の手順に従います。

1. コンパイル済みバージョンをダウンロードします。
1. `/usr/local` ディレクトリにアーカイブを解凍します。
1. コンソールで、`sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg` を実行します。パスを適宜変更します。

**AEM を設定**&#x200B;するには、次の手順に従います。

>[!NOTE]
>
>これらの手順は、コーデックをさらにカスタマイズする必要がある場合にのみ必要です。

1. Web ブラウザーで [!UICONTROL CRXDE Lite] を開きます。[http://localhost:4502/crx/de](http://localhost:4502/crx/de) にアクセスします。
2. `/libs/settings/dam/video/format_aac/jcr:content` ノードを選択し、ノードのプロパティが次のようになっていることを確認します。

   * `audioCodec` マウントされる `aac`.
   * `customArgs` マウントされる `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. 設定をカスタマイズするには、 `/apps/settings/` ノードにオーバーレイを作成し、同じ構造を `/conf/global/settings/` ノードの下に移動します。`/libs` ノードで編集することはできません。例えば、パス `/libs/settings/dam/video/fullhd-bp` をオーバーレイするには、`/conf/global/settings/dam/video/fullhd-bp` で作成します。

   >[!NOTE]
   >
   >変更が必要なプロパティだけでなく、プロファイルノード全体をオーバーレイおよび編集してください。そのようなリソースは SlingResourceMerger 経由で解決されません。

4. いずれかのプロパティを変更した場合は、「**[!UICONTROL すべて保存]**」をクリックします。

>[!NOTE]
>
>AEM インスタンスをアップグレードしても、標準のワークフローモデルに対する変更は保持されません。 アドビでは、変更したワークフローモデルを編集する前にコピーすることをお勧めします。例えば、標準のをコピーします [!UICONTROL DAM アセットの更新] で FFmpeg トランスコーディング手順を編集する前のモデル [!UICONTROL DAM アセットの更新] アップグレード前に存在していたビデオプロファイル名を選択するモデル。 次に、をオーバーレイできます `/apps` ノードを使用して、AEMが標準モデルのカスタム変更を取得できるようにします。
