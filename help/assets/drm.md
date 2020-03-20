---
title: アセットのデジタル著作権管理
description: AEM でライセンスされているアセットの状態と有効期限の情報を管理する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# Digital Rights Management for digital assets {#digital-rights-management-in-assets}

多くの場合、デジタルアセットはライセンスに関連付けられています。ライセンスは、利用条件とその期間を指定します。Adobe Experience Manager(AEM)AssetsはAEMプラットフォームと完全に統合されているので、アセットの有効期限情報とアセットの状態を効率的に管理できます。 ライセンス情報をアセットに関連付けることもできます。

## アセットの有効期限 {#asset-expiration}

アセットの有効期限は、アセットのライセンス要件を徹底する有効な方法です。公開済みアセットの有効期限が切れたらアセットを非公開にすることで、ライセンス違反が発生する可能性を回避します。管理者権限のないユーザーは、有効期限切れのアセットを編集、コピー、移動、公開、ダウンロードできません。

アセットの有効期限ステータスは、カード表示とリスト表示の両方のアセットコンソールで表示できます。

![expired_flag_card](assets/expired_flag_card.png)

*図：カード表示では、カード上のフラグは期限切れのアセットを示します*

**リスト表示**

![expired_flag_list](assets/expired_flag_list.png)

*図：リスト表示では、「[!UICONTROL Status]」列に「[!UICONTROL Expired]」バナーが表示されます。*

タイムラインで、アセットの有効期限切れのステータスを確認できます。アセットを選択してグローバルナビゲーションメニューから「タイムライン」を選択します。

![chlimage_1-144](assets/chlimage_1-144.png)

You can also view the expiration status of assets in the **[!UICONTROL References]** rail. アセットの有効期限のステータスと、複合アセットと、参照されるサブアセット、コレクション、プロジェクトとの関係を管理します。

1. 参照元の Web ページと複合アセットを表示するアセットに移動します。
1. アセットとExperience Managerのロゴを選択します。

1. Choose **[!UICONTROL References]** from the menu.

   ![chlimage_1-146](assets/chlimage_1-146.png)

   For expired assets, the References rail displays the expiry status **[!UICONTROL Asset is Expired]** at the top.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   If the asset has expired subassets, the References rail displays the status **[!UICONTROL Asset has Expired Sub-Assets]**.

   ![chlimage_1-148](assets/chlimage_1-148.png)

### 有効期限切れのアセットの検索 {#search-expired-assets}

検索パネルで、有効期限切れのアセット（有効期限切れのサブアセットを含む）を検索できます。

1. In the Assets console, click the **[!UICONTROL Search]** in the toolbar to display the Omnisearch box.

1. 「Omnisearch」ボックスにカーソルを置き、Returnキーを押して、検索結果ページを表示します。

   ![chlimage_1-150](assets/chlimage_1-150.png)

1. 「Experience Managerロゴ」をクリックして検索パネルを表示します。

   ![chlimage_1-151](assets/chlimage_1-151.png)

1. 「**[!UICONTROL 有効期限ステータス]**」オプションをクリックまたはタップしてそれを展開します。

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 「**[!UICONTROL 期限切れ]**」を選択します。有効期限切れのアセットが検索結果に表示されます。

   ![chlimage_1-153](assets/chlimage_1-153.png)

When you choose the **Expired** option, the Assets console only displays the expired assets and subassets that are referenced by compound assets. 有効期限切れのサブアセットを参照する複合アセットは、サブアセットの有効期限切れの直後には表示されません。代わりに、それらは次回スケジューラーが実行され、有効期限切れのサブアセットを参照していることを AEM Assets が検出した後に表示されます。

公開済みアセットの有効期限をスケジューラーの現在のサイクルより前の日付に変更する場合、スケジューラーは次回の実行時にも引き続きこのアセットを有効期限切れのアセットとして検出し、ステータスにそれを反映させます。

さらに、何らかの誤作動やエラーによりスケジューラーが現在のサイクルの有効期限切れアセットを検出できない場合、スケジューラーはこれらのアセットを次回のサイクルで再確認し、有効期限切れのステータスを検出します。

アセットコンソールに有効期限切れのサブアセットとともに参照元の複合アセットを表示するには、AEM Configuration Manager で **Adobe CQ DAM Expiry Notification** ワークフローを設定します。

1. AEM Configuration Manager を開きます。
1. Choose **[!UICONTROL Adobe CQ DAM Expiry Notification]**. By default, **[!UICONTROL Time based Scheduler]** is selected, which schedules a job to check at a specific time whether an asset has expired subassets. ジョブが完了すると、期限切れのサブアセットと参照アセットを含むアセットが、検索結果に期限切れとして表示されます。

   ![chlimage_1-154](assets/chlimage_1-154.png)

1. ジョブを定期的に実行するには、「**[!UICONTROL 時間ベースのスケジューラールール]**」フィールドをクリアして、「**[!UICONTROL 定期的なスケジューラー]**」フィールドの時間（秒数）を変更します。例えば、式「0 0 0 &amp;ast; &amp;ast; ?」の場合、ジョブが 00 時間でトリガーされます。
1. Select **[!UICONTROL send email]** to receive emails when an asset expires.

   >[!NOTE]
   >
   >アセットの有効期限が切れると、アセットの作成者（AEM Assets に特定のアセットをアップロードしたユーザー）のみが電子メールを受け取ります。AEM の全レベルの電子メール通知の設定に関する追加情報について詳しくは、[電子メール通知の設定](/help/sites-administering/notification.md)を参照してください。

1. 「**[!UICONTROL Prior notification in seconds]**」フィールドで、アセットの有効期限が切れる何秒前に有効期限切れに関する通知を受け取るかを指定します。管理者かアセットの作成者の場合、アセットの有効期限が切れる前に、指定の時間が経過した後にアセットの有効期限が切れることを知らせるメッセージを受け取ります。

   アセットの有効期限が切れると、有効期限が切れたことを知らせる別の通知を受け取ります。さらに、有効期限切れのアセットはアクティベートが解除されます。

1. 「**[!UICONTROL 保存]**」をクリックします。

## アセットの状態 {#asset-states}

Adobe Experience Manager（AEM）Assets のアセットコンソールには、アセットの様々な状態が表示されます。特定のアセットの現在の状態により、カード表示にその状態について記述されたラベル（期限切れ、公開済み、承認済み、却下など）が表示されます。

1. Assets ユーザーインターフェイスでアセットを選択します。

   ![chlimage_1-155](assets/chlimage_1-155.png)

1. ツールバー **[!UICONTROL から]** 「公開」をタップします。 ツールバーに「公開」が表示されな **い場合は** 、ツールバーの「その他」をタ **[!UICONTROL ップし]** 、「公開」オプション **** を見つけます。

   ![chlimage_1-156](assets/chlimage_1-156.png)

1. Choose **[!UICONTROL Publish]** from the menu, and then close the confirmation dialog.
1. 選択モードを終了します。アセットの公開ステータスは、カード表示のアセットのサムネールの下部に表示されます。リスト表示では、「公開」列にアセットが公開された時間が表示されます。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. In the Assets UI, select an asset and tap **[!UICONTROL Properties]** to display its asset details page.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. In the Advanced tab, set an expiration date for the asset from the **[!UICONTROL Expires]** field.

   ![有効期限フィールドにアセットの有効期限の日時を設定します。](assets/asset-properties-advanced-tab.png)


   *図：アセットの有効期限を設定するためのアセットプロパティの「詳細」タブ*

1. Click **[!UICONTROL Save]** and then click **[!UICONTROL Close]** to display the Asset console.
1. アセットの公開ステータスは、カード表示のアセットのサムネールの下部に、有効期限切れのステータスを示します。In the list view, the status of the asset is displayed as **[!UICONTROL Expired]**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. アセットコンソールで、フォルダーを選択してフォルダーにレビュータスクを作成します。
1. Review and approve/reject the assets in the review task and click **[!UICONTROL Complete]**.
1. レビュータスクを作成するフォルダーに移動します。承認または却下したアセットのステータスがカード表示の下部に表示されます。リスト表示では、承認と有効期限のステータスが適切な列に表示されます。

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. ステータスに基づいてアセットを検索するには、「検索」を **[!UICONTROL タップし]** 、Omnisearchバーを表示します。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Returnキーを押し、GlobalNavをタッ **[!UICONTROL プして]** 、検索パネルを表示します。
1. 検索パネルで、「**[!UICONTROL 公開ステータス]**」をタップまたはクリックして「**[!UICONTROL 公開済み]**」を選択し、AEM Assets で公開済みのアセットを検索します。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 「**[!UICONTROL 承認ステータス]**」をタップまたはクリックし、適切なアイコンをクリックして承認済みまたは却下されたアセットを検索します。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 有効期限切れのステータスに基づいてアセットを検索するには、検索パネルで「**[!UICONTROL 有効期限ステータス]**」を選択して適切なオプションを選択します。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 各種検索ファセットで、ステータスの組み合わせに基づいてアセットを検索することもできます。検索ファセットで適切なオプションを選択することで、例えば、レビュータスクで承認されており、まだ有効期限が切れていない公開済みのアセットを検索することもできます。

   ![chlimage_1-166](assets/chlimage_1-166.png)

## アセットのデジタル著作権管理 {#digital-rights-management-in-assets-1}

この機能は、Adobe Experience Manager（AEM）アセットからライセンスの必要なアセットをダウンロードする前に、使用許諾契約書への同意をリクエストするものです。

If you select a protected asset and tap **[!UICONTROL Download]**, you are redirected to a license page where you accept the license agreement. 使用許諾契約書に同意しない場合、「**[!UICONTROL ダウンロード]**」ボタンは無効になります。

選択した項目に保護されたアセットが複数含まれている場合、一度に 1 つずつアセットを選択し、使用許諾契約書に同意し、アセットのダウンロードに進みます。

アセットは、次のいずれかの条件が満たされた場合に保護されていると見なされます。

* アセットのメタデータプロパティ `xmpRights:WebStatement` が、そのアセットの使用許諾契約書を含む CQ ページのパスを指している。
* アセットのメタデータプロパティ `adobe_dam:restrictions` の値が、使用許諾契約書を指定する生の HTML である。

>[!NOTE]
>
>The location `/etc/dam/drm/licenses` used for storing licenses in earlier releases of AEM is deprecated.
>
>If you create or modify licence pages, or port them from previous AEM releases, Adobe recommends that you store them under `/apps/settings/dam/drm/licenses` or `/conf/&ast;/settings/dam/drm/licenses`.

### DRM保護アセットのダウンロード {#downloading-drm-assets}

1. In the Card view, select the assets you want to download and click **[!UICONTROL Download]**.
1. **[!UICONTROL 著作権管理]**&#x200B;ページで、ダウンロードするアセットをリストから選択します。
1. In the License pane, choose **[!UICONTROL Agree]**. A tick mark appears beside the asset for which you accept the license agreement. Tap/click the **[!UICONTROL Download]** button.

   >[!NOTE]
   >
   >「**[!UICONTROL ダウンロード]**」ボタンは、保護されたアセットの使用許諾契約に同意した場合にのみ有効になります。ただし、選択範囲が保護されたアセットと保護されていないアセットの両方で構成されている場合は、保護されたアセットのみが左パネルに表示され、「**[!UICONTROL ダウンロード]**」ボタンが有効になって保護されていないアセットをダウンロードのダウンロードが可能になります。保護された複数のアセットの使用許諾契約に同時に承諾するには、リストからアセットを選択して「**[!UICONTROL 同意する]**」を選択します。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. In the dialog, tap/click **[!UICONTROL Download]** to download the asset or its renditions.
