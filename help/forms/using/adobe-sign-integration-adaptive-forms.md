---
title: Adobe Sign の AEM Forms への統合
seo-title: Integrate Adobe Sign with AEM Forms
description: AEM Forms 用に Adobe Sign を設定する方法
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Adobe Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: 51801dfae47e82f31042f48b113332783464bafb
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 45%

---

# 統合 [!DNL Adobe Sign] AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] アダプティブフォームの電子署名ワークフローを有効にします。 電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

標準 [!DNL Adobe Sign] アダプティブフォームのシナリオで、ユーザーがアダプティブフォームに入力する際に、 **サービスを申し込む**. 例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームの入力、送信、署名を行うと、サービスプロバイダーにそのフォームが送信され、追加の処理が実行されます。サービスプロバイダーは受信した申込フォームを確認し、[!DNL Adobe Sign] を使用して申請を承認します。同様の電子署名ワークフローを有効にするには、 [!DNL Adobe Sign] AEM [!DNL Forms].

使用する [!DNL Adobe Sign] AEM [!DNL Forms]，設定 [!DNL Adobe Sign] AEM Cloud Services の場合：

## 前提条件 {#prerequisites}

を統合するには、以下が必要です。 [!DNL Adobe Sign] AEM [!DNL Forms]:

* 有効な [Adobe Sign 開発者アカウント](https://acrobat.adobe.com/jp/ja/why-adobe/developer-form.html)
* [SSL が有効になっている](/help/sites-administering/ssl-by-default.md) AEM サーバー[!DNL Forms]
* [Adobe Sign API アプリケーション](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* [!DNL Adobe Sign] API アプリケーションの資格情報（クライアント ID およびクライアントの秘密鍵）。
* 再設定時に、既存の [!DNL Adobe Sign] オーサーインスタンスとパブリッシュインスタンスの両方からの設定
* オーサーインスタンスとパブリッシュインスタンスには、[同一の暗号キー](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)を使用します。

## 設定 [!DNL Adobe Sign] AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

前提条件を満たしたら、次の手順を実行してを設定します。 [!DNL Adobe Sign] AEM [!DNL Forms] オーサーインスタンスで、以下の操作を実行します。

1. AEM [!DNL Forms] オーサーインスタンス、次に移動 **ツール** ![ハンマー](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定ブラウザー]**.
1. **[!UICONTROL 設定ブラウザー]**&#x200B;ページで「**[!UICONTROL 作成]**」をタップします。
   * 詳しくは、[設定ブラウザー](/help/sites-administering/configurations.md)のドキュメントを参照してください。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログで、設定の&#x200B;**[!UICONTROL タイトル]**&#x200B;を指定し、「**[!UICONTROL クラウド設定]**」を有効にして「**[!UICONTROL 作成]**」をタップします。これにより、クラウドサービス用の設定コンテナが作成されます。
1. に移動します。 **ツール** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** をクリックし、上記の手順で作成した設定コンテナを選択します。

   >[!NOTE]
   >
   >手順 1～4 を実行して、新しい設定コンテナを作成し、 [!DNL Adobe Sign] コンテナ内の設定、または既存の `global` フォルダー内 **ツール** ![ハンマー](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 新しい設定コンテナで設定を作成する場合、必ず **[!UICONTROL 設定コンテナ]** フィールドに値を入力する必要があります。

   >[!NOTE]
   クラウドサービス設定ページの URL が「**HTTPS**」で始まっていることを確認してください。「HTTPS」で始まっていない場合は、AEM サーバーで [SSL を有効](/help/sites-administering/ssl-by-default.md)にしてください。[!DNL Forms]

1. 設定ページで、をタップします。 **[!UICONTROL 作成]** 作成する [!DNL Adobe Sign] AEMでの設定 [!DNL Forms].
1. 内 **[!UICONTROL 一般]** タブ **[!UICONTROL Adobe Sign設定を作成]** ページで、 **[!UICONTROL 名前]** をタップします。 **[!UICONTROL 次へ]**. 必要に応じてタイトルを指定し、設定のサムネイルを参照して選択することもできます。

1. 現在のブラウザーウィンドウの URL をメモ帳にコピーします。設定が必要です。 [!DNL Adobe Sign] AEMを使用したアプリケーション[!DNL Forms].

1. 以下の手順に従って、[!DNL Adobe Sign] アプリケーションの OAuth 設定を指定します。

   1. ブラウザーウィンドウを開き、 [!DNL Adobe Sign] 開発者アカウント。
   1. AEM用に設定されたアプリケーションを選択します [!DNL Forms]をタップし、 **[!UICONTROL アプリの OAuth を設定]**.
   1. を **[!UICONTROL クライアント ID]** および **[!UICONTROL クライアント秘密鍵]** をメモ帳に追加します。
   1. 内 **[!UICONTROL リダイレクト URL]** 」ボックスに、前の手順でコピーした HTTPS URL を追加します。
   1. [!DNL Adobe Sign] アプリケーションに対して以下の OAuth 設定を有効にして、「**[!UICONTROL 保存]**」をクリックします。
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   [!DNL Adobe Sign] アプリケーション用に OAuth 設定を構成してキーを取得するための詳しい手順については、開発者用ドキュメントの[アプリケーション用に OAuth 設定を構成する](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)を参照してください。

   ![OAuth 設定](assets/oauthconfig_new.png)

1. **[!UICONTROL Adobe Sign 設定を作成]**&#x200B;ページに戻ります。内 **[!UICONTROL 設定]** タブ、 **[!UICONTROL OAuth URL]** 「 」フィールドには、デフォルトの URL が記述されます。 URL の形式は次のとおりです。

   `https://<shard>/public/oAuth/v2`

   次に例を示します。
   `https://secure.na1.echosign.com/public/oauth/v2`

   各パラメーターの意味は次のとおりです。

   **na1** は、デフォルトのデータベースシャードを参照します。

   データベースシャードの値を更新することができます。サーバーを再起動すると、データベースシャードの新しい値を使用することができます。

   >[!NOTE]
   オーサーインスタンスとパブリッシュインスタンスの設定が同じシャードを指していることを確認します。 1 つの組織に対して複数のAdobe Sign設定を作成する場合は、すべての設定で同じシャードが使用されていることを確認します。

1. 次を指定： **クライアント ID** （アプリケーション ID とも呼ばれます）および **クライアント秘密鍵** 手順 8 のをコピーします。 「**[!UICONTROL 添付ファイルにも を有効にする]**」オプションを選択すると、アダプティブフォームに添付されているファイルが、署名用に送信された対応する Adobe Sign ドキュメントに添付されます。[!DNL Adobe Sign]

   「**[!UICONTROL Adobe Sign に接続]**」をタップします。資格情報の入力画面が表示されたら、[!DNL Adobe Sign] アプリケーションの作成時に使用したユーザー名とパスワードを入力します。

   「**[!UICONTROL 作成]**」をタップして、[!DNL Adobe Sign] 設定を作成します。

1. AEM Web コンソールを開きます。URL は `https://'[server]:[port]'/system/console/configMgr` です
1. 開く **[!UICONTROL Forms Common Configuration Service].**
1. 内 **[!UICONTROL 許可]** フィールド **選択** すべてのユーザー — 匿名ユーザーまたはログインユーザーは、添付ファイルのプレビュー、フォームの検証と署名を行い、 **[!UICONTROL 保存].** オーサーインスタンスが [!DNL Adobe Sign].
1. 設定を公開します。
1. 用途 [複製](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) 対応するパブリッシュインスタンスで同じ設定を作成する場合。

さて [!DNL Adobe Sign] は、AEMと統合されています [!DNL Forms] アダプティブフォームで使用する準備が整っています。 宛先 [アダプティブフォームでのAdobe Signサービスの使用](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)で、上記でアダプティブフォームのプロパティで作成した設定コンテナを指定します。



## 設定 [!DNL Adobe Sign] スケジューラー：署名ステータスを同期します {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

An [!DNL Adobe Sign] 有効なアダプティブフォームは、すべての署名者が署名プロセスを完了した後にのみ送信されます。 デフォルトでは、 [!DNL Adobe Sign] スケジューラーサービスは、24 時間ごとに署名者の応答を確認（ポーリング）するようにスケジュールされています。 現在の環境に合わせて、このデフォルト値を変更することができます。デフォルトの間隔を変更するには、次の手順を実行します。

1. AEMにログイン [!DNL Forms] 管理者資格情報を持つサーバーにアクセスし、に移動します。 **ツール** > **[!UICONTROL 運用]** > **[!UICONTROL Web コンソール]**.

   また、ブラウザーウィンドウで次の URL を開くこともできます。
   `https://[localhost]:'port'/system/console/configMgr`

1. 「**[!UICONTROL Adobe Sign 設定サービス]**」オプションを探して選択します。「[ステータス更新スケジューラーの式](https://en.wikipedia.org/wiki/Cron#CRON_expression)」フィールドで **[!UICONTROL Cron 式]**&#x200B;を指定して「**[!UICONTROL 保存]**」をクリックします。例えば、毎日午前 0 時に設定サービスを実行するには、次のように指定します。 `0 0 0 1/1 * ? *` 内 **[!UICONTROL ステータス更新スケジューラの式]** フィールドに入力します。

ステータスを同期するデフォルトの間隔 [!DNL Adobe Sign] が変更されました。

## 関連記事 {#related-articles}

* [アダプティブフォームで Adobe Sign を使用する](../../forms/using/working-with-adobe-sign.md)
* [Adobe SignとAEM Formsの連携（ビデオ）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
