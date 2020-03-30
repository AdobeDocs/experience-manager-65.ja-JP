---
title: インタラクティブ通信をインストールして設定する
seo-title: インタラクティブ通信をインストールして設定する
description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
seo-description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# インタラクティブ通信をインストールして設定する{#install-and-configure-interactive-communications}

## 概要 {#introduction}

AEM Formには、ビジネス通信、ドキュメント、明細書、福利厚生通知、マーケティングメール、請求書、ウェルカムキットなど、安全でインタラクティブなドキュメントの作成、アセンブリ、管理、配信を一元化する機能があります。 この機能は、インタラクティブ通信として知られています。これは、AEM Forms のアドオンパッケージに含まれる機能で、アドオンパッケージは、AEM のオーサーインスタンスまたはパブリッシュインスタンスに展開されます。

インタラクティブ通信機能を使用して、複数形式で通信を作成できます。例えば、Web や PDF です。インタラクティブ通信を AEM ワークフローと統合して、アセンブリした通信を処理し、選択したチャネルの顧客に配信することができます。例えば、電子メールを介してエンドユーザーに通信を送信します。

If you are upgrading from a previous version and have already invested in correspondence management, you can install the [compatibility package](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) to continue using correspondence management. インタラクティブ通信と Correspondence management の違いについて詳しくは、「[インタラクティブ通信の概要](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management)」を参照してください。

AEM Forms は強力なエンタープライズクラスのプラットフォームです。インタラクティブ通信は、AEM Forms のみが持つ機能の 1 つです。機能の完全な一覧については、「[AEM Forms の概要](../../forms/using/introduction-aem-forms.md)」を参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。インタラクティブ通信機能を実行するには、少なくとも 1 つの AEM Author および処理インスタンスのみを必要とします。次のトポロジは、AEM Forms のインタラクティブ通信、Correspondence Management、AEM Forms のデータ取得および OSGi 機能にあるフォーム中心のワークフローを実行するための指標トポロジです。トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![推奨トポロジー](assets/recommended-topology.png)

AEM Forms のインタラクティブ通信は、AEM Forms のオーサーインスタンスで管理者、オーサリングおよびエージェントのユーザーインターフェイスを実行します。パブリッシュインスタンスは、エンドユーザが使用できるようになっているインタラクティブ通信の最終バージョンをホストします。

## システム要件 {#system-requirements}

AEM Formsのインタラクティブな通信および通信管理機能をインストールおよび設定する前に、次のことを確認します。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアおよびソフトウェアの詳細な一覧については、「[技術的要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。AEM の用語では、「インスタンス」は、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。AEM Formsのインタラクティブな通信および通信管理機能を実行するには、少なくとも1つのAEMインスタンス（作成者または処理）が必要です。

   * **作成者：**&#x200B;コンテンツを作成、アップロード、編集し、Web サイトを管理する AEM インスタンス。公開する準備ができたコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **処理：**&#x200B;処理インスタンスは、[強化された AEM オーサー](/help/forms/using/hardening-securing-aem-forms-environment.md)インスタンスです。インストールの実行後に、作成者インスタンスを設定し、強化することができます。

   * **パブリッシュ**：発行されたコンテンツをインターネットまたは社内ネットワークを通じて公開する AEM インスタンス。

* メモリ要件が満たされていること。AEM Forms アドオンパッケージには次の一時領域が必要となります。

   * Microsoft Windows ベースのインストールの場合、15 GB の一時的な空きスペースが必要です。
   * Unix ベースのインストールの場合、6 GB の一時的な空きスペースが必要です。

* Unix ベースのシステムの追加必要システム構成：Unix ベースのオペレーティングシステムを使用する場合は、それぞれのオペレーティングシステムのインストールメディアから、次のパッケージをインストールしてください。

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。このパッケージには、AEM Formsのインタラクティブな通信、Correspondence Management、その他の機能が含まれています。 次の手順を実行してアドオンパッケージをインストールします。

1. [AEM サーバー](https://localhost:4502)に管理者としてログインし、「[パッケージ共有](https://localhost:4502/crx/packageshare)」を開きます。パッケージ共有にログインするには、Adobe ID が必要です。
1. [AEM パッケージ共有](https://localhost:4502/crx/packageshare/login.html)で、**AEM 6.5 Forms アドオンパッケージ**&#x200B;または&#x200B;**最新のサービスパック**&#x200B;を検索し、お使いのオペレーティングシステムに対応するパッケージをクリックして、「**ダウンロード**」をクリックします。ライセンス使用許諾契約書を読んでから同意し、「**OK**」をクリックします。ダウンロードが開始します。ダウンロードが完了したら、パッケージの横に「**ダウンロード済み**」というテキストが表示されます。

   バージョン番号を使用してアドオンパッケージを検索することもできます。最新のパッケージのバージョン番号については、「[AEM Forms リリース](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)」の記事を参照してください。

1. ダウンロードが完了したら、「**ダウンロード済み**」をクリックします。パッケージマネージャーに切り替わります。In the package manager, search the downloaded package, and click **Install**.

   「[AEM Forms リリース](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)」記事に記載された直接リンクからパッケージを手動でダウンロードする場合は、パッケージマネージャーにログインし、「**パッケージをアップロード**」をクリックし、ダウンロード済みパッケージを選択して「アップロード」をクリックします。パッケージのアップロードが完了したら、パッケージ名をクリックし、「**インストール**」をクリックします。

1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**すぐにはサーバーを再起動しないでください。** AEM Formsサーバーを停止する前に、ServiceEvent REGISTEREDおよびServiceEvent UNREGISTEREDメッセージが [AEM-Installation-Directory]/crx-quickstart/logs/error.logファイルに表示されなくなるまで待ち、ログは安定しています。
1. 手順 1 から 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

## インストール後の設定 {#post-installation-configurations}

AEM Forms には、いくつかの必須およびオプションの設定があります。必須の設定には、BouncyCastle ライブラリおよびシリアル化エージェントの設定が含まれます。オプションの設定には、ディスパッチャーおよび Adobe Target の設定が含まれます。

### インストール後の必須の設定 {#mandatory-post-installation-configurations}

#### RSA ライブラリと BouncyCastle ライブラリの設定  {#configure-rsa-and-bouncycastle-libraries}

すべての作成者インスタンスと発行インスタンスで次の手順を実行し、ライブラリをブート委任します。

1. 基になる AEM インスタンスを停止します。
1. Open the [AEM installation directory]\crx-quickstart\conf\sling.properties file for editing.

   [AEMのインストールディレクトリ]\crx-quickstart\bin\start.batをAEMの開始に使用した場合は、 [AEM_root]\crx-quickstart\にあるsling.propertiesを編集します。

1. 以下のプロパティを sling.properties ファイルに追加します。 

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. ファイルを保存して閉じ、AEM インスタンスを起動します。
1. 手順 1 から 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

#### シリアル化エージェントの設定 {#configure-the-serialization-agent}

すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行し、パッケージをホワイトリストに登録します。

1. ブラウザーウィンドウで、AEM Configuration Manager を開きます。The default URL is https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. **デシリアライゼーションファイアウォール設定**&#x200B;を検索して開きます。
1. **sun.util.calendar**&#x200B;パッケージを&#x200B;**ホワイトリスト**&#x200B;フィールドに追加します。「保存」をクリックします。
1. 手順 1 から 3 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### インストール後のオプションの設定 {#optional-post-installation-configurations}

#### 互換性パッケージをインストールする {#install-compatibility-package}

インタラクティブ通信は、顧客通信を作成するためのデフォルトの方法です。AEM 6.5 Forms で顧客通信を作成する場合は、インタラクティブ通信を使用することを推奨します。以前のバージョンからアップグレードまたは移行を行って、引き続きレター（Correspondence Management）を使用する予定の場合は、[AEMFD 互換性パッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT)をインストールします。

AEMFD互換性パッケージを使用すると、AEM 6.5 Forms上のAEM 6.4 Forms、AEM 6.3 FormsおよびAEM 6.2 Formsの次のアセットを使用できます。

* ドキュメントフラグメント
* レター
* データディクショナリ
* アダプティブフォームの非推奨になったテンプレートおよびページ

#### Dispatcher の設定 {#configure-dispatcher}

ディスパッチャーは AEM のキャッシングおよびロードバランスツールです。AEM ディスパッチャーはまた、AEM サーバーを攻撃から保護することにも役立ちます。エンタープライズクラスの Web サーバーと一緒にディスパッチャーを使用することで、AEM インスタンスのセキュリティを向上できます。If you use [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), then perform the following configurations for AEM Forms:

1. AEM Forms のアクセスの設定:

   dispatcher.any ファイルを開いて編集します。フィルターセクションに移動し、次のフィルターをフィルターセクションに追加します。

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   ファイルを保存して閉じます。フィルターについて詳しくは、「[ディスパッチャードキュメント](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)」を参照してください。

1. リファラーフィルターサービスの設定：

   管理者として Apache Felix Configuration Manager にログインします。The Default URL of the configuration manager is https://&#39;server&#39;:[port_number]/system/console/configMgr. **Configurations**&#x200B;メニューで「**Apache Sling Referrer Filter**」を選択します。「Allow Hosts」フィールドで、ディスパッチャーのホスト名を入力してそれをリファラーとして許可し、「**保存**」をクリックします。The format of the entry is https://&#39;[server]:[port]&#39;.

#### Adobe Target の統合 {#integrate-adobe-target}

顧客は、対話型コミュニケーションのエクスペリエンスに魅力がない場合、これを放棄してしまいます。また、フォームが顧客にとって使いにくい場合は、サポート量が増加し組織のコストが膨らむことになります。コンバージョン率を向上させる顧客体験を正しく認識して提供することは非常に重要であり、難題でもあります。この問題を解決するキーは AEM Forms にあります。

AEM Forms は Adobe Marketing Cloud ソリューションである Adobe Target と統合することで、個々の顧客に対応した魅力的な顧客体験を、複数のデジタルチャネルにわたって提供します。To use Adobe Target to personalize an interactive communication, [Integrate Adobe Target with AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### フォームデータモデルに SSL 通信を設定する  {#configure-ssl-communcation-for-form-data-model}

フォームデータモデル用の SSL 通信を有効にすることができます。フォームデータモデル用の SSL 通信を有効にするには、任意の AEM Forms インスタンスを起動する前に、すべてのインスタンスの Java Trust Store に証明書を追加します。次のコマンドを実行して、証明書を追加できます。

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 次の手順 {#next-steps}

インタラクティブな通信と通信環境機能を使用するように、管理を設定しました。 この機能を使用するための手順は、次のとおりです。

* [Correspondence Management の概要](/help/forms/using/interactive-communications-overview.md)

* [インタラクティブ通信の作成](../../forms/using/create-interactive-communication.md)

* [Correspondence Management レターの作成](../../forms/using/create-letter.md)

