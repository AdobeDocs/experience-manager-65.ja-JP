---
title: Dynamic Media - Scene7モードの設定
description: Dynamic Media - Scene7モードの設定方法を説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 4
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configuration,Scene7 Mode
source-git-commit: 2706a069bea731da1f84c15e2da02b53a9db4d28
workflow-type: tm+mt
source-wordcount: '6035'
ht-degree: 44%

---

# Dynamic Media - Scene7モードの設定{#configuring-dynamic-media-scene-mode}

開発、ステージング、実稼動など、異なる環境用にAdobe Experience Managerを設定して使用する場合は、それらの環境のそれぞれにDynamic MediaCloud Servicesを設定します。

## Dynamic Media - Scene7 モードのアーキテクチャ図 {#architecture-diagram-of-dynamic-media-scene-mode}

以下のアーキテクチャ図に Dynamic Media - Scene7 モードの仕組みを示します。

新しいアーキテクチャでは、Experience Managerはプライマリソースアセットを担当し、Dynamic Mediaと同期してアセットの処理と公開をおこないます。

1. プライマリソースアセットがExperience Managerにアップロードされると、Dynamic Mediaにレプリケートされます。 その時点で、Dynamic Media は、ビデオエンコーディングおよび画像の動的バリアントなど、すべてのアセットの処理とレンディションの生成を扱います。(Dynamic Media - Scene7モードでは、デフォルトのアップロードファイルサイズは 2 GB 以下です。 アップロードファイルのサイズを 2 GB まで 15 GB にするには、 [（オプション）2 GB を超えるアセットのアップロードに対するDynamic Media - Scene7モードの設定](#optional-config-dms7-assets-larger-than-2gb).)
1. レンディションが生成されると、Experience Managerは、リモートのDynamic Mediaレンディションに安全にアクセスし、プレビューできます ( バイナリはExperience Managerインスタンスに送り返されません )。
1. コンテンツを公開および承認する準備が整ったら、Dynamic Mediaサービスがコンテンツを配信サーバーにプッシュして CDN（コンテンツ配信ネットワーク）でコンテンツをキャッシュするようトリガーします。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>次の機能のリストでは、Adobe Experience Manager - Dynamic Mediaに組み込まれている標準搭載の CDN を使用する必要があります。 他のカスタム CDN は、これらの機能ではサポートされません。
>
>* [スマートイメージング](/help/assets/imaging-faq.md)
>* [キャッシュの無効化](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [ホットリンクの保護](/help/assets/hotlink-protection.md)
>* [コンテンツの HTTP/2 配信](/help/assets/http2.md)
>* CDN レベルでの URL リダイレクト
>* Akamai ChinaCDN（中国での最適な配信用）


## Scene7モードでのDynamic Mediaの有効化 {#enabling-dynamic-media-in-scene-mode}

[Dynamic Media はデフォルトで無効になっています。](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)Dynamic Mediaの機能を活用するには、有効にする必要があります。

>[!WARNING]
>
>Dynamic Media - Scene7モードは *Experience Managerオーサーインスタンスのみ*. そのため、 `runmode=dynamicmedia_scene7` Experience Managerオーサーインスタンスで、 *not* Experience Managerパブリッシュインスタンス

Dynamic Mediaを有効にするには、次を使用してExperience Managerを起動します。 `dynamicmedia_scene7` ターミナルウィンドウで次のように入力して、コマンドラインから実行モードを指定します（使用するポートの例は 4502）。

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## （オプション）Dynamic Mediaのプリセットと設定を 6.3 から 6.5 にダウンタイムなしで移行 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Experience ManagerDynamic Mediaを 6.3 から 6.4 または 6.5 にアップグレードする際に、ダウンタイムなしのデプロイメントを実行できるようになりました。 すべてのプリセットと設定を次の場所から移行するには： `/etc` から `/conf` CRXDE Liteでは、次の curl コマンドを必ず実行してください。

>[!NOTE]
>
>Experience Managerインスタンスを互換モードで実行する場合（つまり、互換性パッケージがインストールされている場合）、これらのコマンドを実行する必要はありません。

互換性パッケージの有無にかかわらず、すべてのアップグレードについて、次の Linux® curl コマンドを実行して、Dynamic Mediaに付属しているデフォルトの標準提供ビューアプリセットをコピーできます。

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

作成したカスタムビューアプリセットと設定を移行するには `/etc` から `/conf`、次の Linux® curl コマンドを実行します。

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 一括アセット移行用の機能パック18912をインストールする {#installing-feature-pack-for-bulk-asset-migration}

機能パック18912のインストールは次のとおりです。 *オプション*.

機能パック18912では、FTP を使用してアセットを一括取り込むことも、Experience Manager時にDynamic Media — ハイブリッドモードまたはDynamic Media ClassicからDynamic Media - Scene7モードにアセットを移行することもできます。 次の場所から利用できます。 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

詳しくは、 [一括アセット移行用の機能パック18912をインストールする](/help/assets/bulk-ingest-migrate.md) を参照してください。

## Cloud Services での Dynamic Media 設定の作成 {#configuring-dynamic-media-cloud-services}

**Dynamic Mediaを設定する前に** - Dynamic Media資格情報を含むプロビジョニング電子メールを受け取ったら、 [Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)をクリックし、アカウントにサインインしてパスワードを変更します。 プロビジョニング電子メールで提供されたパスワードは、システムが生成したもので、一時的なパスワードです。Dynamic Media Cloud Service が正しい資格情報で設定されるように、パスワードを更新することが重要です。

![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**Cloud ServicesでDynamic Media設定を作成するには：**

1. Experience Manager作成モードで、Experience Managerロゴを選択してグローバルナビゲーションコンソールにアクセスし、ツールアイコンを選択して、 **[!UICONTROL Cloud Services]** > **[!UICONTROL Dynamic Media Configuration]**.
1. Dynamic Media Configuration Browser ページの左側のペインで、を選択します。 **[!UICONTROL global]** ( 左側のフォルダーアイコンを選択しないでください。 **[!UICONTROL global]**) を選択し、「 **[!UICONTROL 作成]**.
1. **[!UICONTROL Dynamic Media 設定を作成]**&#x200B;ページで、タイトル、Dynamic Media アカウントの電子メールアドレス、パスワードを入力し、地域を選択します。この情報は、プロビジョニングの電子メールでアドビから提供されます。電子メールが届かない場合は、Adobeカスタマーサポートにお問い合わせください。

   「**[!UICONTROL Dynamic Media に接続]**」をクリックします。

   >[!NOTE]
   Dynamic Media資格情報を含むプロビジョニング電子メールを受け取ったら、 [Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)をクリックし、アカウントにサインインしてパスワードを変更します。 プロビジョニング電子メールで提供されたパスワードは、システムが生成したもので、一時的なパスワードです。Dynamic Media Cloud Service が正しい資格情報で設定されるように、パスワードを更新することが重要です。

1. 接続に成功したら、次のように設定します。 アスタリスク (*) を含む見出しは必須です。

   * **[!UICONTROL 会社]** - Dynamic Media アカウントの名前です。複数のDynamic Mediaアカウントがある。 例えば、異なるサブブランド、事業部、ステージングまたは実稼動環境を持つことができます。

   <!-- UNHIDE FEBRUARY 24, 2022 See also [Configure Dynamic Media company alias account](/help/assets/dm-alias-account.md). -->

   * **[!UICONTROL 会社のルートフォルダーのパス]**

   * **[!UICONTROL アセットの公開]** - 次の 3 つのオプションから選択できます。
      * **[!UICONTROL 即時公開]**&#x200B;とは、アセットがアップロードされると、システムがアセットを取り込み、URL／埋め込みをすぐに提供することを意味します。アセットを公開するためにユーザーが操作する必要はありません。
      * **[!UICONTROL アクティベーション時]** とは、URL/埋め込みリンクが提供される前に、最初にアセットを明示的に公開する必要があることを意味します。<br><!-- CQDOC-17478, Added March 9, 2021-->Experience Manager6.5.8 以降では、Experience Managerパブリッシュインスタンスは、次のような正確なDynamic Mediaメタデータ値を反映します。 `dam:scene7Domain` および `dam:scene7FileStatus` in **[!UICONTROL アクティベーション時]** 公開モードのみ。 この機能を有効にするには、Service Pack 8 をインストールしてから、Experience Managerを再起動します。 Sling Config Manager に移動します。 の設定を検索 `Scene7ActivationJobConsumer Component` または新しく作成 )。 チェックボックスを選択します。 **[!UICONTROL Dynamic Mediaの公開後にメタデータをレプリケート]**&#x200B;を選択し、「 **[!UICONTROL 保存]**.

         ![「 Dynamic Mediaの公開後にメタデータをレプリケート」チェックボックス](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL 選択的公開]** このオプションを使用すると、Dynamic Mediaに公開するフォルダーを制御できます。 スマート切り抜きや動的レンディションなどの機能を使用したり、プレビュー用にExperience Managerでのみ公開するフォルダーを指定したりできます。 同じ資産が *not* Dynamic Mediaで公開され、パブリックドメインで配信されます。<br>このオプションは、 **[!UICONTROL Dynamic Media Cloud Configuration]** または、必要に応じて、このオプションをフォルダーレベルで、フォルダーの **[!UICONTROL プロパティ]**.<br>詳しくは、[Dynamic Media での選択的公開の操作](/help/assets/selective-publishing.md)を参照してください。<br>この設定を後で変更した場合、または後でフォルダーレベルで変更した場合、その変更の影響を受けるのは、その時点からアップロードする新しいアセットだけです。 フォルダー内の既存のアセットの公開状態は、**[!UICONTROL クイック公開]**&#x200B;または&#x200B;**[!UICONTROL 公開を管理]**&#x200B;ダイアログボックスから手動で変更するまで、そのままになります。
   * **[!UICONTROL プレビューサーバーを保護]** - セキュアなレンディションプレビューサーバーへの URL パスを指定できます。つまり、レンディションが生成されると、Experience Managerは、リモートのDynamic Mediaレンディションに安全にアクセスし、プレビューできます ( バイナリはExperience Managerインスタンスに送り返されません )。
自社のサーバーまたは特別なサーバーを使用する特別な取り決めがない限り、アドビでは、この設定を指定されたとおりにしておくことをお勧めします。

   * **[!UICONTROL すべてのコンテンツを同期]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->デフォルトで選択されています。 Dynamic Media との同期で、アセットを選択して含めるまたは除外する場合は、このオプションの選択を解除します。このオプションの選択を解除すると、次の 2 つの Dynamic Media 同期モードから選択できるようになります。

   * **[!UICONTROL Dynamic Media 同期モード]**
      * **[!UICONTROL デフォルトで有効]** - フォルダーを特別に除外するようにマークしない限り、設定はすべてのフォルダーにデフォルトで適用されます。<!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL デフォルトで無効]** - 選択したフォルダーを Dynamic Media と同期するように明示的にマークしない限り、設定はどのフォルダーにも適用されません。
選択したフォルダーをDynamic Mediaと同期するようにマークするには、アセットフォルダーを選択し、ツールバーで「 **[!UICONTROL プロパティ]**. 「**[!UICONTROL 詳細]**」タブの **[!UICONTROL Dynamic Media 同期モード]**&#x200B;ドロップダウンリストで、次の 3 つのオプションから選択します。完了したら、「**[!UICONTROL 保存]**」を選択します。*注意：以前に「**[!UICONTROL すべてのコンテンツを同期]**」を選択した場合、これら 3 つのオプションは使用できません。*[Dynamic Media のフォルダーレベルでの選択的公開の設定](/help/assets/selective-publishing.md)も参照してください。
         * **[!UICONTROL 継承]**  — フォルダーに明示的な同期値はありません。代わりに、上位フォルダーの 1 つ、またはクラウド設定のデフォルトモードから同期値を継承します。 継承された詳細なステータスは、ツールチップで表示されます。
         * **[!UICONTROL サブフォルダーで有効にする]** - このサブツリー内のすべての項目を Dynamic Media との同期に含めます。フォルダー固有の設定は、クラウド設定内のデフォルトモードよりも優先されます。
         * **[!UICONTROL サブフォルダーで無効にする]** - このサブツリー内のすべての項目を Dynamic Media との同期から除外します。

   >[!NOTE]
   Dynamic Media - Scene7モードでは、バージョン管理はサポートされていません。 また、遅延アクティベーションは、Dynamic Media 設定を編集ページの「**[!UICONTROL アセットを公開]**」が「**[!UICONTROL アクティベーション時]**」に設定されている場合にのみ、アセットが最初にアクティベートされるまでの間に限って適用されます。
   アセットがアクティベートされるとすぐに、すべての更新が S7 配信にライブ公開されます。

1. 「**[!UICONTROL 保存]**」を選択します。
1. 公開前にDynamic Mediaコンテンツを安全にプレビューするには、Experience Managerでトークンベースの検証が使用されるので、Experience Manager作成者は、デフォルトでDynamic Mediaコンテンツをプレビューできます。 ただし、次の操作は可能です。 *許可リスト* コンテンツを安全にプレビューするためのアクセスをユーザーに提供する IP の数が増えました。 このアクションをExperience Managerに設定するには [Image Server 用のDynamic Media公開設定の指定 — 「セキュリティ」タブ](/help/assets/dm-publish-settings.md#security-tab).
<!-- 1. By default Experience Manager Author cannot preview Dynamic Media content. Therefore, to securely preview Dynamic Media content before it gets published, you must *allowlist* the Experience Manager Author instance to connect to Dynamic Media. In addition, if you want to provide users access to securely preview content, you can *allowlist* additional IP addresses:

    * In Experience Manager Author mode, select the Experience Manager logo to access the global navigation console.
    * In the left rail, select the **[!UICONTROL Tools]** icon, then go to **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
    * On the Dynamic Media Image Server page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * Select the **[!UICONTROL Security]** tab.
    * For the **[!UICONTROL Client address]**, select **[!UICONTROL Add]**.
    * Enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * In the upper-right corner of the page, select **[!UICONTROL Save]**.
 -->
これで基本設定が完了しました。Dynamic Media - Scene7 モードを使用する準備が整いました。

設定をさらにカスタマイズする場合は、以下の任意のタスクを任意で実行できます。 [（オプション） Dynamic Media - Scene7モードでの詳細設定](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## （オプション） Dynamic Media - Scene7モードでの詳細設定 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Dynamic Media - Scene7 モードのセットアップと設定をさらにカスタマイズしたり、パフォーマンスを最適化したりする場合は、次の&#x200B;*オプション*&#x200B;タスクを 1 つまたは複数実行できます。

* [（オプション）2 GB を超えるアセットのアップロードに対するDynamic Media - Scene7モードの設定](#optional-config-dms7-assets-larger-than-2gb)

* [（オプション）Dynamic Media - Scene7 モードのセットアップと設定](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [（オプション） Dynamic Media - Scene7モードのパフォーマンスの調整](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [（オプション）レプリケーション用のアセットのフィルタリング](#optional-filtering-assets-for-replication)

### （オプション）2 GB を超えるアセットのアップロードに対するDynamic Media - Scene7モードの設定 {#optional-config-dms7-assets-larger-than-2gb}

Dynamic Media - Scene7モードでは、デフォルトのアセットアップロードファイルサイズは 2 GB 以下です。 ただし、オプションで、2 GB を超え 15 GB までのアセットのアップロードを設定できます。

この機能を使用する場合は、次の前提条件とポイントに注意してください。

* Dynamic Media - Scene7モードで、Experience Manager6.5 と Service Pack 6.5.4.0 以降を実行している。
* この大きなアップロード機能は、次の場合にのみサポートされます。 [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) 顧客。
* Experience ManagerインスタンスにAmazon S3 またはMicrosoft® Azure Blob ストレージが設定されていることを確認してください。

   >[!NOTE]
   この大規模なアップロード機能は BLOB ストレージ構成の AzureSas ではサポートされていないので、アクセスキーと秘密鍵を使用して Azure BLOB ストレージを構成します。

* オークの [直接バイナリアクセスのダウンロード](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) が有効 (Oak の *直接バイナリアクセスのアップロード* は必須ではありません )。

   直接バイナリアクセスのダウンロードを有効にするには、プロパティを設定します `presignedHttpDownloadURIExpirySeconds > 0` （データストア設定内）。 値は、大きなバイナリをダウンロードし、再試行するのに十分な長さにする必要があります。

* 15 GB を超えるアセットはアップロードされません。 （サイズ制限は、以下の手順 8 で設定します）。
* 次の場合に **[!UICONTROL Dynamic Media Reprocess]** assets ワークフローがフォルダーでトリガーされ、Dynamic Mediaの会社と既に同期している大きなアセットが再処理されます。 ただし、大きなアセットがまだフォルダー内で同期されていない場合、アセットはアップロードされません。 したがって、Dynamic Mediaの既存の大きなアセットを同期するには、 **[!UICONTROL Dynamic Media Reprocess]** 個々のアセットに対するアセットワークフロー。

**2 GB を超えるアセットのアップロード用にDynamic Media - Scene7モードを設定するには：**

1. Experience Managerで、Experience Managerロゴを選択してグローバルナビゲーションコンソールにアクセスし、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.

1. CRXDE Liteウィンドウで、次のいずれかの操作を行います。

   * 左側のレールで、次のパスに移動します。

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 上のパスをコピーしてツールバーの下のCRXDE Liteパスフィールドに貼り付け、「 `Enter`.

1. 左側のレールで、を右クリックします。 `fileupload`を選択し、ポップアップメニューから「 **[!UICONTROL ノードをオーバーレイ]**.

   ![ノードをオーバーレイオプション](/help/assets/assets-dm/uploadassets15gb_a.png)

1. ノードをオーバーレイダイアログボックスで、 **[!UICONTROL ノードタイプを一致させる]** チェックボックスをオンにしてオプションを有効（オン）にし、 **[!UICONTROL OK]**.

   ![ノードをオーバーレイダイアログボックス](/help/assets/assets-dm/uploadassets15gb_b.png)

1. CRXDE Liteウィンドウで、次のいずれかの操作を行います。

   * 左側のレールで、次のオーバーレイノードパスに移動します。

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 上のパスをコピーしてツールバーの下のCRXDE Liteパスフィールドに貼り付け、「 `Enter`.

1. 内 **[!UICONTROL プロパティ]** タブの **[!UICONTROL 名前]** 列、場所 `sizeLimit`.
1. 右 `sizeLimit` 名前、 **[!UICONTROL 値]** 列で、値フィールドをダブルクリックします。
1. サイズ制限を、必要な最大アップロードサイズに増やせるよう、適切な値をバイト単位で入力します。 例えば、アップロードアセットのサイズ制限を 10 GB に増やすには、 `10737418240` 」と入力します。
最大 15 GB の値を入力できます (`2013265920` バイト ) です。 この場合、15 GB を超えるアップロード済みアセットはアップロードされません。

   ![サイズ制限値](/help/assets/assets-dm/uploadassets15gb_c.png)

1. [CRXDE Lite] ウィンドウの左上隅付近で、 **[!UICONTROL すべて保存]**.

   *次に、次の操作を行って、AdobeGranite Workflow External Process Job Handler のタイムアウトを設定します。*

1. Experience Managerで、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。
1. 次のいずれかの操作を行います。

   * 次の URL パスに移動します。

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * 上のパスをコピーして、ブラウザーの「 URL 」フィールドに貼り付けます。 必ず `localhost:4502` を独自のExperience Managerインスタンスで

1. 内 **[!UICONTROL AdobeGranite Workflow External Process Job Handler]** ダイアログボックス、 **[!UICONTROL 最大タイムアウト]** フィールドの値を `18000` 分（5 時間）です。 デフォルトは10800分（3 時間）です。

   ![最大タイムアウト値](/help/assets/assets-dm/uploadassets15gb_d.png)

1. ダイアログボックスの右下隅で、 **[!UICONTROL 保存]**.

   *次の手順を実行して、Scene7直接バイナリアップロードプロセスのタイムアウトを設定します。*

1. Experience Managerで、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。
1. **[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動します。
1. ワークフローモデルページで、「 」を選択します。 **[!UICONTROL Dynamic Media Encode Video]**.
1. ツールバーの「**[!UICONTROL 編集]**」を選択します。
1. ワークフローページで、 **[!UICONTROL Scene7直接バイナリアップロード]** プロセスステップ。
1. 内 **[!UICONTROL ステップのプロパティ]** ダイアログボックスの **[!UICONTROL 共通]** タブの **[!UICONTROL 詳細設定]** 見出し、 **[!UICONTROL タイムアウト]** フィールドに値を入力 `18000` 分（5 時間）です。 デフォルトはです。 `3600` 分（1 時間）です。
1. 「**[!UICONTROL OK]**」を選択します。
1. 選択 **[!UICONTROL 同期]**.
1. 手順 14～21 を **[!UICONTROL DAM アセットの更新]** ワークフローモデルと **[!UICONTROL Dynamic Media Reprocess]** ワークフローモデル。

### （オプション）Dynamic Media - Scene7 モードのセットアップと設定 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

<!-- When you are in run mode `dynamicmedia_scene7`, use the Dynamic Media Classic user interface to change your Dynamic Media settings. -->

* [Image Server 用のDynamic Media公開設定の指定](/help/assets/dm-publish-settings.md)
* [Dynamic Mediaの一般設定](/help/assets/dm-general-settings.md)
* [カラーマネジメントの設定](#configuring-color-management)
* [サポートされている形式の MIME タイプの編集](#editing-mime-types-for-supported-formats)
* [サポートされていない形式の MIME タイプの追加](#adding-mime-types-for-unsupported-formats)
* [画像セットおよびスピンセットを自動生成するためのバッチセットプリセットの作成](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) (Dynamic Media Classicユーザーインターフェイスで実行 )

#### Image Server 用のDynamic Media公開設定の指定 {#publishing-setup-for-image-server}

Dynamic Mediaの公開設定ページでは、AdobeDynamic Mediaサーバーから Web サイトやアプリケーションにアセットを配信する方法を決定するデフォルト設定を指定します。

詳しくは、 [Image Server 用のDynamic Media公開設定の指定](/help/assets/dm-publish-settings.md).

#### Dynamic Mediaの一般設定 {#configuring-application-general-settings}

Dynamic Mediaの設定 **[!UICONTROL 公開サーバ名]** URL と **[!UICONTROL オリジンサーバー名]** URL。 また、 **[!UICONTROL アプリケーションにアップロード]** 設定と **[!UICONTROL デフォルトのアップロードオプション]** すべて、特定の使用例に基づいておこないます。

詳しくは、 [Dynamic Mediaの一般設定](/help/assets/dm-general-settings.md).

#### カラーマネジメントの設定 {#configuring-color-management}

Dynamic Media カラーマネジメントを使用すると、アセットをカラー補正できます。カラー補正により、取り込まれたアセットは、カラースペース（RGB、CMYK、グレー）および埋め込みカラープロファイルを維持します。動的レンディションを要求した場合、画像の色は、CMYK、RGB またはグレー出力を使用するターゲットのカラースペースに補正されます。

[画像プリセットの設定](/help/assets/managing-image-presets.md)を参照してください。

>[!NOTE]
デフォルトでは、「 **[!UICONTROL レンディション]** 選択時に 15 個のビューアプリセット **[!UICONTROL ビューア]** （アセットの詳細ビュー）。 この制限は増やすことができます。詳しくは、 [表示される画像プリセットの数を増やします](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) または [表示されるビューアプリセットの数を増やします](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### サポートされている形式の MIME タイプの編集 {#editing-mime-types-for-supported-formats}

Dynamic Media によって処理されるアセットタイプを定義して、高度なアセット処理パラメーターをカスタマイズできます。例えば、アセット処理パラメーターを指定して次のことができます。

* Adobe PDF を eCatalog アセットに変換する。
* Adobe Photoshop ドキュメント（.PSD）をパーソナライズ用のバナーテンプレートアセットに変換する。
* Adobe Illustrator ファイル（.AI）または Adobe Photoshop Encapsulated PostScript® ファイル（.EPS）をラスタライズする。
* [ビデオプロファイル](/help/assets/video-profiles.md) および [イメージプロファイル](/help/assets/image-profiles.md) を使用して、それぞれビデオと画像の処理を定義できます。

[アセットのアップロード](/help/assets/manage-assets.md#uploading-assets)を参照してください。

**サポートされている形式の MIME タイプを編集するには：**

1. Experience Managerで、Experience Managerロゴを選択してグローバルナビゲーションコンソールにアクセスし、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 左側のパネルで、次の場所に移動します。

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME タイプ](assets/mimetypes.png)

1. mimeTypes フォルダーで、MIME タイプを選択します。
1. CRXDE Lite ページの右側の下部で、次の操作をおこないます。

   * 「**[!UICONTROL 有効]**」フィールドをダブルクリックします。デフォルトでは、すべてのアセットの MIME タイプが有効になっています（に設定されています）。 **[!UICONTROL true]**) と呼ばれ、アセットがDynamic Mediaに同期されて処理されます。 このアセットの MIME タイプを処理から除外する場合、この設定を **[!UICONTROL false]** に変更します。

   * **[!UICONTROL jobParam]** をダブルタップして、関連するテキストフィールドを開きます。特定の MIME タイプに使用可能な、許可されている処理パラメーター値のリストについては、[サポートされる MIME タイプ](/help/assets/assets-formats.md#supported-mime-types)を参照してください。

1. 次のいずれかの操作を行います。

   * 手順 3～4 を繰り返して、その他の MIME タイプを編集します。
   * CRXDE Lite ページのメニューバーで、「**[!UICONTROL すべて保存]**」を選択します。

1. ページの左上隅で、「 **[!UICONTROL CRXDE Lite]** Experience Managerに戻る

#### サポートされていない形式のカスタム MIME タイプの追加 {#adding-mime-types-for-unsupported-formats}

Experience Manager Assets でサポートされていない形式のカスタム MIME タイプを追加できます。CRXDE Liteに追加する新しいノードがExperience Managerによって削除されないようにするには、MIME タイプを `image_`. また、有効な値が **[!UICONTROL false]**.

**サポートされていない形式のカスタム MIME タイプを追加するには:**

1. Experience Managerから、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL Web コンソール]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新しいブラウザータブが開き、**[!UICONTROL Adobe Experience Manager Web コンソール設定]**&#x200B;ページが表示されます。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. ページ上で、*Adobe CQ Scene7 Asset MIME type Service* という名前まで下にスクロールします。次のスクリーンショットを参照してください。名前の右側で、 **[!UICONTROL 設定値の編集]** （鉛筆アイコン）を使用します。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. **Adobe CQ Scene7 Asset MIME type Service** ページで、任意のプラス記号アイコン「+」を選択します。新しい MIME タイプを追加する際にプラス記号を選択するテーブル内の場所は簡単です。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 空のテキストフィールドに追加した `DWG=image/vnd.dwg` を入力します。

   例 `DWG=image/vnd.dwg` は、デモ目的でのみ使用します。 ここで追加する MIME タイプは、その他のサポートされていない形式でもかまいません。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. ページの右下隅にある「**[!UICONTROL 保存]**」を選択します。

   この時点で、Adobe Experience Manager Web コンソール設定ページが開いているブラウザータブを閉じることができます。

1. 開いているブラウザーコンソールの「Experience Manager」タブに戻ります。
1. Experience Managerから、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 左側のパネルで、次の場所に移動します。

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. `image_vnd.dwg` MIME タイプをドラッグし、次のスクリーンショットに示すように、ツリー内の `image_` の上にドロップします。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. MIME タイプを使用 `image_vnd.dwg` 選択された状態 ( **[!UICONTROL プロパティ]** タブ、 **[!UICONTROL 有効]** 行、 **[!UICONTROL 値]** 列ヘッダーで、値をダブルタップして **[!UICONTROL 値]** 」ドロップダウンリストから選択できます。
1. フィールドに `false` と入力します（または、ドロップダウンリストから「**[!UICONTROL false]**」を選択します）。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. CRXDE Lite ページの左上隅付近にある「**[!UICONTROL すべて保存]**」を選択します。

#### 画像セットおよびスピンセットを自動生成するためのバッチセットプリセットの作成 {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

アセットを Dynamic Media にアップロードしながら画像セットやスピンセットを自動作成するには、バッチセットプリセットを使用します。

まず、アセットを 1 つのセットにグループ化する際の命名規則を定義します。 次に、一意の名前を持つ、自己完結型の命令のセットであるバッチセットプリセットを作成します。 プリセットレシピ内で定義された命名規則に一致する画像を使用してセットを作成する方法を定義する必要があります。

ファイルをアップロードする際に、Dynamic Media によって、アクティブプリセット内の定義された命名規則に一致するすべてのファイルのセットが自動的に作成されます。

##### デフォルトの命名規則を設定

バッチセットプリセット手法で使用するデフォルトの命名規則を作成します。バッチセットプリセット定義で選択されたデフォルトの命名規則は、セットのバッチ生成に会社で必要なものだけである可能性があります。 バッチセットプリセットは、定義するデフォルトの命名規則を使用するために作成されます。会社が定義するデフォルトの命名規則に例外がある場合のために、特定のコンテンツのセットに必要な代替のカスタム命名規則を含むバッチセットプリセットを、必要なだけいくつでも作成できます。

バッチセットプリセット機能を使用する場合は、デフォルトの命名規則を設定する必要はありませんが、ベストプラクティスでは、デフォルトの命名規則を使用することをお勧めします。 これにより、1 つのセットにグループ化する命名規則の要素をいくつでも定義できるので、バッチセットの作成を合理化できます。

別の方法として、 **[!UICONTROL コードを表示]** フォームフィールドを使用できません。 このビューでは、正規表現を完全に使用して命名規則の定義を作成します。

定義には、一致とベース名という 2 つの要素を使用できます。これらのフィールドでは、命名規則のすべての要素を定義して、要素が含まれるセットを命名するために使用される規則の一部を指定できます。会社の個々の命名規則では、多くの場合、これらの要素ごとに 1 行以上の定義を使用します。 独自の定義行を必要なだけ使用して、メイン画像、カラー要素、代替表示要素およびスウォッチ要素などの個別の要素にグループ化できます。

**デフォルトの命名規則を設定するには：:**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、アドビカスタマーサポートにお問い合わせください。

1. ページ上部付近のナビゲーションバーで、に移動します。 **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション設定]** > **[!UICONTROL バッチセットプリセット]** > **[!UICONTROL デフォルトの名前]**.
1. 「**[!UICONTROL フォームを表示]**」または「**[!UICONTROL コードを表示]**」を選択し、各要素に関する情報の表示と入力の方法を指定します。

   「**[!UICONTROL コードを表示]**」チェックボックスを選択して、選択した形式と同時に作成される正規表現値を表示できます。フォーム表示により制限を受ける場合、命名規則の要素を定義するために正規表現値を入力または変更できます。値をフォーム表示で解析できない場合は、フォームフィールドは非アクティブになります。

   >[!NOTE]
   非アクティブなフォームフィールドは、正規表現の正誤に関する検証を実行しません。「結果」行で各要素に作成する正規表現の結果を確認できます。完全な正規表現は、ページの一番下に表示されます。

1. 必要に応じて各要素を展開し、使用する命名規則を入力します。
1. 必要に応じて、次の操作をおこないます。

   * 選択 **[!UICONTROL 追加]** 別の命名規則を要素に追加する場合。
   * 選択 **[!UICONTROL 削除]** 要素の命名規則を削除する場合。

1. 次のいずれかの操作を行います。

   * 選択 **[!UICONTROL 名前を付けて保存]** プリセットの名前を入力します。
   * 選択 **[!UICONTROL 保存]** （既存のプリセットを編集している場合）

##### バッチセットプリセットの作成



Dynamic Media では、バッチセットプリセットを使用して、アセットをビューアで表示するための画像のセット（代替画像、カラーオプション、360 スピン）に整理します。バッチセットプリセットは、Dynamic Media でのアセットアップロード処理と同時に自動的に実行されます。

バッチセットプリセットを作成、編集および管理できます。バッチセットプリセット定義には次の 2 つの形式があります。1 つは、設定可能なデフォルトの命名規則用、もう 1 つはその場で作成するカスタムの命名規則用です。

バッチセットプリセットを定義するフォームフィールドメソッドとコードメソッドのどちらかを使用できます（正規表現を使用できます）。デフォルトの名前では、「フォームを表示」での定義と同時に「コードを表示」を選択して、正規表現を使用して定義を作成できます。また、どちらかの表示をオフにして、一方の表示のみを使用することもできます。

**バッチセットプリセットを作成するには：:**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、アドビカスタマーサポートにお問い合わせください。

1. ページ上部付近のナビゲーションバーで、に移動します。 **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション設定]** > **[!UICONTROL バッチセットプリセット]** > **[!UICONTROL バッチセットプリセット]**.

   **[!UICONTROL フォームを表示]**&#x200B;詳細ページの右上隅に設定されているように、はデフォルトの表示です。

1. プリセットリストパネルで、「 **[!UICONTROL 追加]** をクリックして、画面の右側にある詳細パネルで定義フィールドをアクティブにします。
1. 詳細パネルの「プリセット名」フィールドに、プリセットの名前を入力します。
1. 「バッチセットの種類」ドロップダウンメニューで、プリセットの種類を選択します。
1. 次のいずれかの操作をおこないます。

   * 以前に **[!UICONTROL アプリケーション設定]** > **[!UICONTROL バッチセットプリセット]** > **[!UICONTROL デフォルトの名前]**、展開 **[!UICONTROL アセットの命名規則]**&#x200B;を選択し、「ファイル名」ドロップダウンリストで、 **[!UICONTROL デフォルト]**.

   * プリセット設定時に新しい命名規則を定義するには、を展開します。 **[!UICONTROL アセットの命名規則]**&#x200B;を選択し、「ファイル名」ドロップダウンリストで、 **[!UICONTROL カスタム]**.

1. 「シーケンスの順序」では、セットがDynamic Mediaでグループ化された後の画像の表示順を定義します。

   デフォルトでは、アセットはアルファベット順に並んでいます。ただし、コンマ区切りの正規表現リストを使用して順番を定義できます。

1. 命名規則と作成オプションの設定では、アセットの命名規則で定義したベース名にサフィックスとプレフィックスを指定します。また、Dynamic Mediaフォルダー構造内でセットを作成する場所を定義します。

   多数のセットを定義する場合は、アセット自体を含むフォルダーとは別にセットを保存してください。 例えば、画像セットフォルダーを作成し、生成したセットをここに配置します。

1. 詳細パネルで、 **[!UICONTROL 保存]**.
1. 選択 **[!UICONTROL アクティブ]** 新しいプリセット名の横に表示されます。

   プリセットをアクティブにすると、アセットを Dynamic Media にアップロードする際に、バッチセットプリセットを適用してセットを生成できます。

##### 2D スピンセットを自動生成するためのバッチセットプリセットの作成

バッチセットの種類の&#x200B;**[!UICONTROL 多軸スピンセット]**&#x200B;を使用して、2D スピンセットの生成を自動化する手法を作成できます。画像のグループ化では行と列の正規表現を使用するので、画像アセットが多次元の配列の対応する場所に正しく配置されます。多軸スピンセットの行数または列数には、上限または下限はありません。

例として、`spin-2dspin` という名前の多軸スピンセットを作成します。1 行あたり 12 個の画像が含まれる 3 行のスピンセット画像セットがあります。画像の名前は次のとおりです。

```
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

この情報を使用して、次のようにバッチセットの種類のレシピを作成できます。

![chlimage_1-560](assets/chlimage_1-560.png)

スピンセット内の共有アセット名部分のグループ化が **[!UICONTROL 一致]** フィールド（ハイライト表示されているとおり） 行と列を含むアセット名の可変部分は、それぞれ「**[!UICONTROL 行]**」フィールドと「**[!UICONTROL 列]**」フィールドに追加しています。

このスピンセットをアップロードして公開する際に、**[!UICONTROL アップロードオプションを設定]**&#x200B;ダイアログボックスの&#x200B;**[!UICONTROL バッチセットプリセット]**&#x200B;の下に表示される 2D スピンセット手法の名前をアクティブ化します。

**2D スピンセットを自動生成するためのバッチセットプリセットを作成するには：:**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、アドビカスタマーサポートにお問い合わせください。

1. ページ上部付近のナビゲーションバーで、に移動します。 **[!UICONTROL 設定]** > **[!UICONTROL アプリケーション設定]** > **[!UICONTROL バッチセットプリセット]** > **[!UICONTROL バッチセットプリセット]**.

   **[!UICONTROL フォームを表示]**&#x200B;詳細ページの右上隅に設定されているように、はデフォルトの表示です。

1. プリセットリストパネルで、「 **[!UICONTROL 追加]** をクリックして、画面の右側にある詳細パネルで定義フィールドをアクティブにします。
1. 詳細パネルの「プリセット名」フィールドに、プリセットの名前を入力します。
1. 「バッチセットの種類」ドロップダウンメニューで、「**[!UICONTROL アセットセット]**」を選択します。
1. 「サブタイプ」ドロップダウンリストで、「**[!UICONTROL 多軸スピンセット]**」を選択します。
1. 展開 **[!UICONTROL アセットの命名規則]**&#x200B;を選択し、「ファイル名」ドロップダウンリストで、 **[!UICONTROL カスタム]**.
1. 「**[!UICONTROL 一致]**」およびオプションとして「**[!UICONTROL ベース名]**」の属性を使用して、グループを構成する画像アセットの命名に使用する正規表現を定義します。

   リテラルの Match 正規表現の例を次に示します。

   `(w+)-w+-w+`

1. 「**[!UICONTROL 行と列の位置]**」を展開し、2D スピンセット配列内の画像アセットの位置の名前形式を定義します。

   ファイル名内での行または列の位置は丸括弧で囲みます。

   例えば、行の正規表現の場合、次のようになります。

   `\w+-R([0-9]+)-\w+`

   または

   `\w+-(\d+)-\w+`

   列の正規表現の例を次に示します。

   `\w+-\w+-C([0-9]+)`

   または

   `\w+-\w+-C(\d+)`

   上記のサンプルは、デモ目的でのみ使用します。 必要に応じて独自の正規表現を作成できます。

   >[!NOTE]
   行と列の正規表現の組み合わせで、多次元スピンセット配列内のアセットの位置を判断できない場合、アセットはセットに追加されません。 エラーもログに記録されます。

1. 命名規則と作成オプションの設定では、アセットの命名規則で定義したベース名にサフィックスとプレフィックスを指定します。

   また、Dynamic Media Classicのフォルダー構造内でスピンセットを作成する場所を定義します。

   多数のセットを定義する場合は、アセット自体を含むフォルダーとは別にセットを保存してください。 例えば、スピンセットフォルダーを作成して、生成されたセットをここに配置します。

1. 詳細パネルで、 **[!UICONTROL 保存]**.
1. 選択 **[!UICONTROL アクティブ]** 新しいプリセット名の横に表示されます。

   プリセットをアクティブにすると、アセットを Dynamic Media にアップロードする際に、バッチセットプリセットを適用してセットを生成できます。

### （オプション） Dynamic Media - Scene7モードのパフォーマンスの調整 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Dynamic Media - Scene7モードのスムーズな実行を維持するために、Adobeでは、次の同期パフォーマンス/拡張性の微調整のヒントをお勧めします。

* 様々なファイル形式の処理に対応する定義済みのジョブパラメーターを更新する。
* 事前定義済みの Granite のワークフロー（ビデオアセット）キューワーカースレッドを更新する。
* Granite の事前定義済みの一時的なワークフロー（画像および非ビデオアセット）キューワーカースレッドを更新する。
* Dynamic Media Classic サーバーへの最大アップロード接続数を更新する。

#### 様々なファイル形式の処理に対応する定義済みジョブパラメーターの更新

ジョブパラメーターを調整して、ファイルアップロード時の処理を高速化できます。例えば、PSD ファイルをアップロードしても、テンプレートとして処理しない場合は、レイヤー抽出を false（オフ）に設定できます。この場合、調整されたジョブパラメーターは次のように表示されます。`process=None&createTemplate=false`

テンプレートの作成を有効にする場合は、次のパラメーターを使用します。`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

PDF ファイル、PostScript® ファイル、PSD ファイルには、以下の「調整済み」ジョブパラメーターを使用することをお勧めします。

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| ファイルタイプ | 推奨されるジョブパラメーター |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

これらのパラメーターのいずれかを更新するには、[MIME タイプベースの Assets／Dynamic Media Classic アップロードジョブパラメーターサポートの有効化](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)の手順に従います。

#### Granite の一時的なワークフローキューの更新 {#updating-the-granite-transient-workflow-queue}

Granite の一時的なワークフローキューは、**[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローに使用されます。Dynamic Media では、画像の取り込みおよび処理に使用されます。

**Granite の一時的なワークフローキューを更新するには：**

1. に移動します。 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) およびを検索します。 **キュー：Granite 一時的なワークフローキュー**.

   >[!NOTE]
   OSGi PID は動的に生成されるので、ダイレクト URL ではなく、テキスト検索が必要です。

1. 「**[!UICONTROL 並列ジョブの最大数]**」フィールドで、目的の値に数値を変更します。

   **[!UICONTROL 並列ジョブの最大数]**&#x200B;を増やすと、Dynamic Media へのファイルの大量アップロードを適切にサポートできます。正確な値は、ハードウェアの容量に依存します。初期移行や 1 回限りのバルクアップロードなど、特定のシナリオでは、大きな値を使用できます。 ただし、大きな値（コア数の 2 倍など）を使用すると、他の同時アクティビティに悪影響を及ぼす可能性があることに注意してください。そのため、特定事例で値をテストして整する必要があります。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 「**[!UICONTROL 保存]**」を選択します。

#### Granite のワークフローキューの更新 {#updating-the-granite-workflow-queue}

Granite のワークフローキューは、一時的でないワークフローに使用されます。Dynamic Media では、**[!UICONTROL Dynamic Media エンコーディングビデオ]**&#x200B;ワークフローでビデオを処理するために使用されます。

**Granite のワークフローキューを更新するには：**

1. `https://<server>/system/console/configMgr` に移動して、**Queue: Granite Workflow Queue** を検索します。

   >[!NOTE]
   OSGi PID は動的に生成されるので、ダイレクト URL ではなく、テキスト検索が必要です。

1. 「**[!UICONTROL 並列ジョブの最大数]**」フィールドで、目的の値に数値を変更します。

   並列ジョブの最大数を増やすと、Dynamic Media へのファイルの大量アップロードを適切にサポートできます。正確な値は、ハードウェアの容量に依存します。初期移行や 1 回限りのバルクアップロードなど、特定のシナリオでは、大きな値を使用できます。 ただし、大きな値（コア数の 2 倍など）を使用すると、他の同時アクティビティに悪影響を及ぼす可能性があることに注意してください。そのため、特定事例で値をテストして整する必要があります。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 「**[!UICONTROL 保存]**」を選択します。

#### Dynamic Media Classicアップロード接続の更新 {#updating-the-scene-upload-connection}

Scene7 アップロード接続の設定は、Experience Manager Assets を Dynamic Media Classic サーバーと同期します。

**Dynamic Media Classicアップロード接続を更新するには：**

1. `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl` に移動します。
1. 「**[!UICONTROL Number of connections]**」フィールドおよび「**[!UICONTROL Active job timeout]**」フィールドで、必要に応じて数値を変更します。

   この **[!UICONTROL 接続数]** 設定は、Dynamic Mediaのアップロードに許可される HTTPExperience Managerの最大数を制御します。通常、事前定義された 10 個の接続の値で十分です。

   「**[!UICONTROL Active job timeout]**」設定は、アップロードされた Dynamic Media アセットが配信サーバーで公開されるまでの待機時間を決定します。デフォルトでは、この値は 2100 秒または 35 分です。

   ほとんどの事例では、2100 の設定で十分です。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 「**[!UICONTROL 保存]**」を選択します。

### （オプション）レプリケーション用のアセットのフィルタリング {#optional-filtering-assets-for-replication}

非Dynamic Mediaデプロイメントでは、 *すべて* アセット（画像とビデオの両方）をExperience Managerオーサー環境からExperience Manager公開ノードに移動します。 このワークフローは、Experience Managerパブリッシュサーバーもアセットを配信するので、必要です。

ただし、Dynamic Mediaデプロイメントでは、アセットはCloud Serviceを通じて配信されるので、Experience Managerのパブリッシュノードに同じアセットをレプリケートする必要はありません。 このような「ハイブリッド公開」ワークフローを使用すると、余分なストレージコストと、アセットをレプリケートする処理時間が長くなるのを防ぐことができます。 サイトページなどのその他のコンテンツは、引き続きExperience Managerパブリッシュノードから提供されます。

フィルターを使用すると、次のことができます。 *除外* アセットのパブリッシュノードへのExperience Managerのレプリケートから。

#### レプリケーションにデフォルトのアセットフィルターを使用 {#using-default-asset-filters-for-replication}

Dynamic Mediaを画像やビデオ、またはその両方に使用する場合、Adobeがそのまま提供するデフォルトのフィルターを使用できます。 次のフィルターがデフォルトでアクティブです。

|  | フィルター | MIME タイプ | レンディション |
| --- | --- | --- | --- |
| ダイナミックメディア画像配信 | filter-image<br>filter-sets | 次で始まる **image/**<br>&#x200B;次を含む **アプリケーション/** で終わる **設定**. | 標準搭載の「filter-images」（インタラクティブ画像を含む単一の画像アセットに適用）および「filter-sets」（スピンセット、画像セット、混在メディアセット、カルーセルセットに適用）は、次のようになります。<br>・元の画像と静的な画像のレンディションをレプリケーションから除外します。 |
| ダイナミックメディアビデオ配信 | filter-video | **video/** で始まる | 標準の「ビデオをフィルター」では、次の操作を実行できます。<br>・元のビデオと静的なサムネールのレンディションをレプリケーションから除外します。 |

>[!NOTE]
フィルターは MIME タイプに適用され、パスに固有にはできません。

#### レプリケーション用のアセットフィルターのカスタマイズ {#customizing-asset-filters-for-replication}

1. Experience Managerで、Experience Managerロゴを選択してグローバルナビゲーションコンソールにアクセスし、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 一般]** > **[!UICONTROL CRXDE Lite]**.
1. 左側のフォルダーツリーで、に移動します。 `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` をクリックして、フィルターを確認します。

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. フィルターの MIME タイプを定義するために、次のように MIME タイプを特定することができます。

   左側のレールで、を展開します。 `content > dam > <locate_your_asset> > jcr:content > metadata`をクリックし、テーブルで `dc:format`.

   次の図は、 `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   この `dc:format` （アセット用） `Fiji Red.jpg` が `image/jpeg`.

   このフィルターをすべての画像に適用するには、形式に関係なく、値をに設定します。 `image/*` 場所 `*` は、あらゆる形式のすべての画像に適用される正規表現です。

   フィルターをタイプが「JPEG」の画像にのみ適用するには、値を `image/jpeg`.

1. レプリケーションに含める、またはレプリケーションから除外するレンディションを定義します。

   レプリケーション用のフィルターに使用できる文字は次のとおりです。

   | 使用する文字 | レプリケーション用のアセットのフィルター方法 |
   | --- | --- |
   | * | ワイルドカード文字 |
   | + | レプリケーション用のアセットを含む |
   | - | レプリケーションからアセットを除外 |

   `content/dam/<locate your asset>/jcr:content/renditions` に移動します。

   次の図は、あるアセットのレンディションの例を示しています。

   ![chlimage_1-4](assets/chlimage_1-4.png)

   オリジナルを複製する場合は、「 `+original`.
