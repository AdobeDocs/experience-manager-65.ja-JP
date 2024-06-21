---
title: データ取得機能をインストールして設定する
description: アダプティブフォーム、PDF フォームおよび HTML5 フォームをインストールして設定します。アダプティブフォーム用に Adobe Analytics および Adobe Target を設定して、プロファイルに基づいてフォームの使用状況を分析し、対象ユーザーを絞ります。
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin, User, Developer
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, OSGI
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 100%

---

# データ取得機能をインストールして設定する{#install-and-configure-data-capture-capabilities}

## はじめに {#introduction}

AEM Forms は、エンドユーザーからデータを取得するためのアダプティブフォーム、HTML5 フォームおよび PDF フォームのフォームセットを提供します。また、web ページ上の利用可能なすべてのフォームを一覧表示し、フォームの使用状況を分析して対象ユーザーを絞るためのツールも提供します。これらの機能は、AEM Forms のアドオンパッケージに含まれています。アドオンパッケージは、AEM のオーサーインスタンスまたはパブリッシュインスタンスにデプロイされます。

**アダプティブフォーム**：インタラクティブで魅力的なこのフォームは、デバイスの画面サイズに基づいて外観を変更できます。アダプティブフォームは、Adobe Analytics、Adobe Sign、Adobe Target とも統合できます。これにより、人口統計やその他の機能に基づいて、パーソナライズされたフォームとプロセス志向のエクスペリエンスをユーザーに提供できます。さらに、アダプティブフォームを Adobe Sign に統合することも可能です。

**PDF フォーム**&#x200B;は、ピクセルパーフェクトな印刷と、PDF ドキュメント内でのデジタル情報取得に適しています。デジタルアバターでは、Adobe Acrobat または Acrobat Reader を使用してフォームを入力できます。このフォームを web サイト上でホストするか、フォームポータルを使用して AEM サイト上に一覧表示できます。また、このフォームを添付ファイルとして他のユーザーにメールで送ることもできます。このフォームはデスクトップ環境に最適です。

**HTML5 フォーム**&#x200B;は、、PDF フォームをブラウザーで使いやすくしたバージョンです。HTML5 Forms は、PDF プラグインをサポートしていない環境に適しています。HTML5 Forms により、XFA ベースの PDF がサポートされていないモバイルデバイスおよびデスクトップブラウザー上の、XFA ベースのフォームのレンダリングが可能です。このフォームはタブレットおよびデスクトップ環境に最適です。

AEM Forms は強力なエンタープライズクラスのプラットフォームで、データキャプチャ（アダプティブフォーム、PDF フォームおよび HTML5 フォーム）機能は AEM Forms のみが持つ機能の 1 つです。機能の完全な一覧については、「[AEM Forms の概要](/help/forms/using/introduction-aem-forms.md)」を参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。AEM Forms のデータキャプチャ機能を実行するには、少なくとも 1 つの AEM オーサーインスタンスおよび AEM パブリッシュインスタンスのみを必要とします。AEM Forms のデータキャプチャ機能を実行するには、次のトポロジを推奨します。トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![推奨トポロジ](assets/recommended-topology.png)

## システム要件 {#system-requirements}

AEM Forms のデータ取得機能をインストールして設定する前に、次のことを確認する必要があります。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアとソフトウェアの一覧について詳しくは、「[技術要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。Windows ユーザーの場合は、昇格されたモードで AEM インスタンスをインストールします。AEM の用語では、「インスタンス」は、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。AEM Forms のデータキャプチャ機能を実行するには、少なくとも 2 つの [AEM インスタンス（1 つはオーサー、もう 1 つはパブリッシュ）](/help/sites-deploying/deploy.md)を必要とします。

   * **オーサー**：コンテンツの作成、アップロードおよび編集や web サイトの管理に使用される AEM インスタンス。公開の準備が整ったコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **パブリッシュ**：公開されたコンテンツをインターネットまたは社内ネットワークを通じて提供する AEM インスタンス。

* メモリ要件が満たされていること。AEM Forms アドオンパッケージでは、次が必要です。

   * Microsoft Windows ベースのインストールの場合、15 GB の一時的な空きスペースが必要です。
   * Unix ベースのインストールの場合、6 GB の一時的な空きスペースが必要です。

* オーサーインスタンスとパブリッシュインスタンスに対してレプリケーションとリバースレプリケーションが設定されていること。詳しくは、[レプリケーション](/help/sites-deploying/replication.md)を参照してください。
* UNIX ベースのシステムの場合：

   *  インストールメディアから次の 32 ビット版パッケージをインストールします。

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
   <td>llibicu</td>
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
>* OpenSSL が既にサーバーにインストールされている場合は、最新バージョンにアップグレードします。
>* libcurl.so、libcrypto.so、libssl.so シンボリックリンクを作成し、それぞれ libcurl、libcrypto、libssl ライブラリの最新バージョンを指します。
>

* インストールメディアから、次の 64 ビット版パッケージをインストールします。

   * llibicu

* [32 ビット版の Microsoft Visual Studio 2019 再頒布可能パッケージ](https://learn.microsoft.com/ja-jp/cpp/windows/latest-supported-vc-redist?view=msvc-170)をインストールします。


## AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。このパッケージには、AEM Forms のデータキャプチャおよびその他の機能が含まれています。次の手順を実行してアドオンパッケージをインストールします。

1. [ソフトウェア配布](https://experience.adobe.com/jp/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」を選択します。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適した Forms アドオンパッケージの名前を選択し、「**[!UICONTROL EULA 利用条件に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」を選択します。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して「**[!UICONTROL インストール]**」をクリックします。

   [AEM Forms リリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)の記事に記載されている直接リンクからパッケージをダウンロードすることもできます。
1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**サーバーをすぐに再起動しないでください。** AEM Forms サーバーを停止する前に、ServiceEvent REGISTERED メッセージと ServiceEvent UNREGISTERED メッセージが `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` ファイルに表示されなくなり、このログファイルが安定した状態になるまで待ってください。

   >[!NOTE]
   >
   > SDK を再起動するには、「Ctrl + C」コマンドを使用することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

1. 手順 1 から 7 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### （Windows のみ）Visual Studio の再配布可能な自動インストール {#automatic-installation-visual-studio-redistributables}

AEM インスタンスを権限昇格モードでインストールすると、AEM Forms アドオンパッケージのインストール時に、32 ビット版の Visual Studio 再頒布可能パッケージ ファイルが自動的にインストールされます。

Visual Studio の再配布可能パッケージが自動的にインストールされているかを評価するには、`/crx-repository/logs/` ディレクトリにある `error.log` ファイルを開きます。ログには次のメッセージが含まれます。

`Redist <service name> already installed on system, will not attempt re-installation`

再配布可能パッケージのインストールに失敗した場合、ログには次のメッセージが含まれます。

`Current user does not have elevated privileges, aborting installation of redist <service name>`

問題を解決するには、AEM サーバーを再起動し、権限昇格モードで AEM をインストールし、AEM Forms アドオンパッケージをインストールします。

権限チェックが失敗した場合、ログには次のメッセージが表示されます。

`Privilege escalation check failed with error: <error message>`

## インストール後の設定 {#post-installation-configurations}

AEM Forms には、必須の設定とオプションの設定がいくつかあります。必須の設定には、BouncyCastle ライブラリおよびシリアル化エージェントの設定が含まれます。オプションの設定には、ディスパッチャー、フォームポータル、Adobe Sign、Adobe Analytics および Adobe Target の設定が含まれます。

### インストール後の必須の設定 {#mandatory-post-installation-configurations}

#### RSA ライブラリと BouncyCastle ライブラリの設定  {#configure-rsa-and-bouncycastle-libraries}

これらのライブラリを起動するには、すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行します。 

1. 基になる AEM インスタンスを停止します。
1. `[AEM installation directory]\crx-quickstart\conf\sling.properties` ファイルを編集用に開きます。

   `[AEM installation directory]\crx-quickstart\bin\start.bat` を使用して AEM インスタンスを起動する場合は、`[AEM_root]\crx-quickstart\` にある sling.properties ファイルを編集します。

1. 以下のプロパティを sling.properties ファイルに追加します。

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. ファイルを保存して閉じ、AEM インスタンスを起動します。
1. 手順 1 ～ 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

#### シリアル化エージェントの設定 {#configure-the-serialization-agent}

このパッケージを許可リストに加えるには、オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. ブラウザーウィンドウで、AEM Configuration Manager を開きます。デフォルトの URL は `https://'[server]:[port]'/system/console/configMgr` です。
1. **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** を検索し、設定を開きます。
1. **sun.util.calendar** パッケージを「**許可リストに加える**」フィールドに追加します。「**保存**」をクリックします。
1. 手順 1 ～ 3 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### インストール後のオプションの設定 {#optional-post-installation-configurations}

#### Dispatcher の設定 {#configure-dispatcher}

Dispatcher は、Adobe Experience Manager のキャッシュやロードバランシングツールで、企業向けの Web サーバーと組み合わせて使用できます。[Dispatcher](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html) を使用する場合は、AEM Forms で次の設定を実行してください。

1. AEM Forms のアクセスの設定：

   dispatcher.any ファイルを開いて編集します。フィルターセクションに移動し、次のフィルターをフィルターセクションに追加します。

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   ファイルを保存して閉じます。フィルターについて詳しくは、[Dispatcher のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja)を参照してください。

1. リファラーフィルターサービスの設定：

   Apache Felix Configuration Manager に管理者としてログインします。Configuration Manager のデフォルト URL は `https://[server]:[port_number]/system/console/configMgr` です。**Configurations**&#x200B;メニューで「**Apache Sling Referrer Filter**」を選択します。「Allow Hosts」フィールドで、ディスパッチャーのホスト名を入力してそれをリファラーとして許可し、「**保存**」をクリックします。URL の形式は、`https://[server]:[port]` です。

#### キャッシュを設定 {#configure-cache}

キャッシュは、データへのアクセスにかかる時間を短縮し、待ち時間を削減して I/O（入出力）速度を改善するメカニズムです。アダプティブフォームのキャッシュは、アダプティブフォームの HTML コンテンツと JSON の構造のみを保存し、事前入力されたデータは保存しません。これにより、アダプティブフォームのレンダリングの時間を短縮します。

* アダプティブフォームのキャッシュを使用するときは、[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja) を使用してアダプティブフォームのクライアントライブラリ（CSS および JavaScript）をキャッシュします。
* カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。

次の手順を実行してアダプティブフォームのキャッシュを設定します。

1. AEM Web コンソール Configuration Manager（https://&#39;[server]:[port]&#39;/system/console/configMgr）に移動します。
1. 「**アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定**」をクリックして、設定値を編集します。設定値を編集ダイアログで、AEM Forms サーバーのインスタンスでキャッシュできるフォームまたはドキュメントの最大数を「**アダプティブフォームの数**」フィールドに指定します。デフォルト値は 100 です。「**保存**」をクリックします。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュ設定を無効にしたり変更したりすると、キャッシュがリセットされ、すべてのフォームとドキュメントがキャッシュから削除されます。

#### フォームデータモデルに SSL 通信を設定 {#configure-ssl-communcation-for-form-data-model}

フォームデータモデルの SSL 通信を有効にすることができます。フォームデータモデルの SSL 通信を有効にするには、任意の AEM Forms インスタンスを起動する前に、すべてのインスタンスの Java Trust Store に証明書を追加します。次のコマンドを実行して証明書を追加することができます。 ``

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Adobe Sign を設定 {#configure-adobe-sign}

Adobe Sign では、アダプティブフォームの電子サインワークフローを有効にすることができます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

Adobe Sign とアダプティブフォームの一般的なシナリオでは、**サービスを申し込む**&#x200B;ためのアダプティブフォームをユーザーが入力します。例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームの入力、送信、署名を行うと、追加のアクションのためにサービスプロバイダーにそのフォームが送信されます。サービスプロバイダーは申込フォームを確認し、Adobe Sign を使用して申請を承認します。これに類似した電子署名ワークフローを有効にするには、Adobe Sign を AEM Forms に統合します。

AEM Forms で Adobe Sign を使用するには、[Adobe Sign を AEM Forms に統合](/help/forms/using/adobe-sign-integration-adaptive-forms.md)を参照してください。

#### Adobe Analytics の設定 {#configure-adobe-analytics}

AEM Forms は、Adobe Analytics と統合されているため、公開済みのフォームとドキュメントのパフォーマンス指標を取得および追跡できます。これらの指標分析の意図は、フォームやドキュメントをさらに使いやすくするために必要な変更に関して、十分な情報に基づいた決定を行えるよう支援することです。

AEM Forms で Adobe Analytics を使用するには、「[分析とレポートの設定](/help/forms/using/configure-analytics-forms-documents.md)」を参照してください。

#### Adobe Target を統合 {#integrate-adobe-target}

顧客は、フォームのエクスペリエンスに魅力がない場合、フォームを放棄してしまいます。顧客にとって不満が生じる一方で、組織のサポート量とコストが増加する可能性もあります。コンバージョン率を向上させるカスタマーエクスペリエンス（顧客体験）を正しく認識して提供することは非常に重要であり、難題でもあります。この問題を解決する鍵は AEM Forms にあります。

AEM Forms は Adobe Marketing Cloud ソリューションである Adobe Target と統合することで、個々の顧客に合わせてパーソナライズした魅力的な顧客体験を、複数のデジタルチャネルにわたって提供します。Adobe Target を A/B テストのアダプティブフォームに対して使用するには、「[Adobe Target を AEM Forms に統合する](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)」を参照してください。 

## 次の手順 {#next-steps}

AEM Forms のデータキャプチャ機能を使用する環境を設定しました。この機能を使用するための次の手順は、以下のとおりです。

* [最初のアダプティブフォームを作成する](/help/forms/using/create-your-first-adaptive-form.md)
* [最初の PDF フォームを作成する](https://www.adobe.com/go/learn_aemforms_designer_quick_start_65_jp)
* [HTML5 フォームの概要](/help/forms/using/introduction.md)
