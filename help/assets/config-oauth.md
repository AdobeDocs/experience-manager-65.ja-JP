---
title: スマートコンテンツサービスを使用したアセットのタグ付けの設定
description: スマートコンテンツサービスを使用して、 [!DNL Adobe Experience Manager] でスマートタグと拡張スマートタグを設定する方法について説明します。
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
source-git-commit: d8d821a64b39b312168733126de8929c04016ff1
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 50%

---

# OAuth 認証情報のスマートタグのトラブルシューティング {#oauth-config}

の同意を採用するには、オープンな認証設定が必要です。 [!DNL Adobe Experience Manager] 安全な方法でスマートコンテンツサービスとやり取りするためのアプリケーション。

>[!NOTE]
>
> 2024 年 6 月以降は、新しい JWT 資格情報を作成できません。 今後は、OAuth サーバー間資格情報のみが作成されます。
> JWT 統合は、既存の AMS およびオンプレミスのユーザーに対してのみ、2025 年 1 月まで引き続き機能します。

## 新しい AMS ユーザー用の OAuth 設定 {#oauth-config-existing-ams-users}

こちらを参照してください [スマートコンテンツサービスの設定](#integrate-adobe-io) 新規ユーザー用の OAuth サービスの設定の場合。 完了したら、次の手順に従います [手順](#prereqs-config-oauth-onprem).

>[!NOTE]
>
>必要に応じて、次の手順でサポートチケットを送信できます [サポートプロセス](https://experienceleague.adobe.com/?lang=ja&amp;support-tab=home#support).

## 既存の AMS ユーザーの OAuth 設定 {#oauth-config-new-ams-users}

この方法に従って手順を実行する前に、以下を実装する必要があります。

### 前提条件 {#prereqs-config-oauth-onprem}

OAuth 設定には、次の前提条件が必要です。

* で新しい OAuth 統合を作成します。 [Developer Console](https://developer.adobe.com/console/user/servicesandapis). の使用 `ClientID`, `ClientSecret`, `OrgID`、および以下の手順のその他のプロパティ：
* 次のファイルがこのパスにあります `/apps/system/config in crx/de`:
   * `com.**adobe**.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

### 既存の AMS およびオンプレミス ユーザー用の OAuth 設定 {#steps-config-oauth-onprem}

次の手順は、システム管理者が実行できます。 AMS のお客様は、Adobe担当者に連絡するか、次の手順に従ってサポートチケットを送信できます [サポートプロセス](https://experienceleague.adobe.com/?lang=ja&amp;support-tab=home#support).

1. で以下のプロパティを追加または更新します `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * を更新 `auth.token.provider.client.id` を新しい OAuth 設定のクライアント ID に置き換えます。
   * 更新 `auth.access.token.request` 対象： `"https://ims-na1.adobelogin.com/ims/token/v3"`
1. ファイル名をに変更 `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
1. で以下の手順を実行します `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * 新しい OAuth 統合から、プロパティ auth.ims.client.secret をクライアント秘密鍵で更新します。
   * ファイル名をに変更 `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
1. コンテンツリポジトリ開発コンソール（例：CRXDE）で、すべての変更を保存します。
<!--
1. Navigate to `/system/console/configMgr` and replace the OSGi configuration from `.<randomnumber>` to `-<randomnumber>`.
1. Delete the old OSGi configuration for `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
-->
1. 対象： `System/console/configMgr`、の古い設定を削除します `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl` およびアクセストークンのプロバイダー名 `adobe-ims-similaritysearch`.
1. コンソールを再起動します。

## 設定の検証 {#validate-the-configuration}

設定を完了したら、JMX MBean を使用して設定を検証できます。検証するには、次の手順に従います。

1. [!DNL Experience Manager] サーバー （`https://[aem_server]:[port]`）にアクセスします。

1. **[!UICONTROL ツール]**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;に移動して、OSGi コンソールを開きます。**[!UICONTROL メイン]／[!UICONTROL JMX]** をクリックします。

1. 「`com.day.cq.dam.similaritysearch.internal.impl`」をクリックします。**[!UICONTROL SimilaritySearch Miscellaneous Tasks]** が開きます。

1. 「`validateConfigs()`」をクリックします。**[!UICONTROL 設定を検証]**&#x200B;ダイアログで、「**[!UICONTROL 起動]**」をクリックします。

同じダイアログに検証結果が表示されます。

## と Adobe 開発者コンソールの統合 {#integrate-adobe-io}

新しいユーザーとしてAdobe Developer コンソールと統合すると、 [!DNL Experience Manager] サーバーは、リクエストをスマートコンテンツサービスに転送する前に、Adobe Developer コンソールゲートウェイを使用してサービス資格情報を認証します。 統合するには、組織の管理者権限と、組織で購入して有効化されたスマートコンテンツサービスライセンスを持つAdobe ID アカウントが必要です。

スマートコンテンツサービスを設定するには、次のトップレベルの手順に従います。

1. 公開鍵を生成するには、次の手順に従います。 [スマートコンテンツサービスの作成](#obtain-public-certificate) での設定 [!DNL Experience Manager]. [公開証明書のダウンロード](#obtain-public-certificate) （OAuth 統合用）。

1. *[既存のユーザーには適用されません]* [Adobe Developer コンソールでの統合の作成](#create-adobe-i-o-integration).

1. Adobe Developer Console の API キーおよびその他の資格情報を使用して、[デプロイメントを設定します](#configure-smart-content-service)。

1. [設定をテストします](#validate-the-configuration)。

## スマートコンテンツサービス設定を作成して公開証明書をダウンロード {#download-public-certificate}

公開証明書により、Adobe Developer コンソールでプロファイルを認証できます。

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL Cloud Services]**／**[!UICONTROL 従来の Cloud Services]** にアクセスします。

1. クラウドサービスページで、「**[!UICONTROL アセットのスマートタグ]**」の「**[!UICONTROL 今すぐ設定]**」をクリックします。

1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、スマートタグ設定のタイトルと名前を指定します。「**[!UICONTROL 作成]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、以下の値を使用します。

   **[!UICONTROL サービス URL]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   （例：`https://smartcontent.adobe.io/apac`）。Experience Manager オーサーインスタンスがホストされている地域として、`na`、`emea` または `apac` を指定することができます。

   >[!NOTE]
   >
   >2022年9月1日（PT）より前に Experience Manager Managed Service がプロビジョニングされている場合は、次のサービス URL を使用します。
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 認証サーバー]**: `https://ims-na1.adobelogin.com`

   その他のフィールドは現時点では空白のままにします（後で指定します）。「**[!UICONTROL OK]**」をクリックします。

   ![コンテンツサービスの URL を指定するための Experience Manager スマートコンテンツサービスダイアログ](assets/aem_scs12.png)

   *図：コンテンツサービスの URL を指定するためのスマートコンテンツサービスダイアログ*

   >[!NOTE]
   >
   >として提供された URL [!UICONTROL サービス URL] はブラウザーからアクセスできず、404 エラーが発生します。 設定は、[!UICONTROL サービス URL] パラメーターの同じ値で正常に動作します。サービスの全体的なステータスとメンテナンススケジュールについては、[https://status.adobe.com](https://status.adobe.com) を参照してください。

1. クリック **[!UICONTROL OAuth 統合用の公開証明書をダウンロード]**&#x200B;公開証明書ファイルをダウンロードします `AEM-SmartTags.crt`. さらに、この証明書をAdobe開発者コンソールにアップロードする必要もなくなりました。

   ![スマートタグ付けサービス用に作成された設定の表現](assets/smart-tags-download-public-cert1.png)

   *図：スマートタグサービスの設定。*

## Adobe 開発者コンソール統合の作成 {#create-adobe-i-o-integration}

スマートコンテンツサービス API を使用するには、Adobe 開発者コンソールで統合を作成して、[!UICONTROL API キー]（Adobe 開発者コンソール統合の[!UICONTROL クライアント ID] フィールドで生成）、[!UICONTROL テクニカルアカウント ID]、[!UICONTROL 組織 ID]、および[!UICONTROL クライアント秘密鍵]を、[!DNL Experience Manager] のクラウド設定の [!UICONTROL Assets スマートタグサービス設定]用に取得します。

1. アクセス [https://developer.adobe.com/console/](https://developer.adobe.com/console/) ブラウザーで。 適切なアカウントを選択し、関連付けられた組織の役割がシステム管理者であることを確認します。

1. 任意の名前でプロジェクトを作成します。「**[!UICONTROL API を追加]**」をクリックします。

1. **[!UICONTROL API を追加]**&#x200B;ページで、「**[!UICONTROL Experience Cloud]**」を選択し、「**[!UICONTROL スマートコンテンツ]**」を選択します。「**[!UICONTROL 次へ]**」をクリックします。

1. を選択します。 **[!UICONTROL OAuth サーバー間]** 認証方法。

1. を追加/変更 **[!UICONTROL 資格情報名]** 必要に応じて、 「**[!UICONTROL 次へ]**」をクリックします。

1. 製品プロファイルの選択 **[!UICONTROL スマートコンテンツサービス]**. クリック **[!UICONTROL 設定済み API を保存]**. OAuth API は、今後の使用のために接続された資格情報の下に追加されます。 をコピーできます [!UICONTROL API キー（クライアント ID）] または [!UICONTROL アクセストークンの生成] そこから。
<!--
1. On the **[!UICONTROL Select product profiles]** page, select **[!UICONTROL Smart Content Services]**. Click **[!UICONTROL Save configured API]**.

   A page displays more information about the configuration. Keep this page open to copy and add these values in [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager] to configure smart tags.

   ![In the Overview tab, you can review the information provided for integration.](assets/integration_details.png)


   *Figure: Details of integration in Adobe Developer Console*
-->

![oauth 設定](assets/oauth-config.png)
*図：Adobe Developer コンソールで設定された OAuth サーバー間*

## スマートコンテンツサービスの設定 {#configure-smart-content-service}

統合を設定するには、Adobe 開発者コンソール統合から、[!UICONTROL テクニカルアカウント ID]、[!UICONTROL 組織 ID]、[!UICONTROL クライアント秘密鍵]、および[!UICONTROL クライアント ID] の各フィールドの値を使用します。スマートタグのクラウド設定を作成すると、[!DNL Experience Manager] デプロイメントからの API 要求を認証できるようになります。

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;に移動して、[!UICONTROL クラウドサービス]コンソールを開きます。

1. 「**[!UICONTROL アセットのスマートタグ]**」で、上記で作成した設定を開きます。サービス設定ページで、「**[!UICONTROL 編集]**」をクリックします。

1. **[!UICONTROL AEM スマートコンテンツサービス]**&#x200B;ダイアログで、「**[!UICONTROL サービス URL]**」および「**[!UICONTROL 認証サーバー]**」フィールドに事前入力された値を使用します。

1. [Adobe 開発者コンソールの統合](#create-adobe-i-o-integration)で生成した次の値を使用して、[!UICONTROL API キー]、[!UICONTROL テクニカルアカウント ID]、[!UICONTROL 組織 ID]、および[!UICONTROL クライアント秘密鍵]の各フィールドにコピーします。

   | [!UICONTROL アセットのスマートタグサービス設定] | [!DNL Adobe Developer Console] 統合フィールド |
   |--- |--- |
   | [!UICONTROL API キー] | [!UICONTROL クライアント ID] |
   | [!UICONTROL テクニカルアカウント ID] | [!UICONTROL テクニカルアカウント ID] |
   | [!UICONTROL 組織 ID] | [!UICONTROL 組織 ID] |
   | [!UICONTROL クライアントの秘密鍵] | [!UICONTROL クライアント秘密鍵] |

>[!MORELIKETHIS]
>
>* [概要とスマートタグのトレーニング方法](enhanced-smart-tags.md)
>* [スマートタグの設定](config-smart-tagging.md)
>* [スマートタグに関するビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html?lang=ja)