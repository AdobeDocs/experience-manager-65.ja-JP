---
title: モバイルアプリケーションのオーサリング
description: AEM Mobile Dashboard を使用すると、モバイルアプリケーションの作成、構築およびデプロイ、アプリケーションメタデータの作成、削除および編集をおこなえます。 このページでは、この機能について詳しく見ていきます。
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 2%

---

# モバイルアプリケーションのオーサリング{#authoring-mobile-applications}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

AEM Mobileダッシュボードを使用すると、モバイルアプリケーションの作成、構築およびデプロイ、アプリケーションメタデータの作成、削除および編集をおこなえます。 アプリケーションが稼働したら、ライフサイクル指標や使用指標を含むアプリケーション分析を実行して、顧客コンバージョンとブランドロイヤルティを向上させることができます。

AEM Mobileアプリケーションを構築するには、 [モバイルアプリケーションの構築](/help/mobile/building-app-mobile-phonegap.md) ページに貼り付けます。

環境を設定して使い始めるには、 [AEM PhoneGap Enterprise を使用するためのAEMの管理](/help/mobile/administer-phonegap.md).

## AEM Mobile Apps カタログ {#the-aem-mobile-apps-catalog}

The [AEM Mobile Apps カタログ](http://localhost:4502/aem/apps.html/content/phonegap) は、AEMで管理されているすべてのモバイルアプリを表示します。

このカタログは、AEM Mobileの「ランディングページ」と考えて、管理者は、テンプレートに基づいて作成するか、モバイル開発者が既に開始した既存のアプリをアップロードすることで、新しいAEM Mobileアプリを開始できます。

アプリカタログのランディングページにアクセスするには、次の手順に従います。

1. 参照先 **ナビゲーション** 次を選択します。 **モバイル**.

1. 選択 **アプリ** をクリックして、アプリカタログを開きます。

![AEM Mobile Apps カタログ](assets/chlimage_1-135.png)

## AEM Mobile App ダッシュボード {#the-aem-mobile-app-dashboard}

カタログからAEM Mobileアプリを選択すると、そのアプリのダッシュボードが表示されます。 ここでは、アプリの管理、統計の表示、モバイルアプリコンテンツの構築、デプロイおよび管理をおこなうことができます。

AEM Mobileダッシュボードの各タイルを展開して、右下隅の「。..」をクリックして、詳細を表示または編集できます。

![AEM Mobile Applications コマンドセンター](assets/chlimage_1-136.png)

### アプリを管理タイル {#the-manage-app-tile}

アプリを管理タイルには、アプリケーションのアイコン、名前、説明、サポートされているプラットフォーム、更新用のホーム URL およびバージョン情報が表示されます。 このタイルをドリルダウンして、PhoneGap アプリケーション設定 (config.xml) を編集および管理し、配布用に様々なアプリケーションストアに送信するためのアプリケーションを準備できます。

クリック [ここ](/help/mobile/phonegap-app-details-tile.md) 」を参照してください。

![chlimage_1-137](assets/chlimage_1-137.png)

### ページコンテンツを管理タイル {#the-manage-page-content-tile}

AEM Sites内でおこなう場合と同じ方法で、AEM Mobileでコンテンツを作成、更新および削除できます。 The **ページコンテンツを管理タイル** 管理されているコンテンツのページ数と最終変更日を表示します。 タイル内の各レコードをクリックして、コンテンツをドリルダウンし、ページの作成、コピー、移動、削除、更新をおこなうことができます。 コンテンツが更新されたら、 **コンテンツパッケージを管理タイル。**

![コンテンツタイル](assets/chlimage_1-138.png)

### コンテンツパッケージを管理タイル {#the-manage-content-packages-tile}

ページコンテンツを管理タイルでコンテンツを追加または変更したら、コンテンツリリースの更新を使用して、変更を顧客にプッシュできます。

コンテンツパッケージを使用すると、AEMアプリ作成者はAEMでページコンテンツを管理し、開発チームに PhoneGap Shell アプリケーション（アプリフレームワークまたはインフラストラクチャ）を変更してもらい、開発者に配布用に様々なストアに再送信する必要がありません。

コンテンツパッケージは、更新ごとにコンテンツリリースパッケージと見なされる ZIP ファイルを作成します。 これらのパッケージには、アプリのレンダリング時に生成される html リソースと html ページが含まれ、最後の更新以降に変更されたファイルのみをパッケージ化するのに十分なインテリジェントです。

コンテンツパッケージを管理タイルの **タイプ** 列には、開発者が管理するアプリのフレームワークやインフラストラクチャなど、アプリケーションシェルのコンテンツを示す「アプリ」、またはコンテンツ作成者が管理するページコンテンツを表す「コンテンツ」が表示されます。

コンテンツは、言語として、またはアプリで複数のコンテンツリリースパッケージを使用するアプリの特定の部分として表すことができます。 コンテンツのバンドル方法の選択は柔軟で、アプリケーションのコンテンツ管理方法に応じて異なります。

The **変更済み** 列には、ページが最も最近変更された日時が示されます。

The **Staged** 列には、最後のコンテンツ更新がいつ作成されたかが表示されます。 コンテンツの更新を作成して変更をステージングするには、タイル内の任意のレコードを開き、更新を作成します。

The **公開済み** 列には、最後のコンテンツ更新が公開され、顧客が使用できるようになった日時が表示されます。 コンテンツを公開するには、まずそのコンテンツをステージングしてから、このタイルにドリルダウンしてコンテンツリリースの詳細コンソールから公開することで、更新を公開する必要があります。

![コンテンツリリースタイル](assets/chlimage_1-139.png) ![アプリシェルのコンテンツ同期パッケージ](do-not-localize/chlimage_1-5.png)

このアイコンは、アプリシェルのコンテンツリリースパッケージを表します

![2 つの四角形で重なっているパッケージシンボルで示されるコンテンツリリースパッケージアイコン。](do-not-localize/chlimage_1-6.png)

これらのアイコンは、アプリコンテンツのコンテンツリリースパッケージを表します

### PhoneGap Buildタイル {#the-phonegap-build-tile}

The **PhoneGap Buildタイル** 次と接続： `https://build.phonegap.com` リモートビルドを構築し、ホストします。 ビルドが完了すると、ビルドはダウンロードとして、または QR コードを介して直接デバイスで利用できるようになります。

または、PhoneGap CLI (`https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html`) をクリックします。

![PhoneGap Buildタイル](assets/chlimage_1-140.png)

### 指標タイル {#the-metrics-tile}

>[!CAUTION]
>
>指標タイルは、Cloud Service を設定した後にのみ表示されます。
>
>詳しくは、 [AdobeMobile ServicesCloud Service](/help/mobile/configure-adobe-mobile-cloud-service.md) 」を参照してください。

AEM MobileとAdobe Analyticsの統合 [AdobeMobile Services SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=en) (AMS) を使用します。

コントロールセンター **指標タイル** アプリケーション用に AMS から取得した概要分析を表示します。 右下の「。..」をクリックして、Analytics ダッシュボードにドリルダウンできます。

![指標タイル](assets/chlimage_1-141.png)

### エンティティコンテンツを管理タイル {#the-manage-entity-content-tile}

エンティティコンテンツを管理タイルでは、アプリの定義を追加および管理できます。 アプリの定義は、アプリに適したスペース（およびその他の設定）を特定する方法です。 これにより、アプリを再コンパイルする必要なく、新しいスペースを追加できます。 アプリの定義が更新され、新しいスペースに関する情報が含まれます。

クリック [ここ](/help/mobile/phonegap-app-definitions.md) をクリックして、アプリの定義を作成および管理します。

右下の「。..」をクリックして、エンティティコンテンツを管理ダッシュボードにドリルダウンできます。

![chlimage_1-142](assets/chlimage_1-142.png)

#### その他のリソース {#additional-resources}

管理者および開発者の役割と責務について詳しくは、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向け開発](/help/mobile/developing-in-phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
