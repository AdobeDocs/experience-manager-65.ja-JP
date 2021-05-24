---
title: Adobe Campaign 6.1 および Adobe Campaign Standard の使用
seo-title: Adobe Campaign 6.1 および Adobe Campaign Standard の使用
description: AEM で電子メールコンテンツを作成して、Adobe Campaign の電子メールで処理することができます。
seo-description: AEM で電子メールコンテンツを作成して、Adobe Campaign の電子メールで処理することができます。
uuid: 439df7fb-590b-45b8-9768-565b022a808b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 61b2bd47-dcef-4107-87b1-6bf7bfd3043b
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 62%

---

# Adobe Campaign 6.1 および Adobe Campaign Standard の使用{#working-with-adobe-campaign-and-adobe-campaign-standard}

AEM で電子メールコンテンツを作成して、Adobe Campaign の電子メールで処理することができます。これを実行するには、次の手順に従う必要があります。

1. AEM で、Adobe Campaign 固有のテンプレートから新しいニュースレターを作成します。
1. コンテンツを編集する前に、すべての機能にアクセスするために [Adobe Campaign サービス](#selectingtheadobecampaigncloudservice)を選択します。
1. コンテンツを編集します。
1. コンテンツを検証します。

これで、コンテンツを Adobe Campaign での配信と同期できるようになります。詳細な手順についてはこのドキュメントで説明します。

>[!NOTE]
>
>この機能を使用するには、AEM を [Adobe Campaign](/help/sites-administering/campaignonpremise.md) または [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) と連携するように設定する必要があります。

## Adobe Campaign を使用した電子メールコンテンツの送信  {#sending-email-content-via-adobe-campaign}

AEM と Adobe Campaign を設定すると、電子メール配信コンテンツを AEM 内で直接作成した後に、それを Adobe Campaign 内で処理できます。

AEMでAdobe Campaignコンテンツを作成する場合、すべての機能にアクセスするには、コンテンツを編集する前にAdobe Campaignサービスにリンクする必要があります。

次の 2 つのケースが考えられます。

* コンテンツを Adobe Campaign からの配信と同期する場合。この場合は、AEM コンテンツを配信に使用できます。
* （オンプレミスの Adobe Campaign のみ）コンテンツを Adobe Campaign に直接送信する場合。この場合は、Adobe Campaign が新しい電子メール配信を自動的に生成します。このモードには制限事項があります。

詳細な手順についてはこのドキュメントで説明します。

### 新しい電子メールコンテンツの作成  {#creating-new-email-content}

>[!NOTE]
>
>電子メールテンプレートを追加する場合は、必ず&#x200B;**/content/campaigns**&#x200B;の下に追加して、使用可能にしてください。


1. AEMで、**Webサイト**&#x200B;フォルダーを選択し、エクスプローラーを参照して電子メールキャンペーンの管理先を見つけます。 次の例では、関連するGeometrixx Outdoorsは&#x200B;**Webサイト** > **キャンペーン** > **** > **電子メールキャンペーン**&#x200B;です。

   >[!NOTE]
   >
   >[電子メールのサンプルは、Geometrixx でのみ使用できます](/help/sites-developing/we-retail.md#weretail)。パッケージ共有からサンプルGeometrixxコンテンツをダウンロードしてください。

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. **新しい** / **新しいページ**&#x200B;を選択して、新しいEメールコンテンツを作成します。
1. Adobe Campaign 固有の使用可能なテンプレートのいずれかを選択し、ページの一般的なプロパティを入力します。デフォルトでは、次の 3 つのテンプレートが使用可能です。

   * **Adobe Campaign電子メール(AC 6.1)**:では、コンテンツを配信用にAdobe Campaign 6.1に送信する前に、事前定義済みのテンプレートに追加できます。
   * **Adobe Campaign Eメール(ACS)**:では、コンテンツを配信用にAdobe Campaign Standardに送信する前に、定義済みのテンプレートに追加できます。

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. 「**作成**」をクリックして、電子メールまたはニュースレターを作成します。

### Adobe Campaign クラウドサービスおよびテンプレートの選択 {#selecting-the-adobe-campaign-cloud-service-and-template}

Adobe Campaign と統合するには、Adobe Campaign クラウドサービスをページに追加する必要があります。これにより、パーソナライズ機能や他の Adobe Campaign 情報にアクセスできるようになります。

さらに、Adobe Campaign テンプレートを選択し、件名を変更したり、HTML 表示を使用しない受信者向けのプレーンテキストのコンテンツを追加したりすることが必要な場合もあります。

1. サイドキックの「**ページ**」タブを選択し、「**ページのプロパティ**」を選択します。
1. ポップアップウィンドウの「**クラウドサービス**」タブで、「**サービスを追加**」を選択してAdobe Campaignサービスを追加し、「**OK**」をクリックします。

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. 使用するAdobe Campaignインスタンスに一致する設定をドロップダウンリストから選択し、「**OK**」をクリックします。

   >[!NOTE]
   >
   >クラウドサービスを追加した後、必ず「**OK**」または「**適用**」をタップまたはクリックしてください。そうすると、「**Adobe Campaign**」タブが正しく機能するようになります。

1. (Adobe Campaignの)特定のEメール配信テンプレートを、デフォルトの&#x200B;**mail**&#x200B;テンプレート以外で適用する場合は、「**ページのプロパティ**」を再度選択します。 「**Adobe Campaign**」タブで、関連するAdobe CampaignインスタンスでEメール配信テンプレートの内部名を入力します。

   Adobe Campaign Standard では、このテンプレートは「**AEM コンテンツで配信**」です。Adobe Campaign 6.1 では、このテンプレートは「**AEM コンテンツで E メール配信**」です。

   テンプレートを選択すると、AEMは自動的に&#x200B;**Adobe Campaignニュースレター**&#x200B;コンポーネントを有効にします。

### 電子メールコンテンツの編集 {#editing-email-content}

クラシック UI またはタッチ操作向け UI のどちらでも、電子メールコンテンツを編集できます。

1. ツールボックスから&#x200B;**ページのプロパティ** > **Email**&#x200B;を選択して、電子メールの件名とテキストバージョンを入力します。

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. サイドキックから要素を適宜追加して、電子メールコンテンツを編集します。要素を追加するにはドラッグ＆ドロップします。その後、編集する要素をダブルクリックします。

   例えば、パーソナライゼーションフィールドを含むテキストを追加できます。

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Adobe Campaign のニュースレターまたは電子メールキャンペーンに使用できるコンポーネントについては、[Adobe Campaign コンポーネント](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)を参照してください。

   ![chlimage_1-177](assets/chlimage_1-177.png)

### パーソナライゼーションの挿入 {#inserting-personalization}

コンテンツを編集するとき、次のものを挿入できます。

* Adobe Campaign コンテキストフィールド。これらは、受信者のデータ（名、姓、ターゲットディメンションの任意のデータなど）に応じて適応する、テキスト内に挿入できるフィールドです。
* Adobe Campaign パーソナライゼーションブロック。これらは、ブランドロゴやミラーページへのリンクなど、受信者のデータとは関係のない定義済みコンテンツのブロックです。

Adobe Campaign コンテンツの詳細については、[Adobe Campaign コンポーネント](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)を参照してください。

>[!NOTE]
>
>* Adobe Campaign の「**プロファイル**」ターゲティングディメンションのフィールドのみが考慮されます。
>* **Sites**&#x200B;からプロパティを表示する場合、Adobe Campaignのコンテキストフィールドにアクセスできません。 これらのフィールドには編集時に電子メール内から直接アクセスできます。

>



1. 新しい&#x200B;**ニュースレター** / **テキスト&amp;パーソナライゼーション(Campaign)**&#x200B;コンポーネントを挿入します。
1. ダブルクリックしてコンポーネントを開きます。**編集**&#x200B;ウィンドウには、パーソナライゼーション要素を挿入できる機能があります。

   >[!NOTE]
   >
   >使用可能なコンテキストフィールドは、Adobe Campaign の「**プロファイル**」ターゲティングディメンションに対応しています。
   >
   >[Adobe Campaign電子メールへのAEMページのリンク](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail)を参照してください。

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. サイドキックで「 **ClientContext** 」を選択し、ペルソナプロファイルのデータを使用してパーソナライゼーションフィールドをテストします。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. ウィンドウが表示され、適切なペルソナを選択できます。パーソナライゼーションフィールドの値は、選択したプロファイルのデータで自動的に置き換えられます。

   ![chlimage_1-180](assets/chlimage_1-180.png)

### ニュースレターのプレビュー {#previewing-a-newsletter}

パーソナライゼーションと同様に、ニュースレターもプレビューすることができます。

1. プレビューするニュースレターを開き、プレビュー（虫眼鏡アイコン）をクリックすると、サイドキックが小さく折りたたまれます。
1. 電子メールクライアントのアイコンをクリックすると、各電子メールクライアントでニュースレターがどのように表示されるかを確認できます。

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. 編集を再開するには、サイドキックを展開します。

### AEM でのコンテンツの承認  {#approving-content-in-aem}

コンテンツの作成が完了したら、承認プロセスを開始できます。ツールボックスの「**ワークフロー**」タブに移動し、「**Adobe Campaignの承認**」ワークフローを選択します。

この既製のワークフローには、改訂して承認または改訂して拒否という 2 つのステップがあります。このワークフローを拡張して、より複雑なプロセスに適合させることができます。

![chlimage_1-182](assets/chlimage_1-182.png)

Adobe Campaignのコンテンツを承認するには、サイドキックで「**Workflow**」を選択し、「**Adobe Campaignの承認**」を選択して、「**ワークフローを開始**」をクリックして、ワークフローを適用します。 手順を完了し、コンテンツを承認します。 ワークフローの最後のステップで、「**承認**」の代わりに「**拒否**」を選択して、コンテンツを拒否することもできます。

![chlimage_1-183](assets/chlimage_1-183.png)

コンテンツを承認すると、承認済みとして Adobe Campaign に表示されます。すると、電子メールを送信できるようになります。

Adobe Campaign Standard の場合：

![chlimage_1-184](assets/chlimage_1-184.png)

Adobe Campaign 6.1 の場合：

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>未承認のコンテンツは、Adobe Campaign の配信と同期できますが、配信を実行することはできません。Adobe Campaign の配信を使用して送信できるのは、承認済みのコンテンツだけです。

## AEM と Adobe Campaign Standard および Adobe Campaign 6.1 のリンク  {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>詳しくは、標準のオーサリングドキュメントの[Adobe Campaign 6.1とAdobe Campaign Standard](/help/sites-authoring/campaign.md)でのAEMのAdobe Campaign StandardおよびAdobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic)とのリンクを参照してください。[
