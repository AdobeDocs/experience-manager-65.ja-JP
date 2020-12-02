---
title: ' [!DNL Assets] と [!DNL InDesign Server]を統合'
description: ' [!DNL Adobe Experience Manager Assets] を [!DNL Adobe InDesign Server]と統合する方法を学びます。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 117208c634613559bb13556e12f094add70006e2
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 31%

---


# [!DNL Adobe Experience Manager Assets]と[!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}を統合

[!DNL Adobe Experience Manager Assets] 使用する:

* プロキシ：特定の処理タスクのロードを分配するために使用します。プロキシは、特定のタスクを満たすためにプロキシワーカーと通信し、その他の[!DNL Experience Manager]インスタンスを使用して結果を配信する[!DNL Experience Manager]インスタンスです。
* プロキシワーカー：特定のタスクを定義し管理するために使用します。これらは様々なタスクをカバーできます。例えば、[!DNL InDesign Server]を使用してファイルを処理する場合などです。

[!DNL Adobe InDesign]で作成したファイルを[!DNL Experience Manager Assets]に完全にアップロードするには、プロキシが使用されます。 これは、プロキシワーカーを使用して[!DNL Adobe InDesign Server]との通信を行います。[スクリプト](https://www.adobe.com/jp/devnet/indesign/documentation.html#idscripting)は、メタデータを抽出して[!DNL Experience Manager Assets]の様々なレンディションを生成するために実行されます。 プロキシワーカーは、クラウド設定の[!DNL InDesign Server]インスタンスと[!DNL Experience Manager]インスタンス間の双方向通信を有効にします。

>[!NOTE]
>
>[!DNL Adobe InDesign] は、2つの異なるオファーとして提供されます。[印刷やデジタル配布](https://www.adobe.com/jp/products/indesign.html) 用のページレイアウトのデザインに使用するAdobeInDesignデスクトップアプリです。[Adobe InDesign](https://www.adobe.com/jp/products/indesignserver.html) サーバーでは、作成した内容に基づいて自動ドキュメントをプログラムで作成でき [!DNL InDesign]ます。[ExtendScript](https://www.adobe.com/jp/devnet/scripting.html)エンジンに対するインターフェイスを提供するサービスとして動作します。スクリプトは[!DNL ExtendScript]に記述され、[!DNL JavaScript]に似ています。 [!DNL InDesign]スクリプトについて詳しくは、[https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)を参照してください。

## 抽出の仕組み{#how-the-extraction-works}

[!DNL Adobe InDesign Server]を[!DNL Experience Manager Assets]と統合して、[!DNL InDesign]で作成されたINDDファイルをアップロード、生成されたレンディション、すべてのメディア（ビデオなど）を抽出し、アセットとして保存できます。

>[!NOTE]
>
>以前のバージョンの[!DNL Experience Manager]ではXMPとサムネールを抽出できましたが、すべてのメディアを抽出できます。

1. INDDファイルを[!DNL Experience Manager Assets]にアップロードします。
1. フレームワークは、SOAP(Simple Object Access Protocol)を介してコマンドスクリプトを[!DNL InDesign Server]に送信します。
このコマンドスクリプトは、次のことを実行します。

   * INDD ファイルを取得します。
   * [!DNL InDesign Server]コマンドを実行：

      * 構造、テキストおよびすべてのメディアファイルが抽出されます。
      * PDF と JPG のレンディションが生成されます。
      * HTML と IDML のレンディションが生成されます。
   * 結果のファイルを[!DNL Experience Manager Assets]にポストします。

   >[!NOTE]
   >
   >IDMLは、[!DNL InDesign]ファイルのすべての内容をレンダリングするXMLベースの形式です。 [ZIP](https://www.techterms.com/definition/zip)圧縮を使用して、圧縮パッケージとして保存されます。 詳しくは、[InDesign交換形式INXおよびIDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8)を参照してください。

   >[!CAUTION]
   >
   >[!DNL InDesign Server]がインストールされていないか設定されていない場合でも、[!DNL Experience Manager]にINDDファイルをアップロードできます。 ただし、この場合に生成されるレンディションは、PNG と JPEG に限定されます。HTML、IDML またはページのレンディションを生成することはできません。

1. 抽出およびレンダリング生成後：

   * 構造が `cq:Page`（レンディションタイプ）に複製されます。
   * 抽出されたテキストとファイルは[!DNL Experience Manager Assets]に保存されます。
   * すべてのレンディションは、アセット自体の[!DNL Experience Manager Assets]に保存されます。

## [!DNL InDesign Server]をExperience Manager{#integrating-the-indesign-server-with-aem}と統合する

[!DNL InDesign Server]を[!DNL Experience Manager Assets]で使用するように統合するには、プロキシを設定した後、次の操作を行う必要があります。

1. [InDesign Server をインストールします](#installing-the-indesign-server)。
1. 必要に応じて、[Experience Managerアセットワークフロー](#configuring-the-aem-assets-workflow)を設定します。
これは、デフォルト値がインスタンスに適さない場合にのみ必要です。
1. [InDesign Server のプロキシワーカー](#configuring-the-proxy-worker-for-indesign-server)を設定します。

### [!DNL InDesign Server] {#installing-the-indesign-server}をインストール

[!DNL Experience Manager]で使用する[!DNL InDesign Server]をインストールして開始するには：

1. [!DNL InDesign Server]をダウンロードしてインストールします。

1. 必要に応じて、[!DNL InDesign Server]インスタンスの設定をカスタマイズできます。

1. コマンドラインから、サーバーを起動します。

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   SOAP プラグインがポート 8080 でリスンする状態でサーバーが起動されます。すべてのログメッセージと出力がコマンドウィンドウに直接書き込まれます。

   >[!NOTE]
   >
   >ファイルに出力メッセージを保存してリダイレクトを使用する場合は、例えば Windows の場合は次のように実行します。
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### [!DNL Experience Manager Assets]ワークフロー{#configuring-the-aem-assets-workflow}を設定

[!DNL Experience Manager Assets] には、次の項目に特にいくつかのプロセス手順を持つ、事前設定済みのワークフロー **[!UICONTROL DAM更新アセット]**&#x200B;があり [!DNL InDesign]ます。

* [メディア抽出](#media-extraction)
* [ページ抽出](#page-extraction)

このワークフローは、様々なオーサーインスタンスで設定に適合できるデフォルト値で設定されます（これは標準的なワークフローです。詳しくは、「ワークフローの編集](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)」を参照してください）。 デフォルト値（SOAPポートを含む）を使用する場合は、設定は不要です。[

設定後、（通常の方法で）[!DNL InDesign]ファイルを[!DNL Experience Manager Assets]にアップロードすると、ワークフローがトリガーされ、アセットの処理と様々なレンディションの準備が行われます。 INDDファイルを[!DNL Experience Manager Assets]にアップロードして設定をテストし、`<*your_asset*>.indd/Renditions`の下にIDSで作成された様々なレンディションが表示されていることを確認します

#### メディア抽出{#media-extraction}

このステップでは、INDD ファイルからのメディアの抽出を制御します。

カスタマイズするには、**[!UICONTROL メディア抽出]**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![メディア抽出の引数とスクリプトパス](assets/media_extraction_arguments_scripts.png)

メディア抽出の引数とスクリプトパス

* **ExtendScript図書館**:これは、他のスクリプトで必要となる、単純なhttpのget/postメソッドライブラリです。

* **拡張スクリプト**:ここでは、異なるスクリプトの組み合わせを指定できます。独自のスクリプトを[!DNL InDesign Server]上で実行する場合は、`/apps/settings/dam/indesign/scripts`にスクリプトを保存します。

[!DNL Adobe InDesign]スクリプトについて詳しくは、[InDesign開発者向けドキュメント](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)を参照してください

>[!CAUTION]
>
>ExtendScript ライブラリは変更しないでください。このライブラリは Sling との通信に必要になる HTTP 機能を提供するものです。この設定は、[!DNL InDesign Server]に送信してそこで使用するライブラリを指定します。

メディア抽出のワークフロー手順で実行される`ThumbnailExport.jsx`スクリプトは、JPG形式のサムネールレンディションを生成します。 このレンディションは、[!DNL Experience Manager]に必要な静的レンディションを生成するために、サムネールを処理ワークフローステップで使用されます。

サムネールを処理ワークフローステップは、異なるサイズの静的レンディションを生成するように設定できます。デフォルト値は[!DNL Experience Manager Assets]インターフェイスで必要なので、削除しないでください。 最後に、「画像プレビューのレンディションを削除」ワークフローの手順で、JPGサムネールのレンディションが不要になったので削除されます。

#### ページ抽出{#page-extraction}

これにより、抽出された要素から[!DNL Experience Manager]ページが作成されます。 抽出ハンドラーが、レンディション（現時点では HTML または IDML）からデータを抽出するために使用されます。このデータを元に、PageBuilder を使用してページが作成されます。

カスタマイズするには、**[!UICONTROL ページ抽出]**&#x200B;ステップの「**[!UICONTROL 引数]**」タブを編集します。

![chlimage_1-96](assets/chlimage_1-289.png)

* **ページ抽出ハンドラ**:ポップアップリストから、使用するハンドラーを選択します。抽出ハンドラーは、関連する `RenditionPicker`（`ExtractionHandler` API を参照）によって選択された特定のレンディションに対して動作します。標準の[!DNL Experience Manager]インストールでは、次のようにします。
   * IDML書き出し抽出ハンドル：MediaExtract手順で生成された`IDML`レンディションを操作します。

* **ページ名**:結果のページに割り当てる名前を指定します。空白の場合、名前は「page」（「page」が既に存在する場合は派生）になります。

* **ページタイトル**:結果のページに割り当てるタイトルを指定します。

* **Page Root Path**:結果のページのルート位置へのパス。空白のままにすると、アセットのレンディションを保持するノードが使用されます。

* **ページテンプレート**:結果のページの生成時に使用するテンプレートです。

* **ページデザイン**:結果のページを生成するときに使用するページデザインです。

### [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}のプロキシワーカーを設定

>[!NOTE]
>
>ワーカーは、プロキシインスタンス上にあります。

1. 「ツール」コンソールの左側のウィンドウで、「**[!UICONTROL クラウドサービス設定]**」を展開します。次に、「**[!UICONTROL クラウドプロキシ設定]**」を展開します。

1. 「**[!UICONTROL IDS ワーカー]**」をダブルクリックし、開いて設定します。

1. 「**[!UICONTROL 編集]**」をクリックして設定ダイアログを開き、必要な設定を定義します。

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **IDS**
Pool SOAPエンドポイントは、との通信に使用され [!DNL InDesign Server]ます。アイテムの追加、削除、および注文は必須にすることができます。

1. 「OK」をクリックして保存します。

### Day CQ Link Externalizerの設定{#configuring-day-cq-link-externalizer}

[!DNL InDesign Server]と[!DNL Experience Manager]が異なるホスト上で実行される場合、またはこれらの両方のアプリケーションがデフォルトポートで実行されない場合は、[!UICONTROL Day CQ Link Externalizer]を設定して[!DNL InDesign Server]のホスト名、ポート、コンテンツパスを設定します。

1. `https://[aem_server]:[port]/system/console/configMgr`のWebコンソールにアクセスします。
1. 設定&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;を探し、**[!UICONTROL Edit]**&#x200B;をクリックして開きます。
1. [!DNL Adobe InDesign Server]のホスト名とコンテキストパスを指定し、「**保存**」をクリックします。

   ![chlimage_1-97](assets/chlimage_1-290.png)

### [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server-s}の並列ジョブ処理を有効にする

IDS の並列ジョブ処理を有効にすることができます。[!DNL InDesign Server]が処理できる並列ジョブ(`x`)の最大数を決定します。

* 1台のマルチプロセッサマシンで、[!DNL InDesign Server]が処理できる並列ジョブ(`x`)の最大数は、IDを実行しているプロセッサの数より1少ない。
* 複数のマシンで IDS を実行する場合は、すべてのマシンで使用可能なプロセッサーの総数を把握して、そこからマシン総数を減算する必要があります。

IDS 並列ジョブ数を設定するには：

1. Felix Console の「**[!UICONTROL Configurations]**」タブを開きます。次に URL の例を挙げます。`https://[aem_server]:[port]/system/console/configMgr`

1. `Apache Sling Job Queue Configuration`の下でIDS処理キューを選択します。

1. 次のように設定します。

   * **Type** - `Parallel`
   * **Maximum Parallel Jobs** - `<*x*>`（上で計算した値）

1. これらの変更を保存します。
1. AdobeCS6以降でマルチセッションのサポートを有効にするには、`com.day.cq.dam.ids.impl.IDSJobProcessor.name`設定の下にある`enable.multisession.name`チェックボックスをオンにします。
1. [IDS ワーカー設定](#configuring-the-proxy-worker-for-indesign-server)に SOAP エンドポイントを追加して、`x` 個の IDS ワーカーから成るプールを作成します。

   [!DNL InDesign Server]を実行する複数のマシンがある場合は、各マシンにSOAPエンドポイント（マシン1台あたりのプロセッサ数）を追加します。

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>ワーカーのプールを使用する場合、IDSワーカーのブロックリストを有効にできます。
>
>これを行うには、`com.day.cq.dam.ids.impl.IDSJobProcessor.name`設定の下の&#x200B;**[!UICONTROL enable.retry.name]**&#x200B;チェックボックスを有効にします。これにより、IDSジョブの再取得が有効になります。
>
>また、`com.day.cq.dam.ids.impl.IDSPoolImpl.name`設定で、`max.errors.to.blacklist`パラメーターに正の値を設定します。この値は、ジョブハンドラーリストからIDを禁止する前に、ジョブの取得回数を決定します。
>
>デフォルトでは、設定可能な(`retry.interval.to.whitelist.name`)時間（分単位）が経過すると、IDSワーカーが再検証されます。 ワーカーがオンラインである場合は、ブロックリストから削除されます。

## [!DNL InDesign Server] 10.0以降の{#enabling-support-for-indesign-server-or-later}のサポートを有効にする

[!DNL InDesign Server] 10.0以降の場合は、次の手順を実行してマルチセッションのサポートを有効にします。

1. [!DNL Experience Manager Assets]インスタンス`https://[aem_server]:[port]/system/console/configMgr`からConfiguration Managerを開きます。
1. 設定 `com.day.cq.dam.ids.impl.IDSJobProcessor.name` を編集します。
1. **[!UICONTROL ids.cc.enable]** オプションを選択し、「**[!UICONTROL 保存]**」をクリックします。

>[!NOTE]
>
>[!DNL InDesign Server]と[!DNL Experience Manager Assets]を統合する場合は、統合に必要なセッションサポート機能がシングルコアシステムではサポートされないので、マルチコアプロセッサを使用してください。

## [!DNL Experience Manager]資格情報を構成{#configure-aem-credentials}

[!DNL InDesign Server]との統合を中断することなく、[!DNL Experience Manager]デプロイメントから[!DNL InDesign Server]にアクセスするためのデフォルトの管理者資格情報（ユーザー名とパスワード）を変更できます。

1. `/etc/cloudservices/proxy.html` にアクセスします。
1. ダイアログで、新しいユーザー名とパスワードを指定します。
1. この資格情報を保存します。

>[!MORELIKETHIS]
>
>* [Adobe InDesign Serverについて](https://www.adobe.com/products/indesignserver/faq.html)

