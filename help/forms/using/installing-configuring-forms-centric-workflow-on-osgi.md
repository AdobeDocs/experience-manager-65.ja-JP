---
title: OSGiでのForms中心のワークフローのインストールと設定
seo-title: OSGiでのForms中心のワークフローのインストールと設定
description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
seo-description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 35b2c9c8c79b3cc3d81e0b92ea17cd7d599fa7ee
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 52%

---


# OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}でのForms中心のワークフローのインストールと設定

## 概要 {#introduction}

企業は、複数のフォーム、バックエンドシステム、その他のデータソースからデータを収集し、処理します。 データの処理には、レビューと承認の手順、繰り返し型のタスク、データのアーカイブが含まれます。 例えば、フォームの確認とPDFドキュメントへの変換を行います。 手動で行うと、繰り返しタスクに多くの時間とリソースがかかる場合があります。

OSGi](../../forms/using/aem-forms-workflow.md)で[Forms中心のワークフローを使用すると、アダプティブフォームベースのワークフローを迅速に構築できます。 これらのワークフローは、レビューと承認のワークフロー、ビジネスプロセスのワークフロー、その他の繰り返し型のタスクの自動化に役立ちます。 これらのワークフローは、ドキュメント(PDFドキュメントの作成、アセンブリ、配布、アーカイブ、電子署名の追加、ドキュメントへのアクセス制限、バーコードフォームのデコードなど)の処理や、フォームとドキュメントでのAdobe Sign署名ワークフローの使用にも役立ちます。

設定が完了すると、これらのワークフローを手動でトリガーして、定義済みのプロセスを完了したり、ユーザーがフォームやインタラクティブな通信を送信したときにプログラムを実行したりできます。 これは、AEM Forms のアドオンパッケージに含まれる機能で、

AEM Forms は強力なエンタープライズクラスのプラットフォームです。OSGiでのForms中心のワークフローは、AEM Formsの機能の1つにすぎません。 機能の完全な一覧については、「[AEM Forms の概要](introduction-aem-forms.md)」を参照してください。

>[!NOTE]
>
>OSGi 上の Forms 中心のワークフローにより、OSGi スタック上の様々なタスクに対するワークフローをすばやく作成してデプロイすることができます。完全な Process Management 機能を JEE スタックにインストールする必要はありません。機能の違いと類似点については、OSGiのForms中心のAEMワークフローとJEEのProcess Managementの[比較](capabilities-osgi-jee-workflows.md)を参照してください。
>
>比較の後、JEEスタックにProcess Management機能をインストールする場合は、JEEスタックのインストールと設定およびプロセス管理機能について詳しくは、[JEE](/help/forms/home.md)のAEM Formsのインストールまたはアップグレードを参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。OSGi機能上でForms中心のワークフローを実行するのに必要なのは、最低1つのAEM作成者または処理インスタンス（実稼働作成者）のみです。 処理インスタンスは、[強化されたAEM作成者](/help/forms/using/hardening-securing-aem-forms-environment.md)のインスタンスです。 実稼動版の作成者は、ワークフローやアダプティブフォームの作成など、実際のオーサリングを実行しないでください。

次のトポロジは、AEM Forms のインタラクティブ通信、Correspondence Management、AEM Forms のデータ取得および OSGi 機能にあるフォーム中心のワークフローを実行するための指標トポロジです。トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![推奨トポロジー](assets/recommended-topology.png)

OSGiでのAEM FormsForms中心のワークフローは、AEM Formsの作成者インスタンスでAEMインボックスとAEMワークフローモデル作成UIを実行します。

## システム要件 {#system-requirements}

>[!NOTE]
>
>「](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps)データ取得機能のインストールと設定[」の説明に従って、OSGiにAEM Formsを既にインストールしている場合は、ドキュメントの「次の手順[」のセクションに進みます。](../../forms/using/installing-configuring-aem-forms-osgi.md)

OSGiでのForms中心のワークフローのインストールと設定を開始する前に、以下のことを確認します。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアおよびソフトウェアの詳細な一覧については、「[技術的要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。AEM の用語では、「インスタンス」は、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。OSGiでForms中心のワークフローを実行するには、少なくとも1つのAEMインスタンス（作成者または処理）が必要です。

   * **作成者：**&#x200B;コンテンツを作成、アップロード、編集し、Web サイトを管理する AEM インスタンス。公開する準備ができたコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **処理：**&#x200B;処理インスタンスは、[強化された AEM オーサー](/help/forms/using/hardening-securing-aem-forms-environment.md)インスタンスです。作成者インスタンスを設定し、インストールの実行後に強化できます。

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

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。このパッケージには、OSGiおよびその他の機能に関するForms中心のワークフローが含まれています。 次の手順を実行してアドオンパッケージをインストールします。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。 ソフトウェアディストリビューションにログインするには、Adobe ID が必要です。
1. ヘッダーメニューにある&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して、結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに対応するパッケージ名をタップし、「**[!UICONTROL EULA条項に同意]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [Package Manager](https://docs.adobe.com/content/help/ja-JP/experience-manager-65/administering/contentmanagement/package-manager.html)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックして、パッケージをアップロードします。
1. パッケージを選択し、「**[!UICONTROL インストール]**」をクリックします。

   [AEM Formsリリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)の記事に記載されている直接リンクからパッケージをダウンロードすることもできます。

1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**すぐにはサーバーを再起動しないでください。** AEM Formsサーバーを停止する前に、 [AEM-Installation-Directory]/crx-quickstart/logs/error.logファイルにServiceEvent REGISTEREDメッセージとServiceEvent UNREGISTEREDメッセージが表示されなくなるまで待ち、ログは安定しています。
1. 手順 1 から 7 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

## インストール後の設定 {#post-installation-configurations}

AEM Forms には、いくつかの必須およびオプションの設定があります。必須の設定には、BouncyCastle ライブラリおよびシリアル化エージェントの設定が含まれます。オプションの設定には、ディスパッチャーおよび Adobe Target の設定が含まれます。

### インストール後の必須の設定 {#mandatory-post-installation-configurations}

#### RSA ライブラリと BouncyCastle ライブラリの設定  {#configure-rsa-and-bouncycastle-libraries}

すべての作成者インスタンスと発行インスタンスで次の手順を実行し、ライブラリの委任をブートします。

1. 基になる AEM インスタンスを停止します。
1. [AEMインストールディレクトリ]\crx-quickstart\conf\sling.propertiesを開いて編集します。

   [AEMインストールディレクトリ]\crx-quickstart\bin\start.batを開始AEMに使用した場合は、[AEM_root]\crx-quickstart\にあるsling.propertiesを編集します。

1. 以下のプロパティを sling.properties ファイルに追加します。

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. ファイルを保存して閉じ、AEM インスタンスを起動します。
1. 手順 1 から 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

#### シリアル化エージェントの設定 {#configure-the-serialization-agent}

すべての作成者インスタンスと発行インスタンスで次の手順を実行し、パッケージを許可リストに追加します。

1. ブラウザーウィンドウで、AEM Configuration Manager を開きます。デフォルトのURLは、https://&#39;[server]:[port]&#39;/system/console/configMgrです。
1. **デシリアライゼーションファイアウォール設定**&#x200B;を検索して開きます。
1. 追加&#x200B;**許可リスト**&#x200B;フィールドに対する&#x200B;**sun.util.calendar**&#x200B;パッケージ。 「保存」をクリックします。
1. 手順 1 から 3 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### インストール後のオプションの設定 {#optional-post-installation-configurations}

#### Dispatcher の設定 {#configure-dispatcher}

ディスパッチャーは AEM のキャッシングおよびロードバランスツールです。AEM ディスパッチャーはまた、AEM サーバーを攻撃から保護することにも役立ちます。エンタープライズクラスの Web サーバーと一緒にディスパッチャーを使用することで、AEM インスタンスのセキュリティを向上できます。[ディスパッチャー](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html)を使用する場合は、AEM Formsに対して次の設定を行います。

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

次の手順を実行してアダプティブフォームのキャッシュを設定します。

1. `https://'[server]:[port]'/system/console/configMgr`のAEM Web Console Configuration Managerに移動します。
1. **「Adaptive Form Configuration Service**」をクリックして、設定値を編集します。 設定値を編集ダイアログで、AEM Formsサーバーのインスタンスがキャッシュできるフォームまたはドキュメントの最大数を「**アダプティブFormsの数**」フィールドに指定します。 デフォルト値は 100 です。「**保存**」をクリックします。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュの設定を無効または変更すると、キャッシュがリセットされ、フォームとドキュメントがすべてキャッシュから削除されます。

#### Adobe Sign の設定 {#configure-adobe-sign}

Adobe Sign により、アダプティブフォームの電子署名ワークフローを有効にすることができます。電子署名を使用すると、法務、販売、給与、人事管理など、さまざまな分野におけるドキュメント処理ワークフローが改善されます。

OSGiの一般的なAdobe SignおよびForms中心のワークフローでは、ユーザーはアダプティブフォームに&#x200B;**apply for a service**&#x200B;に入力します。 例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームを入力、送信し、署名すると、承認/拒否のワークフローが開始されます。 サービスプロバイダーは、AEM受信トレイで申込書をレビューし、Adobe Signを使用して電子署名を行います。 これに類似した電子署名ワークフローを有効にするには、Adobe Sign を AEM Forms に統合します。

AEM Forms で Adobe Sign を使用するには、「[Adobe Sign を AEM Forms に統合する](../../forms/using/adobe-sign-integration-adaptive-forms.md)」を参照してください。

## 次の手順 {#next-steps}

OSGi機能でForms中心のワークフローを使用するように環境を設定しました。 この機能を使用するための手順は次のとおりです。

* [OSGiでのForms中心のワークフローの使用](../../forms/using/aem-forms-workflow.md)
* [ワークフローステップのリファレンス](/help/sites-developing/workflows-step-ref.md)
* [レターとインタラクティブ通信の後処理](../../forms/using/submit-letter-topostprocess.md)

