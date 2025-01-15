---
title: モバイルアプリケーションのオーサリング
description: AEM Mobile ダッシュボードを使用すると、モバイルアプリケーションを作成、構築およびデプロイしたり、アプリケーションのメタデータを作成、削除および編集したりできます。 このページでは、この機能について詳しく見ていきます。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
exl-id: 073daff7-0c1d-4715-bfd4-3e2336e4cb88
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 2%

---

# モバイルアプリケーションのオーサリング{#authoring-mobile-applications}

{{ue-over-mobile}}

AEM Mobile ダッシュボードを使用すると、モバイルアプリケーションを作成、構築およびデプロイしたり、アプリケーションのメタデータを作成、削除および編集したりできます。 アプリケーションが実稼働したら、ライフサイクルや使用状況指標などのアプリケーション分析を分析して、顧客コンバージョンやブランドロイヤルティを向上させることができます。

AEM Mobile アプリケーションを構築するには、[ モバイルアプリケーションの構築 ](/help/mobile/building-app-mobile-phonegap.md) ページを参照してください。

環境の設定と開始については、[AEM PhoneGap Enterprise を使用するためのAEMの管理 ](/help/mobile/administer-phonegap.md) を参照してください。

## AEM Mobile アプリカタログ {#the-aem-mobile-apps-catalog}

[AEM Mobile アプリカタログ ](http://localhost:4502/aem/apps.html/content/phonegap) には、AEMで管理されるすべてのモバイルアプリが表示されます。

このカタログは、AEM Mobileの「ランディングページ」と考えることができます。管理者は、テンプレートに基づいて作成するか、モバイル開発者が既に開始した既存のアプリをアップロードすることで、新しいAEM Mobile アプリケーションを開始できます。

次の手順に従って、アプリカタログのランディングページに移動します。

1. **ナビゲーション** を参照し、「**モバイル**」を選択します。

1. **アプリ** を選択して、アプリカタログを開きます。

![AEM Mobile アプリ カタログ ](assets/chlimage_1-135.png)

## AEM Mobile アプリダッシュボード {#the-aem-mobile-app-dashboard}

カタログからAEM Mobile アプリを選択すると、そのダッシュボードが表示されます。 ここでは、アプリケーションの管理、統計の表示、モバイルアプリのコンテンツの作成、デプロイ、管理を行うことができます。

AEM Mobile ダッシュボードの各タイルに展開して詳細を表示または編集するには、右下隅の「。..」をクリックします。

![AEM Mobile アプリケーション コマンド センター ](assets/chlimage_1-136.png)

### アプリを管理タイル {#the-manage-app-tile}

アプリを管理タイルには、アプリケーションのアイコン、名前、説明、サポートされているプラットフォーム、アップデートの URL とバージョン情報のオートコールが表示されます。 このタイルにドリルダウンして、PhoneGap アプリケーション設定（config.xml）を編集および管理し、配布用のさまざまなアプリケーションストアへの送信用にアプリケーションを準備できます。

詳しくは、[ ここ ](/help/mobile/phonegap-app-details-tile.md) をクリックしてください。

![chlimage_1-137](assets/chlimage_1-137.png)

### ページコンテンツを管理タイル {#the-manage-page-content-tile}

AEM Sites内で行うのと同じ方法で、AEM Mobileでコンテンツを作成、更新、削除できます。 **ページコンテンツを管理** タイルには、管理コンテンツのページ数と最終変更日が表示されます。 コンテンツをドリルインし、タイル内の各レコードをクリックしてページを作成、コピー、移動、削除、更新できます。 コンテンツが更新されたら、**コンテンツパッケージの管理** タイルを通じてコンテンツの更新を顧客にプッシュできます。

![ コンテンツタイル ](assets/chlimage_1-138.png)

### コンテンツパッケージを管理タイル {#the-manage-content-packages-tile}

ページコンテンツを管理タイルでコンテンツを追加または変更すると、コンテンツリリースの更新でこれらの変更を顧客にプッシュできます。

コンテンツパッケージを使用すると、AEM アプリ作成者はAEMでページコンテンツを管理し、開発チームに PhoneGap Shell アプリケーション（アプリのフレームワークやインフラストラクチャ）を変更してもらってから、それらの変更をすばやく顧客にプッシュすることができ、開発者を登録して様々なストアに再提出して配布する必要がなくなります。

コンテンツパッケージは、更新ごとにコンテンツリリースパッケージと見なされる ZIP ファイルを作成します。 これらのパッケージには、アプリケーションのレンダリング中に生成される html リソースと html ページが含まれています。また、これらのファイルは、前回の更新以降に変更されたファイルのみをパッケージ化するほどインテリジェントです。

コンテンツパッケージを管理タイルの **タイプ** 列には、アプリケーションシェルのコンテンツ（開発者が管理するアプリのフレームワークやインフラストラクチャなど）を示す「アプリ」か、コンテンツ作成者が管理するページコンテンツを表す「コンテンツ」のいずれかが表示されます。

コンテンツは、言語として、または複数のコンテンツリリースパッケージがアプリで使用されるアプリの特定の部分として表すことができます。 コンテンツのバンドル方法の選択は、アプリケーションのコンテンツの管理方法に合わせて柔軟に行います。

**変更済み** 列は、ページが最後に変更された日時を示します。

**ステージング済み** 列には、最後のコンテンツ更新が作成された日時が表示されます。 コンテンツの更新を作成し変更をステージ化するには、タイル内の任意のレコードを開いて更新を作成します。

**公開済み** 列には、最新のコンテンツ更新が公開され、顧客が使用できるようになった日時が表示されます。 コンテンツを公開するには、まずそのコンテンツをステージングしてから、このタイルにドリルしてコンテンツリリースの詳細コンソールから公開して、更新を公開する必要があります。

![ アプリシェル用のコンテンツリリースタイル ](assets/chlimage_1-139.png)![ContentSync パッケージ ](do-not-localize/chlimage_1-5.png)

このアイコンは、アプリシェルのコンテンツリリースパッケージを表します

![ コンテンツリリースパッケージアイコンが 2 つの正方形で示され、パッケージシンボルが重なっています。](do-not-localize/chlimage_1-6.png)

これらのアイコンは、アプリコンテンツのコンテンツリリースパッケージを表します

### PhoneGap Buildタイル {#the-phonegap-build-tile}

**PhoneGap Build タイル** は `https://build.phonegap.com` と接続して、リモート ビルドをビルドおよびホストします。 ビルドが完了すると、ビルドはダウンロードとして、または QR コードを使用してデバイスに直接公開できます。

または、PhoneGap CLI （`https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html`）を介してローカルに構築するデバイスソースをダウンロードすることもできます。

![PhoneGap Build タイル ](assets/chlimage_1-140.png)

### 指標タイル {#the-metrics-tile}

>[!CAUTION]
>
>指標タイルは、クラウドサービスを設定した後にのみ表示されます。
>
>詳しくは [Adobe Mobile ServicesCloud Serviceの設定 ](/help/mobile/configure-adobe-mobile-cloud-service.md) を参照してください。

AEM Mobileは、[Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile.html) （AMS）を通じてAdobe Analyticsと統合されます。

コントロールセンター **指標タイル** には、アプリケーションの AMS から取得した概要分析が表示されます。 右下の「。..」をクリックして、分析ダッシュボードにドリルダウンできます。

![ 指標タイル ](assets/chlimage_1-141.png)

### エンティティコンテンツを管理タイル {#the-manage-entity-content-tile}

エンティティコンテンツを管理タイルでは、アプリ定義を追加および管理できます。 アプリ定義は、アプリに適したスペース（およびその他の設定）を識別する方法です。 これにより、アプリを再コンパイルすることなく、新しいスペースを追加できます。 アプリ定義が更新され、新しいスペースの情報が含まれます。

アプリ定義を作成および管理するには、[ ここ ](/help/mobile/phonegap-app-definitions.md) をクリックします。

右下の「。..」をクリックして、エンティティコンテンツを管理ダッシュボードにドリルインできます。

![chlimage_1-142](assets/chlimage_1-142.png)

#### その他のリソース {#additional-resources}

管理者と開発者の役割と責任については、以下のリソースを参照してください。

* [AEMを使用したAdobe PhoneGap Enterprise 向けの開発](/help/mobile/developing-in-phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
