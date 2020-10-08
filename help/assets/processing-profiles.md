---
title: メタデータ、画像およびビデオを処理するためのプロファイル
description: プロファイルは、フォルダーにアップロードされたアセットに適用されるオプションに関する一連のルールです。アップロードするビデオアセットに適用するメタデータプロファイルおよびビデオエンコーディングプロファイルを指定します。画像アセットの場合は、適切に切り抜くために画像アセットに適用するイメージプロファイルを指定することもできます。
uuid: 6ded2a2f-a0d3-4f43-af97-02fbc0902c25
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: b555bf0c-44cb-4fbf-abc4-15971663904d
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 87%

---


# メタデータ、画像およびビデオを処理するためのプロファイル{#profiles-for-processing-metadata-images-and-videos}

プロファイルとは、フォルダーにアップロードされるアセットに適用するオプションを指定したファイルです。例えば、アップロードするビデオアセットに適用するメタデータプロファイルおよびビデオエンコーディングプロファイルを指定できます。また、画像アセットを適切に切り抜くために画像アセットに適用するイメージプロファイルを指定できます。

ルールには、メタデータの追加、画像のスマート切り抜きまたはビデオエンコーディングプロファイルの構築などが含まれます。AEM では、3 種類のプロファイルを作成できます。次のリンク先では、それらのプロファイルについて詳しく説明しています。

* [メタデータプロファイル](/help/assets/metadata-profiles.md)
* [イメージプロファイル](/help/assets/image-profiles.md)
* [ビデオプロファイル](/help/assets/video-profiles.md)

メタデータプロファイル、イメージプロファイルまたはビデオプロファイルを作成、編集および削除するには、管理者権限が必要です。

メタデータプロファイル、イメージプロファイルまたはビデオプロファイルを作成した後、新規にアップロードするアセットのアップロード先として使用する 1 つ以上のフォルダーにそのプロファイルを割り当てます。

プロファイルがフォルダーに割り当てられていることは、AEM Assets でのプロファイルの使用に関する重要な概念です。プロファイル内では、メタデータプロファイルの形式で、ビデオプロファイルまたはイメージプロファイルと共に設定されています。これらの設定は、フォルダーのコンテンツを（そのサブフォルダーのコンテンツを含めて）処理します。そのため、ファイルおよびフォルダーの命名方法、サブフォルダーの順序およびこれらのフォルダー内のファイルの処理方法は、プロファイルがこれらのアセットを処理する方法に大きな影響を与えます。適切なメタデータプラクティスと一緒に、一貫性のある適切なファイルおよびフォルダーの命名戦略を使用することで、デジタルアセットコレクションを最大限に活用して、適切なファイルを適切なプロファイルによって処理することができます。

>[!NOTE]
>
>あるフォルダーから別のフォルダーに移動するアセットは再処理されません。例えば、フォルダー 1 にプロファイル A が割り当てられ、フォルダー 2 にプロファイル B が割り当てられているとします。アセットをフォルダー 1 からフォルダー 2 に移動しても、そのアセットには、元の処理がフォルダー 1 から引き継がれます。
>
>同じプロファイルが割り当てられている 2 つのフォルダー間でアセットを移動する場合にも、同じことが言えます。

## フォルダー内のアセットの再処理 {#reprocessing-assets}

>[!NOTE]
>
>ダイ *ナミックメディア —Scene7モード* (AEM 6.4.6.0以降のみ)に適用されます。

後で変更した既存の処理プロファイルがあるフォルダー内のアセットを再処理できます。

例えば、画像プロファイルを作成してフォルダーに割り当てたとします。フォルダーにアップロードした画像アセットには、画像プロファイルが自動的にアセットに適用されます。ただし、後でプロファイルに新しいスマート切り抜き率を追加することにします。その場合は、もう一度アセットを選択してフォルダーに再度アップロードするのではなく、「*Scene7 : アセットを再処理*」ワークフローを実行するだけです。

処理が初めて失敗したアセットに対して、再処理ワークフローを実行できます。したがって、処理プロファイルを編集していない場合や適用していない場合でも、アセットのフォルダーに対していつでも再処理ワークフローを実行できます。

オプションで、再処理ワークフローのバッチサイズを、デフォルトの 50 アセットから最大 1,000 アセットまで調整できます。フォルダーに対して「_Scene7 : アセットを再処理_」ワークフローを実行すると、アセットは一括でグループ化された後、Dynamic Media サーバーに送信されて処理されます。処理の後、バッチセット全体の各アセットのメタデータが AEM 上で更新されます。バッチサイズが非常に大きい場合は、処理に遅延が生じる可能性があります。また、バッチサイズが小さすぎると、Dynamic Media サーバーへのラウンドトリップの数が多くなりすぎるおそれがあります。

詳しくは、[再処理ワークフローのバッチサイズの調整](#adjusting-load)を参照してください。

>[!NOTE]
>
>Dynamic Media Classic から AEM へのアセットの一括移行を実行する場合は、Dynamic Media サーバー上で移行レプリケーションエージェントを有効にする必要があります。移行が完了したら、このエージェントを必ず無効にします。

>
>再処理ワークフローが期待どおりに動作するように、Dynamic Media サーバー上で移行公開エージェントを無効にする必要があります。

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**フォルダー内のアセットを再処理するには**：
1. AEM のアセットページで、処理プロファイルが割り当てられている、「**Scene7 : アセットを再処理**」ワークフローの適用対象となるアセットフォルダーに移動します。

   既に処理プロファイルが割り当てられているフォルダーには、カード表示のフォルダー名のすぐ下にプロファイルの名前が表示されます。

1. フォルダーを選択します。

   * 選択したフォルダー内のすべてのファイルがワークフローで再帰的に考慮されます。
   * 選択したメインフォルダー内にアセットを含んだ 1 つ以上のサブフォルダーが存在する場合、ワークフローはフォルダー階層内のあらゆるアセットを再処理します。
   * ベストプラクティスとしては、1,000 個を超えるアセットを含んだフォルダー階層に対しては、このワークフローを実行しないでください。

1. Near the upper-left corner of the page, from the drop-down list, click **[!UICONTROL Timeline.]**
1. ページ左下隅付近の「コメント」フィールドの右側にあるカラットアイコン（**^**）をクリックします。

   ![アセット再処理ワークフロー（その 1）](/help/assets/assets/reprocess-assets1.png)

1. Click **[!UICONTROL Start Workflow.]**
1. From the **[!UICONTROL Start Workflow]** drop-down list, choose **[!UICONTROL Scene7: Reprocess Assets.]**
1. （オプション）「**ワークフローのタイトルを入力**」テキストフィールドに、ワークフローの名前を入力します。必要に応じて、ワークフローインスタンスを参照する名前を使用できます。

   ![アセット再処理ワークフロー（その 2）](/help/assets/assets/reprocess-assets2.png)

1. Click **[!UICONTROL Start]**, then click **[!UICONTROL Confirm.]**

   ワークフローを監視したり、進行状況を確認したりするには、AEM のメインコンソールページで&#x200B;**[!UICONTROL ツール／ワークフローをクリックします。]**&#x200B;ワークフローインスタンスページで、ワークフローを選択します。メニューバーの「**[!UICONTROL 履歴を開く」をクリックします。]**&#x200B;同じワークフローインスタンスページで、選択したワークフローの終了、休止、名前変更をおこなうこともできます。

### 再処理ワークフローのバッチサイズの調整 {#adjusting-load}

（オプション）再処理ワークフローのデフォルトのバッチサイズは、1 ジョブあたり 50 アセットです。この最適なバッチサイズは、平均アセットサイズと、再処理が実行されるアセットのMIMEタイプによって制御されます。 値を大きくすると、1 回の再処理ジョブのファイル数が多くなります。したがって、処理バナーが AEM Assets 上に長時間表示されたままになります。ただし、平均ファイルサイズが小さい（1 MB 以下の）場合は、値を数百個（1000 以下）に増やすことをお勧めします。平均ファイルサイズが大きい（数百 MB の）場合は、バッチサイズを最大 10 までに減らすことをお勧めします。

**再処理ワークフローのバッチサイズを調整するには（オプション）**：

1. In Experience Manager, click **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then click the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL Workflow > Models.]**
1. On the Workflow Models page, in Card View or List View, select **[!UICONTROL Scene7: Reprocess Assets.]**

   ![カード表示で「Scene7 : アセットを再処理」ワークフローが選択されたワークフローモデルページ](/help/assets/assets-dm/reprocess-assets7.png)

1. ツールバーの「**[!UICONTROL 編集」をクリックします。]**&#x200B;新しいブラウザータブに、「Scene7 : アセットを再処理」ワークフローモデルページが開きます。
1. On the Scene7: Reprocess Assets workflow page, near the upper-right corner, click **[!UICONTROL Edit]** to &quot;unlock&quot; the workflow.
1. In the workflow, select the Scene7 Batch Upload component to open the toolbar, then click **[!UICONTROL Configure]** on the toolbar.

   ![Scene7 バッチアップロードコンポーネント](/help/assets/assets-dm/reprocess-assets8.png)

1. **[!UICONTROL Scene7 へのバッチアップロード - ステップのプロパティ]**&#x200B;ダイアログボックスで、以下の設定をおこないます。
   * 「**[!UICONTROL タイトル]**」および「**[!UICONTROL 説明]**」テキストフィールドに、必要に応じて、ジョブの新しいタイトルと説明を入力します。
   * ハンドラーが次のステップに進む場合は、「**[!UICONTROL ハンドラー処理の設定]**」を選択します。
   * 「**[!UICONTROL タイムアウト]**」フィールドに、外部プロセスのタイムアウト（秒）を入力します。
   * 「**[!UICONTROL 期間]**」フィールドに、外部プロセスが完了したかどうかを確認するポーリング間隔（秒）を入力します。
   * 「**[!UICONTROL バッチ]**」フィールドに、Dynamic Media サーバーのアップロードジョブのバッチ処理で処理するアセットの最大数（50～1,000）を入力します。
   * タイムアウトに達したときに先に進む場合は、「**[!UICONTROL タイムアウトで先に進む]**」を選択します。タイムアウトに達したときにインボックスまで進む場合は、選択を解除します。

   ![プロパティダイアログボックス](/help/assets/assets-dm/reprocess-assets3.png)

1. In the upper-right corner of the **[!UICONTROL Batch Upload to Scene7 – Step Properties]** dialog box, click **[!UICONTROL Done.]**

1. In the upper-right corner of the Scene7: Reprocess Assets workflow model page, click **[!UICONTROL Sync.]**「**[!UICONTROL 同期済み]**」と表示された場合、ワークフローランタイムモデルは正常に同期されており、フォルダー内のアセットを再処理する準備が整います。

   ![ワークフローモデルの同期](/help/assets/assets-dm/reprocess-assets1.png)

1. 「Scene7 : アセットを再処理」ワークフローモデルを表示しているブラウザータブを閉じます。

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, click **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then click the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite.]**
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, click **[!UICONTROL Add.]** The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, click **[!UICONTROL Save All.]**
1. In the upper-left corner of the page, click **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
