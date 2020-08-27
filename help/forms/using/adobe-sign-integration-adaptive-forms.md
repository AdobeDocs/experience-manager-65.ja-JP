---
title: Adobe Sign を AEM Forms に統合する
seo-title: Adobe Sign を AEM Forms に統合する
description: AEM Forms 用に Adobe Sign を設定する方法
seo-description: AEM Forms 用に Adobe Sign を設定する方法
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: 6eb6ea86c5544329be5cb28500c59c632ccc9639
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 67%

---


# Adobe Sign を AEM Forms に統合する{#integrate-adobe-sign-with-aem-forms}

Adobe Sign により、アダプティブフォームの電子署名ワークフローを有効にすることができます。電子署名を使用すると、法務、販売、給与、人事管理など、さまざまな分野におけるドキュメント処理ワークフローが改善されます。

Adobe Sign とアダプティブフォームの一般的なシナリオでは、**サービスを申し込む**&#x200B;ためのアダプティブフォームをユーザーが入力します。例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームの入力、送信、署名を行うと、サービスプロバイダーにそのフォームが送信され、追加の処理が実行されます。サービスプロバイダーは受信した申込フォームを確認し、Adobe Sign を使用してそのフォームを承認します。これに類似した電子署名ワークフローを有効にするには、Adobe Sign を AEM Forms に統合します。

AEM FormsでAdobe Signを使用するには、AEMクラウドサービスでAdobe Signを設定します。

## 前提条件 {#prerequisites}

Adobe Sign を AEM Forms に統合するには、以下のものが必要になります。

* 有効な [Adobe Sign 開発者アカウント](https://acrobat.adobe.com/jp/ja/why-adobe/developer-form.html)
* [SSL が有効になっている](/help/sites-administering/ssl-by-default.md) AEM Forms サーバー
* [Adobe Sign API アプリケーション](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Adobe Sign API アプリケーションの資格情報（クライアントの ID と秘密鍵）
* 再設定時に、作成者インスタンスと発行インスタンスの両方から既存のAdobe Sign設定を削除します。
* オーサーインスタンスとパブリッシュインスタンスに [同じ暗号化キー](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) を使用します。

## AEM Forms を使用して Adobe Sign を設定する {#configure-adobe-sign-with-aem-forms}

上記の前提条件の準備が完了したら、以下の手順により、オーサーインスタンス上の AEM Forms を使用して Adobe Sign を設定します。

1. On AEM Forms author instance, navigate to **Tools** ![hammer](assets/hammer.png) > **General** > **Configuration Browser**.
1. On the **[!UICONTROL Configuration Browser]** page, tap **[!UICONTROL Create]**.
1. In the **[!UICONTROL Create Configuration]** dialog, specify a **[!UICONTROL Title]** for the configuration, enable **[!UICONTROL Cloud Configurations]**, and tap **[!UICONTROL Create]**. これにより、クラウドサービス用の設定コンテナが作成されます。
1. Navigate to **Tools** ![hammer](assets/hammer.png) > **Cloud Services** > **Adobe Sign** and select the configuration container you created in the above step.

   >[!NOTE]
   >
   >クラウドサービス設定ページの URL が「**HTTPS**」で始まっていることを確認してください。「HTTPS」で始まっていない場合は、AEM Forms サーバーで [SSL を有効](/help/sites-administering/ssl-by-default.md)にしてください。

1. On the configuration page, tap **[!UICONTROL Create]** to create Adobe Sign configuration in AEM Forms.
1. In the **[!UICONTROL General]** tab of the **[!UICONTROL Create Adobe Sign Configuration]** page, specify a **Name** for the configuration and tap **Next**. 必要に応じてタイトルを指定し、設定のサムネイルを参照して選択することもできます。

1. 現在のブラウザーウィンドウのURLをメモ帳にコピーします。 この URL は、AEM Forms で Adobe Sign アプリケーションを設定する際に必要になります。

1. 以下の手順により、Adobe Sign アプリケーション用に OAuth 設定を構成します。

   1. ブラウザーウィンドウを開き、Adobe Sign 開発者アカウントにサインインします。
   1. AEM Forms 用に設定されているアプリケーションを選択し、「アプリケーションの OAuth を設定」をタップします。
   1. 上記の手順でコピーした HTTPS URL を「**リダイレクト URL**」ボックスに追加して「**保存**」をクリックします。
   1. Adobe Sign アプリケーションに対して以下の OAuth 設定を有効にして、「**保存**」をクリックします。
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Adobe Sign アプリケーション用に OAuth 設定を構成してキーを取得するための詳しい手順については、開発者用ドキュメントの「[アプリケーション用に OAuth 設定を構成する](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)」を参照してください。

   ![OAuth 設定](assets/oauthconfig_new.png)

1. 「**Adobe Sign 設定を作成**」ページに戻ります。「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL OAuth URL]**」フィールドに以下のデフォルトの URL が表示されます。

   https://secure.na1.echosign.com/public/oauth

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。

   データベースシャードの値を更新することができます。サーバーを再起動すると、データベースシャードの新しい値を使用することができます。

1. Specify the **Client ID** (also referred to as Application ID) and **Client Secret**. 「**添付ファイルにも Adobe Sign を有効にする**」オプションを選択すると、アダプティブフォームに添付されているファイルが、署名用に送信された対応する Adobe Sign ドキュメントに添付されます。

   Tap **[!UICONTROL Connect to Adobe Sign]**. 資格情報の入力画面が表示されたら、Adobe Sign アプリケーションの作成時に使用したユーザー名とパスワードを入力します。

   「**[!UICONTROL 作成]**」をタップして、Adobe Sign 設定を作成します。

1. AEM Web コンソールを開きます。The URL is `https://'[server]:[port]'/system/console/configMgr`
1. **Forms 共通設定サービス**&#x200B;を開きます。
1. In the **Allow** field, **select** All users - All the users, anonymous or logged in, can preview attachments, verify and sign forms, and click **Save.**&#x200B;オーサーインスタンスが Adobe Sign を使用するように設定されます。
1. 対応する発行インスタンスに同じ設定を作成するには [、レプリケーションを使用します](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) 。

これで Adobe Sign が AEM Forms に統合され、アダプティブフォームで使用できるようになりました。To [use Adobe Sign service in an adaptive form](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), specify the configuration container created above in adaptive form properties.



## Adobe Sign スケジューラーを設定して署名ステータスを同期する {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Adobe Sign が有効になっているアダプティブフォームは、すべての署名者がフォームに署名するまで送信されません。Adobe Sign スケジューラーサービスは、デフォルトで、署名者からの応答を 24 時間ごとにチェック（ポーリング）するように設定されています。現在の環境に合わせて、このデフォルト値を変更することができます。次の手順を実行して、デフォルトの間隔を変更します。

1. 管理者の資格情報を使用して AEM Forms サーバーにログインし、**ツール**／**操作**／**Web コンソール**&#x200B;に移動します。

   次のURLをブラウザーウィンドウで開くこともできます。
   `https://[localhost]:'port'/system/console/configMgr`

1. 「**Adobe Sign 設定サービス**」オプションを探して選択します。「[ステータス更新スケジューラーの式](https://en.wikipedia.org/wiki/Cron#CRON_expression)」フィールドで **Cron 式**&#x200B;を指定して「**保存**」をクリックします。例えば、毎日午前0時にConfiguration Serviceを実行するには、「 `0 0 0 1/1 * ? *` ステータス更新スケジューラー式 **** 」フィールドでを指定します。

これで、Adobe Sign のステータスを同期するデフォルトの間隔が変更されました。

## 関連記事 {#related-articles}

* [アダプティブフォームで Adobe Sign を使用する](../../forms/using/working-with-adobe-sign.md)
* [Adobe SignとAEM Formsの併用（ビデオ）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Adobe Sign を AEM Forms に統合する](../../forms/using/adobe-sign-integration-adaptive-forms.md)

