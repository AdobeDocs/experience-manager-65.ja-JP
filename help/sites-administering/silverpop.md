---
title: Silverpop Engage との統合
seo-title: Integrating with Silverpop Engage
description: Adobe Experience Managerを Silverpop Engage と統合する方法を説明します。
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 95%

---

# Silverpop Engage との統合{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. You must download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

AEM を Silverpop Engage と統合すると、AEM で作成したメールを Silverpop を使用して管理および送信できます。また、AEMページ上のAEM forms を使用して、Silverpop のリード管理機能を使用することもできます。

この統合によって次の機能を使用できるようになります。

* AEM でメールを作成し、Silverpop に公開して配信する機能。
* AEM フォームのアクションを設定して、Silverpop サブスクライバーを作成する機能。

Silverpop Engage が設定されると、Silverpop Engage にニュースレターまたはメールを発行できます。

## Silverpop 設定の作成 {#creating-a-silverpop-configuration}

Silverpop 設定は、**クラウドサービス**、**ツール**、**API エンドポイント**&#x200B;のいずれかの方法で追加できます。このセクションでは、すべての方法について説明します。

### Cloud Services を使用した Silverpop の設定 {#configuring-silverpop-via-cloudservices}

Cloud Services で Silverpop 設定の作成するには：

1. AEM で、**ツール**／**デプロイメント**／**クラウドサービス**&#x200B;をタップまたはクリックします。（または `https://<hostname>:<port>/etc/cloudservices.html` に直接アクセスします。）
1. サードパーティのサービスで、「**Silverpop Engage**」、「**設定**」の順にクリックします。Silverpop 設定ウィンドウが開きます。

   >[!NOTE]
   >
   >Silverpop Engage のパッケージをパッケージ共有からダウンロードしない限り、Silverpop Engage をサードパーティのサービスのオプションとして使用できません。

1. タイトルを入力し、オプションで名前を入力して、「**作成**」をクリックします。Silverpop 設定ウィンドウが開きます。
1. ユーザー名、パスワードを入力し、API エンドポイントをドロップダウンリストから選択します。
1. 「**Silverpop に接続」をクリックします。** 接続に成功したら、成功ダイアログボックスが表示されます。「**OK**」をクリックしてウィンドウを閉じます。「**Silverpop Engage に移動**」をクリックすることで、Silverpop に移動できます。
1. Silverpop が設定されました。「**編集**」をクリックして、この設定を編集できます。
1. また、Silverpop Engage フレームワークは、タイトルと名前（オプション）を提供することで、パーソナライズされたアクション用に設定できます。「作成」をクリックすると、既に設定済みの Silverpop 接続用のフレームワークが正常に作成されます。

   読み込まれたデータ拡張列は、後で AEM コンポーネントの「**テキストおよびパーソナライゼーション**」で使用できます。

### ツールを使用した Silverpop の設定 {#configuring-silverpop-via-tools}

ツールで Silverpop 設定を作成するには：

1. AEM で、**ツール**／**デプロイメント**／**クラウドサービス**&#x200B;をタップまたはクリックします。または、`https://<hostname>:<port>/misadmin#/etc` にアクセスして直接移動します。
1. **ツール**／**クラウドサービス設定**／**Silverpop Engage** を選択します。
1. 「**新規**」をクリックします。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. **ページの作成**&#x200B;ウィンドウで、**タイトル**&#x200B;と必要に応じて&#x200B;**名前**&#x200B;を入力し、「**作成**」をクリックします。
1. 前の手順 4 で説明した設定情報を入力します。Silverpop の設定を完了するには、次の手順に従います。

### 複数の設定の追加 {#adding-multiple-configurations}

複数の設定を追加するには：

1. ようこそページで「**クラウドサービス**」をクリックし、「**Silverpop Engage**」をクリックします。「**設定を表示**」ボタンをクリックします。このボタンは、利用可能な Silverpop 設定がある場合に表示されます。利用可能なすべての設定が一覧表示されます。
1. 「利用可能な設定」の横にある「**+**」記号をクリックします。**設定を作成**&#x200B;ウィンドウが開きます。前述の設定手順に従って新しい設定を作成します。

### Silverpop に接続するための API エンドポイントの設定 {#configuring-api-end-points-for-connecting-to-silverpop}

現在、AEM には 6 つの保護されていないエンドポイント（Engage 1 ～ 6）があります。Silverpop は、2 つの新しいエンドポイントと、既存のもの用に変更した接続エンドポイントを提供します。

API エンドポイントを設定するには：

1. `https://<hostname>:<port>/crxde.` で `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` に移動します。
1. 右クリックして、**Create**／**Create Node**&#x200B;を選択します。
1. 「**名前**」に「`sp-e0`」と入力して、「**タイプ**」で「`cq:Widget`」を選択します。
1. 新しく追加したノードに 2 つのプロパティを追加します。

   1. **名前**：`text`、**タイプ**：`String`、**値**：`Engage 0`
   1. **名前**：`value`、**タイプ**：`String`、**値**：`https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   「すべて保存」をクリックします。

1. 「**名前**」に「`sp-e7`」と入力し、「**タイプ**」で「`cq:Widget` 」を選択して、もう 1 つのノードを作成します。

   新しく追加したノードに 2 つのプロパティを追加します。

   1. **名前**：`text`、**タイプ**：`String`、**値**：`Pilot`
   1. **名前**：`value`、**タイプ**：`String`、**値**：`https://apipilot.silverpop.com/XMLAPI`

1. 既存の API エンドポイント（Engage 1～6）を変更するには、それぞれを 1 つずつクリックして、値を次のように置き換えます。

   | **ノード名** | **既存のエンドポイント値** | **新しいエンドポイント値** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. 「**すべて保存**」をクリックします。これで、AEM は、保護されたエンドポイントで Silverpop と接続する準備ができました。

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
