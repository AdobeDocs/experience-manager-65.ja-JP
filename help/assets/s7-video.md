---
title: ビデオ
description: 自動エンコード用のビデオを Dynamic Media Classic にアップロードし、Experience Manager Assets から直接 Dynamic Media Classic ビデオにアクセスできる、一元化されたビデオアセット管理 Adobe Experience Manager Assets について説明します。Dynamic Media Classic のビデオの統合により、最適化されたビデオの範囲が、すべての画面に拡張されます。
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
role: User, Admin
mini-toc-levels: 3
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: Video
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: ht
source-wordcount: '1563'
ht-degree: 100%

---

# ビデオ {#video}

Adobe Experience Manager Assets では、ビデオアセットを統合管理できます。ビデオを直接アセットにアップロードして、Dynamic Media Classic に対する自動エンコーディングを行ったり、アセットから直接 Dynamic Media Classic ビデオにアクセスしてページオーサリングを行ったりできます。

Dynamic Media Classic のビデオの統合により、最適化されたビデオの範囲を全画面に拡大します（デバイスと帯域幅の自動検出）。

* **[!UICONTROL Scene7 ビデオ]**&#x200B;コンポーネントでは、デスクトップ、タブレットおよびモバイルで適切な形式と画質を使用してビデオを再生するために、デバイスと帯域幅の検出を自動的に実行します。
* Assets - 単一のビデオアセットだけでなく、アダプティブビデオセットを含めることもできます。アダプティブビデオセットには、複数の画面をシームレスに再生するのに必要なすべてのビデオレンディションが含まれています。アダプティブビデオセットでは、同じビデオを、400 kbps、800 kbps、1000 kbps などの様々なビットレートと形式でエンコードしたバージョンにグループ分けします。デスクトップ、iOS、Android™、BlackBerry®、Windows モバイルデバイスなど、複数の画面にわたるアダプティブビデオストリーミングに、S7 ビデオコンポーネントとアダプティブビデオセットを使用します。
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## FFMPEG と Dynamic Media Classic について {#about-ffmpeg-and-scene}

デフォルトのビデオエンコーディングプロセスは、ビデオプロファイルとの FFMPEG ベースの統合の使用に基づいています。そのため、組み込みの DAM 収集ワークフローには、ffmpeg ベースの次の 2 つのワークフローのステップが含まれています。

* FFMPEG のサムネール
* FFMPEG エンコーディング

Dynamic Media Classic の統合を有効にして設定を行っても、これらの 2 つのワークフロー手順は、標準の DAM 取り込みワークフローから自動的に削除されたり無効になったりするわけではありません。FFMPEG ベースのビデオエンコーディングを既に Adobe Experience Manager で使用している場合は、オーサリング環境に FFMPEG がインストールされている可能性があります。その場合は、DAM を使用して取り込んだ新しいビデオが 2 回（1 回は FFMPEG エンコーダーから、もう 1 回は Dynamic Media Classic 統合から）エンコードされます。

Experience Manager で FFMPEG ベースのビデオエンコーディングが設定済みで、FFMPEG がインストールされている場合は、2 つの FFMPEG ワークフローを DAM 取り込みワークフローから削除することをお勧めします。

## サポートされるファイル形式 {#supported-formats}

Scene7 ビデオコンポーネントでは次の形式がサポートされます。

* F4V H.264
* MP4 H.264

## ビデオのアップロード先を指定 {#deciding-where-to-upload-your-video}

ビデオアセットのアップロード先の指定は、次の条件によって決まります。

* ビデオアセットのワークフローが必要かどうか
* ビデオアセットのバージョン管理が必要かどうか

これらの質問のいずれかまたは両方に対する回答が「はい」の場合は、ビデオを Adobe DAM に直接アップロードします。両方の質問に対する回答が「いいえ」の場合は、ビデオを Dynamic Media Classic に直接アップロードします。次の節では、各シナリオのワークフローについて説明します。

### ビデオを直接 Adobe DAM にアップロードする場合 {#if-you-are-uploading-your-video-directly-to-adobe-dam}

アセットのワークフローまたはバージョン管理が必要な場合は、まず Adobe DAM にアップロードします。推奨されるワークフローは次のとおりです。

1. Adobe DAM にビデオアセットをアップロードして、Dynamic Media Classic に自動的にエンコードして公開します。
1.  Experience Manager で、コンテンツファインダーの「**[!UICONTROL ムービー]**」タブにある WCM のビデオアセットにアクセスします。
1. **[!UICONTROL Scene7 ビデオ]**&#x200B;コンポーネントまたは&#x200B;**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントを使用してオーサリングします。

### ビデオを Dynamic Media Classic にアップロードする場合 {#if-you-are-uploading-your-video-to-scene}

アセットのワークフローまたはバージョン管理が必要でない場合は、Scene7 にアセットをアップロードします。推奨されるワークフローは次のとおりです。

1. Dynamic Media Classic で、[Scene7 に対する FTP アップロードとエンコーディングのスケジュールを設定（システムで自動化）します](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html?lang=ja#upload-files-using-via-ftp)。
1. Experience Manager の WCM（コンテンツファインダーの「**[!UICONTROL Scene7]**」タブ）で、ビデオアセットにアクセスします。
1. **[!UICONTROL Scene7 ビデオ]**&#x200B;コンポーネントを使用してオーサリングします。

## Scene7 ビデオとの統合を設定 {#configuring-integration-with-scene-video}

1. **[!UICONTROL クラウドサービス]**&#x200B;で、**[!UICONTROL Scene7]** の設定に移動して「**[!UICONTROL 編集]**」を選択します。
1. 「**[!UICONTROL ビデオ]**」タブを選択します。

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >クラウド設定がページにない場合は、「**[!UICONTROL ビデオ]**」タブが表示されません。

1. アダプティブビデオエンコーディングプロファイル、組み込みの単一のビデオエンコーディングプロファイルまたはカスタムビデオエンコーディングプロファイルを選択します。

   >[!NOTE]
   >
   >ビデオプリセットについて詳しくは、[Dynamic Media Classic のドキュメント](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=ja#video-presets-for-encoding-video-files)を参照してください。
   >
   >ユニバーサルプリセットを設定する際に両方のアダプティブビデオセットを選択するか、「**[!UICONTROL アダプティブビデオエンコーディング]**」オプションを選択することをお勧めします。

1. 選択したエンコーディングプロファイルは、この Scene7 クラウド設定用に指定した CQ DAM のターゲットフォルダーにアップロードされたすべてのビデオに自動的に適用されます。必要に応じて、別のターゲットフォルダーに別のエンコーディングプロファイルを適用することで、複数の Scene7 クラウド設定を指定できます。

## ビューアとエンコーディングプリセットを更新 {#updating-viewer-and-encoding-presets}

Scene7 でプリセットが更新されているので、ビデオのビューアとエンコーディングプリセットを更新する必要がある場合は、クラウド設定の Scene7 設定に移動して、「**[!UICONTROL ビューアとエンコーディングプリセットを更新]**」をクリックします。

![chlimage_1-364](assets/chlimage_1-364.png)

## Adobe DAM からプライマリソースビデオを Scene7 にアップロード {#uploading-your-master-video}

1. Scene7 のエンコーディングプロファイルと共にクラウド設定を指定した CQ DAM のターゲットフォルダーに移動します。
1. 「 **[!UICONTROL アップロード]** 」を選択して、プライマリソースビデオをアップロードします。[!UICONTROL DAM アセットの更新]ワークフローが完了し、「**[!UICONTROL Scene7 に公開]**」にチェックマークが付くと、ビデオのアップロードとエンコーディングが完了します。

   >[!NOTE]
   >
   >ビデオのサムネイルが生成されるまでには、多少時間がかかります。

   DAM プライマリソースビデオをビデオコンポーネントにドラッグすると、Scene7 でエンコードされた配信用の&#x200B;*すべての*&#x200B;プロキシレンディションにアクセスできます。

## 基盤ビデオコンポーネントと Scene7 ビデオコンポーネントの比較 {#foundation-video-component-versus-scene-video-component}

Experience Manage を使用する場合は、サイトで使用可能なビデオコンポーネントと Scene7 ビデオコンポーネントの両方にアクセスできます。これらのコンポーネントに互換性はありません。

Scene7 ビデオコンポーネントは、Scene7 ビデオでのみ使用できます。基盤コンポーネントは、Experience Manager（ffmpeg を使用） から格納されたビデオと Scene7 ビデオで使用できます。

次のマトリクスは、どのコンポーネントをどのようなシナリオで使用すべきかを示しています。

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>既製の S7 ビデオコンポーネントはユニバーサルビデオプロファイルを使用します。ただし、Experience Manager で使用する HTML5 ベースのビデオプレーヤーを入手することはできます。Scene7 で、組み込みの HTML5 ビデオプレーヤーの埋め込みコードをコピーして、Experience Manager ページに貼り付けます。

## Experience Manager ビデオコンポーネント {#aem-video-component}

Scene7 のビデオを表示するには Scene7 のビデオコンポーネントを使用することが推奨されていますが、この節では、完全を期すために、 Experience Manager の基盤ビデオコンポーネントで Scene7 ビデオを使用する方法を説明します。

### Experience Manager ビデオとScene7 ビデオの比較 {#aem-video-and-scene-video-comparison}

次の表は、Experience Manager 基盤ビデオコンポーネントと Scene7 ビデオコンポーネントでサポートされている機能を簡単に比較したものです。

|  | Experience Manager の基盤ビデオ | Scene7 ビデオ |
|---|---|---|
| アプローチ | HTML5 における最優先のアプローチです。Flash は HTML5 以外のフォールバックでのみ使用されます。 | ほとんどのデスクトップでは Flash です。HTML5 はモバイルとタブレットで使用されます。 |
| 配信 | プログレッシブ | アダプティブストリーミング |
| 追跡 | はい | はい |
| 拡張性 | 可 | 不可 |
| モバイルビデオ | はい | はい |

### 設定 {#setting-up}

#### ビデオプロファイルの作成 {#creating-video-profiles}

S7 クラウド設定で選択した S7 エンコーディングプリセットに応じて、様々なビデオエンコーディングが作成されます。基盤ビデオコンポーネントで使用するには、選択した S7 エンコーディングプリセットごとにビデオプロファイルを作成する必要があります。これにより、対応する DAM レンディションをビデオコンポーネントで選択できます。

>[!NOTE]
>
>新しいビデオプロファイルおよびビデオプロファイルに対する変更をアクティベートして公開する必要があります。

1. Experience Manager で、**[!UICONTROL ツール]**／**[!UICONTROL 設定コンソール]**&#x200B;を選択します。
1. **[!UICONTROL 設定コンソール]**&#x200B;で、ナビゲーションツリーの&#x200B;**[!UICONTROL ツール]**／**[!UICONTROL DAM]**／**[!UICONTROL ビデオプロファイル]**&#x200B;に移動します。
1. S7 ビデオプロファイルを作成します。**[!UICONTROL 新規]**&#x200B;メニューで「**[!UICONTROL ページを作成]**」を選択し、Scene7 ビデオプロファイルのテンプレートを選択します。新しいビデオプロファイルのページに名前を付けて、「**[!UICONTROL 作成]**」を選択します。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 新しいビデオプロファイルを編集します。最初にクラウド設定を選択します。次に、クラウド設定で選択したものと同じエンコーディングプリセットを選択します。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | プロパティ | 説明 |
   |---|---|
   | Scene7 クラウド設定 | エンコーディングプリセットで使用するクラウド設定です。 |
   | Scene7 エンコーディングプリセット | このビデオプロファイルをマップするために使用するエンコーディングプリセットです。 |
   | HTML5 ビデオタイプ | このプロパティを使用すると、HTML5 ビデオのソース要素の type プロパティの値を設定できます。この情報は、S7 エンコーディングプリセットでは提供されませんが、HTML5 ビデオ要素を使用してビデオを適切にレンダリングするために必要です。共通の形式用のリストが提供されますが、他の形式用に上書きできます。 |

   ビデオコンポーネントで使用する、クラウド設定で選択したすべてのエンコーディングプリセットについて、この手順を繰り返します。

#### デザインの設定 {#configuring-design}

**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントは、ビデオソースリストを作成するためにどのようなビデオプロファイルを使用するのか知っている必要があります。ビデオコンポーネントのデザインダイアログボックスを開き、新しいビデオプロファイルを使用するためのコンポーネントデザインを設定します。

>[!NOTE]
>
>**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントをモバイルページで使用する場合は、ここに示す手順をモバイルページのデザインで繰り返します。

>[!NOTE]
>
>デザインを変更するには、デザインのアクティベーションをおこなって、公開時に変更を有効にする必要があります。

1. **[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントのデザインダイアログを開き、「**[!UICONTROL プロファイル]**」タブに変更します。次に、デフォルトのプロファイルを削除して、新しい S7 ビデオプロファイルを追加します。デザインダイアログのプロファイルリストの順序で、レンダリング時のビデオソース要素の順序を定義します。
1. HTML5 をサポートしていないブラウザーの場合は、ビデオコンポーネントで Flash フォールバックを設定します。ビデオコンポーネントのデザインダイアログボックスを開き、「**[!UICONTROL Flash]**」タブに変更します。Flash Player 設定を指定して、Flash Player のフォールバックプロファイルを割り当てます。

#### チェックリスト {#checklist}

1. S7 クラウド設定を作成します。ビデオエンコーディングプリセットが設定され、インポーターが実行中であることを確認します。
1. クラウド設定で選択した各ビデオエンコーディングプリセット用の S7 ビデオプロファイルを作成します。
1. ビデオプロファイルをアクティベートする必要があります。
1. 目的のページで&#x200B;**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントの設計を設定します。
1. デザインの変更が完了したら、デザインをアクティベートします。
