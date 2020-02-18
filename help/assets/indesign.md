---
title: AEM AssetsとAdobe inDesign serverの統合
description: AEM AssetsをAdobe inDesign Serverと統合する方法を説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 07c1a4102539ba4678c55dee3a4882101e39864f

---


# AEM AssetsとAdobe inDesign serverの統合 {#integrating-aem-assets-with-indesign-server}

Adobe Experience Manager（AEM）Assets では、次のものが使用されます。

* プロキシ：特定の処理タスクのロードを分配するために使用します。プロキシとは、プロキシワーカーと通信して特定のタスクを実行し、他の AEM インスタンスと通信して結果を送信する AEM インスタンスです。
* プロキシワーカー：特定のタスクを定義し管理するために使用します。
これらは幅広いタスクを取り扱うことができます。例えば、InDesign Server を使用してファイルを処理することができます。

Adobe InDesign で作成したファイルを AEM Assets に完全にアップロードするために、プロキシが使用されます。このプロキシはプロキシワーカーを使用して Adobe InDesign Server と通信します。Adobe InDesign Server ではメタデータを抽出し、AEM Assets 用の様々なレンディションを生成するための[スクリプト](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)が実行されます。プロキシワーカーは、クラウド構成での InDesign Server と AEM インスタンスとの双方向通信を実現します。

>[!NOTE]
>
>Adobe InDesign は次の 2 製品で構成されます。
>
>* [InDesign](https://www.adobe.com/products/indesign.html)
   >  印刷やデジタル配信のためのページレイアウトをデザインできます。
   >
   >
* [InDesign Server](https://www.adobe.com/products/indesignserver.html)
   >  このエンジンを使用すれば、InDesign での作成物に基づいてドキュメントをプログラムによって自動生成できます。このエンジンは、[ExtendScript](https://www.adobe.com/devnet/scripting.html) エンジンへのインターフェイスを提供するサービスとして動作します。
   >  スクリプトはExtendScriptで記述されますが、これはjavascriptと同様です。 For information about InDesign scripts see [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).


## How the extraction works {#how-the-extraction-works}

Adobe inDesign serverをAEM Assetsと統合して、InDesignで作成したINDDファイルをアップロード、生成、すべてのメディア（ビデオなど）を抽出し、アセットとして保存できます。

>[!NOTE]
>
>以前のバージョンの AEM では XMP とサムネールを抽出できましたが、現在はすべてのメディアを抽出できるようになりました。

1. INDDファイルをAEM Assetsにアップロードします。
1. フレームワークにより、コマンドスクリプトが SOAP（Simple Object Access Protocol）経由で InDesign Server に送信されます。このコマンドスクリプトは、次のことを実行します。

   * INDDファイルを取得します。
   * InDesign Server コマンドを実行します。

      * 構造、テキストおよびすべてのメディアファイルが抽出されます。
      * PDF と JPG のレンディションが生成されます。
      * HTML と IDML のレンディションが生成されます。
   * 生成されたファイルを AEM Assets に送り返します。
   >[!NOTE]
   >
   >IDMLは、InDesignファイルのすべてのコンテンツをレンダリングするXMLベースの形式です。 It is stored as an compressed package using [ZIP](https://www.techterms.com/definition/zip) compression. 詳しくは、 [InDesign Interchange Formats INXおよびIDMLを参照してください](http://www.peachpit.com/articles/article.aspx?p=1381880&seqNum=8)。

   >[!CAUTION]
   >
   >InDesign serverがインストールされていないか設定されていない場合でも、INDDファイルをAEMにアップロードできます。 ただし、生成されるレンディションはPNGおよびJPEGに制限されます。HTML、.idmlまたはページレンディションを生成することはできません。

1. 抽出およびレンダリング生成後：

   * 構造が `cq:Page`（レンディションタイプ）に複製されます。
   * 抽出されたテキストとファイルが AEM Assets に保存されます。
   * すべてのレンディションが AEM Assets のアセット自体に保存されます。

## Integrate the InDesign Server with AEM {#integrating-the-indesign-server-with-aem}

InDesign serverをAEM Assetsと統合し、プロキシを設定した後で使用するには、次の操作を行う必要があります。

1. [InDesign Server をインストールします](#installing-the-indesign-server)。
1. 必要に応じて、[AEM Assets ワークフロー](#configuring-the-aem-assets-workflow)を設定します。これは、デフォルト値がインスタンスに適さない場合にのみ必要です。
1. [InDesign Server のプロキシワーカー](#configuring-the-proxy-worker-for-indesign-server)を設定します。

### Install the InDesign Server {#installing-the-indesign-server}

InDesign Server をインストールして AEM と連携して使用を開始するには：

1. Adobe InDesign Server をダウンロードしてインストールします。

1. 必要に応じて、InDesign Server インスタンスの設定をカスタマイズできます。

1. コマンドラインから、サーバーを起動します。

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   SOAP プラグインがポート 8080 でリスンする状態でサーバーが起動されます。すべてのログメッセージと出力がコマンドウィンドウに直接書き込まれます。

   >[!NOTE]
   >
   >ファイルに出力メッセージを保存してリダイレクトを使用する場合は、例えば Windows の場合は次のように実行します。
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configure the AEM Assets workflow {#configuring-the-aem-assets-workflow}

AEM Assets has a pre-configured workflow **[!UICONTROL DAM Update Asset]**, that has several process steps specifically for InDesign:

* [メディア抽出](#media-extraction)
* [ページ抽出](#page-extraction)

This workflow is setup with default values that can be adapted for your setup on the various author instances (this is a standard workflow, so further information is available under [Editing a Workflow](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). If you are using the default values (including the SOAP port), then no configuration is needed.

設定後、通常の方法のいずれかによって InDesign ファイルを AEM Assets にアップロードすると、そのアセットを処理して各種レンディションを準備するのに必要となるワークフローが実行されます。Test your configuration by uploading an INDD file into AEM Assets to confirm that you see the different renditions created by IDS under `<*your_asset*>.indd/Renditions`

#### Media extraction {#media-extraction}

この手順では、INDDファイルからのメディアの抽出を制御します。

カスタマイズするには、**[!UICONTROL メディア抽出]**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![メディア抽出の引数とスクリプトパス](assets/media_extraction_arguments_scripts.png)

メディア抽出の引数とスクリプトパス

* **ExtendScriptライブラリ**:これは、他のスクリプトで必要とされる、単純なhttpのget/postメソッドライブラリです。

* **スクリプトの拡張**:ここでは、異なるスクリプトの組み合わせを指定できます。 If you want your own scripts to be executed on the InDesign Server, save the scripts at `/apps/settings/dam/indesign/scripts`.

Indesignスクリプトについて詳しくは、 [InDesign開発者向けドキュメントを参照してください](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>ExtendScript ライブラリは変更しないでください。このライブラリは Sling との通信に必要になる HTTP 機能を提供するものです。この設定では、InDesign Server で使用するために送信するライブラリを指定します。

メディア抽出ワークフローステップで実行される `ThumbnailExport.jsx` スクリプトにより、サムネールのレンディションを .jpg 形式で生成します。このレンディションは、プロセスサムネールワークフローステップで、AEMに必要な静的レンディションを生成するために使用されます。

サムネールを処理ワークフローステップは、異なるサイズの静的レンディションを生成するように設定できます。デフォルトの設定は AEM Assets UI によって要求されるので、削除しないでください。最後に、画像プレビューレンディションを削除ワークフローステップで不要になった .jpg 形式のサムネールレンディションが削除されます。

#### Page extraction {#page-extraction}

抽出された要素から AEM ページを作成します。抽出ハンドラーが、レンディション（現時点では HTML または IDML）からデータを抽出するために使用されます。このデータを元に、PageBuilder を使用してページが作成されます。

カスタマイズするには、**[!UICONTROL ページ抽出]**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![chlimage_1-96](assets/chlimage_1-289.png)

* **ページ抽出ハンドラ**:ポップアップリストから、使用するハンドラーを選択します。 抽出ハンドラーは、関連する `RenditionPicker`（`ExtractionHandler` API を参照）によって選択された特定のレンディションに対して動作します。標準の AEM インストールでは、次の抽出ハンドラーを使用できます。
   * IDML Export Extraction Handle: Operates on the `IDML` rendition generated in the MediaExtract step.

* **ページ名**:結果のページに割り当てる名前を指定します。空白の場合、名前は「page」（「page」が既に存在する場合は派生）になります。

* **ページタイトル**:結果のページに割り当てるタイトルを指定します。

* **Page Root Path**:結果のページのルート位置へのパス。空白のままにすると、アセットのレンディションを保持するノードが使用されます。

* **ページテンプレート**:結果ページの生成時に使用するテンプレートです。

* **ページデザイン**:結果のページの生成時に使用するページデザインです。

### Configure the proxy worker for InDesign Server {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>ワーカーは、プロキシインスタンス上にあります。

1. 「ツール」コンソールの左側のウィンドウで、「**[!UICONTROL クラウドサービス設定]**」を展開します。次に、「**[!UICONTROL クラウドプロキシ設定]**」を展開します。

1. 「**[!UICONTROL IDS ワーカー]**」をダブルクリックして設定用に開きます。

1. 「**[!UICONTROL 編集]**」をクリックして設定ダイアログを開き、必要な設定を定義します。

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS プール**
InDesign Server との通信に使用する SOAP エンドポイント。必要になる項目の追加、削除および並べ替えを行うことができます。

1. 「OK」をクリックして保存します。

### Configure Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

InDesign Server と AEM が別のホストで実行されている、またはどちらかまた両方のアプリケーションがデフォルトのポートで実行されていない場合は、[!UICONTROL Day CQ Link Externalizer] で InDesign Server のホスト名、ポートおよびコンテンツを設定します。

1. Access the Web Console at `https://[aem_server]:[port]/system/console/configMgr`.
1. Locate the configuration **[!UICONTROL Day CQ Link Externalizer]**, and tap **[!UICONTROL Edit]** to open it.
1. InDesign Server のホスト名とコンテンツパスを指定し、「**Save**」をクリックします。

   ![chlimage_1-97](assets/chlimage_1-290.png)

### InDesignサーバーの並列ジョブ処理の有効化 {#enabling-parallel-job-processing-for-indesign-server-s}

IDS の並列ジョブ処理を有効にすることができます。InDesign Serverが処理できる並列ジョブの最大`x`数を決定します。

* On a single multiprocessor machine, the maximum number of parallel jobs (`x`) that an InDesign Server can process is one less than the number of processors running IDS.
* 複数のマシンで IDS を実行する場合は、すべてのマシンで使用可能なプロセッサーの総数を把握して、そこからマシン総数を減算する必要があります。

IDS 並列ジョブ数を設定するには：

1. Felix Console の「**[!UICONTROL Configurations]**」タブを開きます。次に URL の例を挙げます。 `https://[aem_server]:[port]/system/console/configMgr`.

1. Select the IDS processing queue under `Apache Sling Job Queue Configuration`.

1. 次のように設定します。

   * **タイプ** - `Parallel`
   * **最大並列ジョブ** - `<*x*>` （上述の計算結果）

1. これらの変更を保存します。
1. Adobe CS6以降でマルチセッションサポートを有効にするには、設定の下のチェ `enable.multisession.name` ックボックスをオンに `com.day.cq.dam.ids.impl.IDSJobProcessor.name` します。
1. Create a [pool of `x` IDS workers by adding SOAP endpoints to the IDS Worker configuration](#configuring-the-proxy-worker-for-indesign-server).

   複数のマシンで InDesign Server を実行している場合は、マシンあたりのプロセッサー数から 1 を減算した数の SOAP エンドポイントを各マシンに追加します。

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

## InDesign Server 10.0以降のサポートの有効化 {#enabling-support-for-indesign-server-or-later}

InDesign Server 10.0 以降では、次の手順を実行してマルチセッションサポートを有効化します。

1. Open Configuration Manager from your AEM Assets instance `https://[aem_server]:[port]/system/console/configMgr`.
1. Edit the configuration `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Select the **[!UICONTROL ids.cc.enable]** option, and click **[!UICONTROL Save]**.

>[!NOTE]
>
>AEM Assets に InDesign Server を統合する場合、統合に必要なセッションサポート機能はシングルコアのシステムではサポートされていないので、マルチコアのプロセッサーを使用してください。

## AEM 資格情報の設定 {#configure-aem-credentials}

InDesignサーバーとの統合を中断することなく、AEMインスタンスからInDesignサーバーにアクセスするためのデフォルトの管理者資格情報（ユーザー名とパスワード）を変更できます。

1. 移動 `/etc/cloudservices/proxy.html`.
1. ダイアログで、新しいユーザー名とパスワードを指定します。
1. この資格情報を保存します。

>[!MORELIKETHIS]
>
>* [Adobe inDesign Serverについて](https://www.adobe.com/products/indesignserver/faq.html)

