---
title: AEM Assetsを使用したデジタルアセットの管理
description: デジタルアセットのアップロード、ダウンロード、編集、検索、削除、注釈の追加、バージョンなどのアセット管理タスクについて説明します。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 68fb4c08b8093ff50e74dc9e29011325cdf7e7d7

---


# デジタルアセットの管理 {#managing-assets-with-the-touch-optimized-ui}

ここでは、Adobe Experience Manager (AEM) Assets でアセットを管理および編集する方法について説明します。ユーザーインターフェイスとレイアウトの使用を開始するには、タッチ操作対応UI [の基本的な処理を参照してくださ](/help/sites-authoring/basic-handling.md)い。 To manage Content Fragments, see [Managing Content Fragments](content-fragments-managing.md) assets.

## フォルダーの作成 {#creating-folders}

`Nature` に関するすべての画像などの、アセットのコレクションを構成する場合に、それらを保存するフォルダーを作成できます。フォルダーを使用すると、アセットを分類および整理できます。ただし、効率向上のためには必ずアセットをフォルダーで整理しなければならないということではありません。

>[!NOTE]
>
>* Sharing an Assets folder of the type `sling:OrderedFolder` is not supported when sharing to Marketing Cloud. フォルダーを共有する場合は、フォルダーを作成するときに [!UICONTROL Ordered] を選択しないでください。
>* Experience Managerでは、単語をフォルダーの名 `subassets` 前として使用することはできません。 これは、複合アセットのサブアセットを含むノード用に予約されたキーワードです。


1. 新しいフォルダーを作成するデジタルアセットフォルダーの場所に移動します。メニューで、「**[!UICONTROL 作成]**」をクリックします。「**[!UICONTROL 新規フォルダ]**」を選択します。
1. 「**[!UICONTROL タイトル]**」フィールドにフォルダー名を入力します。デフォルトでは、フォルダー名として指定したタイトルが使用されます。フォルダーが作成されると、デフォルトのフォルダー名を上書きして、別のフォルダー名を指定できます。
1. 「**[!UICONTROL 作成]**」をクリックします。作成したフォルダーがデジタルアセットフォルダーに表示されます。

以下の文字（スペース区切りリスト）はサポートされません。

* アセットファイル名に次の文字を含めることはできません。`* / : [ \\ ] | # % { } ? &`
* アセットフォルダー名に次の文字を含めることはできません。`* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## アセットのアップロード {#uploading-assets}

<!-- TBD the following:
Move this section into a new article. CQDOC-14874 ticket is created for this.
In this complete article, replace emphasis with UICONTROL where appropriate.
-->

様々な種類のアセット（画像、PDF ファイル、RAW ファイルなど）をローカルフォルダーやネットワークドライブから AEM Assets にアップロードできます。

>[!NOTE]
>
>Dynamic Media - Scene7 モードでは、ファイルサイズが 2 GB 以下のアセットのみアップロードできます。

アセットは、処理プロファイルが割り当てられたまたは割り当てられていないフォルダーにアップロードできます。

処理プロファイルが割り当てられているフォルダーの場合、プロファイル名がカード表示のサムネールに表示されます。リスト表示では、プロファイル名が「**処理プロファイル**」に表示されます。詳しくは、[処理プロファイル](/help/assets/processing-profiles.md)を参照してください。

Before uploading an asset, ensure that it is in a [format](/help/assets/assets-formats.md) that AEM Assets supports.

1. Assets ユーザーインターフェイスで、デジタルアセットを追加する場所に移動します。
1. アセットをアップロードするには、以下のいずれかの操作をおこないます。

   * ツールバーの「**[!UICONTROL 作成]**」アイコンをタップします。Then on the menu, tap **[!UICONTROL Files]**. 表示されたダイアログで、必要に応じてファイル名を変更できます。
   * HTML5 をサポートするブラウザーで、アセットを Assets ユーザーインターフェイスに直接ドラッグします。ファイル名を変更するためのダイアログは表示されません。
   ![アセットをアップロードするオプションの作成](assets/create-options.png)

   複数のファイルを選択するには、ファイル選択ダイアログで、Ctrl キーまたは Command キーを押しながらアセットを選択します。iPad を使用している場合、一度に選択できるファイルは 1 つだけです。

   サイズの大きなアセット（500 MB 超）のアップロードを一時停止して、同じページから後で再開できます。Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   ![アセットのアップロードの進行状況バー](assets/chlimage_1-5.png)

   サイズが大きいと見なされるアセットのサイズは変更できます。例えば、（500 MB でなく）1000 MB を超えるサイズのアセットをサイズが大きいと見なすようにシステムを設定できます。In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   1000 MB を超えるファイル 1 つと 1000 MB 未満のファイル 1 つをアップロードする場合、一時停止ボタンは表示されません。ただし、1000 MB 未満のファイルのアップロードをキャンセルすると、**[!UICONTROL 一時停止]**&#x200B;ボタンが表示されます。

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload`node in the CRX repository.

   **[!UICONTROL 一時停止]**&#x200B;アイコンをクリックすると、**[!UICONTROL 再生]**&#x200B;アイコンに切り替わります。To resume uploading, click the **[!UICONTROL Play]** icon.

   ![再生アイコンを使用して、一時停止したアセットのアップロードを再開します](assets/chlimage_1-6.png)

   進行中のアップロードをキャンセルするには、進行状況バーの横にある閉じるボタン（「`X`」）をクリックします。アップロード処理をキャンセルすると、AEM Assets はアセットのアップロード済みの部分を削除します。

   アップロードを再開する機能は、帯域幅が狭く、ネットワークの誤作動によりサイズの大きなアセットのアップロードに時間がかかるシナリオで特に便利です。アップロード処理を一時停止して、後で状況が改善したときに処理を再開できます。再開すると、処理を一時停止した箇所からアップロードが開始されます。

   アップロード処理中、AEM はアップロード中の部分のアセットをデータのチャンクとして CRX リポジトリに保存します。アップロードが完了すると、AEM はリポジトリ内のチャンクを 1 つのブロックに統合します。

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.

   アセットのアップロード先に既に存在するアセットと同じ名前のアセットをアップロードすると、警告ダイアログが表示されます。

   既存のアセットを置き換えるか、別のバージョンを作成するか、アップロードする新しいアセットの名前を変更して両方のアセットを残すかを選択できます。既存のアセットを置き換えると、アセットのメタデータと、既存のアセットに対して行った以前の変更（注釈や切り抜きなど）がすべて削除されます。 If you choose to keep both assets, the new asset is renamed with number `1` appended to its name.

   ![名前の競合ダイアログボックスを使用して、アセット名の競合を解決します。](assets/chlimage_1-7.png)

   >[!NOTE]
   >
   >[!UICONTROL 名前の競合]ダイアログで「**[!UICONTROL 置換]**」を選択すると、新しいアセットのアセット ID が再生成されます。この ID は以前のアセットの ID とは異なります。
   >
   >アセットインサイトによる Adobe Analytics でのインプレッション数やクリック数の追跡が有効になっている場合は、再生成されたアセット ID により、Analytics から取得したアセットのデータが無効になります。

   If the asset you upload exists in AEM Assets, the **[!UICONTROL Duplicates Detected]** dialog warns that you are attempting to upload a duplicate asset. The dialog appears only if the `SHA 1` checksum value of the binary of the existing asset matches the checksum value of the asset you upload. この場合、アセットの名前は関係ありません。

   >[!NOTE]
   >
   >The [!UICONTROL Duplicates Detected] dialog appears only when the duplicate detection feature is enabled. To enable the duplicate detection feature, see [Enable Duplicate Detection](/help/assets/duplicate-detection.md).

   ![重複アセットが検出されましたダイアログ](assets/chlimage_1-8.png)

   重複したアセットを AEM Assets で保持するには、「**[!UICONTROL 保持]**」をタップまたはクリックします。アップロードした重複アセットを削除するには、「**[!UICONTROL 削除]**」をタップまたはクリックします。

   AEM Assets では、ファイル名に禁止文字が含まれるアセットをアップロードできません。ファイル名に禁止文字が含まれるアセットをアップロードしようとすると、AEM Assets に警告メッセージが表示され、これらの文字を削除するか使用可能な名前でアップロードするまでアップロードが停止されます。

   組織固有のファイル命名規則に合うように、[!UICONTROL アセットをアップロード]ダイアログでは、アップロードするファイルに長い名前を指定できます。

   ただし、以下の文字（スペース区切りリスト）はサポートされていません。

   * アセットファイル名に含めてはいけない文字：`* / : [ \\ ] | # % { } ? &`
   * アセットフォルダー名に含めてはいけない文字：`* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`
   ![アップロードの進行状況ダイアログに、正常にアップロードされたファイルと、アップロードに失敗したファイルのステータスが表示されます。](assets/chlimage_1-10.png)

   さらに、Assets ユーザーインターフェイスには、アップロードした最新のアセットまたは最初に作成したフォルダーが表示されます。

   ファイルがアップロードされる前にアップロード操作をキャンセルすると、AEM Assets が現在のファイルのアップロードを停止し、コンテンツを更新します。ただし、既にアップロードされているファイルは削除されません。

   AEM Assets のアップロード進行状況ダイアログには、アップロードが成功したファイルと失敗したファイルの数が表示されます。

### 順次アップロード {#serialuploads}

一括で多数のアセットをアップロードすると、多くの I/O リソースを消費し、AEM Assets インスタンスのパフォーマンスが悪化することがあります。特に、インターネット接続が低速の場合、ディスク I/O のスパイクによりアップロード時間が非常に長くなります。さらに、Web ブラウザーでは、アセットの同時アップロードで AEM Assets が処理できる POST リクエスト数に制限が課されることがあります。その結果、アップロード操作に失敗したり、途中で終了してしまったりします。つまり、AEM Assets で多数のファイルを取り込むときに、一部のファイルを取り込めないことがあったり、まったくファイルを取り込めないことがあります。

この状況を回避するために、AEM Assets は一括アップロード操作時にすべてのアセットを同時に取り込まず、一度に 1 つずつアセットを取り込みます（順次アップロード）。

アセットの順次アップロードは、デフォルトで有効になっています。To disable the feature and allow concurrent uploading, overlay the `fileupload` node in Crx-de and set the value of the `parallelUploads` property to `true`.

### Upload assets using FTP {#uploading-assets-using-ftp}

Dynamic Media では、FTP サーバー経由でアセットをバッチアップロードできます。大きなアセット（1 GBを超える）をアップロードする場合、またはフォルダとサブフォルダ全体をアップロードする場合は、FTPを使用する必要があります。 定期的にFTPアップロードを行うように設定することもできます。

>[!NOTE]
>
>Dynamic Media - Scene7 モードでは、ファイルサイズが 2 GB 以下のアセットのみアップロードできます。

>[!NOTE]
>
>ダイナミックメディア — Scene7モードでFTP経由でアセットをアップロードするには、AEM作成者インスタンスに機能パック18912をインストールします。 Contact [Adobe Customer Care](https://helpx.adobe.com/jp/contact/enterprise-support.ec.html) to get access to FP-18912 and complete the setup of your FTP account. 詳しくは、一括アセット移行の機 [能パック18912のインストールを参照してください](/help/assets/bulk-ingest-migrate.md)。
>
>アセットのアップロードに FTP を使用する場合、AEM で指定したアップロード設定は無視されます。代わりに、Dynamic Media Classic で定義したファイル処理ルールが使用されます。

**FTP によりアセットをアップロードするには**

1. 任意の FTP クライアントを使用して、プロビジョニングメールで受け取った FTP ユーザー名とパスワードで FTP サーバーにログインします。FTP クライアントで、ファイルやフォルダーを FTP サーバーにアップロードします。
1. プロビジョニングメールで受け取った資格情報で [Dynamic Media Classic にログイン](https://www.adobe.com/jp/marketing/experience-manager/scene7-login.html)します。グローバルナビゲーションバーの「**[!UICONTROL アップロード]**」をタップします。

1. アップロードページの左上隅付近で「**[!UICONTROL FTP 経由]**」タブをタップします。
1. ページの左側でファイルのアップロード元の FTP フォルダーを選択し、ページの右側でアップロード先のフォルダーを選択します。
1. ページの右下隅付近で「**[!UICONTROL オプション]**」をクリックし、選択したフォルダー内のアセットに基づいて必要なオプションを設定します。

   [アップロードオプションを設定](#upload-job-options)を参照してください。

   >[!NOTE]
   >
   >FTP 経由でアセットをアップロードする場合、Dynamic Media Classic（S7）で設定したアップロードジョブのオプションのほうが AEM で設定した処理パラメーターより優先されます。

1. アップロードオプションを設定ダイアログボックスの右下隅で「**[!UICONTROL 保存]**」をタップします。
1. アップロードページの右下隅で「**[!UICONTROL アップロードを送信]**」をタップします。

   アップロードの進行状況を確認するには、グローバルナビゲーションバーの「**[!UICONTROL ジョブ]**」をタップします。ジョブページに、アップロードの進行状況が表示されます。ユーザーは、AEM で作業を続け、いつでも Dynamic Media Classic のジョブページに戻って進行中のジョブを確認できます。進行中のアップロードジョブをキャンセルするには、経過時間の横の「**[!UICONTROL キャンセル]**」をタップします。

#### アップロードオプションを設定 {#upload-job-options}

| アップロードオプション | サブオプション | 説明 |
|---|---|---|
| Job Name |  | テキストフィールドにあらかじめ入力されるデフォルト名。ユーザーが入力した名前部分や日付と時刻のスタンプが含まれます。デフォルト名を使用するか、このアップロードジョブ用に独自に作成した名前を入力することができます。<br>このジョブと他のアップロードジョブや公開ジョブはジョブページに記録されます。ここでジョブのステータスを確認できます。 |
| アップロード後に公開 |  | アップロードしたアセットを自動的に公開します。 |
| 任意のフォルダーでベース名が同じファイルを上書き |  | アップロードするファイルと同じ名前のファイルが既にある場合にアップロードするファイルで置き換えるには、このオプションを選択します。このオプションの名前は、**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**／**[!UICONTROL アプリケーションへのアップロード]**／**[!UICONTROL 画像を上書き]**&#x200B;での設定に応じて異なる可能性があります。 |
| アップロード時に Zip または Tar ファイルを解凍 |  |  |
| オプション |  | Tap/ click **[!UICONTROL Job Options]** to open the [!UICONTROL Upload Job Options] dialog box and choose options that affect the entire upload job. これらのオプションはすべてのファイルタイプで同じです。<br>アプリケーションの全般設定ページから、ファイルのアップロード用のデフォルトオプションを選択できます。このページを開くには、**[!UICONTROL セットアップ]**／**[!UICONTROL アプリケーション設定]**&#x200B;を選択します。Tap the **[!UICONTROL Default Upload Options]** button to open the [!UICONTROL Upload Job Options] dialog box. |
|  | 実行時 | 「一時」または「定期」を選択します。定期ジョブを設定するには、繰り返しオプション（毎日、毎週、またはカスタム）を選択し、FTP アップロードジョブを反復する頻度を指定します。次に、必要に応じてスケジューリングオプションを指定します。 |
|  | サブフォルダーを含める | アップロードしたいフォルダー内のすべてのサブフォルダーをアップロードします。アップロードするフォルダーとそのサブフォルダーの名前は AEM Assets に自動的に登録されます。 |
|  | 切り抜きツールオプション | 画像の端から手動で切り抜くには、切り抜きメニューを選択し、「手動」を選択します。次に、画像のいずれかの辺または各辺から切り抜くピクセル数を入力します。画像から切り抜かれる範囲は、画像ファイルの ppi（画素密度）設定に応じて異なります。例えば、画像が 150 ppi で表示されている場合に、「上」、「右」、「下」、「左」テキストボックスに 75 と入力すると、各辺から 0.5 inch ずつ切り抜かれます。<br>画像からホワイトスペースを自動的に切り抜くには、切り抜きメニューを開き、「手動」を選択し、「上」、「右」、「下」、「左」フィールドに画像の各辺から切り抜くピクセル数を入力します。また、切り抜きメニューで「トリミング」を選択し、以下のオプションを選択することもできます。<br> **トリミング対象カラー** <ul><li>**色** - 「色」オプションを選択します。 次に、隅メニューを選択し、切り抜きたいホワイトスペースの色を最も表現している色の画像の角を選択します。</li><li>****&#x200B;透明度 - 「透明度」オプションを選択します。<br> **許容値** — スライダをドラッグして、許容値を0 ～ 1の範囲で指定します。色に基づいてトリミングする場合は、0を指定すると、画像の隅で選択した色と正確に一致する場合にのみピクセルが切り抜かれます。 1 に近いほど、色の違いに対する許容度が高くなります。<br> 透明度に基づくトリミングでは、切り抜くピクセルが透明な場合のみ、0 を指定してください。1 に近いほど、不透明さに対する許容度が高くなります。</li></ul><br>これらの切り抜きツールオプションは、非破壊です（何度でも修正できます）。 |
|  | カラープロファイルオプション | 配信に使用される最適なファイルを作成するときのカラー変換を選択します。<ul><li>デフォルトの色保存：画像にカラースペース情報が含まれる場合はソース画像の色を保持します。カラー変換はおこなわれません。今日ほぼすべての画像に適切なカラープロファイルが埋め込まれています。ただし、CMYK のソース画像にカラープロファイルが埋め込まれていないと、色が standard Red Green Blue（sRGB）カラースペースに変換されます。sRGB は Web ページでの画像表示に最適なカラースペースです。</li><li>オリジナルカラースペースを維持：アップロード時にカラー変換をおこなわずに元の色を保持します。カラープロファイルが埋め込まれていない画像の場合、カラー変換はすべて、公開設定で設定したデフォルトのカラープロファイルを使用しておこなわれます。このカラープロファイルは、このオプションで作成したファイルのカラーと一致しない可能性があります。したがって、「デフォルトの色保存」オプションを使用することをお勧めします。</li><li>カスタム アップロード元／アップロード先<br> アップロード元とアップロード先のカラースペースを選択できるメニューが開きます。この詳細オプションは、ソースファイルに埋め込まれたカラー情報より優先されます。送信するすべての画像のカラープロファイルデータが正しくないか不足している場合に、このオプションを選択します。</li></ul> |
|  | 画像編集オプション | 画像のクリッピングマスクを保持し、カラープロファイルを選択できます。<br>[アップロード時の画像編集オプションの設定](#setting-image-editing-options-at-upload)を参照してください。 |
|  | Postscript オプション | PostScript® ファイルのラスタライズ、ファイルの切り抜き、透明背景の維持、解像度の選択、カラースペースの選択をおこなうことができます。<br>[PostScript および Illustrator のアップロードオプションの設定](#setting-postscript-and-illustrator-upload-options)を参照してください。 |
|  | Photoshop オプション | Adobe® Photoshop® ファイルからのテンプレート作成、レイヤーの維持、レイヤーの命名方法の指定、テキストの抽出、テンプレートへの画像のアンカー方法の指定をおこなうことができます。<br>テンプレートは AEM ではサポートされていません。<br>[Photoshop アップロードオプションの設定](#setting-photoshop-upload-options)を参照してください。 |
|  | PDF オプション | ファイルのラスタライズ、検索単語とリンクの抽出、eCatalog の自動生成、解像度の設定、カラースペースの選択をおこなうことができます。<br> AEMではeCatalogはサポートされていません。 <br>[PDF アップロードオプションの設定](#setting-pdf-upload-options)を参照してください。 |
|  | Illustrator オプション | Adobe Illustrator® ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択をおこなうことができます。<br>[PostScript および Illustrator のアップロードオプションの設定](#setting-postscript-and-illustrator-upload-options)を参照してください。 |
|  | EVideo オプション | ビデオプリセットを選択して、ビデオファイルをトランスコードできます。<br>[eVideo アップロードオプションの設定](#setting-evideo-upload-options)を参照してください。 |
|  | バッチセットプリセット | アップロードしたファイルから画像セットまたはスピンセットを作成するには、使用したいプリセットの「アクティブ」列をクリックします。複数のプリセットを選択できます。プリセットは、Dynamic Media Classic のアプリケーション設定／バッチセットプリセットページで作成します。<br>バッチセットプリセットの作成について詳しくは、[画像セットとスピンセットの自動生成用のバッチセットプリセットの設定](config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を参照してください。<br>[アップロード時のバッチセットプリセットの設定](#setting-batch-set-presets-at-upload)を参照してください。 |

#### Set image editing options at upload {#setting-image-editing-options-at-upload}

When uploading image files, including AI, EPS, and PSD files, you can take the following editing actions in the [!UICONTROL Upload Job Options] dialog box:

* 画像の端からホワイトスペースを切り抜く（上の表の説明を参照してください）。
* 画像の側面から手動で切り抜く（上の表の説明を参照してください）。
* カラープロファイルを選択する（上の表でオプションの説明を参照してください）。
* クリッピングパスからマスクを作成する。
* アンシャープマスクオプションで画像にシャープニングを適用する
* ノックアウトの背景

<!--
| Option | Sub-option | Description |
|---|---|---|
| Create Mask From Clipping Path | | Create a mask for the image based on its clipping path information. This option applies to images created with image-editing applications in which a clipping path was created. |
| Unsharp Masking | | Lets you fine-tune a sharpening filter effect on the final downsampled image, controlling the intensity of the effect, the radius of the effect (as measured in pixels), and a threshold of contrast that is ignored.<br> This effect uses the same options as Photoshop’s Unsharp Mask filter. Contrary to what the name suggests, Unsharp Mask is a sharpening filter. Under Unsharp Masking, set the options you want. Setting options are described in the following: |
| | Amount | Controls the amount of contrast that is applied to edge pixels.<br> Think of it as the intensity of the effect. The main difference between the amount values of Unsharp Mask in Dynamic Media and the amount values in Adobe Photoshop, is that Photoshop has an amount range of 1% to 500%. Whereas, in Dynamic Media, the value range is 0.0 to 5.0. A value of 5.0 is the rough equivalent of 500% in Photoshop; a value of 0.9 is the equivalent of 90%, and so on. |
| | Radius | Controls the radius of the effect. The value range is 0-250.<br> The effect is run on all pixels in an image and radiates out from all pixels in all directions. The radius is measured in pixels. For example, to get a similar sharpening effect for a 2000 x 2000 pixel image and 500 x 500 pixel image, you would set a radius of two pixels on the 2000 x 2000 pixel image and a radius value of one pixel on the 500 x 500 pixel image. A larger value is used for an image that has more pixels. |
| | Threshold | Threshold is a range of contrast that is ignored when the Unsharp Mask filter is applied. It is important so that no "noise" is introduced to an image when this filter is used. The value range is 0-255, which is the number of brightness steps in a grayscale image. 0=black, 128=50% gray and 255=white.<br> For example, a threshold value of 12 ignores slight variations is skin tone brightness to avoid adding noise, but still add edge contrast to areas such as where eyelashes meet skin.<br> For example, if you have a photo of someone’s face, the Unsharp Mask affects the parts of the image, such as where eyelashes and skin meet to create an obvious area of contrast, and the smooth skin itself. Even the smoothest skin exhibits subtle changes in brightness values. If you do not use a threshold value, the filter accentuates these subtle changes in skin pixels. In turn, a noisy and undesirable effect is created while contrast on the eyelashes is increased, enhancing sharpness.<br> To avoid this issue, a threshold value is introduced that tells the filter to ignore pixels that do not change contrast dramatically, like smooth skin.<br> In the zipper graphic shown earlier, notice the texture next to the zippers. Image noise is exhibited because the threshold values were too low to suppress the noise. |
| | Monochrome | Select to unsharp-mask image brightness (intensity).<br> Deselect to unsharp-mask each color component separately. |
| Knockout Background | | Automatically removes the background of an image when you upload it. This technique is useful to draw attention to a particular object and make it stand out from a busy background. Select to enable or “turn on” the Knockout Background feature and the following sub-options: |
| | Corner | Required.<br> The corner of the image that is used to define the background color to knockout.<br> You can choose from **Upper Left**, **Bottom Left**, **Upper Right**, or **Bottom Right**. |
| | Fill Method | Required.<br> Controls pixel transparency from the Corner location that you set.<br> You can choose from the following fill methods: <ul><li>**Flood Fill** - turns all pixels transparent that match the Corner that you have specified and are connected to it.</li><li>**Match Pixel** - turns all matching pixels transparent, regardless of their location on the image.</li></ul> |
| | Tolerance | Optional.<br> Controls the allowable amount of variation in pixel color matching based on the Corner location that you set.<br> Use a value of 0.0 to match pixel colors exactly or, use a value of 1.0 to allow for the greatest variation. |
-->

#### Set PostScript and Illustrator upload options {#setting-postscript-and-illustrator-upload-options}

PostScript（EPS）または Illustrator（AI）画像ファイルのアップロード時に、様々な方法でファイルをフォーマットできます。ファイルのラスタライズ、透明背景の維持、解像度の選択、カラースペースの選択ができます。Options for formatting PostScript and Illustrator files are available in the [!UICONTROL Upload Job Options] dialog box under [!UICONTROL PostScript Options] and [!UICONTROL Illustrator Options].

| オプション | サブオプション | 説明 |
|---|---|---|
| 処理中 |  | **[!UICONTROL ラスタライズ]**&#x200B;を選択して、ファイル内のベクターグラフィックスをビットマップ形式に変換します。 |
| レンダリングされた画像で透明な背景を保持する |  | ファイルの背景の透明度を維持します。 |
| 解決方法 |  | 解像度設定を決定します。この設定により、ファイル内の 1 inch あたりに表示するピクセル数を決定します。 |
| カラースペース |  | 「カラースペース」メニューを選択し、次のカラースペースオプションから選択します。 |
|  | 自動検出 | ファイルのカラースペースを保持します。 |
|  | RGB として強制 | RGB カラースペースに変換します。 |
|  | CMYKとしてレンダリング | CMYK カラースペースに変換します。 |
|  | グレースケールとして強制 | グレースケールカラースペースに変換します。 |

#### Photoshopのアップロードオプションの設定 {#setting-photoshop-upload-options}

Photoshopドキュメント(PSD)ファイルは、画像テンプレートの作成に最もよく使用されます。 When you upload a PSD file, you can create an image template automatically from the file (select the [!UICONTROL Create Template] option on the Upload screen).

レイヤーの含まれる PSD ファイルをテンプレートの作成に使用すると、Dynamic Media はこのファイルから複数の画像を作成します。1 レイヤーにつき 1 画像作成されます。

Use the [!UICONTROL Crop Options] and [!UICONTROL Color Profile Options], described above, with Photoshop upload options.

>[!NOTE]
>
>テンプレートは AEM ではサポートされていません。

| オプション | サブオプション | 説明 |
|---|---|---|
| レイヤーを維持 |  | PSD にレイヤーがあれば切り離して個別のアセットにします。アセットレイヤーは PSD に関連付けられたまま維持されます。詳細ビューで PSD ファイルを開き、レイヤーパネルを選択して、これらを確認できます。 |
| テンプレートを作成 |  | PSD ファイル内のレイヤーからテンプレートを作成します。 |
| テキストを抽出 |  | テキストを抽出して、ユーザーがビューア内でテキストを検索できるようにします。 |
| レイヤーを背景サイズに拡大 |  | 切り離した画像レイヤーのサイズを、背景レイヤーのサイズに拡大します。 |
| レイヤーの名前 |  | PSD ファイル内のレイヤーを別々の画像としてアップロードします。 |
|  | レイヤー名 | PSD ファイル内のレイヤー名に従って画像に名前を付けます。例えば、元の PSD ファイルに Price Tag という名前のレイヤーがある場合、Price Tag という名前の画像になります。ただし、PSD ファイル内のレイヤー名がデフォルトの Photoshop レイヤー名（背景、レイヤー 1、レイヤー 2 など）である場合、画像の名前はデフォルトレイヤー名ではなく PSD ファイル内のレイヤー番号に従って付けられます。 |
|  | Photoshop とレイヤー番号 | PSD ファイル内のレイヤー番号に従って画像の名前を付け、元のレイヤー名は無視します。Photoshop ファイル名の後にレイヤー番号を付けたものが画像の名前になります。例えば、Spring Ad.psd というファイルの 2 番目のレイヤーは、Photoshop でデフォルト以外の名前が付いていたとしても Spring Ad_2 という名前になります。 |
|  | Photoshop とレイヤー名 | PSD ファイル名の後にレイヤー名またはレイヤー番号を付けた名前になります。PSD ファイル内のレイヤー名がデフォルトの Photoshop レイヤー名である場合、レイヤー番号が使用されます。例えば、SpringAd という名前の PSD ファイルに Price Tag という名前のレイヤーがある場合、Spring Ad_Price Tag という名前になります。レイヤー 2 というデフォルト名のレイヤーは Spring Ad_2 となります。 |
| アンカー |  | PSD ファイルから作成されたレイヤーコンポジションから生成されたテンプレートに画像がどのようにアンカーされるのかを指定します。デフォルトで、アンカーは中央です。中央アンカーにより、置換画像の縦横比に関わらず、置換画像で同じ領域をより適切に埋めることができます。この画像を置換する縦横比が異なる画像が、テンプレートの参照時やパラメーターの置き換えの使用時に、同じ領域を効果的に専有します。アプリケーションでテンプレート内の割り当てられた領域を置換画像で埋める必要がある場合、別の設定に変更してください。 |

#### PDFアップロードオプションの設定 {#setting-pdf-upload-options}

PDF ファイルのアップロード時に、様々な方法でファイルをフォーマットできます。ページの切り抜き、検索単語の抽出、ppi 解像度の入力、カラースペースの選択ができます。PDF ファイルにはトリミング余白、内トンボ、登録マーク、その他のプリンター用マークなどが含まれる場合があります。PDF ファイルのアップロード時に、ページの端からこれらのマークを切り抜くことができます。

>[!NOTE]
>
>eCatalog は AEM ではサポートされていません。

次のいずれかのオプションを選択します。

| オプション | サブオプション | 説明 |
|---|---|---|
| 処理中 | ラスタライズ | （デフォルト）PDF ファイルのページをリッピングし、ベクターグラフィックスをビットマップイメージに変換します。eCatalog を作成するには、このオプションを選択します。 |
| 抽出 | 検索ワード | PDF ファイルから単語を抽出し、eCatalog ビューア内でこのファイルをキーワード検索できるようにします。 |
|  | リンク | PDF ファイルからリンクを抽出し、eCatalog ビューアで使用できる画像マップに変換します。 |
| 複数ページの PDFから eCatalog を自動生成 |  | PDF ファイルから eCatalog を自動的に作成します。eCatalog の名前は、アップロードした PDF ファイルと同じになります。（このオプションは、アップロード時に PDF ファイルをラスタライズする場合にのみ使用できます。） |
| 解決方法 |  | 解像度設定を決定します。この設定により、PDF ファイル内の 1 inch あたりに表示するピクセル数を決定します。デフォルトは 150 です。 |
| カラースペース |  | 「カラースペース」メニューを選択し、PDF ファイルのカラースペースを選択します。ほとんどの PDF ファイルには、RGB と CMYK の両方のカラー画像が含まれています。RGB カラースペースはオンラインでの表示に適しています。 |
|  | 自動検出 | PDF ファイルのカラースペースを保持します。 |
|  | RGB として強制 | RGB カラースペースに変換します。 |
|  | CMYK として強制 | CMYK カラースペースに変換します。 |
|  | グレースケールとして強制 | グレースケールカラースペースに変換します。 |

#### eVideoアップロードオプションの設定 {#setting-evideo-upload-options}

様々なビデオプリセットから選択してビデオファイルをトランスコードする。

| オプション | サブオプション | 説明 |
|---|---|---|
| アダプティブビデオ |  | モバイル、タブレットおよびデスクトップに配信するビデオを作成するための、任意の縦横比で機能する単一のエンコーディングプリセットです。 このプリセットでエンコードされたアップロード済みソースビデオは、固定の高さに設定されます。ただし、幅はビデオの縦横比を保持して自動的に拡大・縮小します。<br>ベストプラクティスは、アダプティブビデオのエンコーディングを使用することです。 |
| シングルエンコーディングプリセット | エンコードプリセットの並べ替え | 「名前」または「サイズ」を選択して、「デスクトップ」、「モバイル」および「タブレット」の下に表示されるエンコーディングプリセットを、名前または解像度サイズで並べ替えます。 |
|  | デスクトップ | デスクトップコンピュータにストリーミングビデオまたはプログレッシブビデオを配信するMP4ファイルを作成します。必要な解像度サイズとターゲットデータレートを持つ1つ以上の縦横比を選択します。 |
|  | モバイル | iPhoneまたはAndroid携帯端末で配信用のMP4ファイルを作成します。必要な解像度サイズとターゲットデータレートを持つ1つ以上の縦横比を選択します。 |
|  | タブレットなど）のアクティブマーカーを確認する。 | iPadまたはAndroidタブレットデバイスで配信用のMP4ファイルを作成します。解像度サイズとターゲットデータレートを指定して、1つ以上の縦横比を選択します。 |

#### Set Batch Set Presets at upload {#setting-batch-set-presets-at-upload}

アップロードした画像から画像セットまたはスピンセットを自動的に作成する場合は、使用するプリセットの「アクティブ」列をクリックします。 複数のプリセットを選択できます。

バッチセットプリセットの作成について詳しくは、[画像セットとスピンセットの自動生成用のバッチセットプリセットの設定](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)を参照してください。

### ストリーミングアップロード {#streamed-uploads}

AEM に多数のアセットをアップロードする場合、サーバーへの I/O 要求が大幅に増加するので、アップロードの効率が低下し、一部のアップロードタスクがタイムアウトする場合があります。AEM Assets はアセットのストリーミングアップロードをサポートします。ストリーミングアップロードにより、リポジトリにアセットをコピーする前にサーバーの一時フォルダーのアセットストレージを回避することで、アップロード操作中のディスクの I/O が低減します。代わりに、データはリポジトリに直接転送されます。これにより、サイズの大きいアセットのアップロードにかかる時間を抑え、タイムアウトが発生する可能性を減少することができます。AEM Assets では、ストリーミングアップロードはデフォルトで有効になっています。

>[!NOTE]
>
>ストリーミングアップロードは、servlet-api バージョンが 3.1 未満の JEE サーバー上で機能する AEM では無効です。

### アセットが含まれている ZIP アーカイブの抽出 {#extractzip}

ZIP アーカイブは、サポートされているその他のアセットと同じようにアップロードできます。ファイル名についても、同様のルールが ZIP ファイルに適用されます。AEM を使用すると、ZIP アーカイブを DAM の場所に抽出できます。アーカイブファイルに拡張子として ZIP が含まれていない場合、コンテンツを使用してファイルタイプの検出を有効にします。

一度に 1 つの ZIP アーカイブを選択し、「**[!UICONTROL アーカイブの抽出]**」をクリックして、抽出先フォルダーを選択します。ファイルの重複に対処するためのオプションを選択します（該当する場合）。ZIP ファイル内のアセットが抽出先フォルダー内に既に存在する場合は、抽出をスキップする、既存のファイルを置き換える、名前を変更して両方のアセットを保持する、または新しいバージョンを作成する、のいずれかを選択できます。

抽出が完了すると、AEM は通知領域にメッセージを表示します。AEM が ZIP を抽出している間、抽出を中断することなく作業に戻ることができます。

![ZIPファイルの通知抽出](assets/Zip-extraction-notification.png)

この機能には、いくつかの制限があります。

* 抽出先に同じ名前のフォルダーが存在する場合、ZIP ファイル内のアセットは既存のフォルダーに抽出されます。
* 抽出をキャンセルしても、既に抽出されたアセットは削除されません。
* 2 つの ZIP ファイルを同時に選択して抽出することはできません。一度に抽出できる ZIP アーカイブは 1 つだけです。
* ZIP アーカイブをアップロードするときに、アップロードダイアログに 500 サーバーエラーが表示される場合は、最新のサービスパックをインストールしてから再試行してください。

## アセットのプレビュー {#previewing-assets}

アセットをプレビューするには、次の手順に従います。

1. Assets ユーザーインターフェイスで、プレビューするアセットの場所に移動します。
1. 目的のアセットをタップして開きます。

1. プレビューモードでは、[サポートされている画像タイプ](/help/assets/assets-formats.md#supported-raster-image-formats)で（インタラクティブ編集中に）ズームオプションを使用できます。

   アセットにズームインするには、`+` をタップまたはクリック（またはアセット上の虫眼鏡アイコンをタップまたはクリック）します。ズームアウトするには、`-` をタップまたはクリックします。ズームインすると、パンニングによって画像の任意の場所を詳細に確認できます。「ズームをリセット」矢印をクリックすると、元の表示に戻ります。

   **[!UICONTROL リセット]**&#x200B;をタップすると、表示を元のサイズに戻すことができます。

   ![リセットアイコンを使用して元の表示](assets/chlimage_1-11.png)

**プレビューキーのみを使用したキーボードアセット**

キーボードを使用してプレビューを行うには、次の手順に従います。

1. アセットユーザーインターフェイスから、および矢印キーを使用して目的のア `Tab` セットに移動します。

1. 目的の `Enter` アセットのキーを押して開きます。 アセットをズームインするには、プレビューモードを使用します。

1. アセットをズームインするには：
   1. ズームイ `Tab` ンアイコンにフォーカスを移動するには、Keyキーを使用します。
   1. キーを使 `Enter` 用して画像をズームインします。
   ズームアウトするには、 `Tab` キーを使用してズームアウトアイコンにフォーカスを移動し、を押しま `Enter`す。

1. +キーを `Shift` 使用 `Tab` して、画像にフォーカスを戻します。

1. 矢印キーを使用して、ズームされた画像の周りを移動します。

>[!MORELIKETHIS]
>
>* [プレビューダイナミックメディアアセット](/help/assets/previewing-assets.md)。
>* [サブアセットの表示](managing-linked-subassets.md#viewing-subassets).


## プロパティとメタデータの編集 {#editing-properties}

1. メタデータを編集するアセットの場所に移動します。

1. アセットを選択し、ツールバーの「**[!UICONTROL プロパティ]**」をタップまたはクリックして、アセットのプロパティを表示します。または、アセットカードで&#x200B;**[!UICONTROL プロパティ]**&#x200B;クイックアクションを選択します。

   ![アセットカードのプロパティクイックアクション表示](assets/properties_quickaction.png)

1. [!UICONTROL プロパティ]ページの様々なタブで、メタデータのプロパティを編集します。例えば、「**[!UICONTROL 基本]**」タブでは、タイトルや説明などを編集します。

   >[!NOTE]
   >
   >[!UICONTROL プロパティ]ページのレイアウトと編集できるメタデータのプロパティは、基になるメタデータスキーマによって変わります。[!UICONTROL プロパティ]ページのレイアウトを変更する方法については、[メタデータスキーマ](/help/assets/metadata-schemas.md)を参照してください。

1. アセットをアクティベートする特定の日付と時間をスケジュールするには、「**[!UICONTROL オンタイム]**」フィールドの横にある日付選択を使用します。

   ![日付の時間選択または「時間」フィールドのキーボードキーを使用して、アセットのアクティベーション](assets/schedule-activation.png)

   *図：スケジュールアセットのアクティベーション*

1. 特定の期間の後にアセットのアクティベートを解除するには、「**[!UICONTROL オフタイム]**」フィールドの横にある日付選択を使用して、アクティベートを解除する日付と時間を選択します。アクティベートを解除する日付は、アセットに設定されたアクティベート日より後の日付にしてください。[!UICONTROL オフタイム]の経過後、アセットとそのレンディションは、Assets Web インターフェイスでも HTTP API でも使用できません。

   ![日付の時間選択または「オフ時間」フィールドのキーボードキーを使用して、アセットのアクティベーション解除の日時を追加](assets/schedule-deactivation.png)

   *図：アセットの非アクティブ化のスケジュール*

1. 「**[!UICONTROL タグ]**」フィールドで、タグを 1 つ以上選択します。カスタムタグを追加するには、ボックスにタグの名前を入力し、Enter キーを押します。新しいタグが AEM に保存されます。YouTubeにはタグが必要です。 See [publish videos to YouTube](video.md#publishing-videos-to-youtube).

   >[!NOTE]
   >
   >タグを作成するには、CRXリポジトリでの書き込み権 `/content/cq:tags/default` 限が必要です。

1. アセットに評価を指定するには、「**[!UICONTROL 詳細]**」タブをタップまたはクリックし、適切な位置の星をタップまたはクリックして、目的の評価を割り当てます。

   ![評価を割り当てるアセットのプロパティの「詳細」タブ](assets/ratings.png)

   アセットに割り当てた評価スコアは、「**[!UICONTROL あなたの評価]**」の下に表示されます。ユーザーによるアセットの評価の平均スコアは、「**[!UICONTROL 評価]**」の下に表示されます。さらに、平均評価スコアの評価スコアの内訳は、「**[!UICONTROL 評価分類]**」の下に表示されます。平均評価スコアに基づいてアセットを検索できます。

1. アセットの使用状況の統計を確認するには、「**[!UICONTROL インサイト]**」タブをタップまたはクリックします。

   使用状況の統計には、次の情報が含まれています。

   * アセットが表示またはダウンロードされた回数
   * アセットが使用されたチャネルまたはデバイス
   * アセットが最近使用されたクリエイティブソリューション
   詳しくは、[アセットインサイト](/help/assets/touch-ui-asset-insights.md)を参照してください。

1. 「**[!UICONTROL 保存して閉じる]**」をタップまたはクリックします。
1. アセットユーザーインターフェイスに移動します。編集済みのメタデータのプロパティ（タイトル、説明、評価など）は、カード表示のアセットカードまたはリスト表示の関連する列に表示されます。

## アセットのコピー {#copying-assets}

アセットやフォルダーをコピーすると、そのアセットやフォルダーがコンテンツ構造と共にコピーされます。コピーされたアセットやフォルダーはコピー先に複製されます。コピー元にあるアセットは変更されません。

アセットの特定のコピーに一意に関連付けられる属性は継承されません。例えば、以下のものが該当します。

* アセットID、作成日時、バージョンとバージョン履歴。 Some of these properties are indicated by the properties `jcr:uuid`, `jcr:created`, and `cq:name`.

* 作成時間と参照パスは、各アセットとその各レンディションに対して一意です。

その他のプロパティとメタデータ情報は保持されます。アセットをコピーするときに、部分的なコピーが作成されることはありません。

1. Assets UI から 1 つ以上のアセットを選択し、ツールバーの「**[!UICONTROL コピー]**」アイコンをタップまたはクリックします。または、アセットカードから&#x200B;**[!UICONTROL コピー]**   クイックアクションを選択します。
   ![アセットUIツールバーのコピーアイコン](assets/copy_icon.png)

   >[!NOTE]
   >
   >[!UICONTROL コピー]クイックアクションを使用した場合、一度にコピーできるアセットは 1 つだけです。

1. アセットをコピーする場所に移動します。

   >[!NOTE]
   >
   >同じ場所でアセットをコピーすると、AEM は自動的に名前のバリエーションを生成します。例えば、「`Square`」というタイトルのアセットをコピーすると、AEM は自動的にそのコピーのタイトルを「`Square1`」として生成します。

1. Click/ tap the **[!UICONTROL Paste]** asset icon from the toolbar.

   ![アセットのUIツールバーの貼り付けアイコン](assets/chlimage_1-14.png)アセットがこの場所にコピーされます。

   >[!NOTE]
   >
   >ツールバーの&#x200B;**[!UICONTROL 貼り付け]**&#x200B;アイコンが使用できるのは、貼り付け操作が完了するまでです。

### アセットの移動または名前変更 {#moving-or-renaming-assets}

1. 移動するアセットの場所に移動します。

1. アセットを選択し、ツールバーの&#x200B;**[!UICONTROL 移動]**アイコン   をタップまたはクリックします。
   ![アセットUIツールバーの移動アイコン](assets/move_icon.png)

1. アセットを移動ウィザードで、次のいずれかの操作をおこないます。

   * 移動後のアセットの名前を指定します。その後、「**[!UICONTROL 次へ]**」をタップまたはクリックして先に進みます。

   * 「**[!UICONTROL キャンセル]**」をタップまたはクリックして、プロセスを停止します。
   >[!NOTE]
   >
   >* 新しい場所に同じ名前のアセットがない場合は、同じ名前を指定できます。ただし、アセットの移動先に同じ名前のアセットが既に存在する場合は、別の名前を使用する必要があります。同じ名前を使用すると、その名前のバリエーションが自動的に生成されます。例えば、「Square」という名前のアセットの場合、自動的にそのコピーの名前が「Square1」として生成されます。
   >* 名前の変更時に、ファイル名に空白は使用できません。


1. **[!UICONTROL 宛先を選択]**&#x200B;ダイアログで、次のいずれかの操作をおこないます。

   * アセットの移動先に移動し、「**[!UICONTROL 次へ]**」をタップまたはクリックして次に進みます。

   * 「**[!UICONTROL 戻る]**」をタップまたはクリックして、**[!UICONTROL 名前を変更]**&#x200B;画面に戻ります。

1. 移動されるアセットに参照ページ、アセット、コレクションがある場合は、「**[!UICONTROL 宛先を選択]**」タブの横に「**[!UICONTROL 参照を調整]**」タブが表示されます。

   **[!UICONTROL 参照を調整]**&#x200B;画面で次のいずれかの操作を実行します。

   * 新しい情報に基づいて調整する参照を指定し、「**[!UICONTROL 移動]**」をタップまたはクリックして次に進みます。

   * 「**[!UICONTROL 調整]**」列で、アセットへの参照を選択／選択解除します。
   * 「**[!UICONTROL 戻る]**」をタップまたはクリックして、**[!UICONTROL 宛先を選択]**&#x200B;画面に戻ります。

   * 「**[!UICONTROL キャンセル]**」をタップまたはクリックして、移動操作を停止します。
   参照を更新しなければ、引き続きアセットの以前のパスが示されます。参照を調整すると、更新され、アセットの新しいパスが反映されます。

## レンディションの管理 {#managing-renditions}

1. アセットのレンディション（オリジナルを除く）を追加または削除できます。レンディションを追加または削除するアセットの場所に移動します。

1. アセットをタップまたはクリックして、そのアセットページを開きます。

   ![chlimage_1-220](assets/chlimage_1-15.png)

1. グローバルナビゲーションアイコンをタップまたはクリックし、リストから「**[!UICONTROL レンディション]**」を選択します。

   ![renditions_menu](assets/renditions_menu.png)

1. **[!UICONTROL レンディション]**&#x200B;パネルで、アセットに生成されたレンディションのリストを表示します。

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >デフォルトで、AEM Assets はプレビューモードでアセットのオリジナルレンディションを表示しません。管理者の場合、オーバーレイを使用して AEM Assets を設定し、プレビューモードでもオリジナルレンディションを表示できます。

1. 表示または削除するレンディションを選択します。

   **レンディションの削除**

   **[!UICONTROL レンディション]**&#x200B;パネルからレンディションを選択し、ツールバーの「**[!UICONTROL レンディションを削除]**」アイコンをタップまたはクリックします。

   ![レンディションを削除するオプション](assets/delete_renditionicon.png)

   **新しいレンディションのアップロード**

   アセットの詳細ページに移動し、ツールバーの「**[!UICONTROL レンディションを追加]**」アイコンをタップまたはクリックして、アセットの新しいレンディションをアップロードします。

   ![chlimage_1-221](assets/chlimage_1-16.png)

   >[!NOTE]
   >
   >**[!UICONTROL レンディション]**&#x200B;パネルからレンディションを選択する場合、ツールバーのコンテキストが変わり、レンディションに関連するアクションのみが表示されます。レンディションをアップロードアイコンなどのオプションは表示されません。これらのオプションをツールバーに表示するには、アセットの詳細ページに移動します。

   画像またはビデオアセットの詳細ページに表示するレンディションのサイズを設定できます。指定するサイズに基づいて、AEM Assets はレンディションを正確なサイズまたは最も近いサイズで表示します。

   アセットの詳細レベルで画像のレンディションのサイズを設定するには、`renditionpicker` ノード（`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`）をオーバーレイして、幅のプロパティの値を設定します。画像サイズに基づいてアセットの詳細ページでレンディションをカスタマイズするには、幅の代わりに **[!UICONTROL size (Long) in KB]** プロパティを設定します。サイズベースのカスタマイズの場合、`preferOriginal` プロパティを使用すると、一致するレンディションのサイズがオリジナルより大きい場合でも、オリジナルが優先されます。

   同様に、`libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker` をオーバーレイして注釈ページの画像をカスタマイズできます。

   ![chlimage_1-222](assets/chlimage_1-17.png)

   ビデオアセットのレンディションサイズを設定するには、CRX リポジトリ内の `videopicker` ノード（`/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`）に移動し、ノードをオーバーレイし、該当するプロパティを編集します。

   >[!NOTE]
   >
   >ビデオの注釈は、HTML5 互換のビデオ形式に対応したブラウザーでのみサポートされます。また、ブラウザーによってサポートされるビデオ形式が異なります。

サブアセットの生成と表示について詳しくは、「サブアセットの管理」を [参照してくださ](managing-linked-subassets.md#generate-subassets)い。

## アセットの削除 {#deleting-assets}

他のページからの入力参照を解決または削除するには、アセットを削除する前に、関連する参照を更新します。

また、オーバーレイを使用して「削除を強制」ボタンを無効にすることで、参照元のアセットの削除と壊れたリンクの放置を禁止します。

1. 削除するアセットの場所に移動します。

1. アセットを選択し、ツールバーの「**[!UICONTROL 削除]**」アイコンをタップまたはクリックします。

   ![delete_icon](assets/delete_icon.png)

1. 確認ダイアログで、次のいずれかをクリックします。

   * **[!UICONTROL キャンセル]**：アクションを停止します。
   * **[!UICONTROL 削除]**：アクションの実行を確定します。

      * アセットに参照がない場合は、アセットが削除されます。
      * アセットに参照がある場合は、「**1 つ以上のアセットが参照されています。**」というエラーメッセージが表示されます。「**[!UICONTROL 削除を強制]**」または「**[!UICONTROL キャンセル]**」を選択できます。
   >[!NOTE]
   >
   >アセットを削除するには、ユーザーがに対する削除権限が必要で `dam/asset`す。 変更権限のみ付与されている場合、アセットのメタデータの編集とアセットへの注釈の追加のみが可能で、アセットやそのメタデータの削除は実行できません。

   >[!NOTE]
   >
   >他のページからの入力参照を解決または削除するには、アセットを削除する前に、関連する参照を更新します。また、オーバーレイを使用して「削除を強制」ボタンを無効にすることで、参照元のアセットの削除と壊れたリンクの放置を禁止します。

## アセットのダウンロード {#downloading-assets}

[AEM からのアセットのダウンロード](/help/assets/download-assets-from-aem.md)を参照してください。

## アセットの公開 {#publishing-assets}

>[!NOTE]
>
>Dynamic Media 特有の追加情報については、[Dynamic Media アセットの公開](/help/assets/publishing-dynamicmedia-assets.md)を参照してください。

1. 発行するアセットまたはフォルダーの場所に移動します。

1. アセットカードで&#x200B;**[!UICONTROL 公開]**&#x200B;クイックアクションを選択するか、アセットを選択し、ツールバーの「**[!UICONTROL クイック公開]**」アイコンをタップまたはクリックします。
1. アセットが他のアセットを参照する場合は、その参照がウィザードに表示されます。表示されるのは、非公開の参照か、最後に公開または非公開にされた後に変更された参照だけです。公開する参照を選択します。

   >[!NOTE]
   >
   >公開したフォルダの一部である空のフォルダは、公開されません。

1. 「**[!UICONTROL 公開]**」をタップまたはクリックして、アセットのアクティベートを確認します。

>[!CAUTION]
>
>処理中のアセットを公開した場合は、オリジナルのコンテンツのみが公開されます。処理中のレンディションは失われます。処理が完了するまで待ってから公開するか、処理の完了後にアセットを公開し直してください。

## アセットの非公開 {#unpublishing-assets}

1. パブリッシュ環境から削除する（非公開にする）アセットまたはアセットフォルダーの場所に移動します。

1. 非公開にするアセットまたはフォルダーを選択し、ツールバーの「**[!UICONTROL 公開を管理]**」アイコンをタップまたはクリックします。

   ![manage_publication](assets/manage_publication.png)

1. リストから「**[!UICONTROL 非公開]**」アクションを選択します。

   ![unpublish_action](assets/unpublish_action.png)

1. 後でアセットを非公開にするには、「**[!UICONTROL 後で非公開にする]**」を選択して、アセットを非公開にする日付を選択します。
1. パブリッシュ環境でアセットを非公開にする日付をスケジュールします。
1. アセットが他のアセットを参照する場合は、非公開にする参照を選択します。「**[!UICONTROL 非公開]**」をタップまたはクリックします。
1. 確認ダイアログで、次のいずれかをタップまたはクリックします。

   * **[!UICONTROL キャンセル]**：アクションを停止します。
   * **[!UICONTROL 非公開]**：指定された日付にアセットを非公開にします（パブリッシュ環境では使用できません）。
   >[!NOTE]
   >
   >複雑なアセットを非公開にする場合は、アセットだけを非公開にします。参照は他の公開済みアセットから参照されている可能性があるので、非公開にしないでください。

## 閉じられたユーザーグループ {#closed-user-group}

閉じられたユーザーグループ（CUG）は、AEM から公開された特定のアセットフォルダーへのアクセスを制限するために使用します。フォルダーに対して CUG を作成すると、そのフォルダー（フォルダーのアセットとサブフォルダーを含む）へのアクセスは、割り当てられたメンバーまたはグループのみに制限されます。フォルダーにアクセスするには、セキュリティ資格情報を使用してログインする必要があります。

CUG は、アセットへのアクセスを制限する追加の方法です。また、フォルダーのログインページを設定することもできます。

1. Assets UI からフォルダーを選択し、ツールバーの「プロパティ」アイコンをタップまたはクリックして、プロパティページを表示します。
1. 「**[!UICONTROL 権限]**」タブで、「**[!UICONTROL 閉じられたユーザーグループ]**」の下でメンバーまたはグループを追加します。

   ![add_user](assets/add_user.png)

1. ユーザーがフォルダーにアクセスしたときにログイン画面を表示するには、「**[!UICONTROL 有効]**」オプションを選択します。次に、AEM 内のログインページへのパスを選択し、変更を保存します。

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >ログインページへのパスを指定しないと、AEM はパブリッシュインスタンスでデフォルトのログインページを表示します。

1. フォルダーを公開し、パブリッシュインスタンスからアクセスすると、ログイン画面が表示されます。
1. CUG メンバーの場合は、自分のセキュリティ資格情報を入力します。AEM によって認証されると、フォルダーが表示されます。

## アセットの検索 {#assetsearch}

アセットの検索は、デジタルアセット管理システムの利用の中核を成します。用途は、クリエイティブ担当者によるさらなる利用、ビジネスユーザーやマーケティング担当者によるアセットの堅牢な管理、DAM 管理者による管理などです。

最も適切なアセットを検出し使用するためのシンプル検索、アドバンス検索、カスタム検索については、[AEM でのアセットの検索](search-assets.md)を参照してください。

## クイックアクション {#quick-actions}

クイックアクションのアイコンは、一度に 1 つのアセットに対してのみ利用できます。デバイスに応じて、次の操作を実行してクイックアクションアイコンを表示します。

* タッチデバイス：タッチ＆ホールド。例えば iPad では、アセットをタップ＆ホールドするとクイックアクションが表示されます。
* 非タッチデバイス：マウスポインターで指す。例えばデスクトップデバイスでは、アセットのサムネールをマウスポインターで指すとクイックアクションバーが表示されます。

### アセットの移動と選択 {#navigating-and-selecting-assets}

You can view, navigate through, and select assets with any of the available views (Card, Column, and List) using the **[!UICONTROL Select]** option.

リスト表示と列表示で、アセッ **[!UICONTROL トのサムネールに]** （ポインターを合わせたとき）「選択」オプションが表示されます。

![select_quick_in_listview](assets/select_quick_in_listview.png)

![select_quick_in_columnview](assets/select_quick_in_columnview.png)

カード表示では、「 **[!UICONTROL Select]** 」オプションがクイックアクションとして表示されます。

![select_quick_action](assets/select_quick_action.png)

ブラウザのアセットユーザインターフェイスでフォルダまたはコレクションを参照する場合、右上隅の「すべて選択」オプションを使用して、表示または読み込まれたすべてのアセットを  「選択」で選択できます。 最初は、100個のアセットのみがカード表示に読み込まれ、200個のアセットがリスト表示に読み込まれます。 検索結果ページをスクロールすると、表示に読み込まれるアセットが増えます。 「すべて [!UICONTROL 選択] 」オプションは、読み込まれたアセットのみを選択します。

For more information, see [view and selecting your resources](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).

## 画像の編集 {#editing-images}

AEM Assets インターフェイスの編集ツールを使用すると、画像アセットで細かい編集ジョブを実行できます。画像に対して切り抜き、回転、反転などの編集ジョブを実行できます。アセットに画像マップを追加することもできます。

>[!NOTE]
>
>一部のコンポーネントでは、全画面表示モードで追加のオプションも使用できます。

1. 編集モードでアセットを開くには、次のいずれかの操作をおこないます。

   * アセットを選択し、ツールバーの「**[!UICONTROL 編集]**」アイコンをクリックまたはタップします。
   * カード表示で、アセットに表示される「**[!UICONTROL 編集]**」アイコンをタップまたはクリックします。
   * アセットページで、ツールバーの「**[!UICONTROL 編集]**」アイコンをタップまたはクリックします。
   ![edit_icon](assets/edit_icon.png)

1. 画像を切り抜くには、**切り抜き**&#x200B;アイコンをタップまたはクリックします。

   ![chlimage_1-226](assets/chlimage_1-22.png)

1. リストから必要なオプションを選択します。選択したオプションに基づいて、画像に切り抜き領域が表示されます。「**フリーハンド**」オプションを使用すると、縦横比の制限に関係なく画像を切り抜くことができます。

   ![chlimage_1-227](/help/assets/assets/chlimage_1-23.png)

1. 切り抜く領域を選択し、画像上でそのサイズまたは位置を変更します。
1. **完了**&#x200B;アイコン（右上隅）を使用して、画像を切り抜きます。**完了**&#x200B;アイコンをクリックすると、レンディションの再生成もおこなわれます。

   ![chlimage_1-228](assets/chlimage_1-24.png)

1. 切り抜く前の画像に戻すには、右上の&#x200B;**取り消し**&#x200B;アイコンを使用します。切り抜いた画像を保持するには、右上の&#x200B;**やり直し**&#x200B;アイコンを使用します。

   ![chlimage_1-229](assets/chlimage_1-25.png)

1. 適切な回転アイコンをタップまたはクリックして、画像を時計回りまたは反時計回りに回転します。

   ![chlimage_1-230](assets/chlimage_1-26.png)

1. 適切な反転アイコンをタップまたはクリックして、画像を水平方向または垂直方向に反転します。

   ![chlimage_1-231](assets/chlimage_1-27.png)

1. **完了**&#x200B;アイコンをタップまたはクリックして変更を保存します。

   ![chlimage_1-232](assets/chlimage_1-28.png)

>[!NOTE]
>
>BMP、GIF、PNG、JPEG の各ファイル形式については、画像編集がサポートされています。

画像エディターを使用して画像マップを追加することもできます。詳しくは、[画像マップの追加](/help/assets/image-maps.md)を参照してください。

>[!NOTE]
>
>TXT ファイルを編集するには、Configuration Manager で **Day CQ Link Externalizer** を設定します。

## タイムライン {#timeline}

タイムラインを使用すると、アセットのアクティブなワークフロー、コメントや注釈、アクティビティログ、バージョンなど、選択した項目の様々なイベントを表示できます。

![アセットのタイムラインエントリの並べ替え](assets/sort_timeline.gif)

*図：アセットのタイムラインエントリの並べ替え*

>[!NOTE]
>
>[コレクションコンソール](/help/assets/managing-collections-touch-ui.md#navigating-the-collections-console)の&#x200B;**[!UICONTROL すべて表示]**&#x200B;リストには、コメントとワークフローだけを表示するオプションがあります。さらに、タイムラインはコンソールにリストされているトップレベルのコレクションについてのみ表示されます。これらのコレクション内を移動する場合、タイムラインは表示されません。

>[!NOTE]
>
>タイムラインには、[コンテンツフラグメントに固有のオプション](/help/assets/content-fragments-managing.md#timeline-for-content-fragments)がいくつか含まれています。

## アセットに注釈を付ける {#annotating}

注釈とは、画像やビデオに追加するコメントまたは注記です。マーケティング担当者は、注釈により、アセットについてコラボレーションし、フィードバックを残すことができます。

ビデオの注釈は、HTML5 互換のビデオ形式に対応したブラウザーでのみサポートされます。AEM Assets がサポートするビデオの形式は、ブラウザーによって異なります。

>[!NOTE]
>
>コンテンツフラグメントの場合、[注釈はフラグメントエディターで作成されます](/help/assets/content-fragments-variations.md#annotating-a-content-fragment)。

1. 注釈を追加するアセットの場所に移動します。
1. 以下のいずれかから&#x200B;**[!UICONTROL 注釈]**&#x200B;アイコンをタップまたはクリックします。

   * [クイックアクション](/help/assets/managing-assets-touch-ui.md#quick-actions)
   * アセットを選択した後またはアセットページに移動した後に、ツールバーから
   ![chlimage_1-233](assets/chlimage_1-29.png)

1. タイムラインの一番下の&#x200B;**[!UICONTROL コメント]**&#x200B;ボックスにコメントを追加します。または、画像内の任意の領域をマークアップし、**[!UICONTROL 注釈を追加]**&#x200B;ダイアログに注釈を追加します。

   ![chlimage_1-234](assets/chlimage_1-30.png)

1. 注釈についてユーザーに通知するには、ユーザーの電子メールアドレスを指定して、コメントを追加します。例えば、注釈について Aaron MacDonald というユーザーに通知するには、@aa と入力します。一致するすべてのユーザーに関するヒントがリストに表示されます。Aaron の電子メールアドレスをリストから選択し、コメントを使用してタグ付けします。同様に、注釈内の任意の場所、またはコメントの前後で追加のユーザーにタグ付けできます。

   >[!NOTE]
   >
   >管理者以外のユーザーには、Crx-de で */home* に読み取り権限がある場合にのみ候補が表示されます。

   ![chlimage_1-235](assets/chlimage_1-31.png)

1. 注釈を追加したら、「**[!UICONTROL 追加]**」をクリックして注釈を保存します。注釈に関する通知が Aaron に送信されます。

   ![chlimage_1-236](assets/chlimage_1-32.png)

   >[!NOTE]
   >
   >複数の注釈を追加してから、それらを保存できます。

1. 「**[!UICONTROL 閉じる]**」をタップまたはクリックして注釈モードを終了します。
1. 通知を表示するには、Aaron MacDonald の資格情報を使用して AEM Assets にログインし、「**[!UICONTROL 通知]**」アイコンをクリックします。

   >[!NOTE]
   >
   >注釈はビデオアセットにも追加できます。ビデオに注釈を追加する際は、ユーザーがフレームに注釈を追加できるようにプレーヤーが一時停止します。詳しくは、[ビデオアセットの管理](/help/assets/managing-video-assets.md)を参照してください。

1. 別の色を選択してユーザーを区別できるようにするには、プロファイルアイコンをクリックまたはタップし、「**[!UICONTROL 環境設定]**」をクリックまたはタップします。

   ![ユーザープロファイルアイコンを選択し、「環境設定」を選択して、「ユーザー環境設定」を開きます](assets/User-profile-preferences.png)

   **[!UICONTROL 注釈カラー]**&#x200B;ボックスに必要な色を指定し、**[!UICONTROL 確定]**&#x200B;をクリックまたはタップします。

   ![ユーザ環境設定で注釈の色を選択し、ユーザペルソナの色を設定](assets/Annotation-color.png)

>[!NOTE]
>
>コレクションにも注釈を追加できます。ただし、コレクションに子コレクションが含まれる場合、親コレクションに対してのみ注釈／コメントを追加できます。「注釈」オプションは子コレクションでは使用できません。

### 保存された注釈の表示 {#viewing-saved-annotations}

1. アセットに対して保存された注釈を表示するには、アセットの場所に移動して、そのアセットのアセットページを開きます。

1. グローバルナビゲーションアイコンをタップまたはクリックし、リストから「**[!UICONTROL タイムライン]**」を選択します。

   ![chlimage_1-239](assets/chlimage_1-35.png)

1. タイムラインの「**[!UICONTROL すべて表示]**」のリストから「**[!UICONTROL コメント]**」を選択し、注釈に基づいて結果にフィルターを適用します。

   ![chlimage_1-240](assets/chlimage_1-36.png)

   **[!UICONTROL タイムライン]**&#x200B;パネルでコメントをタップまたはクリックし、対応する画像の注釈を表示します。

   ![chlimage_1-241](assets/chlimage_1-37.png)

   特定のコメントを削除するには、「**[!UICONTROL 削除]**」をタップまたはクリックします。

### 注釈の印刷 {#printing-annotations}

アセットに注釈がある場合や、レビューワークフローの対象になっている場合は、オフラインでのレビュー用に注釈とレビューステータス付きでアセットを PDF ファイルとして印刷できます。

注釈またはレビューステータスのみ印刷することも選択できます。

注釈とレビューステータスを印刷するには、**[!UICONTROL 印刷]**&#x200B;アイコンをタップまたはクリックし、ウィザードの指示に従ってください。**[!UICONTROL 印刷]**&#x200B;アイコンは、アセットに注釈またはレビューステータスが少なくとも 1 つ割り当てられている場合にのみ、ツールバーに表示されます。

1. Assets UI から、アセットのプレビューページを開きます。
1. 次のいずれかの操作をおこないます。

   * すべての注釈とレビューステータスを印刷するには、手順 3 をスキップして手順 4 に直接進みます。
   * 特定の注釈やレビューステータスを印刷するには、[タイムライン](/help/assets/managing-assets-touch-ui.md#timeline)を開き、手順 3 に進みます。

1. 特定の注釈を印刷するには、タイムラインから注釈を選択します。

   ![chlimage_1-242](assets/chlimage_1-38.png)

   レビューステータスのみを印刷するには、タイムラインからレビューステータスを選択します。

   ![chlimage_1-243](assets/chlimage_1-39.png)

1. ツールバーの&#x200B;**[!UICONTROL 印刷]**&#x200B;アイコンをタップまたはクリックします。

   ![chlimage_1-244](assets/chlimage_1-40.png)

1. 印刷ダイアログから、注釈／レビューステータスを PDF のどこに表示したいかを選択します。例えば、印刷する画像が含まれるページの右上に注釈／ステータスを印刷したい場合は、「**左上**」設定を使用します。デフォルトで選択されています。

   ![印刷ダイアログからPDFに表示する注釈/レビューステータスの位置を選択](assets/Print-annotation-dialog.png)

   印刷する PDF のどこに注釈／ステータスを表示するかに応じて、別の設定も選択できます。印刷されるアセットとは別のページに注釈／ステータスを表示したい場合、「**[!UICONTROL 次のページ]**」を選択します。

   >[!NOTE]
   >
   >長い注釈は PDF ファイルに適切にレンダリングされない可能性があります。最適なレンダリングのために、注釈を 50 語以内に制限することをお勧めします。

1. 「**[!UICONTROL 印刷]**」をタップまたはクリックします。手順 2 で選択したオプションに応じて、生成される PDF の特定の位置に注釈／ステータスが表示されます。例えば、注釈とレビューステータスの両方を「**左上**」設定を使用して印刷することを選択した場合、生成される PDF ファイルは次のようになります。

   ![chlimage_1-246](assets/chlimage_1-42.png)

1. 右上のオプションを使用して PDF をダウンロードまたは印刷します。

   ![chlimage_1-247](assets/chlimage_1-43.png)

   >[!NOTE]
   >
   >アセットにサブアセットがある場合、特定のページに関する注釈と共にすべてのサブアセットを印刷できます。

   レンダリングされた PDF ファイルの外観を変更するには、Configuration Manager から&#x200B;**[!UICONTROL 注釈 PDF の設定]**&#x200B;を開き、必要なオプションを変更します。例えば、コメントとステータスのフォントカラー、サイズ、スタイル、背景色を変更できます。例えば、承認済みステータスの表示色を変更したり、対応フィールドのカラーコードを変更したりします。注釈のフォントカラーの変更について詳しくは、[注釈](/help/assets/managing-assets-touch-ui.md#annotating)を参照してください。

   ![chlimage_1-248](assets/chlimage_1-44.png)

   レンダリングされた PDF ファイルに戻り、更新します。更新された PDF に、変更が反映されています。

アセットに外国語（特に非ラテン言語）の注釈が含まれる場合、これらの注釈を印刷するには、まず AEM サーバーで CQ-DAM-Handler-Gibson Font Manager サービスを設定する必要があります。CQ-DAM-Handler-Gibson Font Manager サービスの設定では、必要な言語のフォントがある場所を指定します。

1. CQ-DAM-Handler-Gibson Font Manager サービスの設定ページを、URL `https://[aem_server]:[port]/system/console/configMgr/com.day.cq.dam.handler.gibson.fontmanager.impl.FontManagerServiceImpl` から開きます。
1. CQ-DAM-Handler-Gibson Font Manager サービスを設定するには、以下のいずれかをおこないます。

   * 「システムフォントディレクトリ」オプションで、システムのフォントディレクトリの完全パスを指定する。例えば Mac ユーザーの場合、「システムフォントディレクトリ」オプションで */Library/Fonts* と指定します。AEM はこのディレクトリからフォントを取得します。
   * `fonts` フォルダー内に ``crx-quickstart`` という名前のディレクトリを作成する。CQ-DAM-Handler-Gibson Font Manager サービスは `crx-quickstart/fonts` からフォントを自動的に取得します。「Adobe サーバーフォントディレクトリ」オプション内でデフォルトパスを上書きすることができます。

   * システムにフォント用の新しいフォルダーを作成し、必要なフォントをこのフォルダーに保存する。次に、「カスタマーフォントディレクトリ」オプションにこのフォルダーへの完全パスを指定します。

1. URL `https://[aem_server]:[4502]/system/console/configMgr/com.day.cq.dam.core.impl.annotation.pdf.AnnotationPdfConfig` から注釈 PDF の設定にアクセスします。
1. 以下のように、正しいフォントファミリのセットを使用して注釈 PDF を設定します。

   * 文字列 `<font_family_name_of_custom_font, sans-serif>` をフォントファミリオプションに含めます。例えば、注釈を CJK（中国語、日本語、韓国語）で印刷したい場合、フォントファミリオプションに文字列 `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif` を含めます。ヒンディー語の注釈を印刷したい場合、適切なフォントをダウンロードし、フォントファミリを Arial Unicode MS, Noto Sans, Noto Sans CJK JP, Noto Sans Devanagari, sans-serif として設定します。

1. AEM インスタンスを再起動します。

以下の例は、注釈を CJK（中国語、日本語、韓国語）で印刷する場合の AEM の設定方法を示しています。

1. 以下のリンクから Google Noto CJK フォントをダウンロードし、Font Manager サービスで設定したフォントディレクトリに保存します。

   * All In One Super CJK フォント：[https://www.google.com/get/noto/help/cjk/](https://www.google.com/get/noto/help/cjk/)
   * Noto Sans（欧文用）：[https://www.google.com/get/noto/](https://www.google.com/get/noto/)
   * 選択した言語用の Noto フォント：[https://www.google.com/get/noto/](https://www.google.com/get/noto/)

1. フォントファミリパラメーターを `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif` に設定して、注釈 PDF ファイルを設定します。この設定はデフォルトで使用でき、すべての欧文および CJK 言語で機能します。
1. 選択した言語が手順 2 の言語と異なる場合は、デフォルトフォントファミリに適切なエントリを（コンマで区切って）追加してください。

## アセットのバージョンの作成、管理、プレビューおよび元に戻す {#asset-versioning}

バージョン管理では、特定の時点でのデジタルアセットのスナップショットが作成されます。バージョン管理を使用すると、後で、以前の状態にアセットを復元できます。例えば、アセットに対しておこなった変更を取り消したい場合、バージョン管理を使用して未編集のバージョンにアセットを復元できます。Experience Managerでは、表示を作成し、現在のリビジョンを表示し、画像の2つのバージョン間で画像を左右に並べて比較し、アセットを以前のバージョンに戻すことができます。

次のシナリオで、Experience Managerでバージョンを作成できます。

* 同じ場所に存在するのと同じファイル名でアセットをアップロードします。 新しいアセット、または同じアセットの変更済みバージョンを使用できます。
* Experience Managerで画像を編集し、変更を保存します。
* アセットのメタデータを編集します。
* AEMデスクトップアプリを使用して、既存のアセットをチェックアウトし、編集して、変更をア [ップロードします](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#edit-assets-upload-updated-assets)。

また、ワークフローを使用して、自動バージョン管理を有効にすることもできます。アセットのバージョンを作成すると、バージョンと共にメタデータとレンディションが保存されます。レンディションによって、同じ画像の代替となる画像が表示されます（例えば、アップロードされた JPEG ファイルの PNG レンディション）。

1. バージョンを作成するアセットの場所に移動し、そのアセットをクリックして開きます。プレビュー ページの左上隅からメニューを開き、「タイムライン」を選択し **[!UICONTROL ます]**。

   ![左側のナビゲーションメニューで、タイムラインオプションを選択します](assets/timeline.png)

   *図：ページの左上の領域からメニューを開き、「タイムライン」オプション[!UICONTROL を選択し]ます。*

1. アセットのバージョンを作成するには：

   * Click the **[!UICONTROL Actions]** at the bottom.
   * 「**[!UICONTROL 保存するバージョン]**」をクリックして、アセットのバージョンを作成します。オプションで、ラベルとコメントを追加します。
   * Click **[!UICONTROL Create]** to create a version.

      ![chlimage_1-251](assets/create-new-version-from-timeline.png)

      *図：タイムラインの左側のサイドバーからアセットのバージ[!UICONTROL ョンを]作成します。*

1. アセットの表示を行うには：

   * タイムライ **[!UICONTROL ンで「すべてを表示]** 」をク [!UICONTROL リックしま]す。
   * 「バージョン」 **[!UICONTROL をクリックしま]**&#x200B;す。 アセット用に作成されたすべてのバージョンが左側のサイドバーに表示されます。

      ![versions_option](assets/versions_option.png)

   * アセットの特定のバージョンを選択し、「バージョン」をク **[!UICONTROL プレビューしま]**&#x200B;す。

1. 古いバージョンのアセットに戻すには、次の手順を実行します。 元に戻すと、このバージョンがインターフェイスに表示 [!DNL Assets] され、使用できるようになります。

   * アセットのバージョンをクリックします。 オプションで、ラベルとコメントを追加します。
   * Click **[!UICONTROL Revert to this Version]**.

      ![select_version](assets/select_version.png)

      *図：バージョンを選択し、元に戻します。 DAMユーザーが使用できる現在のバージョンになります。*

1. 2つのバージョンの画像を比較するには、次の手順に従います。
   * 現在のバージョンと比較するバージョンをクリックします。
   * スライダを左にドラッグして、このバージョンを現在のバージョンに重ねて比較します。
   ![スライダを使用して、選択したバージョンのアセットと現在のバージョンを比較します。](assets/version-slider.gif)

   *図：スライダを使用して、選択したバージョンのアセットと現在のバージョンを簡単に比較できます。*

### Start a workflow on an asset {#starting-a-workflow-on-an-asset}

ワークフローを適用してアセットを処理する方法については、アセットに対する [開始ワークフローを参照してくださ](/help/assets/assets-workflow.md#apply-a-workflow-to-an-asset)い。

## コレクション {#collections}

コレクションとは、一連のアセットを順序よく並べたものです。コレクションを使用して、関連するアセットをユーザー間で共有したり、類似のアセットをクラスター化して、簡単に見つけることができます。

* 1 つのコレクションにはアセットへの参照のみが含まれるので、様々な場所のアセットを含めることができます。各コレクションは、アセットの参照整合性を維持します。
* コレクションは、特権レベル（編集、表示など）の異なる複数のユーザー間で共有できます。

See [manage collections](/help/assets/managing-collections-touch-ui.md) for details on collection management.
