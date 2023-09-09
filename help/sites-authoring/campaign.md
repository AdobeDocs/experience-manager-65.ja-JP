---
title: Adobe Campaign Classic および Adobe Campaign Standard の使用
seo-title: Working with Adobe Campaign 6.1 and Adobe Campaign Standard
description: AEM でメールコンテンツを作成して、Adobe Campaign のメールで処理することができます。
seo-description: You can create email content in AEM and process it in Adobe Campaign emails
uuid: 23195f0b-71c0-4554-8c8b-b0e7704d71d7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 2fd0047d-d0f6-4289-98cf-454486f9cd61
exl-id: d7e4d424-0ca7-449f-95fb-c4fe19dd195d
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2755'
ht-degree: 43%

---

# Adobe Campaign Classic および Adobe Campaign Standard の使用{#working-with-adobe-campaign-classic-and-adobe-campaign-standard}

AEM でメールコンテンツを作成して、Adobe Campaign のメールで処理することができます。これを実行するには、次の手順に従う必要があります。

1. AEM で、Adobe Campaign 固有のテンプレートから新しいニュースレターを作成します。
1. 選択 [Adobe Campaignサービス](#selecting-the-adobe-campaign-cloud-service-and-template) コンテンツを編集してすべての機能にアクセスする前に、
1. コンテンツを編集します。
1. コンテンツを検証します。

その後、Adobe Campaignの配信とコンテンツを同期できます。 詳細な手順については、このドキュメントを参照してください。

関連トピック [AEMでのAdobe Campaign Formsの作成](/help/sites-authoring/adobe-campaign-forms.md).

>[!NOTE]
>
>この機能を使用する前に、AEMを [Adobe Campaign](/help/sites-administering/campaignonpremise.md) または [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## Adobe Campaign経由での電子メールコンテンツの送信 {#sending-email-content-via-adobe-campaign}

AEMとAdobe Campaignを設定した後、E メール配信コンテンツをAEMで直接作成し、Adobe Campaignで処理できます。

Adobe Campaign のコンテンツを AEM 内で作成する場合は、すべての機能にアクセスするために、コンテンツを編集する前に Adobe Campaign サービスにリンクする必要があります。

次の 2 つの場合が考えられます。

* コンテンツは、Adobe Campaignからの配信と同期できます。 これにより、配信でAEMコンテンツを使用できます。
* (Adobe Campaign Classicのみ ) コンテンツをAdobe Campaignに直接送信できます。これにより、新しい E メール配信が自動的に生成されます。 このモードには制限があります。

詳細な手順については、このドキュメントを参照してください。

### 新しいメールコンテンツの作成 {#creating-new-email-content}

>[!NOTE]
>
>メールテンプレートを追加する場合は、テンプレートを使用可能にするために、必ず **/content/campaigns** の下に追加してください。

#### 新しいメールコンテンツの作成 {#creating-new-email-content-1}

1. AEM で、**サイト**／**キャンペーン**&#x200B;を選択し、メールキャンペーンを管理する場所を参照します。次の例では、パスは&#x200B;**サイト**／**Campaigns**／**Geometrixx Outdoors**／**メールキャンペーン** です。

   >[!NOTE]
   >
   >[メールのサンプルは、Geometrixx でのみ使用できます](/help/sites-developing/we-retail.md)。Geometrixx のサンプルコンテンツをパッケージ共有からダウンロードしてください。

   ![chlimage_1-15](assets/chlimage_1-15a.png)

1. 選択 **作成** その後 **ページを作成**.
1. 接続先のAdobe Campaignに固有の使用可能なテンプレートの 1 つを選択し、「 **次へ**. デフォルトでは、次の 3 つのテンプレートを使用できます。

   * **Adobe Campaign Classic メール**：コンテンツを事前定義済みのテンプレート（2 列）に追加してから、配信のために Adobe Campaign Classic に送信できます。
   * **Adobe Campaign Standard メール**：コンテンツを事前定義済みのテンプレート（2 列）に追加してから、配信のために Adobe Campaign Standard に送信できます。

1. 「**タイトル**」に入力し、オプションで「**説明**」に入力して、「**作成**」をクリックします。メールの編集中に上書きしない限り、タイトルはニュースレターまたはメールの件名として使用されます。

### Adobe Campaign Cloud Service とテンプレートの選択 {#selecting-the-adobe-campaign-cloud-service-and-template}

Adobe Campaignと統合するには、ページにAdobe Campaignクラウドサービスを追加する必要があります。 これにより、パーソナライゼーションやその他のAdobe Campaign情報にアクセスできます。

また、Adobe Campaignテンプレートを選択し、件名を変更し、HTMLで E メールを表示しないユーザー向けにプレーンテキストコンテンツを追加する必要が生じる場合もあります。

クラウドサービスは、 **Sites** タブ、または電子メール/ニュースレターを作成した後に、内から。

次からのクラウドサービスの選択： **Sites** 「 」タブを使用することをお勧めします。 電子メール/ニュースレターからクラウドサービスを選択する場合は、回避策が必要です。

次から： **Sites** ページ：

1. AEMで電子メールページを選択し、 **プロパティを表示**.

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. 「**編集**」、「**クラウドサービス**」タブの順に選択し、下までスクロールダウンして「+」記号をクリックし、設定を追加してから、「**Adobe Campaign**」を選択します。

   ![chlimage_1-17](assets/chlimage_1-17a.png)

1. 使用している Adobe Campaign インスタンスに一致する設定をドロップダウンリストから選択し、「**保存**」をクリックして確認します。
1. 「**Adobe Campaign**」タブをクリックすると、メールに適用されるテンプレートを表示できます。別のテンプレートを選択したい場合は、編集時にメール内からテンプレートにアクセスできます。

   デフォルトのメールテンプレート以外の（Adobe Campaign の）特定のメール配信テンプレートを適用したい場合は、「**プロパティ**」で「**Adobe Campaign**」タブを選択します。関連するAdobe Campaignインスタンスで、E メール配信テンプレートの内部名を入力します。

   選択したテンプレートによって、Adobe Campaignで使用できるパーソナライゼーションフィールドが決まります。

   ![chlimage_1-18](assets/chlimage_1-18a.png)

オーサリング時のニュースレター／メール内から選択する場合は、レイアウト上の問題によって、「**ページのプロパティ**」で Adobe Campaign クラウドサービス設定を選択できないことがあります。その場合は、以下に説明する回避策を使用できます。

1. AEMで電子メールページを選択し、 **編集**. 「**プロパティを開く**」をクリックします。

   ![chlimage_1-19](assets/chlimage_1-19a.png)

1. 「**クラウドサービス**」を選択し、「**+**」をクリックして設定を追加します。表示される任意の設定を選択します（どれでもかまいません）。「**+**」記号をクリックまたはタップして、別の設定を追加してから、「**Adobe Campaign**」を選択します。

   >[!NOTE]
   >
   >または、「**サイト**」タブで「**プロパティを表示**」を選択して、クラウドサービスを選択することができます。

1. 使用している Adobe Campaign インスタンスに一致する設定をドロップダウンリストから選択し、最初に作成した、Adobe Campaign 用ではない設定を削除してから、チェックマークをクリックして確認します。
1. 前述の手順のステップ 4 を続行して、テンプレートを選択し、プレーンテキストを追加します。

### E メールコンテンツの編集 {#editing-email-content}

E メールコンテンツを編集するには：

1. 電子メールを開き、デフォルトでは編集モードに入ります。

   ![chlimage_1-20](assets/chlimage_1-20a.png)

1. メールの件名を変更したい場合や、HTML 表示を使用しない受信者用のプレーンテキストを追加したい場合は、「**メール**」を選択し、件名とテキストを追加します。ページアイコンを選択すると、プレーンテキストのバージョンが HTML から自動生成されます。終了したら、チェックマークをクリックします。

   Adobe Campaignのパーソナライゼーションフィールドを使用して、ニュースレターをパーソナライズできます。 パーソナライゼーションフィールドを追加するには、Adobe Campaignのロゴを表示するボタンをクリックして、パーソナライゼーションフィールドピッカーを開きます。 その後、このニュースレターで使用できるすべてのフィールドから選択できます。

   >[!NOTE]
   >
   >エディター内のプロパティのパーソナライゼーションフィールドがグレー表示になっている場合は、設定を再確認してください。

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. 画面左側のコンポーネントパネルを開き、ドロップダウンメニューから「**Adobe Campaign ニュースレター**」を選択して、以下のコンポーネントを探します。

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. コンポーネントをページ上に直接ドラッグし、コンポーネントに応じて編集します。例えば、**テキストおよびパーソナライゼーション（キャンペーン）**&#x200B;コンポーネントをドラッグして、パーソナライズしたテキストを追加することができます。

   ![chlimage_1-23](assets/chlimage_1-23a.png)

   各コンポーネントの詳細については、[Adobe Campaign コンポーネント](/help/sites-authoring/adobe-campaign-components.md)を参照してください。

   ![chlimage_1-24](assets/chlimage_1-24a.png)

### パーソナライゼーションの挿入 {#inserting-personalization}

コンテンツの編集時に、以下を挿入できます。

* Adobe Campaign コンテキストフィールド。これらは、受信者のデータ（姓名、ターゲットディメンションのデータなど）に応じて変化する値をテキスト内に挿入するためのフィールドです。
* Adobe Campaign パーソナライゼーションブロック。ブランドのロゴやミラーページへのリンクなど、受信者のデータに関係なく表示される、事前定義されたコンテンツのブロックです。

詳しくは、 [Adobe Campaign Components](/help/sites-authoring/adobe-campaign-components.md) を参照してください。

>[!NOTE]
>
>* Adobe Campaignのフィールドのみ **プロファイル** ターゲティングディメンションが考慮されます。
>* プロパティを「**サイト**」から表示すると、Adobe Campaign コンテキストフィールドにアクセスできません。これらのフィールドには、編集時にメール内から直接アクセスできます。

パーソナライゼーションを挿入するには：

1. 新しい&#x200B;**ニュースレター**／**テキストおよびパーソナライゼーション （Campaign）**&#x200B;コンポーネントをページ上にドラッグして挿入します。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 鉛筆アイコンをクリックして、コンポーネントを開きます。 インプレースエディターが開きます。

   ![chlimage_1-26](assets/chlimage_1-26a.png)

   >[!NOTE]
   >
   >**Adobe Campaign Standardの場合：**
   >
   >* 使用可能なコンテキストフィールドは、 **プロファイル** Adobe Campaignのターゲティングディメンション。
   >* [Adobe Campaign メールへの AEM ページのリンク](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard)を参照してください。
   >
   >**Adobe Campaign Classic の場合：**
   >
   >* 使用可能なコンテキストフィールドは、Adobe Campaign の **nms:seedMember** スキーマから動的に復元されます。ターゲット拡張データは、コンテンツと同期される配信を含むワークフローから動的に復元されます。（[AEM で作成されたコンテンツと Adobe Campaign の配信の同期](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)の節を参照してください）。
   >
   >* パーソナライゼーション要素を追加または非表示にするには、[パーソナライゼーションフィールドおよびブロックの管理](/help/sites-administering/campaignonpremise.md#managing-personalization-fields-and-blocks)を参照してください。
   >* **重要**：すべてのシードテーブルフィールドは、受信者テーブル（または対応する連絡先テーブル）にも存在する必要があります。

1. 入力してテキストを挿入します。 Adobe Campaignコンポーネントをクリックして選択し、コンテキストフィールドまたはパーソナライゼーションブロックを挿入します。 終了したら、チェックマークを選択します。

   ![chlimage_1-27](assets/chlimage_1-27a.png)

   コンテキストフィールドまたはパーソナライゼーションブロックを挿入したら、ニュースレターをプレビューして、フィールドをテストできます。[ニュースレターのプレビュー](#previewing-a-newsletter)を参照してください。

### ニュースレターのプレビュー {#previewing-a-newsletter}

ニュースレターの外観やパーソナライゼーションのプレビューを確認できます。

1. ニュースレターを開いた状態で、AEM の右上隅の「**プレビュー**」をクリックします。ユーザーが受信したときにニュースレターがどのように見えるかが表示されます。

   ![chlimage_1-28](assets/chlimage_1-28a.png)

   >[!NOTE]
   >
   >Adobe Campaign Standardを使用していて、サンプルテンプレートを使用している場合、初期コンテンツを表示する 2 つのパーソナライゼーションブロック — **&quot;&lt;%@ include view=&quot;MirrorPage&quot; %>&quot;** および **&quot;&lt;%@ include view=&quot;UnsubscriptionLink&quot; %>&quot;**  — 配信中にコンテンツをインポートする際にエラーが発生します。 パーソナライゼーションブロックピッカーを使用して、対応するブロックを選択することで、これらを調整できます。

1. パーソナライゼーションをプレビューするには、ツールバーの対応するアイコンをクリックまたはタップして ContextHub を開きます。 パーソナライゼーションフィールドのタグが、選択したペルソナのシードデータに置き換えられるようになりました。 ContextHub でペルソナを切り替える際の変数の適応方法を確認します。

   ![chlimage_1-29](assets/chlimage_1-29a.png)

1. 現在選択されているペルソナに関連付けられている、Adobe Campaignからのシードデータを表示できます。 これをおこなうには、ContextHub バーでAdobe Campaignモジュールをクリックまたはタップします。 現在のプロファイルのすべてのシードデータが表示されるダイアログボックスが開きます。 再度別のペルソナに切り替えると、データが変化します。

   ![chlimage_1-30](assets/chlimage_1-30a.png)

### AEMでのコンテンツの承認 {#approving-content-in-aem}

コンテンツの作成が完了したら、承認プロセスを開始できます。 ツールボックスの「**ワークフロー**」タブに移動して、「**Adobe Campaign 用に承認**」ワークフローを選択します。

そのまま使用できるこのワークフローには、リビジョンと承認、またはリビジョンと却下の 2 つのステップがあります。 ただし、このワークフローは、より複雑なプロセスに拡張し、適応させることができます。

![chlimage_1-31](assets/chlimage_1-31a.png)

Adobe Campaign 用にコンテンツを承認するには、「**ワークフロー**」を選択し、「**Adobe Campaign 用に承認**」を選択することでワークフローを適用し、「**ワークフローを開始**」をクリックします。ステップを実行して、コンテンツを承認します。ワークフローの最後のステップで、「**承認**」の代わりに「**拒否**」を選択して、コンテンツを拒否することもできます。

![chlimage_1-32](assets/chlimage_1-32a.png)

コンテンツが承認されると、Adobe Campaignに承認済みと表示されます。 その後、E メールを送信できます。

ADOBE CAMPAIGN STANDARD:

![chlimage_1-33](assets/chlimage_1-33a.png)

Adobe Campaign Classic の場合：

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
>
未承認のコンテンツは、Adobe Campaignの配信と同期できますが、配信を実行できません。 承認済みコンテンツのみキャンペーン配信経由で送信できます。

## AEMとAdobe Campaign StandardおよびAdobe Campaign Classicとのリンク {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic}

AEMとAdobe Campaignのリンクや同期の方法は、サブスクリプションベースのAdobe Campaign Standardを使用しているか、オンプレミスベースのAdobe Campaign Classicを使用しているかによって異なります。

使用している Adobe Campaign ソリューションに応じた手順は、以下の節を参照してください。

* [Adobe Campaign メールへの AEM ページのリンク（Adobe Campaign Standard）](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard)
* [AEM で作成されたコンテンツと Adobe Campaign Classic の配信の同期](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)

### AEMページとAdobe Campaign E メールのリンク (Adobe Campaign Standard) {#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard}

Adobe Campaign Standardを使用すると、AEMで作成したコンテンツを復元し、次の情報とリンクできます。

* 電子メール。
* 電子メールテンプレート。

これにより、コンテンツを配信できます。 ニュースレターが単一の配信にリンクされているかどうかは、ページに表示されるコードで確認できます。

![chlimage_1-35](assets/chlimage_1-35a.png)

>[!NOTE]
>
ニュースレターが複数の配信にリンクされている場合は、リンクされている配信の数が表示されます（ただし、すべての ID が表示されるわけではありません）。

AEM で作成されたページと Adobe Campaign のメールをリンクするには：

1. AEM 固有のメールテンプレートをベースに新しいメールを作成します。詳しくは、[Adobe Campaign Standard でのメールの作成](https://helpx.adobe.com/jp/campaign/standard/channels/using/creating-an-email.html)を参照してください。

   ![chlimage_1-36](assets/chlimage_1-36a.png)

1. 配信ダッシュボードから&#x200B;**コンテンツ**&#x200B;ブロックを開きます。

   ![chlimage_1-37](assets/chlimage_1-37a.png)

1. ツールバーで「**Adobe Experience Manager コンテンツとリンク**」を選択し、AEM で使用可能なコンテンツのリストにアクセスします。

   >[!NOTE]
   >
   アクションバーに「**Adobe Experience Manager コンテンツとリンク**」オプションが表示されない場合は、メールのプロパティで「**コンテンツ編集モード**」が「**Adobe Experience Manager**」に正しく設定されていることを確認してください。

   ![chlimage_1-38](assets/chlimage_1-38a.png)

1. E メールで使用するコンテンツを選択します。

   このリストでは、次の内容を指定します。

   * AEMのコンテンツのラベル。
   * AEMのコンテンツの承認ステータス。 コンテンツが承認されていない場合は、コンテンツを同期できますが、配信が送信される前に承認が必要になります。 ただし、配達確認の送信やプレビューテストなど、特定の操作を実行することもできます。
   * コンテンツが最後に変更された日付。
   * 既に配信にリンクされているすべてのコンテンツ。

   >[!NOTE]
   >
   デフォルトでは、配信と既に同期されているコンテンツは非表示になります。 ただし、表示して使用することはできます。 例えば、コンテンツを複数の配信のテンプレートとして使用する場合などです。

   E メールがAEMコンテンツにリンクされている場合、Adobe Campaignでコンテンツを編集することはできません。

1. 電子メールのその他のパラメーターをダッシュボードから指定します（オーディエンス、実行スケジュール）。
1. E メール配信を実行します。 配信分析時に、AEMコンテンツの最新バージョンが取得されます。

   >[!NOTE]
   >
   E メールにリンクされている間にAEMでコンテンツが更新された場合、分析中にAdobe Campaignでコンテンツが自動的に更新されます。 コンテンツアクションバーの「**Adobe Experience Manager コンテンツを更新**」を使用して、同期を手動で実行することもできます。
   >
   E メールとAEMコンテンツ間のリンクは、 **Adobe Experience Managerコンテンツとのリンクを削除** コンテンツアクションバーから。 このボタンは、コンテンツが既に配信にリンクされている場合にのみ使用できます。 別のコンテンツを配信にリンクするには、新しいリンクを確立する前に、現在のコンテンツのリンクを削除する必要があります。
   >
   リンクが削除されると、ローカルコンテンツは保持され、Adobe Campaignで編集可能になります。 コンテンツを変更した後に再びリンクすると、すべての変更内容が失われます。

### AEMで作成されたコンテンツとAdobe Campaign Classicからの配信との同期 {#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic}

Adobe Campaignを使用すると、AEMで作成されたコンテンツを次のものと復元して同期できます。

* キャンペーン配信
* キャンペーンワークフローの配信アクティビティ
* 繰り返し配信
* 連続配信
* Message Center の配信
* 配信テンプレート

AEMでは、ニュースレターが単一の配信にリンクされている場合、配信コードがページに表示されます。

![chlimage_1-39](assets/chlimage_1-39a.png)

>[!NOTE]
>
ニュースレターが複数の配信にリンクされている場合は、リンクされている配信の数が表示されます（すべての ID が表示されるわけではありません）。
>
[!NOTE]
>
ワークフローステップ **Adobe Campaignに公開** はAEM 6.1 で非推奨（廃止予定）となりました。この手順は、Adobe CampaignとのAEM 6.0 統合の一部で、不要になりました。

AEMで作成したコンテンツをAdobe Campaignからの配信と同期するには：

1. 「**AEM コンテンツでメール配信（mailAEMContent）**」配信テンプレートを選択して、配信を作成または配信アクティビティをキャンペーンワークフローに追加します。

   ![chlimage_1-40](assets/chlimage_1-40a.png)

1. ツールバーで「**同期**」を選択して、AEM で使用可能なコンテンツのリストにアクセスします。

   >[!NOTE]
   >
   「**同期**」オプションが配信のツールバーに表示されない場合は、**プロパティ**／**詳細**&#x200B;を選択して、**AEM** で「**コンテンツ編集モード**」フィールドが正しく設定されていることを確認してください。

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 配信と同期するコンテンツを選択します。

   このリストでは、次の内容を指定します。

   * AEMのコンテンツのラベル。
   * AEMのコンテンツの承認ステータス。 コンテンツが承認されていない場合は、コンテンツを同期できますが、配信が送信される前に承認が必要になります。 ただし、BAT の送信やプレビューテストなど、特定の操作を実行することができます。
   * コンテンツが最後に変更された日付。
   * 既に配信にリンクされているすべてのコンテンツ。

   >[!NOTE]
   >
   デフォルトでは、配信と既に同期されているコンテンツは非表示になります。 ただし、表示して使用することはできます。 例えば、コンテンツを複数の配信のテンプレートとして使用する場合などです。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 配信の他のパラメーター（ターゲットなど）を
1. 必要に応じて、Adobe Campaignで配信の承認プロセスを開始します。 Adobe Campaignで設定された承認（予算、ターゲットなど）に加えて、AEMでのコンテンツの承認が必要です。 Adobe Campaignでのコンテンツの承認は、コンテンツがAEMで既に承認されている場合にのみ可能です。
1. 配信を実行します。 配信分析中に、AEMコンテンツの最新バージョンが復元されます。

   >[!NOTE]
   >
   * 配信とコンテンツを同期すると、Adobe Campaignの配信コンテンツは読み取り専用になります。 E メールの件名とコンテンツは変更できなくなりました。
   * Adobe Campaignの配信にリンクされている間にAEMでコンテンツが更新された場合、配信の分析中に配信内でコンテンツが自動的に更新されます。 「**今すぐコンテンツを更新**」ボタンを使用して、同期を手動で実行することもできます。
   * 「**同期解除**」ボタンを使用して、配信と AEM コンテンツの同期をキャンセルできます。これは、コンテンツが既に配信と同期されている場合にのみ使用できます。 別のコンテンツを配信と同期するには、新しいリンクを確立する前に現在のコンテンツの同期をキャンセルする必要があります。
   * 同期が解除されると、ローカルコンテンツは保持され、Adobe Campaignで編集可能になります。 コンテンツを変更した後に再同期すると、すべての変更内容が失われます。
   * 繰り返し配信および連続配信の場合、配信が実行されるたびにAEMコンテンツとの同期が停止されます。
