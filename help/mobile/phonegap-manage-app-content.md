---
title: アプリコンテンツの作成および管理
description: アプリコンテンツの管理には、開発者、コンテンツ作成者および管理者の協力が必要です。 作成者がページを操作します。これは、アプリ開発者が生成したテンプレートとコンポーネントに基づいています。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 8%

---

# アプリコンテンツの作成および管理{#creating-and-managing-app-content}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

アプリコンテンツの管理には、次からの共同作業が必要です [開発者](#developer), コンテンツ [作成者](#author)、および [管理者](#administrator). 作成者がページを操作します。これは、アプリ開発者が生成したテンプレートとコンポーネントに基づいています。

最後に、管理者は、更新されたアプリコンテンツを戦略的に公開します。

>[!NOTE]
>
>**前提条件**:
>
>対象： [デプロイとメンテナンス](/help/sites-deploying/deploy.md)を参照し、開発者はAdobe Experience Manager（AEM）のシステムコンポーネントとテンプレートについて理解しました。

## ページコンテンツを管理タイル {#the-manage-page-content-tile}

>[!CAUTION]
>
>標準のアプリテンプレートを使用していない場合、新しいアプリコンテンツを OTA で公開するには、コンテンツ同期ハンドラーを設定する必要があります。
>
>参照： [モバイルとコンテンツ同期](/help/mobile/phonegap-contentsync.md) 詳しくは、開発者の節を参照してください。

このコンソールでは、AEM Sites内と同じ方法でAEM Mobileのコンテンツを作成、編集、削除できます。

この **ページコンテンツ管理タイル** 特定のペイロードについて、管理コンテンツと最終変更日のページ数を表示します。 コンテンツをドリルインし、タイル内の各レコードをクリックしてページを作成、コピー、移動、削除、更新できます。

コンテンツが更新されると、管理者は、 **コンテンツパッケージを管理タイル。**

![chlimage_1-161](assets/chlimage_1-161.png)

リストに表示されたコンテンツパッケージの 1 つを選択して、ページの作成、編集、削除、ナビゲーションとページ順序の変更、コンテンツの作成または更新（コピー（テキスト）やメディアなど）を行います。

注意 *すべてがコンテンツである*&#x200B;つまり、アプリケーションスタイル、コピー（テキスト）、メディア、ページ、ナビゲーション、およびコンテンツのターゲティングはすべて、アプリストアに出向かなくても OTA で編集および更新できます。

AEM Mobileのコンテンツを編集するには、*AEM作成者*がAEM コンテンツ編集インターフェイスについて理解している必要があります。 [AEMでのページのオーサリング。](/help/sites-authoring/qg-page-authoring.md)

## コンテンツパッケージを管理タイル {#the-manage-content-packages-tile}

ここで、 *AEM管理者* は、アプリを迅速かつ簡単に更新して、エンゲージメントを高めビジネス目標を達成するための魅力的なエクスペリエンスと最新のコンテンツを提供できます。開発者やアプリストアの再提出は必要ありません。

![chlimage_1-162](assets/chlimage_1-162.png)

1 回 *AEM オーサー* コンテンツを管理タイルを使用してコンテンツを追加または変更している。 *AEM管理者* コンテンツパッケージのアップデートにより、これらの変更を顧客にプッシュできます。

コンテンツパッケージのアクションにより、 *AEM オーサー* 開発チームがホストアプリケーションの設計と実装（ナビゲーション、スタイル、サーバーサイドロジック、テンプレート、コンポーネントなど）に変更を加えた後、それらの変更を顧客にプッシュする際、様々なストアに再提出して配布する必要をなくし、ページコンテンツを作成および編集する。

**新しいコンテンツまたは更新されたコンテンツを公開するには**

タイルからコンテンツパッケージ（この例では英語パッケージ）を選択します。 コンテンツ更新ダイアログボックスには、関連するが一覧表示されます *コンテンツ同期* 設定。 前回の更新以降にアプリのコンテンツが変更されている場合は、ステータスが表示されます *保留中*&#x200B;を参照してください。

![chlimage_1-163](assets/chlimage_1-163.png)

次に、 **ステージ** コンテンツの更新を作成する右上のアクション。 適切な更新情報を追加し、「完了」を押します。

![chlimage_1-164](assets/chlimage_1-164.png)

この *コンテンツ同期* 次に、ハンドラーは差分（ *のみ* 変更点）。 完了すると、この更新コンテンツパッケージは次に示すようにステージングされます。

コンテンツに更新をステージングすると、モバイルデバイスに OTA で公開する前に複数の更新を行うことができます。

>[!NOTE]
>
>ステージングされたコンテンツは、公開前にAEM検証アプリを使用して検証できます。
>
>参照： [AEM用モバイルクイックスタートの検証](/help/mobile/phonegap-mobile-quickstart.md) AEM Verify アプリについて詳しくは、こちらを参照してください。

![chlimage_1-165](assets/chlimage_1-165.png)

コンテンツ同期 OTA を使用してアプリユーザーに新しいコンテンツを配信する準備ができたら、次を選択します。 **公開** 下図を参照してください。

![chlimage_1-166](assets/chlimage_1-166.png)

### 次の手順 {#the-next-steps}

アプリケーションダッシュボードでのアプリコンテンツの作成と管理について理解したら、他のオーサリングの役割について、次のリソースを参照してください。

* [アプリを管理タイル](/help/mobile/phonegap-app-details-tile.md)
* [アプリのメタデータの編集](/help/mobile/phonegap-editmetadata.md)
* [アプリの定義](/help/mobile/phonegap-app-definitions.md)
* [アプリの作成ウィザードを使用した新しいアプリの作成](/help/mobile/phonegap-create-new-app.md)
* [既存のハイブリッドアプリを読み込む](/help/mobile/phonegap-adding-content-to-imported-app.md)

### その他のリソース {#additional-resources}

管理者と開発者の役割と責任については、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けの開発](/help/mobile/developing-in-phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
