---
title: Dynamic Media - Scene7 モードの設定
description: Dynamic Media - Scene7 モードの設定方法を学習します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 4
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configuration,Scene7 Mode
source-git-commit: f2cfe62c561e772a10ede4f76314a5904d6d64ff
workflow-type: tm+mt
source-wordcount: '6048'
ht-degree: 98%

---

# Dynamic Media - Scene7 モードの設定{#configuring-dynamic-media-scene-mode}

開発、ステージング、実稼動など、様々な環境で Adobe Experience Manager を使用する場合は、環境ごとに Dynamic Media Cloud Services を設定します。

## Dynamic Media - Scene7 モードのアーキテクチャ図 {#architecture-diagram-of-dynamic-media-scene-mode}

以下のアーキテクチャ図に Dynamic Media - Scene7 モードの仕組みを示します。

新しいアーキテクチャでは、Experience Manager は、プライマリソースアセットを扱い、Dynamic Media と同期してアセットの処理や公開をおこないます。

1. プライマリソースアセットが Experience Manager にアップロードされると、Dynamic Media にレプリケートされます。その時点で、Dynamic Media は、ビデオエンコーディングおよび画像の動的バリアントなど、すべてのアセットの処理とレンディションの生成を扱います。（Dynamic Media - Scene7 モードでは、デフォルトのアップロードファイルサイズは 2 GB 以下です。アップロードファイルのサイズを 2 GB まで 15 GB にするには、 [（オプション）2 GB を超えるアセットのアップロードに対するDynamic Media - Scene7モードの設定](#optional-config-dms7-assets-larger-than-2gb)を参照してください。）
1. レンディションが生成されると、Experience Manager から、リモート Dynamic Media レンディションに安全にアクセスしてプレビューできます（バイナリが Experience Manager インスタンスに送り返されることはありません）。
1. コンテンツを公開および承認する準備ができると、Dynamic Media サービスがトリガーされ、コンテンツが配信サーバーにプッシュされて、CDN（コンテンツ配信ネットワーク）にコンテンツがキャッシュされます。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>次の機能では、Adobe Experience Manager - Dynamic Media に組み込まれている標準搭載の CDN を使用する必要があります。他のカスタム CDN は、これらの機能ではサポートされません。
>
>* [スマートイメージング](/help/assets/imaging-faq.md)
>* [キャッシュの無効化](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [ホットリンクの保護](/help/assets/hotlink-protection.md)
>* [コンテンツの HTTP/2 配信](/help/assets/http2.md)
>* CDN レベルでの URL リダイレクト
>* Akamai ChinaCDN（中国での最適な配信用）


## Scene7 モードの Dynamic Media の有効化 {#enabling-dynamic-media-in-scene-mode}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) はデフォルトで無効になっています。Dynamic Media の機能を活用するには、Dynamic Media を有効にする必要があります。

>[!WARNING]
>
>Dynamic Media - Scene7 モードは *Experience Manager オーサーインスタンス専用*&#x200B;です。そのため、`runmode=dynamicmedia_scene7` は、Experience Manager パブリッシュインスタンス&#x200B;*ではなくて* Experience Manager オーサーインスタンスで構成する必要があります。

Dynamic Media を有効にするには、ターミナルウィンドウに次のように入力し（使用されるポートの例は 4502 です）、コマンドラインから `dynamicmedia_scene7` 実行モードを使用して Experience Manager を起動します。

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## （オプション）Dynamic Media のプリセットおよび設定を 6.3 から 6.5 にダウンタイムなしで移行 {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

Experience Manager Dynamic Media を 6.3 から 6.4 または 6.5 にアップグレードする際に、ダウンタイムなしのデプロイメントを実行できるようになりました。すべてのプリセットと設定を CRXDE Lite で `/etc` から `/conf` に移行するには、次の curl コマンドを実行するようにしてください。

>[!NOTE]
>
>Experience Manager インスタンスを互換モードで実行する場合（つまり、互換性パッケージがインストールされている場合）、これらのコマンドを実行する必要はありません。

互換パッケージの有無を問わず、すべてのアップグレードについて、次の Linux curl コマンドを実行することにより、Dynamic Media に付属しているデフォルトの標準提供ビューアプリセットをコピーできます。

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

作成されたカスタムのビューアプリセットと設定のすべてを `/etc` から `/conf` に移行するには、次の Linux® curl コマンドを実行します。

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## 一括アセット移行用の機能パック 18912 をインストールする {#installing-feature-pack-for-bulk-asset-migration}

機能パック 18912 のインストールは&#x200B;*オプション*&#x200B;です。

機能パック 18912 を使用すると、FTP 経由でアセットを一括取り込みするか、Experience Manager で Dynamic Media - ハイブリッドモードまたは Dynamic Media Classic から Dynamic Media - Scene7 モードにアセットを移行できます。これは、[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) から入手できます。

詳しくは、[一括アセット移行用の機能パック 18912 をインストールする](/help/assets/bulk-ingest-migrate.md)を参照してください。

## Cloud Services での Dynamic Media 設定の作成 {#configuring-dynamic-media-cloud-services}

**Dynamic Media を設定する前に** - Dynamic Media 資格情報を含むプロビジョニングメールを受け取ったら、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)をクリックし、アカウントにサインインしてパスワードを変更します。プロビジョニング電子メールで提供されたパスワードは、システムが生成したもので、一時的なパスワードです。Dynamic Media Cloud Service が正しい資格情報で設定されるように、パスワードを更新することが重要です。

![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**Cloud Services での Dynamic Media 設定の作成：**

1. Experience Manager オーサーモードで、Experience Manager ロゴを選択してグローバルナビゲーションコンソールにアクセスし、ツールアイコンを選択して、**[!UICONTROL Cloud Services]** ／**[!UICONTROL Dynamic Media Configuration]** に移動します。
1. Dynamic Media 設定ブラウザーページの左側のパネルで、「**[!UICONTROL グローバル]**」を選択して（「**[!UICONTROL グローバル]**」の左側にあるフォルダーアイコンは選択しないでください）、「**[!UICONTROL 作成]**」を選択します。
1. **[!UICONTROL Dynamic Media 設定を作成]**&#x200B;ページで、タイトル、Dynamic Media アカウントの電子メールアドレス、パスワードを入力し、地域を選択します。この情報は、プロビジョニングの電子メールでアドビから提供されます。メールを受け取っていない場合は、アドビカスタマーサポートにお問い合せください。

   **[!UICONTROL Dynamic Media に接続]**&#x200B;を選択します。

   >[!NOTE]
   Dynamic Media 資格情報を含むプロビジョニングメールを受け取ったら、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにサインインしてパスワードを変更します。プロビジョニング電子メールで提供されたパスワードは、システムが生成したもので、一時的なパスワードです。Dynamic Media Cloud Service が正しい資格情報で設定されるように、パスワードを更新することが重要です。

1. 接続に成功したら、次のように設定します。アスタリスク（*）を含む見出しが必須です。

   * **[!UICONTROL 会社]** - Dynamic Media アカウントの名前です。複数の Dynamic Media アカウントがある。 例えば、異なるサブブランド、事業部、ステージングまたは実稼動環境を持つことができます。

   <!-- UNHIDE FEBRUARY 24, 2022 See also [Configure Dynamic Media company alias account](/help/assets/dm-alias-account.md). -->

   * **[!UICONTROL 会社のルートフォルダーのパス]**

   * **[!UICONTROL アセットの公開]** - 次の 3 つのオプションから選択できます。
      * **[!UICONTROL 即時公開]**&#x200B;とは、アセットがアップロードされると、システムがアセットを取り込み、URL／埋め込みをすぐに提供することを意味します。アセットを公開するためにユーザーが操作する必要はありません。
      * **[!UICONTROL アクティベーション時]**&#x200B;とは、URL／埋め込みリンクが提供される前に、最初にアセットを明示的に公開する必要があることを意味します。<br><!-- CQDOC-17478, Added March 9, 2021-->Experience Manager 6.5.8 以降では、Experience Manager パブリッシュインスタンスは、**[!UICONTROL アクティベーション時]**&#x200B;公開モードでのみ`dam:scene7Domain`や `dam:scene7FileStatus` などの正確な Dynamic Media メタデータ値を反映します。この機能を有効にするには、Service Pack 8 をインストールしてから、Experience Manager を再起動します。Sling Config Manager に移動します。 `Scene7ActivationJobConsumer Component` の設定を検索または新しく作成します）。「**[!UICONTROL Dynamic Media の公開後にメタデータをレプリケート]**」チェックボックスを選択してから「 **[!UICONTROL 保存]**」を選択します。

         ![「 Dynamic Media の公開後にメタデータをレプリケート」チェックボックス](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL 選択的公開]** このオプションを使用すると、Dynamic Media に公開するフォルダーを制御できます。スマート切り抜きや動的レンディションなどの機能を使用したり、プレビュー用に Experience Manager でのみ公開するフォルダーを指定したりできます。これらの同じアセットは、パブリックドメインで配信するために Dynamic Media で公開され&#x200B;*ません*。<br>このオプションは、**[!UICONTROL Dynamic Media Cloud Configuration]** で設定できます。または、必要に応じて、このオプションはフォルダーの **[!UICONTROL プロパティ]**&#x200B;でフォルダーレベルで設定できます。<br>詳しくは、[Dynamic Media での選択的公開の操作](/help/assets/selective-publishing.md)を参照してください。<br>この設定を後で変更した場合、または後でフォルダーレベルで変更した場合、その変更の影響を受けるのは、その時点からアップロードする新しいアセットだけです。フォルダー内の既存のアセットの公開状態は、**[!UICONTROL クイック公開]**&#x200B;または&#x200B;**[!UICONTROL 公開を管理]**&#x200B;ダイアログボックスから手動で変更するまで、そのままになります。
   * **[!UICONTROL プレビューサーバーを保護]** - セキュアなレンディションプレビューサーバーへの URL パスを指定できます。つまり、レンディションが生成されると、Experience Manager は、リモート Dynamic Media レンディションに安全にアクセスしてプレビューできます（バイナリが Experience Manager インスタンスに送り返されることはありません）。
自社のサーバーまたは特別なサーバーを使用する特別な取り決めがない限り、この設定を指定されたとおりにしておくことをお勧めします。

   * **[!UICONTROL すべてのコンテンツを同期]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->デフォルトで選択されています。Dynamic Media との同期で、アセットを選択して含めるまたは除外する場合は、このオプションの選択を解除します。このオプションの選択を解除すると、次の 2 つの Dynamic Media 同期モードから選択できるようになります。

   * **[!UICONTROL Dynamic Media 同期モード]**
      * **[!UICONTROL デフォルトで有効]** - フォルダーを特別に除外するようにマークしない限り、設定はすべてのフォルダーにデフォルトで適用されます。<!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL デフォルトで無効]** - 選択したフォルダーを Dynamic Media と同期するように明示的にマークしない限り、設定はどのフォルダーにも適用されません。
選択したフォルダーを Dynamic Media と同期するようにマークするには、アセットフォルダーを選択した後、ツールバーで「**[!UICONTROL プロパティ]**」を選択します。「**[!UICONTROL 詳細]**」タブの **[!UICONTROL Dynamic Media 同期モード]**&#x200B;ドロップダウンリストで、次の 3 つのオプションから選択します。完了したら、「**[!UICONTROL 保存]**」を選択します。*注意：以前に「**[!UICONTROL すべてのコンテンツを同期]**」を選択した場合、これら 3 つのオプションは使用できません。*[Dynamic Media のフォルダーレベルでの選択的公開の設定](/help/assets/selective-publishing.md) も参照してください。
         * **[!UICONTROL 継承]** - フォルダーに明示的な同期値はなく、代わりに、上位フォルダーの 1 つまたはクラウド設定のデフォルトモードから同期値を継承します。継承した場合の詳細なステータスは、ツールチップで表示されます。
         * **[!UICONTROL サブフォルダーに対して有効にする]** - このサブツリー内のすべての項目を Dynamic Media との同期に含めます。フォルダー固有の設定は、クラウド設定内のデフォルトモードよりも優先されます。
         * **[!UICONTROL サブフォルダーで無効にする]** - このサブツリー内のすべての項目を Dynamic Media との同期から除外します。

   >[!NOTE]
   Dynamic Media - Scene7 モードではバージョン管理はサポートされていません。また、遅延アクティベーションは、「Dynamic Media 設定を編集」ページの&#x200B;**[!UICONTROL アセットを公開]**&#x200B;が&#x200B;**[!UICONTROL アクティベーション時]**&#x200B;に設定されている場合にのみ、アセットが最初にアクティベートされるまでの間に限って適用されます。
   アセットがアクティベートされるとすぐに、すべての更新が S7 配信にライブ公開されます。

1. 「**[!UICONTROL 保存]**」を選択します。
1. デフォルトでは、Experience Manager作成者はDynamic Mediaコンテンツをプレビューできません。 したがって、Dynamic Mediaコンテンツを公開する前に安全にプレビューするには、次の手順を実行する必要があります *許可リスト* Dynamic Mediaに接続するExperience Managerオーサーインスタンス また、ユーザーが安全にプレビューできるコンテンツにアクセスできるようにする場合は、次の操作を行います。 *許可リスト* 追加の IP アドレス。
このアクションをExperience Managerに設定するには [Image Server 用のDynamic Media公開設定の指定 — 「セキュリティ」タブ](/help/assets/dm-publish-settings.md#security-tab).

<!-- 1. To securely preview Dynamic Media content before it gets published, Experience Manager uses token-based validation and hence Experience Manager Author previews Dynamic Media content by default. However, you can *allowlist* more IPs to provide users access to securely preview content. To set up this action in Experience Manager, see [Configure Dynamic Media Publish Setup for Image Server - Security tab](/help/assets/dm-publish-settings.md#security-tab).     * In Experience Manager Author mode, select the Experience Manager logo to access the global navigation console.
    * In the left rail, select the **[!UICONTROL Tools]** icon, then go to **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
    * On the Dynamic Media Image Server page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * Select the **[!UICONTROL Security]** tab.
    * For the **[!UICONTROL Client address]**, select **[!UICONTROL Add]**.
    * Enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * In the upper-right corner of the page, select **[!UICONTROL Save]**. -->

これで基本設定が完了しました。Dynamic Media - Scene7 モードを使用する準備が整いました。

設定をさらにカスタマイズする場合は、[（任意）Dynamic Media - Scene7 モードでの詳細設定](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)で示す任意のタスクを実行できます。

## （任意）Dynamic Media - Scene7 モードでの詳細設定 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Dynamic Media - Scene7 モードのセットアップと設定をさらにカスタマイズしたり、パフォーマンスを最適化したりする場合は、次の&#x200B;*オプション*&#x200B;タスクを 1 つまたは複数実行できます。

* [（任意）2 GB を超えるアセットのアップロードに対する Dynamic Media - Scene7 モードの設定](#optional-config-dms7-assets-larger-than-2gb)

* [（オプション）Dynamic Media - Scene7 モードのセットアップと設定](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [（任意）Dynamic Media - Scene7 モードのパフォーマンスの調整](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [（任意）レプリケーション用のアセットのフィルタリング](#optional-filtering-assets-for-replication)

### （任意）2 GB を超えるアセットのアップロードに対する Dynamic Media - Scene7 モードの設定 {#optional-config-dms7-assets-larger-than-2gb}

Dynamic Media - Scene7 モードでは、デフォルトのアセットアップロードのファイルサイズは 2 GB 以下です。ただし、2～15 GB までのアセットのアップロードを任意で設定できます。

この機能を使用する場合は、前提条件を含む以下の点に注意してください。

* Dynamic Media - Scene7 モードで、Experience Manager 6.5 と Service Pack 6.5.4.0 以降を実行している必要があります。
* 大きなアセットのアップロード機能は、[*Managed Services*](https://business.adobe.com/jp/products/experience-manager/managed-services.html) をご利用のお客様に対してのみサポートされます。
* Experience Manager インスタンスに Amazon S3 または Microsoft® Azure Blob ストレージが設定されていることを確認してください。

   >[!NOTE]
   大きなアセットのアップロード機能は、Blob ストレージ設定の Azure SAS ではサポートされていないので、アクセスキーと秘密鍵を使用して Azure Blob ストレージを設定します。

* Oak の[直接バイナリアクセスのダウンロード](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)を有効にします（Oak の&#x200B;*直接バイナリアクセスのアップロード*&#x200B;は必須ではありません）。

   直接バイナリアクセスのダウンロードを有効にするには、データストア設定内で `presignedHttpDownloadURIExpirySeconds > 0` プロパティを設定します。この値は、大きなバイナリをダウンロードして再試行するのに十分な時間に設定する必要があります。

* 15 GB を超えるアセットはアップロードされません。（サイズ制限は、以下の手順 8 で設定します。）
* **[!UICONTROL Dynamic Media Reprocess]** アセットワークフローがフォルダーでトリガーされた場合、Dynamic Media の会社と既に同期している大きなアセットが再処理されます。ただし、大きなアセットがまだフォルダー内で同期されていない場合、そのアセットはアップロードされません。したがって、Dynamic Media の既存の大きなアセットを同期するには、個々のアセットに対して **[!UICONTROL Dynamic Media Reprocess]** アセットワークフローを実行します。

**2 GB を超えるアセットのアップロードに対して Dynamic Media - Scene7 モードを設定するには：**

1. Experience Manager で、Experience Manager ロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL CRXDE Lite]** に移動します。

1. CRXDE Lite ウィンドウで、以下のいずれかの操作を実行します。

   * 左側のパネルで、以下のパスに移動します。

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 上記のパスをコピーしてツールバーの下の CRXDE Lite パスフィールドに貼り付け、`Enter` を押します。

1. 左側のパネルで、`fileupload` を右クリックし、ポップアップメニューから「 **[!UICONTROL ノードをオーバーレイ]**」を選択します。

   ![「ノードをオーバーレイ」オプション](/help/assets/assets-dm/uploadassets15gb_a.png)

1. ノードをオーバーレイダイアログボックスで、「**[!UICONTROL ノードタイプを一致させる]**」チェックボックスをオンにして有効にし、「**[!UICONTROL OK]**」を選択します。

   ![ノードをオーバーレイダイアログボックス](/help/assets/assets-dm/uploadassets15gb_b.png)

1. CRXDE Lite ウィンドウで、以下のいずれかの操作を実行します。

   * 左側のパネルで、以下のオーバーレイノードパスに移動します。

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * 上記のパスをコピーしてツールバーの下の CRXDE Lite パスフィールドに貼り付け、`Enter` を押します。

1. 「**[!UICONTROL プロパティ]** 」タブの「**[!UICONTROL 名前]**」列の下にある「`sizeLimit`」を探します。
1. `sizeLimit` の名前の右側にある「**[!UICONTROL 値]**」列の下で、値フィールドをダブルクリックします。
1. 適切な値をバイト単位で入力して、アップロードサイズ上限を任意の値に設定します。例えば、アップロードアセットのサイズ上限を 10 GB に増やすには、値フィールドに「`10737418240` 」と入力します。
最大 15 GB（`2013265920` バイト）の値を入力できます。その場合、15 GB を超えるアップロード済みアセットはアップロードされません。

   ![サイズ上限値](/help/assets/assets-dm/uploadassets15gb_c.png)

1. CRXDE Lite ウィンドウの左上隅付近にある「**[!UICONTROL すべて保存]**」を選択します。

   *次に、以下の操作を実行して、Adobe Granite Workflow External Process Job Handler のタイムアウトを設定します。*

1. Experience Manager で、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。
1. 次のいずれかの操作をおこないます。

   * 以下の URL パスに移動します。

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * 上記のパスをコピーして、ブラウザーの URL フィールドに貼り付けます。 `localhost:4502` を独自の Experience Manager インスタンスと置き換えてください。

1. **[!UICONTROL Adobe Granite Workflow External Process Job Handler]** ダイアログボックスで、**[!UICONTROL 最大タイムアウト]**&#x200B;フィールドの値を `18000` 分（5 時間）に設定します。デフォルトは 10800 分（3 時間）です。

   ![最大タイムアウト値](/help/assets/assets-dm/uploadassets15gb_d.png)

1. ダイアログボックスの右下隅にある「**[!UICONTROL 保存]**」を選択します。

   *以下の操作を実行して、Scene7 直接バイナリアップロードプロセスのステップのタイムアウトを設定します。*

1. Experience Manager で、Experience Manager ロゴを選択して、グローバルナビゲーションコンソールにアクセスします。
1. **[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;に移動します。
1. ワークフローモデルページで「**[!UICONTROL Dynamic Media エンコーディングビデオ]**」を選択します。
1. ツールバーの&#x200B;**[!UICONTROL 編集]**&#x200B;を選択します。
1. ワークフローページで、**[!UICONTROL Scene7 直接バイナリアップロード]**&#x200B;プロセスのステップをダブルクリックします。
1. **[!UICONTROL ステップのプロパティ]**&#x200B;ダイアログボックスにある「**[!UICONTROL 共通]**」タブの「**[!UICONTROL 詳細設定]**」見出しで、**[!UICONTROL タイムアウト]**&#x200B;フィールドに `18000` 分（5 時間）の値を入力します。デフォルトは `3600` 分（1 時間）です。
1. **[!UICONTROL OK]** を選択します。
1. 「**[!UICONTROL 同期]**」を選択します。
1. **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローモデルと **[!UICONTROL Dynamic Media 再処理]**&#x200B;ワークフローモデルの手順 14～21 を繰り返します。

### （オプション）Dynamic Media - Scene7 モードのセットアップと設定 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

<!-- When you are in run mode `dynamicmedia_scene7`, use the Dynamic Media Classic user interface to change your Dynamic Media settings. -->

* [Image Server 用の Dynamic Media の公開設定](/help/assets/dm-publish-settings.md)
* [Dynamic Media の一般設定](/help/assets/dm-general-settings.md)
* [カラーマネジメントの設定](#configuring-color-management)
* [サポートされている形式の MIME タイプの編集](#editing-mime-types-for-supported-formats)
* [サポートされていない形式の MIME タイプの追加](#adding-mime-types-for-unsupported-formats)
* [画像セットおよびスピンセットを自動生成するためのバッチセットプリセットの作成](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)（Dynamic Media Classic ユーザーインターフェイスで実行）

#### Image Server 用の Dynamic Media の公開設定 {#publishing-setup-for-image-server}

Dynamic Media の公開設定ページでは、Adobe Dynamic Media サーバーから web サイトやアプリケーションにアセットを配信する方法を決定するデフォルト設定を指定します。

詳しくは、[Image Server 用の Dynamic Media の公開設定](/help/assets/dm-publish-settings.md)を参照してください。

#### Dynamic Media の一般設定 {#configuring-application-general-settings}

Dynamic Media の&#x200B;**[!UICONTROL 公開サーバー名]**&#x200B;の URL と&#x200B;**[!UICONTROL オリジンサーバー名]**&#x200B;の URL を設定します。また、**[!UICONTROL アプリケーションにアップロード]**&#x200B;設定と&#x200B;**[!UICONTROL デフォルトのアップロードオプション]**&#x200B;はすべて、特定のユースケースに基づいて指定できます。

詳しくは、[Dynamic Media の一般設定](/help/assets/dm-general-settings.md)を参照してください。

#### カラーマネジメントの設定 {#configuring-color-management}

Dynamic Media カラーマネジメントを使用すると、アセットをカラー補正できます。カラー補正により、取り込まれたアセットは、カラースペース（RGB、CMYK、グレー）および埋め込みカラープロファイルを維持します。動的レンディションを要求した場合、画像の色は、CMYK、RGB またはグレー出力を使用するターゲットのカラースペースに補正されます。

[画像プリセットの設定](/help/assets/managing-image-presets.md)を参照してください。

>[!NOTE]
デフォルトでは、アセットの詳細表示で「**[!UICONTROL レンディション]** 」を選択した場合 15 個のレンディションが表示され、「**[!UICONTROL ビューア]**」を選択した場合 15 個のビューアプリセットが表示されます。この制限は増やすことができます。[表示する画像プリセット数を増やす](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)または[表示するビューアプリセット数を増やす](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)を参照してください。

#### サポートされている形式の MIME タイプの編集 {#editing-mime-types-for-supported-formats}

Dynamic Media によって処理されるアセットタイプを定義して、高度なアセット処理パラメーターをカスタマイズできます。例えば、アセット処理パラメーターを指定して次のことができます。

* Adobe PDF を eCatalog アセットに変換する。
* Adobe Photoshop ドキュメント（.PSD）をパーソナライズ用のバナーテンプレートアセットに変換する。
* Adobe Illustrator ファイル（.AI）または Adobe Photoshop Encapsulated PostScript® ファイル（.EPS）をラスタライズする。
* [ビデオプロファイル](/help/assets/video-profiles.md)および[イメージングプロファイル](/help/assets/image-profiles.md)は、それぞれ、ビデオおよび画像の処理を定義するのに使用できます。

[アセットのアップロード](/help/assets/manage-assets.md#uploading-assets)を参照してください。

**サポートされている形式の MIME タイプを編集するには：**

1. Experience Manager で、Experience Manager ロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL CRXDE Lite]** に移動します。
1. 左側のパネルで、次の場所に移動します。

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME タイプ](assets/mimetypes.png)

1. mimeTypes フォルダーで、MIME タイプを選択します。
1. CRXDE Lite ページの右側の下部で、次の操作をおこないます。

   * 「**[!UICONTROL 有効]**」フィールドをダブルクリックします。デフォルトでは、すべてのアセットの MIME タイプが有効になって（**[!UICONTROL true]** に設定されて）います。これは、処理に関してアセットが Dynamic Media に同期されることを意味します。このアセットの MIME タイプを処理から除外する場合、この設定を **[!UICONTROL false]** に変更します。

   * **[!UICONTROL jobParam]** をダブルタップして、関連するテキストフィールドを開きます。特定の MIME タイプに使用可能な、許可されている処理パラメーター値のリストについては、[サポートされる MIME タイプ](/help/assets/assets-formats.md#supported-mime-types)を参照してください。

1. 次のいずれかの操作を行います。

   * 手順 3～4 を繰り返して、その他の MIME タイプを編集します。
   * CRXDE Lite ページのメニューバーで、「**[!UICONTROL すべて保存]**」を選択します。

1. ページの左上隅にある「**[!UICONTROL CRXDE Lite]**」を選択して、Experience Manager に戻ります。

#### サポートされていない形式の MIME タイプの追加 {#adding-mime-types-for-unsupported-formats}

Experience Manager Assets でサポートされていない形式のカスタム MIME タイプを追加できます。CRXDE Lite に追加した新しいノードが Experience Manager によって削除されないようにするには、MIME タイプを `image_` の前に移動します。また、有効な値が **[!UICONTROL false]** に設定されていることを確認します。

**サポートされていない形式の MIME タイプを追加するには:**

1. Experience Manager から、**[!UICONTROL ツール]**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;に移動します。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新しいブラウザータブが開き、**[!UICONTROL Adobe Experience Manager Web コンソール設定]**&#x200B;ページが表示されます。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. ページ上で、*Adobe CQ Scene7 Asset MIME type Service* という名前まで下にスクロールします。次のスクリーンショットを参照してください。名前の右側にある&#x200B;**[!UICONTROL 設定値を編集]**（鉛筆アイコン）を選択します。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. **Adobe CQ Scene7 Asset MIME type Service** ページで、任意のプラス記号アイコン「+」を選択します。新しい MIME タイプを追加する場合に、テーブルで選択するプラス記号の場所はわかりやすくなっています。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 空のテキストフィールドに追加した `DWG=image/vnd.dwg` を入力します。

   この`DWG=image/vnd.dwg`の例は、説明の目的でのみ使用します。ここで追加する MIME タイプは、その他のサポートされていない形式でもかまいません。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. ページの右下隅にある「**[!UICONTROL 保存]**」を選択します。

   この時点で、Adobe Experience Manager Web コンソール設定ページが開いているブラウザータブを閉じることができます。

1. Experience Manager のコンソールを開いているブラウザータブに戻ります。
1. Experience Manager から、**[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL CRXDE Lite]** に移動します。

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 左側のパネルで、次の場所に移動します。

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. `image_vnd.dwg` MIME タイプをドラッグし、次のスクリーンショットに示すように、ツリー内の `image_` の上にドロップします。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. MIME タイプ `image_vnd.dwg` を選択したまま、「**[!UICONTROL プロパティ]**」タブの「**[!UICONTROL 有効]**」行で、「**[!UICONTROL 値]**」列見出しの値をダブルクリックして、「**[!UICONTROL 値]**」ドロップダウンリストを開きます。
1. フィールドに `false` と入力します（または、ドロップダウンリストから「**[!UICONTROL false]**」を選択します）。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. CRXDE Lite ページの左上隅付近にある「**[!UICONTROL すべて保存]**」を選択します。

#### 画像セットおよびスピンセットを自動生成するためのバッチセットプリセットの作成 {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

アセットを Dynamic Media にアップロードしながら画像セットやスピンセットを自動作成するには、バッチセットプリセットを使用します。

最初に、アセットをセットにグループ化するための命名規則を定義します。次に、一意の名前を持つ、自己完結型の命令のセットであるバッチセットプリセットを作成します。プリセットレシピ内で定義された命名規則に一致する画像を使用して、セットを作成する方法を定義する必要があります。

ファイルをアップロードする際に、Dynamic Media によって、アクティブプリセット内の定義された命名規則に一致するすべてのファイルのセットが自動的に作成されます。

##### デフォルトの命名を設定

任意のバッチセットプリセット手法で使用するデフォルトの命名規則を作成します。バッチセットプリセット定義で選択されたデフォルトの命名規則は、セットをバッチ生成するための会社の要件になる場合があります。バッチセットプリセットは、定義するデフォルトの命名規則を使用するために作成されます。会社が定義するデフォルトの命名規則に例外がある場合のために、特定のコンテンツのセットに必要な代替のカスタム命名規則を含むバッチセットプリセットを、必要なだけいくつでも作成できます。

バッチセットプリセット機能を使用するためにデフォルトの命名規則を設定する必要はありませんが、ベストプラクティスとしては、デフォルトの命名規則を使用することをお勧めします。それにより、命名規則の要素を必要なだけセットにまとめて定義し、バッチセットの作成を効率化できます。

または、フォームフィールドを利用しないで、「**[!UICONTROL コードを表示]**」を使用することもできます。この表示では、正規表現を使用する命名規則の定義を作成します。

定義には、一致とベース名という 2 つの要素を使用できます。これらのフィールドでは、命名規則のすべての要素を定義して、要素が含まれるセットを命名するために使用される規則の一部を指定できます。会社の個々の命名規則では、多くの場合、これら 2 つの要素のそれぞれに含まれている 1 行以上の定義を使用します。独自の定義行を必要なだけ使用して、メイン画像、カラー要素、代替表示要素およびスウォッチ要素などの個別の要素にグループ化できます。

**デフォルトの命名規則を設定するには、以下の手順に従います。**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、アドビカスタマーサポートにお問い合わせください。

1. ページの上付近にあるナビゲーションバーで、**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL バッチセットプリセット]**／**[!UICONTROL デフォルトの名前]**&#x200B;に移動します。
1. 「**[!UICONTROL フォームを表示]**」または「**[!UICONTROL コードを表示]**」を選択し、各要素に関する情報の表示と入力の方法を指定します。

   「**[!UICONTROL コードを表示]**」チェックボックスを選択して、選択した形式と同時に作成される正規表現値を表示できます。フォーム表示により制限を受ける場合、命名規則の要素を定義するために正規表現値を入力または変更できます。値をフォーム表示で解析できない場合は、フォームフィールドは非アクティブになります。

   >[!NOTE]
   非アクティブなフォームフィールドは、正規表現の正誤に関する検証を実行しません。「結果」行で各要素に作成する正規表現の結果を確認できます。完全な正規表現は、ページの一番下に表示されます。

1. 必要に応じて各要素を展開し、使用する命名規則を入力します。
1. 必要に応じて、次の操作をおこないます。

   * 要素に別の命名規則を追加するには、「**[!UICONTROL 追加]**」を選択します。
   * 要素の命名規則を削除するには、「**[!UICONTROL 削除]**」を選択します。

1. 次のいずれかの操作をおこないます。

   * 「**[!UICONTROL 別名で保存]**」を選択し、プリセットの名前を入力します。
   * 既存のプリセットを編集している場合は、「**[!UICONTROL 保存]**」を選択します。

##### バッチセットプリセットの作成



Dynamic Media では、バッチセットプリセットを使用して、アセットをビューアで表示するための画像のセット（代替画像、カラーオプション、360 スピン）に整理します。バッチセットプリセットは、Dynamic Media でのアセットアップロード処理と同時に自動的に実行されます。

バッチセットプリセットを作成、編集および管理できます。バッチセットプリセット定義には 2 つの形式があります。デフォルトの命名規則を設定するものと、その場で作成するカスタムの命名規則のものです。

バッチセットプリセットを定義するフォームフィールドメソッドとコードメソッドのどちらかを使用できます（正規表現を使用できます）。デフォルトの名前では、「フォームを表示」での定義と同時に「コードを表示」を選択して、正規表現を使用して定義を作成できます。また、どちらかの表示をオフにして、一方の表示のみを使用することもできます。

**バッチセットプリセットを作成するには：:**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、アドビカスタマーサポートにお問い合わせください。

1. ページの上付近にあるナビゲーションバーで、**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL バッチセットプリセット]**／**[!UICONTROL バッチセットプリセット]**&#x200B;に移動します。

   詳細ページの右上隅に設定されている「**[!UICONTROL フォームを表示]**」は、デフォルトの表示です。

1. プリセットリストパネルの「**[!UICONTROL 追加]**」を選択して、画面の右側にある詳細パネルの定義フィールドをアクティブにします。
1. 詳細パネルの「プリセット名」フィールドに、プリセットの名前を入力します。
1. 「バッチセットの種類」ドロップダウンメニューで、プリセットの種類を選択します。
1. 次のいずれかの操作をおこないます。

   * 以前、**[!UICONTROL アプリケーション設定]**／**[!UICONTROL バッチセットプリセット]**／**[!UICONTROL 初期設定の名前]**&#x200B;で設定したデフォルトの命名規則を使用する場合は、「**[!UICONTROL アセットの命名規則]**」を展開し、「ファイル名」ドロップダウンリストで「**[!UICONTROL 初期設定]**」を選択します。

   * プリセット設定時に新しい命名規則を定義するには、「**[!UICONTROL アセットの命名規則]**」を展開し、「ファイル名」ドロップダウンリストで「**[!UICONTROL カスタム]**」を選択します。

1. 「シーケンスの順番」では、Dynamic Media でグループ化されたセットの画像の表示順を定義します。

   デフォルトでは、アセットはアルファベット順に並んでいます。ただし、コンマ区切りの正規表現リストを使用して順番を定義できます。

1. 命名規則と作成オプションの設定では、アセットの命名規則で定義したベース名にサフィックスとプレフィックスを指定します。また、Dynamic Media のフォルダー構造内のセットの作成場所を定義します。

   多数のセットを定義する場合は、アセット自体を含むフォルダーとは別にセットを保存してください。 例えば、画像セットフォルダーを作成して、そこに生成されたセットを配置できます。

1. 詳細パネルで、「**[!UICONTROL 保存]**」を選択します。
1. 新しいプリセット名の隣にある「**[!UICONTROL アクティブ]**」を選択します。

   プリセットをアクティブにすると、アセットを Dynamic Media にアップロードする際に、バッチセットプリセットを適用してセットを生成できます。

##### 2D スピンセットを自動生成するためのバッチセットプリセットを作成

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

この情報から、このバッチセットの種類の手法は次のように作成できます。

![chlimage_1-560](assets/chlimage_1-560.png)

スピンセットのアセット名における共通部分のグループは、（ハイライト表示されているように）「**[!UICONTROL 一致]**」フィールドに追加しています。行と列を含むアセット名の可変部分は、それぞれ「**[!UICONTROL 行]**」フィールドと「**[!UICONTROL 列]**」フィールドに追加しています。

このスピンセットをアップロードして公開する際に、**[!UICONTROL アップロードオプションを設定]**&#x200B;ダイアログボックスの&#x200B;**[!UICONTROL バッチセットプリセット]**&#x200B;の下に表示される 2D スピンセット手法の名前をアクティブ化します。

**2D スピンセットを自動生成するためのバッチセットプリセットを作成するには：**

1. [Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、アカウントにログインします。

   資格情報とログオンの詳細は、プロビジョニング時にアドビから付与されたものです。この情報をお持ちでない場合は、アドビカスタマーサポートにお問い合わせください。

1. ページの上付近にあるナビゲーションバーで、**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL バッチセットプリセット]**／**[!UICONTROL バッチセットプリセット]**&#x200B;に移動します。

   詳細ページの右上隅に設定されている「**[!UICONTROL フォームを表示]**」は、デフォルトの表示です。

1. プリセットリストパネルの「**[!UICONTROL 追加]**」を選択して、画面の右側にある詳細パネルの定義フィールドをアクティブにします。
1. 詳細パネルの「プリセット名」フィールドに、プリセットの名前を入力します。
1. 「バッチセットの種類」ドロップダウンメニューで、「**[!UICONTROL アセットセット]**」を選択します。
1. 「サブタイプ」ドロップダウンリストで、「**[!UICONTROL 多軸スピンセット]**」を選択します。
1. 「**[!UICONTROL アセットの命名規則]**」を展開し、「ファイル名」ドロップダウンリストで「**[!UICONTROL カスタム]**」を選択します。
1. **[!UICONTROL 一致]**&#x200B;およびオプションとして&#x200B;**[!UICONTROL ベース名]**&#x200B;の属性を使用して、グループを構成する画像アセットの命名に使用する正規表現を定義します。

   リテラル一致正規表現の例を次に示します。

   `(w+)-w+-w+`

1. 「**[!UICONTROL 行と列の位置]**」を展開し、2D スピンセット配列内の画像アセットの位置の名前形式を定義します。

   ファイル名内での行または列の位置は丸括弧で囲みます。

   行の正規表現の例を次に示します。

   `\w+-R([0-9]+)-\w+`

   または

   `\w+-(\d+)-\w+`

   列の正規表現の例を次に示します。

   `\w+-\w+-C([0-9]+)`

   または

   `\w+-\w+-C(\d+)`

   上記のサンプルは、デモ目的でのみ使用されています。 必要に応じて独自の正規表現を作成できます。

   >[!NOTE]
   行と列の正規表現の組み合わせから、多次元スピンセットの配列内でアセットの位置を特定できない場合、そのアセットはセットに追加されません。また、エラーがログに記録されます。

1. 命名規則と作成オプションの設定では、アセットの命名規則で定義したベース名にサフィックスとプレフィックスを指定します。

   また、Dynamic Media Classic のフォルダー構造内のスピンセットの作成場所を定義します。

   多数のセットを定義する場合は、アセット自体を含むフォルダーとは別にセットを保存してください。 例えば、スピンセットフォルダーを作成して、そこに生成されたセットを配置します。

1. 詳細パネルで、「**[!UICONTROL 保存]**」を選択します。
1. 新しいプリセット名の隣にある「**[!UICONTROL アクティブ]**」を選択します。

   プリセットをアクティブにすると、アセットを Dynamic Media にアップロードする際に、バッチセットプリセットを適用してセットを生成できます。

### （任意）Dynamic Media - Scene7 モードのパフォーマンスの調整 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Dynamic Media - Scene7 モードのスムーズな実行を維持するために、アドビでは、以下の同期パフォーマンス／スケーラビリティの微調整のヒントをお勧めします。

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

1. [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) に移動して、**Queue: Granite Transient Workflow Queue** を検索します。

   >[!NOTE]
   OSGi PID は動的に生成されるので、ダイレクト URL ではなく、テキスト検索が必要です。

1. 「**[!UICONTROL 並列ジョブの最大数]**」フィールドで、目的の値に数値を変更します。

   **[!UICONTROL 並列ジョブの最大数]**&#x200B;を増やすと、Dynamic Media へのファイルの大量アップロードを適切にサポートできます。正確な値は、ハードウェアの容量に依存します。初回の移行や 1 回限りのバルクアップロードなど、特定のシナリオでは、大きな値を使用できます。ただし、大きな値（コア数の 2 倍など）を使用すると、他の同時アクティビティに悪影響を及ぼす可能性があることに注意してください。そのため、特定事例で値をテストして整する必要があります。

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

   並列ジョブの最大数を増やすと、Dynamic Media へのファイルの大量アップロードを適切にサポートできます。正確な値は、ハードウェアの容量に依存します。初回の移行や 1 回限りのバルクアップロードなど、特定のシナリオでは、大きな値を使用できます。ただし、大きな値（コア数の 2 倍など）を使用すると、他の同時アクティビティに悪影響を及ぼす可能性があることに注意してください。そのため、特定事例で値をテストして整する必要があります。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 「**[!UICONTROL 保存]**」を選択します。

#### Dynamic Media Classic アップロード接続の更新 {#updating-the-scene-upload-connection}

Scene7 アップロード接続の設定は、Experience Manager Assets を Dynamic Media Classic サーバーと同期します。

**Dynamic Media Classic アップロード接続を更新するには：**

1. `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl` に移動します。
1. 「**[!UICONTROL Number of connections]**」フィールドおよび「**[!UICONTROL Active job timeout]**」フィールドで、必要に応じて数値を変更します。

   「**[!UICONTROL 接続数]**」の設定は、Experience Manage が Dynamic Media へのアップロードで許可される HTTP 接続の最大数を制御します。通常、事前定義済みの値の 10 接続で十分です。

   「**[!UICONTROL Active job timeout]**」設定は、アップロードされた Dynamic Media アセットが配信サーバーで公開されるまでの待機時間を決定します。デフォルトでは、この値は 2100 秒または 35 分です。

   ほとんどの事例では、2100 の設定で十分です。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 「**[!UICONTROL 保存]**」を選択します。

### （任意）レプリケーション用のアセットのフィルタリング {#optional-filtering-assets-for-replication}

Dynamic Media 以外のデプロイメントでは、*すべて*&#x200B;のアセット（画像とビデオ）を Experience Manager オーサー環境から Experience Manager パブリッシュノードにレプリケートします。Experience Manager のパブリッシュサーバーもアセットを配信するので、このワークフローが必要になります。

ただし、Dynamic Media のデプロイメントではアセットが Cloud Service によって配信されるので、上記のアセットを Experience Manager パブリッシュノードにレプリケートする必要がありません。そのような「ハイブリッドパブリッシング」ワークフローでは、ストレージコストの増大を防ぎ、アセットをレプリケートするための処理時間を短縮します。サイトページなどのその他のコンテンツは、引き続き Experience Manager パブリッシュノードから配信されます。

フィルターによって、アセットを Experience Manager パブリッシュノードへのレプリケート対象から&#x200B;*除外*&#x200B;することができます。

#### レプリケーションへのデフォルトのアセットフィルターの使用 {#using-default-asset-filters-for-replication}

Dynamic Media を画像、ビデオまたはその両方に使用する場合は、アドビがそのまま提供するデフォルトのフィルターを使用できます。以下のフィルターがデフォルトでアクティブになっています。

|  | フィルター | MIME タイプ | レンディション |
| --- | --- | --- | --- |
| Dynamic Media 画像配信 | filter-image<br>filter-sets | **image/**<br> で始まり、**applications/** を含み、**set** で終わる | 標準の「filter-images」（インタラクティブ画像を含む、単一の画像アセットに適用される）および「filter-sets」（スピンセット、画像セット、混在メディアセットおよびカルーセルセットに適用される）は、以下の操作を実行します。<br>• 元の画像および静的な画像のレンディションをレプリケーションから除外します。 |
| ダイナミックメディアビデオ配信 | filter-video | **video/** で始まる | 標準の「filter-video」は、以下の操作を実行します。<br>• 元のビデオと静的なサムネールのレンディションをレプリケーションから除外します。 |

>[!NOTE]
フィルターは、MIME タイプに適用されます。パスを指定することはできません。

#### レプリケーション用のアセットフィルターのカスタマイズ {#customizing-asset-filters-for-replication}

1. Experience Manager で、Experience Manager のロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL CRXDE Lite]** に移動します。
1. 左側のフォルダーツリーで、`/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` に移動し、フィルターを確認します。

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. フィルターの MIME タイプを定義するために、次のように MIME タイプを特定することができます。

   左側のレールで、 `content > dam > <locate_your_asset> > jcr:content > metadata`を展開し、テーブルで`dc:format`を見つけます。

   次の図は、あるアセットの`dc:format`へのパスの例を示しています。

   ![chlimage_1-18](assets/chlimage_1-3.png)

   アセット`Fiji Red.jpg`の`dc:format`が`image/jpeg`となっています。

   このフィルターを形式に関係なくすべての画像に適用するには、値を `image/*` に設定します。`*` は、あらゆる形式のすべての画像に適用される正規表現です。

   このフィルターを JPEG タイプの画像のみに適用するには、`image/jpeg` という値を入力します。

1. レプリケーションに含める、または除外するレンディションを定義します。

   レプリケーション用のフィルターに使用できる文字は次のとおりです。

   | 使用する文字 | レプリケーション用のアセットのフィルター方法 |
   | --- | --- |
   | * | ワイルドカード文字 |
   | + | レプリケーション用にアセットを含める |
   | - | レプリケーションからアセットを除外する |

   `content/dam/<locate your asset>/jcr:content/renditions` に移動します。

   次の図は、あるアセットのレンディションの例を示しています。

   ![chlimage_1-4](assets/chlimage_1-4.png)

   オリジナルのみをレプリケートする場合は、「`+original`」と入力します。
