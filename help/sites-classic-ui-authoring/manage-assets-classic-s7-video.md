---
title: ビデオ
seo-title: ビデオ
description: アセットでは、ビデオアセットを統合管理できます。ビデオを直接アセットにアップロードして、Scene7 に対する自動エンコーディングをおこなったり、アセットから直接 Scene7 ビデオにアクセスしてページオーサリングをおこなったりできます。
seo-description: アセットでは、ビデオアセットを統合管理できます。ビデオを直接アセットにアップロードして、Scene7 に対する自動エンコーディングをおこなったり、アセットから直接 Scene7 ビデオにアクセスしてページオーサリングをおこなったりできます。
uuid: 46da7a0d-d17b-4716-a304-ce5496421b5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1741'
ht-degree: 37%

---


# ビデオ{#video}

アセットを使用すると、ビデオアセット管理を一元化できます。この機能を使用して、ビデオをアセットに直接アップロードし、Dynamic Media Classicに自動エンコードしたり、アセットから直接Dynamic Media Classicビデオにアクセスしてページをオーサリングできます。

Dynamic Media Classicビデオの統合により、最適化されたビデオの提供先がすべての画面（自動デバイスおよび帯域幅検出）に拡張されます。

* Dynamic Media Classic(Scene7)ビデオコンポーネントは、デバイスと帯域幅の検出を自動的に実行し、デスクトップ、タブレット、モバイルで適切な形式と品質のビデオを再生します。
* アセット — 単一のビデオアセットだけでなく、アダプティブビデオセットも含めることができます。アダプティブビデオセットは、複数の画面にわたってビデオをシームレスに再生するために必要なすべてのビデオレンディションを対象としたコンテナです。アダプティブビデオセットは、同じビデオを異なるビットレート（400 kbps、800 kbps、1000 kbpsなど）やフォーマットでエンコードしたバージョンをグループ化します。デスクトップ、iOS、Android、Blackberry、Windows携帯端末を含む複数の画面でアダプティブビデオストリーミングを行う場合は、S7ビデオコンポーネントと共にアダプティブビデオセットを使用します。詳しくは、[Scene7のアダプティブビデオセットに関するドキュメントを参照してください。](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html)

## FFMPEGとDynamic Media Classic {#about-ffmpeg-and-scene}について

デフォルトのビデオエンコーディングプロセスは、ビデオプロファイルとの FFMPEG ベースの統合の使用に基づいています。したがって、そのまま使用できる[!UICONTROL DAM Update Asset]ワークフローには、次の2つのffmpegベースのワークフロー手順が含まれています。

* FFMPEG のサムネイル
* FFMPEG エンコーディング

Dynamic Media Classic統合の有効化と設定を行っても、初期設定の[!UICONTROL DAM Update Asset]インジェストワークフローからこれら2つのワークフロー手順が自動的に削除または非アクティブ化されることはありません。 FFMPEG ベースのビデオエンコーディングを既に AEM で使用している場合は、オーサリング環境に FFMPEG がインストールされている可能性があります。この場合、Assetsを使用して取り込む新しいビデオは2回エンコードされます。をFFMPEGエンコーダーから、またはDynamic Media Classic統合から1回呼び出します。

AEMが設定され、FFMPEGがインストールされているFFMPEGベースのビデオエンコーディングがある場合、Adobeでは、[!UICONTROL DAM Update Asset]ワークフローから2つのFFMPEGワークフローを削除することを推奨します。

### サポートされるファイル形式 {#supported-formats}

ダイナミックメディアクラシックビデオコンポーネントでは、次の形式がサポートされています。

* F4V H.264
* MP4 H.264

### ビデオのアップロード先の指定  {#deciding-where-to-upload-your-video}

ビデオアセットのアップロード先の指定は、次の条件によって決まります。

* ビデオアセットのワークフローが必要かどうか
* ビデオアセットのバージョン管理が必要かどうか

これらの質問のいずれかまたは両方に対する回答が「はい」の場合は、ビデオをAdobeDAMに直接アップロードします。 両方の質問に対する答えが「いいえ」の場合は、ビデオを直接Dynamic Media Classicにアップロードします。 各シナリオのワークフローについて、次の節で説明します。

#### ビデオを直接 Adobe Assets にアップロードする場合 {#if-you-are-uploading-your-video-directly-to-adobe-assets}

アセットのワークフローまたはバージョン管理が必要な場合は、まず Adobe Assets にアップロードする必要があります。推奨されるワークフローは次のとおりです。

1. ビデオアセットをAdobeアセットにアップロードし、自動的にエンコードしてDynamic Media Classicに公開します。
1. AEM の WCM（コンテンツファインダーの「**[!UICONTROL ムービー]**」タブ）で、ビデオアセットにアクセスします。
1. Dynamic Media ClassicビデオまたはFoundationビデオコンポーネントを使用するオーサー。

#### ビデオをダイナミックメディアクラシック{#if-you-are-uploading-your-video-to-scene}にアップロードする場合

アセットのワークフローまたはバージョン管理が必要ない場合は、アセットをDynamic Media Classicにアップロードする必要があります。 推奨されるワークフローは次のとおりです。

1. Dynamic Media Classicでは、[Dynamic Media Classic(system automated)](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html)に対するFTPのスケジュールアップロードとエンコードを設定します。
1. AEMでは、コンテンツファインダーの&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;タブのWCMのビデオアセットにアクセスします。
1. Dynamic Media Classicビデオコンポーネントを使用して作成する場合。

### ダイナミックメディアクラシックビデオとの統合の設定{#configuring-integration-with-scene-video}

**ユニバーサルプリセットを設定するには**:

1. **[!UICONTROL Cloud Services]**&#x200B;で、**[!UICONTROL ダイナミックメディアクラシック]**&#x200B;の設定に移動し、**[!UICONTROL 編集をクリックします。]**
1. 「**[!UICONTROL ビデオ]**」タブを選択します。

   >[!NOTE]
   >
   >クラウド設定がページにない場合は、「**[!UICONTROL ビデオ]**」タブが表示されません。[WCM用のDynamic Media Classicの有効化](#enablingscene7forwcm)を参照してください。

1. アダプティブビデオエンコーディングプロファイル、組み込みの単一のビデオエンコーディングプロファイルまたはカスタムビデオエンコーディングプロファイルを選択します。

   >[!NOTE]
   >
   >ビデオプリセットの意味について詳しくは、[ダイナミックメディアクラシックドキュメント](https://help.adobe.com/en_US/scene7/using/WSE86ACF2B-BD50-4c48-A1D7-9CD4405B62D0.html)を参照してください。
   >
   >ユニバーサルプリセットを設定する際に両方のアダプティブビデオセットを選択するか、「**[!UICONTROL アダプティブビデオエンコーディング]**」オプションを選択することをお勧めします。

1. 選択したエンコーディングプロファイルは、このDynamic Media Classicクラウド設定用に設定したCQ DAMターゲットフォルダーにアップロードされたすべてのビデオに自動的に適用されます。 必要に応じて異なるエンコーディングプロファイルを適用するために、異なるターゲットーを持つ複数のDynamic Media Classicクラウド設定を設定できます。

### ビューアとエンコーディングプリセットの更新 {#updating-viewer-and-encoding-presets}

プリセットがDynamic Media Classicで更新されたので、AEMでビデオのビューアおよびエンコーディングプリセットを更新する必要がある場合は、クラウド設定のDynamic Media Classic設定に移動し、「**ビューアおよびエンコーディングプリセットを更新**」をクリックします。

![chlimage_1-131](assets/chlimage_1-131.png)

### プライマリソースビデオのアップロード{#uploading-your-master-video}

AdobeDAMからDynamic Media Classicにプライマリソースビデオをアップロードするには：

1. Dynamic Media Classicエンコーディングプロファイルを使用したクラウド設定を設定したCQ DAMターゲットフォルダーに移動します。
1. 「**[!UICONTROL アップロード]**」をクリックして、プライマリソースビデオをアップロードします。 [!UICONTROL DAM Update Asset]ワークフローが完了し、**[!UICONTROL Dynamic Media Classic]**&#x200B;に公開でチェックマークが付いた後に、ビデオのアップロードとエンコーディングが完了します。

   >[!NOTE]
   >
   >ビデオのサムネイルの生成にはある程度の時間がかかることがあります。

   DAMプライマリソースビデオをビデオコンポーネントにドラッグすると、配信用のDynamic Media Classicエンコードプロキシレンディションの&#x200B;*すべて*&#x200B;にアクセスできます。

### FoundationビデオコンポーネントとDynamic Media Classicビデオコンポーネント{#foundation-video-component-versus-scene-video-component}

AEMを使用する場合、サイトで使用できるビデオコンポーネントと、ダイナミックメディアクラシック(Scene7)ビデオコンポーネントの両方にアクセスできます。 これらのコンポーネントに互換性はありません。

ダイナミックメディアクラシックビデオコンポーネントは、ダイナミックメディアクラシックビデオに対してのみ機能します。 Foundationコンポーネントは、AEM（ffmpegを使用）およびDynamic Media Classicビデオから保存されたビデオで機能します。

次の表は、どのコンポーネントをどのようなシナリオで使用すべきかを示しています。

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>デフォルトでは、ダイナミックメディアクラシックビデオコンポーネントはユニバーサルビデオプロファイルを使用します。 ただし、AEMで使用するHTML5ベースのビデオプレーヤーを取得できます。 Dynamic Media Classicで、標準搭載のHTML5ビデオプレーヤーの埋め込みコードをコピーし、AEMページに配置します。


## AEM ビデオコンポーネント {#aem-video-component}

Dynamic Media Classicビデオの表示には、Dynamic Media Classicビデオコンポーネントの使用が推奨される場合でも、完全性を確保するために、AEMでDynamic Media Classicビデオを[!UICONTROL Foundation Video Component]と共に使用する方法について説明します。

### AEMビデオとダイナミックメディアクラシックビデオの比較{#aem-video-and-scene-video-comparison}

次の表は、AEM 基盤ビデオコンポーネントと Scene7 ビデオコンポーネントでサポートされている機能の簡単な比較です。

|  | AEM 基盤ビデオ | ダイナミックMedia Classicビデオ |
|---|---|---|
| アプローチ | HTML5 における最優先のアプローチです。Flash は HTML5 以外のフォールバックでのみ使用されます。 | ほとんどのデスクトップでは Flash です。HTML5 はモバイルとタブレットで使用されます。 |
| 配信 | プログレッシブ | アダプティブストリーミング |
| 追跡 | はい | はい |
| 拡張性 | 可 | はい（Dynamic Media ClassicビューアSDKを使用） |
| モバイルビデオ | はい | はい |

### 設定  {#setting-up}

#### ビデオプロファイルの作成 {#creating-video-profiles}

様々なビデオエンコーディングが、Dynamic Media Classicクラウド設定で選択されたDynamic Media Classicエンコーディングプリセットに従って作成されます。 Foundationビデオコンポーネントがこれらを使用するには、選択した各Dynamic Media Classicエンコーディングプリセットに対してビデオプロファイルを作成する必要があります。 これにより、対応する DAM レンディションをビデオコンポーネントで選択できます。

>[!NOTE]
>
>新しいビデオプロファイルおよびビデオプロファイルに対する変更をアクティベートして公開する必要があります。

1. AEM で、**[!UICONTROL ツール]**&#x200B;に移動し、「**[!UICONTROL 設定コンソール」を選択します。]** 設定コンソールで、ナビゲーションツリーの **[!UICONTROL ツール]** / **[!UICONTROL アセット]** / **[!UICONTROL ビデオ]** プロファイルに移動します。
1. 新しいダイナミックメディアクラシックビデオプロファイルを作成します。 **[!UICONTROL New...]**&#x200B;メニューで、「**[!UICONTROL ページを作成]**」を選択し、「ダイナミックメディアクラシックビデオプロファイル」テンプレートを選択します。 新しいビデオプロファイルページに名前を付け、「**[!UICONTROL 作成」をクリックします。]**

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 新しいビデオプロファイルを編集します。最初にクラウド設定を選択します。次に、クラウド設定で選択したものと同じエンコーディングプリセットを選択します。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | プロパティ | 説明 |
   |---|---|
   | Dynamic Media Classic(Scene7)クラウド設定 | エンコーディングプリセットで使用するクラウド設定です。 |
   | Dynamic Media Classic(Scene7)エンコーディングプリセット | このビデオプロファイルをマップするために使用するエンコーディングプリセットです。 |
   | HTML5 ビデオタイプ | このプロパティを使用すると、HTML5 ビデオのソース要素の type プロパティの値を設定できます。この情報は、Dynamic Media Classicのエンコーディングプリセットでは提供されませんが、HTML5ビデオ要素を使用してビデオを正しくレンダリングするために必要です。 共通の形式用のリストが提供されますが、他の形式用に上書きできます。 |

   ビデオコンポーネントで使用する、クラウド設定で選択したすべてのエンコーディングプリセットについて、この手順を繰り返します。

#### デザインの設定  {#configuring-design}

ビデオソースリストを作成するには、基盤ビデオコンポーネントが、使用するビデオプロファイルについて認識しておく必要があります。ビデオコンポーネントのデザインダイアログを開いて、新しいビデオプロファイルを使用するためのコンポーネントのデザインを設定してください。

>[!NOTE]
>
>基盤ビデオコンポーネントをモバイルページで使用する場合は、ここに示す手順をモバイルページのデザインで繰り返す必要がある可能性があります。

>[!NOTE]
>
>デザインを変更するには、デザインのアクティベーションをおこなって、公開時に変更を有効にする必要があります。

1. 基盤ビデオコンポーネントのデザインダイアログを開き、「**[!UICONTROL プロファイル]**」タブに変更します。次に、そのまま使用できるプロファイルを削除し、新しいDynamic Media Classicビデオプロファイルを追加します。 デザインダイアログ内のプロファイルリストの順序は、レンダリング時のビデオソース要素の順序も定義します。
1. HTML5 をサポートしていないブラウザーの場合は、ビデオコンポーネントで Flash フォールバックを設定できます。ビデオコンポーネントのデザインダイアログを開き、「**[!UICONTROL Flash]**」タブに変更します。Flash Player 設定を指定して、Flash Player のフォールバックプロファイルを割り当てます。

#### チェックリスト {#checklist}

1. ダイナミックメディアクラシック(Scene7)クラウド設定を作成します。 ビデオエンコーディングプリセットが設定され、インポーターが実行されていることを確認します。
1. クラウド設定で選択した各ビデオエンコーディングプリセットに対して、Dynamic Media Classicビデオプロファイルを作成します。
1. ビデオプロファイルをアクティベートする必要があります。
1. 目的のページで基盤ビデオコンポーネントの設計を設定します。
1. デザインの変更が完了したら、デザインをアクティベートします。

