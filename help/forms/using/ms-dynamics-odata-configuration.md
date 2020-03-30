---
title: Microsoft Dynamics OData の設定
seo-title: Microsoft Dynamics ODtata の設定
description: 統合機能の使用方法と、フォームデータモデルでオンラインとオンプレミスの Microsoft Dynamics サービスを使用する方法について説明します。
seo-description: ここでは、統合機能の使用方法と、フォームデータモデルでオンラインとオンプレミスの Microsoft Dynamics サービスを使用する方法について説明します。
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Microsoft Dynamics OData の設定{#microsoft-dynamics-odata-configuration}

![データ統合](assets/data-integeration.png)

Microsoft Dynamics は、顧客関係管理（CRM）および企業資源計画（ERP）用のソフトウェアで、顧客の口座や連絡先、潜在顧客、顧客機会、顧客事例を作成して管理する企業ソリューションを提供します。[AEM Forms のデータ統合機能](../../forms/using/data-integration.md)の OData クラウドサービス設定を使用して、オンラインの Microsoft Dynamics サービスとオンプレミスの Microsoft Dynamics サービスの両方に Forms を統合することができます。これにより、Microsoft Dynamics サービスで定義されているエンティティ、属性、サービスに基づいて、フォームデータモデルを作成できるようになります。フォームデータモデルを使用して、Microsoft Dynamics Serverとやり取りするアダプティブフォームを作成し、ビジネスワークフローを可能にできます。 次に例を示します。

* クエリMicrosoft Dynamics Serverでのデータの取得とアダプティブフォームの自動埋め込み
* アダプティブフォームの送信時にMicrosoft Dynamicsにデータを書き込む
* フォームデータモデルで定義されたカスタムエンティティを通じてMicrosoft Dynamicsでデータを書き込む、またはその逆

AEM Formsアドオンパッケージには、Microsoft DynamicsとAEM Formsをすばやく統合するために利用できる参照OData設定も含まれています。

パッケージがインストールされると、AEM Forms インスタンス上で以下のエンティティとサービスを使用できるようになります。

* MS Dynamics OData Cloud Service（OData サービス）
* 事前に設定されたMicrosoft Dynamicsのエンティティおよびサービスを含むフォームデータモデル。

The OData Cloud Service and form data model with preconfigured Microsoft Dynamics entities and services are available on your AEM Forms instance only if the run mode for the AEM instance is set as `samplecontent`(default). AEM インスタンスの実行モードの設定について詳しくは、「[実行モード](/help/sites-deploying/configure-runmodes.md)」を参照してください。

## 前提条件 {#prerequisites}

Microsoft Dynamics の設定を開始する前に、以下の項目が使用可能な状態になっていることを確認する必要があります。

* [AEM Formsアドオンパッケージのインストール](../../forms/using/installing-configuring-aem-forms-osgi.md)
* Microsoft Dynamics 365 がオンライン環境で設定されているか、以下のいずれかのバージョンの Microsoft Dynamics のインスタンスがインストールされていること：

   * オンプレミス環境の Microsoft Dynamics 365
   * オンプレミス環境の Microsoft Dynamics 2016

* [Microsoft Azure Active DirectoryにMicrosoft Dynamics Onlineサービス用のアプリケーションを登録しました](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)。 登録済みサービスのクライアントID(アプリケーション ID)とクライアントシークレットの値を控えておきます。 これらの値は [Microsoft Dynamics サービス用にクラウドサービスを設定する](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service)時に使用します。

## 登録された Microsoft Dynamics アプリケーションの応答 URL を設定する {#set-reply-url-for-registered-microsoft-dynamics-application}

以下の手順で、登録された Microsoft Dynamics アプリケーションの応答 URL を設定します。

>[!NOTE]
>
>この手順は、AEM Forms をオンラインの Microsoft Dynamics サーバーと統合する場合にのみ使用してください。

1. Go to Microsoft Azure Active Directory account and add the following cloud service configuration URL in **Reply URLs** settings for your registered application:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azureディレクトリ](assets/azure_directory_new.png)

1. 設定を保存します。

## IFD 用に Microsoft Dynamics を設定する {#configure-microsoft-dynamics-for-ifd}

外部のユーザーは、Microsoft Dynamics でクレームベース認証を使用して、Microsoft Dynamics CRM サーバー上のデータにアクセスすることができます。この機能を有効にするには、以下の手順により、インターネット接続展開（IFD）用に Microsoft Dynamics を有効にして、クレーム設定を構成します。

>[!NOTE]
>
>この手順は、AEM Forms をオンプレミスの Microsoft Dynamics サーバーと統合する場合にのみ使用してください。

1. Configure Microsoft Dynamics on-premises instance for IFD as described in [Configure IFD for Microsoft Dynamics](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Windows PowerShell を使用して以下のコマンドを実行し、IFD が有効になっている Microsoft Dynamics でクレームを設定します。

   ```
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   See [App registration for CRM on-premises (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) for details.

## AD FS マシンで OAuth クライアントを設定する {#configure-oauth-client-on-ad-fs-machine}

OAuth クライアントを Active Directory Federation Services（AD FS）マシンに登録し、AD FS マシンでアクセス権限を設定するには、以下の手順を実行します。

>[!NOTE]
>
>この手順は、AEM Forms をオンプレミスの Microsoft Dynamics サーバーと統合する場合にのみ使用してください。

1. 次のコマンドを実行します。

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   ここで、

   * `Client-ID` は、任意の GUID ジェネレーターを使用して生成できるクライアント ID です。
   * `redirect-uri` は、AEM Forms 上の Microsoft Dynamics OData クラウドサービスに対する URL です。AEM Formsパッケージと共にインストールされるデフォルトのクラウドサービスは、次のURLにデプロイされます。
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 以下のコマンドを実行して、AD FS マシン上でアクセス権を設定します。

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   ここで、

   * `resource` は、Microsoft Dynamics の組織 URL です。

1. Microsoft Dynamics では、HTTPS プロトコルが使用されます。Forms サーバーから AD FS のエンドポイントを呼び出すには、AEM Forms が稼働しているコンピューターで `keytool` コマンドを使用して、Microsoft Dynamics のサイト証明書を Java の証明書ストアにインストールします。

## Microsoft Dynamics サービス用にクラウドサービスを設定する {#configure-cloud-service-for-your-microsoft-dynamics-service}

**MS Dynamics OData Cloud Service (OData Service)の構成には、既定のOData構成が含まれています** 。 Odata サービスを設定して Microsoft Dynamics サービスに接続するには、以下の手順を実行します。

1. **[!UICONTROL ツール／クラウドサービス／データソース]**&#x200B;に移動し、`global` 設定フォルダーをタップします。
1. **MS Dynamics OData Cloud Service（OData サービス）**&#x200B;の設定を選択して「**[!UICONTROL プロパティ]**」をタップします。クラウドサービスの設定プロパティを表示するダイアログが開きます。

   「**認証設定**」タブで、次のように設定します。

   1. 「**サービスルート**」フィールドの値を入力します。Go to the Dynamics instance and navigate to **Developer Resources** to view the value for the Service Root field. 例：https://&lt;tenant-name>/api/data/v9.1/

   1. 「**クライアント ID**」（「**アプリケーション ID**」とも呼ばれます）、「**クライアントの秘密鍵**」、「**OAuth URL**」、「**更新トークン URL**」、「**アクセストークン URL**」、「**リソース**」の各フィールドのデフォルト値を、Microsoft Dynamics サービス設定の値と置き換えます。It is mandatory to specify the dynamics instance URL in the **Resource** field to configure Microsoft Dynamics with a form data model. サービスルートURLを使用して、ダイナミクスインスタンスURLを取得します。 For example, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Specify **openid** in the **Authorization Scope** field for authorization process on Microsoft Dynamics.
   ![認証の設定](assets/dynamics_authentication_settings_new.png)

1. 「**[!UICONTROL OAuth に接続]**」をクリックします。Microsoft Dynamics のログインページにリダイレクトされます。
1. Microsoft Dynamicsの資格情報を使用してログインし、承認して、クラウドサービスの設定をMicrosoft Dynamicsサービスに接続できるようにします。 このサービスとクラウドサービスとの間に接続を確立する操作は 1 回だけ行います。

   クラウドサービス設定のページに切り替わります。このページには、OData の設定が正常に保存されたことを示すメッセージが表示されます。

これで、MS Dynamics OData Cloud Service（OData サービス）がクラウドサービスとして設定され、Dynamics サービスに接続されます。

## フォームデータモデルの作成 {#create-form-data-model}

When you install the AEM Forms package, a form data model,**Microsoft Dynamics FDM**, is deployed on your AEM instance. デフォルトでは、フォームデータモデルは、MS Dynamics ODataクラウドサービス（ODataサービス）で構成されたMicrosoft Dynamicsサービスをデータソースとして使用します。

初めてフォームデータモデルを開くと、設定済みの Microsoft Dynamics サービスにフォームデータモデルが接続され、Microsoft Dynamics インスタンスからエンティティが取得されます。Microsoft Dynamics から取得される「連絡先」エンティティと「潜在顧客」エンティティは、フォームデータモデル内に既に追加されています。

フォームデータモデルを確認するには、**[!UICONTROL フォーム／データ統合]**&#x200B;に移動します。**Microsoft Dynamics FDM** を選択し、「**編集**」をクリックしてフォームデータモデルを編集モードで開きます。または、次のURLから直接フォームデータモデルを開くこともできます。

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

次に、フォームデータモデルに基づいてアダプティブフォームを作成し、次のような様々なアダプティブフォームの使用例で使用できます。

* Microsoft Dynamicsのエンティティやサービスから情報を照会して、アダプティブフォームに事前入力する
* アダプティブフォームルールを使用して、フォームデータモデルで定義されたMicrosoft Dynamicsサーバー操作を呼び出す
* 送信されたフォームデータを Microsoft Dynamics のエンティティに書き込む

AEM Forms パッケージに付属したフォームデータモデルのコピーを作成し、要件に合わせてデータモデルとサービスを設定することをお勧めします。これにより、今後のパッケージの更新時に、フォームデータモデルが上書きされることがなくなります。

ビジネスワークフローでのフォームデータモデルの作成および使用について詳しくは、「[データ統合](../../forms/using/data-integration.md)」を参照してください。
