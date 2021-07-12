---
title: OSGiへのForms中心型ワークフローのインストールと設定
seo-title: OSGiへのForms中心型ワークフローのインストールと設定
description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
seo-description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
role: Admin
exl-id: 4b24a38a-c1f0-4c81-bb3a-39ce2c4892b1
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 56%

---

# OSGiへのForms中心型ワークフローのインストールと設定{#installing-and-configuring-forms-centric-workflow-on-osgi}

## はじめに {#introduction}

企業は、複数のフォーム、バックエンドシステム、その他のデータソースからデータを収集し、処理します。 データの処理には、レビューと承認の手順、繰り返しのタスク、データのアーカイブが含まれます。 例えば、フォームをレビューしてPDFドキュメントに変換する場合などです。 手動で実行すると、繰り返しタスクには多くの時間とリソースがかかる場合があります。

OSGi](../../forms/using/aem-forms-workflow.md)上の[Forms中心のワークフローを使用して、アダプティブフォームベースのワークフローをすばやく構築できます。 これらのワークフローは、レビューと承認のワークフロー、ビジネスプロセスのワークフロー、その他の反復的なタスクの自動化に役立ちます。 これらのワークフローは、ドキュメントの処理（PDFドキュメントの作成、アセンブリ、配布、アーカイブ、電子署名の追加など）や、ドキュメントへのアクセス制限、バーコードフォームのデコードなどのAdobe Sign署名ワークフローの使用にも役立ちます。

設定後は、これらのワークフローを手動でトリガーして、定義済みのプロセスを完了したり、ユーザーがフォームやインタラクティブ通信を送信する際にプログラムを使用して実行したりできます。 これは、AEM Forms のアドオンパッケージに含まれる機能で、

AEM Forms は強力なエンタープライズクラスのプラットフォームです。OSGi上のForms中心のワークフローは、AEM Formsの機能の1つに過ぎません。 機能の完全な一覧については、「[AEM Forms の概要](introduction-aem-forms.md)」を参照してください。

>[!NOTE]
>
>OSGi での Forms 中心のワークフローを使用すると、JEE スタックに本格的なプロセス管理機能をインストールしなくても、OSGi スタックで様々なタスクのワークフローを迅速に構築およびデプロイできます。機能の違いと類似点については、OSGi上のForms中心型AEM WorkflowsとJEE上のProcess Managementの[比較](capabilities-osgi-jee-workflows.md)を参照してください。
>
>比較の後、JEEスタックにProcess Management機能をインストールする場合は、JEEスタックのインストールと設定およびProcess Management機能について詳しくは、[JEE上のAEM Formsのインストールまたはアップグレード](/help/forms/home.md)を参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。OSGi機能でForms中心のワークフローを実行するには、少なくとも1つのAEMオーサーインスタンスまたは処理インスタンス（実稼動オーサー）のみが必要です。 処理インスタンスは、[堅牢化されたAEMオーサー](/help/forms/using/hardening-securing-aem-forms-environment.md)インスタンスです。 実稼動環境の作成者では、ワークフローやアダプティブフォームの作成など、実際のオーサリングを実行しないでください。

次のトポロジは、AEM Forms のインタラクティブ通信、Correspondence Management、AEM Forms のデータ取得および OSGi 機能にあるフォーム中心のワークフローを実行するための指標トポロジです。トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![推奨トポロジ](assets/recommended-topology.png)

AEM Forms Forms中心のOSGi上のワークフローは、AEM FormsのオーサーインスタンスでAEMインボックスとAEMワークフローモデルの作成UIを実行します。

## システム要件 {#system-requirements}

>[!NOTE]
>
>ドキュメントの「[データ取得機能のインストールと設定](../../forms/using/installing-configuring-aem-forms-osgi.md)」の説明に従って、OSGiにAEM Formsを既にインストールしている場合は、ドキュメントの「[次の手順](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps)」の節に進んでください。

OSGiへのForms中心型ワークフローのインストールと設定を開始する前に、以下を確認してください。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアおよびソフトウェアの詳細な一覧については、「[技術的要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。AEM の用語では、「インスタンス」は、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。OSGi上でForms中心のワークフローを実行するには、少なくとも1つのAEMインスタンス（オーサーインスタンスまたは処理インスタンス）が必要です。

   * **作成者：**&#x200B;コンテンツを作成、アップロード、編集し、Web サイトを管理する AEM インスタンス。公開する準備ができたコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **処理：**&#x200B;処理インスタンスは、[強化された AEM オーサー](/help/forms/using/hardening-securing-aem-forms-environment.md)インスタンスです。オーサーインスタンスを設定し、インストールの実行後に強化することができます。

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

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。このパッケージには、OSGi上のForms中心のワークフローとその他の機能が含まれています。 次の手順を実行してアドオンパッケージをインストールします。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 **[!UICONTROL ダウンロードの検索]**&#x200B;オプションを使用して、結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージ名をタップし、「**[!UICONTROL EULA利用条件]**&#x200B;に同意し、**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

   [AEM Formsリリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)の記事に記載されている直接リンクからパッケージをダウンロードすることもできます。

1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**すぐにはサーバーを再起動しないでください。** AEM Formsサーバーを停止する前に、ServiceEvent REGISTEREDメッセージとServiceEvent UNREGISTEREDメッセージが [AEM-Installation-Directory] /crx-quickstart/logs/error.logファイルに表示されなくなり、ログが安定するまで待ちます。
1. 手順 1 から 7 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

## インストール後の設定 {#post-installation-configurations}

AEM Forms には、いくつかの必須およびオプションの設定があります。必須の設定には、BouncyCastle ライブラリおよびシリアル化エージェントの設定が含まれます。オプションの設定には、ディスパッチャーおよび Adobe Target の設定が含まれます。

### インストール後の必須の設定 {#mandatory-post-installation-configurations}

#### RSA ライブラリと BouncyCastle ライブラリの設定  {#configure-rsa-and-bouncycastle-libraries}

すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行し、ライブラリの委任を起動します。

1. 基になる AEM インスタンスを停止します。
1. [AEMインストールディレクトリ]\crx-quickstart\conf\sling.propertiesファイルを開いて編集します。

   [AEMインストールディレクトリ]\crx-quickstart\bin\start.batを使用してAEMを起動した場合は、[AEM_root]\crx-quickstart\にあるsling.propertiesを編集します。

1. 以下のプロパティを sling.properties ファイルに追加します。

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. ファイルを保存して閉じ、AEM インスタンスを起動します。
1. 手順 1 から 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

#### シリアル化エージェントの設定 {#configure-the-serialization-agent}

すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行し、パッケージをに追加許可リストします。

1. ブラウザーウィンドウで、AEM Configuration Manager を開きます。デフォルトのURLはhttps://&#39;[server]:[port]&#39;/system/console/configMgrです。
1. **デシリアライゼーションファイアウォール設定**&#x200B;を検索して開きます。
1. **sun.util.calendar**&#x200B;パッケージを&#x200B;**許可リスト**&#x200B;フィールドに追加します。 「保存」をクリックします。
1. 手順 1 から 3 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### インストール後のオプションの設定 {#optional-post-installation-configurations}

#### Dispatcher の設定 {#configure-dispatcher}

ディスパッチャーは AEM のキャッシングおよびロードバランスツールです。AEM ディスパッチャーはまた、AEM サーバーを攻撃から保護することにも役立ちます。エンタープライズクラスの Web サーバーと一緒にディスパッチャーを使用することで、AEM インスタンスのセキュリティを向上できます。[Dispatcher](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html)を使用する場合は、AEM Formsに対して次の設定を実行します。

1. AEM Forms のアクセスの設定:

   dispatcher.any ファイルを開いて編集します。フィルターセクションに移動し、次のフィルターをフィルターセクションに追加します。

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   ファイルを保存して閉じます。フィルターについて詳しくは、「[ディスパッチャードキュメント](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)」を参照してください。

1. リファラーフィルターサービスの設定：

   管理者として Apache Felix Configuration Manager にログインします。Configuration ManagerのデフォルトURLは、https://&#39;server&#39;:[port_number]/system/console/configMgrです。 **Configurations**&#x200B;メニューで「**Apache Sling Referrer Filter**」を選択します。「Allow Hosts」フィールドで、ディスパッチャーのホスト名を入力してそれをリファラーとして許可し、「**保存**」をクリックします。エントリの形式は`https://'[server]:[port]'`です。

#### キャッシュの設定 {#configure-cache}

キャッシングは、データへのアクセスにかかる時間を短縮し、遅延を削減して I/O 速度を改善するメカニズムです。アダプティブフォームのキャッシュは、アダプティブフォームの HTML コンテンツと JSON の構造のみを保存し、事前入力されたデータは保存しません。これにより、アダプティブフォームのレンダリングの時間を短縮します。

* アダプティブフォームのキャッシュを使用するときは、[AEM ディスパッチャー](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) を使用してアダプティブフォームのクライアントライブラリ（CSS および JavaScript）をキャッシュします。
* カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。

アダプティブフォームのキャッシュを設定するには、以下の手順を実行します。

1. `https://'[server]:[port]'/system/console/configMgr` の AEM Web コンソール設定マネージャーに移動します。
1. 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定]**」をクリックして、設定値を編集します。設定値を編集ダイアログで、「**アダプティブFormsの数**」フィールドに、AEM Formsサーバーのインスタンスでキャッシュできるフォームまたはドキュメントの最大数を指定します。 デフォルト値は 100 です。「**保存**」をクリックします。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュ設定を無効にしたり変更したりすると、キャッシュがリセットされ、すべてのフォームとドキュメントがキャッシュから削除されます。

#### Adobe Sign の設定 {#configure-adobe-sign}

Adobe Sign により、アダプティブフォームの電子署名ワークフローを有効にすることができます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

OSGi上の一般的なAdobe SignおよびForms中心のワークフローシナリオでは、ユーザーが&#x200B;**サービスの申し込みを行うアダプティブフォームに入力します。** 例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームに記入、送信、署名すると、承認/却下ワークフローが開始されます。 サービスプロバイダーは、AEMインボックス内のアプリケーションを確認し、Adobe Signを使用してアプリケーションに電子署名します。 これに類似した電子署名ワークフローを有効にするには、Adobe Sign を AEM Forms に統合します。

AEM Forms で Adobe Sign を使用するには、「[Adobe Sign を AEM Forms に統合する](../../forms/using/adobe-sign-integration-adaptive-forms.md)」を参照してください。

## 次の手順 {#next-steps}

OSGi機能でForms中心のワークフローを使用する環境を設定した。 この機能を使用する手順は次のとおりです。

* [OSGiでのForms中心のワークフローの使用](../../forms/using/aem-forms-workflow.md)
* [ワークフローステップのリファレンス](/help/sites-developing/workflows-step-ref.md)
* [レターとインタラクティブ通信の後処理](../../forms/using/submit-letter-topostprocess.md)
