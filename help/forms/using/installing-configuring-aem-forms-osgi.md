---
title: データ取得機能をインストールして設定する
seo-title: データ取得機能をインストールして設定する
description: アダプティブフォーム、PDF フォームおよび HTML5 フォームをインストールして設定します。アダプティブフォーム用に Adobe Analytics および Adobe Target を設定して、プロファイルに基づいてフォームの使用状況を分析し、対象ユーザーを絞ります。
seo-description: アダプティブフォーム、PDF フォームおよび HTML5 フォームをインストールして設定します。アダプティブフォーム用に Adobe Analytics および Adobe Target を設定して、プロファイルに基づいてフォームの使用状況を分析し、対象ユーザーを絞ります。
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
role: Administrator
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 76%

---

# データ取得機能をインストールして設定する{#install-and-configure-data-capture-capabilities}

## はじめに {#introduction}

AEM Forms は、エンドユーザーからデータを取得するためのアダプティブフォーム、HTML5 フォームおよび PDF フォームのフォームセットを提供します。また、Web ページ上の利用可能なすべてのフォームを一覧表示し、フォームの使用状況を分析して対象ユーザーを絞るためのツールも提供します。これらの機能は、AEM Forms のアドオンパッケージに含まれています。アドオンパッケージは、AEM のオーサーインスタンスまたはパブリッシュインスタンスに展開されます。

**アダプティブフォーム：**&#x200B;インタラクティブで魅力的なこのフォームは、デバイスの画面サイズに基づいて外観を変更できます。また、アダプティブフォームは Adobe Analytics、Adobe Sign および Adobe Target と統合できます。これにより、人口統計やその他の機能に基づいて、パーソナライズされたフォームとプロセス志向のエクスペリエンスをユーザーに提供できます。さらに、アダプティブフォームを Adobe Sign に統合することも可能です。

**PDF フォーム**&#x200B;は、ピクセルパーフェクトな印刷と、PDF 文書内でのデジタル情報取得に適しています。デジタルアバターでは、Adobe Acrobat または Acrobat Reader を使用して PDF フォームを入力できます。このフォームを Web サイト上でホストするか、フォームポータルを使用して AEM サイト上に一覧表示できます。また、このフォームを添付ファイルとして他のユーザーに電子メールで送ることもできます。PDF フォームはデスクトップ環境に最適です。

**HTML5 フォーム**&#x200B;は、PDF フォームのブラウザーで使いやすいバージョンです。HTML5 フォームは、PDF プラグインをサポートしていない環境に適しています。HTML5 フォームにより、XFA ベースの PDF がサポートされていないモバイルデバイスおよびデスクトップブラウザー上の、XFA ベースのフォームのレンダリングが可能です。このフォームはタブレットおよびデスクトップ環境に最適です。

AEM Forms は強力なエンタープライズクラスのプラットフォームで、データ取得（アダプティブフォーム、PDF フォームおよび HTML5 フォーム）機能は AEM Forms のみが持つ機能の 1 つです。機能の完全な一覧については、「[AEM Forms の概要](/help/forms/using/introduction-aem-forms.md)」を参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。AEM Forms のデータ取得機能を実行するには、少なくとも 1 つの AEM オーサーインスタンスおよび AEM パブリッシュインスタンスのみを必要とします。AEM Forms のデータ取得機能を実行するには、次のトポロジーを推奨します。トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![推奨トポロジ](assets/recommended-topology.png)

## システム要件 {#system-requirements}

AEM Formsのデータキャプチャ機能のインストールと設定を開始する前に、次の点を確認してください。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアおよびソフトウェアの詳細な一覧については、「[技術的要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。Windowsユーザーの場合は、管理者権限モードでAEMインスタンスをインストールします。 AEM の用語では、「インスタンス」は、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。AEM Forms のデータ取得機能を実行するには、少なくとも 2 つの [AEM インスタンス（1 つはオーサー、もう 1 つはパブリッシュ）](/help/sites-deploying/deploy.md)を必要とします。

   * **オーサー：**&#x200B;コンテンツを作成、アップロード、編集し、Web サイトを管理する AEM インスタンス。公開する準備ができたコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **パブリッシュ：**&#x200B;発行されたコンテンツをインターネットまたは社内ネットワークを通じて公開する AEM インスタンス。

* メモリ要件が満たされていること。AEM Forms アドオンパッケージには次の一時領域が必要となります。

   * Microsoft Windows ベースのインストールの場合、15 GB の一時的な空きスペースが必要です。
   * Unix ベースのインストールの場合、6 GB の一時的な空きスペースが必要です。

* オーサーインスタンスとパブリッシュインスタンスに対して複製と逆複製が設定されていること。詳しくは、「[複製](/help/sites-deploying/replication.md)」を参照してください。
* UNIXベースのシステムの場合：

   * 次の32ビットパッケージをインストールメディアからインストールします。

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>リビク</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* OpenSSLが既にサーバーにインストールされている場合は、最新バージョンにアップグレードします。
>* libcurl.so、libcrypto.so、libssl.soシンボリックリンクを作成し、それぞれlibcurl、libcrypto、libsslライブラリの最新バージョンを指定します。

>



* 次の64ビットパッケージをインストールメディアからインストールします。

   * リビク

## AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。このパッケージには、AEM Forms データ取得およびその他の機能が含まれています。次の手順を実行してアドオンパッケージをインストールします。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 **[!UICONTROL ダウンロードの検索]**&#x200B;オプションを使用して、結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージ名をタップし、「**[!UICONTROL EULA利用条件]**&#x200B;に同意し、**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

   [AEM Formsリリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)の記事に記載されている直接リンクからパッケージをダウンロードすることもできます。
1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**すぐにはサーバーを再起動しないでください。** AEM Formsサーバーを停止する前に、 ServiceEvent REGISTEREDメッセージとServiceEvent UNREGISTEREDメッセージがファイルに表示されなくな `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` り、ログが安定するまで待ちます。
1. 手順 1 から 7 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### （Windowsのみ）Visual Studioの再頒布可能パッケージの自動インストール{#automatic-installation-visual-studio-redistributables}

AEMインスタンスを管理者権限モードでインストールした場合、見つからないVisual Studioの再配布可能パッケージは、AEM Formsアドオンパッケージのインストール中に自動的にインストールされます。

Visual Studioの再配布可能ファイルが自動的にインストールされているかどうかを評価するには、`/crx-repository/logs/`ディレクトリにある`error.log`ファイルを開きます。 ログには次のメッセージが含まれます。

`Redist <service name> already installed on system, will not attempt re-installation`

再頒布可能パッケージをインストールできない場合、ログには次のメッセージが含まれます。

`Current user does not have elevated privileges, aborting installation of redist <service name>`

この問題を解決するには、AEMサーバーを再起動し、AEMを管理者特権モードでインストールしてから、AEM Formsアドオンパッケージをインストールします。

権限チェックが失敗した場合、ログには次のメッセージが含まれます。

`Privilege escalation check failed with error: <error message>`

## インストール後の設定 {#post-installation-configurations}

AEM Forms には、いくつかの必須およびオプションの設定があります。必須の設定には、BouncyCastle ライブラリおよびシリアル化エージェントの設定が含まれます。オプションの設定には、ディスパッチャー、フォームポータル、Adobe Sign、Adobe Analytics および Adobe Target の設定が含まれます。

### インストール後の必須の設定 {#mandatory-post-installation-configurations}

#### RSA ライブラリと BouncyCastle ライブラリの設定  {#configure-rsa-and-bouncycastle-libraries}

すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行し、ライブラリの委任を起動します。

1. 基になる AEM インスタンスを停止します。
1. `[AEM installation directory]\crx-quickstart\conf\sling.properties`ファイルを開いて編集します。

   `[AEM installation directory]\crx-quickstart\bin\start.bat`を使用してAEMを起動した場合は、`[AEM_root]\crx-quickstart\`にあるsling.propertiesを編集します。

1. 以下のプロパティを sling.properties ファイルに追加します。

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. ファイルを保存して閉じ、AEM インスタンスを起動します。
1. 手順 1 から 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

#### シリアル化エージェントの設定 {#configure-the-serialization-agent}

すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行し、パッケージをに追加許可リストします。

1. ブラウザーウィンドウで、AEM Configuration Manager を開きます。デフォルトの URL は `https://'[server]:[port]'/system/console/configMgr` です。
1. **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name**&#x200B;を探し、設定を開きます。
1. **sun.util.calendar**&#x200B;パッケージを&#x200B;**許可リスト**&#x200B;フィールドに追加します。 「**保存**」をクリックします。
1. 手順 1 から 3 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### インストール後のオプションの設定 {#optional-post-installation-configurations}

#### Dispatcher の設定 {#configure-dispatcher}

Dispatcherは、Adobe Experience Managerのキャッシュやロードバランシングを行うツールで、エンタープライズクラスのWebサーバーと組み合わせて使用できます。 [Dispatcher](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html)を使用する場合は、AEM Formsに対して次の設定を実行します。

1. AEM Forms のアクセスの設定:

   dispatcher.any ファイルを開いて編集します。フィルターセクションに移動し、次のフィルターをフィルターセクションに追加します。

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   ファイルを保存して閉じます。フィルターについて詳しくは、「[ディスパッチャードキュメント](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)」を参照してください。

1. リファラーフィルターサービスの設定：

   管理者として Apache Felix Configuration Manager にログインします。Configuration ManagerのデフォルトURLは`https://[server]:[port_number]/system/console/configMgr`です。 **Configurations**&#x200B;メニューで「**Apache Sling Referrer Filter**」を選択します。「Allow Hosts」フィールドで、ディスパッチャーのホスト名を入力してそれをリファラーとして許可し、「**保存**」をクリックします。エントリの形式は、「https://[server]:[port]」です。

#### キャッシュの設定 {#configure-cache}

キャッシングは、データへのアクセスにかかる時間を短縮し、遅延を削減して I/O 速度を改善するメカニズムです。アダプティブフォームのキャッシュは、アダプティブフォームの HTML コンテンツと JSON の構造のみを保存し、事前入力されたデータは保存しません。これにより、アダプティブフォームのレンダリングの時間を短縮します。

* アダプティブフォームのキャッシュを使用するときは、[AEM ディスパッチャー](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) を使用してアダプティブフォームのクライアントライブラリ（CSS および JavaScript）をキャッシュします。
* カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。

アダプティブフォームのキャッシュを設定するには、以下の手順を実行します。

1. https://&#39;[server]:[port]&#39;/system/console/configMgrでAEM Web Console Configuration Managerに移動します。
1. 「**アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定**」をクリックして、設定値を編集します。設定値を編集ダイアログで、「**アダプティブFormsの数**」フィールドに、AEM Formsサーバーのインスタンスでキャッシュできるフォームまたはドキュメントの最大数を指定します。 デフォルト値は 100 です。「**保存**」をクリックします。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュ設定を無効にしたり変更したりすると、キャッシュがリセットされ、すべてのフォームとドキュメントがキャッシュから削除されます。

#### フォームデータモデルに SSL 通信を設定する {#configure-ssl-communcation-for-form-data-model}

フォームデータモデル用の SSL 通信を有効にすることができます。フォームデータモデル用の SSL 通信を有効にするには、任意の AEM Forms インスタンスを起動する前に、すべてのインスタンスの Java Trust Store に証明書を追加します。次のコマンドを実行して、証明書を追加できます。&quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Adobe Sign の設定 {#configure-adobe-sign}

Adobe Sign により、アダプティブフォームの電子署名ワークフローを有効にすることができます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

Adobe Sign とアダプティブフォームの一般的なシナリオでは、**サービスを申し込む**&#x200B;ためのアダプティブフォームをユーザーが入力します。例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームの入力、送信、署名を行うと、サービスプロバイダーにそのフォームが送信され、追加の処理が実行されます。サービスプロバイダーは受信した申込フォームを確認し、Adobe Sign を使用してそのフォームを承認します。これに類似した電子署名ワークフローを有効にするには、Adobe Sign を AEM Forms に統合します。

AEM Forms で Adobe Sign を使用するには、「[Adobe Sign を AEM Forms に統合する](/help/forms/using/adobe-sign-integration-adaptive-forms.md)」を参照してください。

#### Adobe Analytics の設定  {#configure-adobe-analytics}

AEM Forms は、Adobe Analytics と統合されているため、発行済みのフォームとドキュメントのパフォーマンス指標を取得および追跡できます。これらの指標分析の意図は、フォームやドキュメントをさらに有効利用するために必要な変更に関して十分な情報に基づいた決定を行えるよう支援することです。

AEM Forms で Adobe Analytics を使用するには、「[分析とレポートの設定](/help/forms/using/configure-analytics-forms-documents.md)」を参照してください。

#### Adobe Target の統合 {#integrate-adobe-target}

顧客は、フォームのエクスペリエンスに魅力がない場合、フォームを放棄してしまいます。また、フォームが顧客にとって使いにくい場合は、サポート量が増加し組織のコストが膨らむことになります。コンバージョン率を向上させる顧客体験を正しく認識して提供することは、難題であると同時に非常に重要です。この問題を解決するキーは AEM Forms にあります。

AEM Forms は Adobe Marketing Cloud ソリューションである Adobe Target と統合することで、個々の顧客に対応した魅力的な顧客体験を、複数のデジタルチャネルにわたって提供します。Adobe TargetをA/Bテスト用のアダプティブフォームに使用するには、[Adobe TargetをAEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)と統合します。

## 次の手順 {#next-steps}

AEM Forms のデータ取得機能を使用するための環境を設定しました。この機能を使用するための手順は、次のとおりです。

* [最初のアダプティブフォームを作成する](/help/forms/using/create-your-first-adaptive-form.md)
* [最初の PDF フォームを作成する](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65_jp)
* [HTML5 フォームの概要](/help/forms/using/introduction.md)
