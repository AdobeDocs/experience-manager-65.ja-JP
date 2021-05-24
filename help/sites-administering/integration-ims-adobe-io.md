---
title: Adobe I/O を使用した Adobe Target との統合
seo-title: Adobe I/O を使用した Adobe Target との統合
description: Adobe I/Oを使用したAEMとAdobe Targetの統合について説明します
seo-description: Adobe I/Oを使用したAEMとAdobe Targetの統合について説明します
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
exl-id: ba7abc53-7db8-41b1-a0fa-4e4dbbeca402
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 19%

---

# Adobe I/O を使用した Adobe Target との統合{#integration-with-adobe-target-using-adobe-i-o}

Target Standard APIを使用してAEMとAdobe Targetを統合するには、AdobeIMS(Identity Managementシステム)とAdobe I/Oの設定が必要です。

>[!NOTE]
>
>Adobe Target Standard APIのサポートは、AEM 6.5で新たに追加されました。Target Standard APIはIMS認証を使用します。
>
>AEMでのAdobe Target Classic APIの使用は、後方互換性のために引き続きサポートされます。 [Target Classic APIは、ユーザーの資格情報認証](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)を使用します。
>
>APIの選択は、AEM/Targetの統合に使用される認証方法によって実行されます。
>[テナントIDとクライアントコード](#tenant-client)の節も参照してください。

## 前提条件 {#prerequisites}

この手順を開始する前に、以下を実行します。

* [Adobeサ](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html) ポートは、アカウントを次の目的でプロビジョニングする必要があります。

   * Adobeコンソール
   * Adobe I/O
   * Adobe Targetと
   * AdobeIMS(Identity Managementシステム)

* 組織のシステム管理者は、Admin Consoleを使用して、組織内の必要な開発者を関連する製品プロファイルに追加する必要があります。

   * これにより、特定の開発者に対し、開発内での統合を有効にする権限をAdobe I/Oできます。
   * 詳しくは、[開発者の管理](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)を参照してください。


## IMS設定の指定 — 公開鍵の生成{#configuring-an-ims-configuration-generating-a-public-key}

設定の最初の段階は、AEMでIMS設定を作成し、公開鍵を生成することです。

1. AEMで、**ツール**&#x200B;メニューを開きます。
1. 「**セキュリティ**」セクションで、「**AdobeIMS設定**」を選択します。
1. 「**作成**」を選択して、「**AdobeIMSテクニカルアカウント設定**」を開きます。
1. 「**クラウド設定**」の下のドロップダウンを使用して、「**Adobe Target**」を選択します。
1. **新しい証明書を作成**&#x200B;をアクティブにし、新しいエイリアスを入力します。
1. **証明書を作成**&#x200B;して確定します。

   ![](assets/integrate-target-io-01.png)

1. 「**ダウンロード**」（または「**公開鍵をダウンロード**」）を選択して、ファイルをローカルドライブにダウンロードし、[AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem)とAdobe Targetを統合するAdobe I/Oを設定する際に使用できるようにします。

   >[!CAUTION]
   >
   >この設定は開いたままにしておきます。 [AEM](#completing-the-ims-configuration-in-aem)でIMS設定を完了すると、再度必要になります。

   ![](assets/integrate-target-io-02.png)

## Adobe TargetとAEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}を統合するためのAdobe I/Oの設定

AEMが使用するAdobe I/Oプロジェクト（統合）をAdobe Targetと作成し、必要な権限を割り当てる必要があります。

### プロジェクト{#creating-the-project}の作成

Adobe I/Oコンソールを開き、AEMが使用するAdobe TargetとのI/Oプロジェクトを作成します。

>[!NOTE]
>
>[Adobe I/Oチュートリアル](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html)も参照してください。

1. プロジェクトのAdobe I/Oコンソールを開きます。

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. 既に存在するすべてのプロジェクトが表示されます。 「**新しいプロジェクトを作成**」を選択します。場所と使用方法は次の条件によって異なります。

   * まだプロジェクトがない場合は、**新しいプロジェクトを作成**は中央、下に配置されます。
      ![新規プロジェクトの作成 — 最初のプロジェクト](assets/integration-target-io-02.png)
   * 既に既存のプロジェクトがある場合は、それらが一覧表示され、**新しいプロジェクトを作成**が右上に表示されます。
      ![新規プロジェクトの作成 — 複数のプロジェクト](assets/integration-target-io-03.png)


1. 「**プロジェクトに追加**」を選択し、次に&#x200B;**API**&#x200B;を選択します。

   ![](assets/integration-target-io-10.png)

1. **Adobe Target**&#x200B;を選択し、**次へ**&#x200B;を選択します。

   >[!NOTE]
   >
   >Adobe Targetを購読しているが、リストに表示されない場合は、[前提条件](#prerequisites)を確認してください。

   ![](assets/integration-target-io-12.png)

1. **公開鍵**&#x200B;をアップロードし、完了したら、「次 **へ**」を続行します。

   ![](assets/integration-target-io-13.png)

1. 資格情報を確認し、**次へ**&#x200B;を続行します。

   ![](assets/integration-target-io-15.png)

1. 必要な製品プロファイルを選択し、「**設定済みAPIを保存**」で続行します。

   >[!NOTE]
   >
   >と共に表示される製品プロファイルは、以下の条件によって異なります。
   >
   >* Adobe Target Standard — デフォルトのワークスペース&#x200B;**のみ使用可能**
   >* Adobe Target Premium — 使用可能なすべてのワークスペースが次のように表示されます


   ![](assets/integration-target-io-16.png)

1. 作成が確認されます。

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### 統合{#assigning-privileges-to-the-integration}への権限の割り当て

次に、必要な権限を統合に割り当てる必要があります。

1. Adobe **Admin Console**&#x200B;を開きます。

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. **Products**（上部のツールバー）に移動し、**Adobe Target - &lt;*your-tenant-id***（左側のパネルから）を選択します。
1. 「**製品プロファイル**」を選択し、表示されるリストから必要なワークスペースを選択します。 例えば、「デフォルトのワークスペース」などです。
1. 「**統合**」を選択し、必要な統合設定を選択します。
1. ****&#x200B;製品ロール&#x200B;**としてエディター**&#x200B;を選択します。**監視者**&#x200B;の代わりに。

## Adobe I/O統合プロジェクト{#details-stored-for-the-adobe-io-integration-project}の詳細

Adobe I/Oプロジェクトコンソールから、すべての統合プロジェクトのリストを表示できます。

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

**表示**（特定のプロジェクトエントリの右側）を選択して、設定に関する詳細を表示します。 有効なタイプには以下が含まれます。

* プロジェクトの概要
* インサイト
* 秘密鍵証明書
   * サービスアカウント(JWT)
      * 資格情報の詳細
      * JWTを生成
* API
   * 例： Adobe Target

これらの一部は、AEMでTargetのAdobe I/O統合を完了する必要があります。

## AEM {#completing-the-ims-configuration-in-aem}でのIMS設定の完了

AEMに戻ると、TargetのAdobe I/O統合から必要な値を追加して、IMS設定を完了できます。

1. AEM](#configuring-an-ims-configuration-generating-a-public-key)で開いている[IMS設定に戻ります。
1. 「**次へ**」を選択します。

1. ここでは、Adobe I/O](#details-stored-for-the-adobe-io-integration-project)の[の詳細を使用できます。

   * **タイトル**:テキスト。
   * **認証サーバー**:下の例のように、下の「 `"aud"` Payload」セクシ **** ョンの行からこれをコピー&amp;ペ `"https://ims-na1.adobelogin.com"` ーストします。
   * **APIキー**:Targetの統合の「概要」セク [](#details-stored-for-the-adobe-io-integration-project) ションからAdobe I/Oをコピーします。
   * **クライアント秘密鍵**:TargetのAdobe I/O統合の「 [](#details-stored-for-the-adobe-io-integration-project) 概要」セクションでこれを生成し、
   * **ペイロード**:TargetのAdobe I/O統合の「 [JWTを生](#details-stored-for-the-adobe-io-integration-project) 成」セクションからコピーします。

   ![](assets/integrate-target-io-10.png)

1. **作成**&#x200B;で確定します。

1. Adobe Target設定がAEMコンソールに表示されます。

   ![](assets/integrate-target-io-11.png)

## IMS設定の確認{#confirming-the-ims-configuration}

設定が期待どおりに動作していることを確認するには：

1. 次のファイルを開きます。

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   次に例を示します。

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 設定を選択します。
1. ツールバーの「**ヘルスチェック**」を選択し、「**チェック**」を選択します。

   ![](assets/integrate-target-io-12.png)

1. 成功した場合は、次のメッセージが表示されます。

   ![](assets/integrate-target-io-13.png)

## Adobe TargetCloud Service{#configuring-the-adobe-target-cloud-service}の設定

設定は、Target Standard APIを使用するCloud Service向けに参照できるようになりました。

1. **ツール**&#x200B;メニューを開きます。 次に、「**Cloud Services**」セクションで、「**レガシーCloud Services**」を選択します。
1. **Adobe Target**&#x200B;まで下にスクロールし、「**今すぐ設定**」を選択します。

   **設定を作成**&#x200B;ダイアログが開きます。

1. **タイトル**&#x200B;を入力し、必要に応じて&#x200B;**名前**&#x200B;を入力します（空白の場合、タイトルから生成されます）。

   また、必要なテンプレートを選択することもできます（複数のテンプレートが使用可能な場合）。

1. **作成**&#x200B;で確定します。

   **コンポーネントを編集**&#x200B;ダイアログが開きます。

1. 「**Adobe Target設定**」タブに詳細を入力します。

   * **認証**:IMS
   * **テナントID**:AdobeIMSテナントID。[テナントIDとクライアントコード](#tenant-client)の節も参照してください。

      >[!NOTE]
      >
      >IMSの場合、この値はTarget自体から取得する必要があります。 Targetにログインし、URLからテナントIDを抽出できます。
      >
      >例えば、URLが次のような場合、
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >次に、`yourtenantid`を使用します。
   * **クライアントコード**:テナントIDとク [ライアントコードの節を参照し](#tenant-client) てください。
   * **IMSの設定**:IMS設定の名前を選択します。
   * **APIタイプ**:REST
   * **A4T Analytics クラウド設定**：ターゲットアクティビティの目標と指標に使用する Analytics クラウド設定。これは、コンテンツをターゲット化するときに、Adobe Analytics をレポートソースとして使用している場合に必要です。クラウド設定が表示されない場合は、[A4T Analytics Cloud設定の設定](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration)の注意を参照してください。
   * **正確なターゲット設定を使用する**:デフォルトでは、このチェックボックスはオンになっています。オンにすると、クラウドサービス設定はコンテンツが読み込まれるまでコンテキストの読み込みを待機します。続きのメモを確認してください。
   * **Adobe Targetからのセグメントの同期**:このオプションを選択すると、Targetで定義されたセグメントをダウンロードしてAEMで使用できます。「API のタイプ」プロパティが REST のときは、インラインのセグメントがサポートされておらず、常に Target からセグメントを使用する必要があるので、このオプションをオンにする必要があります（AEM の用語「セグメント」は、Target の「オーディエンス」と同じです）。
   * **クライアントライブラリ**:AT.jsクライアントライブラリとmbox.js（非推奨）のどちらを使用するかを選択します。
   * **タグ管理システムを使用したクライアントライブラリの配信**:DTM（非推奨）、AdobeLaunchまたはその他のタグ管理システムを使用します。
   * **カスタムAT.js**:「タグ管理」ボックスをオンにした場合や、デフォルトのAT.jsを使用する場合は空白のままにします。それ以外の場合は、カスタム AT.js をアップロードします。AT.js を選択した場合にのみ表示されます。

   >[!NOTE]
   >
   >[Target Classic APIを使用するCloud Serviceの設定は廃止されま](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) した(「Adobe Recommendations設定」タブを使用)。
1. 「**Targetに接続**」をクリックして、Adobe Targetとの接続を初期化します。

   接続に成功すると、「**接続に成功しました**」というメッセージが表示されます。

1. メッセージで「**OK**」を選択し、ダイアログで「**OK**」を選択して設定を確認します。
1. 次に、[Targetフレームワーク](/help/sites-administering/target-configuring.md#adding-a-target-framework)の追加に進み、Targetに送信するContextHubまたはClientContextのパラメーターを設定します。 これは、AEMエクスペリエンスフラグメントをTargetに書き出す場合には必要ない場合があります。

### テナントIDとクライアントコード{#tenant-client}

[Adobe Experience Manager 6.5.8.0](/help/release-notes/sp-release-notes.md)では、Target設定ウィンドウに「Client Code」フィールドが追加されていました。

「テナントID 」フィールドと「クライアントコード」フィールドを設定する際は、次の点に注意してください。

1. ほとんどのお客様の場合、テナント ID とクライアントコードは同じです。つまり、両方のフィールドに同じ情報が含まれ、フィールドは同じになります。両方のフィールドにテナント ID を必ず入力してください。
2. 従来の目的では、テナント ID とクライアントコードのフィールドに異なる値を入力することもできます。

どちらの場合も、次の点に注意してください。

* デフォルトでは、（最初に追加された場合は）クライアントコードもテナント ID フィールドに自動的にコピーされます。
* デフォルトのテナント ID 設定を変更するオプションがあります。
* これにより、バックエンドから Target への呼び出しはテナント ID に基づいておこなわれ、クライアントサイドから Target への呼び出しはクライアントコードに基づいておこなわれます。

前述のように、最初の例はAEM 6.5で最も一般的です。どちらの場合も、**両方**&#x200B;のフィールドに、要件に応じた正しい情報が含まれていることを確認してください。

>[!NOTE]
>
> 既存の Target 設定を変更する場合：
>
> 1. テナント ID を再入力します。
> 2. Target に再接続します。
> 3. 設定を保存します。

