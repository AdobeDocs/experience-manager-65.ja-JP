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
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 43%

---


# コミュニティのための FFmpeg {#ffmpeg-for-communities}

## 概要 {#overview}

FFmpeg は、オーディオとビデオの変換およびストリーミングのためのソリューションです。インストールすると、[ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video)の適切なトランスコーディングと AEM Communities のイネーブルメント 能に使用できます。

FFmpeg は、オーサー環境で、アップロードしたイネーブルメントリソースのメタデータを取得したり、イネーブルメントリソースの一覧に表示するサムネイルを生成するときに使用します。

## FFmpeg のインストール  {#installing-ffmpeg}

FFmpeg は AEM *オーサー*&#x200B;インスタンスをホストしているサーバーにインストールする必要があります。

1. [https://www.ffmpeg.org](https://www.ffmpeg.org/)に移動します。
1. ご使用の環境（Macintosh、Windows、またはLinux）用の最新バージョンのFFmpegをダウンロードします。

   * 古いバージョンのセキュリティの脆弱性により、FMPEGを最新の状態に保つことが重要です。

1. OS の手順に従って FFmpeg をインストールします。

1. システムパスにFmpeg実行可能ファイルが設定されていることを確認してください。

   システム内の任意のディレクトリからFFmpegを実行できるはずです。

   * 例：`ffmpeg -version`

## FFmpeg トランスコーディングサービスの設定 {#configure-ffmpeg-transcoding-service}

デフォルトでは、FMPEGがインストールされると、[!UICONTROL DAM Update Asset]ワークフロー定義に従って、複数のレンディションが設定（トランスコーディング）されます。

トランスコーディングは CPU を集中的に使用するので、対象レンディションのリストを変更することを推奨します。ほとんどの場合、トランスコードは必要ありません。

[!UICONTROL DAM Update Asset]ワークフローを変更し、次の例でトランスコードをオフにするには：

* 管理者権限で作成者インスタンスにサインインします。
* グローバルナビゲーションから、**[!UICONTROL ツール]** > **[!UICONTROL ワークフロー]** > **[!UICONTROL モデル]**&#x200B;に移動します。
* **[!UICONTROL DAM Update Asset]**&#x200B;を探します。
* 重複を押しながらクリックすると、編集用のワークフローがクラシックUIで開きます。

   結果の場所：[http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* **[!UICONTROL Fmpegトランスコード]**&#x200B;の手順を重複クリックして、手順のプロパティダイアログにアクセスします。
* 「**[!UICONTROL プロセス]**」タブの下：

   * **[!UICONTROL 軍備]**:すべてのエントリを消去してトランスコードのデフォルト値を無効にします。  `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 「**[!UICONTROL OK]**」を選択して`Step Properties`ダイアログを閉じます。

* 「**[!UICONTROL 保存]**」を選択して、`DAM Update Asset`ワークフローを保存します。



