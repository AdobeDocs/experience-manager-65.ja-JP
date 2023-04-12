---
title: Silverpop Engage との統合
seo-title: Integrating with Silverpop Engage
description: AEMを Silverpop Engage と統合する方法を説明します
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: e17deeb6-5339-4ead-9086-cbe2167cdec6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 01029a80-f80e-450c-9c73-16d0662af26d
docset: aem65
exl-id: 6c4b8aaa-bda0-4066-a3fc-d91a5ab1621c
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 39%

---

# Silverpop Engage との統合{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. You must download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

AEM を Silverpop Engage と統合すると、AEM で作成したメールを Silverpop を使用して管理および送信できます。また、AEM ページ上の AEM フォームを使用して、Silverpop のリード管理機能を使用できます。

統合により、次の機能を利用できます。

* 電子メールをAEMで作成し、配布用に Silverpop に公開する機能。
* AEMフォームのアクションを設定して Silverpop 購読者を作成する機能。

Silverpop Engage が設定されると、Silverpop Engage にニュースレターまたはメールを発行できます。

## Silverpop 設定の作成 {#creating-a-silverpop-configuration}

Silverpop 設定は、 **Cloud Services**, **ツール**&#x200B;または **API エンドポイント**. この節では、すべてのメソッドについて説明します。

### 「Cloud Services」を使用した Silverpop の設定 {#configuring-silverpop-via-cloudservices}

Cloud Servicesで Silverpop 設定を作成するには：

1. AEM で、**ツール**／**デプロイメント**／**クラウドサービス**&#x200B;をタップまたはクリックします。（または `https://<hostname>:<port>/etc/cloudservices.html` に直接アクセスします。）
1. サードパーティのサービスで、「**Silverpop Engage**」、「**設定**」の順にクリックします。Silverpop 設定ウィンドウが開きます。

   >[!NOTE]
   >
   >Silverpop Engage は、パッケージ共有からパッケージをダウンロードしない限り、サードパーティのサービスのオプションとして使用できません。

1. タイトルを入力し、オプションで名前を入力して、「**作成**」をクリックします。Silverpop 設定ウィンドウが開きます。
1. ユーザー名とパスワードを入力し、ドロップダウンリストから API エンドポイントを選択します。
1. クリック **Silverpop に接続します。** 正常に接続すると、成功ダイアログボックスが表示されます。 クリック **OK** 窓を閉めて 「**Silverpop Engage に移動**」をクリックすることで、Silverpop に移動できます。
1. Silverpop が設定されました。「**編集**」をクリックして、この設定を編集できます。
1. また、Silverpop Engage フレームワークは、タイトルと名前（オプション）を指定することで、パーソナライズされたアクション用に設定できます。 「作成」をクリックすると、既に設定済みの Silverpop 接続用のフレームワークが正常に作成されます。

   読み込まれたデータ拡張列は、後でAEMコンポーネントで使用できます。 **テキストとパーソナライゼーション**.

### ツールを使用した Silverpop の設定 {#configuring-silverpop-via-tools}

ツールで Silverpop 設定を作成するには：

1. AEM で、**ツール**／**デプロイメント**／**クラウドサービス**&#x200B;をタップまたはクリックします。または、`https://<hostname>:<port>/misadmin#/etc` にアクセスして直接移動します。
1. **ツール**／**クラウドサービス設定**／**Silverpop Engage** を選択します。
1. 「**新規**」をクリックします。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. 内 **ページを作成** ウィンドウで、 **タイトル** オプションで **名前**&#x200B;をクリックし、 **作成**.
1. 前の手順 4 で説明した設定情報を入力します。 Silverpop の設定を完了するには、次の手順に従います。

### 複数の設定の追加 {#adding-multiple-configurations}

複数の設定を追加するには：

1. ようこそページで、 **Cloud Services** をクリックし、 **Silverpop Engage**. クリック **設定を表示** ボタンが表示されます。 使用可能なすべての設定が表示されます。
1. 次をクリック： **+** [ 利用可能な設定 ] の横に記号を付けます。 すると、 **設定を作成** ウィンドウ 前の設定手順に従って、設定を作成できます。

### Silverpop に接続するための API エンドポイントの設定 {#configuring-api-end-points-for-connecting-to-silverpop}

現在、AEMには、セキュリティで保護されていないエンドポイントが 6 つあります（エンゲージ 1 ～ 6）。 Silverpop で、既存のエンドポイントに対して、2 つの新しいエンドポイントと変更された接続エンドポイントが提供されるようになりました。

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

1. 既存の API エンドポイント（エンゲージメント 1～6）を変更するには、それぞれを 1 つずつクリックし、値を次のように置き換えます。

   | **ノード名** | **既存のエンドポイント値** | **新しいエンドポイント値** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. 「**すべて保存**」をクリックします。AEMは、セキュアなエンドポイントで Silverpop に接続する準備が整いました。

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
