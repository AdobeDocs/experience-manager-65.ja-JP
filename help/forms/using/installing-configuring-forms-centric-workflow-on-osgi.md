---
title: OSGiでのフォーム中心のワークフローのインストールと設定
seo-title: OSGiでのフォーム中心のワークフローのインストールと設定
description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
seo-description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# OSGiでのフォーム中心のワークフローのインストールと設定{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 概要 {#introduction}

企業は、複数のフォーム、バックエンドシステム、その他のデータソースからデータを収集し、処理します。 データの処理には、レビューと承認の手順、繰り返しのタスク、データのアーカイブが含まれます。 例えば、フォームのレビューとPDFドキュメントへの変換を行います。 手動で実行すると、繰り返しタスクに多くの時間とリソースがかかる場合があります。

OSGiでフォーム中心のワ [ークフローを使用して](../../forms/using/aem-forms-workflow.md) 、アダプティブフォームベースのワークフローを迅速に構築できます。 これらのワークフローは、レビューと承認のワークフロー、ビジネスプロセスのワークフロー、その他の繰り返し型のタスクの自動化に役立ちます。 また、これらのワークフローは、ドキュメントの処理（PDFドキュメントの作成、アセンブリ、配布およびアーカイブ、電子署名の追加、ドキュメントへのアクセス制限、バーコードフォームのデコードなど）や、フォームとドキュメントでのAdobe Sign署名ワークフローの使用にも役立ちます。

設定後は、これらのワークフローを手動でトリガーして、定義済みのプロセスを完了したり、ユーザーがフォームやインタラクティブな通信を送信する際にプログラム的に実行したりできます。 これは、AEM Forms のアドオンパッケージに含まれる機能で、

AEM Forms は強力なエンタープライズクラスのプラットフォームです。OSGi上のフォーム中心のワークフローは、AEM Formsの機能の1つにすぎません。 機能の完全な一覧については、「[AEM Forms の概要](../../forms/using/introduction-aem-forms.md)」を参照してください。

>[!NOTE]
>
>OSGi 上の Forms 中心のワークフローにより、OSGi スタック上の様々なタスクに対するワークフローをすばやく作成してデプロイすることができます。完全な Process Management 機能を JEE スタックにインストールする必要はありません。機能の違い [と類似点については](../../forms/using/capabilities-osgi-jee-workflows.md) 、OSGi上のForms中心のAEM WorkflowsとJEE上のProcess Managementの比較を参照してください。
>
>比較後、JEEスタックにProcess Management機能をインストールする場合は、JEEスタックとProcess Management機能のインストールと設定に関する詳細な情報について、「 [JEE上のAEM Formsのインストールまたはアップグレード](/help/forms/home.md) 」を参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。OSGi機能でフォーム中心のワークフローを実行するのに必要なのは、少なくとも1つのAEM作成者または処理インスタンス（実稼動作成者）のみです。 A processing instance is a [hardened AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) instance. 実稼動版の作成者は、ワークフローやアダプティブフォームの作成など、実際のオーサリングを実行しないでください。

次のトポロジは、AEM Forms のインタラクティブ通信、Correspondence Management、AEM Forms のデータ取得および OSGi 機能にあるフォーム中心のワークフローを実行するための指標トポロジです。トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![推奨トポロジー](assets/recommended-topology.png)

OSGi上のAEM Forms Forms中心のワークフローは、AEM formsの作成者インスタンスでAEM InboxおよびAEM Workflow Model Creation UIを実行します。

## システム要件 {#system-requirements}

>[!NOTE]
>
>「データ取得機能のイ [ンストール](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) と設定」の記事の説明に従ってOSGiにAEM Formsを既にインストールしている場合は、ドキュメントの「次の手 [順」の節に進みます](../../forms/using/installing-configuring-aem-forms-osgi.md) 。

OSGiでフォーム中心のワークフローをインストールおよび設定する前に、次のことを確認します。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアおよびソフトウェアの詳細な一覧については、「[技術的要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。AEM の用語では、「インスタンス」は、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。OSGiでフォーム中心のワークフローを実行するには、少なくとも1つのAEMインスタンス（作成者または処理）が必要です。

   * **作成者：**&#x200B;コンテンツを作成、アップロード、編集し、Web サイトを管理する AEM インスタンス。公開する準備ができたコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **処理：**&#x200B;処理インスタンスは、[強化された AEM オーサー](/help/forms/using/hardening-securing-aem-forms-environment.md)インスタンスです。インストールの実行後に作成者インスタンスを設定し、強化することができます。

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

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。このパッケージには、OSGiおよびその他の機能に対するフォーム中心のワークフローが含まれています。 次の手順を実行してアドオンパッケージをインストールします。

1. [AEM サーバー](https://localhost:4502)に管理者としてログインし、「[パッケージ共有](https://localhost:4502/crx/packageshare)」を開きます。パッケージ共有にログインするには、Adobe ID が必要です。
1. [AEM パッケージ共有](https://localhost:4502/crx/packageshare/login.html)で、**AEM 6.5 Forms アドオンパッケージ**&#x200B;または&#x200B;**最新のサービスパック**&#x200B;を検索し、お使いのオペレーティングシステムに対応するパッケージをクリックして、「**ダウンロード**」をクリックします。ライセンス使用許諾契約書を読んでから同意し、「**OK**」をクリックします。ダウンロードが開始します。ダウンロードが完了したら、パッケージの横に「**ダウンロード済み**」というテキストが表示されます。

   バージョン番号を使用してアドオンパッケージを検索することもできます。最新のパッケージのバージョン番号については、「[AEM Forms リリース](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)」の記事を参照してください。

1. ダウンロードが完了したら、「**ダウンロード済み**」をクリックします。パッケージマネージャーに切り替わります。In the package manager, search the downloaded package, and click **Install**.

   「[AEM Forms リリース](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)」記事に記載された直接リンクからパッケージを手動でダウンロードする場合は、パッケージマネージャーにログインし、「**パッケージをアップロード**」をクリックし、ダウンロード済みパッケージを選択して「アップロード」をクリックします。パッケージのアップロードが完了したら、パッケージ名をクリックし、「**インストール**」をクリックします。

1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**すぐにはサーバーを再起動しないでください。** AEM Formsサーバーを停止する前に、ServiceEvent REGISTEREDメッセージとServiceEvent UNREGISTEREDメッセージが [AEM-Installation-Directory]/crx-quickstart/logs/error.logファイルに表示されなくなるまで待ち、ログは安定しています。
1. 手順 1 から 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

## インストール後の設定 {#post-installation-configurations}

AEM Forms には、いくつかの必須およびオプションの設定があります。必須の設定には、BouncyCastle ライブラリおよびシリアル化エージェントの設定が含まれます。オプションの設定には、ディスパッチャーおよび Adobe Target の設定が含まれます。

### インストール後の必須の設定 {#mandatory-post-installation-configurations}

#### RSA ライブラリと BouncyCastle ライブラリの設定  {#configure-rsa-and-bouncycastle-libraries}

すべての作成者インスタンスと発行インスタンスで次の手順を実行し、ライブラリの委任を起動します。

1. 基になる AEM インスタンスを停止します。
1. Open the [AEM installation directory]\crx-quickstart\conf\sling.properties file for editing.

   If you used [AEM installation directory]\crx-quickstart\bin\start.bat to start AEM, then edit the sling.properties located at [AEM_root]\crx-quickstart\.

1. 以下のプロパティを sling.properties ファイルに追加します。 

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. ファイルを保存して閉じ、AEM インスタンスを起動します。
1. 手順 1 から 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

#### シリアル化エージェントの設定 {#configure-the-serialization-agent}

すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行し、パッケージをホワイトリストに登録します。

1. ブラウザーウィンドウで、AEM Configuration Manager を開きます。The default URL is https://[server]:[port]/system/console/configMgr.
1. **デシリアライゼーションファイアウォール設定**&#x200B;を検索して開きます。
1. **sun.util.calendar**&#x200B;パッケージを&#x200B;**ホワイトリスト**&#x200B;フィールドに追加します。「保存」をクリックします。
1. 手順 1 から 3 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### インストール後のオプションの設定 {#optional-post-installation-configurations}

#### Dispatcher の設定 {#configure-dispatcher}

ディスパッチャーは AEM のキャッシングおよびロードバランスツールです。AEM ディスパッチャーはまた、AEM サーバーを攻撃から保護することにも役立ちます。エンタープライズクラスの Web サーバーと一緒にディスパッチャーを使用することで、AEM インスタンスのセキュリティを向上できます。If you use [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html), then perform the following configurations for AEM Forms:

1. AEM Forms のアクセスの設定:

   dispatcher.any ファイルを開いて編集します。フィルターセクションに移動し、次のフィルターをフィルターセクションに追加します。

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   ファイルを保存して閉じます。フィルターについて詳しくは、「[ディスパッチャードキュメント](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)」を参照してください。

1. リファラーフィルターサービスの設定：

   管理者として Apache Felix Configuration Manager にログインします。The Default URL of the configuration manager is https://[server]:[port_number]/system/console/configMgr. **Configurations**&#x200B;メニューで「**Apache Sling Referrer Filter**」を選択します。「Allow Hosts」フィールドで、ディスパッチャーのホスト名を入力してそれをリファラーとして許可し、「**保存**」をクリックします。The format of the entry is `https://[server]:[port]`.

#### キャッシュの設定 {#configure-cache}

キャッシングは、データへのアクセスにかかる時間を短縮し、遅延を削減して I/O 速度を改善するメカニズムです。アダプティブフォームのキャッシュは、アダプティブフォームの HTML コンテンツと JSON の構造のみを保存し、事前入力されたデータは保存しません。これにより、アダプティブフォームのレンダリングの時間を短縮します。

* アダプティブフォームのキャッシュを使用するときは、[AEM ディスパッチャー](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) を使用してアダプティブフォームのクライアントライブラリ（CSS および JavaScript）をキャッシュします。
* カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。

次の手順を実行して、アダプティブフォームのキャッシュを設定します。

1. Go to AEM web console configuration manager at `https://[server]:[port]/system/console/configMgr`.
1. Click **Adaptive Form Configuration Service** to edit its configuration values. In the edit configuration values dialog, specify the maximum number of forms or documents an instance of the AEM Forms server can cache in the **Number of Adaptive Forms** field. デフォルト値は 100 です。「**保存**」をクリックします。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュの設定を無効にするか変更すると、キャッシュがリセットされ、すべてのフォームとドキュメントがキャッシュから削除されます。

#### Adobe Sign の設定 {#configure-adobe-sign}

Adobe Sign により、アダプティブフォームの電子署名ワークフローを有効にすることができます。電子署名を使用すると、法務、販売、給与、人事管理など、さまざまな分野におけるドキュメント処理ワークフローが改善されます。

In a typical Adobe Sign and Forms-centric workflow on OSGi scenario, a user fills an adaptive form to **apply for a service**. 例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームに入力、送信および署名を行うと、承認/拒否のワークフローが開始されます。 サービスプロバイダーは、AEMのインボックスでアプリケーションを確認し、Adobe signを使用してアプリケーションに電子署名を行います。 これに類似した電子署名ワークフローを有効にするには、Adobe Sign を AEM Forms に統合します。

AEM Forms で Adobe Sign を使用するには、「[Adobe Sign を AEM Forms に統合する](../../forms/using/adobe-sign-integration-adaptive-forms.md)」を参照してください。

## 次の手順 {#next-steps}

OSGi機能でフォーム中心のワークフローを使用するように環境を設定した。 この機能を使用する手順は次のとおりです。

* [OSGiでのフォーム中心のワークフローの使用](../../forms/using/aem-forms-workflow.md)
* [ワークフローステップのリファレンス](/help/sites-developing/workflows-step-ref.md)
* [レターとインタラクティブ通信の後処理](../../forms/using/submit-letter-topostprocess.md)

