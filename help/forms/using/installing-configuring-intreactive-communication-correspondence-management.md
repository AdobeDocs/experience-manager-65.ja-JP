---
title: インタラクティブ通信をインストールして設定する
seo-title: Install and configure Interactive Communications
description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1385'
ht-degree: 100%

---

# インタラクティブ通信をインストールして設定する{#install-and-configure-interactive-communications}

## はじめに {#introduction}

AEM Forms を使用すると、業務上の通信、ドキュメント、取引明細書、給付金通知、マーケティング用メール、請求書、ウェルカムキットなど、安全でインタラクティブなドキュメントの作成、組み立て、管理、配信を集中管理できます。この機能は、インタラクティブ通信として知られています。これは、AEM Forms のアドオンパッケージに含まれる機能で、アドオンパッケージは、AEM のオーサーインスタンスまたはパブリッシュインスタンスに展開されます。

インタラクティブ通信機能を使用して、複数形式で通信を作成できます。例えば、Web や PDF です。インタラクティブ通信を AEM ワークフローと統合して、アセンブリした通信を処理し、選択したチャネルの顧客に配信することができます。例えば、電子メールを介してエンドユーザーに通信を送信します。

以前のバージョンからアップグレードして、既に Correspondence Management を使用している場合は、[互換性パッケージ](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package)をインストールすると引き続き Correspondence Management を使用できます。インタラクティブ通信と Correspondence management の違いについて詳しくは、「[インタラクティブ通信の概要](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management)」を参照してください。

AEM Forms は強力なエンタープライズクラスのプラットフォームです。インタラクティブ通信は、AEM Forms のみが持つ機能の 1 つです。機能の完全な一覧については、「[AEM Forms の概要](../../forms/using/introduction-aem-forms.md)」を参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。インタラクティブ通信機能を実行するには、少なくとも 1 つの AEM Author および処理インスタンスのみを必要とします。次のトポロジは、AEM Forms のインタラクティブ通信、Correspondence Management、AEM Forms のデータ取得および OSGi 機能にあるフォーム中心のワークフローを実行するための指標トポロジです。トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![推奨トポロジ](assets/recommended-topology.png)

AEM Forms のインタラクティブ通信は、AEM Forms のオーサーインスタンスで管理者、オーサリングおよびエージェントのユーザーインターフェイスを実行します。パブリッシュインスタンスは、エンドユーザが使用できるようになっているインタラクティブ通信の最終バージョンをホストします。

## システム要件 {#system-requirements}

AEM Forms のインタラクティブ通信および通信の管理機能をインストールして設定する前に、次のことを確認してください。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアとソフトウェアの一覧について詳しくは、「[技術要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。AEM の用語では、「インスタンス」とは、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。AEM Forms のインタラクティブ通信および通信管理機能を実行するには、少なくとも 1 つの AEM インスタンス（作成者または処理）を必要とします。

   * **作成者：**&#x200B;コンテンツを作成、アップロード、編集し、Web サイトを管理する AEM インスタンス。公開する準備ができたコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **処理：**&#x200B;処理インスタンスは、[強化された AEM オーサー](/help/forms/using/hardening-securing-aem-forms-environment.md)インスタンスです。オーサーインスタンスを設定し、インストールを実行した後でこれを強化することができます。 

   * **パブリッシュ**：発行されたコンテンツをインターネットまたは社内ネットワークを通じて公開する AEM インスタンス。

* メモリ要件が満たされていること。AEM Forms アドオンパッケージでは、次が必要です。

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

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。このパッケージには、AEM Forms インタラクティブ通信、通信管理およびその他の機能が含まれています。次の手順を実行してアドオンパッケージをインストールします。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージの名前をタップし、「**[!UICONTROL EULA 利用規約に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して「**[!UICONTROL インストール]**」をクリックします。

   [AEM Forms リリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)の記事に記載されている直接リンクからパッケージをダウンロードすることもできます。

1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**すぐにはサーバーを再起動しないでください。** AEM Forms サーバーを停止する前に、ServiceEvent REGISTERED メッセージと ServiceEvent UNREGISTERED メッセージが [AEM-Installation-Directory]/crx-quickstart/logs/error.log ファイルに表示されなくなり、このログファイルが安定した状態になるまで待ってください。
1. 手順 1 から 7 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

## インストール後の設定 {#post-installation-configurations}

AEM Forms には、いくつかの必須およびオプションの設定があります。必須の設定には、BouncyCastle ライブラリおよびシリアル化エージェントの設定が含まれます。オプションの設定には、ディスパッチャーおよび Adobe Target の設定が含まれます。

### インストール後の必須の設定 {#mandatory-post-installation-configurations}

#### RSA ライブラリと BouncyCastle ライブラリの設定  {#configure-rsa-and-bouncycastle-libraries}

これらのライブラリを起動するには、すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行します。 

1. 基になる AEM インスタンスを停止します。
1. 編集用に [AEM インストールディレクトリ ]\crx-quickstart\conf\sling.properties ファイルを開きます。

   [AEM インストールディレクトリ ]\crx-quickstart\bin\start.bat を使用して AEM を起動する場合は、[AEM ルート ]\crx-quickstart\ にある sling.properties を編集してください。

1. 以下のプロパティを sling.properties ファイルに追加します。

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. ファイルを保存して閉じ、AEM インスタンスを起動します。
1. 手順 1 から 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

#### シリアル化エージェントの設定 {#configure-the-serialization-agent}

このパッケージを許可リストに加えるには、オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. ブラウザーウィンドウで、AEM Configuration Manager を開きます。デフォルトの URL は https://&#39;[server]:[port]&#39;/system/console/configMgr です。
1. **デシリアライゼーションファイアウォール設定**&#x200B;を検索して開きます。
1. **sun.util.calendar** パッケージを&#x200B;**許可リストに加える**&#x200B;フィールドに追加します。「保存」をクリックします。
1. 手順 1 から 3 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### インストール後のオプションの設定 {#optional-post-installation-configurations}

#### 互換性パッケージをインストールする {#install-compatibility-package}

インタラクティブ通信は、顧客通信を作成するためのデフォルトの方法です。AEM 6.5 Forms で顧客通信を作成する場合は、インタラクティブ通信を使用することを推奨します。以前のバージョンからアップグレードまたは移行を行って、引き続きレター（Correspondence Management）を使用する予定の場合は、[AEMFD 互換性パッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT)をインストールします。

AEMFD 互換性パッケージを使用すると、AEM 6.5 Forms で AEM 6.2 Forms、AEM 6.3 Forms および AEM 6.4 Forms の次のアセットを使用できます。

* ドキュメントフラグメント
* レター
* データディクショナリ
* アダプティブフォームの非推奨になったテンプレートおよびページ

#### Dispatcher の設定 {#configure-dispatcher}

Dispatcher は、Adobe Experience Manager のキャッシュやロードバランシングツールで、企業向けの Web サーバーと組み合わせて使用できます。[Dispatcher](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html) を使用する場合は、AEM Forms で次の設定を実行してください。

1. AEM Forms のアクセスの設定：

   dispatcher.any ファイルを開いて編集します。フィルターセクションに移動し、次のフィルターをフィルターセクションに追加します。

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   ファイルを保存して閉じます。フィルターについて詳しくは、「[ディスパッチャードキュメント](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)」を参照してください。

1. リファラーフィルターサービスの設定：

   管理者として Apache Felix Configuration Manager にログインします。Configuration Manager のデフォルト URL は https://&#39;server&#39;:[port_number]/system/console/configMgr です。**Configurations**&#x200B;メニューで「**Apache Sling Referrer Filter**」を選択します。「Allow Hosts」フィールドで、ディスパッチャーのホスト名を入力してそれをリファラーとして許可し、「**保存**」をクリックします。入力の形式は https://&#39;[server]:[port]&#39; です。

#### Adobe Target の統合 {#integrate-adobe-target}

顧客は、対話型コミュニケーションのエクスペリエンスに魅力がない場合、これを放棄してしまいます。また、フォームが顧客にとって使いにくい場合は、サポート量が増加し組織のコストが膨らむことになります。コンバージョン率を向上させる顧客体験を正しく認識して提供することは非常に重要であり、難題でもあります。この問題を解決するキーは AEM Forms にあります。

AEM Forms は Adobe Marketing Cloud ソリューションである Adobe Target と統合することで、個々の顧客に対応した魅力的な顧客体験を、複数のデジタルチャネルにわたって提供します。Adobe Target を使用してインタラクティブ通信をパーソナライズするには、[Adobe Target を AEM Forms に統合する](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)を参照してください。

#### フォームデータモデルに SSL 通信を設定する  {#configure-ssl-communcation-for-form-data-model}

フォームデータモデル用の SSL 通信を有効にすることができます。フォームデータモデル用の SSL 通信を有効にするには、任意の AEM Forms インスタンスを起動する前に、すべてのインスタンスの Java Trust Store に証明書を追加します。次のコマンドを実行すると証明書を追加できます。

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 次の手順 {#next-steps}

インタラクティブ通信および通信管理機能を使用するための環境を設定しました。この機能を使用するための手順は、次のとおりです。

* [Correspondence Management の概要](/help/forms/using/interactive-communications-overview.md)

* [インタラクティブ通信の作成](../../forms/using/create-interactive-communication.md)

* [Correspondence Management レターの作成](../../forms/using/create-letter.md)
