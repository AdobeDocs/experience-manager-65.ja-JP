---
title: AEM Assets統合とExperience Cloudの設定
description: AEM Assetsとの統合を設定するExperience Cloud。
contentOwner: AG
feature: Asset Management
role: User, Architect, Admin
exl-id: d167cf97-6829-45a7-ba46-2239d530b060
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 44%

---

# AEM Assets統合とExperience Cloudの設定 {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

Adobe Experience Cloudをご利用のお客様は、Adobe Experience Manager Assets 内のアセットをAdobe Creative Cloudと（またはその逆と）同期できます。 また、アセットを Experience Cloud に（またはその逆に）同期することもできます。この同期は [!DNL Adobe I/O] を使用して設定できます。 [!DNL Adobe Marketing Cloud] の更新名は [!DNL Adobe Experience Cloud] です。

この統合をセットアップするためのワークフローを以下に示します。

1. [!DNL Adobe I/O] で公開ゲートウェイを使用して認証を作成し、アプリケーション ID を取得します。
1. アプリケーション ID を使用して、AEM Assetsインスタンス上にプロファイルを作成します。
1. この設定を使用して、アセットを同期します。

バックエンドでは、 サーバーがゲートウェイを使用してプロファイルを認証し、AEM Assets と Experience Cloud 間でデータを同期します。

>[!NOTE]
>
>この機能は [!DNL Assets] で非推奨（廃止予定）となりました。 [AEMとCreative Cloudの統合のベストプラクティス ](/help/assets/aem-cc-integration-best-practices.md) で代替品を検索します。 質問がある場合は、[Adobeカスタマーサポート ](https://www.adobe.com/account/sign-in.supportportal.html) にお問い合わせください。

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## アプリケーションの作成 {#create-an-application}

1. [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/) でログインして Adobe Developer ゲートウェイインターフェイスにアクセスします。

   >[!NOTE]
   >
   >アプリケーション ID を作成するには管理者権限が必要です。

1. 左側のウィンドウから、**[!UICONTROL 開発者ツール]** / **[!UICONTROL アプリケーション]** に移動して、アプリケーションのリストを表示します。
1. 「**** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) を追加」をクリックして、アプリケーションを作成します。
1. 「**[!UICONTROL クライアント資格情報]**」リストから「**[!UICONTROL サービスアカウント（JWT アサーション）]**」を選択します。これは、サーバー認証用のサーバー間通信サービスです。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. アプリケーションの名前とオプションの説明を指定します。
1. 「**[!UICONTROL 組織]**」リストからアセットを同期する組織を選択します。
1. **[!UICONTROL スコープ]** リストから、**[!UICONTROL dam-read]**、**[!UICONTROL dam-sync]**、**[!UICONTROL dam-write]**、**[!UICONTROL cc-share]** を選択します。
1. 「**[!UICONTROL 作成]**」をクリックします。アプリケーションが作成されたことを示すメッセージが表示されます。

   ![AEM AssetsとCreative Cloudを統合するアプリケーションが正常に作成されたことの通知](assets/chlimage_1-50.png)

1. 新規アプリケーションに対して生成された&#x200B;**[!UICONTROL アプリケーション ID]** をコピーします。

   >[!CAUTION]
   >
   >**[!UICONTROL アプリケーション ID]** ではなく&#x200B;**[!UICONTROL アプリケーションの秘密鍵]**&#x200B;を誤ってコピーしないようにしてください。

## 新しい設定をExperience Cloudに追加 {#add-a-new-configuration}

1. AEM Assets のローカルインスタンスの UI で AEM のロゴをクリックし、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;の順に移動します。

1. **[!UICONTROL Adobe Experience Cloud]** サービスを探します。 設定が存在しない場合は、「**[!UICONTROL 今すぐ設定]**」をクリックします。 設定が存在する場合は、「**[!UICONTROL 設定を表示]**」をクリックし、「`+`」をクリックして新しい設定を追加します。

   >[!NOTE]
   >
   >組織の管理者権限を持つ Adobe ID アカウントを使用してください。

1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、新しい設定のタイトルと名前を指定し、「**[!UICONTROL 作成]**」をクリックします。

   ![AEM Assets と Creative Cloud を統合する新しい設定の命名](assets/aem-ec-integration-config1.png)

1. 「**[!UICONTROL テナント URL]**」フィールドに、AEM Assets の URL を指定します。以前は、URL が `https://<tenant_id>.marketing.adobe.com` と定義されていた場合は、`https://<tenant_id>.experiencecloud.adobe.com` に変更します。

   1. **ツール／クラウドサービス／従来のクラウドサービス**&#x200B;に移動します。Adobe Experience Cloudで、「**設定を表示**」をクリックします。
   1. 編集する既存の設定を選択します。 設定を編集し、 `marketing.adobe.com` を `experiencecloud.adobe.com` に置き換えます。
   1. 設定を保存します。MAC-sync レプリケーションエージェントをテストします。

1. **[!UICONTROL クライアント ID]** フィールドに、コピーしたアプリケーション ID を、手順 [ アプリケーション ](#create-an-application) の作成の最後に貼り付けます。

   ![AEM Assets と Creative Cloud の統合に必要なアプリケーション ID 値の入力](assets/cloudservices_tenant_info.png)

1. 「 **[!UICONTROL 同期]**」で「**[!UICONTROL 有効]**」を選択して同期を有効にし、「**[!UICONTROL OK]**」をクリックします。**disabled** を選択した場合、同期は単一の方向で動作します。

1. 設定ページから「**[!UICONTROL 公開鍵を表示]**」をクリックして、インスタンスに対して生成された公開鍵を表示します。または、「**[!UICONTROL OAuth Gateway の公開鍵をダウンロード]**」をクリックして、公開鍵を含むファイルをダウンロードします。 次に、ファイルを開いて公開鍵を表示します。

## 同期の有効化 {#enable-synchronization}

1. 手順 [ の最後の手順で説明した、次のいずれかの方法を使用して公開鍵を表示し、新しい設定をExperience Cloud](#add-a-new-configuration) に追加します。 「**[!UICONTROL 公開鍵を表示]**」をクリックします。

1. 公開鍵をコピーして、[ アプリケーションの作成 ](#create-an-application) で作成したアプリケーションの設定インターフェイスの **[!UICONTROL 「公開鍵]**」フィールドに貼り付けます。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. 「**[!UICONTROL 更新]**」をクリックします。アセットをAEM Assetsインスタンスと同期します。

## 同期のテスト {#test-the-synchronization}

1. ローカルのAEM AssetsインスタンスのユーザーインターフェイスでAEMのロゴをクリックし、**[!UICONTROL ツール]** **[!UICONTROL デプロイメント]** **[!UICONTROL  レプリケーション ]**に移動して、同期用に作成されたレプリケーションプロファイルを探します。
1. **[!UICONTROL レプリケーション]** ページで、「**[!UICONTROL 作成者のエージェント]**」をクリックします。
1. プロファイルのリストから、組織のデフォルトのレプリケーションプロファイルをクリックし、それを開きます。
1. ダイアログで、「**[!UICONTROL 接続をテスト]**」をクリックします。

   ![接続のテストと組織のデフォルトのレプリケーションプロファイルの設定](assets/chlimage_1-54.png)

1. レプリケーションのテストが完了したら、テスト結果の末尾の成功メッセージを確認します。

## ユーザーをExperience Cloudに追加 {#add-users-to-experience-cloud}

1. 管理者の資格情報を使用してExperience Cloudにログインします。
1. レールから、**[!UICONTROL 管理]** に移動し、**[!UICONTROL Enterprise Dashboard を起動]** をクリックします。
1. レールの「**[!UICONTROL ユーザー]**」をクリックして、**[!UICONTROL ユーザー管理]**&#x200B;ページを開きます。
1. ツールバーの「****![aem_assets_add_icon](assets/aem_assets_add_icon.png) を追加」をクリックします。
1. Creative Cloud とアセットを共有できるようにするユーザーを 1 人以上追加します。

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## AEM AssetsとExperience Cloud {#exchange-assets-between-aem-and-experience-cloud}

1. AEM Assets にログインします。
1. Assets コンソールで、フォルダーを作成し、いくつかのアセットをアップロードします。例えば、**mc-demo** というフォルダーを作成して、アセットをアップロードします。
1. フォルダーを選択し、「**共有** ![assets_share](assets/do-not-localize/assets_share.png)」をクリックします。
1. メニューから **[!UICONTROL Adobe Experience Cloud]** を選択し、「**[!UICONTROL 共有]**」をクリックします。 フォルダーがフォルダーと共有されたことを示すメッセージがExperience Cloudされます。

   >[!NOTE]
   >
   >タイプ `sling:OrderedFolder` の Assets フォルダーの共有は、Adobe Experience Cloudでの共有のコンテキストではサポートされません。 フォルダーを共有したい場合は、AEM Assets でフォルダーを作成するときに「**[!UICONTROL 並べ替え]**」オプションを選択しないでください。

1. AEM Assetsユーザーインターフェイスを更新します。 ローカルのAEM Assetsインスタンスの Assets コンソールで作成したフォルダーが、Experience Cloudユーザーインターフェイスにコピーされます。 AEM Assetsのフォルダーにアップロードしたアセットは、AEMサーバーで処理された後、Experience Cloudーのフォルダーのコピーに表示されます。
1. フォルダー内のレプリケートされたコピーにアセットをアップロードすることもできます。Experience Cloud 処理された後、アセットは AEM Assets 内の共有フォルダーに表示されます。

<!-- Removing as per PM guidance via https://jira.corp.adobe.com/browse/CQDOC-16834?focusedCommentId=22881523&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-22881523.

## Exchange assets between AEM Assets and Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
>
>The AEM to Creative Cloud Folder Sharing feature is deprecated. Customers are strongly advised to use newer capabilities, like [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Learn more in [AEM and Creative Cloud Integration Best Practices](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets lets you share folders containing assets with Adobe Creative Cloud users.

1. In the Assets console, select the folder to share with Creative Cloud.
1. From the toolbar, click **[!UICONTROL Share]** ![assets_share](assets/do-not-localize/assets_share.png).
1. From the list, select the **[!UICONTROL Adobe Creative Cloud]** option.

   >[!NOTE]
   >
   >The options are available for users with read permissions on the root. Users must have the required permission to access the replication agent information of Marketing Cloud.

1. In the **[!UICONTROL Creative Cloud Sharing]** page, add the user to share the folder with and choose a role for the user. Click **[!UICONTROL Save]** and click **[!UICONTROL OK]**.

1. Log on to Creative Cloud with the credentials of the user you shared the folder with. The shared folder is available in Creative Cloud.

The AEM Assets-Marketing Cloud synchronization is designed in a way that the user machine instance from where the asset is uploaded retains the right to modify the asset. Only these changes are propagated to the other instance.

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and vice versa for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [アセットとCreative Cloudの統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)

