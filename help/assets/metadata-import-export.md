---
title: アセットメタデータの一括読み込みおよび書き出し.
description: デジタルアセットのメタデータの一括読み込みと書き出し。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2fd9a32396152eaf46e69c3141cbe1b6a69a3891

---


# アセットメタデータの一括読み込みおよび書き出し {#import-and-export-asset-metadata-in-bulk}

[!DNL Adobe Experience Manager Assets] では、CSV ファイルを使用して、アセットのメタデータを一括で読み込むことができます。CSV ファイルを読み込むことで、最近アップロードされたアセットや既存のアセットの一括更新をおこなうことができます。また、サードパーティシステムから CSV 形式でアセットメタデータを一括で取り込むこともできます。

## メタデータの読み込み {#import-metadata}

メタデータの読み込みは非同期であり、システムのパフォーマンスに影響はありません。ワークフロー実行フラグがチェックされている場合、XMP 書き戻しアクティビティが発生するので、複数のアセットのメタデータを同時に更新すると、リソースが集中的に使用されるおそれがあります。このような読み込みは、他のユーザーのパフォーマンスに影響しないように、サーバー使用率が低いときに計画します。

>[!NOTE]
>
>カスタム名前空間にメタデータを読み込むには、まず、その名前空間を登録します。

1. Navigate to the [!DNL Assets] user interface, and click **[!UICONTROL Create]** from the toolbar.
1. メニューから「**[!UICONTROL メタデータ]**」を選択します。
1. In the **[!UICONTROL Metadata Import]** page, click **[!UICONTROL Select File]**. メタデータが入った CSV ファイルを選択します。
1. 以下のパラメーターを指定します。

   | メタデータ読み込みパラメーター | 説明 |
   |:---|:---|
   | [!UICONTROL バッチサイズ] | メタデータを読み込むバッチ内のアセット数。デフォルト値は 50 です。最大値は 100 です。 |
   | [!UICONTROL フィールドセパレーター] | デフォルト値は `,`（コンマ）です。他の文字も指定できます。 |
   | [!UICONTROL 複数の値の区切り文字] | メタデータ値のセパレーター。デフォルト値は `|` です。 |
   | [!UICONTROL ワークフローを開始] | デフォルトでは false です。When set to `true` and default Launcher settings are in effect for the [!UICONTROL DAM Metadata WriteBack] workflow (that writes metadata to the binary XMP data). 「ワークフローを開始」を有効にすると、システムの反応が遅くなります。 |
   | [!UICONTROL アセットパス列名] | アセットが含まれている、CSV ファイルの列名を定義します。 |

1. ツールバーの「**[!UICONTROL 読み込み]**」をタップまたはクリックします。After the metadata is imported, a notification is sent to your [!UICONTROL Notification] inbox. アセットのプロパティページに移動し、メタデータ値がアセットに正常に読み込まれたかどうかを確認します。

メタデータの読み込み時に日付とタイムスタンプを追加するには、日付と時刻の `YYYY-MM-DDThh:mm:ss.fff-00:00` 形式を使用します。 日付と時刻は、で区切ら `T`れます。 `hh` は24時間形式の時間、 `fff` はナノ秒、 `-00:00` はタイムゾーンオフセットです。 例えば、2020年3月26日 `2020-03-26T11:26:00.000-07:00` の午前11:26:00.000 PST時などです。

>[!CAUTION]
>
>日付形式が一致しない場合 `YYYY-MM-DDThh:mm:ss.fff-00:00`、日付値は設定されません。 書き出されたメタデータCSVファイルの日付形式は、形式になり `YYYY-MM-DDThh:mm:ss-00:00`ます。 読み込む場合は、で示すナノ秒値を追加して、有効な形式に変換し `fff`ます。

## メタデータの書き出し {#export-metadata}

CSV形式で複数のアセットのメタデータを書き出すことができます。 メタデータは非同期的に書き出され、システムのパフォーマンスに影響を及ぼしません。To export metadata, [!DNL Experience Manager] traverses through the properties of the asset node `jcr:content/metadata` and its child nodes and exports the metadata properties in a CSV file.

メタデータの一括書き出しの使用例は次のとおりです。

* アセットの移行時にサードパーティシステムにメタデータを読み込む。
* より広範なプロジェクトチームとアセットメタデータを共有する。
* メタデータをテストまたは監査してコンプライアンスを確保する。
* メタデータを外部化して個別にローカライズできるようにする。

1. メタデータを書き出すアセットを含んだアセットフォルダーを選択します。ツールバーの「**[!UICONTROL メタデータを書き出し]**」を選択します。

1. In the [!UICONTROL Metadata Export] dialog, specify a name for the CSV file. サブフォルダー内のアセットのメタデータを書き出すには、「**[!UICONTROL サブフォルダーのアセットを含める]**」を選択します。

   ![フォルダー内のすべてのアセットのメタデータを書き出すためのインターフェイスとオプション](assets/export_metadata_page.png "フォルダー内のすべてのアセットのメタデータを書き出すためのインターフェイスとオプション")

1. 目的のオプションを選択します。ファイル名を指定し、必要に応じて日付を指定します。

1. 「**[!UICONTROL 書き出すプロパティ]**」フィールドで、すべてのプロパティを書き出すか、特定のプロパティを書き出すかを指定します。書き出すプロパティを選択する場合は、目的のプロパティを追加します。

1. From the toolbar, click **[!UICONTROL Export]**. メタデータが書き出されることを確認するメッセージが表示されます。メッセージを閉じます。

1. 書き出しジョブのインボックス通知を開きます。ジョブを選択し、ツールバーの「**[!UICONTROL 開く]**」をクリックします。To download the CSV file with the metadata, click **[!UICONTROL CSV Download]** from the toolbar. 「**[!UICONTROL 閉じる]**」をクリックします。

   ![一括で書き出したメタデータを格納した CSV ファイルをダウンロードするためのダイアログ](assets/csv_download.png)

   *図：一括で書き出したメタデータを格納した CSV ファイルをダウンロードするためのダイアログ.*

>[!MORELIKETHIS]
>
>* [Experience Manager Assetsでのメタデータの読み込みと書き出し](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)

