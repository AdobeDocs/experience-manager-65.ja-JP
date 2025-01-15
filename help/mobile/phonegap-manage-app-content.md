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
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 5%

---

# アプリコンテンツの作成および管理{#creating-and-managing-app-content}

{{ue-over-mobile}}

アプリコンテンツの管理には、[ 開発者 ](#developer)、コンテンツ [ 作成者 ](#author)、[ 管理者 ](#administrator) の共同作業が必要です。 作成者がページを操作します。これは、アプリ開発者が生成したテンプレートとコンポーネントに基づいています。

最後に、管理者は、更新されたアプリコンテンツを戦略的に公開します。

>[!NOTE]
>
>**前提条件**:
>
>[ デプロイとメンテナンス ](/help/sites-deploying/deploy.md) では、開発者はAdobe Experience Manager（AEM）のシステムコンポーネントとテンプレートについて理解しました。

## ページコンテンツを管理タイル {#the-manage-page-content-tile}

>[!CAUTION]
>
>標準のアプリテンプレートを使用していない場合、新しいアプリコンテンツを OTA で公開するには、コンテンツ同期ハンドラーを設定する必要があります。
>
>詳しくは、開発者の節の [ コンテンツ同期を使用したモバイル ](/help/mobile/phonegap-contentsync.md) を参照してください。

このコンソールでは、AEM Sites内と同じ方法でAEM Mobileのコンテンツを作成、編集、削除できます。

**ページコンテンツを管理** タイルには、特定のペイロードに関する管理コンテンツのページ数と最終変更日が表示されます。 コンテンツをドリルインし、タイル内の各レコードをクリックしてページを作成、コピー、移動、削除、更新できます。

コンテンツが更新されると、管理者は、**コンテンツパッケージの管理** タイルを通じて、コンテンツアップデートのペイロードを無線（OTA）で顧客に公開できます。

![chlimage_1-161](assets/chlimage_1-161.png)

リストに表示されたコンテンツパッケージの 1 つを選択して、ページの作成、編集、削除、ナビゲーションとページ順序の変更、コンテンツの作成または更新（コピー（テキスト）やメディアなど）を行います。

メモ *すべてがコンテンツです*。つまり、アプリケーションスタイル、コピー（テキスト）、メディア、ページ、ナビゲーション、およびコンテンツのターゲティングはすべて、アプリストアに出向かなくても OTA で編集および更新できます。

AEM Mobileのコンテンツを編集するには、*AEM作成者*がAEM コンテンツ編集インターフェイス（[AEMでのページのオーサリング ](/help/sites-authoring/qg-page-authoring.md) についてしっかりと理解している必要があります。

## コンテンツパッケージを管理タイル {#the-manage-content-packages-tile}

このリリースでは、*AEM管理者* は、開発者やアプリストアの再提出を必要とせずに、魅力的なエクスペリエンスと最新のコンテンツを提供するアプリをすばやく簡単に更新して、ブランドエンゲージメントを促進し、ビジネス目標を達成できます。

![chlimage_1-162](assets/chlimage_1-162.png)

*AEM作成者* がコンテンツを管理タイルを使用してコンテンツを追加または変更すると、*AEM管理者* は、コンテンツパッケージの更新でこれらの変更をお客様にプッシュできます。

コンテンツパッケージのアクションを使用すると、*AEM オーサー* はページコンテンツの作成と編集を行うことができます。開発チームは、ナビゲーション、スタイル、サーバーサイドロジック、テンプレート、コンポーネントなどのホストアプリケーションの設計と実装に変更を加えた後、それらの変更を OTA にプッシュするので、配信用に様々なストアに再送信する必要はありません。

**新しいコンテンツまたは更新されたコンテンツを公開するには**

タイルからコンテンツパッケージ（この例では英語パッケージ）を選択します。 コンテンツを更新ダイアログボックスに、関連する *コンテンツ同期* 設定が一覧表示されます。 前回の更新以降にアプリのコンテンツが変更されている場合は、次に示すように、ステータスが *保留中* と表示されます。

![chlimage_1-163](assets/chlimage_1-163.png)

次に、右上の **ステージ** アクションを選択して、コンテンツの更新を作成します。 適切な更新情報を追加し、「完了」を押します。

![chlimage_1-164](assets/chlimage_1-164.png)

次に、*コンテンツ同期* ハンドラーは、差分（（変更内容の *のみ* パッケージ）を作成して必要なパッケージを作成します。 完了すると、この更新コンテンツパッケージは次に示すようにステージングされます。

コンテンツに更新をステージングすると、モバイルデバイスに OTA で公開する前に複数の更新を行うことができます。

>[!NOTE]
>
>ステージングされたコンテンツは、公開前にAEM検証アプリを使用して検証できます。
>
>AEM Verify アプリについて詳しくは、[AEM Verify 用モバイルクイックスタート ](/help/mobile/phonegap-mobile-quickstart.md) を参照してください。

![chlimage_1-165](assets/chlimage_1-165.png)

コンテンツ同期 OTA を使用してアプリユーザーに新しいコンテンツを配信する準備ができたら、以下に示すように、「**Publish**」を選択します。

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
