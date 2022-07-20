---
title: IMS を使用した Adobe Target との統合
description: IMS を使用した AEM と Adobe Target の統合について説明します
exl-id: 8ddd86d5-a5a9-4907-b07b-b6552d7afdc8
source-git-commit: eb05fb92491932e4c2489c5adb533bbbae1d2870
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 100%

---

# IMS を使用した Adobe Target との統合{#integration-with-adobe-target-using-ims}

Target Standard API を介して AEM と Adobe Target を統合するには、Adobe Developer Console を使用して Adobe IMS（Identity Management System）を設定する必要があります。

>[!NOTE]
>
>Adobe Target Standard API のサポートは、AEM 6.5 の新機能です。Target Standard API は IMS 認証を使用します。
>
>AEM での Adobe Target Classic API の使用は、後方互換性のために引き続きサポートされています。[Target Classic API はユーザーの資格情報認証を使用します](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)。
>
>API の選択は、AEM/Target 統合に使用される認証方法によって決定されます。
>「[テナント ID とクライアントコード](#tenant-client) 」の節も参照してください。

## 前提条件 {#prerequisites}

この手順を開始する前に、以下を実行します。

* [アドビサポート](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html)は、次のアカウントをプロビジョニングする必要があります。

   * アドビコンソール
   * Adobe 開発者コンソール
   * Adobe Target と
   * Adobe IMS（Identity Management System）

* 組織のシステム管理者は、Admin Console を使用して、組織内で必要な開発者を関連する製品プロファイルに追加する必要があります。

   * これにより、Adobe Developer Console 内で統合を有効にするための権限が特定の開発者に与えられます。
   * 詳しくは、[開発者の管理](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)を参照してください。


## IMS 設定の指定 - 公開鍵の生成 {#configuring-an-ims-configuration-generating-a-public-key}

設定の最初の段階は、AEMで IMS 設定を作成し、公開鍵を生成することです。

1. AEM で、**ツール**&#x200B;メニューを開きます。
1. **セキュリティ**&#x200B;セクションで、**Adobe IMS 設定**&#x200B;を選択します。
1. **作成**&#x200B;を選択して、**Adobe IMS テクニカルアカウント設定**&#x200B;を開きます。
1. **クラウド設定**&#x200B;の下のドロップダウンを使用して、**Adobe Target**&#x200B;を選択します。
1. **新しい証明書の作成**&#x200B;をアクティブにして、新しいエイリアスを入力します。
1. 「**証明書の作成**」で確認します。

   ![](assets/integrate-target-io-01.png)

1. **ダウンロード**（または&#x200B;**公開鍵のダウンロード**）を選択してファイルをローカルドライブにダウンロードし、[AEM と Adobe Target 統合のための IMS の設定](#configuring-ims-for-adobe-target-integration-with-aem)時に使用できるようにします。

   >[!CAUTION]
   >
   >この設定は、[AEM で IMS 設定を完了する](#completing-the-ims-configuration-in-aem)ときに再び必要になるため、開いたままにしてください。

   ![](assets/integrate-target-io-02.png)

## AEM と Adobe Target 統合のための IMS 設定 {#configuring-ims-for-adobe-target-integration-with-aem}

Adobe Developer Console を使用して、AEM が使用する Adobe Target とのプロジェクト（統合）を作成し、必要な権限を割り当てる必要があります。

### プロジェクトの作成 {#creating-the-project}

Adobe Developer Console を開いて、AEM が使用する Adobe Target でプロジェクトを作成します。

1. Adobe Developer Console を開いて、プロジェクトを表示します。

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 既に作成したプロジェクトが表示されます。**新規プロジェクトの作成**&#x200B;を選択 - 場所と使用方法は、以下に依存します。

   * まだプロジェクトがない場合は、 **新規プロジェクトを作成**が中央の下に表示されます。
      ![新規プロジェクトの作成 - 最初のプロジェクト](assets/integration-target-io-02.png)
   * 既存のプロジェクトがある場合は、それらがリストされ、 **新規プロジェクトの作成**が右上に表示されます。
      ![新規プロジェクトの作成 - 複数のプロジェクト](assets/integration-target-io-03.png)


1. **プロジェクトに追加**&#x200B;を選択し、続いて **API** を選択します。

   ![](assets/integration-target-io-10.png)

1. **Adobe Target** を選択し、続いて&#x200B;**次へ**&#x200B;を選択します。

   >[!NOTE]
   >
   >Adobe Target を購読しているが、リストに表示されない場合は、 [前提条件](#prerequisites)を確認する必要があります。

   ![](assets/integration-target-io-12.png)

1. **公開鍵**&#x200B;をアップロードして、完了したら&#x200B;**次へ**&#x200B;に進みます。

   ![](assets/integration-target-io-13.png)

1. 資格情報を確認して、**次へ**&#x200B;に進みます。 

   ![](assets/integration-target-io-15.png)

1. 必要な製品プロファイルを選択して、**設定済み API を保存**&#x200B;に進みます。 

   >[!NOTE]
   >
   >で表示される製品プロファイルは、次のものがあるかどうかによって異なります。
   >
   >* Adobe Target Standard - **デフォルトのワークスペース**&#x200B;のみ使用可能です
   >* Adobe Target Premium - 以下に示すように、使用可能なすべてのワークスペースが一覧表示されます


   ![](assets/integration-target-io-16.png)

1. 作成が確定します。

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### 統合への権限の割り当て {#assigning-privileges-to-the-integration}

次に、必要な権限を統合に割り当てる必要があります。

1. Adobe **Admin Console** を開きます。

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. **製品** （上部のツールバー）に移動し、**Adobe Target - &lt;*your-tenant-id*>**（左のパネルから）を選択します。
1. **製品プロファイル**&#x200B;を選択して、表示されるリストから必要なワークスペースを選択します（例：「デフォルトのワークスペース」）。
1. **API 資格情報**&#x200B;を選択して、必要な統合設定を選択します。
1. **製品の役割**&#x200B;として、**オブザーバー**&#x200B;の代わりに&#x200B;**編集者**&#x200B;を選択します。

## Adobe Developer Console 統合プロジェクト用に保存された詳細 {#details-stored-for-the-ims-integration-project}

Adobe Developer Console - プロジェクトから、すべての統合プロジェクトのリストを表示できます。

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

**表示**（特定のプロジェクトエントリの右側）を選択して、設定に関する詳細を表示します。次のものが含まれます。

* プロジェクトの概要
* Insights
* 資格情報
   * サービスアカウント（JWT）
      * 資格情報の詳細
      * JWT の生成
* API
   * 例：Adobe Target

これらの一部は、IMS に基づいて AEM で Adobe Target の統合を完了する必要があります。

## AEM での IMS 設定の完了 {#completing-the-ims-configuration-in-aem}

AEM に戻り、Adobe Developer Console の Target 向け統合から必要な値を追加して、IMS 設定を完了できます。

1. [AEM で IMS 設定を開く](#configuring-an-ims-configuration-generating-a-public-key)に戻ります。
1. 「**次へ**」を選択します。

1. ここで、[Adobe Developer Console のプロジェクト設定からの詳細](#details-stored-for-the-ims-integration-project)を使用できます。

   * **タイトル**：テキスト。
   * **認証サーバー**：以下の&#x200B;**ペイロード**&#x200B;セクションの `aud` 行からこれをコピーして貼り付けます。例：以下の例では `https://ims-na1.adobelogin.com`　
   * **API キー**：これを「[概要](#details-stored-for-the-ims-integration-project)」セクションからコピーします
   * **クライアント秘密鍵**：これを「[概要](#details-stored-for-the-ims-integration-project)」セクションで生成してコピーします
   * **ペイロード**：これを「[JWT を生成](#details-stored-for-the-ims-integration-project)」セクションからコピーします

   ![](assets/integrate-target-io-10.png)

1. 「**作成**」で確認します。

1. Adobe Target の設定が AEM コンソールに表示されます。

   ![](assets/integrate-target-io-11.png)

## IMS 設定の確認 {#confirming-the-ims-configuration}

設定が期待どおりに動作していることを確認するには：

1. 次を開きます。

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   次に例を示します。

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 設定を選択します。
1. ツールバーから&#x200B;**ヘルスチェック**&#x200B;を選択し、次に&#x200B;**チェック**&#x200B;を選択します。

   ![](assets/integrate-target-io-12.png)

1. 成功すると、次のメッセージが表示されます。

   ![](assets/integrate-target-io-13.png)

## Adobe Target Cloud Service の設定 {#configuring-the-adobe-target-cloud-service}

これで、Cloud Service の設定を参照して Target Standard API を使用できるようになりました。

1. **ツール**&#x200B;メニューを開きます。次に、**クラウドサービス**&#x200B;セクション内で、**従来のクラウドサービス**&#x200B;を選択します。
1. **Adobe Target** までスクロールダウンし、「**今すぐ設定**」を選択します。

   **設定の作成**&#x200B;ダイアログが開きます。

1. **タイトル**&#x200B;と、必要に応じて&#x200B;**名前**&#x200B;を入力します（空白の場合、タイトルから生成されます）。

   また、必要なテンプレートを選択することもできます（複数のテンプレートを使用できる場合）。

1. 「**作成**」で確認します。

   **コンポーネントの編集**&#x200B;ダイアログが開きます。

1. **Adobe Target 設定**&#x200B;タブに詳細を入力します。

   * **認証**：IMS

   * **テナント ID**：Adobe IMS テナント ID。[テナント ID とクライアントコード](#tenant-client)セクションも参照してください。

      >[!NOTE]
      >
      >IMS の場合、この値は Target 自体から取得する必要があります。Target にログインし、URL からテナント ID を抽出できます。
      >
      >例えば、URL が次のような場合：
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >次に、`yourtenantid`を使用します。

   * **クライアントコード**：[テナント ID とクライアントコード](#tenant-client)セクションを参照してください。

   * **IMS 設定**：IMS 設定の名前を選択します。

   * **API のタイプ**：REST

   * **A4T Analytics クラウド設定**：ターゲットアクティビティの目標と指標に使用する Analytics クラウド設定を選択します。これは、コンテンツをターゲット化するときに、Adobe Analytics をレポートソースとして使用している場合に必要です。クラウド設定が表示されない場合は、[A4T Analytics クラウド設定の設定](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration)の注意を参照してください。

   * **正確なターゲティングの使用**：デフォルトではこのチェックボックスはオンになっています。オンにすると、クラウドサービス設定はコンテンツが読み込まれるまでコンテキストの読み込みを待機します。続きのメモを確認してください。

   * **Adobe Target からセグメントを同期**：Target で定義されているセグメントをダウンロードして AEM で使用するには、このオプションをオンにします。「API のタイプ」プロパティが REST のときは、インラインのセグメントがサポートされておらず、常に Target からセグメントを使用する必要があるので、このオプションをオンにする必要があります（AEM の用語「セグメント」は、Target の「オーディエンス」と同じです）。

   * **クライアントライブラリ**：AT.js クライアントライブラリと mbox.js（非推奨）のどちらを使用するかを選択します。

   * **タグ管理システムを使用したクライアントライブラリの配信**：DTM（非推奨）、Adobe Launch またはその他のタグ管理システムを使用します。

   * **カスタムの AT.js**：タグ管理ボックスをオンにした場合またはデフォルトの AT.js を使用する場合は空にします。それ以外の場合は、カスタム AT.js をアップロードします。AT.js を選択した場合にのみ表示されます。
   >[!NOTE]
   >
   >[Target Classic API を使用する Cloud Service の設定](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)は廃止されました（「Adobe Recommendations 設定」タブを使用します）。

1. 「**Target に接続**」をクリックして、Adobe Target との接続を初期化します。

   接続に成功すると、「**接続に成功しました**」というメッセージが表示されます。

1. メッセージで **OK** を選択し、ダイアログで **OK** を選択して、設定を確認します。

1. これで、[Target フレームワークの追加](/help/sites-administering/target-configuring.md#adding-a-target-framework)に進んで、Target に送信する ContextHub または ClientContext パラメーターを設定できます。AEM エクスペリエンスフラグメントを Target に書き出す場合は、この設定が不要な場合があります。

### テナント ID と クライアントコード {#tenant-client}

[Adobe Experience Manager 6.5.8.0](/help/release-notes/release-notes.md) では、Target 設定ウィンドウに「クライアントコード」フィールドが追加されました。

テナント ID と クライアントコードのフィールドを設定する場合は、次の点に注意してください。

1. ほとんどのお客様の場合、テナント ID とクライアントコードは同じです。つまり、両方のフィールドに同じ情報が含まれ、フィールドは同じになります。両方のフィールドにテナント ID を必ず入力してください。
2. 従来の目的では、テナント ID とクライアントコードのフィールドに異なる値を入力することもできます。

どちらの場合も、次の点に注意してください。

* デフォルトでは、（最初に追加された場合は）クライアントコードもテナント ID フィールドに自動的にコピーされます。
* デフォルトのテナント ID 設定を変更するオプションがあります。
* これにより、バックエンドから Target への呼び出しはテナント ID に基づいて行われ、クライアントサイドから Target への呼び出しはクライアントコードに基づいて行われます。

前述のように、AEM 6.5 では最初のケースが最も一般的です。いずれにせよ、**両方**&#x200B;のフィールドに、要件に応じた正しい情報が含まれていることを確認してください。

>[!NOTE]
>
> 既存の Target 設定を変更する場合：
>
> 1. テナント ID を再入力します。
> 2. Target に再接続します。
> 3. 設定を保存します。

