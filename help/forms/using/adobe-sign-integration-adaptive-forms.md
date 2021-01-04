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
source-git-commit: 93ee9338fc2e78d01a9b62e8040c4674262ef6be
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 31%

---


# [!DNL Adobe Sign]とAEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}を統合

[!DNL Adobe Sign] アダプティブフォームのe署名ワークフローを有効にします。電子署名を使用すると、法務、販売、給与、人事管理など、さまざまな分野におけるドキュメント処理ワークフローが改善されます。

一般的な[!DNL Adobe Sign]およびアダプティブフォームのシナリオでは、ユーザーはアダプティブフォームに&#x200B;**apply for a service**&#x200B;に入力します。 例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームの入力、送信、署名を行うと、サービスプロバイダーにそのフォームが送信され、追加の処理が実行されます。サービスプロバイダーは申込書をレビューし、[!DNL Adobe Sign]を使用して申込書を承認済みとマークします。 同様の電子署名ワークフローを有効にするには、[!DNL Adobe Sign]をAEM [!DNL Forms]と統合します。

AEM [!DNL Forms]で[!DNL Adobe Sign]を使用するには、AEMクラウドサービスで[!DNL Adobe Sign]を設定します。

## 前提条件 {#prerequisites}

[!DNL Adobe Sign]をAEM [!DNL Forms]と統合するには、次が必要です。

* 有効な [Adobe Sign 開発者アカウント](https://acrobat.adobe.com/jp/ja/why-adobe/developer-form.html)
* [SSL が有効になっている](/help/sites-administering/ssl-by-default.md) AEM サーバー[!DNL Forms]
* [Adobe Sign API アプリケーション](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* [!DNL Adobe Sign] APIアプリケーションの資格情報（クライアントIDとクライアントシークレット）。
* 再設定時に、既存の[!DNL Adobe Sign]設定を作成者インスタンスと発行インスタンスの両方から削除します。
* 作成者インスタンスとパブリッシュインスタンスには、[同一の暗号キー](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)を使用します。

## AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}で[!DNL Adobe Sign]を設定

前提条件を満たしたら、次の手順を実行して、作成者インスタンスでAEM [!DNL Forms]を使用して[!DNL Adobe Sign]を設定します。

1. AEM [!DNL Forms]作成者インスタンスで、**ツール** ![ハンマー](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定ブラウザー]**&#x200B;に移動します。
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで、**[!UICONTROL 作成]**&#x200B;をタップします。
   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定に&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、**[!UICONTROL クラウド設定]**&#x200B;を有効にして、**[!UICONTROL 作成]**&#x200B;をタップします。 これにより、クラウドサービス用の設定コンテナが作成されます。
1. **ツール** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**&#x200B;に移動し、上記の手順で作成した設定コンテナを選択します。

   >[!NOTE]
   >
   >手順1 ～ 4を実行して新しい設定コンテナを作成し、コンテナに[!DNL Adobe Sign]設定を作成するか、**ツール** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**&#x200B;の既存の`global`フォルダを使用します。 新しい設定コンテナで設定を作成する場合は、アダプティブフォームを作成する際に、**[!UICONTROL 設定コンテナ]**&#x200B;フィールドにコンテナ名を必ず指定してください。

   >[!NOTE]
   クラウドサービス設定ページの URL が「**HTTPS**」で始まっていることを確認してください。「HTTPS」で始まっていない場合は、AEM サーバーで [SSL を有効](/help/sites-administering/ssl-by-default.md)にしてください。[!DNL Forms]

1. 設定ページで、「**[!UICONTROL 作成]**」をタップしてAEM [!DNL Forms]に[!DNL Adobe Sign]設定を作成します。
1. **[!UICONTROL Adobe Sign構成を作成]**&#x200B;ページの「**[!UICONTROL 一般]**」タブで、設定の&#x200B;**[!UICONTROL 名前]**&#x200B;を指定し、「**[!UICONTROL 次へ]**」をタップします。 必要に応じてタイトルを指定し、設定のサムネイルを参照して選択することもできます。

1. 現在のブラウザーウィンドウのURLをメモ帳にコピーします。 AEM[!DNL Forms]で[!DNL Adobe Sign]アプリケーションを構成する必要があります。

1. [!DNL Adobe Sign]アプリケーションのOAuth設定を構成します。

   1. ブラウザーウィンドウを開き、[!DNL Adobe Sign]デベロッパーアカウントにサインインします。
   1. AEM [!DNL Forms]用に設定されたアプリケーションを選択し、「**[!UICONTROL Configure OAuth for Application]**」をタップします。
   1. **[!UICONTROL クライアントID]**&#x200B;と&#x200B;**[!UICONTROL クライアントシークレット]**&#x200B;をメモ帳にコピーします。
   1. 「**[!UICONTROL リダイレクトURL]**」ボックスに、前の手順でコピーしたHTTPS URLを追加します。
   1. [!DNL Adobe Sign]アプリケーションの次のOAuth設定を有効にし、「**[!UICONTROL 保存]**」をクリックします。
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   [!DNL Adobe Sign]アプリケーションのOAuth設定を構成し、キーを取得する手順については、[アプリケーション](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)開発者向けドキュメントのoAuth設定を構成するを参照してください。

   ![OAuth 設定](assets/oauthconfig_new.png)

1. 「**[!UICONTROL Adobe Sign 設定を作成]**」ページに戻ります。「**[!UICONTROL 設定]**」タブで、「**[!UICONTROL OAuth URL]**」フィールドに以下のデフォルトの URL が表示されます。

   https://secure.na1.echosign.com/public/oauth

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。

   データベースシャードの値を更新することができます。サーバーを再起動すると、データベースシャードの新しい値を使用することができます。

1. 手順8でコピーした&#x200B;**クライアントID**(アプリケーション IDとも呼ばれます)と&#x200B;**クライアントシークレット**&#x200B;を指定します。 「**[!UICONTROL 添付ファイルにも を有効にする]**」オプションを選択すると、アダプティブフォームに添付されているファイルが、署名用に送信された対応する Adobe Sign ドキュメントに添付されます。[!DNL Adobe Sign]

   「**[!UICONTROL Adobe Signに接続]**」をタップします。 資格情報の入力を求められたら、[!DNL Adobe Sign]アプリケーションの作成時に使用するアカウントのユーザー名とパスワードを入力します。

   「**[!UICONTROL 作成]**」をタップして[!DNL Adobe Sign]設定を作成します。

1. AEM Web コンソールを開きます。URLは`https://'[server]:[port]'/system/console/configMgr`です
1. **[!UICONTROL Forms共通構成サービス]を開きます。**
1. 「**[!UICONTROL 許可]**」フィールドで、「**すべてのユーザーを選択 — 匿名ユーザーまたはログインユーザーは、添付ファイルをプレビューでき、フォームを検証して署名できます。**[!UICONTROL &#x200B;保存]」をクリックします。**** 作成者インスタンスは、を使用するように設定されてい [!DNL Adobe Sign]ます。
1. 設定を公開します。
1. [複製](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html)を使用して、対応する発行インスタンスに同じ設定を作成します。

これで、[!DNL Adobe Sign]はAEM [!DNL Forms]と統合され、アダプティブフォームで使用できる状態になりました。 [アダプティブフォーム](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)でAdobe Signサービスを使用するには、上記で作成した設定コンテナをアダプティブフォームのプロパティで指定します。



## [!DNL Adobe Sign]スケジューラーを構成して署名ステータス{#configure-adobe-sign-scheduler-to-sync-the-signing-status}を同期します

[!DNL Adobe Sign]が有効なアダプティブフォームは、すべての署名者が署名プロセスを完了した後でのみ送信されます。 デフォルトでは、[!DNL Adobe Sign]スケジューラーサービスは、24時間ごとに署名者の応答を確認（ポーリング）するようにスケジュールされています。 現在の環境に合わせて、このデフォルト値を変更することができます。次の手順を実行して、デフォルトの間隔を変更します。

1. 管理者の資格情報を使用してAEM [!DNL Forms]サーバーにログインし、**ツール**/**[!UICONTROL 操作]**/**[!UICONTROL Webコンソール]**&#x200B;に移動します。

   次のURLをブラウザーウィンドウで開くこともできます。
   `https://[localhost]:'port'/system/console/configMgr`

1. 「**[!UICONTROL Adobe Sign 設定サービス]**」オプションを探して選択します。「[ステータス更新スケジューラーの式](https://en.wikipedia.org/wiki/Cron#CRON_expression)」フィールドで **[!UICONTROL Cron 式]**&#x200B;を指定して「**[!UICONTROL 保存]**」をクリックします。例えば、毎日午前0時にConfiguration Serviceを実行するには、**[!UICONTROL Status Updateスケジューラー式]**&#x200B;フィールドで`0 0 0 1/1 * ? *`を指定します。

[!DNL Adobe Sign]の状態を同期するデフォルトの間隔が変更されました。

## 関連記事 {#related-articles}

* [アダプティブフォームで Adobe Sign を使用する](../../forms/using/working-with-adobe-sign.md)
* [Adobe SignとAEM Formsの併用（ビデオ）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Adobe Sign を AEM Forms に統合する](../../forms/using/adobe-sign-integration-adaptive-forms.md)

