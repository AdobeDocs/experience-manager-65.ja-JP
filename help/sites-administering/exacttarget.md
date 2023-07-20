---
title: ExactTarget との統合
description: Adobe Experience Managerを ExactTarget と統合する方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 4183fe78-5055-4b77-8a54-55666e86a04e
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 26%

---

# ExactTarget との統合{#integrating-with-exacttarget}

Adobe Experience Manager(AEM) と ExactTarget の統合により、ExactTarget を使用してAEMで作成した電子メールを管理および送信できます。 また、AEMページ上のAEMフォームを使用して、ExactTarget のリード管理機能を使用することもできます。

この統合によって次の機能を使用できるようになります。

* E メールをAEMで作成し、ExactTarget に公開して配布する機能。
* AEMフォームのアクションを設定して、ExactTarget 購読者を作成する機能。

ExactTarget の設定後、ExactTarget にニュースレターや電子メールを発行できます。 詳しくは、 [電子メールサービスへのニュースレターの公開](/help/sites-authoring/personalization.md).

## ExactTarget 設定の作成 {#creating-an-exacttarget-configuration}

ExactTarget 設定は、クラウドサービスまたはツールを使用して追加できます。 この節では、両方の方法について説明します。

### クラウドサービスを使用した ExactTarget の設定 {#configuring-exacttarget-via-cloudservices}

Cloud Servicesで ExactTarget 設定を作成するには：

1. ようこそページで、 **Cloud Services**. （または `https://<hostname>:<port>/etc/cloudservices.html` で直接アクセスします）。
1. 「**ExactTarget**」、「**設定**」の順にクリックします。ExactTarget 設定ウィンドウが開きます。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. タイトルを入力し、オプションで名前を入力して、「**作成**」をクリックします。**ExactTarget 設定**&#x200B;の設定ウィンドウが開きます。

   ![chlimage_1](assets/chlimage_1.jpeg)

1. ユーザー名、パスワードを入力し、API エンドポイント（例： ）を選択します。 **https://webservice.exacttarget.com/Service.asmx**) をクリックします。
1. クリック **ExactTarget に接続します。** 正常に接続すると、成功ダイアログが表示されます。 box クリック **OK** をクリックしてウィンドウを閉じます。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. アカウントを選択します（使用可能な場合）。 このアカウントは Enterprise 2.0 のお客様向けです。 「**OK**」をクリックします。

   ExactTarget が設定されました。 「**編集**」をクリックして、この設定を編集できます。「**ExactTarget に移動**」をクリックして、ExactTarget に移動できます。

1. AEMにデータ拡張機能が追加されました。 ExactTarget データ拡張列をインポートできます。 ExactTarget 設定が正常に作成された以外に表示される「+」記号をクリックすることで、設定できます。 ドロップダウンリストから既存のデータ拡張を選択できます。 データ拡張機能の設定方法について詳しくは、 [ExactTarget ドキュメント](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_relationships_classic.htm&amp;type=5).

   インポートされたデータ拡張列は、後で **テキストとパーソナライゼーション** コンポーネント。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

### ツールを使用した ExactTarget の設定 {#configuring-exacttarget-via-tools}

ツールで ExactTarget 設定を作成するには：

1. ようこそページで、 **ツール**. または、`https://<hostname>:<port>/misadmin#/etc` に移動して直接そこに移動します。
1. 「**ツール**」、「**クラウドサービス設定**」、「**ExactTarget**」の順に選択します。
1. 「**新規**」をクリックして、ページを作成ウィンドウを開きます。

   ![chlimage_1-34](assets/chlimage_1-3.jpeg)

1. 次を入力します。 **タイトル** オプションで **名前**&#x200B;をクリックし、 **作成**.
1. 前の手順 4 で説明した設定情報を入力します。この手順に従って、ExactTarget の設定を完了します。

### 複数の設定の追加 {#adding-multiple-configurations}

複数の設定を追加するには：

1. ようこそページで、 **Cloud Services** をクリックし、 **ExactTarget**. クリック **設定を表示** 1 つ以上の ExactTarget 設定が使用可能な場合に表示されます。 利用可能なすべての設定が一覧表示されます。
1. 「利用可能な設定」の横にある「**+**」記号をクリックします。これにより、 **設定を作成** ウィンドウ 上記の設定手順に従って、設定を作成します。
