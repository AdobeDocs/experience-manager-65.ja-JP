---
title: Experience Manager AssetsをAdobeAsset Link 用に設定
description: Experience Manager Assetsを設定アプリケーション用のAdobeAsset Link 拡張機能と共に使用するようにCreative Cloudします。
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
source-git-commit: e91fa04d87c7ecacf3ad8a148227948eafe15b1e
workflow-type: tm+mt
source-wordcount: '3149'
ht-degree: 5%

---


# Experience Manager AssetsをAdobeAsset Link 用に設定 {#adobe-asset-link}

[Adobeアセットリンク (AAL)](https://www.adobe.com/jp/creativecloud/business/enterprise/adobe-asset-link.html) は、コンテンツ作成プロセスでのクリエイティブ担当者とマーケターのコラボレーションを合理化します。 Adobe Experience Manager Assets をCreative Cloudのデスクトップアプリケーション、Adobe InDesign、Adobe Photoshop、Adobe Illustratorに接続します。 Adobe Asset Link パネルを使用すると、AEM Assets に保存されたコンテンツに対して、クリエイティブが最もなじみのあるクリエイティブアプリケーションからアクセスして、変更を加えることができます。

Experience Manager Assetsを Asset Link と共に使用するように設定するには、次のタスクを実装します。 Experience Manager管理者アカウントを使用して設定を行います。

1. 必要に応じて、パッケージをインストールします。 詳細は、 [前提条件](#prerequisites).

1. 設定Experience Manager [手動](#manual-configuration) または [パッケージ](#configure-using-package).

1. Creative CloudのライセンスユーザーをExperience Managerユーザーにマッピングするには、 [ユーザーのアクセス制御](#user-access).

1. 作成 [カスタムクエリインデックス](#create-custom-index)，設定 [FPO レンディション](/help/assets/configure-fpo-renditions.md) InDesignの場合は、 [Adobe Stock統合](/help/assets/aem-assets-adobe-stock.md)、および設定 [視覚的または類似性検索](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## 様々な機能の前提条件とサポート {#prerequisites}

必要に応じて、適切なサービスパックとパッケージをインストールしてください。 各機能のバージョンとExperience Managerについて、次の要件を参照してください。

| Assets の機能 | Experience Managerのバージョンとサポートの要件 |
|--- |--- |
| アセットリンクはデフォルトで機能します | Experience Manager6.5 および 6.5.2 以降。 </br> Experience Manager6.4.4 および 6.4.6 以降。 </br> Adobeは、最新の [Experience Managerサービスパック (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html) AAL を使用する前に |
| パッケージのインストール後に Asset Link が機能する | Experience Manager6.4.0～6.4.3 の場合は、をインストールします。 [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) パッケージ。 |
| Adobe Stock との連携 | Adobe Experience Manager 6.4.2 以降 |
| ビジュアル検索または類似検索 | Adobe Experience Manager 6.5.0 以降 |


## 設定パッケージを使用したExperience Managerの設定 {#configure-using-package}

Adobeでは、 [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) 設定パッケージを使用して、ほとんどの設定タスクを自動化し、その後いくつかの手動タスクを実行します。 または、 [手動で設定](#manual-configuration).

>[!CAUTION]
>
>Experience ManagerインスタンスがユーザーアカウントでのAdobe IMSログイン用に設定されている場合は、設定パッケージを使用しないでください。 代わりに、 [手動で設定](#manual-configuration) Experience Managerインスタンス。

1. パッケージマネージャーを開くには、Experience ManagerWeb インターフェイスで、 **[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL パッケージ共有]**. インストール `adobe-asset-link-config` パッケージ。

1. **[!UICONTROL ツール]**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;にアクセスします。場所 **[!UICONTROL AdobeGranite OAuth IMS プロバイダー]** 設定を編集し、クリックして編集します。

   次のプロパティを設定し、変更を保存します。

   * [!UICONTROL グループマッピング]:必要に応じて、空のままにします。 詳しくは、 [グループマッピング](#group-mapping).
   * [!UICONTROL 組織]:Adobe Admin Consoleで使用する組織 ID を入力します。 組織 ID について詳しくは、 [ユーザーグループを作成](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html).

1. 場所 **[!UICONTROL AdobeGranite Bearer Authentication Handler]** 設定を編集し、クリックして編集します。

   追加 **[!UICONTROL InDesignAem2]** クライアント ID を **[!UICONTROL 許可されている OAuth クライアント ID]** 設定プロパティ。


## 手動設定Experience Manager {#manual-configuration}

Experience Managerパッケージを使用しない場合、またはExperience ManagerのデプロイメントがAdobe IMSアカウントでのユーザーログインをサポートするように設定されている場合は、設定を手動で設定します。

手動でExperience Managerを設定するには：

1. Configuration Manager にアクセスするには、 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL Web コンソール]**. 選択 **[!UICONTROL OSGi]** > **[!UICONTROL 設定]** 上部のメニューから。

1. を **[!UICONTROL AdobeGranite OAuth IMS プロバイダー]** 設定し、「 」をクリックして編集します。

   次の設定を行い、 **[!UICONTROL 保存]**.

   * [!UICONTROL 認証エンドポイント]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL トークンエンドポイント]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL プロファイルエンドポイント]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL 検証 URL]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL 組織]:を [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL グループマッピング]:特殊なケースがない場合は、空のままにします。 詳しくは、 [グループマッピング](#group-mapping).

1. 場所 **[!UICONTROL AdobeGranite Bearer Authentication Handler]** 設定を編集し、クリックして編集します。

   次のクライアント ID を **[!UICONTROL 許可されている OAuth クライアント ID]** 設定プロパティ： `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   各 `Client ID`をクリックし、 `+`. クリック **[!UICONTROL 保存]** すべての ID を追加した後。

1. In **[!UICONTROL AdobeGranite OAuth Application and Provider]** 設定、既存の **[!UICONTROL AdobeGranite OAuth Authentication Handler]** インスタンス。 インスタンスを見つけた場合、 `Config ID` 値 `ims`を使用する場合は、この手順の手順に使用します。 それ以外の場合は、 `+` をクリックして、設定インスタンスを作成します。 次のプロパティ値を設定し、 **[!UICONTROL 保存]**.

   * [!UICONTROL クライアント ID]:変更しない
   * [!UICONTROL クライアント秘密鍵]:変更しない
   * [!UICONTROL 設定 ID]: ` ims`
   * [!UICONTROL 範囲]: `AdobeID, OpenID, read_organizations` （他の値も設定に含まれる場合があります）
   * [!UICONTROL プロバイダー ID]: ` ims`
   * [!UICONTROL ユーザーの作成]: ` Checked`
   * [!UICONTROL ユーザー ID プロパティ]: `Email` 新しく作成された設定用。 それ以外の場合は、変更しないでください。

1. を **[!UICONTROL Apache Jackrabbit Oak デフォルト同期ハンドラー]** 設定 **[!UICONTROL 同期ハンドラー名]** `ims` をクリックして編集します。

   次の設定プロパティを設定し、「 **[!UICONTROL 保存]**.

   * [!UICONTROL ユーザーの有効期限とユーザーメンバーシップの有効期限]:&#39;m&#39;の後の分単位の時間（スペースなし）。 例： `15m` 15 分間。 詳しくは、 [グループマッピング](#group-mapping).
   * [!UICONTROL ユーザーの自動メンバーシップ]:変更しない
   * [!UICONTROL ユーザーの動的メンバーシップ]: ` Deslect`

1. を **[!UICONTROL AdobeGranite OAuth Authentication Handler]** 設定し、「 」をクリックして編集します。 変更を加えずに、 **[!UICONTROL 保存]**.

1. bearer 認証ハンドラーの相対的な優先度を調整するには、CRXDE で、に移動します。 `/apps/system/config`. 場所 `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` 設定を開きます。 最後に、 `service.ranking=I"-10"`. 変更内容を保存します。

   >[!NOTE]
   >
   >bearer トークンで認証される各リクエストには、Adobe IMSへの 3 回の呼び出し、ユーザーの同期、Experience Managerでのログイントークンの作成のオーバーヘッドが発生します。 このオーバーヘッドを克服するため、Adobeアセットリンクは、Experience Managerからの応答で返されたログイントークンをキャプチャし、後続のリクエストと共に送信します。 このプロセスを機能させるには、bearer 認証ハンドラーの相対的な優先度を調整する必要があります。

1. （オプション）Experience Managerユーザーの電子メール ID に大文字と小文字を混在させたドメイン名がある場合は、 **[!UICONTROL ユーザーのロックを小文字に変更]** in **[!UICONTROL AdobeGranite ACP プラットフォーム設定]** (Experience ManagerWeb コンソール )

## ビジネスプロファイルへの移行後の追加の設定 {#configure-migration-activity}

AdobeAsset Link のユーザーは、Experience Managerに接続して、Enterprise(CCE) 組織のメインCreative Cloudから IMS ログインを許可できます。 Experience Managerはクライアント ID を使用して、許可された IMS 組織を識別します。 ビジネスプロファイルに移行した後、Bearer Authentication Handler をExperience Managerして、IMS 組織のクライアント ID と秘密鍵を設定する必要があります。 ビジネスプロファイルについて詳しくは、 [Adobeプロファイルの概要](https://helpx.adobe.com/jp/enterprise/kb/introducing-adobe-profiles.html).

追加の設定が必要なのは、Experience Managerと Enterprise(CCE) のCreative Cloudに異なるAdobe IMS組織を使用し、これら 2 つの組織間でドメインの信頼関係が確立されている場合のみです。

>[!NOTE]
>
>* ビジネスプロファイルの修正は、Experience Manager6.5.11.0で提供されています。
>* Experience ManagerとCCEで同じAdobe IMS組織を使用している場合、既存の設定は引き続き機能します。



**前提条件**

1. AAL 用に設定された BearerExperience Managerを持つ起動および実行中の認証インスタンス。
1. Experience Manager6.5 インスタンスに、次のパッケージ (Service Pack 11) をインストールします。

   [Experience Manager6.5.11.0のダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. 連絡先 [!UICONTROL カスタマーサポート] をクリックして、IMS 組織の Bearer 認証用のクライアント ID と秘密鍵を取得します。

ビジネスプロファイルへの移行後に必要な追加の設定を次に示します。

1. In **[!UICONTROL AdobeGranite OAuth IMS 設定プロバイダー]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`)、設定：

   * OAuth 設定 ID (`oauth.configmanager.ims.configid`): `ims` （一度確認してください。既に設定されている可能性があります）

   * IMS 所有エンティティ (`ims.owningEntity`):IMS 組織 ID

   ![IMS 設定 ID](assets/bearer-authentication1.png)

1. 開く **[!UICONTROL Bearer Authentication Handler]** 設定を行い、次の場所から取得したクライアント ID を追加します。 [!UICONTROL カスタマーサポート] リストに **[!UICONTROL 許可されている OAuth クライアント ID]**.

   ![クライアント ID を追加](assets/add-clientid-bearer-auth.png)

1. 開く **[!UICONTROL AdobeGranite OAuth Application and Provider]** 設定を行い、 **[!UICONTROL クライアント ID]** および **[!UICONTROL クライアント秘密鍵]** （秘密鍵）カスタマーサポートから取得したもの。

   次を確認します。 **[!UICONTROL 設定 ID]** フィールド (`oauth.config.id`) には、 **[!UICONTROL OAuth 設定 ID]** フィールド (`oauth.configmanager.ims.configid`) を参照してください。

   ![クライアント ID を検証](assets/clientid-secretkey.png)

1. 開く **[!UICONTROL AdobeGranite IMS クラスター交換トークンプリプロセッサー]** 設定して次のように設定します。 `enable`.

## ユーザーアクセス制御を管理 {#user-access}

この節では、ユーザーと、ユーザーリポジトリへのアクセスを管理するExperience Managerを説明します。

### グループマッピング {#group-mapping}

グループマッピングによって、Experience Manager内のグループとAdobe IMS内のグループとの対応関係が決まります。 これは、AdobeAsset Link のユーザーにExperience Manager Assetsへのアクセス権限を付与する方法に重要な役割を果たします。

AdobeAsset Link と共に使用すると、Experience Managerはユーザー管理機能をAdobe IMSに委任します。 Adobe IMSのユーザーとグループに対応するユーザーとグループが自動的に作成されます。 また、ユーザー、グループ、グループのメンバーシップをExperience Managerと同期して、Adobe IMSのメンバーシップと一致させます。

例えば、AdobeアセットリンクユーザーがAdobe IMSグループ assetlink-users のメンバーである場合を考えてみましょう。 この場合、そのAdobe IMSグループのユーザーが初めてAdobeアセットリンクに接続すると、 assetlink-users という名前の同期済みグループがExperience Managerに作成されます。 Adobe IMSグループの各新規ユーザーが、初めてAdobeの Asset Link を通じてExperience Managerに接続すると、Experience Manager内の対応するグループに追加されます。

Experience Manager内のAdobe IMSに対応し、グループと同期しているグループは、直接アクセスを許可するか、別のグループのメンバーにすることでアクセスを許可できます。 権限の管理方法の例を次に示します。

![グループの例](assets/group-examples.png)

次のルールは、Experience Managerのグループマッピングに適用されます。

* 次を確認します。 **[!UICONTROL グループマッピング]** プロパティ **[!UICONTROL AdobeGranite OAuth IMS プロバイダー]** 設定が空です。
* AdobeAsset Link ユーザーグループのメンバーシップは、ユーザーの認証時に評価され、 **[!UICONTROL ユーザーの有効期限]** プロパティ **[!UICONTROL Apache Jackrabbit Oak デフォルト同期ハンドラー]** 設定が経過しました。 現在、ユーザーをExperience Manager内のグループに追加したり、グループから削除したりして、Adobe IMS内のグループと同期させることができます。
* グループ名の競合を回避します。 Adobe IMSで作成したグループに使用する名前が、すべてのExperience Managerシステムグループ名とは異なることを確認します。

   例えば、 `dam-users` グループと、グループ管理者が作成したExperience Manager。

   名前がAdobe IMSシステムグループの名前と競合するExperience Managerグループまたは手動で作成したグループは、ユーザー権限の制御に使用されません。
* Adobe IMSユーザーが、以前に作成したExperience ManagerExperience Managerと競合するAdobe IMSインスタンスに接続すると、ユーザーの名前には、一意にするために数字が追加された別の名前が付けられます。

**初回のアクセス制御の設定**

Adobeアセットリンクを通じて接続するユーザーは、必要な権限が付与された後にのみ、アセットの表示とインタラクションをおこなうことができます。 この [グループマッピング](#group-mapping) 上記の節では、Experience Managerで作成されたユーザーグループが、Adobe IMS内の組織内のユーザーグループに対応し、同期される方法について説明します。 Experience Manager管理者は、これらのグループを使用して、AdobeAsset Link ユーザーのアクセス制御を管理することをお勧めします。

Experience Manager・グループ (Adobe IMS・アクセス制御の管理に使用 ) と同期される各ユーザー・グループに対して、次の操作を行います。

1. グループに、AdobeAsset Link からの最初の接続に使用できるメンバーがあることを確認します。
1. そのユーザーを使用してAdobeAsset Link にログインし、Experience Managerに接続します。 この接続は失敗すると想定されています。
1. Experience Managerで、Adobe IMS内のグループに対応するグループを探し、目的のアクセス制御を許可します。 例えば、新しいグループが dam-users グループのメンバーになるとします。
1. Adobeアセットリンクを閉じ、アセットアプリケーションをCreative Cloudし直します。
1. ユーザーが期待どおりのアクセス権を持っていることを確認するには、Adobeアセットリンクを再度開きます。

これらの手順を実行すると、同じグループ内の他のユーザーは、最初の試行で、Adobeアセットリンクを使用してExperience Managerに接続できます。 自動的に、グループの他のユーザーと同じ権限が付与されます。

## Experience ManagerアセットリンクのAdobeユーザーを管理 {#manage-users}

AdobeAsset Link ユーザーは、Experience Managerアプリケーションにサインインすると、Creative Cloudに接続できます。 この認証は、Adobe IMSテクノロジーを使用し、ユーザー情報が存在しない場合はExperience Managerで作成します。 Experience Managerの企業のお客様は、Experience Managerと統合された外部の ID プロバイダーを使用してユーザーを管理するのが一般的です。 ID プロバイダーには、Adobe IMSや、SAML および LDAP プロトコルを使用する他の製品が含まれます。 または、ユーザーをローカルのExperience Managerで作成および管理できます。

次の場合、AdobeアセットリンクからExperience Managerに接続するユーザーは、以前のダイレクトサインインのExperience Managerに保存されている既存のユーザー情報と競合しません。

* Experience Managerへの直接ログインに使用されるユーザー名は、Creative CloudのログインにAdobe IMSで使用されるユーザー名とは異なります。
* Adobe IMSは、直接のExperience Managerログインの ID プロバイダーとして使用されます。
* ユーザーは、同じアカウントで直接Experience Managerサインインする前に、AdobeアセットリンクからExperience Managerに接続します。


一方、次のシナリオでは、直接Experience Managerログインによって作成されたAdobe情報を、Asset Link を使用できるように更新する必要があります。

* Adobe IMSを使用するCreative Cloud内のアカウントと、Adobe IMS以外の外部 ID プロバイダー内のアカウントの両方に、同じユーザー名（ユーザーの電子メールアドレスなど）が使用されます。
* 同じユーザー名が、Creative Cloud内のアカウントとローカルのExperience Managerアカウントの両方で使用されます。
* Adobe IMSのCreative Cloudアカウントは Federated ID で、ダイレクトサインイン用にExperience Managerと統合されているのと同じ外部 ID プロバイダーから提供されます。

これらのシナリオで作成されたユーザーには、Adobe IMSと同期される、ユーザーに必要なプロパティがありません。

Asset Link を使用するようにExperience ManagerでこのようなAdobeを更新するには：

1. Experience ManagerWeb コンソールで、 **[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]** 設定し、「 」をクリックして編集します。 選択を解除する **[!UICONTROL 外部 ID 保護]** チェックボックスをオンにして、 **[!UICONTROL 保存]**.
1. ユーザー管理インターフェイスにアクセスするには、Experience Managerで **[!UICONTROL ツール]** > **[!UICONTROL セキュリティ]** > **[!UICONTROL ユーザー]**. 更新するユーザーを選択し、そのユーザーのブラウザーの URL パスの末尾をメモします（で始まります）。 `/home/users`. または、CRXDE でユーザー名を検索することもできます。 サンプルのユーザーパス： `/home/users/x/xTac082TDh-guJzzG7WM`.
1. CRXDE で、ユーザーパスに移動し、ユーザーノードを選択し、ノードのプロパティを表示するには、 **[!UICONTROL プロパティ]** 」タブをクリックします。 このノードには `jcr:primaryType` プロパティ値 `rep:User`.
1. の下部に **[!UICONTROL プロパティ]** タブ領域に、 `Name` 値 `rep:externalId`, `Type` 値 `String`、および `Value` 値 `rep:authorizableId`;`ims`で、 `rep:authorizableId` が `rep:authorizableId` ノードのプロパティ。 ( セミコロンは、 `rep:authorizableId` 値 `ims`.)
1. 次をクリック： **[!UICONTROL 追加]** ボタンをクリックし、 **[!UICONTROL すべて保存]**.
1. 手順 2 ～ 5 を繰り返して、AdobeAsset Link を使用する他のユーザーに対して実行します。
1. Experience ManagerWeb コンソールで、 **[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]** 設定し、「 」をクリックして編集します。 選択を解除する **[!UICONTROL 外部 ID 保護]** チェックボックスをオンにして、 **[!UICONTROL 保存]**.

>[!NOTE]
>
>数分間でサービスが復元されない場合は、Experience Managerを再起動して正常に認証できるようにします。

この変更後、更新されたExperience ManagerユーザーはAdobeAsset Link に接続し、更新前に使用されていたExperience Managerへの直接ログインの方法を引き続き使用できます。 Adobe IMSによる認証が成功すると、Experience Managerユーザプロファイル情報は、Adobe IMSでユーザプロファイルと同期されます。

複数のExperience Managerユーザーの一括移行を実行して、ユーザーがAdobeAsset Link を操作できるようにする方法があります。 このオプションのAdobeに関する詳細およびサポートについては、サポートにお問い合わせください。

手順の代わりに、特定の状況で、Adobeの Asset Link ユーザーがExperience Managerにすばやくアクセスできるようになります。 その場合、既存のAdobe情報は、Experience ManagerAsset Link との接続前に、Experience Managerの User Management またはの CRXDE で見つかり、削除されます。 接続後に、新しいユーザ情報がExperience Managerに作成されます。 この方法は、ユーザーノードの子として追加される重要なデータがないことが確実な場合にのみ使用します。 このような余分なデータは、以下の条件を満たさないユーザーノードの子ノードです。 `tokens`, `preferences`, `profile`, `profiles`, `profiles/public`、および `rep:policy/*` ノード。

## アセットを条件付きで処理する自動開始ワークフロー {#auto-start-workflow}

Experience Manager6.4 およびExperience Manager6.5 では、管理者は、事前に定義された条件に基づいてアセットを自動的に実行および処理するようにワークフローを設定できます。

この設定は、事業部門のユーザーやマーケターが、例えば、いくつかの特定のフォルダーにカスタムワークフローを作成する場合に役立ちます。 例えば、代理店の撮影したすべてのアセットに透かしを付けたり、フリーランサーがアップロードしたすべてのアセットを処理して特定のレンディションを作成したりできます。

詳しくは、「 [アセットでのワークフローの自動実行](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets).


## Experience Manager6.4.x でのカスタムインデックスの作成 {#create-custom-index}

Experience Managerには、クエリに使用されるインデックスが含まれます。 指定したバージョンに対して次のカスタムインデックスを作成します。 Experience Manager6.5.0 には、デフォルトでこのインデックスが含まれています。 Adobeがチェックアウトしたアセットを判断するには、このインデックスが必要です。

1. CRXDE で、 `/oak:index` ノード。 という名前のノードを作成します。 `cqDrivelock` そして、 `Type` から `oak:QueryIndexDefinition`.

1. 次のプロパティを新しいノードに追加し、変更を保存します。

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## 視覚検索または類似検索の設定 {#configure-visual-similarity-search}

ビジュアル検索機能を使用すると、Asset Link パネルを使用して、AEM Assetsリポジトリ内で視覚的に類似したAdobeを検索できます。 この機能は 6.5.0 以降のバージョンで使用可能で、インデックス付きのアセットのみが検索されます。 詳しくは、 [ビジュアル検索の設定方法](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## Adobe InDesign 用のプレースメント専用レンディションの生成 {#fpo-renditions}

Experience Manager には、配置専用（FPO）のレンディションが用意されています。これらの FPO レンディションは、ファイルサイズは小さいですが、縦横比は同じです。FPO レンディションがアセットに使用できない場合、Adobe InDesign は元のアセットを代わりに使用します。このフォールバックメカニズムにより、クリエイティブワークフローは中断することなく確実に続行されます。詳しくは、 [FPO レンディションを生成](/help/assets/configure-fpo-renditions.md).


## Adobe Stockとの統合 {#adobe-stock-integration}

組織は、Adobe StockアカウントをExperience Manager Assetsと統合します。 これにより、マーケターは、ライセンスを許諾された高品質でロイヤリティフリーの写真、ベクター、イラスト、ビデオ、テンプレートおよび 3D アセットを、クリエイティブやマーケティングプロジェクトで利用できるようになります。 クリエイティブプロフェッショナルは、Asset Link パネルを使用して、これらのアセットを使用できます。

Adobe Stockと統合するには、 [Experience Manager AssetsのAdobe Stock assets](/help/assets/aem-assets-adobe-stock.md). Adobe Stockとの統合には、Experience Manager6.4.2 以降が必要です。


## Experience Managerに関する問題のトラブルシューティング {#troubleshoot}


Asset Asset Link の設定時や使用時に問題が発生した場合は、次の操作をAdobeしてください。

* デプロイメントが前提条件を満たしていることを確認します。 特に、適切な機能パックまたはパッケージがインストールされていることを確認します。
* 組織のパートナーまたはシステムインテグレーターに問い合わせてください。
* Creative Cloudユーザーがチェックアウトされたアセットを確認できない場合は、電子メール ID でドメイン名の大文字と小文字を確認します。 修正方法については、 [手動設定](#manual-configuration).
* 詳しくは、 [Asset Link のトラブルシューティング](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [Adobe Asset Link について](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [アセットデスクトップアプリケーションでのCreative Cloudリンクの使用とアセットの管理](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [Adobe Experience Manager Assets のas a Cloud Service設定](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html).






