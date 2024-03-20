---
title: Adobe Campaign 6.1 および Adobe Campaign Standard の使用
description: AEM でメールコンテンツを作成して、Adobe Campaign のメールで処理することができます。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 100%

---

# Adobe Campaign 6.1 および Adobe Campaign Standard の使用 {#working-with-adobe-campaign-and-adobe-campaign-standard}

AEM でメールコンテンツを作成して、Adobe Campaign のメールで処理することができます。これを実行するには、次の手順に従う必要があります。

1. AEM で、Adobe Campaign 固有のテンプレートからニュースレターを作成します。
1. すべての機能にアクセスするには、コンテンツを編集する前に [Adobe Campaign サービス](#selectingtheadobecampaigncloudservice)を選択します。
1. コンテンツを編集します。
1. コンテンツを検証します。

これで、コンテンツを Adobe Campaign での配信と同期できるようになります。詳細な手順については、このドキュメントを参照してください。

>[!NOTE]
>
>この機能を使用するには、AEM を [Adobe Campaign](/help/sites-administering/campaignonpremise.md) または [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) と統合するよう設定する必要があります。

## Adobe Campaign を使用したメールコンテンツの送信 {#sending-email-content-via-adobe-campaign}

AEM と Adobe Campaign を設定すると、メール配信コンテンツを AEM 内で直接作成し、作成したコンテンツを Adobe Campaign 内で処理できます。

Adobe Campaign のコンテンツを AEM 内で作成する場合は、すべての機能にアクセスするために、コンテンツを編集する前に Adobe Campaign サービスにリンクする必要があります。

次の 2 つの場合が考えられます。

* コンテンツを Adobe Campaign からの配信と同期する場合。この場合は、AEM コンテンツを配信に使用できます。
* （オンプレミスの Adobe Campaign のみ）コンテンツを Adobe Campaign に直接送信する場合。この場合は、Adobe Campaign が新しいメール配信を自動的に生成します。このモードには制限があります。

詳細な手順については、このドキュメントを参照してください。

### 新しいメールコンテンツの作成 {#creating-new-email-content}

>[!NOTE]
>
>メールテンプレートを追加する場合は、テンプレートを使用可能にするために、必ず **/content/campaigns** の下に追加してください。
>

1. AEM で、**Websites** フォルダーを選択してから、エクスプローラーを参照して、メールキャンペーンを管理している場所を探します。次の例では、関係するノードは **Web サイト**／**Campaigns**／**Geometrixx Outdoors**／**メールキャンペーン**&#x200B;です。

   >[!NOTE]
   >
   >[メールのサンプルは、Geometrixx でのみ使用できます](/help/sites-developing/we-retail.md#weretail)。Geometrixx のサンプルコンテンツをパッケージ共有からダウンロードしてください。

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. **新規**／**新しいページ**&#x200B;を選択して、新しいメールコンテンツを作成します。
1. Adobe Campaign 固有の使用可能なテンプレートのいずれかを選択し、ページの一般的なプロパティを入力します。デフォルトでは、次の 3 つのテンプレートが使用可能です。

   * **Adobe Campaign メール（AC 6.1）**：コンテンツを定義済みのテンプレートに追加してから、配信のために Adobe Campaign 6.1 に送信します。
   * **Adobe Campaign メール（ACS）**：コンテンツを定義済みのテンプレートに追加してから、配信のために Adobe Campaign Standard に送信します。

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. 「**作成**」をクリックして、メールまたはニュースレターを作成します。

### Adobe Campaign Cloud Service およびテンプレートの選択 {#selecting-the-adobe-campaign-cloud-service-and-template}

Adobe Campaign と統合するには、Adobe Campaign Cloud Service をページに追加する必要があります。これにより、パーソナライズ機能や他の Adobe Campaign 情報にアクセスできるようになります。

さらに、Adobe Campaign テンプレートを選択し、件名を変更したり、HTML 表示を使用しない受信者向けにプレーンテキストのコンテンツを追加したりする必要がある場合もあります。

1. サイドキックで「**ページ**」タブを選択し、「**ページのプロパティ**」を選択します。
1. ポップアップウィンドウの「**クラウドサービス**」タブで、「**サービスを追加**」を選択して Adobe Campaign サービスを追加し、「**OK**」をクリックします。

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. 使用している Adobe Campaign インスタンスに一致する設定をドロップダウンリストから選択し、「**OK**」をクリックします。

   >[!NOTE]
   >
   >クラウドサービスを追加した後、必ず「**OK**」または「**適用**」をクリックしてください。そうすると、「**Adobe Campaign**」タブが正しく機能するようになります。

1. デフォルトの&#x200B;**メール**&#x200B;テンプレート以外の、（Adobe Campaign の）特定のメール配信テンプレートを適用したい場合は、「**ページのプロパティ**」を再度選択します。「**Adobe Campaign**」タブで、関連する Adobe Campaign インスタンス内でのメール配信テンプレートの内部名を入力します。

   Adobe Campaign Standard では、このテンプレートは「**AEM コンテンツで配信**」です。Adobe Campaign 6.1 では、このテンプレートは「**AEM コンテンツでメール配信**」です。

   このテンプレートを選択すると、**Adobe Campaign ニュースレター**&#x200B;コンポーネントが自動的に有効になります。

### メールコンテンツの編集 {#editing-email-content}

クラシック UI またはタッチ操作向け UI のどちらでも、メールコンテンツを編集できます。

1. ツールボックスから&#x200B;**ページのプロパティ**／**メール**&#x200B;を選択して、メールの件名とテキストバージョンを入力します。

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. サイドキックから要素を適宜追加して、メールコンテンツを編集します。要素を追加するには、ドラッグ＆ドロップします。その後、編集する要素をダブルクリックします。

   例えば、パーソナライゼーションフィールドを含むテキストを追加できます。

   ![chlimage_1-176](assets/chlimage_1-176.png)

   Adobe Campaign のニュースレターまたはメールキャンペーンに使用できるコンポーネントの説明については、[Adobe Campaign コンポーネント](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)を参照してください。

   ![chlimage_1-177](assets/chlimage_1-177.png)

### パーソナライゼーションの挿入 {#inserting-personalization}

コンテンツを編集する際に、以下を挿入できます。

* Adobe Campaign コンテキストフィールド。これらは、受信者のデータ（姓名、ターゲットディメンションのデータなど）に応じて変化する値をテキスト内に挿入するためのフィールドです。
* Adobe Campaign パーソナライゼーションブロック。ブランドのロゴやミラーページへのリンクなど、受信者のデータに関係なく表示される、事前定義されたコンテンツのブロックです。

Campaign コンポーネントについて詳しくは、[Adobe Campaign コンポーネント](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)を参照してください。

>[!NOTE]
>
>* Adobe Campaign の「**プロファイル**」ターゲティングディメンションのフィールドのみが考慮されます。
>* プロパティを「**サイト**」から表示すると、Adobe Campaign コンテキストフィールドにアクセスできません。これらのフィールドには編集時にメール内から直接アクセスできます。
>

1. 新しい&#x200B;**ニュースレター**／**テキストおよびパーソナライゼーション（キャンペーン）**&#x200B;コンポーネントを挿入します。
1. コンポーネントをダブルクリックして開きます。**編集**&#x200B;ウィンドウには、パーソナライゼーション要素を挿入できる機能があります。

   >[!NOTE]
   >
   >使用可能なコンテキストフィールドは、Adobe Campaign の「**プロファイル**」ターゲティングディメンションに対応しています。
   >
   >[Adobe Campaign メールへの AEM ページのリンク](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail)を参照してください。

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. ペルソナプロファイルのデータを使用してパーソナライゼーションフィールドをテストするには、サイドキックで「**ClientContext**」を選択します。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. ウィンドウが表示され、適切なペルソナを選択できます。パーソナライゼーションフィールドの値は、選択したプロファイルのデータで自動的に置き換えられます。

   ![chlimage_1-180](assets/chlimage_1-180.png)

### ニュースレターのプレビュー {#previewing-a-newsletter}

ニュースレターがどのように表示されるかをプレビューでき、パーソナライゼーションをプレビューできます。

1. プレビューするニュースレターを開き、プレビュー（虫眼鏡）アイコンをクリックすると、サイドキックが小さく折りたたまれます。
1. メールクライアントのアイコンをクリックすると、各メールクライアントでニュースレターがどのように表示されるかを確認できます。

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. 編集を再開するには、サイドキックを展開します。

### AEM でのコンテンツの承認 {#approving-content-in-aem}

コンテンツの作成が完了したら、承認プロセスを開始できます。ツールボックスの「**ワークフロー**」タブに移動して、「**Adobe Campaign 用に承認**」ワークフローを選択します。

この標準のワークフローには、改訂して承認または改訂して拒否という 2 つのステップがあります。ただし、このワークフローは拡張して、より複雑なプロセスに適合させることができます。

![chlimage_1-182](assets/chlimage_1-182.png)

Adobe Campaign 用にコンテンツを承認するには、サイドキックで「**ワークフロー**」を選択し、「**Adobe Campaign 用に承認**」を選択し、「**ワークフローを開始**」をクリックします。ステップを実行して、コンテンツを承認します。ワークフローの最後のステップで、「**承認**」の代わりに「**拒否**」を選択して、コンテンツを拒否することもできます。

![chlimage_1-183](assets/chlimage_1-183.png)

コンテンツが承認されると、承認済みとして Adobe Campaign に表示されます。これで、メールを送信できるようになります。

Adobe Campaign Standard の場合：

![chlimage_1-184](assets/chlimage_1-184.png)

Adobe Campaign 6.1 の場合：

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>未承認のコンテンツは、Adobe Campaign の配信と同期できますが、配信を実行することはできません。Adobe Campaign の配信を使用して送信できるのは、承認済みのコンテンツだけです。

## AEM と Adobe Campaign Standard および Adobe Campaign 6.1 のリンク {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>詳しくは、標準のオーサリングドキュメントの [Adobe Campaign 6.1 および Adobe Campaign Standard の使用](/help/sites-authoring/campaign.md)にある [AEM と Adobe Campaign Standard および Adobe Campaign 6.1 のリンク](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic)を参照してください。
