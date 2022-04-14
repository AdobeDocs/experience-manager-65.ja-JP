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
role: User, Admin
feature: Workflow,Asset Management,Renditions
exl-id: 3d9367ed-5a02-43aa-abd9-24fae457d4c5
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: ht
source-wordcount: '1375'
ht-degree: 100%

---

# メタデータ、画像およびビデオを処理するためのプロファイル{#profiles-for-processing-metadata-images-and-videos}

プロファイルとは、フォルダーにアップロードされるアセットに適用するオプションを指定したファイルです。例えば、アップロードするビデオアセットに適用するメタデータプロファイルおよびビデオエンコーディングプロファイルを指定できます。また、画像アセットを適切に切り抜くために画像アセットに適用するイメージプロファイルを指定できます。

ルールには、メタデータの追加、画像のスマート切り抜きまたはビデオエンコーディングプロファイルの構築などが含まれます。Adobe Experience Manager では、3 種類のプロファイルを作成することができ、その詳細は次のリンクで説明されています。

* [メタデータプロファイル](/help/assets/metadata-config.md#metadata-profiles)
* [イメージプロファイル](/help/assets/image-profiles.md)
* [ビデオプロファイル](/help/assets/video-profiles.md)

メタデータプロファイル、イメージプロファイルまたはビデオプロファイルを作成、編集および削除するには、管理者権限が必要です。

メタデータプロファイル、イメージプロファイルまたはビデオプロファイルを作成した後、新規にアップロードするアセットのアップロード先として使用する 1 つ以上のフォルダーにそのプロファイルを割り当てます。

プロファイルがフォルダーに割り当てられることは、Experience Manager Assets でのプロファイルの使用に関する重要な概念です。プロファイル内では、メタデータプロファイルの形式で、ビデオプロファイルまたはイメージプロファイルと共に設定されています。これらの設定は、フォルダーのコンテンツを（そのサブフォルダーコンテンツを含めて）処理します。そのため、ファイルおよびフォルダーの命名方法、サブフォルダーの配置およびこれらのフォルダー内にあるファイルの処理方法は、プロファイルによるこれらのアセットの処理方法に大きな影響を与えます。
ファイルおよびフォルダーの一貫した適切な命名戦略と優れたメタデータプラクティスを使用することで、デジタルアセットコレクションを最大限に活用して、適切なファイルを適切なプロファイルによって処理することができます。

>[!NOTE]
>
>あるフォルダーから別のフォルダーに移動するアセットは再処理されません。例えば、フォルダー 1 にプロファイル A が割り当てられ、フォルダー 2 にプロファイル B が割り当てられているとします。アセットをフォルダー 1 からフォルダー 2 に移動しても、そのアセットには、元の処理がフォルダー 1 から引き継がれます。
>
>同じプロファイルが割り当てられている 2 つのフォルダー間でアセットを移動する場合にも、同じことが言えます。

## フォルダー内のアセットを再処理 {#reprocessing-assets}

>[!NOTE]
>
>Experience Manager 6.4.6.0 以降の *Dynamic Media ー Scene7 mode* にのみ適用されます。

後で変更した既存の処理プロファイルがあるフォルダー内のアセットを再処理できます。

例えば、画像プロファイルを作成してフォルダーに割り当てたとします。フォルダーにアップロードした画像アセットには、画像プロファイルが自動的にアセットに適用されます。ただし、後でプロファイルに新しいスマート切り抜き率を追加することにします。その場合は、もう一度アセットを選択してフォルダーに再度アップロードするのではなく、「*Scene7 : アセットを再処理*」ワークフローを実行するだけです。

処理が初めて失敗したアセットに対して、再処理ワークフローを実行できます。このように、処理プロファイルを編集していなくても、処理プロファイルを適用していなくても、いつでもアセットフォルダーに対して再処理ワークフローを実行することができます。

オプションで、再処理ワークフローのバッチサイズを、デフォルトの 50 アセットから最大 1,000 アセットまで調整できます。フォルダーに対して「_Scene7：アセットを再処理_」ワークフローを実行すると、アセットは一括でグループ化された後、Dynamic Media サーバーに送信されて処理されます。処理の後、バッチセット全体の各アセットのメタデータが Experience Manager 上で更新されます。バッチサイズが大きい場合、処理に遅延が発生することがあります。また、バッチサイズが小さすぎると、Dynamic Media サーバーへのラウンドトリップの数が多くなりすぎるおそれがあります。

詳しくは、[再処理ワークフローのバッチサイズの調整](#adjusting-load)を参照してください。

>[!NOTE]
>
>Dynamic Media Classic から Experience Manager へのアセットの一括移行を実行する場合は、Dynamic Media サーバー上で移行レプリケーションエージェントを有効にする必要があります。移行が完了したら、このエージェントを必ず無効にします。

>
>再処理ワークフローが期待どおりに動作するように、Dynamic Media サーバー上で移行公開エージェントを無効にする必要があります。

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**フォルダー内のアセットを再処理するには：**

1. Experience Manager のアセットページで、処理プロファイルが割り当てられている、「**[!UICONTROL Scene7：アセットを再処理]**」ワークフローの適用対象となるアセットフォルダーに移動します。

   既に処理プロファイルが割り当てられているフォルダーには、カード表示のフォルダー名のすぐ下にプロファイルの名前が表示されます。

1. フォルダーを選択します。

   * 選択したフォルダー内のすべてのファイルがワークフローで再帰的に考慮されます。
   * 選択したメインフォルダー内にアセットを含んだ 1 つ以上のサブフォルダーが存在する場合、ワークフローはフォルダー階層内のあらゆるアセットを再処理します。
   * ベストプラクティスとしては、1,000 個を超えるアセットを含んだフォルダー階層に対しては、このワークフローを実行しないでください。

1. ページの左上隅付近にあるドロップダウンリストで「**[!UICONTROL タイムライン]**」を選択します。
1. ページ左下隅付近の「コメント」フィールドの右側にあるカラットアイコン（**^**）を選択します。

   ![アセット再処理ワークフロー（その 1）](/help/assets/assets/reprocess-assets1.png)

1. 「**[!UICONTROL ワークフローを開始]**」を選択します。
1. 「**[!UICONTROL ワークフローを開始]**」ドロップダウンリストから「**[!UICONTROL Scene7：アセットを再処理]**」を選択します。
1. （オプション）「**ワークフローのタイトルを入力**」テキストフィールドに、ワークフローの名前を入力します。必要に応じて、ワークフローインスタンスを参照する名前を使用できます。

   ![アセット再処理ワークフロー（その 2）](/help/assets/assets/reprocess-assets2.png)

1. 「**[!UICONTROL 開始]**」を選択したあと、「**[!UICONTROL 確認]**」を選択します。

   ワークフローを監視したり、進行状況を確認したりするには、Experience Manager のメインコンソールページで&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**&#x200B;をクリックします。ワークフローインスタンスページで、ワークフローを選択します。メニューバーの「**[!UICONTROL 履歴を開く]**」を選択します。同じワークフローインスタンスページで、選択したワークフローの終了、休止、名前変更を行うこともできます。

### 再処理ワークフローのバッチサイズの調整 {#adjusting-load}

（オプション）再処理ワークフローのデフォルトのバッチサイズは、1 ジョブあたり 50 アセットです。この最適なバッチサイズは、再処理の実行対象となるアセットの平均アセットサイズと MIME タイプによって決まります。値を大きくすると、1 回の再処理ジョブのファイル数が多くなります。したがって、処理バナーが Adobe Experience Manager Assets 上に長時間表示されたままになります。ただし、平均ファイルサイズが小さい（1 MB 以下の）場合は、 Adobe では値を数百個（1000 以下）に増やすことをお勧めしています。平均ファイルサイズが数百 MBなど大きい場合、Adobe はバッチサイズを最大 10 までに減らすことをお勧めしています。

**再処理ワークフローのバッチサイズを調整するには（オプション）**：

1. Experience Manager で、「**[!UICONTROL Adobe Experience Manager]**」を選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**（ハンマー）アイコン／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;を選択します。
1. ワークフローモデルページのカード表示またはリスト表示で、「**[!UICONTROL Scene7：アセットを再処理]**」を選択します。

   ![カード表示で「Scene7：アセットを再処理」ワークフローが選択されたワークフローモデルページ](/help/assets/assets-dm/reprocess-assets7.png)

1. ツールバーの「**[!UICONTROL 編集]**」をクリックします。新しいブラウザータブに、「Scene7：アセットを再処理」ワークフローモデルページが開きます。
1. 「Scene7：アセットを再処理」ワークフローページで、右上隅付近の「**[!UICONTROL 編集]**」を選択して、ワークフローを「ロック解除」します。
1. ワークフローで、Scene7 バッチアップロードコンポーネントを選択してツールバーを開き、ツールバーの「**[!UICONTROL 設定]**」を選択します。

   ![Scene7 バッチアップロードコンポーネント](/help/assets/assets-dm/reprocess-assets8.png)

1. **[!UICONTROL Scene7 へのバッチアップロード ー ステップのプロパティ]**&#x200B;ダイアログボックスで、以下の設定をおこないます。
   * 「**[!UICONTROL タイトル]**」および「**[!UICONTROL 説明]**」テキストフィールドに、必要に応じて、ジョブの新しいタイトルと説明を入力します。
   * ハンドラーが次のステップに進む場合は、「**[!UICONTROL ハンドラー処理の設定]**」を選択します。
   * 「**[!UICONTROL タイムアウト]**」フィールドに、外部プロセスのタイムアウト（秒）を入力します。
   * 「**[!UICONTROL 期間]**」フィールドに、外部プロセスが完了したかどうかを確認するポーリング間隔（秒）を入力します。
   * 「**[!UICONTROL バッチ]**」フィールドに、Dynamic Media サーバーのアップロードジョブのバッチ処理で処理するアセットの最大数（50～1,000）を入力します。
   * タイムアウトに達したときに先に進む場合は、「**[!UICONTROL タイムアウトで先に進む]**」を選択します。タイムアウトに達したときにインボックスまで進む場合は、選択を解除します。

   ![プロパティダイアログボックス](/help/assets/assets-dm/reprocess-assets3.png)

1. **[!UICONTROL Scene7 へのバッチアップロード - ステップのプロパティ]**&#x200B;ダイアログボックスの右上隅にある「**[!UICONTROL 完了]**」を選択します。

1. 「Scene7：アセットを再処理」ワークフローモデルページの右上隅にある「**[!UICONTROL 同期]**」を選択します。「**[!UICONTROL 同期済み]**」と表示された場合、ワークフローランタイムモデルは正常に同期されており、フォルダー内のアセットを再処理する準備が整います。

   ![ワークフローモデルの同期](/help/assets/assets-dm/reprocess-assets1.png)

1. 「Scene7：アセットを再処理」ワークフローモデルを表示しているブラウザータブを閉じます。

<!--1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.-->
