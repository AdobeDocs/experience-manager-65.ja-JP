---
title: コミュニティのための FFmpeg
description: コミュニティ用の FFmpeg のインストールと設定の方法
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 3%

---

# コミュニティのための FFmpeg {#ffmpeg-for-communities}

## 概要 {#overview}

FFmpeg は、オーディオとビデオの変換とストリーミングを行うソリューションで、インストール時に、 [ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video).

## FFmpeg のインストール {#installing-ffmpeg}

AEMをホストするサーバーに FFmpeg をインストールする必要があります *作成者* インスタンス。

1. に移動します。 [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. お使いの環境（Macintosh、Windows または Linux）向けの最新バージョンの FFmpeg をダウンロードします。

   * 古いバージョンのセキュリティの脆弱性により、FFmpeg を最新の状態に保つことが重要です。

1. OS の手順に従って FFmpeg をインストールします。

1. FFmpeg 実行可能ファイルがシステムパスに設定されていることを確認します。

   システム内の任意のディレクトリから FFmpeg を実行できるはずです。

   * 例：`ffmpeg -version`。

## FFmpeg トランスコーディングサービスを設定 {#configure-ffmpeg-transcoding-service}

デフォルトでは、FFmpeg がインストールされている場合、 [!UICONTROL DAM アセットの更新] ワークフロー定義。

トランスコーディングは CPU を大量に消費するので、ターゲットレンディションのリストを変更することをお勧めします。 ほとんどの場合、トランスコードは必要ありません。

次の手順で [!UICONTROL DAM アセットの更新] ワークフロー、およびこの例では、トランスコードをオフにするには：

* 管理者権限でオーサーインスタンスにログインします。
* グローバルナビゲーションから、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL ワークフロー]** > **[!UICONTROL モデル]**.
* 場所 **[!UICONTROL DAM アセットの更新]**.
* ダブルクリックして、編集用のワークフローをクラシック UI で開きます。

  結果の場所： [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 次をダブルクリックします。 **[!UICONTROL FFmpeg トランスコード]** ステップ：ステップのプロパティダイアログにアクセスします。
* の下 **[!UICONTROL プロセス]** タブ：

   * **[!UICONTROL アルグメント]**：すべてのエントリをクリアして、トランスコードを無効にします。デフォルト値： `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

  ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 選択 **[!UICONTROL OK]** 閉じる `Step Properties` ダイアログ。

* 選択 **[!UICONTROL 保存]** 保存する `DAM Update Asset` ワークフロー。
