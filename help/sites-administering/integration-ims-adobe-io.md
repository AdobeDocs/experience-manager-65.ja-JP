---
title: Adobe I/O を使用した Adobe Target との統合
seo-title: Adobe I/O を使用した Adobe Target との統合
description: Adobe I/Oを使用してAEMとAdobe Targetを統合する方法を説明します
seo-description: Adobe I/Oを使用してAEMとAdobe Targetを統合する方法を説明します
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: 26efba567985dcb89b2610935cab18943b7034b3
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 12%

---


# Adobe I/O を使用した Adobe Target との統合{#integration-with-adobe-target-using-adobe-i-o}

Target Standard APIを介してAEMをAdobe Targetと統合するには、AdobeIMS(Identity Managementシステム)とAdobe I/Oの設定が必要です。

>[!NOTE]
>
>Adobe Target標準APIのサポートは、AEM 6.5で新たに追加されました。Target Standard APIはIMS認証を使用します。
>
>AEMでのAdobe TargetクラシックAPIの使用は、後方互換性を維持するために引き続きサポートされています。 [ターゲットクラシックAPIは、ユーザー資格情報認証](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)を使用します。
>
>APIの選択は、AEM/ターゲット統合に使用される認証方式によって決定されます。

## 前提条件 {#prerequisites}

この手順を開始する前に、次の手順を実行します。

* [Adobe](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html) サポートは、次の目的でアカウントをプロビジョニングする必要があります。

   * Adobeコンソール
   * Adobe I/O
   * Adobe Targetと
   * AdobeIMS(Identity Managementシステム)

* 組織のシステム管理者は、Admin Consoleを使用して、組織内の必要な開発者を関連する製品プロファイルに追加する必要があります。

   * これにより、特定の開発者に対して、Adobe I/O内での統合を有効にする権限を提供します。
   * 詳しくは、[開発者の管理](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)を参照してください。


## IMS設定の設定 — 公開鍵の生成{#configuring-an-ims-configuration-generating-a-public-key}

設定の最初の段階は、AEMでIMS設定を作成し、公開鍵を生成することです。

1. AEMで、**ツール**&#x200B;メニューを開きます。
1. 「**セキュリティ**」セクションで、「**AdobeIMS設定**」を選択します。
1. 「**作成**」を選択して、**AdobeIMSテクニカルアカウント設定**&#x200B;を開きます。
1. 「**クラウド設定**」の下のドロップダウンを使用して、「**Adobe Target**」を選択します。
1. **新しい証明書を作成**&#x200B;をアクティブ化し、新しいエイリアスを入力します。
1. **証明書の作成**&#x200B;で確認します。

   ![](assets/integrate-target-io-01.png)

1. 「**Download**（または&#x200B;**Download Public Key**）」を選択してファイルをローカルドライブにダウンロードし、[AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem)とのAdobe Target統合用にAdobe I/Oを設定する際に使用できるようにします。

   >[!CAUTION]
   >
   >この設定を開いたままにしておくと、[AEM](#completing-the-ims-configuration-in-aem)でIMS設定を完了したときに、再び必要になります。

   ![](assets/integrate-target-io-02.png)

## AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}とのAdobe Target統合のためのAdobe I/Oの設定

AEMで使用するAdobe TargetとのAdobe I/Oプロジェクト（統合）を作成し、必要な権限を割り当てる必要があります。

### プロジェクトの作成{#creating-the-project}

Adobe I/Oコンソールを開き、AEMで使用するAdobe TargetのI/Oプロジェクトを作成します。

>[!NOTE]
>
>[Adobe I/Oのチュートリアル](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html)も参照してください。

1. プロジェクト用のAdobe I/Oコンソールを開く：

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. 自分が所有しているプロジェクトが表示されます。 「**新しいプロジェクトを作成**」を選択します。場所と使用方法は次のとおりです。

   * まだプロジェクトがない場合は、**新しいプロジェクトを作成**は中央、下に配置されます。
      ![新規プロジェクトの作成 — 最初のプロジェクト](assets/integration-target-io-02.png)
   * 既に既存のプロジェクトがある場合は、これらが一覧表示され、**新しいプロジェクトを作成**が右上に表示されます。
      ![新規プロジェクトの作成 — 複数のプロジェクト](assets/integration-target-io-03.png)


1. プロジェクト&#x200B;**追加に**&#x200B;を選択し、次に&#x200B;**API**&#x200B;を選択します。

   ![](assets/integration-target-io-10.png)

1. **Adobe Target**&#x200B;を選択し、**次へ**:

   >[!NOTE]
   >
   >Adobe Targetを購読しているが、リストに表示されていない場合は、[前提条件](#prerequisites)を確認する必要があります。

   ![](assets/integration-target-io-12.png)

1. **公開鍵をアップロードし**、完了したら **次へ**:

   ![](assets/integration-target-io-13.png)

1. 秘密鍵証明書を確認し、**次へ**&#x200B;に進みます。

   ![](assets/integration-target-io-15.png)

1. 必要な製品プロファイルを選択し、**設定済みAPIの保存**&#x200B;に進みます。

   >[!NOTE]
   >
   >に表示される製品プロファイルは、次の項目があるかどうかによって異なります。
   >
   >* Adobe Target標準 — **デフォルトのワークスペース**&#x200B;のみ使用可能
   >* Adobe Targetプレミアム — 使用可能なすべてのワークスペースが、次のように表示されます。


   ![](assets/integration-target-io-16.png)

1. 作成が確認される。

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### 統合への権限の割り当て{#assigning-privileges-to-the-integration}

次に、必要な権限を統合に割り当てる必要があります。

1. Adobe **Admin Console**&#x200B;を開きます。

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. **製品**（上部のツールバー）に移動し、**Adobe Target- &lt;*your-tenant-id*>**（左のパネル）を選択します。
1. 「**製品のプロファイル**」を選択し、表示されるリストから必要なワークスペースを選択します。 例えば、デフォルトのワークスペースです。
1. 「**統合**」を選択し、必要な統合設定を選択します。
1. **エディター**&#x200B;を&#x200B;**製品の役割**&#x200B;として選択します。**オブザーバー**&#x200B;の代わりに。

## Adobe I/O統合プロジェクト用に保存された詳細{#details-stored-for-the-adobe-io-integration-project}

Adobe I/Oプロジェクトコンソールから、すべての統合プロジェクトのリストを確認できます。

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

**表示**（特定のプロジェクトエントリの右側）を選択して、設定に関する詳細を表示します。 有効なタイプには以下が含まれます。

* プロジェクトの概要
* インサイト
* 秘密鍵証明書
   * サービスアカウント(JWT)
      * 秘密鍵証明書の詳細
      * JWTを生成
* API
   * 例えば、Adobe Target

これらの一部は、AEMでのターゲット用にAdobe I/O統合を完了する必要があります。

## AEM {#completing-the-ims-configuration-in-aem}でのIMS設定の完了

AEMに戻ると、ターゲットに必要な値をAdobe I/O統合から追加して、IMS設定を完了できます。

1. AEM](#configuring-an-ims-configuration-generating-a-public-key)で開いている[IMS設定に戻ります。
1. 「**次へ**」を選択します。

1. ここでは、Adobe I/O](#details-stored-for-the-adobe-io-integration-project)の[詳細を使用できます。

   * **タイトル**:テキスト。
   * **認証サーバー**:下の `"aud"` 例のように、下の **** Payloadセクションの `"https://ims-na1.adobelogin.com"` 行からこれをコピー&amp;ペーストします。
   * **APIキー**:ターゲットのために、Adobe I/O統合の [](#details-stored-for-the-adobe-io-integration-project) 概要セクションからこれをコピーします。
   * **クライアントシークレット**:ターゲット用にAdobe I/O統合の [](#details-stored-for-the-adobe-io-integration-project) 概要セクションでこれを生成し、
   * **ペイロード**:ターゲット用に、Adobe I/O統合の [Generate ](#details-stored-for-the-adobe-io-integration-project) JWTセクションからこれをコピーします。

   ![](assets/integrate-target-io-10.png)

1. **作成**&#x200B;で確認します。

1. Adobe Target設定がAEMコンソールに表示されます。

   ![](assets/integrate-target-io-11.png)

## IMS設定の確認{#confirming-the-ims-configuration}

設定が期待どおりに動作していることを確認するには：

1. 次のファイルを開きます。

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   次に例を示します。

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 設定を選択します。
1. ツールバーから「**ヘルスをチェック**」を選択し、続けて「**チェック**」を選択します。

   ![](assets/integrate-target-io-12.png)

1. 成功すると、次のメッセージが表示されます。

   ![](assets/integrate-target-io-13.png)

## Adobe TargetCloud Serviceの設定{#configuring-the-adobe-target-cloud-service}

Target Standard APIを使用するCloud Serviceに対して、設定を参照できるようになりました。

1. **ツール**&#x200B;メニューを開きます。 次に、**Cloud Services**&#x200B;セクション内で、**レガシーCloud Services**&#x200B;を選択します。
1. **Adobe Target**&#x200B;まで下にスクロールし、**今すぐ設定**&#x200B;を選択します。

   **設定を作成**&#x200B;ダイアログが開きます。

1. **タイトル**&#x200B;を入力し、必要に応じて&#x200B;**名前**&#x200B;を入力します（空白の場合は、タイトルから生成されます）。

   また、必要なテンプレートを選択することもできます（複数のテンプレートが使用可能な場合）。

1. **作成**&#x200B;で確認します。

   **コンポーネントを編集**&#x200B;ダイアログが開きます。

1. 「**Adobe Target設定**」タブに詳細を入力します。

   * **認証**:IMS
   * **テナントID**:adobeIMSテナントID

      >[!NOTE]
      >
      >IMSの場合、この値はターゲット自体から取得する必要があります。 ターゲットにログインし、URLからテナントIDを抽出できます。
      >
      >例えば、URLが次の場合、
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >その場合は`yourtenantid`を使用します。

   * **IMS設定**:IMS設定の名前を選択します
   * **APIタイプ**:REST
   * **A4T Analytics クラウド設定**：ターゲットアクティビティの目標と指標に使用する Analytics クラウド設定。これは、コンテンツをターゲット化するときに、Adobe Analytics をレポートソースとして使用している場合に必要です。クラウド設定が表示されない場合は、「[A4TAnalytics Cloud設定](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration)の設定」の注意を参照してください。
   * **正確なターゲット設定を使用**:デフォルトでは、このチェックボックスは選択されています。オンにすると、クラウドサービス設定はコンテンツが読み込まれるまでコンテキストの読み込みを待機します。続きのメモを確認してください。
   * **Adobe Targetからのセグメントの同期**:AEMで使用するターゲットで定義されたセグメントをダウンロードするには、このオプションを選択します。「API のタイプ」プロパティが REST のときは、インラインのセグメントがサポートされておらず、常に Target からセグメントを使用する必要があるので、このオプションをオンにする必要があります（AEM の用語「セグメント」は、Target の「オーディエンス」と同じです）。
   * **クライアントライブラリ**:AT.jsクライアントライブラリまたはmbox.js（非推奨）のどちらにするかを選択します。
   * **Tag Management Systemを使用したクライアントライブラリの配信**:DTM（非推奨）、Adobe起動、またはその他のタグ管理システムを使用します。
   * **Custom AT.js**:「Tag Management」ボックスをオンにした場合、またはデフォルトのAT.jsを使用する場合は、空白のままにします。それ以外の場合は、カスタム AT.js をアップロードします。AT.js を選択した場合にのみ表示されます。

   >[!NOTE]
   >
   >[ターゲットクラシックAPIを使用するCloud Serviceの設定は廃止されました(「Adobe Recommendations設定」タブを使用)。](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) 

   次に例を示します。

   ![](assets/integrate-target-io-14.png)

1. 「**ターゲットに接続**」をクリックして、Adobe Targetとの接続を初期化します。

   接続に成功すると、「**接続に成功しました**」というメッセージが表示されます。

1. メッセージで「**OK**」を選択し、次に設定を確認するダイアログで「**OK**」を選択します。
1. これで、[ターゲットフレームワーク](/help/sites-administering/target-configuring.md#adding-a-target-framework)の追加に進み、ターゲットに送信するContextHubまたはClientContextのパラメーターを設定できます。 これは、AEMエクスペリエンスフラグメントをターゲットに書き出す場合には必要でない場合があります。

