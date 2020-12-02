---
title: Experience Cloud および Creative Cloud との AEM Assets 統合の設定
seo-title: Marketing Cloud および Creative Cloud との AEM Assets 統合の設定
description: Experience Cloud および Creative Cloud との AEM Assets 統合の設定方法について説明します。
seo-description: Experience Cloud および Creative Cloud との AEM Assets 統合の設定方法について説明します。
uuid: ec36ea0e-607f-4c73-89df-e095067fccd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 82a8e807-a2df-4fe3-a68c-2dabc9328eca
docset: aem65
translation-type: tm+mt
source-git-commit: c7f06670ca8b488a661fde7a133bce6886ee7f5d
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 72%

---


# Experience Cloud および Creative Cloud との AEM Assets 統合の設定 {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

Adobe Experience Cloud のお客様は、Adobe Experience Manager（AEM）Assets 内のアセットを Adobe Creative Cloud と同期できます。また、その逆も可能です。また、アセットを Experience Cloud に（またはその逆に）同期することもできます。Adobe I/O 経由でこの同期をセットアップできます。

この統合をセットアップするためのワークフローを以下に示します。

1. Adobe I/O で公開ゲートウェイを使用して認証を作成し、アプリケーション ID を取得します。
1. アプリケーション IDを使用して、AEM Assetsインスタンスにプロファイルを作成します。
1. この設定を使用して、AEM Assets 内のアセットを Creative Cloud と同期します。

バックエンドでは、AEM サーバーがゲートウェイを使用してプロファイルを認証し、AEM Assets と Experience Cloud 間でデータを同期します。

>[!CAUTION]
>
>AEM Assets で AEM／Creative Cloud フォルダー共有機能が廃止されました。詳細を参照し、代わりの方法については、[AEMとCreative Cloud統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)を参照してください。

![AEM Assets と Creative Cloud の統合時のデータフロー](assets/chlimage_1-48.png)

AEM Assets と Creative Cloud の統合時のデータフロー

>[!NOTE]
>
>Adobe Experience Cloud と Adobe Creative Cloud でアセットを共有するには、AEM インスタンス上で管理者権限が必要です。

>[!CAUTION]
>
>Adobe Marketing CloudはAdobe Experience Cloudの烙印を押された。 以下の手順では、現在のインターフェイスを反映するため、Marketing Cloud がまだ使用されています。これらの使用は後日変更される予定です。

## アプリケーションの作成  {#create-an-application}

1. [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/) でログインして Adobe Developer ゲートウェイインターフェイスにアクセスします。

   >[!NOTE]
   >
   >アプリケーション ID を作成するには管理者権限が必要です。

1. 左側のウィンドウから、**[!UICONTROL 開発者ツール]** > **[!UICONTROL アプリケーション]**&#x200B;に移動して、アプリケーションのリストを表示します。
1. **[!UICONTROL 追加]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png)をクリックして、アプリを作成します。
1. 「**[!UICONTROL クライアント資格情報]**」リストから「**[!UICONTROL サービスアカウント（JWT アサーション）]**」を選択します。これは、サーバー認証用のサーバー間通信サービスです。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. アプリケーションの名前とオプションの説明を指定します。
1. 「**[!UICONTROL 組織]**」リストからアセットを同期する組織を選択します。
1. **[!UICONTROL スコープ]**&#x200B;リストから、**[!UICONTROL dam-read]**、**[!UICONTROL dam-sync]**、**[!UICONTROL dam-write]**、および&#x200B;**[!UICONTROL cc-share]**&#x200B;を選択します。
1. 「**[!UICONTROL 作成]**」をクリックします。アプリケーションが作成されたことを示すメッセージが表示されます。

   ![AEM Assets と Adobe CC を統合するアプリケーションの作成成功通知](assets/chlimage_1-50.png)

1. 新規アプリケーションに対して生成された&#x200B;**[!UICONTROL アプリケーション ID]** をコピーします。

   >[!CAUTION]
   >
   >**[!UICONTROL アプリケーション ID]** ではなく&#x200B;**[!UICONTROL アプリケーションの秘密鍵]**&#x200B;を誤ってコピーしないようにしてください。

## Marketing Cloud への新しい設定の追加 {#add-a-new-configuration-to-marketing-cloud}

1. AEM Assets のローカルインスタンスの UI で AEM のロゴをクリックし、**[!UICONTROL ツール]**／**[!UICONTROL クラウドサービス]**／**[!UICONTROL 従来のクラウドサービス]**&#x200B;の順に移動します。

1. **[!UICONTROL Adobe Marketing Cloud]**&#x200B;サービスを探します。 設定が存在しない場合は、「**[!UICONTROL 今すぐ設定]**」をクリックします。 設定が存在する場合は、「**[!UICONTROL 設定を表示]**」をクリックし、「`+`」をクリックして新しい設定を追加します。

   >[!NOTE]
   >
   >組織の管理者権限を持つ Adobe ID アカウントを使用してください。

1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、新しい設定のタイトルと名前を指定し、「**[!UICONTROL 作成]**」をクリックします。

   ![AEM Assets と CC を統合する新しい設定の命名](assets/chlimage_1-51.png)

1. 「**[!UICONTROL テナント URL]**」フィールドに、AEM Assets の URL を指定します。

   >[!CAUTION]
   >
   >リブランディングのため、テナントURLを`https://<tenant_id>.marketing.adobe.com`として入力した場合は、`https://<tenant_id>.experiencecloud.adobe.com.`に変更する必要があります。これを行うには、次の手順に従います。
   >
   >1. **ツール／クラウドサービス／従来のクラウドサービス**&#x200B;に移動します。
   1. Adobe Marketing Cloud の下にある「**設定を表示**」をクリックします。
   1. AEM-MAC-CC 同期のセットアップ中に作成された設定を選択します。
   1. cloudservice設定を編集し、「テナントURL」フィールドの&#x200B;**marketing.adobe.com**&#x200B;を&#x200B;**experiencecloud.adobe.com**&#x200B;に置き換えます。
   1. 設定を保存します。
   1. MAC 同期レプリケーションエージェントをテストします。


1. 「**[!UICONTROL クライアント ID]**」フィールドに、[アプリケーションを作成する](/help/sites-administering/configure-assets-cc-integration.md#create-an-application)手順の最後でコピーしたアプリケーション ID を貼り付けます。

   ![AEM Assets と Creative Cloud の統合に必要なアプリケーション ID 値の入力](assets/cloudservices_tenant_info.png)

1. 「 **[!UICONTROL 同期]**」で「**[!UICONTROL 有効]**」を選択して同期を有効にし、「**[!UICONTROL OK]**」をクリックします。

   >[!NOTE]
   「**無効**」を選択した場合、同期は単一方向に機能します。

1. 設定ページから「**[!UICONTROL 公開鍵を表示]**」をクリックして、インスタンスに対して生成された公開鍵を表示します。または、「**[!UICONTROL Download Public Key for OAuth Gateway]**」をクリックして、公開鍵を含むファイルをダウンロードします。 次に、ファイルを開いて公開鍵を表示します。

## 同期の有効化  {#enable-synchronization}

1. Marketing Cloud[に対する新しい設定の最後の手順で説明した、次の方法のいずれかを使用して、公開鍵を表示します。](/help/sites-administering/configure-assets-cc-integration.md#add-a-new-configuration-to-marketing-cloud) 「**[!UICONTROL 公開鍵を表示]**」をクリックします。

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. 公開鍵をコピーして、[アプリケーションを作成する](/help/sites-administering/configure-assets-cc-integration.md#create-an-application)手順で作成したアプリケーションの設定インターフェイスの「**[!UICONTROL 公開鍵]**」フィールドに貼り付けます。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. 「**[!UICONTROL 更新]**」をクリックします。アセットを今すぐAEM Assetsインスタンスと同期します。

## 同期のテスト {#test-the-synchronization}

1. ローカルAEM AssetsインスタンスのユーザーインターフェイスでAEMロゴをクリックし、**[!UICONTROL ツール]** **[!UICONTROL 導入]** **[!UICONTROL レプリケーション]**に移動して、同期用に作成したレプリケーションプロファイルを探します。
1. **[!UICONTROL レプリケーション]**&#x200B;ページで、**[!UICONTROL 作成者]**&#x200B;のエージェントをクリックします。
1. プロファイルのリストから、組織のデフォルトのレプリケーションプロファイルをクリックし、それを開きます。
1. ダイアログで、「**[!UICONTROL 接続をテスト]**」をクリックします。

   ![接続のテストと組織のデフォルトのレプリケーションプロファイルの設定](assets/chlimage_1-54.png)

1. レプリケーションのテストが完了したら、テスト結果の末尾の成功メッセージを確認します。

## Marketing Cloud へのユーザーの追加 {#add-users-to-marketing-cloud}

1. 管理者の資格情報を使用して Marketing Cloud にログインします。
1. レールから、**[!UICONTROL 管理]**&#x200B;に移動し、**[!UICONTROL エンタープライズダッシュボードを起動]**&#x200B;をクリックまたはタップします。
1. レールの「**[!UICONTROL ユーザー]**」をクリックして、**[!UICONTROL ユーザー管理]**&#x200B;ページを開きます。
1. ツールバーで、**追加** ![aem_assets_add_icon](assets/aem_assets_add_icon.png)をクリックまたはタップします。
1. Creative Cloud とアセットを共有できるようにするユーザーを 1 人以上追加します。

   >[!NOTE]
   Marketing Cloud に追加されたユーザーのみが、AEM Assets から Creative Cloud にアセットを共有できます。

## AEM Assets と Marketing Cloud 間でのアセットの交換  {#exchange-assets-between-aem-assets-and-marketing-cloud}

1. AEM Assets にログインします。
1. Assets コンソールで、フォルダーを作成し、いくつかのアセットをアップロードします。例えば、**mc-demo** というフォルダーを作成して、アセットをアップロードします。
1. フォルダーを選択し、「**共有** ![assets_share](assets/assets_share.png)」をクリックします。
1. メニューから「**[!UICONTROL Adobe Marketing Cloud]**」を選択し、「**[!UICONTROL 共有]**」をクリックします。フォルダーが Marketing Cloud と共有されたことを示すメッセージが表示されます。

   ![chlimage_1-55](assets/chlimage_1-55.png)

   >[!NOTE]
   `sling:OrderedFolder` タイプの Assets フォルダーの共有は、Adobe Marketing Cloud での共有の文脈ではサポートされません。フォルダーを共有したい場合は、AEM Assets でフォルダーを作成するときに「**[!UICONTROL 並べ替え]**」オプションを選択しないでください。

1. AEM Assetsのユーザインターフェイスを更新します。 ローカルのAEM Assetsインスタンスのアセットコンソールで作成したMarketing Cloudーが、フォルダーUIにコピーされます。 AEM Assetsのフォルダにアップロードしたアセットは、AEMサーバで処理された後、Marketing Cloud内のフォルダのコピーに表示されます。
1. Marketing Cloud 内にレプリケートされたフォルダーのコピーにアセットをアップロードすることもできます。処理された後、アセットは AEM Assets 内の共有フォルダーに表示されます。

## AEM Assets と Creative Cloud 間でのアセットの交換  {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
AEM／Creative Cloud フォルダー共有機能は廃止されました。お客様には、[Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)や[AEMデスクトップアプリ](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html)など、新しい機能を使用することを強くお勧めします。 詳しくは、[AEM と Creative Cloud の統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)を参照してください。

AEM Assets では、アセットを含むフォルダーを Adobe Creative Cloud のユーザーと共有できます。

1. アセットコンソールで、Creative Cloud と共有するフォルダーを選択します。
1. ツールバーで、**[!UICONTROL 共有]** ![assets_share](assets/assets_share.png)をクリックします。
1. リストから&#x200B;**[!UICONTROL Adobe Creative Cloud]**&#x200B;オプションを選択します。

   >[!NOTE]
   これらのオプションは、ルートに対する読み取り権限を持つユーザーが使用できます。ユーザーは、Adobe Marketing Cloud のレプリケーションエージェント情報にアクセスするための権限を持っている必要があります。

1. **[!UICONTROL Creative Cloud共有]**&#x200B;ページで、フォルダーを共有するユーザーを追加し、ユーザーの役割を選択します。 「**[!UICONTROL 保存]**」をクリックし、「**[!UICONTROL OK]**」をクリックします。

1. フォルダーを共有したユーザーの資格情報を使用して Creative Cloud にログオンします。Creative Cloud で共有フォルダーを利用できます。

AEM Assets と Marketing Cloud 間の同期は、アセットのアップロード元のユーザーのマシンのインスタンスがアセットを変更する権限を保持するように設計されています。これらの変更のみが他のインスタンスに反映されます。

例えば、アセットが AEM Assets の（オンプレミス）インスタンスからアップロードされている場合、このインスタンスのアセットに対する変更は Marketing Cloud のインスタンスに反映されます。ただし、Marketing Cloudインスタンスから同じアセットに対して行われた変更はAEMインスタンスに反映されず、Marketing Cloudからアップロードされたアセットの場合はインスタンスに反映されません。

>[!MORELIKETHIS]
* [AEM と Creative Cloud の統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)
* [AEM／CC フォルダー共有のベストプラクティス](/help/assets/aem-cc-folder-sharing-best-practices.md)

