---
title: アプリコンテンツの作成および管理
description: アプリコンテンツの管理には、開発者、コンテンツ作成者、管理者が共同で取り組む必要があります。 作成者は、アプリ開発者が生成したテンプレートとコンポーネントに基づいて、ページを操作します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 9d350935-129a-40d3-89f4-2e6f69676e5e
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 5%

---

# アプリコンテンツの作成および管理{#creating-and-managing-app-content}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

アプリコンテンツの管理には、 [開発者](#developer)，コンテンツ [作成者](#author)、および [管理者](#administrator). 作成者は、アプリ開発者が生成したテンプレートとコンポーネントに基づいて、ページを操作します。

最後に、管理者は更新されたアプリコンテンツを戦略的に公開します。

>[!NOTE]
>
>**前提条件**:
>
>In [デプロイと保守](/help/sites-deploying/deploy.md)を使用すると、開発者はAdobe Experience Manager(AEM) のシステムコンポーネントとテンプレートに精通していました。

## ページコンテンツを管理タイル {#the-manage-page-content-tile}

>[!CAUTION]
>
>標準のアプリテンプレートを使用しない場合は、新しいアプリコンテンツを OTA で公開できるようにするには、コンテンツ同期ハンドラーを設定する必要があります。
>
>詳しくは、 [モバイルとコンテンツ同期](/help/mobile/phonegap-contentsync.md) 詳しくは、開発者向けの節を参照してください。

ここでは、AEM Sites内と同じ方法で、AEM Mobileでコンテンツを作成、編集および削除できます。

この **ページコンテンツを管理タイル** 特定のペイロードに対する管理コンテンツのページ数と最終変更日を表示します。 タイル内の各レコードをクリックして、コンテンツをドリルダウンし、ページの作成、コピー、移動、削除、更新をおこなうことができます。

コンテンツが更新されると、管理者は、 **コンテンツパッケージを管理タイル。**

![chlimage_1-161](assets/chlimage_1-161.png)

リストに表示されたコンテンツパッケージの 1 つを選択して、コンテンツの作成または編集 ( ページの作成、編集または削除、ナビゲーションとページ順序の変更、コピー（テキスト）やメディアなどのコンテンツの作成または更新など ) を行います。

注意 *すべてがコンテンツ*&#x200B;つまり、アプリのスタイル、コピー（テキスト）、メディア、ページ、ナビゲーション、コンテンツのターゲティングは、すべて OTA で編集および更新でき、アプリストアにアクセスする必要はありません。

AEM Mobileコンテンツを編集するには、AEM作成者は、AEMコンテンツ編集インターフェイスに関する明確な理解が必要です。 [AEMでのページのオーサリング。](/help/sites-authoring/qg-page-authoring.md)

## コンテンツパッケージを管理タイル {#the-manage-content-packages-tile}

ここで *AEM Administrators* は、開発者やアプリストアを再送信しなくても、魅力的なエクスペリエンスと最新のコンテンツを提供して、ブランドエンゲージメントを促進し、ビジネス目標を満たすために、すばやく簡単にアプリを更新できます。

![chlimage_1-162](assets/chlimage_1-162.png)

1 回 *AEM 作成者* コンテンツを管理タイルでコンテンツを追加または変更した *AEM Administrators* は、コンテンツパッケージの更新をおこなって、変更をお客様に提示できます。

コンテンツパッケージアクションを使用すると、 *AEM オーサー* 開発チームがナビゲーション、スタイル、サーバー側ロジック、テンプレート、コンポーネントなどのホストアプリケーションの設計と実装を変更し、それらの変更を OTA にプッシュして、配布用に様々なストアに再送信する必要はありません。

**新しいコンテンツまたは更新されたコンテンツを公開するには**

タイルからコンテンツパッケージ（この例では英語のパッケージ）を選択します。 コンテンツ更新ダイアログボックスに関連する *コンテンツ同期* 設定。 前回の更新以降にアプリのコンテンツが変更されている場合は、ステータスが表示されます *保留中*、以下に示すように。

![chlimage_1-163](assets/chlimage_1-163.png)

次に、 **ステージ** アクションを使用して、コンテンツ更新を作成することができます。 適切な更新情報を追加し、「完了」を押します。

![chlimage_1-164](assets/chlimage_1-164.png)

この *コンテンツ同期* 次に、ハンドラーはデルタ ( *のみ* 変更内容 )。 完了すると、この更新コンテンツパッケージは、次に示すようにステージングされます。

コンテンツの更新をステージングすると、OTA でモバイルデバイスに公開する前に、複数の更新をおこなうことができます。

>[!NOTE]
>
>ステージングされたコンテンツは、公開前にAEM Verify アプリを使用して検証できます。
>
>詳しくは、 [AEM Verify のモバイルクイックスタート](/help/mobile/phonegap-mobile-quickstart.md) 詳しくは、 AEM Verify アプリを参照してください。

![chlimage_1-165](assets/chlimage_1-165.png)

コンテンツ同期 OTA を使用して、アプリユーザーに新しいコンテンツを配信する準備が整ったら、 **公開** 以下に示すように。

![chlimage_1-166](assets/chlimage_1-166.png)

### 次の手順 {#the-next-steps}

アプリケーションダッシュボードでのアプリコンテンツの作成と管理について学習したら、他のオーサリングの役割に関する次のリソースを参照してください。

* [アプリを管理タイル](/help/mobile/phonegap-app-details-tile.md)
* [アプリのメタデータの編集](/help/mobile/phonegap-editmetadata.md)
* [アプリの定義](/help/mobile/phonegap-app-definitions.md)
* [アプリを作成ウィザードを使用した新しいアプリの作成](/help/mobile/phonegap-create-new-app.md)
* [既存のハイブリッドアプリの読み込み](/help/mobile/phonegap-adding-content-to-imported-app.md)

### その他のリソース {#additional-resources}

管理者および開発者の役割と責務について詳しくは、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向け開発](/help/mobile/developing-in-phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
