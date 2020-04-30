---
title: '[!DNL Adobe Experience Manager Assets]を[!DNL Adobe InDesign Server]と統合する'
description: '[!DNL Adobe Experience Manager Assets]を[!DNL Adobe InDesign Server]と統合する方法を説明します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 統合 [!DNL Adobe Experience Manager Assets] 対象 [!DNL Adobe InDesign Server] : {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 使用する:

* プロキシ：特定の処理タスクのロードを分配するために使用します。A proxy is an [!DNL Experience Manager] instance that communicates with a proxy worker to fulfil a specific task, and other [!DNL Experience Manager] instances to deliver the results.
* プロキシワーカー：特定のタスクを定義し管理するために使用します。These can cover a wide variety of tasks; for example, using an [!DNL InDesign Server] to process files.

To fully upload files to [!DNL Experience Manager Assets] that you have created with [!DNL Adobe InDesign] a proxy is used. This uses a proxy worker to communicate with the [!DNL Adobe InDesign Server], where [scripts](https://www.adobe.com/jp/devnet/indesign/documentation.html#idscripting) are run to extract metadata and generate various renditions for [!DNL Experience Manager Assets]. The proxy worker enables the two-way communication between the [!DNL InDesign Server] and the [!DNL Experience Manager] instance(s) in a cloud configuration.

>[!NOTE]
>
>[!DNL Adobe InDesign] は、2つの異なるオファーとして提供されます。 [印刷やデジタル配布用のページレイアウトをデザインするために使用されるAdobe InDesign](https://www.adobe.com/jp/products/indesign.html) デスクトップアプリケーション。 [Adobe InDesign Serverを使用すると](https://www.adobe.com/jp/products/indesignserver.html) 、で作成した内容に基づいて、自動ドキュメントをプログラムで作成できま [!DNL InDesign]す。 ExtendScriptエンジンに対するインターフェイスを提供するサービスとし [て動作します](https://www.adobe.com/jp/devnet/scripting.html) 。スクリプトは、に似た形で [!DNL ExtendScript]記述されています [!DNL JavaScript]。 For information about [!DNL InDesign] scripts see [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/jp/devnet/indesign/documentation.html#idscripting).

## How the extraction works {#how-the-extraction-works}

The [!DNL Adobe InDesign Server] can be integrated with [!DNL Experience Manager Assets] so that INDD files created with [!DNL InDesign] can be uploaded, renditions generated, all media extracted (for example, video) and stored as assets:

>[!NOTE]
>
>Previous versions of [!DNL Experience Manager] were able to extract XMP and the thumbnail, now all media can be extracted.

1. Upload your INDD file to [!DNL Experience Manager Assets].
1. A framework sends command script(s) to the [!DNL InDesign Server] via SOAP (Simple Object Access Protocol).
このコマンドスクリプトは、次のことを実行します。

   * INDD ファイルを取得します。
   * 実行コ [!DNL InDesign Server] マンド：

      * 構造、テキストおよびすべてのメディアファイルが抽出されます。
      * PDF と JPG のレンディションが生成されます。
      * HTML と IDML のレンディションが生成されます。
   * Post the resulting files back to [!DNL Experience Manager Assets].
   >[!NOTE]
   >
   >IDMLは、ファイルのすべてのコンテンツをレンダリングするXMLベースの形式 [!DNL InDesign] です。 It is stored as an compressed package using [ZIP](https://www.techterms.com/definition/zip) compression. 詳しくは、 [InDesign Interchange Formats INX and IDMLを参照してください](http://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)。

   >[!CAUTION]
   >
   >If the [!DNL InDesign Server] is not installed or not configured, then you can still upload an INDD file into [!DNL Experience Manager]. ただし、この場合に生成されるレンディションは、PNG と JPEG に限定されます。HTML、IDML またはページのレンディションを生成することはできません。

1. 抽出およびレンダリング生成後：

   * 構造が `cq:Page`（レンディションタイプ）に複製されます。
   * The extracted text and files are stored in [!DNL Experience Manager Assets].
   * All renditions are stored in [!DNL Experience Manager Assets], in the asset itself.

## AEMとの [!DNL InDesign Server] 統合 {#integrating-the-indesign-server-with-aem}

To integrate the [!DNL InDesign Server] for use with [!DNL Experience Manager Assets] and after configuring your proxy, you need to:

1. [InDesign Server をインストールします](#installing-the-indesign-server)。
1. If required, [configure the Experience Manager Assets Workflow](#configuring-the-aem-assets-workflow).
これは、デフォルト値がインスタンスに適さない場合にのみ必要です。
1. [InDesign Server のプロキシワーカー](#configuring-the-proxy-worker-for-indesign-server)を設定します。

### Install the [!DNL InDesign Server] {#installing-the-indesign-server}

To install and start the [!DNL InDesign Server] for use with [!DNL Experience Manager]:

1. Download and install the [!DNL InDesign Server].

1. If required, you can customize the configuration of your [!DNL InDesign Server] instance.

1. コマンドラインから、サーバーを起動します。

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   SOAP プラグインがポート 8080 でリスンする状態でサーバーが起動されます。すべてのログメッセージと出力がコマンドウィンドウに直接書き込まれます。

   >[!NOTE]
   >
   >ファイルに出力メッセージを保存してリダイレクトを使用する場合は、例えば Windows の場合は次のように実行します。
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### ワークフローの [!DNL Experience Manager Assets] 設定 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] には、次の処理手順を含む、事前設定さ **[!UICONTROL れたワークフローDAM更新アセット]**（特に次の場合）がありま [!DNL InDesign]す。

* [メディア抽出](#media-extraction)
* [ページ抽出](#page-extraction)

This workflow is setup with default values that can be adapted for your setup on the various author instances (this is a standard workflow, so further information is available under [Editing a Workflow](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). If you are using the default values (including the SOAP port), then no configuration is needed.

After the setup, uploading [!DNL InDesign] files into [!DNL Experience Manager Assets] (by any of the usual methods) triggers the workflow to process the asset and prepare the various renditions. Test your configuration by uploading an INDD file into [!DNL Experience Manager Assets] to confirm that you see the different renditions created by IDS under `<*your_asset*>.indd/Renditions`

#### Media extraction {#media-extraction}

このステップでは、INDD ファイルからのメディアの抽出を制御します。

カスタマイズするには、**[!UICONTROL メディア抽出]**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![メディア抽出の引数とスクリプトパス](assets/media_extraction_arguments_scripts.png)

メディア抽出の引数とスクリプトパス

* **ExtendScriptライブラリ**:これは、他のスクリプトで必要な、単純なhttpのget/postメソッドライブラリです。

* **スクリプトの拡張**:ここでは、異なるスクリプトの組み合わせを指定できます。 If you want your own scripts to be executed on the [!DNL InDesign Server], save the scripts at `/apps/settings/dam/indesign/scripts`.

Indesignスクリプトについて詳しくは、 [InDesign開発者向けドキュメントを参照してください](https://www.adobe.com/jp/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>ExtendScript ライブラリは変更しないでください。このライブラリは Sling との通信に必要になる HTTP 機能を提供するものです。This setting specifies the library to be send to the [!DNL InDesign Server] for use there.

The `ThumbnailExport.jsx` script run by the Media Extraction workflow step generates a thumbnail rendition in JPG format. This rendition is used by the Process Thumbnails workflow step to generate the static renditions required by [!DNL Experience Manager].

サムネールを処理ワークフローステップは、異なるサイズの静的レンディションを生成するように設定できます。Ensure that you do not remove the defaults, because they are required by the [!DNL Experience Manager Assets] interface. 最後に、画像プレビューレンディションを削除ワークフローステップで不要になった .jpg 形式のサムネールレンディションが削除されます。

#### Page extraction {#page-extraction}

This creates an [!DNL Experience Manager] page from the extracted elements. 抽出ハンドラーが、レンディション（現時点では HTML または IDML）からデータを抽出するために使用されます。このデータを元に、PageBuilder を使用してページが作成されます。

カスタマイズするには、**[!UICONTROL ページ抽出]**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![chlimage_1-96](assets/chlimage_1-289.png)

* **ページ抽出ハンドラ**:ポップアップリストから、使用するハンドラーを選択します。 抽出ハンドラーは、関連する `RenditionPicker`（`ExtractionHandler` API を参照）によって選択された特定のレンディションに対して動作します。In a standard [!DNL Experience Manager] installation the following is available:
   * IDML Export Extraction Handle: Operates on the `IDML` rendition generated in the MediaExtract step.

* **ページ名**:結果のページに割り当てる名前を指定します。空白の場合、名前は「page」（または「page」が既に存在する場合は派生）です。

* **ページタイトル**:結果のページに割り当てるタイトルを指定します。

* **Page Root Path**:結果のページのルート位置へのパス。空白のままにすると、アセットのレンディションを保持するノードが使用されます。

* **ページテンプレート**:結果のページの生成時に使用するテンプレートです。

* **ページデザイン**:結果のページの生成時に使用するページデザインです。

### 次のプロキシワーカーの設 [!DNL InDesign Server] 定 {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>ワーカーは、プロキシインスタンス上にあります。

1. 「ツール」コンソールの左側のウィンドウで、「**[!UICONTROL クラウドサービス設定]**」を展開します。次に、「**[!UICONTROL クラウドプロキシ設定]**」を展開します。

1. 「**[!UICONTROL IDS ワーカー]**」をダブルクリックし、開いて設定します。

1. 「**[!UICONTROL 編集]**」をクリックして設定ダイアログを開き、必要な設定を定義します。

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDSプール**：との通信に使用するSOAPエンドポイントです [!DNL InDesign Server]。アイテムの追加、削除、および注文が必要な場合は、

1. 「OK」をクリックして保存します。

### Configure Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

If the [!DNL InDesign Server] and [!DNL Experience Manager] run on different hosts or either or both these applications do not run on default ports, configure [!UICONTROL Day CQ Link Externalizer] to set the host name, port, and content path for the [!DNL InDesign Server].

1. Access the Web Console at `https://[aem_server]:[port]/system/console/configMgr`.
1. Locate the configuration **[!UICONTROL Day CQ Link Externalizer]**, and tap **[!UICONTROL Edit]** to open it.
1. Specify the host name and context path for the [!DNL Indesign Server] and click **Save**.

   ![chlimage_1-97](assets/chlimage_1-290.png)

### ジョブの並列処理を有効に [!DNL InDesign Server] する {#enabling-parallel-job-processing-for-indesign-server-s}

IDS の並列ジョブ処理を有効にすることができます。処理できる並列ジョブの最大数(`x`)を決 [!DNL InDesign Server] 定します。

* On a single multiprocessor machine, the maximum number of parallel jobs (`x`) that an [!DNL InDesign Server] can process is one less than the number of processors running IDS.
* 複数のマシンで IDS を実行する場合は、すべてのマシンで使用可能なプロセッサーの総数を把握して、そこからマシン総数を減算する必要があります。

IDS 並列ジョブ数を設定するには：

1. Felix Console の「**[!UICONTROL Configurations]**」タブを開きます。次に URL の例を挙げます。 `https://[aem_server]:[port]/system/console/configMgr`.

1. Select the IDS processing queue under `Apache Sling Job Queue Configuration`.

1. 次のように設定します。

   * **Type** - `Parallel`
   * **Maximum Parallel Jobs** - `<*x*>`（上で計算した値）

1. これらの変更を保存します。
1. Adobe CS6以降でマルチセッションのサポートを有効にするには、設定の下にあるチェ `enable.multisession.name` ックボックスをオンに `com.day.cq.dam.ids.impl.IDSJobProcessor.name` します。
1. [IDS ワーカー設定](#configuring-the-proxy-worker-for-indesign-server)に SOAP エンドポイントを追加して、`x` 個の IDS ワーカーから成るプールを作成します。

   If there are multiple machines running [!DNL InDesign Server], add SOAP endpoints (number of processors per machine -1) for each machine.

   >[!NOTE]
   >
   >ワーカーのプールを操作するときに、IDS ワーカーのブラックリスト設定を有効にすることもできます。
   >
   >
   >To do so, enable the **[!UICONTROL enable.retry.name]** checkbox, under the `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configuration, which enables IDS job retrials.
   >
   >
   >Also, under the `com.day.cq.dam.ids.impl.IDSPoolImpl.name` configuration, set a positive value for `max.errors.to.blacklist` parameter which determines number of job retrials before barring an IDS from the job handlers list.
   >
   >
   >デフォルトでは、設定可能な（retry.interval.to.whitelist.name）時間（分）が経過した後で、IDS ワーカーが再検証されます。ワーカーがオンラインである場合は、ブラックリストから削除されます。。

## 10.0以降のサ [!DNL InDesign Server] ポートを有効にする {#enabling-support-for-indesign-server-or-later}

For [!DNL InDesign Server] 10.0 or higher, perform the following steps to enable multi-session support.

1. Open Configuration Manager from your [!DNL Experience Manager Assets] instance `https://[aem_server]:[port]/system/console/configMgr`.
1. 設定 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` を編集します。
1. **[!UICONTROL ids.cc.enable]** オプションを選択し、「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>For [!DNL InDesign Server] integration with [!DNL Experience Manager Assets], use a multi-core processor because the Session Support feature necessary for the integration is not supported on single core systems.

## 資格情報の [!DNL Experience Manager] 設定 {#configure-aem-credentials}

You can change the default administrator credentials (user name and password) for accessing the [!DNL InDesign Server] from your [!DNL Experience Manager] instance without breaking the integration with the [!DNL InDesign Server].

1. `/etc/cloudservices/proxy.html` にアクセスします。
1. ダイアログで、新しいユーザー名とパスワードを指定します。
1. この資格情報を保存します。

>[!MORELIKETHIS]
>
>* [Adobe InDesign Serverについて](https://www.adobe.com/products/indesignserver/faq.html)

