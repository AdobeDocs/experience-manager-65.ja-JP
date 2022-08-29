---
title: Adobe Campaign Classic との統合
seo-title: Integrating with Adobe Campaign Classic
description: AEM と Adobe Campaign Classic の統合方法について説明します。
seo-description: Learn how to integrate AEM with Adobe Campaign Classic
uuid: 3c998b0e-a885-4aa9-b2a4-81b86f9327d3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: df94dd1b-1b65-478b-a28d-81807a8084b1
exl-id: a7281ca0-461f-4762-a631-6bb539596200
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 100%

---

# Adobe Campaign Classic との統合{#integrating-with-adobe-campaign-classic}

>[!NOTE]
>
>このドキュメントでは、AEM をオンプレミスソリューションの Adobe Campaign Classic と統合する方法について説明します。Adobe Campaign Standard を使用している場合の指示については、[Adobe Campaign Standard との統合](/help/sites-administering/campaignstandard.md)を参照してください。

Adobe Campaign を使用すると、電子メール配信コンテンツおよびフォームを Adobe Experience Manager で直接管理できます。

両方のソリューションを同時に使用するには、最初に互いに接続するように設定する必要があります。これには、Adobe Campaign と Adobe Experience Manager の両方での設定手順が含まれます。これらの手順は、このドキュメントで詳しく説明します。

AEM での Adobe Campaign の操作には、Adobe Campaign を使用して電子メールを送信する機能が含まれています。これについては [Adobe Campaign の操作](/help/sites-authoring/campaign.md)で説明します。また、AEM ページのフォームを使用したデータの操作も含まれます。

さらに、AEM を [Adobe Campaign](https://helpx.adobe.com/jp/support/campaign/classic.html) と統合する際に参考となるトピックを次に示します。

* [電子メールテンプレートのベストプラクティス](/help/sites-administering/best-practices-for-email-templates.md)
* [Adobe Campaign 統合に関するトラブルシューティング](/help/sites-administering/troubleshooting-campaignintegration.md)

Adobe Campaign との統合を拡張する場合は、次のページが参考になります。

* [カスタム拡張の作成](/help/sites-developing/extending-campaign-extensions.md)
* [カスタムフォームマッピングの作成](/help/sites-developing/extending-campaign-form-mapping.md)

## AEM と Adobe Campaign の統合ワークフロー {#aem-and-adobe-campaign-integration-workflow}

ここでは、キャンペーンを作成し、コンテンツを配信する際の AEM と Adobe Campaign の間の一般的なワークフローについて説明します。

一般的なワークフローには、次が含まれます。詳細について説明します。

1. （Adobe Campaign と AEM で）キャンペーンの構築を開始します。
1. コンテンツをリンクして配信する前に、AEM でコンテンツをパーソナライズして、Adobe Campaign で配信を作成します。
1. Adobe Campaign で、コンテンツをリンクして配信します。

### キャンペーンの作成の開始 {#start-building-your-campaign}

キャンペーンの作成は、いつでも開始できます。コンテンツをリンクする前は、AEM と AC は独立しています。つまり、マーケティング担当者は、キャンペーンの作成およびターゲティングを Adobe Campaign で開始でき、同時にコンテンツ作成者は、AEM でデザインに取り組むことができます。

### コンテンツのリンクおよび配信の前に {#before-linking-content-and-delivery}

コンテンツをリンクして配信メカニズムを作成する前に、次の手順を実行する必要があります。

**AEM で**

* **テキストおよびパーソナライゼーション**&#x200B;コンポーネントのパーソナライゼーションフィールドを使用してパーソナライズする

**Adobe Campaign の場合：**

* **aemContent** タイプの配信を作成する

### コンテンツのリンクと配信の設定 {#linking-content-and-setting-delivery}

リンクおよび配信用のコンテンツを用意したら、コンテンツのリンク方法とリンク先を決めます。

これらのすべての手順は、Adobe Campaign で完了します。

1. どの AEM インスタンスを使用するかを指定します。
1. 「同期」ボタンをクリックして、コンテンツを同期します。
1. コンテンツピッカーを開いて、コンテンツを選択します。

### AEM を初めて使用する場合 {#if-you-are-new-to-aem}

AEM を初めて使用する場合は、AEM を理解するのに次のリンクが参考になります。

* [AEM の開始](/help/sites-deploying/deploy.md)
* [レプリケーションエージェントの概要](/help/sites-deploying/replication.md)
* [ログファイルの検索と使用](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)
* [AEM プラットフォームの概要](/help/sites-deploying/platform.md)

## Adobe Campaign の設定 {#configuring-adobe-campaign}

Adobe Campaign の設定には、次が含まれます。

1. AEM 統合パッケージの Adobe Campaign へのインストール。
1. 外部アカウントの設定。
1. AEMResourceTypeFilter が正しく設定されていることの検証。

さらに、ユーザーが設定可能な次のような高度な設定があります。

* コンテンツブロックの管理
* パーソナライゼーションフィールドの管理

[高度な設定](#advanced-configurations)を参照してください。

>[!NOTE]
>
>これらの操作を実行するには、Adobe Campaign の&#x200B;**管理**&#x200B;ロールを持っている必要があります。

### 前提条件 {#prerequisites}

事前に、次の要素があることを確認してください。

* [AEM 作成者インスタンス](/help/sites-deploying/deploy.md#getting-started)
* [AEM 発行インスタンス](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign Classic インスタンス](https://helpx.adobe.com/support/campaign/classic.html) - クライアントおよびサーバーを含みます
* Internet Explorer 11

>[!NOTE]
>
>Adobe Campaign Classic ビルド 8640 より前のバージョンを実行している場合、詳しくは、[アップグレードに関するドキュメント](https://docs.campaign.adobe.com/doc/AC6.1/en/PRO_Updating_Adobe_Campaign_Upgrading.html)を参照してください。クライアントとデータベースの両方を同じビルドにアップグレードする必要があります。

>[!CAUTION]
>
>[Adobe Campaign の設定](#configuring-adobe-campaign)および [Adobe Experience Manager の設定](#configuring-adobe-experience-manager)の節で詳しく述べた操作は、AEM と Adobe Campaign の間の統合機能が正しく機能するために必要です。

### AEM 統合パッケージのインストール {#installing-the-aem-integration-package}

**AEM 統合**&#x200B;パッケージを Adobe Campaign にインストールする必要があります。次の手順を実行します。

1. AEM とリンクしたい Adobe Campaign インスタンスに移動します。
1. *ツール*／*詳細*／*パッケージをインポート...*&#x200B;を選択します。

   ![chlimage_1-132](assets/chlimage_1-132a.png)

1. 「**標準パッケージをインストール**」をクリックして、「**AEM 統合**」パッケージを選択します。

   ![chlimage_1-133](assets/chlimage_1-133a.png)

1. 「**次へ**」をクリックし、「**開始**」をクリックします。

   このパッケージには、AEM サーバーを Adobe Campaign に接続するために使用する **aemserver** 演算子が含まれています。

   >[!CAUTION]
   >
   >デフォルトでは、この演算子には、セキュリティゾーンは設定されていません。AEM を使用して Adobe Campaign に接続するには、これを選択する必要があります。
   >
   >ログイン／パスワードで認証して AEM を Adobe Campaign に接続するには、**serverConf.xml** ファイルで、選択したセキュリティゾーンの **allowUserPassword** 属性を **true** に設定する必要があります。
   >
   >セキュリティの問題を回避するために、AEM 専用のセキュリティゾーンを作成することを強くお勧めします。この件について詳しくは、[インストールガイド](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html?lang=ja)を参照してください。

   ![chlimage_1-134](assets/chlimage_1-134a.png)

### AEM 外部アカウントの設定 {#configuring-an-aem-external-account}

Adobe Campaign を AEM インスタンスに接続可能な外部アカウントを設定する必要があります。

>[!NOTE]
>
>* **AEM 統合**&#x200B;パッケージをインストールする際に、外部 AEM アカウントが作成されます。そこから AEM インスタンスへの接続を設定するか、新しいものを作成できます。
>* AEM で、campaign-remote ユーザーのパスワードを設定してください。AEM で Adobe Campaign に接続するにはこのパスワードを設定する必要があります。管理者としてログインし、ユーザー管理コンソールで campaign-remote ユーザーを探して「**パスワードを設定**」をクリックします。
>


外部 AEM アカウントを設定するには：

1. **管理**／**プラットフォーム**／**外部アカウント**&#x200B;ノードに移動します。
1. 新しい外部アカウントを作成して、**AEM** タイプを選択します。
1. AEM オーサーインスタンスのアクセスパラメーター（サーバーアドレスと、このインスタンスに接続するために使用される ID およびパスワード）を入力します。campaign-api ユーザーアカウントのパスワードは、AEM で campaign-remote user に設定したパスワードと同じです。

   >[!NOTE]
   >
   >サーバーアドレスは、末尾がスラッシュで&#x200B;**終わらない**&#x200B;ようにします。例えば、`https://yourserver:4502/` の代わりに `https://yourserver:4502` を入力します

   ![chlimage_1-135](assets/chlimage_1-135a.png) ![chlimage_1-136](assets/chlimage_1-136a.png)

1. 「**有効**」チェックボックスが選択されていることを確認します。

### AEMResourceTypeFilter オプションの検証 {#verifying-the-aemresourcetypefilter-option}

「**AEMResourceTypeFilter**」オプションを使用すると、Adobe Campaign で使用できる AEM リソースのタイプをフィルタリングできます。これにより、Adobe Campaign でのみ使用されるように特別に設計された AEM コンテンツを Adobe Campaign で取得できます。

このオプションは、事前設定されている必要があります。ただし、このオプションを変更すると、統合が機能しなくなる可能性があります。

**AEMResourceTypeFilter** オプションが設定されていることを検証するには：

1. **プラットフォーム**／**オプション**&#x200B;に移動します。
1. 「**AEMResourceTypeFilter**」オプションで、パスが正しいことをチェックします。このフィールドには、次の値が含まれている必要があります。

   **mcm/campaign/components/newsletter,mcm/campaign/components/campaign_newsletterpage,mcm/neolane/components/newsletter**

   また、場合によっては、この値は次のようになります。

   **mcm/campaign/components/newsletter**

   ![chlimage_1-137](assets/chlimage_1-137a.png)

## Adobe Experience Manager の設定 {#configuring-adobe-experience-manager}

AEM を設定するには、次の手順を実行する必要があります。

* インスタンス間のレプリケーションを設定します。
* クラウドサービスを使用して、AEM を Adobe Campaign に接続します。
* Externalizer を設定します。

### AEM インスタンス間のレプリケーションの設定 {#configuring-replication-between-aem-instances}

AEM オーサーインスタンスから作成されたコンテンツは、最初にパブリッシュインスタンスに送信されます。ニュースレターの画像をパブリッシュインスタンスで利用でき、ニュースレター受信者が入手できるように、公開する必要があります。レプリケーションエージェントは、その結果として、AEM オーサーインスタンスから AEM パブリッシュインスタンスにレプリケートするように設定される必要があります。

>[!NOTE]
>
>レプリケーション URL を使用せずに公開 URL を使用する場合は、OSGi で次のように&#x200B;**公開 URL** を設定できます（**AEM のロゴ**／「**ツール**」アイコン／**運用**／**Web コンソール**／**OSGi 設定**／**AEM Campaign 統合 - 設定**）。
>**公開 URL：** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

また、この手順は、あるオーサーインスタンス設定をパブリッシュインスタンスにレプリケートするためにも必要です。

AEM インスタンス間のレプリケーションを設定するには：

1. オーサーインスタンスで、**AEM のロゴ**／「**ツール**」アイコン／**導入**／**レプリケーション**／**作成者のエージェント**&#x200B;を選択し、「**デフォルトエージェント**」をクリックします。

   ![chlimage_1-138](assets/chlimage_1-138a.png)

   >[!NOTE]
   >パブリッシュおよびオーサーインスタンスが両方とも同じコンピューターにある場合を除いて、Adobe Campaign との統合を設定する際に、localhost（これは、AEM のローカルコピーです）を使用するのを回避します。

1. 「**編集**」をタップまたはクリックして、「**トランスポート**」タブを選択します。
1. **localhost** を IP アドレスまたは AEM パブリッシュインスタンスのアドレスに置き換えることで、URI を設定します。

   ![chlimage_1-139](assets/chlimage_1-139a.png)

### AEM から Adobe Campaign への接続 {#connecting-aem-to-adobe-campaign}

AEM と Adobe Campaign を一緒に使用する前に、両方のソリューション間のリンクを確立して、通信できるようにする必要があります。

1. AEM オーサーインスタンスに接続します。
1. **AEM のロゴ**／「**ツール**」アイコン&#x200B;**／導入**／**クラウドサービス**&#x200B;を選択して、Adobe Campaign セクションの「**今すぐ設定**」を選択します。

   ![chlimage_1-140](assets/chlimage_1-140a.png)

1. 「**タイトル**」にタイトルを入力して「**作成**」をクリックするか、Adobe Campaign インスタンスとリンクしたい既存の設定を選択することで、新しい設定を作成します。
1. 設定を編集して、Adobe Campaign インスタンスのパラメーターと一致するようにします。

   * **ユーザー名**：**aemserver**（2 つのソリューション間のリンクを確立するために使用される Adobe Campaign AEM 統合パッケージ演算子）。
   * **パスワード**：Adobe Campaign aemserver 演算子のパスワード。この演算子のパスワードを Adobe Campaign で直接再指定する必要があることがあります。
   * **API エンドポイント**：Adobe Campaign インスタンス URL。

1. 「**Adobe Campaign に接続**」を選択し、「**OK**」をクリックします。

   ![chlimage_1-141](assets/chlimage_1-141a.png)

   >[!NOTE]
   >[電子メールを作成して公開](/help/sites-authoring/campaign.md)したら、パブリッシュインスタンスに設定を再公開する必要があります。

   ![chlimage_1-142](assets/chlimage_1-142a.png)

>[!NOTE]
>接続に失敗する場合は、次を確認してください。
>* Adobe Campaign インスタンスへのセキュリティで保護された接続（https）を使用する際、証明書の問題が発生する可能性があります。Adobe Campaign インスタンスの証明書を AEM インスタンスの JDK の **cacerts** ファイルに追加する必要があります。
>* セキュリティゾーンは、Adobe Campaign の [aemserver 演算子](#connecting-aem-to-adobe-campaign)用に設定される必要があります。さらに、**serverConf.xml** ファイルで、セキュリティゾーンの **allowUserPassword** 属性を **true** に設定し、ログイン／パスワードモードを使用して Adobe Campaign への AEM の接続を認証する必要があります。
>また、[AEM／Adobe Campaign 統合のトラブルシューティング](/help/sites-administering/troubleshooting-campaignintegration.md)も参照してください。

### Externalizer の設定 {#configuring-the-externalizer}

オーサーインスタンスの AEM に [Externalizer を設定](/help/sites-developing/externalizer.md)する必要があります。Externalizer は、リソースパスを外部 URL および絶対 URL に変換できる OSGi サービスです。このサービスは、これらの外部 URL を設定および構築するための一元化された場所を提供します。

一般的な指示については、[Externalizer の設定](/help/sites-developing/externalizer.md)を参照してください。Adobe Campaign 統合について、`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` の公開サーバーが `localhost:4503` ではなく、Adobe Campaign コンソールが到達可能なサーバーを指すように設定していることを確認してください。

`localhost:4503` または Adobe Campaign が到達できない別のサーバーを指している場合、Adobe Campaign コンソールに画像が表示されません。

![chlimage_1-143](assets/chlimage_1-143a.png)

## 高度な設定 {#advanced-configurations}

また、次のような高度な設定を実行できます。

* パーソナライゼーションフィールドおよびブロックの管理。
* パーソナライゼーションブロックのアクティベート解除。
* ターゲット拡張データの管理。

### パーソナライゼーションフィールドおよびブロックの管理 {#managing-personalization-fields-and-blocks}

パーソナライゼーションを AEM の電子メールコンテンツに追加可能なフィールドおよびブロックは、Adobe Campaign で管理されます。

デフォルトのリストは提供されますが、変更できます。また、パーソナライゼーションフィールドおよびブロックを追加または非表示にすることができます。

#### パーソナライゼーションフィールドの追加 {#adding-a-personalization-field}

新しいパーソナライゼーションフィールドを既に利用可能なフィールドに追加するには、次のように Adobe Campaign の **nms:seedMember** スキーマを拡張する必要があります。

>[!CAUTION]
>追加する必要があるフィールドは、受信者スキーマ拡張（**nms:受信者**）で既に追加されている必要があります。詳しくは、[設定](https://docs.campaign.adobe.com/doc/AC6.1/en/CFG_Editing_schemas_Editing_schemas.html)ガイドを参照してください。

1. Adobe Campaign のナビゲーションで、**管理**／**設定**／**データスキーマ**&#x200B;ノードに移動します。
1. 「**新規**」を選択します。

   ![chlimage_1-144](assets/chlimage_1-144a.png)

1. ポップアップウィンドウで「**拡張スキーマを使用してテーブルのデータを拡張する**」を選択し、「**次へ**」をクリックします。

   ![chlimage_1-145](assets/chlimage_1-145a.png)

1. 拡張されたスキーマの別のパラメーターを入力します。

   * **スキーマ**：**nms:seedMember** スキーマを選択します。ウィンドウのその他のフィールドは、自動的に入力されます。
   * **名前空間**：拡張されたスキーマの名前空間をパーソナライズします。

1. スキーマの XML コードを編集して、そこに追加したいフィールドを指定します。Adobe Campaign のスキーマ拡張について詳しくは、[設定ガイド](https://docs.campaign.adobe.com/doc/AC6.1/en/CFG_Editing_schemas_Extending_a_schema.html)を参照してください。
1. スキーマを保存してから、コンソールの&#x200B;**ツール**／**詳細**／**データベース構造を更新**&#x200B;メニューで、Adobe Campaign データベース構造を更新します。
1. 変更を保存するために、Adobe Campaign コンソールを切断してから再接続します。AEM で利用可能なパーソナライゼーションフィールドのリストに新しいフィールドが表示されます。

#### 例 {#example}

「**登録番号**」フィールドを追加するには、次の要素が必要です。

* 次を含む **cus:recipient** という名前の **nms:recipient** スキーマ拡張：

```xml
<element desc="Recipient table (profiles)" img="nms:recipient.png" label="Recipients" labelSingular="Recipient" name="recipient">

  <attribute dataPolicy="smartCase" desc="Recipient registration number"
  label="Registration Number"
  length="50" name="registrationNumber" type="string"/>

</element>
```

次を含む **cus:seedMember** という名前の **nms:seedMember** スキーマ拡張：

```xml
<element desc="Seed to insert in the export files" img="nms:unknownad.png" label="Seed addresses" labelSingular="Seed" name="seedMember">

  <element name="custom_nms_recipient">
    <attribute name="registrationNumber"
    template="cus:recipient:recipient/@registrationNumber"/>
  </element>

</element>
```

「**登録番号**」フィールドが、利用可能なパーソナライゼーションフィールドに含まれるようになります。

![chlimage_1-146](assets/chlimage_1-146.png)

#### パーソナライゼーションフィールドを非表示にする {#hiding-a-personalization-field}

パーソナライゼーションフィールドを既に利用可能なフィールドの中から非表示にするには、[パーソナライゼーションフィールドの追加](#adding-a-personalization-field)の節で説明しているとおり、Adobe Campaign の **nms:seedMember** スキーマを拡張する必要があります。次の手順を適用します。

1. 拡張されたスキーマの **nms:seedMember** スキーマから取得したいフィールドをコピーします（例：**cus:seedMember**）。
1. **advanced=&quot;true&quot;** XML 属性をフィールドに追加します。AEM で利用可能なパーソナライゼーションフィールドのリストに表示されなくなります。

   例えば「**ミドルネーム**」フィールドを非表示にするには、**cud:seedMember** スキーマに次の要素を含める必要があります。

   ```xml
   <element desc="Seed to insert in the export files" img="nms:unknownad.png" label="Seed addresses" labelSingular="Seed" name="seedMember">
   
     <element name="custom_nms_recipient">
       <attribute advanced="true" name="middleName"/>
     </element>
   
   </element>
   ```

### パーソナライゼーションブロックのアクティベート解除 {#deactivating-a-personalization-block}

利用可能なもののパーソナライゼーションブロックのアクティベートを解除するには：

1. Adobe Campaign のナビゲーションで、**リソース**／**キャンペーン管理**／**パーソナライゼーションブロック**&#x200B;ノードに移動します。
1. AEM でアクティベートを解除したいパーソナライゼーションブロックを選択します。
1. 「**カスタマイズメニューに表示**」チェックボックスをオフにして、変更を保存します。ブロックが、Adobe Campaign で利用可能なパーソナライゼーションブロックのリストに表示されなくなります。

   ![chlimage_1-147](assets/chlimage_1-147a.png)

### ターゲット拡張データの管理 {#managing-target-extension-data}

パーソナライゼーション用にターゲット拡張データを挿入することもできます。ターゲット拡張データ（「Target データ」とも呼ばれる）は、例えば、キャンペーンワークフローのクエリのデータを機能強化または追加することに由来します。詳しくは、[クエリの作成](https://docs.campaign.adobe.com/doc/AC/en/PTF_Creating_queries_About_queries_in_Campaign.html)および[データの機能強化](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Enriching_data.html)の節を参照してください。

>[!NOTE]
>ターゲットにあるデータは、AEM コンテンツが Adobe Campaign 配信と同期されている場合にのみ利用できます。[AEM で作成されたコンテンツと Adobe Campaign の配信の同期](/help/sites-authoring/campaign.md#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)を参照してください。

![chlimage_1-148](assets/chlimage_1-148a.png)
