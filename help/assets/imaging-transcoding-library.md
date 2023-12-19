---
title: 画像トランスコーディングライブラリ
description: エンコーディング、トランスコーディング、画像のリサンプリング、画像のサイズ変更などの中心的な画像処理機能を実行できる画像処理ソリューションであるアドビの画像トランスコーディングライブラリを設定および使用する方法について説明します。
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
exl-id: b67465f9-177c-49c4-b4eb-a1d6e09ac9a2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 98%

---

# 画像トランスコーディングライブラリ {#imaging-transcoding-library}

アドビの画像トランスコーディングライブラリは独自の画像処理ソリューションであり、以下のような中心的な画像処理機能を実行できます。

* エンコーディング
* トランスコーディング（サポートされる形式間での変換）
* PS およびインテル IPP アルゴリズムを使用する画像リサンプリング
* ビット深度とカラープロファイルの保持
* JPEG 品質の圧縮
* 画像のサイズ変更

画像トランスコーディングライブラリは、CMYK のサポートと、CMYK -Alpha を除く完全なアルファをサポートします。

幅広いファイル形式とプロファイルのサポートに加え、画像トランスコーディングライブラリは他のサードパーティソリューションに比べ、パフォーマンス、拡張性、品質の面で非常に優れています。画像トランスコーディングライブラリには、主に以下のような利点があります。

* **ファイルサイズまたは解像度を増やして拡大**：拡大／縮小は、主にファイルのデコード中のサイズ変更によって実現します。これは画像トランスコーディングライブラリに搭載された特許取得済みの機能です。この機能により、実行時のメモリ使用状況が常に最適化され、ファイルサイズの増加やメガピクセル解像度の二次関数ではなくなります。画像トランスコーディングライブラリは、より大容量の高解像度（メガピクセル値がより高い）ファイルを処理できます。ImageMagick などのサードパーティツールの場合は、大容量のファイルを処理できず、ファイルの処理中にクラッシュします。
* **Photoshop 品質の圧縮およびサイズ変更アルゴリズム**：ダウンサンプリングの品質（スムーズ、シャープ、自動バイキュービック）および圧縮品質に関する業界標準に準拠しています。画像トランスコーディングライブラリは、入力画像の品質係数をさらに評価し、最適なテーブルと品質設定を出力画像にインテリジェントに適用します。この機能により、画質を損なうことなく最適なサイズのファイルが作成されます。
* **高スループット**：ImageMagick より応答時間が短く、スループットは安定して高くなります。そのため、画像トランスコーディングライブラリはユーザーの待ち時間を短縮し、ホスティングコストを低減します。
* **同時読み込みによる拡大・縮小の向上**：画像トランスコーディングライブラリは、同時読み込み状態で最適に機能します。CPU パフォーマンスとメモリ使用状況を最適化し、応答時間を短縮しながら、高スループットを実現するため、ホスティングコストを抑えることができます。

## サポートされているプラットフォーム {#supported-platforms}

画像トランスコーディングライブラリは、RHEL 7 および CentOS 7 ディストリビューションでのみ使用できます。

>[!NOTE]
>
>Mac OS やその他の *nix 系ディストリビューション（Debian、Ubuntu など）はサポートされていません。

## 使用方法 {#usage}

画像トランスコーディングライブラリ用のコマンドライン引数には、以下のものを使用できます。

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth '4' is automatically converted to '8'
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

`-resize` パラメーターには、以下のオプションを設定できます。

* `X`：[!DNL Experience Manager] と同様に機能。例えば、-resize 319 のように指定します。
* `WxH`：縦横比が維持されない（例： ） `-resize 319x319`.
* `Wx`：幅を固定し、アスペクト比を維持して高さを計算。例えば、`-resize 319x` のように指定します。
* `xH`：高さを固定し、アスペクト比を維持して幅を計算。例えば、`-resize x319` のように指定します。

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 画像トランスコーディングライブラリの設定 {#configuring-imaging-transcoding-library}

ITL 処理を設定するには、設定ファイルを作成し、ワークフローを更新して実行します。

### 抽出されたバンドルの設定ファイルを作成 {#create-conf-file}

ライブラリを設定するには、次の手順で、ライブラリを示す CONF ファイルを作成します。管理者またはルート権限が必要です。

1. [Software Distribution から画像トランスコーディングライブラリパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg)をダウンロードし、パッケージマネージャーを使用してインストールします。このパッケージは [!DNL Experience Manager] 6.5 と互換性があります。

1. `com.day.cq.dam.cq-dam-switchengine` のバンドル ID を調べるには、web コンソールにログインし、 **[!UICONTROL OSGi]**／**[!UICONTROL バンドル]**&#x200B;をクリックします。または、バンドルコンソールを開くには、 `https://[aem_server:[port]/system/console/bundles/` URL にアクセスします。`com.day.cq.dam.cq-dam-switchengine` バンドルとその ID を見つけます。

1. コマンド `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` を使用してフォルダーを確認し、必要なすべてのライブラリーが抽出されていることを確認します。フォルダー名はバンドル ID を使用して作成されます。例えば、バンドル ID が `588` の場合、コマンドは `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` になります。

1. `SWitchEngineLibs.conf` ファイルを作成して、ライブラリにリンクします。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. `cat SWitchEngineLibs.conf` コマンドを使用して、 `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` パスを conf ファイルに追加します。

1. `ldconfig` コマンドを実行して、必要なリンクとキャッシュを作成します。

1. [!DNL Experience Manager] の開始に使用するアカウントで、`.bash_profile` ファイルを編集します。次を追加して、`LD_LIBRARY_PATH` を追加します。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. パスの値が `.` に設定されていることを確認するには、`echo $LD_LIBRARY_PATH` コマンドを使用します。出力は `.` のみです。値が `.` に設定されている場合は、セッションを再起動します。

### [!UICONTROL DAM アセットの更新]ワークフローの設定 {#configure-dam-asset-update-workflow}

[!UICONTROL DAM アセットの更新]ワークフローを更新して、画像の処理にライブラリを使用します。

1. [!DNL Experience Manager] ユーザインタフェースで、 **[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;を選択します。

1. **[!UICONTROL ワークフローモデル]**&#x200B;ページで、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローモデルを編集モードで開きます。

1. **[!UICONTROL サムネールを処理]**&#x200B;ワークフロープロセスステップを開きます。「**[!UICONTROL サムネール]**」タブで、デフォルトのサムネール生成プロセスをスキップする MIME タイプを「**[!UICONTROL スキップ MIME タイプ]**」リストに追加します。例えば、画像トランスコーディングライブラリを使用して TIFF 画像のサムネールを作成する場合、「**[!UICONTROL MIME タイプをスキップ]**」フィールドで「`image/tiff`」を指定します。

1. 「**[!UICONTROL Web に対応した画像]**」タブで、デフォルトの Web レンディション生成プロセスをスキップする MIME タイプを「**[!UICONTROL リストをスキップ]**」に追加します。例えば、上記の手順 で MIME タイプ `image/tiff` をスキップした場合は、「`image/tiff`」をスキップリストに追加します。

1. **[!UICONTROL EPS のサムネール（powered by ImageMagic）]**&#x200B;ステップを開き、「**[!UICONTROL 引数]**」タブに移動します。画像トランスコーディングライブラリで処理する MIME タイプを「**[!UICONTROL MIME タイプ]**」リストに追加します。例えば、上記の手順 で MIME タイプ `image/tiff` をスキップした場合は、「**[!UICONTROL MIME タイプ]**」リストに「`image/jpeg`」を追加します。

1. デフォルトのコマンドが存在する場合は、そのコマンドを削除します。

1. サイドパネルを切り替えて、ステップのリストから&#x200B;**[!UICONTROL SWitchEngine ハンドラー]**&#x200B;を追加します。

1. カスタム要件に基づいて、コマンドを [!UICONTROL SwitchEngine ハンドラー]に追加します。必要に応じて、指定したコマンドのパラメーターを調整します。例えば、JPEG 画像のカラープロファイルを保持したい場合、「**[!UICONTROL コマンド]**」リストに以下のコマンドを追加します。

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![chlimage](assets/chlimage_1-199.png)

1. 単一のコマンドを使用して中間レンディションからサムネールを生成します。中間レンディションは静的レンディションと web レンディションを生成するソースとなります。この方法は最初の方法より処理が高速です。ただし、この方法ではサムネールにカスタムパラメーターを適用できません。

   ![chlimage](assets/chlimage_1-200.png)

1. Web レンディションを生成するには、「 **[!UICONTROL Web に対応した画像]** 」タブでパラメーターを設定します。

1. 更新した [!UICONTROL DAM アセットの更新]ワークフローモデルを同期します。ワークフローを保存します。

設定を確認し、TIFF 画像をアップロードして、error.log ファイルを監視します。`SwitchEngineHandlingProcess execute: executing command line` が記載された `INFO` メッセージ が表示されます。ログには、生成されたレンディションが記録されます。ワークフローが完了したら、[!DNL Experience Manager] で新しいレンディションを表示できます。

>[!MORELIKETHIS]
>
>* [サポートされる MIME タイプに関する記事](assets-formats.md#supported-image-transcoding-library)
