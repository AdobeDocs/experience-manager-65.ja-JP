---
title: 画像トランスコーディングライブラリ
description: エンコーディング、トランスコーディング、画像のリサンプリング、画像のサイズ変更などの中心的な画像処理機能を実行する画像処理ソリューションであるアドビの画像トランスコーディングライブラリを設定および使用する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 画像トランスコーディングライブラリ {#imaging-transcoding-library}

アドビの画像トランスコーディングライブラリは独自の画像処理ソリューションであり、以下のような中心的な画像処理機能を実行できます。

* エンコード
* トランスコーディング（サポートされる形式間での変換）
* PS およびインテル IPP アルゴリズムを使用する画像リサンプリング
* ビット深度およびカラープロファイルの保持
* JPEG画質圧縮
* 画像のサイズ変更

Imaging Transcoding Libraryは、CMYKをサポートし、CMYK -Alphaを除く完全なアルファをサポートします。

Imaging Transcoding Libraryは、幅広いファイル形式やプロファイルをサポートするだけでなく、パフォーマンス、拡張性、品質に関して、他のサードパーティ製ソリューションよりも大きな利点を備えています。 Imaging Transcoding Libraryを使用する主な利点を次に示します。

* **ファイルサイズまたは解像度を増やして拡大**：拡大・縮小は、主にファイルのデコード中のサイズ変更によって実現します。これは画像トランスコーディングライブラリに搭載された特許取得済みの機能です。この機能により、ランタイム中のメモリ使用状況が常に最適化され、ファイルサイズの増加やメガピクセル解像度の二次関数ではなくなります。画像トランスコーディングライブラリは、より大容量の高解像度（メガピクセル値がより高い）ファイルを処理できます。ImageMagick などのサードパーティツールの場合、大容量のファイルを処理できず、ファイルの処理中にクラッシュします。
* **Photoshop 品質の圧縮およびサイズ変更アルゴリズム**：ダウンサンプリングの品質（スムーズ、シャープ、自動バイキュービック）および圧縮品質に関する業界標準に準拠しています。Imaging Transcoding Libraryは、入力画像の画質係数をさらに評価し、出力画像の最適なテーブルと画質設定をインテリジェントに使用します。 この機能により、画質を損なうことなく最適なサイズのファイルが作成されます。
* **** 高スループット：応答時間は短く、スループットはImageMagickよりも常に長くなります。 したがって、Imaging Transcoding Libraryは、ユーザーの待ち時間を短縮し、ホスティングのコストを削減する必要があります。
* **** 同時読み込みに応じて拡張性を向上：Imaging Transcoding Libraryは、同時読み込み条件下で最適に動作します。 CPU パフォーマンスとメモリ使用状況を最適化し、応答時間を短縮しながら、高スループットを実現するため、ホスティングコストを抑えることができます。

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

You can configure the following options for the `-resize` parameter:

* `X`: `Works similar to AEM. For example -resize 319.`
* `WxH`: `Aspect Ratio will not be maintained, For example -resize 319X319.`
* `Wx`: `Fixes the width and calculates the height maintaining the aspect ratio. For example -resize 319x.`
* `xH`: `Fixes the height and calculates the width maintaining the aspect ratio. For example -resize x319.`

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 画像トランスコーディングライブラリの設定 {#configuring-imaging-transcoding-library}

ITL処理を設定するには、設定ファイルを作成し、ワークフローを更新して実行します。

### 抽出されたバンドルの設定ファイルの作成 {#create-conf-file}

ライブラリを設定するには、次の手順を使用して、ライブラリを示す.confファイルを作成します。 管理者権限またはルート権限が必要です。

1. Download the [Imaging Transcoding Library package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) and install it using the Package Manager. このパッケージはAEM 6.5と互換性があります。

1. のバンドルIDを確認するに `com.day.cq.dam.cq-dam-switchengine`は、Webコンソールにログインし、OSGi/Bundlesをタ **[!UICONTROL ップします]**。 または、バンドルコンソールを開くには、 `https://[aem_server:[port]/system/console/bundles/` URLにアクセスします。 バンドル `com.day.cq.dam.cq-dam-switchengine` とそのIDを検索します。

1. コマンドを使用してフォルダーをチェックし、必要なすべてのライブラリが抽出されているこ `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`とを確認します。ここで、フォルダー名はバンドルIDを使用して構築されます。 例えば、コマンドは `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` if bundle idがです `588`。

1. ライブラリ `SWitchEngineLibs.conf` にリンクするファイルを作成します。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. confファ `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` イルにパスを追加するには、コマンドを使 `cat SWitchEngineLibs.conf` 用します。

1. コマンドを `ldconfig` 実行して、必要なリンクとキャッシュを作成します。

1. AEMの起動に使用するアカウントで、ファイルを編集し `.bash_profile` ます。 次を追 `LD_LIBRARY_PATH` 加して追加します。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. パスの値がに設定されていることを確認するには、コマンド `.`を使用し `echo $LD_LIBRARY_PATH` ます。 出力は単にです `.`。 値がに設定されていない場合は、セ `.`ッションを再開します。

### DAM更新アセットの設定ワークフロー {#configure-dam-asset-update-workflow}

DAMアセットの更新ワ [!UICONTROL ークフローを更新し] 、画像の処理にライブラリを使用するようにします。

1. AEM のロゴをタップまたはクリックし、**[!UICONTROL ツール／ワークフロー／モデル]**&#x200B;に移動します。

1. From the **[!UICONTROL Workflow Models]** page, open the **[!UICONTROL DAM Update Asset]** workflow model in edit mode.

1. Open the **[!UICONTROL Process Thumbnails]** workflow process step. In the **[!UICONTROL Thumbnails]** tab, add the MIME types for which you want to skip the default thumbnail generation process in the **[!UICONTROL Skip Mime Types]** list.
For example, if you want to create thumbnails for a TIFF image using Imaging Transcoding Library, specify `image/tiff` in the **[!UICONTROL Skip Mime Types]** field.

1. 「**[!UICONTROL Web に対応した画像]**」タブで、デフォルトの Web レンディション生成プロセスをスキップする MIME タイプを「**[!UICONTROL リストをスキップ]**」に追加します。For example, if you skipped MIME type `image/tiff` in the above step, add `image/tiff` to the skip list.

1. Open the **[!UICONTROL EPS thumbnails (powered by ImageMagick)]** step, navigate to the **[!UICONTROL Arguments]** tab. In the **[!UICONTROL Mime Types]** list, add the MIME types you want Imaging Transcoding Library to process. For example, if you skipped the MIME type `image/tiff` in the above step, add `image/jpeg` to the **[!UICONTROL Mime Types]** list.

1. 既定のコマンドが存在する場合は、それを削除します。

1. サイドパネルを切り替えて、ステップのリストから&#x200B;**[!UICONTROL SWitchEngine ハンドラー]**&#x200B;を追加します。

1. カスタム要件に基づ [!UICONTROL いて] 、SwitchEngineハンドラにコマンドを追加します。 必要に応じて、指定したコマンドのパラメータを調整します。 例えば、JPEG 画像のカラープロファイルを保持したい場合、「**[!UICONTROL コマンド]**」リストに以下のコマンドを追加します。

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`
   ![小石](assets/chlimage_1-199.png)

1. （オプション）1つのコマンドを使用して、中間レンディションからサムネールを生成します。 中間レンディションは静的レンディションと Web レンディションを生成するソースとなります。この方法は最初の方法より処理が高速です。ただし、この方法ではサムネールにカスタムパラメーターを適用できません。

   ![小石](assets/chlimage_1-200.png)

1. Webレンディションを生成するには、「 **[!UICONTROL Web対応の画像」タブでパラメータを設定します]** 。

1. 更新された [!UICONTROL DAM Update Assetワークフローモデルを同期します] 。 ワークフローを保存します。

設定を確認し、TIFF画像をアップロードして、error.logファイルを監視します。 のメンションを含む `INFO` メッセージが表示されま `SwitchEngineHandlingProcess execute: executing command line`す。 ログには、生成されたレンディションが記述されます。 ワークフローが完了すると、AEMで新しいレンディションを表示できます。

>[!MORELIKETHIS]
>
>* [サポートされるMIMEタイプの記事](assets-formats.md#supported-image-transcoding-library)