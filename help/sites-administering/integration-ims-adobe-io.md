---
title: Adobe I/O を使用した Adobe Target との統合
seo-title: Integration with Adobe Target using Adobe I/O
description: Adobe I/Oを使用したAEMとAdobe Targetの統合について説明します
seo-description: Learn about integrating AEM with Adobe Target using Adobe I/O
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
exl-id: ba7abc53-7db8-41b1-a0fa-4e4dbbeca402
source-git-commit: 9fbf338b18e73fbd272af061381baf34b694239a
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 18%

---

# Adobe I/O を使用した Adobe Target との統合{#integration-with-adobe-target-using-adobe-i-o}

Target Standard API を使用してAEMとAdobe Targetを統合するには、Adobe IMS(Identity Management System) とAdobe I/Oの設定が必要です。

>[!NOTE]
>
>AEM 6.5 で新しく導入されたAdobe Target Standard API のサポート。Target Standard API は IMS 認証を使用します。
>
>AEMでのAdobe Target Classic API の使用は、後方互換性のために引き続きサポートされます。 この [Target Classic API はユーザーの資格情報認証を使用します](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>API の選択は、AEM/Target 統合に使用される認証方法によって実行されます。
>関連トピック [テナント ID とクライアントコード](#tenant-client) 」セクションに入力します。

## 前提条件 {#prerequisites}

この手順を開始する前に、以下を実行します。

* [Adobeサポート](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html) は次のアカウントをプロビジョニングする必要があります。

   * Adobeコンソール
   * Adobe I/O
   * Adobe Targetと
   * Adobe IMS(Identity Management System)

* 組織のシステム管理者は、Admin Consoleを使用して、組織内の必要なデベロッパーを関連する製品プロファイルに追加する必要があります。

   * これにより、特定の開発者に、開発内で統合を有効にする権限をAdobe I/Oできます。
   * 詳しくは、 [開発者の管理](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## IMS 設定の指定 — 公開鍵の生成 {#configuring-an-ims-configuration-generating-a-public-key}

設定の最初の段階は、AEMで IMS 設定を作成し、公開鍵を生成することです。

1. AEMで、 **ツール** メニュー
1. 内 **セキュリティ** セクション選択 **Adobe IMS設定**.
1. 選択 **作成** 開く **Adobe IMSテクニカルアカウント設定**.
1. 下のドロップダウンを使用 **クラウド設定**&#x200B;を選択します。 **Adobe Target**.
1. 有効化 **新しい証明書を作成** 新しいエイリアスを入力します。
1. 次で確認： **証明書を作成**.

   ![](assets/integrate-target-io-01.png)

1. 選択 **ダウンロード** ( または **公開鍵をダウンロード**) をクリックして、ファイルをローカルドライブにダウンロードし、 [Adobe TargetとAEMの統合のためのAdobe I/Oの設定](#configuring-adobe-i-o-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >この設定を開いたままにします。 [AEMでの IMS 設定の完了](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## Adobe TargetとAEMの統合用のAdobe I/Oの設定 {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

AEMが使用するAdobe I/Oプロジェクト（統合）をAdobe Targetで作成し、必要な権限を割り当てる必要があります。

### プロジェクトの作成 {#creating-the-project}

Adobe I/Oコンソールを開き、AEMが使用するAdobe Targetで I/O プロジェクトを作成します。

>[!NOTE]
>
>関連トピック [Adobe I/Oチュートリアル](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html).

1. プロジェクトのAdobe I/Oコンソールを開きます。

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. 既に作成したプロジェクトが表示されます。 選択 **新規プロジェクトを作成**  — 場所と使用方法は、次のものに依存します。

   * まだプロジェクトがない場合は、 **新規プロジェクトを作成** 中央、下に配置します。
      ![新規プロジェクトを作成 — 最初のプロジェクト](assets/integration-target-io-02.png)
   * 既存のプロジェクトがある場合は、それらがリストされ、 **新規プロジェクトを作成** が右上に表示されます。
      ![新規プロジェクトを作成 — 複数のプロジェクト](assets/integration-target-io-03.png)


1. 選択 **プロジェクトに追加** 続いて **API**:

   ![](assets/integration-target-io-10.png)

1. 選択 **Adobe Target**&#x200B;を、 **次へ**:

   >[!NOTE]
   >
   >Adobe Targetを購読しているが、リストに表示されない場合は、 [前提条件](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **公開鍵をアップロード**&#x200B;をクリックし、完了したら次の操作を続行します。 **次へ**:

   ![](assets/integration-target-io-13.png)

1. 資格情報を確認し、次に進みます。 **次へ**:

   ![](assets/integration-target-io-15.png)

1. 必要な製品プロファイルを選択し、次に進みます。 **設定済み API を保存**:

   >[!NOTE]
   >
   >と共に表示される製品プロファイルは、次の条件によって異なります。
   >
   >* Adobe Target Standard — のみ **デフォルトのワークスペース** 使用可能な
   >* Adobe Target Premium — 使用可能なすべてのワークスペースが、次に示すようにリストされます


   ![](assets/integration-target-io-16.png)

1. 作成が確定されます。

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### 統合への権限の割り当て {#assigning-privileges-to-the-integration}

次に、必要な権限を統合に割り当てる必要があります。

1. Adobeを開く **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. に移動します。 **製品** （上部のツールバー）、「 **Adobe Target - &lt;*your-tenant-id*>** （左のパネルから）。
1. 選択 **製品プロファイル**&#x200B;を選択し、表示されるリストから必要なワークスペースを選択します。 例えば、「デフォルトのワークスペース」などです。
1. 選択 **統合**&#x200B;を選択し、必要な統合設定を選択します。
1. 選択 **編集者** を **製品の役割**;の代わりに **監視者**.

## Adobe I/O統合プロジェクト用に保存された詳細 {#details-stored-for-the-adobe-io-integration-project}

Adobe I/Oプロジェクトコンソールから、すべての統合プロジェクトのリストを表示できます。

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

選択 **表示** （特定のプロジェクトエントリの右側）をクリックして、設定に関する詳細を表示します。 次の機能が含まれます。

* プロジェクトの概要
* インサイト
* 秘密鍵証明書
   * サービスアカウント (JWT)
      * 資格情報の詳細
      * JWT を生成
* API
   * 例： Adobe Target

これらの一部は、AEMで Target のAdobe I/O統合を完了する必要があります。

## AEMでの IMS 設定の完了 {#completing-the-ims-configuration-in-aem}

AEMに戻ると、Target のAdobe I/O統合から必要な値を追加することで、IMS 設定を完了できます。

1. に戻る [AEMで IMS 設定を開く](#configuring-an-ims-configuration-generating-a-public-key).
1. 「**次へ**」を選択します。

1. ここで、 [Adobe I/Oの詳細](#details-stored-for-the-adobe-io-integration-project):

   * **タイトル**:テキスト。
   * **認証サーバー**:次の場所からコピー&amp;ペースト `aud` 行 **ペイロード** の下のセクション、例： `https://ims-na1.adobelogin.com` 以下の例では
   * **API キー**:これを [概要](#details-stored-for-the-adobe-io-integration-project) Target のAdobe I/O統合の節
   * **クライアント秘密鍵**:これを [概要](#details-stored-for-the-adobe-io-integration-project) Target のAdobe I/O統合のセクション、
   * **ペイロード**:これを [JWT を生成](#details-stored-for-the-adobe-io-integration-project) Target のAdobe I/O統合の節

   ![](assets/integrate-target-io-10.png)

1. 「**作成**」で確定します。

1. Adobe Targetの設定がAEMコンソールに表示されます。

   ![](assets/integrate-target-io-11.png)

## IMS 設定の確認 {#confirming-the-ims-configuration}

設定が期待どおりに動作していることを確認するには：

1. 次を開きます：:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   次に例を示します。

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 設定を選択します。
1. 選択 **ヘルスチェック** ツールバーから、 **チェック**.

   ![](assets/integrate-target-io-12.png)

1. 成功した場合は、次のメッセージが表示されます。

   ![](assets/integrate-target-io-13.png)

## Adobe TargetCloud Serviceの設定 {#configuring-the-adobe-target-cloud-service}

これで、Target Standard API を使用するCloud Serviceに対して、設定を参照できるようになりました。

1. を開きます。 **ツール** メニュー 次に、 **Cloud Services** セクション、選択 **従来のCloud Services**.
1. 下にスクロールして **Adobe Target** を選択し、 **今すぐ設定**.

   この **設定を作成** ダイアログが開きます。

1. を入力します。 **タイトル** 必要に応じて、 **名前** （空白の場合、タイトルから生成されます）。

   また、必要なテンプレートを選択することもできます（複数のテンプレートを使用できる場合）。

1. 「**作成**」で確定します。

   この **コンポーネントを編集** ダイアログが開きます。

1. 詳細を **Adobe Target Settings** タブ：

   * **認証**:IMS

   * **テナント ID**:Adobe IMSテナント ID。 関連トピック [テナント ID とクライアントコード](#tenant-client) 」セクションに入力します。

      >[!NOTE]
      >
      >IMS の場合、この値は Target 自体から取得する必要があります。 Target にログインし、URL からテナント ID を抽出できます。
      >
      >例えば、URL が次のような場合、
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >次に、 `yourtenantid`.

   * **クライアントコード**:詳しくは、 [テナント ID とクライアントコード](#tenant-client) 」セクションに入力します。

   * **IMS 設定**:IMS 設定の名前を選択します。

   * **API タイプ**:REST

   * **A4T Analytics クラウド設定**：ターゲットアクティビティの目標と指標に使用する Analytics クラウド設定。これは、コンテンツをターゲット化するときに、Adobe Analytics をレポートソースとして使用している場合に必要です。クラウド設定が表示されない場合は、 [A4T Analytics Cloud設定の指定](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).

   * **正確なターゲット設定を使用**:デフォルトでは、このチェックボックスはオンになっています。 オンにすると、クラウドサービス設定はコンテンツが読み込まれるまでコンテキストの読み込みを待機します。続きのメモを確認してください。

   * **Adobe Targetからセグメントを同期**:このオプションを選択すると、Target で定義されたセグメントをダウンロードしてAEMで使用することができます。 「API のタイプ」プロパティが REST のときは、インラインのセグメントがサポートされておらず、常に Target からセグメントを使用する必要があるので、このオプションをオンにする必要があります（AEM の用語「セグメント」は、Target の「オーディエンス」と同じです）。

   * **クライアントライブラリ**:AT.js クライアントライブラリと mbox.js（非推奨）のどちらを使用するかを選択します。

   * **タグ管理システムを使用したクライアントライブラリの配信**:DTM（非推奨）、AdobeLaunch、またはその他のタグ管理システムを使用します。

   * **カスタムの AT.js**:「Tag Management」ボックスをオンにした場合、またはデフォルトの AT.js を使用する場合は空白のままにします。 それ以外の場合は、カスタム AT.js をアップロードします。AT.js を選択した場合にのみ表示されます。
   >[!NOTE]
   >
   >[Target Classic API を使用するCloud Serviceの設定](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) は廃止されました (「 Adobe Recommendations設定」タブを使用します )。

1. クリック **Target に接続** :Adobe Targetとの接続を初期化します。

   接続に成功すると、「**接続に成功しました**」というメッセージが表示されます。

1. 選択 **OK** メッセージに続いて **OK** をクリックして、設定を確認します。

1. 次に進むことができます： [Target フレームワークの追加](/help/sites-administering/target-configuring.md#adding-a-target-framework) :Target に送信する ContextHub またはClientContextのパラメーターを設定します。 AEMエクスペリエンスフラグメントを Target に書き出す場合は、この設定が不要な場合があります。

### テナント ID とクライアントコード {#tenant-client}

を使用 [Adobe Experience Manager 6.5.8.0](/help/release-notes/release-notes.md)の場合、「クライアントコード」フィールドが Target 設定ウィンドウに追加されていました。

「テナント ID 」フィールドと「クライアントコード」フィールドを設定する際は、次の点に注意してください。

1. ほとんどのお客様の場合、テナント ID とクライアントコードは同じです。つまり、両方のフィールドに同じ情報が含まれ、フィールドは同じになります。両方のフィールドにテナント ID を必ず入力してください。
2. 従来の目的では、テナント ID とクライアントコードのフィールドに異なる値を入力することもできます。

どちらの場合も、次の点に注意してください。

* デフォルトでは、（最初に追加された場合は）クライアントコードもテナント ID フィールドに自動的にコピーされます。
* デフォルトのテナント ID 設定を変更するオプションがあります。
* これにより、バックエンドから Target への呼び出しはテナント ID に基づいて行われ、クライアントサイドから Target への呼び出しはクライアントコードに基づいて行われます。

前述のように、最初のケースはAEM 6.5 で最も一般的です。どちらの方法でも、次の点を確認してください。 **両方** フィールドには、必要に応じて正しい情報が含まれます。

>[!NOTE]
>
> 既存の Target 設定を変更する場合：
>
> 1. テナント ID を再入力します。
> 2. Target に再接続します。
> 3. 設定を保存します。

