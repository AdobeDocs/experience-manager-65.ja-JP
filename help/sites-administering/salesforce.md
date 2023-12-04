---
title: Salesforce との統合
description: Adobe Experience Manager (AEM) と Salesforce の統合について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0f3aaa0a-ccfb-4162-97a6-ee5485595d28
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 27%

---


# Salesforce との統合 {#integrating-with-salesforce}

Salesforce とAdobe Experience Manager(AEM) の統合により、リード管理機能が提供され、Salesforce が標準で提供する既存の機能を使用できます。 リードを Salesforce に投稿し、Salesforce から直接データにアクセスするコンポーネントを作成するようにAEMを設定できます。

AEMと Salesforce の双方向で拡張可能な統合により、次のことが可能になります。

* 顧客体験を強化するために、データを完全に使用および修正する組織。
* マーケティングからセールス活動へのエンゲージメント。
* Salesforce データストアからデータを自動的に送受信する組織。

このドキュメントは次の内容について説明します。

* SalesforceCloud Serviceの設定方法 (AEMを Salesforce と統合するように設定 )。
* ClientContext での Salesforce リード/連絡先情報の使用方法と、パーソナライゼーションの使用方法。
* Salesforce ワークフローモデルを使用してAEMユーザーを Salesforce にリードとして投稿する方法。
* Salesforce のデータを表示するコンポーネントの作成方法。

## Salesforce と統合するAEMの設定 {#configuring-aem-to-integrate-with-salesforce}

AEMと Salesforce を統合するように設定するには、まず Salesforce でリモートアクセスアプリケーションを設定します。 次に、このリモートアクセスアプリケーションを指すように Salesforce クラウドサービスを設定します。

>[!NOTE]
>
>Salesforce で無料の開発者アカウントを作成できます。

Salesforce と統合するAEMを設定するには：

>[!CAUTION]
>
>をインストールします。 [Salesforce API](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=salesforce*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=2&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcom.adobe.cq.mcm.salesforce.content-1.0.4.zip) 統合パッケージを使用してください。 パッケージの操作方法について詳しくは、[パッケージの使用方法](/help/sites-administering/package-manager.md#package-share)ページを参照してください。

1. AEM で「**クラウドサービス**」に移動します。「サードパーティのサービス」で、「**Salesforce**」の「**今すぐ設定**」をクリックします。

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 設定を作成します（例： ）。 **開発者**.

   >[!NOTE]
   >
   >新しい設定は、新しいページにリダイレクトされます。 **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. これは、Salesforce でリモートアクセスアプリケーションを作成する際にコールバック URL で指定する必要がある値とまったく同じです。 これらの値が一致しなければなりません。

1. Salesforce アカウントにログインします ( ログインしていない場合は、 [https://developer.salesforce.com](https://developer.salesforce.com).)
1. Salesforce で、に移動します。 **作成** > **アプリ** ～に行く **接続済みアプリ** ( 以前のバージョンの Salesforce では、ワークフローは **デプロイ** > **リモートアクセス**) をクリックします。
1. クリック **新規** AEMと Salesforce を連携できます。

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. 次を入力します。 **接続されたアプリ名**, **API 名**、および **連絡先メール**. を選択します。 **OAuth 設定を有効にする** チェックボックスをオンにし、 **コールバック URL** OAuth 範囲（フルアクセスなど）を追加します。 コールバック URL は以下のようになります。`http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   設定に合わせてサーバー名／ポート番号およびページ名を変更します。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. クリック **保存** Salesforce 設定を保存します。 Salesforce が、AEM 設定に必要な&#x200B;**消費者キー**&#x200B;と&#x200B;**消費者の秘密鍵**&#x200B;を作成します。

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >Salesforce のリモートアクセスアプリケーションがアクティブ化されるまで、数分（最大 15 分）待ちます。

1. AEMで、に移動します。 **Cloud Service** 前に作成した Salesforce 設定（例： ）に移動します。 **開発者**) をクリックします。 クリック **編集** salesforce.comから、顧客キーおよび顧客秘密鍵を入力します。

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | ログイン URL | これは Salesforce 認証エンドポイントです。 この値は事前入力されており、ほとんどの場合に役立ちます。 |
   |---|---|
   | 顧客キー | salesforce.comの「リモートアクセスアプリケーションの登録」ページから取得した値を入力します。 |
   | 顧客秘密鍵 | salesforce.comの「リモートアクセスアプリケーションの登録」ページから取得した値を入力します。 |

1. クリック **Salesforce に連携** 接続するには Salesforce は、設定から Salesforce への接続を許可するように要求します。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   AEM に、正常に接続されたことを示す確認ダイアログが表示されます。

1. Web サイトのルートページに移動して、「**ページプロパティ**」をクリックします。「**クラウドサービス**」を選択し、「**Salesforce**」を追加して、正しい設定（例：**developer**）を選択します。

   ![chlimage_1-75](assets/chlimage_1-75.png)

   これで、ワークフローモデルを使用して、リードを Salesforce に投稿し、Salesforce のデータにアクセスするコンポーネントを作成できます。

## AEMユーザーを Salesforce リードとしてエクスポート中 {#exporting-aem-users-as-salesforce-leads}

AEMユーザーを Salesforce リードとしてエクスポートする場合は、リードを Salesforce に投稿するようにワークフローを設定します。

AEMユーザーを Salesforce リードとしてエクスポートするには：

1. `http://localhost:4502/workflow` で、「**Salesforce.com でのエクスポート**」ワークフローを右クリックし、「**開始**」をクリックして、この Salesforce ワークフローに移動します。

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. リードとして作成するAEMユーザーを **ペイロード** このワークフロー用（ホーム/ユーザー）。 ユーザーのプロファイルノードは、次のような情報が含まれているので、必ず選択してください。 **givenName**、および  **familyName**(Salesforce リードの **名** および **姓** フィールド。

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >このワークフローを開始する前に、必須フィールドを設定します。AEM のリードノードには、Salesforce に公開する前に設定しておく必要がある必須フィールドがいくつかあります。以下が該当します。 **givenName**, **familyName**, **会社**、および **電子メール**. AEMユーザーと Salesforce リードのマッピングの完全なリストを確認するには、 [AEMユーザーと Salesforce リードのマッピング設定。](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. 「**OK**」をクリックします。ユーザー情報はsalesforce.comに書き出されます。 salesforce.comで確認できます。

   >[!NOTE]
   >
   >エラーログには、リードがインポートされたかどうかが示されます。 詳しくは、エラーログを確認してください。

### Salesforce.comエクスポートワークフローの設定 {#configuring-the-salesforce-com-export-workflow}

必要に応じて、適切なSalesforce.com設定に合わせてSalesforce.comエクスポートワークフローを設定するか、その他の変更を行います。

Salesforce.comエクスポートワークフローを設定するには：

1. `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.` に移動します。

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. 「Salesforce.com でのエクスポート」ステップを開き、「**引数**」タブを選択し、正しい設定を選択して「**OK**」をクリックします。さらに、Salesforce で削除されたリードをワークフローで再作成する場合は、このチェックボックスをオンにします。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 「**保存**」をクリックして変更を保存します。

   ![chlimage_1-79](assets/chlimage_1-79.png)

### AEM ユーザーと Salesforce のリードのマッピング設定 {#mapping-configuration-between-aem-user-and-salesforce-lead}

AEM ユーザーと Salesforce リードの現在のマッピング設定を表示または編集するには、Configuration Manager（`https://<hostname>:<port>/system/console/configMgr`）を開いて「**Salesforce Lead Mapping Configuration**」を検索します。

1. 「**Web コンソール**」をクリックするか、直接 `https://<hostname>:<port>/system/console/configMgr.` にアクセスして Configuration Manager を開きます。
1. 「**Salesforce Lead Mapping Configuration**」を検索します。

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 必要に応じてマッピングを変更します。デフォルトのマッピングは、**aemUserAttribute=sfLeadAttribute** というパターンになります。「**保存**」をクリックして変更を保存します。

## Salesforce ClientContext Store の設定 {#configuring-salesforce-client-context-store}

Salesforce クライアントコンテキストストアには、AEM内で既に利用可能な情報よりも、現在ログインしているユーザーに関する追加情報が表示されます。 ユーザーと Salesforce の連携に応じて、この追加情報を Salesforce から取り込みます。

これをおこなうには、次の設定を行います。

1. Salesforce Connect コンポーネントを使用して、AEMユーザーを Salesforce ID にリンクします。
1. Salesforce プロファイルデータを ClientContext ページに追加して、表示するプロパティを設定できます。
1. （オプション）Salesforce Client Context Store のデータを使用するセグメントを作成します。

### AEMユーザーと Salesforce ID のリンク {#linking-an-aem-user-with-a-salesforce-id}

AEMユーザーを Salesforce ID にマッピングして、ClientContext に読み込めるようにします。 実際のシナリオでは、既知のユーザーデータに基づいてリンクし、検証をおこないます。 デモ用に、この手順では、 **Salesforce Connect** コンポーネント。

1. AEMで Web サイトに移動し、ログインして、 **Salesforce Connect** サイドキックからコンポーネントを選択します。

   >[!NOTE]
   >
   >次の場合、 **Salesforce Connect** コンポーネントが使用できません。次に移動してください： **デザイン** 表示して選択し、で使用できるようにします。 **編集** 表示。

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   コンポーネントをページにドラッグすると、「**Salesforce へのリンク**」が「オフ」と表示されます。

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >このコンポーネントは、デモ目的でのみ使用します。 実際のシナリオでは、ユーザーをリードとリンク/マッチングする別のプロセスが存在します。

1. ページ上にコンポーネントをドラッグした後、開いて設定します。 設定、連絡先のタイプ、Salesforce のリードまたは連絡先を選択し、 **OK**.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM がユーザーと Salesforce の連絡先またはリードをリンクします。

   ![chlimage_1-83](assets/chlimage_1-83.png)

### ClientContext への Salesforce データの追加 {#adding-salesforce-data-to-client-context}

ClientContext で Salesforce からユーザーデータを読み込み、パーソナライゼーションに使用できます。

1. 拡張する ClientContext を開きます（例： ）。 `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. **Salesforce プロフィールデータ**&#x200B;コンポーネントを ClientContext にドラッグします。

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. コンポーネントをダブルクリックして開きます。 選択 **項目を追加** をクリックし、ドロップダウンリストからプロパティを選択します。 必要な数のプロパティを追加して、「 」を選択します。 **OK**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. これで、Salesforce 固有のプロパティが ClientContext に表示されます。

   ![chlimage_1-85](assets/chlimage_1-85.png)

### Salesforce Client Context Store のデータを使用したセグメントの作成 {#building-a-segment-using-data-from-salesforce-client-context-store}

Salesforce Client Context Store のデータを使用するセグメントを構築できます。 次の手順を実行します。

1. **ツール**／**セグメント化**&#x200B;に移動するか、[http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation) に移動して、AEM のセグメント化に移動します。
1. セグメントを作成または更新して、Salesforce のデータを含めます。 詳しくは、 [セグメント化](/help/sites-administering/campaign-segmentation.md).

## リードを検索中 {#searching-leads}

AEMには、指定した条件に従って Salesforce 内のリードを検索する、サンプルの検索コンポーネントが付属しています。 このコンポーネントでは、Salesforce REST API を使用して Salesforce オブジェクトを検索する方法を示します。 salesforce.comへの呼び出しをトリガーするには、Salesforce 設定にページをリンクします。

>[!NOTE]
>
>これは、Salesforce REST API を使用して Salesforce オブジェクトに対してクエリを実行する方法を示すサンプルコンポーネントです。 これを例として使用し、ニーズに基づいて、より複雑なコンポーネントを作成します。

このコンポーネントを使用するには：

1. この設定を使用するページに移動します。 ページのプロパティを開き、「 」を選択します。 **Cloud Service。** クリック **サービスを追加** を選択し、 **Salesforce** をクリックし、適切な設定を行って、 **OK**.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. Salesforce 検索コンポーネントを（有効になっている場合）ページにドラッグします。 有効にするには、デザインモードに移動し、適切な領域に追加します )。

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. 検索コンポーネントを開き、検索パラメーターを指定して、「**OK**」をクリックします。

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. 検索コンポーネントで指定した条件に一致するリードが表示されます。

   ![chlimage_1-87](assets/chlimage_1-87.png)
