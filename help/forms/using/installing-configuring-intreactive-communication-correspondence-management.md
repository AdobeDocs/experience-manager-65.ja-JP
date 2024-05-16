---
title: インタラクティブ通信をインストールして設定する
description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
topic-tags: installing
docset: aem65
role: Admin, User, Developer
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '1383'
ht-degree: 100%

---

# インタラクティブ通信をインストールして設定する{#install-and-configure-interactive-communications}

## はじめに {#introduction}

AEM Forms を使用すると、業務上の通信、ドキュメント、取引明細書、給付金通知、マーケティング用メール、請求書、ウェルカムキットなど、安全でインタラクティブなドキュメントの作成、組み立て、管理、配信を集中管理できます。この機能は、インタラクティブ通信として知られています。これは、AEM Forms のアドオンパッケージに含まれる機能です。アドオンパッケージは、AEM のオーサーインスタンスまたはパブリッシュインスタンスにデプロイされます。

インタラクティブ通信機能を使用して、複数の形式で通信を作成できます。例えば、web や PDF です。インタラクティブ通信を AEM ワークフローと統合して、アセンブリした通信を処理し、選択したチャネルの顧客に配信することができます。例えば、メールを介してエンドユーザーに通信を送信します。

以前のバージョンからアップグレードして、既に Correspondence Management を使用している場合は、[互換性パッケージ](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package)をインストールすると引き続き Correspondence Management を使用できます。インタラクティブ通信と Correspondence management の違いについて詳しくは、「[インタラクティブ通信の概要](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management)」を参照してください。

AEM Forms は強力なエンタープライズクラスのプラットフォームです。インタラクティブ通信は、AEM Forms の機能の 1 つにすぎません。機能の完全な一覧については、「[AEM Forms の概要](../../forms/using/introduction-aem-forms.md)」を参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。インタラクティブ通信機能を実行するのに最低限必要なのは、1 つの AEM オーサーおよび処理インスタンスのみです。次のトポロジは、AEM Forms のインタラクティブ通信、Correspondence Management、AEM Forms のデータ取得および OSGi 機能にある Forms 中心のワークフローを実行するための指標トポロジです。トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![推奨トポロジ](assets/recommended-topology.png)

AEM Forms のインタラクティブ通信は、AEM Forms のオーサーインスタンスで管理者、オーサリングおよびエージェントのユーザーインターフェイスを実行します。パブリッシュインスタンスは、エンドユーザが使用できるようになっているインタラクティブ通信の最終バージョンをホストします。

## システム要件 {#system-requirements}

AEM Forms のインタラクティブ通信および通信の管理機能をインストールして設定する前に、次のことを確認してください。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアとソフトウェアの一覧について詳しくは、「[技術要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。AEM の用語では、「インスタンス」とは、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。AEM Forms のインタラクティブ通信および通信管理機能を実行するには、少なくとも 1 つの AEM インスタンス（作成者または処理）を必要とします。

   * **オーサー**：コンテンツの作成、アップロードおよび編集や web サイトの管理に使用される AEM インスタンス。公開の準備が整ったコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **処理：**&#x200B;処理インスタンスは、[強化された AEM オーサー](/help/forms/using/hardening-securing-aem-forms-environment.md)インスタンスです。オーサーインスタンスを設定し、インストールを実行した後でこれを強化することができます。 

   * **パブリッシュ**：公開されたコンテンツをインターネットまたは社内ネットワークを通じて提供する AEM インスタンス。

* メモリ要件が満たされていること。AEM Forms アドオンパッケージでは、次が必要です。

   * Microsoft® Windows ベースのインストールの場合、15 GB の一時的な空きスペースが必要です。
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
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」を選択します。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適した Forms アドオンパッケージの名前を選択し、「**[!UICONTROL EULA 利用条件に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」を選択します。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して「**[!UICONTROL インストール]**」をクリックします。

   [AEM Forms リリース](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)の記事に記載されている直接リンクからパッケージをダウンロードすることもできます。

1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**サーバーをすぐに再起動しないでください。** AEM Forms サーバーを停止する前に、ServiceEvent REGISTERED メッセージと ServiceEvent UNREGISTERED メッセージが [AEM-Installation-Directory]/crx-quickstart/logs/error.log ファイルに表示されなくなり、このログファイルが安定した状態になるまで待ってください。

   >[!NOTE]
   >
   > SDK を再起動するには、「Ctrl + C」コマンドを使用することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

1. 手順 1 から 7 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

## インストール後の設定 {#post-installation-configurations}

AEM Forms には、必須の設定とオプションの設定がいくつかあります。必須の設定には、BouncyCastle ライブラリおよびシリアル化エージェントの設定が含まれます。オプションの設定には、Dispatcher と Adobe Target の設定が含まれます。

### インストール後の必須の設定 {#mandatory-post-installation-configurations}

#### RSA ライブラリと BouncyCastle ライブラリの設定  {#configure-rsa-and-bouncycastle-libraries}

これらのライブラリを起動するには、すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行します。 

1. 基になる AEM インスタンスを停止します。
1. 編集用に [AEM インストールディレクトリ ]\crx-quickstart\conf\sling.properties ファイルを開きます。

   [AEM installation directory]\crx-quickstart\bin\start.bat を使用して AEM を起動する場合は、[AEM_root]\crx-quickstart\ にある sling.properties を編集します。

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

インタラクティブ通信は、顧客通信を作成するためのデフォルトの方法です。AEM 6.5 Forms で顧客通信を作成する場合は、インタラクティブ通信を使用することを推奨します。以前のバージョンからアップグレードまたは移行を行って、引き続きレター（Correspondence Management）を使用する予定の場合は、[AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/aem-forms-osgi-upgrade/compatibility-package.html?lang=ja)をインストールします。

AEMFD 互換性パッケージを使用すると、AEM 6.4 Forms、AEM 6.3 Forms および AEM 6.2 Forms の次のアセットを、AEM 6.5 Forms で使用できます。

* ドキュメントフラグメント
* レター
* データディクショナリ
* アダプティブフォームの非推奨（廃止予定）になったテンプレートおよびページ

#### Dispatcher の設定 {#configure-dispatcher}

Dispatcher は、Adobe Experience Manager のキャッシュやロードバランシングツールで、企業向けの web サーバーと組み合わせて使用します。[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja) を使用する場合は、AEM Forms で次の設定を実行してください。

1. AEM Forms のアクセスの設定：

   dispatcher.any ファイルを開いて編集します。フィルターセクションに移動し、次のフィルターをフィルターセクションに追加します。

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   ファイルを保存して閉じます。フィルターについて詳しくは、[Dispatcher のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja)を参照してください。

1. リファラーフィルターサービスの設定：

   Apache Felix Configuration Manager に管理者としてログインします。Configuration Manager のデフォルト URL は https://&#39;server&#39;:[port_number]/system/console/configMgr です。**Configurations**&#x200B;メニューで「**Apache Sling Referrer Filter**」を選択します。「Allow Hosts」フィールドで、Dispatcher のホスト名を入力してそれをリファラーとして許可し、「**保存**」をクリックします。入力の形式は https://&#39;[server]:[port]&#39; です。

#### Adobe Target の統合 {#integrate-adobe-target}

顧客は、インタラクティブ通信のエクスペリエンスに魅力がない場合、これを放棄してしまいます。顧客にとって不満が生じると同時に、サポート量が増加し組織のコストが膨らむことになります。コンバージョン率を向上させるカスタマーエクスペリエンス（顧客体験）を正しく認識して提供することは非常に重要であり、難題でもあります。この問題を解決する鍵は AEM Forms にあります。

AEM Forms は Adobe Experience Cloud ソリューションである Adobe Target と統合することで、個々の顧客に対応した魅力的な顧客体験を、複数のデジタルチャネルにわたって提供します。Adobe Target を使用してインタラクティブ通信をパーソナライズするには、[Adobe Target を AEM Forms に統合する](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)を参照してください。

#### フォームデータモデルへの SSL 通信の設定  {#configure-ssl-communcation-for-form-data-model}

フォームデータモデルの SSL 通信を有効にすることができます。フォームデータモデルの SSL 通信を有効にするには、任意の AEM Forms インスタンスを起動する前に、すべてのインスタンスの Java™ Trust Store に証明書を追加します。次のコマンドを実行すると証明書を追加できます。

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 次の手順 {#next-steps}

インタラクティブ通信および通信管理機能を使用するための環境を設定しました。この機能を使用するための手順は、次のとおりです。

* [Correspondence Management の概要](/help/forms/using/interactive-communications-overview.md)

* [インタラクティブ通信の作成](../../forms/using/create-interactive-communication.md)

* [Correspondence Management レターの作成](../../forms/using/create-letter.md)
