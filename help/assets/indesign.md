---
title: ' [!DNL Assets]  と  [!DNL InDesign Server] の統合'
description: ' [!DNL Adobe Experience Manager Assets] と [!DNL Adobe InDesign Server] を統合する方法について説明します。'
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager Assets] と [!DNL Adobe InDesign Server] の統合 {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] 使用する:

* プロキシ：特定の処理タスクのロードを分配するために使用します。プロキシとは、プロキシワーカーと通信して特定のタスクを実行し、他の [!DNL Experience Manager] インスタンスと通信して結果を送信する [!DNL Experience Manager] インスタンスです。
* プロキシワーカー：特定のタスクを定義し管理するために使用します。これらは幅広いタスクを取り扱うことができます。例えば、[!DNL InDesign Server] を使用してファイルを処理することができます。

[!DNL Adobe InDesign] で作成したファイルを [!DNL Experience Manager Assets] に完全にアップロードするために、プロキシが使用されます。このプロキシはプロキシワーカーを使用して [!DNL Adobe InDesign Server] と通信します。そこでは、メタデータを抽出して [!DNL Experience Manager Assets] 用の様々なレンディションを生成するための[スクリプト](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)が実行されます。プロキシワーカーは、クラウド設定における [!DNL InDesign Server] インスタンスと [!DNL Experience Manager] インスタンスとの双方向通信を実現します。

>[!NOTE]
>
>[!DNL Adobe InDesign] は、2 つの異なる製品として提供されます。[Adobe InDesign](https://www.adobe.com/jp/products/indesign.html) は、印刷およびデジタル配布用のページレイアウトのデザインに使用するデスクトップアプリケーションです。[Adobe InDesign Server](https://www.adobe.com/jp/products/indesignserver.html) は、[!DNL InDesign] で作成した内容に基づいて、ドキュメントをプログラムによって自動生成できるようにします。これは、[ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) エンジンへのインターフェイスを提供するサービスとして動作します。スクリプトは、[!DNL JavaScript] に似た [!DNL ExtendScript]で記述されます。[!DNL InDesign] のスクリプトについて詳しくは、[https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) を参照してください。

## 抽出の仕組み {#how-the-extraction-works}

 [!DNL Adobe InDesign Server] と [!DNL Experience Manager Assets] を統合すると、[!DNL InDesign] で作成された INDD ファイルのアップロードやレンディションの生成のほか、すべてのメディアを抽出（ビデオなど）したり、アセットとして保存したりできます。

>[!NOTE]
>
>以前のバージョンの [!DNL Experience Manager] では XMP とサムネールを抽出できましたが、現在はすべてのメディアを抽出できるようになりました。

1. INDD ファイルを [!DNL Experience Manager Assets] にアップロードします。
1. フレームワークにより、コマンドスクリプトが SOAP（Simple Object Access Protocol）経由で [!DNL InDesign Server] に送信されます。
このコマンドスクリプトは、次のことを実行します。

   * INDD ファイルを取得します。
   * 次の [!DNL InDesign Server] コマンドを実行します。

      * 構造、テキストおよびすべてのメディアファイルが抽出されます。
      * PDF と JPG のレンディションが生成されます。
      * HTML と IDML のレンディションが生成されます。
   * 生成されたファイルを [!DNL Experience Manager Assets] に送り返します。

   >[!NOTE]
   >
   >IDML は、 [!DNL InDesign] ファイルのすべてのコンテンツをレンダリングする XML ベースの形式です。[ZIP](https://www.techterms.com/definition/zip) 圧縮を使用した圧縮パッケージとして保存されます。詳しくは、 [InDesign の交換形式 INX および IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8) を参照してください。

   >[!CAUTION]
   >
   >[!DNL InDesign Server] をインストールしていない場合や設定していない場合でも、INDD ファイルを [!DNL Experience Manager] にアップロードすることができます。ただし、この場合に生成されるレンディションは、PNG と JPEG に限定されます。HTML、IDML またはページのレンディションを生成することはできません。

1. 抽出およびレンダリング生成後：

   * 構造が `cq:Page`（レンディションタイプ）に複製されます。
   * 抽出されたテキストとファイルが [!DNL Experience Manager Assets] に保存されます。
   * すべてのレンダリングが [!DNL Experience Manager Assets] のアセット自体に保存されます。

## [!DNL InDesign Server] と Experience Manager の統合 {#integrating-the-indesign-server-with-aem}

プロキシを設定した後で、[!DNL Experience Manager Assets] で使用するために [!DNL InDesign Server] を統合するには 、次の手順を実行する必要があります。

1. [InDesign Server をインストールします](#installing-the-indesign-server)。
1. 必要に応じて、[Experience Manager アセットのワークフロー](#configuring-the-aem-assets-workflow) を設定します。
これは、デフォルト値がインスタンスに適さない場合にのみ必要です。
1. [InDesign Server のプロキシワーカー](#configuring-the-proxy-worker-for-indesign-server)を設定します。

### [!DNL InDesign Server] のインストール {#installing-the-indesign-server}

[!DNL InDesign Server] をインストールして [!DNL Experience Manager] と連携して使用を開始するには：

1. [!DNL InDesign Server] をダウンロードしてインストールします。

1. 必要に応じて、 [!DNL InDesign Server] インスタンスの設定をカスタマイズできます。

1. コマンドラインから、サーバーを起動します。

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   SOAP プラグインがポート 8080 でリスンする状態でサーバーが起動されます。すべてのログメッセージと出力がコマンドウィンドウに直接書き込まれます。

   >[!NOTE]
   >
   >ファイルに出力メッセージを保存してリダイレクトを使用する場合は、例えば Windows の場合は次のように実行します。
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### [!DNL Experience Manager Assets] ワークフローの設定 {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] には事前設定済みの **[!UICONTROL DAM アセットの更新]**&#x200B;というワークフローがあります。このプロセスには、[!DNL InDesign] 向けの次のプロセス手順が含まれています。

* [メディア抽出](#media-extraction)
* [ページ抽出](#page-extraction)

このワークフローには、様々な作成者インスタンス上の設定に合わせて変更できるデフォルト値が設定されています（これは標準ワークフローであり、詳しい情報は[ワークフローの編集](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)に記載されています）。デフォルト値（SOAP ポートを含む）を使用する場合は、設定は不要です。

設定後、通常のいずれかの方法で [!DNL InDesign] ファイルを [!DNL Experience Manager Assets] にアップロードすると、そのアセットを処理して各種レンダリングを準備するワークフローがトリガーされます。INDD ファイルを [!DNL Experience Manager Assets] にアップロードし、IDS で作成された各種レンディションが `<*your_asset*>.indd/Renditions` の下にあることを確認して、設定をテストします。

#### メディア抽出 {#media-extraction}

このステップでは、INDD ファイルからのメディアの抽出を制御します。

カスタマイズするには、**[!UICONTROL メディア抽出]**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![メディア抽出の引数とスクリプトパス](assets/media_extraction_arguments_scripts.png)

メディア抽出の引数とスクリプトパス

* **ExtendScript ライブラリ**：他のスクリプトに必要とされる単純な http get/post メソッドライブラリです。

* **スクリプトを拡張**：ここで複数のスクリプトの組み合わせを指定できます。[!DNL InDesign Server] で独自のスクリプトを実行する場合は、 `/apps/settings/dam/indesign/scripts` にスクリプトを保存します。

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>ExtendScript ライブラリは変更しないでください。このライブラリは Sling との通信に必要になる HTTP 機能を提供するものです。この設定では、[!DNL InDesign Server] で使用するために送信するライブラリを指定します。

メディア抽出ワークフロー手順で実行される `ThumbnailExport.jsx` スクリプトにより、サムネールのレンディションを JPG 形式で生成します。このレンディションはサムネール処理ワークフロー手順で使用され、[!DNL Experience Manager] で要求される静的レンディションを生成します。

サムネールを処理ワークフローステップは、異なるサイズの静的レンディションを生成するように設定できます。デフォルトの設定は、[!DNL Experience Manager Assets] で必要となるため、削除しないでください。最後に、画像プレビューレンディションを削除ワークフロー手順で不要になった .JPG 形式のサムネールレンディションが削除されます。

#### ページ抽出 {#page-extraction}

抽出された要素から [!DNL Experience Manager] ページを作成します。抽出ハンドラーが、レンディション（現時点では HTML または IDML）からデータを抽出するために使用されます。このデータを元に、PageBuilder を使用してページが作成されます。

カスタマイズするには、**[!UICONTROL ページ抽出]**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![chlimage_1-96](assets/chlimage_1-289.png)

* **ページ抽出ハンドラー**：ポップアップリストから、使用するハンドラーを選択します。抽出ハンドラーは、関連する `RenditionPicker`（`ExtractionHandler` API を参照）によって選択された特定のレンディションに対して動作します。標準の [!DNL Experience Manager] インストールでは、次の抽出ハンドラーを使用できます。
   * IDML 書き出し抽出ハンドラー：MediaExtract ステップで生成された `IDML` レンディションに対して動作します。

* **ページ名**：生成されるページに割り当てる名前を指定します。空白にした場合、名前は「page」（「page」が既に存在する場合は、その派生形）になります。

* **ページタイトル**：生成されるページに割り当てるタイトルを指定します。

* **ページルートのパス**：生成されるページのルート位置を示すパス。空白にした場合、アセットのレンディションを保持しているノードが使用されます。

* **ページテンプレート**：ページの生成時に使用するテンプレート。

* **ページデザイン**：ページの生成時に使用するページデザイン。

### [!DNL InDesign Server] のプロキシワーカーを設定 {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>ワーカーは、プロキシインスタンス上にあります。

1. 「ツール」コンソールの左側のウィンドウで、「**[!UICONTROL クラウドサービス設定]**」を展開します。次に、「**[!UICONTROL クラウドプロキシ設定]**」を展開します。

1. 「**[!UICONTROL IDS ワーカー]**」をダブルクリックし、開いて設定します。

1. 「**[!UICONTROL 編集]**」をクリックして設定ダイアログを開き、必要な設定を定義します。

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS プール**
[!DNL InDesign Server] との通信に使用する SOAP エンドポイント。必要になる項目の追加、削除および並べ替えを行うことができます。

1. 「OK」をクリックして保存します。

### Day CQ Link Externalizer を設定 {#configuring-day-cq-link-externalizer}

 [!DNL InDesign Server] と [!DNL Experience Manager] が異なるホスト上にある場合、またはこれらのアプリケーションの一方または両方がデフォルトのポートで動作していない場合は、[!UICONTROL Day CQ Link Externalizer] で [!DNL InDesign Server] のホスト名、ポート、コンテンツパスを設定します。

1. `https://[aem_server]:[port]/system/console/configMgr` で web コンソールにアクセスします。
1. **[!UICONTROL Day CQ Link Externalizer]** の設定を探します。「**[!UICONTROL 編集]**」をクリックして開きます。
1. Link Externalizer の設定は、[!DNL Experience Manager] デプロイメントと [!DNL InDesign Server] の 絶対 URL を作成するのに役立ちます。「**[!UICONTROL ドメイン]**」フィールドを使用して、[!DNL Adobe InDesign Server] のホスト名を指定します。「**保存**」をクリックします。

   絶対 URL では、次の図のように、`localhost` をローカル（オーサー）インスタンスのホスト名、およびパブリッシュインスタンスのホスト名または IP アドレスとして使用します。

   ![Link Externalizer の設定](assets/link-externalizer-config.png)

### [!DNL InDesign Server] の並列ジョブ処理を有効にする {#enabling-parallel-job-processing-for-indesign-server}

IDS の並列ジョブ処理を有効にすることができます。[!DNL InDesign Server] が処理できる並列ジョブの最大数（`x`）を決定します。

* 単一のマルチプロセッサーマシンでは、[!DNL InDesign Server] が処理できる並列ジョブの最大数（`x`）は、IDS を実行するプロセッサー数から 1 を減算した数です。
* 複数のマシンで IDS を実行する場合は、すべてのマシンで使用可能なプロセッサーの総数を把握して、そこからマシン総数を減算する必要があります。

IDS 並列ジョブ数を設定するには：

1. Felix Console の「**[!UICONTROL Configurations]**」タブを開きます。次に URL の例を挙げます。`https://[aem_server]:[port]/system/console/configMgr` です。

1. `Apache Sling Job Queue Configuration` で IDS 処理キューを選択します。

1. 次のように設定します。

   * **Type** - `Parallel`
   * **Maximum Parallel Jobs** - `<*x*>`（上で計算した値）

1. これらの変更を保存します。
1. Adobe CS6 以降のマルチセッションサポートを有効にするには、`com.day.cq.dam.ids.impl.IDSJobProcessor.name` 設定の「`enable.multisession.name`」チェックボックスをオンにします。
1. [IDS ワーカー設定](#configuring-the-proxy-worker-for-indesign-server)に SOAP エンドポイントを追加して、`x` 個の IDS ワーカーから成るプールを作成します。

   複数のマシンで [!DNL InDesign Server] を実行している場合は、マシンあたりのプロセッサー数から 1 を減算した数の SOAP エンドポイントを各マシンに追加します。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>ワーカーのプールを使用する場合、IDS ワーカーのブロックリストを有効にできます。
>
>その場合は、`com.day.cq.dam.ids.impl.IDSJobProcessor.name` 設定の下にある「**[!UICONTROL enable.retry.name]**」チェックボックスをオンにします。これにより、IDS ジョブの再試行が可能になります。
>
>また、`com.day.cq.dam.ids.impl.IDSPoolImpl.name` 設定で、`max.errors.to.blacklist` パラメーターに正の値を設定します。このパラメーターでは、IDS をジョブハンドラーリストから除外するまでのジョブ再試行回数を指定します。
>
>デフォルトでは、設定可能な（`retry.interval.to.whitelist.name`）時間（分単位）が経過した後で、IDS ワーカーが再検証されます。ワーカーがオンラインである場合は、ブロックリストから削除されます。

## [!DNL InDesign Server] 10.0 以降のサポートを有効にする {#enabling-support-for-indesign-server-or-later}

[!DNL InDesign Server] 10.0 以降では、次の手順を実行してマルチセッションサポートを有効にします。

1. [!DNL Experience Manager Assets] インスタンス `https://[aem_server]:[port]/system/console/configMgr` から Configuration Manager を開きます。
1. 設定 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` を編集します。
1. **[!UICONTROL ids.cc.enable]** オプションを選択し、「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>[!DNL Experience Manager Assets] に [!DNL InDesign Server] を統合する場合、統合に必要なセッションサポート機能はシングルコアのシステムではサポートされていないので、マルチコアのプロセッサーを使用してください。

## [!DNL Experience Manager] 資格情報を設定 {#configure-aem-credentials}

[!DNL Experience Manager] デプロイメントから [!DNL InDesign Server] にアクセスするためのデフォルトの管理者資格情報（ユーザー名とパスワード）を、[!DNL InDesign Server] との統合を中断することなく、変更できます。

1. `/etc/cloudservices/proxy.html` にアクセスします。
1. ダイアログで、新しいユーザー名とパスワードを指定します。
1. この資格情報を保存します。

>[!MORELIKETHIS]
>
>* [Adobe InDesign Server について](https://www.adobe.com/jp/products/indesignserver/faq.html)

