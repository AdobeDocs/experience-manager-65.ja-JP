---
title: 'ビデオ '
seo-title: Video
description: Assets では、ビデオアセットを統合管理できます。ビデオを直接 Assets にアップロードして Dynamic Media Classic に対する自動エンコーディングを行ったり、Assets から直接 Dynamic Media Classic ビデオにアクセスしてページオーサリングを行ったりできます。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: b5cf18d8e83786a23005aadf8aafe43d006a2e67
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 100%

---

# ビデオ {#video}

Assets では、ビデオアセットを統合管理できます。ビデオを直接 Assets にアップロードして Dynamic Media Classic に対する自動エンコーディングを行ったり、Assets から直接 Dynamic Media Classic ビデオにアクセスしてページオーサリングを行ったりできます。

Dynamic Media Classic ビデオの統合により、最適化されたビデオの範囲をすべての画面に拡大します（デバイスと帯域幅の自動検出）。

* Dynamic Media Classic ビデオコンポーネントでは、デスクトップ、タブレットおよびモバイルで適切な形式と画質を使用してビデオを再生するために、デバイスと帯域幅を自動的に検出します。
* Assets - 単一のビデオアセットだけでなく、アダプティブビデオセットを含めることもできます。アダプティブビデオセットは、複数の画面にまたがってシームレスにビデオを再生するために必要なビデオレンディションをすべて含んだコンテナです。 アダプティブビデオセットでは、同じビデオを、400 kbps、800 kbps、1000 kbps などの様々なビットレートと形式でエンコードしたバージョンにグループ分けします。デスクトップ、iOS、Android™、BlackBerry®、Windows モバイルデバイスなど、複数の画面にまたがるアダプティブビデオのストリーミングには、S7 ビデオコンポーネントと共にアダプティブビデオセットを使用します。 詳しくは、[アダプティブビデオセットに関する Dynamic Media Classic のドキュメント](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html?lang=ja#video)を参照してください。

## FFMPEG と Dynamic Media Classic について {#about-ffmpeg-and-scene}

デフォルトのビデオエンコーディングプロセスは、FFMPEG ベースでビデオプロファイルと統合することを基にしています。そのため、標準の [!UICONTROL DAM アセットの更新]ワークフローには、ffmpeg ベースの次の 2 つのステップが含まれています。

* FFMPEG のサムネイル
* FFMPEG エンコーディング

Dynamic Media Classic 統合を有効にして設定を行っても、この 2 つのワークフローのステップは、標準の「[!UICONTROL DAM アセットの更新]」取り込みワークフローから自動的に削除されたりアクティベートが解除されたりしません。FFMPEG ベースのビデオエンコーディングを Adobe Experience Manager で既に使用している場合は、オーサリング環境に FFMPEG がインストールされている可能性があります。この場合、Experience Manager Assets を使用して取り込まれた新しいビデオは 2 回エンコードされます。FFMPEG エンコーダーから 1 回、Dynamic Media Classic 統合から 1 回です。

Experience Manager で FFMPEG ベースのビデオエンコーディングが設定済みで、FFMPEG がインストールされている場合は、この 2 つの FFMPEG ワークフローを [!UICONTROL DAM アセットの更新]ワークフローから削除することをお勧めします。

### サポートされるファイル形式 {#supported-formats}

Dynamic Media Classic ビデオコンポーネントでは次の形式がサポートされます。

* F4V H.264
* MP4 H.264

### ビデオのアップロード先を指定 {#deciding-where-to-upload-your-video}

ビデオアセットのアップロード先の指定は、次の条件によって決まります。

* ビデオアセットのワークフローが必要かどうか
* ビデオアセットのバージョン管理が必要かどうか

これらの質問のいずれかまたは両方に対する回答が「はい」の場合は、ビデオを Adobe DAM に直接アップロードします。両方の質問に対する回答が「いいえ」の場合は、ビデオを Dynamic Media Classic に直接アップロードします。次の節では、各シナリオのワークフローについて説明します。

#### ビデオを直接 Adobe Assets にアップロードする場合 {#if-you-are-uploading-your-video-directly-to-adobe-assets}

アセットのワークフローまたはバージョン管理が必要な場合は、まず Adobe Assets にアップロードする必要があります。推奨されるワークフローは次のとおりです。

1. Adobe Assets にビデオアセットをアップロードして、Dynamic Media Classic に自動的にエンコードして公開します。
1. Experience Manager の WCM（コンテンツファインダーの「**[!UICONTROL ムービー]**」タブ）で、ビデオアセットにアクセスします。
1. Dynamic Media Classic ビデオまたは基盤ビデオコンポーネントを使用して作成します。

#### ビデオを Dynamic Media Classic にアップロードする場合 {#if-you-are-uploading-your-video-to-scene}

アセットのワークフローやバージョン管理が不要な場合、Dynamic Media Classic にアセットをアップロードします。推奨されるワークフローは次のとおりです。

1. Dynamic Media Classic デスクトップアプリケーションで、[Dynamic Media Classic（システム自動化）へのスケジュールされた FTP アップロードとエンコーディングを設定](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html?lang=ja#upload-options)します。
1. Experience Manager で、コンテンツファインダーの「**[!UICONTROL Dynamic Media Classic]**」タブにある WCM のビデオアセットにアクセスします。
1. Dynamic Media Classic ビデオコンポーネントを使用して作成します。

### Dynamic Media Classic ビデオとの統合の設定 {#configuring-integration-with-scene-video}

1. **[!UICONTROL Cloud Services]** で **[!UICONTROL Dynamic Media Classic]** の設定に移動し、「**[!UICONTROL 編集]**」を選択します。
1. 「**[!UICONTROL ビデオ]**」タブを選択します。

   >[!NOTE]
   >
   >クラウド設定がページにない場合は、「**[!UICONTROL ビデオ]**」タブが表示されません。詳しくは、[WCM 用 Dynamic Media Classic の有効化](#enablingscene7forwcm)を参照してください。

1. アダプティブビデオのエンコーディングプロファイル、単一の標準ビデオのエンコーディングプロファイル、またはカスタムビデオのエンコーディングプロファイルを選択します。

   >[!NOTE]
   >
   >ビデオプリセットの意味について詳しくは、 [ビデオファイルをエンコーディングするためのビデオプリセット](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=ja#video-presets-for-encoding-video-files)を参照してください。
   >
   >ユニバーサルプリセットを設定する際に両方のアダプティブビデオセットを選択するか、「**[!UICONTROL アダプティブビデオエンコーディング]**」オプションを選択することをお勧めします。

1. 選択したエンコーディングプロファイルは、CQ DAM のターゲットフォルダーにアップロードされたすべてのビデオに自動的に適用されます。このフォルダーは、Dynamic Media Classic クラウド設定用に指定したものです。必要に応じて、別のターゲットフォルダーに別のエンコーディングプロファイルを適用することで、複数の Dynamic Media Classic クラウド設定を指定できます。

### ビューアとエンコーディングプリセットの更新 {#updating-viewer-and-encoding-presets}

Dynamic Media Classic でプリセットが更新されている場合は、Experience Manager でビデオのビューアとエンコーディングプリセットを更新します。 その場合は、クラウド設定の Dynamic Media Classic 設定に移動して、「 **ビューアとエンコーディングプリセットの更新** 」を選択します。

![chlimage_1-131](assets/chlimage_1-131.png)

### プライマリソースビデオをアップロード {#uploading-your-master-video}

Adobe DAM から Dynamic Media Classic にプライマリソースビデオをアップロードする方法。

1. Dynamic Media Classic のエンコーディングプロファイルでクラウド設定を指定した CQ DAM のターゲットフォルダーに移動します。
1. **[!UICONTROL アップロード]**&#x200B;を選択して、プライマリソースビデオをアップロードします。 [!UICONTROL DAM アセットの更新]ワークフローが完了し、「**[!UICONTROL Dynamic Media Classic に公開]**」にチェックマークが付くと、ビデオのアップロードとエンコーディングが完了します。

   >[!NOTE]
   >
   >ビデオのサムネールの生成にはある程度の時間がかかることがあります。

   DAM プライマリソースのビデオをビデオコンポーネントにドラッグすると、*すべての* Dynamic Media Classic がエンコードした配信用のプロキシレンディションにアクセスします。

### 基盤ビデオコンポーネントと Dynamic Media Classic ビデオコンポーネントの比較 {#foundation-video-component-versus-scene-video-component}

Experience Manager を使用する場合は、Sites で使用可能なビデオコンポーネントと、Dynamic Media Classic ビデオコンポーネントの両方にアクセスできます。これらのコンポーネントに互換性はありません。

Dynamic Media Classic ビデオコンポーネントは、Dynamic Media Classic ビデオでのみ使用できます。 基盤コンポーネントは、Experience Manager（ffmpeg を使用）および Dynamic Media Classic ビデオから保存されたビデオで使用できます。

次の表は、どのコンポーネントをどのようなシナリオで使用するべきかを示しています。

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>デフォルトでは、 Dynamic Media Classic ビデオコンポーネントはユニバーサルビデオプロファイルを使用します。ただし、Experience Manager で使用する HTML5 ベースのビデオプレーヤーを入手することはできます。  Dynamic Media Classic で、デフォルトの HTML5 ビデオプレーヤーの埋め込みコードをコピーして、Experience Manager ページに貼り付けます。

## Experience Manager ビデオコンポーネント {#aem-video-component}

Dynamic Media Classic ビデオの閲覧には Dynamic Media Classic ビデオコンポーネントの使用をお勧めしますが、ここでは念のため、Experience Manager の[!UICONTROL 基盤ビデオコンポーネント]で Dynamic Media Classic ビデオを使用する方法を説明します。

### Experience Manager ビデオと Dynamic Media Classic ビデオの比較 {#aem-video-and-scene-video-comparison}

次の表は、Experience Manager の基盤ビデオコンポーネントと Dynamic Media Classic ビデオコンポーネントの間でサポートされる機能を比較したものです。

|  | Experience Manager の基盤ビデオ | Dynamic Media Classic ビデオ |
|---|---|---|
| アプローチ | HTML5 における最優先のアプローチです。Flash は HTML5 以外のフォールバックでのみ使用されます。 | ほとんどのデスクトップでは Flash です。HTML5 はモバイルとタブレットで使用されます。 |
| 配信 | プログレッシブ | アダプティブストリーミング |
| 追跡 | はい | はい |
| 拡張性 | はい | いいえ |
| モバイルビデオ | はい | はい |

### 設定 {#setting-up}

#### ビデオプロファイルの作成 {#creating-video-profiles}

Dynamic Media Classic クラウド設定で選択した Dynamic Media Classic のエンコーディングプリセットに従って、様々なビデオエンコーディングが作成されます。基盤ビデオコンポーネントで使用するには、選択した各 Dynamic Media Classic エンコーディングプリセットに対してビデオプロファイルを作成する必要があります。 これにより、対応する DAM レンディションをビデオコンポーネントで選択できます。

>[!NOTE]
>
>新しいビデオプロファイルとそのプロファイルに加えた変更は、アクティベートして公開する必要があります。

1. Experience Manager で&#x200B;**[!UICONTROL ツール]**&#x200B;に移動し、「**[!UICONTROL 設定コンソール]**」を選択します。
1. 設定コンソールで、ナビゲーションツリーの&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL Assets]**／**[!UICONTROL ビデオプロファイル]**&#x200B;に移動します。
1. Dynamic Media Classic ビデオプロファイルを作成します。「**[!UICONTROL 新規]** 」メニュー内の「 **[!UICONTROL ページを作成]**」を選択します。
1. Dynamic Media Classic ビデオプロファイルのテンプレートを選択します。 新しいビデオプロファイルページに名前を付け、「**[!UICONTROL 作成]**」を選択します。

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 新しいビデオプロファイルを編集します。最初にクラウド設定を選択します。次に、クラウド設定で選択したものと同じエンコーディングプリセットを選択します。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | プロパティ | 説明 |
   |---|---|
   | Dynamic Media Classic クラウド設定 | エンコーディングプリセットで使用するクラウド設定です。 |
   | Dynamic Media Classic エンコーディングプリセット | このビデオプロファイルをマップするために使用するエンコーディングプリセットです。 |
   | HTML5 ビデオタイプ | このプロパティを使用すると、HTML5 ビデオのソース要素の type プロパティの値を設定できます。この情報は、Dynamic Media Classic のエンコーディングプリセットでは提供されませんが、HTML5 ビデオ要素を使用してビデオを適切にレンダリングするために必要です。共通の形式用のリストが提供されますが、他の形式用に上書きできます。 |

   ビデオコンポーネントで使用する、クラウド設定で選択したすべてのエンコーディングプリセットについて、この手順を繰り返します。

#### デザインを設定 {#configuring-design}

ビデオのソースリストを作成するには、どのビデオプロファイルを使用するのか、基盤ビデオコンポーネントが認識している必要があります。ビデオコンポーネントのデザインダイアログを開いて、新しいビデオプロファイルを使用するためのコンポーネントデザインを設定してください。

>[!NOTE]
>
>基盤ビデオコンポーネントをモバイルページで使用する場合は、ここに示す手順をモバイルページのデザインで繰り返します。

>[!NOTE]
>
>デザインを変更するには、デザインのアクティベーションをおこなって、公開時に変更を有効にする必要があります。

1. 基盤ビデオコンポーネントのデザインダイアログを開き、「**[!UICONTROL プロファイル]**」タブに変更します。その後、標準のプロファイルを削除し、Dynamic Media Classic ビデオの新しいプロファイルを追加します。デザインダイアログのプロファイルリストの順序で、レンダリング時のビデオソース要素の順序も定義します。
1. HTML5 をサポートしていないブラウザーの場合は、ビデオコンポーネントで Flash フォールバックを設定できます。ビデオコンポーネントのデザインダイアログを開き、「**[!UICONTROL Flash]**」タブに変更します。Flash Player 設定を指定して、Flash Player のフォールバックプロファイルを割り当てます。

#### チェックリスト {#checklist}

1. Dynamic Media Classic クラウド設定を作成します。 ビデオエンコーディングのプリセットが設定され、インポーターが実行中であることを確認します。
1. クラウド設定で選択した各ビデオエンコーディングのプリセットに対して、Dynamic Media Classic ビデオプロファイルを作成します。
1. ビデオプロファイルをアクティベートする必要があります。
1. 目的のページで基盤ビデオコンポーネントの設計を設定します。
1. デザインの変更が完了したら、デザインをアクティベートします。
