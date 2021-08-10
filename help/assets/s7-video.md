---
title: ビデオ
description: Dynamic Media Classicに自動エンコーディング用のビデオをアップロードし、Experience ManagerAssetsから直接Dynamic Media Classicビデオにアクセスできる、一元化されたビデオアセット管理Adobe Experience Manager Assetsについて説明します。 Dynamic Media Classicビデオの統合により、最適化されたビデオのリーチがすべての画面に広がります。
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
role: User, Admin
mini-toc-levels: 3
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: ビデオ
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 33%

---

# ビデオ {#video}

Adobe Experience Manager Assetsは、ビデオアセット管理を一元化し、Assetsに直接ビデオをアップロードしてDynamic Media Classicに自動エンコードし、Assetsから直接Dynamic Media Classicビデオにアクセスしてページをオーサリングできます。

Dynamic Media Classicビデオの統合により、最適化されたビデオの範囲がすべての画面に広がります（自動デバイスと帯域幅の検出）。

* **[!UICONTROL Scene7ビデオ]**&#x200B;コンポーネントは、デスクトップ、タブレット、モバイルで適切な形式と画質のビデオを再生するために、デバイスと帯域幅の検出を自動的に実行します。
* アセット — 単一のビデオアセットではなく、アダプティブビデオセットを含めることができます。 アダプティブビデオセットには、複数の画面をシームレスに再生するために必要なすべてのビデオレンディションが含まれています。 アダプティブビデオセットでは、同じビデオを、400 kbps、800 kbps、1000 kbps などの様々なビットレートと形式でエンコードしたバージョンにグループ分けします。デスクトップ、iOS、Android™、BlackBerry®、Windowsモバイルデバイスを含む複数の画面にわたるアダプティブビデオストリーミングには、アダプティブビデオセットとS7ビデオコンポーネントを使用します。
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## FFMPEGとDynamic Media Classicについて {#about-ffmpeg-and-scene}

デフォルトのビデオエンコーディングプロセスは、ビデオプロファイルとの FFMPEG ベースの統合の使用に基づいています。そのため、組み込みの DAM 収集ワークフローには、ffmpeg ベースの次の 2 つのワークフローのステップが含まれています。

* FFMPEG のサムネール
* FFMPEG エンコーディング

Dynamic Media Classic統合を有効にして設定しても、標準のDAM取り込みワークフローからこれら2つのワークフロー手順が自動的に削除または非アクティブ化されることはありません。 Adobe Experience Managerで既にFFMPEGベースのビデオエンコーディングを使用している場合は、FFMPEGがオーサリング環境にインストールされている可能性があります。 この場合、DAMを使用して取り込まれた新しいビデオは2回エンコードされます。FFMPEGエンコーダーから、またはDynamic Media Classic統合から1回。

Experience ManagerでのFFMPEGベースのビデオエンコーディングが設定済みで、FFMPEGがインストールされている場合、DAM取り込みワークフローから2つのFFMPEGワークフローを削除することをAdobeにお勧めします。

## サポートされるファイル形式 {#supported-formats}

Scene7 ビデオコンポーネントでは次の形式がサポートされます。

* F4V H.264
* MP4 H.264

## ビデオのアップロード場所の決定 {#deciding-where-to-upload-your-video}

ビデオアセットのアップロード先の指定は、次の条件によって決まります。

* ビデオアセットのワークフローが必要かどうか
* ビデオアセットのバージョン管理が必要かどうか

これらの質問のいずれかまたは両方に対する回答が「はい」の場合は、ビデオをAdobeDAMに直接アップロードします。 両方の質問に対する回答が「いいえ」の場合は、ビデオをDynamic Media Classicに直接アップロードします。 各シナリオのワークフローについて、次の節で説明します。

### ビデオを直接 Adobe DAM にアップロードする場合 {#if-you-are-uploading-your-video-directly-to-adobe-dam}

アセットのワークフローまたはバージョン管理が必要な場合は、まずAdobeDAMにアップロードします。 推奨されるワークフローは次のとおりです。

1. ビデオアセットをAdobeDAMにアップロードし、Dynamic Media Classicに自動的にエンコードして公開します。
1. Experience Managerで、WCMのビデオアセットにアクセスするには、コンテンツファインダーの「**[!UICONTROL Movies]**」タブを使用します。
1. **[!UICONTROL Scene7ビデオ]**&#x200B;または&#x200B;**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントを使用するオーサー。

### ビデオをDynamic Media Classicにアップロードする場合 {#if-you-are-uploading-your-video-to-scene}

アセットのワークフローやバージョン管理が必要ない場合は、Scene7にアセットをアップロードします。 推奨されるワークフローは次のとおりです。

1. Dynamic Media Classicでは、[Scene7（システム自動）に対するFTPアップロードおよびエンコーディングのスケジュールを設定します](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp)。
1. Experience Managerで、WCMのコンテンツファインダーの「**[!UICONTROL Scene7]**」タブでビデオアセットにアクセスします。
1. **[!UICONTROL Scene7ビデオ]**&#x200B;コンポーネントを使用してオーサーします。

## Scene7との統合の設定ビデオ {#configuring-integration-with-scene-video}

1. **[!UICONTROL Cloud Services]**&#x200B;で、**[!UICONTROL Scene7]**&#x200B;設定に移動し、「**[!UICONTROL 編集]**」を選択します。
1. 「**[!UICONTROL ビデオ]**」タブを選択します。

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >クラウド設定がページにない場合は、「**[!UICONTROL ビデオ]**」タブが表示されません。

1. アダプティブビデオエンコーディングプロファイル、組み込みの単一のビデオエンコーディングプロファイルまたはカスタムビデオエンコーディングプロファイルを選択します。

   >[!NOTE]
   >
   >ビデオプリセットの意味について詳しくは、[Dynamic Media Classicのドキュメント](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files)を参照してください。
   >
   >ユニバーサルプリセットを設定する際に両方のアダプティブビデオセットを選択するか、「**[!UICONTROL アダプティブビデオエンコーディング]**」オプションを選択することをお勧めします。

1. 選択したエンコーディングプロファイルは、この Scene7 クラウド設定用に指定した CQ DAM のターゲットフォルダーにアップロードされたすべてのビデオに自動的に適用されます。必要に応じて、別のターゲットフォルダーに別のエンコーディングプロファイルを適用することで、複数の Scene7 クラウド設定を指定できます。

## ビューアとエンコーディングプリセットを更新 {#updating-viewer-and-encoding-presets}

Scene7でプリセットが更新されたのでビデオのビューアとエンコーディングプリセットを更新するには、クラウド設定のScene7設定に移動し、「**[!UICONTROL ビューアとエンコーディングプリセットを更新]**」を選択します。

![chlimage_1-364](assets/chlimage_1-364.png)

## AdobeDAMからScene7にプライマリソースビデオをアップロード {#uploading-your-master-video}

1. Scene7 のエンコーディングプロファイルと共にクラウド設定を指定した CQ DAM のターゲットフォルダーに移動します。
1. 「**[!UICONTROL アップロード]**」を選択して、プライマリソースビデオをアップロードします。 ビデオのアップロードとエンコーディングは、[!UICONTROL DAMアセットの更新]ワークフローが完了し、**[!UICONTROL Scene7に公開]**&#x200B;にチェックマークが付いた後に完了します。

   >[!NOTE]
   >
   >ビデオサムネールの生成には時間がかかります。

   DAMプライマリソースビデオをビデオコンポーネントにドラッグすると、Scene7でエンコードされた配信用のプロキシレンディションがすべて&#x200B;*にアクセスされます。*

## 基盤ビデオコンポーネントと Scene7 ビデオコンポーネントの比較 {#foundation-video-component-versus-scene-video-component}

Experience Managerを使用する場合、Sitesで使用できるビデオコンポーネントとScene7ビデオコンポーネントの両方にアクセスできます。 これらのコンポーネントに互換性はありません。

Scene7 ビデオコンポーネントは、Scene7 ビデオでのみ使用できます。基盤コンポーネントは、Experience Manager（ffmpegを使用）とScene7ビデオから保存されたビデオで使用します。

次の表に、どのコンポーネントを使用するかを示します。

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>既製の S7 ビデオコンポーネントはユニバーサルビデオプロファイルを使用します。ただし、Experience Managerで使用するHTML5ベースのビデオプレーヤーを入手することはできます。 Scene7で、標準搭載のHTML5ビデオプレーヤーの埋め込みコードをコピーし、Experience Managerページに配置します。

## Experience Managerビデオコンポーネント {#aem-video-component}

Scene7ビデオの視聴にScene7ビデオコンポーネントの使用をお勧めしますが、完全性を考慮して、Scene7ビデオをExperience Managerで使用する方法について説明します。

### Experience ManagerビデオとScene7ビデオの比較 {#aem-video-and-scene-video-comparison}

次の表に、Experience Manager基盤ビデオコンポーネントとScene7ビデオコンポーネントの間でサポートされている機能の大まかな比較を示します。

|  | Experience Manager基盤ビデオ | Scene7 ビデオ |
|---|---|---|
| アプローチ | HTML5 における最優先のアプローチです。Flash は HTML5 以外のフォールバックでのみ使用されます。 | ほとんどのデスクトップでは Flash です。HTML5 はモバイルとタブレットで使用されます。 |
| 配信 | プログレッシブ | アダプティブストリーミング |
| 追跡 | はい | はい |
| 拡張性 | 可 | 不可 |
| モバイルビデオ | はい | はい |

### 設定 {#setting-up}

#### ビデオプロファイルの作成 {#creating-video-profiles}

S7 クラウド設定で選択した S7 エンコーディングプリセットに応じて、様々なビデオエンコーディングが作成されます。基盤ビデオコンポーネントで使用するには、選択したS7エンコーディングプリセットごとにビデオプロファイルを作成する必要があります。 この方法を使用すると、ビデオコンポーネントがそれに応じてDAMレンディションを選択できます。

>[!NOTE]
>
>新しいビデオプロファイルおよびビデオプロファイルに対する変更をアクティベートして公開する必要があります。

1. Experience Managerで、**[!UICONTROL ツール]** / **[!UICONTROL 設定コンソール]**&#x200B;を選択します。
1. **[!UICONTROL 設定コンソール]**&#x200B;で、ナビゲーションツリーの&#x200B;**[!UICONTROL ツール]**/**[!UICONTROL DAM]**/**[!UICONTROL ビデオプロファイル]**&#x200B;に移動します。
1. S7ビデオプロファイルを作成します。 **[!UICONTROL New]**&#x200B;で、 メニューで、「**[!UICONTROL ページを作成]**」を選択し、「Scene7ビデオプロファイル」テンプレートを選択します。 新しいビデオプロファイルページに名前を付け、「**[!UICONTROL 作成]**」を選択します。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 新しいビデオプロファイルを編集します。最初にクラウド設定を選択します。次に、クラウド設定で選択したものと同じエンコーディングプリセットを選択します。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | プロパティ | 説明 |
   |---|---|
   | Scene7 クラウド設定 | エンコーディングプリセットで使用するクラウド設定です。 |
   | Scene7 エンコーディングプリセット | このビデオプロファイルをマップするために使用するエンコーディングプリセットです。 |
   | HTML5 ビデオタイプ | このプロパティを使用すると、HTML5ビデオソース要素のtypeプロパティの値を設定できます。 この情報は、S7 エンコーディングプリセットでは提供されませんが、HTML5 ビデオ要素を使用してビデオを適切にレンダリングするために必要です。共通の形式用のリストが提供されますが、他の形式用に上書きできます。 |

   ビデオコンポーネントで使用する、クラウド設定で選択したすべてのエンコーディングプリセットについて、この手順を繰り返します。

#### デザインの設定 {#configuring-design}

**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントは、ビデオソースリストを作成するために使用するビデオプロファイルについて認識する必要があります。 ビデオコンポーネントデザインダイアログボックスを開き、新しいビデオプロファイルを使用するためのコンポーネントデザインを設定します。

>[!NOTE]
>
>モバイルページで&#x200B;**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントを使用する場合は、モバイルページのデザインでこれらの手順を繰り返します。

>[!NOTE]
>
>デザインを変更するには、デザインのアクティベーションをおこなって、公開時に変更を有効にする必要があります。

1. **[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントのデザインダイアログボックスを開き、「**[!UICONTROL プロファイル]**」タブに変更します。 次に、標準のプロファイルを削除し、新しいS7ビデオプロファイルを追加します。 デザインダイアログボックスでのプロファイルリストの順序によって、レンダリング時のビデオソース要素の順序が決まります。
1. HTML5をサポートしていないブラウザーの場合、ビデオコンポーネントを使用すると、Flashフォールバックを設定できます。 ビデオコンポーネントデザインダイアログボックスを開き、「**[!UICONTROL Flash]**」タブに変更します。 Flashプレーヤーの設定を行い、Flash Playerのフォールバックプロファイルを割り当てます。

#### チェックリスト {#checklist}

1. S7クラウド設定を作成します。 ビデオエンコーディングプリセットが設定され、インポーターが実行中であることを確認します。
1. クラウド設定で選択した各ビデオエンコーディングプリセット用の S7 ビデオプロファイルを作成します。
1. ビデオプロファイルをアクティベートする必要があります。
1. ページ上の&#x200B;**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントのデザインを設定します。
1. デザインの変更が完了したら、デザインをアクティベートします。
