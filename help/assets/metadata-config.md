---
title: メタデータ機能の設定と管理。
description: メタデータの追加と管理に関連した  [!DNL Experience Manager Assets]  機能の設定と管理。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 100%

---

# [!DNL Assets] でのメタデータ機能の設定と管理  {#config-metadata}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=ja) |
| AEM 6.5 | この記事 |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, and so on, operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] では、あらゆるアセットのメタデータを保持します。したがって、アセットの分類と編成が容易にでき、特定のアセットを検索しやすくなります。メタデータをアセットと共に保持して管理する機能により、メタデータに基づいてアセットを自動的に整理および処理できます。[!DNL Adobe Experience Manager Assets] を使用すると、管理者は、メタデータ機能を設定およびカスタマイズして、デフォルトのアドビ製品／サービスを変更できます。

## メタデータスキーマの編集 {#metadata-schema}

詳しくは、[メタデータスキーマフォームの編集](metadata-schemas.md#edit-metadata-schema-forms)を参照してください。

## [!DNL Experience Manager] 内でのカスタム名前空間の登録 {#registering-a-custom-namespace-within-aem}

[!DNL Experience Manager] 内で独自の名前空間を追加できます。`cq`、`jcr`、`sling` などの事前定義された名前空間があるのと同じように、リポジトリメタデータおよび XML 処理用の名前空間を設定できます。

1. ノードタイプ管理ページ（`https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`）にアクセスします。
1. 名前空間管理ページにアクセスするには、ページ上部の「**[!UICONTROL 名前空間]**」をクリックします。
1. 名前空間を追加するには、ページ下部の「**[!UICONTROL 新規]**」をクリックします。
1. XML 名前空間規則に従って、カスタム名前空間を指定します。URI およびその ID に関連付けられたプレフィックスの形式で ID を指定します。「**[!UICONTROL 保存]**」をクリックします。

## バルクメタデータ更新の制限の設定 {#bulk-metadata-update-limit}

サービス拒否（DoS）などの状況を防ぐために、[!DNL Enterprise Manager] では、Sling リクエストでサポートされるパラメーターの数を制限しています。一度に多くのアセットのメタデータを更新すると、上限に到達する可能性があり、それ以上のアセットでメタデータが更新されなくなります。Enterprise Manager は、ログに次の警告を生成します。

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

制限を変更するには、**[!UICONTROL ツール]**／**[!UICONTROL 操作]**／**[!UICONTROL Web コンソール]**&#x200B;にアクセスし、**[!UICONTROL Apache Sling Request Parameter Handling]** OSGi 設定で **[!UICONTROL Maximum POST Parameters]** の値を変更します。

## メタデータプロファイル {#metadata-profiles}

メタデータプロファイルを使用すると、フォルダー内のアセットにデフォルトのメタデータを適用できます。メタデータプロファイルを作成し、フォルダーに適用します。それ以降にそのフォルダーにアップロードするすべてのアセットには、メタデータプロファイルで設定したデフォルトのメタデータが継承されます。

### メタデータプロファイルの追加 {#adding-a-metadata-profile}

1. **[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL メタデータプロファイル]**&#x200B;に移動し、「**[!UICONTROL 作成]**」をクリックします。
1. プロファイルのタイトル（例：`Sample Metadata`）を入力して、「**[!UICONTROL 作成]**」をクリックします。メタデータプロファイルの「[!UICONTROL フォームを編集]」が表示されます。

   ![メタデータフォームの編集](assets/metadata-edit-form.png)

1. コンポーネントをクリックし、「**[!UICONTROL 設定]**」タブでプロパティを設定します。例えば、「**[!UICONTROL 説明]**」コンポーネントをクリックして、そのプロパティを編集します。

   ![メタデータプロファイルでのコンポーネントの設定](assets/metadata-profile-component-setting.png)

   **[!UICONTROL 説明]**&#x200B;コンポーネントについて、次のプロパティを編集します。

   * **[!UICONTROL フィールドラベル]**：メタデータプロパティの表示名。ユーザーの参照用です。

   * **[!UICONTROL プロパティにマッピング]**：このプロパティの値は、リポジトリに保存されているアセットノードへの相対パスまたは名前を提供します。この値は、パスがアセットのノードの下にあることを示すので、常に「`./`」から開始する必要があります。

   ![メタデータプロファイルのプロパティ設定へのマッピング](assets/metadata-profile-setting-map-property.png)

   「**[!UICONTROL プロパティにマッピング]**」に指定する値は、アセットのメタデータノードの下のプロパティとして格納されます。例えば、「**[!UICONTROL プロパティにマッピング]**」の名前として `./jcr:content/metadata/dc:desc` を指定すると、[!DNL Assets] は、アセットのメタデータノードに値 `dc:desc` を格納します。メタデータスキーマの特定のプロパティに 1 つのフィールドのみをマッピングすることをお勧めします。それ以外の場合は、プロパティにマッピングされた、最後に追加されたフィールドが、システムによって選択されます。

   * **[!UICONTROL デフォルト値]**：メタデータコンポーネントのデフォルト値を追加するには、このプロパティを使用します。例えば、「My description」と指定すると、この値がアセットのメタデータノードにあるプロパティ `dc:desc` に割り当てられます。

   ![メタデータプロファイルへのデフォルトの説明の設定](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >（`/jcr:content/metadata` ノードに存在していない）新しいメタデータプロパティにデフォルト値を追加しても、プロパティとその値は、アセットの[!UICONTROL プロパティ]ページにデフォルトでは表示されません。アセットの[!UICONTROL プロパティ]ページに新しいプロパティを表示するには、対応するスキーマフォームを変更します。

1. （オプション）「**[!UICONTROL フォームを作成]**」タブで、その他のコンポーネントを[!UICONTROL フォームを編集]に追加して、「**[!UICONTROL 設定]**」タブでそのプロパティを設定します。「**[!UICONTROL フォームを作成]**」タブでは、次のプロパティを使用できます。

| コンポーネント | プロパティ |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL セクションヘッダー] | フィールドラベル、<br> 説明 |
| [!UICONTROL 1 行のテキスト] | フィールドラベル、<br> プロパティにマッピング、<br> デフォルト値 |
| [!UICONTROL 複数値テキスト] | フィールドラベル、<br> プロパティにマッピング、<br> デフォルト値 |
| [!UICONTROL 数値] | フィールドラベル、<br> プロパティにマッピング、<br> デフォルト値 |
| [!UICONTROL 日付] | フィールドラベル、<br> プロパティにマッピング、<br> デフォルト値 |
| [!UICONTROL 標準タグ] | フィールドラベル、<br> プロパティにマッピング、<br> デフォルト値、<br> 説明 |

1. 「**[!UICONTROL 完了]**」をクリックします。メタデータプロファイルが、**[!UICONTROL メタデータプロファイル]**&#x200B;ページのプロファイルのリストに追加されます。<br>

   ![メタデータプロファイルページに追加されたメタデータプロファイル](assets/MetadataProfiles-page.png)

### メタデータプロファイルのコピー {#copying-a-metadata-profile}

1. **[!UICONTROL メタデータプロファイル]**&#x200B;ページで、コピーを作成するメタデータプロファイルを選択します。

   ![メタデータプロファイルのコピー](assets/metadata-profile-edit-copy-option.png)

1. ツールバーの「**[!UICONTROL コピー]**」をクリックします。
1. **[!UICONTROL メタデータプロファイルをコピー]**&#x200B;ダイアログで、メタデータプロファイルの新しいコピーのタイトルを入力します。
1. 「**[!UICONTROL コピー]**」をクリックします。メタデータプロファイルのコピーが、**[!UICONTROL メタデータプロファイル]**&#x200B;ページのプロファイルのリストに表示されます。

   ![メタデータプロファイルページに追加されたメタデータプロファイルのコピー](assets/copy-metadata-profile.png)

### メタデータプロファイルの削除 {#deleting-a-metadata-profile}

1. **[!UICONTROL メタデータプロファイル]**&#x200B;ページで、削除するプロファイルを選択します。

1. ツールバーの「**[!UICONTROL メタデータプロファイルを削除]**」をクリックします。
1. ダイアログで、「**[!UICONTROL 削除]**」をクリックして、削除操作を確定します。メタデータプロファイルがリストから削除されます。

<!-- TBD: Revisit to find out the correct config. and update these steps. When fixed, also o
These steps have been carried forward from old AEM versions. See https://helpx.adobe.com/experience-manager/6-2/assets/using/metadata-profiles.html#ApplyingaMetadataProfiletoFolders

### Configuration to apply a metadata profile globally {#apply-a-metadata-profile-globally}

In addition to applying a profile to a folder, you can also apply one globally so that any content uploaded into [!DNL Experience Manager] assets in any folder has the selected profile applied.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets).

To apply a metadata profile globally, follow these steps:

* Navigate to `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` and apply the appropriate profile and click **[!UICONTROL Save]**.

  ![Apply metadata profile to a folder globally](assets/metadata-profile-folder-setting.png)

* In CRXDE Lite, navigate to the following node: `/content/dam/jcr:content`. Add the property `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` and click **[!UICONTROL Save All]**.

  ![See applied metadata profile to a folder in the JCR in CRXDE](assets/metadata-profile-folder-setting2.png)
-->

## フォルダーのメタデータスキーマ {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] では、フォルダープロパティページに表示されるレイアウトおよびメタデータを定義する、アセットフォルダーのメタデータスキーマを作成できます。

### フォルダーメタデータスキーマフォームの追加 {#add-a-folder-metadata-schema-form}

フォルダーメタデータスキーマフォームエディターを使用して、フォルダーのメタデータスキーマを作成および編集します。

1. [!DNL Experience Manager] インターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL フォルダーメタデータスキーマ]**&#x200B;に移動します。
1. [!UICONTROL フォルダーメタデータスキーマフォーム]ページの「**[!UICONTROL 作成]**」をクリックします。
1. フォームの名前を指定し、「**[!UICONTROL 作成]**」をクリックします。新しいスキーマフォームが[!UICONTROL スキーマフォーム]ページにリストされます。

### フォルダーメタデータスキーマフォームの編集 {#edit-folder-metadata-schema-forms}

以下を含む、新しく追加された、または既存のメタデータスキーマフォームを編集できます。

* タブ
* タブ内のフォーム項目。

これらのフォーム項目を CRX リポジトリーのメタデータノード内のフィールドにマップしたり、フォーム項目を設定したりできます。新しいタブまたはフォーム項目をメタデータスキーマフォームに追加できます。

1. スキーマフォームページで、作成したフォームを選択し、ツールバーの「**[!UICONTROL 編集]**」オプションを選択します。
1. フォルダーメタデータスキーマエディターページで、`+` をクリックしてフォームにタブを追加します。タブの名前を変更するには、デフォルト名をクリックし、「**[!UICONTROL 設定]**」に新しい名前を指定します。

   ![custom_tab](assets/custom_tab.png)

   タブを追加するには、`+` をクリックします。削除するには、タブの `X` をクリックします。

1. アクティブになっているタブで、「**[!UICONTROL フォームを作成]**」タブから 1 つ以上のコンポーネントを追加します。

   ![adding_components](assets/adding_components.png)

   複数のタブを作成する場合は、コンポーネントを追加する特定のタブをクリックします。

1. コンポーネントを設定するには、コンポーネントを選択して、「**[!UICONTROL 設定]**」タブでそのプロパティを変更します。

   必要に応じて、「**[!UICONTROL 設定]**」タブからコンポーネントを削除します。

   ![configure_properties](assets/configure_properties.png)

1. 変更を保存するには、ツールバーから「**[!UICONTROL 保存]**」を選択します。

#### フォームを作成するコンポーネント {#components-to-build-forms}

「**[!UICONTROL フォームを作成]**」タブには、フォルダーメタデータスキーマフォーム内で使用するフォーム項目が一覧表示されます。「**[!UICONTROL 設定]**」タブには、「**[!UICONTROL フォームを作成]**」タブで選択した各項目の属性が表示されます。以下は、「**[!UICONTROL フォームを作成]**」タブで使用可能なフォーム項目のリストです。

| コンポーネント名 | 説明 |
|---|---|
| [!UICONTROL セクションヘッダー] | 共通コンポーネントのリストに対してセクションヘッダーを追加します。 |
| [!UICONTROL 1 行のテキスト] | 1 行のテキストのプロパティを追加します。これは文字列として保存されます。 |
| [!UICONTROL 複数値テキスト] | 複数値テキストプロパティを追加します。これは文字列の配列として保存されます。 |
| [!UICONTROL 数値] | 数値コンポーネントを追加します。 |
| [!UICONTROL 日付] | 日付コンポーネントを追加します。 |
| [!UICONTROL ドロップダウン] | ドロップダウンリストを追加します。 |
| [!UICONTROL 標準タグ] | タグを追加します。 |
| [!UICONTROL 非表示のフィールド] | 非表示のフィールドを追加します。このフィールドは、アセットの保存時に POST パラメーターとして送信されます。 |

#### フォーム項目の編集 {#editing-form-items}

フォーム項目のプロパティを編集するには、コンポーネントをクリックし、**[!UICONTROL 設定]**&#x200B;タブで次のプロパティのすべてまたはサブセットを編集してください。

**[!UICONTROL フィールドラベル]**：フォルダーのプロパティページに表示されるメタデータプロパティの名前。

**[!UICONTROL プロパティにマッピング]**：このプロパティは、フォルダーノードが保存されている CRX リポジトリ内でのフォルダーノードの相対パスを指定します。「**/**」で始まり、パスがそのフォルダーのノードの配下にあることを示します。

このプロパティの有効な値は次のとおりです。

* `./jcr:content/metadata/dc:title`：フォルダーのメタデータノードにある値を、プロパティ `dc:title` として格納します。

* `./jcr:created`：フォルダーのノードにある JCR プロパティを表示します。これらのプロパティを CRXDE で設定する場合、これらのプロパティは保護されているので、「編集を無効にする」としてマークすることをお勧めします。そうしない場合は、アセットのプロパティを保存するときに、「`Asset(s) failed to modify`」というエラーが発生します。

プロパティパスにスペースを含めないでください。コンポーネントがメタデータスキーマフォームに適切に表示されなくなります。

**[!UICONTROL JSON パス]**：オプションのキーと値のペアを指定する JSON ファイルのパスを指定します。

**[!UICONTROL プレースホルダー]**：このプロパティを使用して、メタデータプロパティに関連するプレースホルダーテキストを指定します。

**[!UICONTROL 選択肢]**：リストの選択肢を指定するには、このプロパティを使用します。

**[!UICONTROL 説明]**：メタデータコンポーネントの短い説明を追加するには、このプロパティを使用します。

**[!UICONTROL クラス]**：プロパティが関連付けられているオブジェクトクラス。

### フォルダーメタデータスキーマフォームを削除 {#delete-folder-metadata-schema-forms}

フォルダーメタデータスキーマフォームページから、フォルダーメタデータスキーマフォームを削除できます。フォームを削除するには、フォームを選択してから、ツールバーの「削除」オプションをクリックしてください。

![delete_form](assets/delete_form.png)

### フォルダーメタデータスキーマの割り当て {#assign-a-folder-metadata-schema}

フォルダーメタデータスキーマフォームページから、またはフォルダーの作成時に、フォルダーにフォルダーメタデータスキーマを割り当てることができます。

フォルダーのメタデータスキーマを設定すると、スキーマフォームのパスは、`./jcr:content` の下のフォルダーノードの `folderMetadataSchema` プロパティに格納されます。

#### フォルダーメタデータスキーマページからのスキーマへの割り当て {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. [!DNL Experience Manager]インターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL アセット]**／**[!UICONTROL フォルダーのメタデータスキーマ]**&#x200B;に移動します。
1. フォルダーメタデータスキーマフォームページから、フォルダーに適用するスキーマフォームを選択します。
1. ツールバーの&#x200B;**[!UICONTROL フォルダーに適用]**&#x200B;をクリックします。

1. スキーマを適用するフォルダーを選択し、「**[!UICONTROL 適用]**」をクリックします。既にフォルダーにメタデータスキーマが適用されている場合は、既存のメタデータスキーマを上書きするかどうかを確認する警告メッセージが表示されます。「**[!UICONTROL 上書き]**」をクリックします。
1. メタデータスキーマを適用したフォルダーのメタデータプロパティを開きます。

   ![folder_properties](assets/folder_properties.png)

   フォルダーメタデータフィールドを表示するには、「**[!UICONTROL フォルダーメタデータ]**」タブをクリックします。

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### フォルダー作成時のスキーマの割り当て {#assign-a-schema-when-creating-a-folder}

フォルダーの作成時に、フォルダーメタデータスキーマを割り当てることができます。システムに 1 つ以上のフォルダーメタデータスキーマが存在する場合は、**[!UICONTROL フォルダーを作成]**&#x200B;ダイアログに追加リストが表示されます。目的のスキーマを選択できます。 デフォルトでは、スキーマは選択されていません。

1. [!DNL Experience Manager Assets] ユーザーインターフェイスで、ツールバーの「**[!UICONTROL 作成]**」をクリックします。
1. フォルダーのタイトルと名前を指定します。
1. フォルダーメタデータスキーマリストで、目的のスキーマを選択します。次に、「**[!UICONTROL 作成]**」をクリックします。

   ![select_schema](assets/select_schema.png)

1. メタデータスキーマを適用したフォルダーのメタデータプロパティを開きます。
1. フォルダーメタデータフィールドを表示するには、「**[!UICONTROL フォルダーメタデータ]**」タブをクリックします。

### フォルダーメタデータスキーマの使用 {#use-the-folder-metadata-schema}

フォルダーメタデータスキーマが設定されたフォルダーのプロパティを開きます。フォルダー[!UICONTROL プロパティ]ページに「**[!UICONTROL フォルダーメタデータ]**」タブが表示されます。フォルダーメタデータスキーマフォームを表示するには、このタブを選択します。

各種フィールドにメタデータ値を入力し、「**[!UICONTROL 保存]**」をクリックして値を保存してください。指定した値は、CRX リポジトリ内のフォルダーノードに保存されます。

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## ヒントと制限事項 {#best-practices-limitations}

* カスタム名前空間にメタデータを読み込むには、まず、その名前空間を登録します。
* プロパティピッカーは、スキーマエディターおよび検索フォームで使用されるプロパティを表示します。プロパティピッカーはアセットからメタデータプロパティを選択しません。
* [!DNL Experience Manager] 6.5 にアップグレードする前から、既存のメタデータプロファイルが存在している可能性があります。アップグレード後、「[!UICONTROL メタデータプロファイル]」タブのフォルダー[!UICONTROL プロパティ]にそのようなプロファイルを適用すると、メタデータフォームフィールドは表示されません。ただし、新しく作成したメタデータプロファイルを適用すると、フォームのフィールドは表示されますが、期待どおりに使用できません。機能は失われませんが、（使用できない）フォームフィールドを表示したい場合は、既存のメタデータプロファイルを編集して保存します。

>[!MORELIKETHIS]
>
>* [メタデータの概念と理解](metadata-concepts.md)。
>* [複数コレクションのメタデータプロパティの編集](manage-collections.md#editing-collection-metadata-in-bulk)。
>* [Experience Manager Assetsでのメタデータの読み込みと書き出し](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html?lang=ja)。
>* [メタデータ、画像およびビデオを処理するためのプロファイル](processing-profiles.md)。
>* [プロファイルを使用するためのデジタルアセットの整理のベストプラクティス](/help/assets/organize-assets.md)。
>* [XMP の書き戻し](/help/assets/xmp-writeback.md)。
