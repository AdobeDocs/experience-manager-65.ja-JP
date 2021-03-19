---
title: 画像トランスコーディングライブラリ
description: エンコーディング、トランスコーディング、画像のリサンプリング、画像のサイズ変更などの中心的な画像処理機能を実行する画像処理ソリューションであるアドビの画像トランスコーディングライブラリを設定および使用する方法について説明します。
contentOwner: AG
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 38%

---


# 画像トランスコーディングライブラリ {#imaging-transcoding-library}

アドビの画像トランスコーディングライブラリは独自の画像処理ソリューションであり、以下のような中心的な画像処理機能を実行できます。

* エンコード
* トランスコーディング（サポートされる形式間での変換）
* PS およびインテル IPP アルゴリズムを使用する画像リサンプリング
* ビット深度およびカラープロファイルの保持
* JPEG画質圧縮
* 画像のサイズ変更

画像処理トランスコードライブラリは、CMYKをサポートし、CMYK -Alphaを除く完全なアルファをサポートします。

Imaging Transcoding Libraryは、幅広いファイル形式とプロファイルをサポートするだけでなく、パフォーマンス、拡張性、品質に関して、他のサードパーティ製のソリューションと比べて大きな利点を有します。 Imaging Transcoding Libraryを使用する主な利点は次のとおりです。

* **ファイルサイズまたは解像度を増やして拡大**：拡大・縮小は、主にファイルのデコード中のサイズ変更によって実現します。これは画像トランスコーディングライブラリに搭載された特許取得済みの機能です。この機能により、ランタイム中のメモリ使用状況が常に最適化され、ファイルサイズの増加やメガピクセル解像度の二次関数ではなくなります。画像トランスコーディングライブラリは、より大容量の高解像度（メガピクセル値がより高い）ファイルを処理できます。ImageMagick などのサードパーティツールの場合、大容量のファイルを処理できず、ファイルの処理中にクラッシュします。
* **Photoshop 品質の圧縮およびサイズ変更アルゴリズム**：ダウンサンプリングの品質（スムーズ、シャープ、自動バイキュービック）および圧縮品質に関する業界標準に準拠しています。Imaging Transcoding Libraryは、入力画像の画質係数をさらに評価し、出力画像の最適なテーブルと画質設定をインテリジェントに使用します。 この機能により、画質を損なうことなく最適なサイズのファイルが作成されます。
* **高スループット：応答時間** は短く、スループットはImageMagickより高いことが一貫して示されます。したがって、Imaging Transcoding Libraryは、ユーザーの待ち時間を短縮し、ホスティングのコストを削減する必要があります。
* **同時負荷に対する拡張性の向上：** イメージングトランスコードライブラリは、同時負荷条件下で最適に動作します。CPU パフォーマンスとメモリ使用状況を最適化し、応答時間を短縮しながら、高スループットを実現するため、ホスティングコストを抑えることができます。

## サポートされているプラットフォーム {#supported-platforms}

Imaging Transcoding Libraryは、RHEL 7およびCentOS 7ディストリビューションでのみ使用できます。

>[!NOTE]
>
>Mac OS やその他の *nix 系ディストリビューション（Debian、Ubuntu など）はサポートされていません。

## 使用方法 {#usage}

画像トランスコーディングライブラリ用のコマンドライン引数には、以下を使用できます。

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

`-resize`パラメーターには、次のオプションを設定できます。

* `X`:と同様の動作 [!DNL Experience Manager]です。例えば、-resize 319。
* `WxH`:例えば、縦横比は維持されません `-resize 319x319`。
* `Wx`：幅を固定し、アスペクト比を維持して高さを計算。例えば、`-resize 319x` のように指定します。
* `xH`：高さを固定し、アスペクト比を維持して幅を計算。例えば、`-resize x319` のように指定します。

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 画像トランスコーディングライブラリの設定 {#configuring-imaging-transcoding-library}

ITL処理を設定するには、設定ファイルを作成し、ワークフローを更新して実行します。

### 抽出されたバンドルの構成ファイルを作成{#create-conf-file}

ライブラリを設定するには、次の手順でライブラリを示すCONFファイルを作成します。 管理者またはルート権限が必要です。

1. [Imaging Transcoding LibraryパッケージをSoftware Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg)からダウンロードし、Package Managerを使用してインストールします。 パッケージは[!DNL Experience Manager] 6.5と互換性があります。

1. `com.day.cq.dam.cq-dam-switchengine`のバンドルIDを知るには、Webコンソールにログインし、**[!UICONTROL OSGi]**/**[!UICONTROL Bundles]**&#x200B;をクリックします。 または、バンドルコンソールを開くには、`https://[aem_server:[port]/system/console/bundles/` URLにアクセスします。 `com.day.cq.dam.cq-dam-switchengine`バンドルとそのIDを探します。

1. `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`コマンドを使用してフォルダーをチェックし、必要なライブラリがすべて抽出されていることを確認します。ここで、フォルダー名はバンドルIDを使用して構築されます。 例えば、バンドルIDが`588`の場合、コマンドは`ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/`です。

1. ライブラリにリンクする`SWitchEngineLibs.conf`ファイルを作成します。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 追加`/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` `cat SWitchEngineLibs.conf`コマンドを使用したconfファイルへのパス。

1. `ldconfig`コマンドを実行して、必要なリンクとキャッシュを作成します。

1. [!DNL Experience Manager]の開始に使用するアカウントで、`.bash_profile`ファイルを編集します。 追加`LD_LIBRARY_PATH`を追加します。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. パスの値を`.`に確実に設定するには、`echo $LD_LIBRARY_PATH`コマンドを使用します。 出力は`.`にする必要があります。 値が`.`に設定されていない場合は、セッションを再起動します。

### [!UICONTROL DAM更新アセット]ワークフロー{#configure-dam-asset-update-workflow}を構成

[!UICONTROL DAM Update Asset]ワークフローを更新して、画像の処理にライブラリを使用します。

1. [!DNL Experience Manager]ユーザーインターフェイスで、**[!UICONTROL ツール]**/**[!UICONTROL ワークフロー]**/**[!UICONTROL モデル]**&#x200B;を選択します。

1. **[!UICONTROL ワークフローモデル]**&#x200B;ページから、**[!UICONTROL DAM更新アセット]**&#x200B;ワークフローモデルを編集モードで開きます。

1. **[!UICONTROL プロセスサムネール]**&#x200B;ワークフローのプロセスステップを開きます。 「**[!UICONTROL サムネール]**」タブで、**[!UICONTROL MIMEタイプをスキップ]**リストのデフォルトのサムネール生成プロセスをスキップするMIMEタイプを追加します。
例えば、Imaging Transcoding Libraryを使用してTIFF画像のサムネールを作成する場合は、「**[!UICONTROL MIMEタイプをスキップ]**」フィールドに`image/tiff`を指定します。

1. 「**[!UICONTROL Web に対応した画像]**」タブで、デフォルトの Web レンディション生成プロセスをスキップする MIME タイプを「**[!UICONTROL リストをスキップ]**」に追加します。例えば、上記の手順でMIMEタイプ`image/tiff`をスキップした場合、スキップリストに`image/tiff`を追加します。

1. **[!UICONTROL EPSサムネール(powered by ImageMagick)]**&#x200B;を開き、**[!UICONTROL 「引数]**」タブに移動します。 **[!UICONTROL MIMEタイプ]**&#x200B;リストーに、Imaging Transcoding Libraryで処理するMIMEタイプを追加します。 例えば、上記の手順でMIMEタイプ`image/tiff`をスキップした場合、**[!UICONTROL Mimeタイプ]**&#x200B;リストに`image/jpeg`を追加します。

1. 既定のコマンドが存在する場合は、そのコマンドを削除します。

1. サイドパネルを切り替えて、ステップのリストから&#x200B;**[!UICONTROL SWitchEngine ハンドラー]**&#x200B;を追加します。

1. カスタムの要件に追加基づいて、[!UICONTROL SwitchEngine Handler]に対するコマンドを指定します。 指定するコマンドのパラメータを要件に合わせて調整します。 例えば、JPEG 画像のカラープロファイルを保持したい場合、「**[!UICONTROL コマンド]**」リストに以下のコマンドを追加します。

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![小粒](assets/chlimage_1-199.png)

1. （オプション）1つのコマンドを使用して、中間レンディションからサムネールを生成します。 中間レンディションは静的レンディションと Web レンディションを生成するソースとなります。この方法は最初の方法より処理が高速です。ただし、この方法ではサムネールにカスタムパラメーターを適用できません。

   ![小粒](assets/chlimage_1-200.png)

1. Webレンディションを生成するには、「**[!UICONTROL Web対応の画像]**」タブでパラメーターを設定します。

1. 更新された[!UICONTROL DAM更新アセット]ワークフローモデルを同期します。 ワークフローを保存します。

設定の検証を行い、TIFF画像をアップロードしてerror.logファイルを監視します。 `INFO`のメンションが`SwitchEngineHandlingProcess execute: executing command line`であることに気づくでしょう。 ログには、生成されたレンディションが記述されています。 ワークフローが完了したら、[!DNL Experience Manager]に新しいレンディションを表示できます。

>[!MORELIKETHIS]
>
>* [サポートされるMIMEタイプの記事](assets-formats.md#supported-image-transcoding-library)

