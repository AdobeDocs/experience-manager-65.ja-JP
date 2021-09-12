---
title: ビデオ
seo-title: Video
description: Assetsでは、ビデオアセット管理を一元化し、Assetsに直接ビデオをアップロードしてDynamic Media Classicに自動エンコーディングし、Assetsから直接Dyビデオにアクセスしてページをオーサリングできます。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: b5cf18d8e83786a23005aadf8aafe43d006a2e67
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 25%

---

# ビデオ{#video}

Assetsでは、ビデオアセット管理を一元化できます。Assetsに直接アップロードしてDynamic Media Classicに自動エンコーディングし、Assetsから直接Dynamic Media Classicビデオにアクセスしてページをオーサリングできます。

Dynamic Media Classicビデオの統合により、最適化されたビデオの範囲がすべての画面に広がります（自動デバイスと帯域幅の検出）。

* Dynamic Media Classicビデオコンポーネントは、デスクトップ、タブレット、モバイルで適切な形式と画質のビデオを再生するために、デバイスと帯域幅の検出を自動的に実行します。
* アセット — 単一のビデオアセットではなく、アダプティブビデオセットを含めることができます。 アダプティブビデオセットは、複数の画面をシームレスに再生するために必要なすべてのビデオレンディション用のコンテナです。 アダプティブビデオセットでは、同じビデオを、400 kbps、800 kbps、1000 kbps などの様々なビットレートと形式でエンコードしたバージョンにグループ分けします。デスクトップ、iOS、Android™、BlackBerry®、Windowsモバイルデバイスを含む複数の画面にわたるアダプティブビデオストリーミングには、アダプティブビデオセットとS7ビデオコンポーネントを使用します。 詳しくは、[Dynamic Media Classicのアダプティブビデオセットに関するドキュメントを参照してください。](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video)

## FFMPEGとDynamic Media Classicについて {#about-ffmpeg-and-scene}

デフォルトのビデオエンコーディングプロセスは、ビデオプロファイルとの FFMPEG ベースの統合の使用に基づいています。そのため、標準の[!UICONTROL DAMアセットの更新]ワークフローには、ffmpegベースの次の2つのワークフローステップが含まれています。

* FFMPEG のサムネイル
* FFMPEG エンコーディング

Dynamic Media Classic統合を有効にして設定しても、標準の[!UICONTROL DAMアセットの更新]取り込みワークフローからこれら2つのワークフロー手順が自動的に削除または非アクティブ化されることはありません。 Adobe Experience Managerで既にFFMPEGベースのビデオエンコーディングを使用している場合は、FFMPEGがオーサリング環境にインストールされている可能性があります。 この場合、Experience ManagerAssetsを使用して取り込まれる新しいビデオは2回エンコードされます。FFMPEGエンコーダーから、またはDynamic Media Classic統合から1回。

Experience ManagerでFFMPEGベースのビデオエンコーディングを設定し、FFMPEGをインストールしている場合は、[!UICONTROL DAMアセットの更新]ワークフローから2つのFFMPEGワークフローを削除することをお勧めします。

### サポートされるファイル形式 {#supported-formats}

Dynamic Media Classicビデオコンポーネントでは、次の形式がサポートされています。

* F4V H.264
* MP4 H.264

### ビデオのアップロード場所の決定 {#deciding-where-to-upload-your-video}

ビデオアセットのアップロード先の指定は、次の条件によって決まります。

* ビデオアセットのワークフローが必要かどうか
* ビデオアセットのバージョン管理が必要かどうか

これらの質問のいずれかまたは両方に対する回答が「はい」の場合は、ビデオをAdobeDAMに直接アップロードします。 両方の質問に対する回答が「いいえ」の場合は、ビデオをDynamic Media Classicに直接アップロードします。 各シナリオのワークフローについて、次の節で説明します。

#### ビデオを直接 Adobe Assets にアップロードする場合 {#if-you-are-uploading-your-video-directly-to-adobe-assets}

アセットのワークフローまたはバージョン管理が必要な場合は、まず Adobe Assets にアップロードする必要があります。推奨されるワークフローは次のとおりです。

1. ビデオアセットをAssetsにアップロードし、AdobeAssetsに自動的にエンコードしてDynamic Media Classicに公開します。
1. Experience Managerで、WCMのビデオアセットにアクセスするには、コンテンツファインダーの「**[!UICONTROL Movies]**」タブを使用します。
1. Dynamic Media Classicビデオまたは基盤ビデオコンポーネントを使用したオーサー。

#### ビデオをDynamic Media Classicにアップロードする場合 {#if-you-are-uploading-your-video-to-scene}

アセットのワークフローやバージョン管理が必要ない場合は、Dynamic Media Classicにアセットをアップロードする必要があります。 推奨されるワークフローは次のとおりです。

1. Dynamic Media Classicデスクトップアプリケーションで、[Dynamic Media Classicに対するFTPのアップロードとエンコーディングのスケジュールを設定します（システム自動）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-options)。
1. Experience Managerで、WCMのビデオアセットにアクセスするには、コンテンツファインダーの「**[!UICONTROL Dynamic Media Classic]**」タブを使用します。
1. Dynamic Media Classicビデオコンポーネントを使用したオーサリング。

### Dynamic Media Classicビデオとの統合の設定 {#configuring-integration-with-scene-video}

1. **[!UICONTROL Cloud Services]**&#x200B;で、**[!UICONTROL Dynamic Media Classic]**&#x200B;設定に移動し、「**[!UICONTROL 編集]**」を選択します。
1. 「**[!UICONTROL ビデオ]**」タブを選択します。

   >[!NOTE]
   >
   >クラウド設定がページにない場合は、「**[!UICONTROL ビデオ]**」タブが表示されません。[WCM用のDynamic Media Classicの有効化](#enablingscene7forwcm)を参照してください。

1. アダプティブビデオエンコーディングプロファイル、組み込みの単一のビデオエンコーディングプロファイルまたはカスタムビデオエンコーディングプロファイルを選択します。

   >[!NOTE]
   >
   >ビデオプリセットの意味について詳しくは、[ビデオファイルのエンコーディング用のビデオプリセット](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files)を参照してください。
   >
   >ユニバーサルプリセットを設定する際に両方のアダプティブビデオセットを選択するか、「**[!UICONTROL アダプティブビデオエンコーディング]**」オプションを選択することをお勧めします。

1. 選択したエンコーディングプロファイルは、このDynamic Media Classicクラウド設定用に設定したCQ DAMターゲットフォルダーにアップロードされたすべてのビデオに自動的に適用されます。 必要に応じて、様々なターゲットフォルダーを持つ複数のDynamic Media Classicクラウド設定を設定し、様々なエンコーディングプロファイルを適用できます。

### ビューアとエンコーディングプリセットの更新 {#updating-viewer-and-encoding-presets}

Dynamic Media Classicで更新された場合は、ビデオのビューアプリセットとエンコーディングプリセットをExperience Managerで更新します。 その場合は、クラウド設定のDynamic Media Classic設定に移動し、「**ビューアとエンコーディングプリセットを更新**」を選択します。

![chlimage_1-131](assets/chlimage_1-131.png)

### プライマリソースビデオのアップロード {#uploading-your-master-video}

AdobeDAMからDynamic Media Classicにプライマリソースビデオをアップロードするには：

1. Dynamic Media Classicエンコーディングプロファイルを使用してクラウド設定を行ったCQ DAMターゲットフォルダーに移動します。
1. 「**[!UICONTROL アップロード]**」を選択して、プライマリソースビデオをアップロードします。 ビデオのアップロードとエンコーディングは、[!UICONTROL DAMアセットの更新]ワークフローが完了し、**[!UICONTROL Dynamic Media Classicに公開]**&#x200B;にチェックマークが付いた後に完了します。

   >[!NOTE]
   >
   >ビデオのサムネイルの生成にはある程度の時間がかかることがあります。

   DAMプライマリソースビデオをビデオコンポーネントにドラッグすると、*すべての* Dynamic Media Classicエンコードされた配信用のプロキシレンディションにアクセスします。

### 基盤ビデオコンポーネントとDynamic Media Classicビデオコンポーネントの比較 {#foundation-video-component-versus-scene-video-component}

Experience Managerを使用する場合、Sitesで使用できるビデオコンポーネントとDynamic Media Classicビデオコンポーネントの両方にアクセスできます。 これらのコンポーネントに互換性はありません。

Dynamic Media Classicビデオコンポーネントは、Dynamic Media Classicビデオに対してのみ機能します。 基盤コンポーネントは、Experience Manager（ffmpegを使用）およびDynamic Media Classicビデオから保存されたビデオで使用します。

次の表は、どのコンポーネントをどのようなシナリオで使用すべきかを示しています。

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>標準では、Dynamic Media Classicビデオコンポーネントはユニバーサルビデオプロファイルを使用します。 ただし、HTML5ベースのビデオプレーヤーを入手して、Experience Managerで使用することはできます。 Dynamic Media Classicで、標準搭載のHTML5ビデオプレーヤーの埋め込みコードをコピーし、Experience Managerページに配置します。

## Experience Managerビデオコンポーネント {#aem-video-component}

Dynamic Media Classicビデオの視聴には、Dynamic Media Classicビデオコンポーネントの使用が推奨される場合でも、完全性を考慮して、Dynamic Media Classicビデオを[!UICONTROL 基盤ビデオコンポーネント]と共にExperience Managerして使用する方法について説明します。

### Experience ManagerビデオとDynamic Media Classicビデオの比較 {#aem-video-and-scene-video-comparison}

次の表に、Experience Managerの基盤ビデオコンポーネントとDynamic Media Classicビデオコンポーネントの間でサポートされている機能の大まかな比較を示します。

|  | Experience Manager基盤ビデオ | Dynamic Media Classicビデオ |
|---|---|---|
| アプローチ | HTML5 における最優先のアプローチです。Flash は HTML5 以外のフォールバックでのみ使用されます。 | ほとんどのデスクトップでは Flash です。HTML5 はモバイルとタブレットで使用されます。 |
| 配信 | プログレッシブ | アダプティブストリーミング |
| 追跡 | はい | はい |
| 拡張性 | 可 | 不可 |
| モバイルビデオ | はい | ○ |

### 設定 {#setting-up}

#### ビデオプロファイルの作成 {#creating-video-profiles}

様々なビデオエンコーディングは、Dynamic Media Classicクラウド設定で選択したDynamic Media Classicエンコーディングプリセットに従って作成されます。 基盤ビデオコンポーネントで使用するには、選択したDynamic Media Classicエンコーディングプリセットごとにビデオプロファイルを作成する必要があります。 これに応じて、ビデオコンポーネントがDAMレンディションを選択できます。

>[!NOTE]
>
>新しいビデオプロファイルおよびビデオプロファイルに対する変更をアクティベートして公開する必要があります。

1. Experience Managerで、**[!UICONTROL ツール]**&#x200B;に移動し、**[!UICONTROL 設定コンソール]**&#x200B;を選択します。
1. 設定コンソールで、ナビゲーションツリーの&#x200B;**[!UICONTROL ツール]** / **[!UICONTROL アセット]** / **[!UICONTROL ビデオプロファイル]**&#x200B;に移動します。
1. Dynamic Media Classicビデオプロファイルを作成します。 **[!UICONTROL 新規]**&#x200B;メニューで、「**[!UICONTROL ページを作成]**」を選択します。
1. 「 Dynamic Media Classicビデオプロファイル」テンプレートを選択します。 新しいビデオプロファイルページに名前を付け、「**[!UICONTROL 作成]**」を選択します。

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 新しいビデオプロファイルを編集します。最初にクラウド設定を選択します。次に、クラウド設定で選択したものと同じエンコーディングプリセットを選択します。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | プロパティ | 説明 |
   |---|---|
   | Dynamic Media Classicクラウド設定 | エンコーディングプリセットで使用するクラウド設定です。 |
   | Dynamic Media Classicエンコーディングプリセット | このビデオプロファイルをマップするために使用するエンコーディングプリセットです。 |
   | HTML5 ビデオタイプ | このプロパティを使用すると、HTML5ビデオソース要素のtypeプロパティの値を設定できます。 この情報は、Dynamic Media Classicのエンコーディングプリセットでは提供されませんが、HTML5ビデオ要素を使用してビデオを適切にレンダリングするために必要です。 共通の形式用のリストが提供されますが、他の形式用に上書きできます。 |

   ビデオコンポーネントで使用する、クラウド設定で選択したすべてのエンコーディングプリセットについて、この手順を繰り返します。

#### デザインの設定 {#configuring-design}

基盤ビデオコンポーネントは、ビデオソースリストを作成するために使用するビデオプロファイルについて把握しておく必要があります。ビデオコンポーネントデザインダイアログを開き、新しいビデオプロファイルを使用するためのコンポーネントデザインを設定します。

>[!NOTE]
>
>モバイルページで基盤ビデオコンポーネントを使用する場合は、モバイルページのデザインでこれらの手順を繰り返します。

>[!NOTE]
>
>デザインを変更するには、デザインのアクティベーションをおこなって、公開時に変更を有効にする必要があります。

1. 基盤ビデオコンポーネントのデザインダイアログを開き、「**[!UICONTROL プロファイル]**」タブに変更します。次に、標準のプロファイルを削除し、新しいDynamic Media Classicビデオプロファイルを追加します。 デザインダイアログでのプロファイルリストの順序は、レンダリング時のビデオソース要素の順序も定義します。
1. HTML5をサポートしていないブラウザーの場合、ビデオコンポーネントを使用すると、Flashフォールバックを設定できます。 ビデオコンポーネントのデザインダイアログを開き、「**[!UICONTROL Flash]**」タブに変更します。Flash Player 設定を指定して、Flash Player のフォールバックプロファイルを割り当てます。

#### チェックリスト {#checklist}

1. Dynamic Media Classicクラウド設定を作成します。 ビデオエンコーディングプリセットが設定され、インポーターが実行中であることを確認します。
1. クラウド設定で選択した各ビデオエンコーディングプリセットに対して、 Dynamic Media Classicビデオプロファイルを作成します。
1. ビデオプロファイルをアクティベートする必要があります。
1. 目的のページで基盤ビデオコンポーネントの設計を設定します。
1. デザインの変更が完了したら、デザインをアクティベートします。
