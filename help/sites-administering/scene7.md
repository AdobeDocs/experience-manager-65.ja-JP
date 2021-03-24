---
title: Dynamic MediaClassicとの統合
description: Adobe Experience ManagerとDynamic Mediaクラシックの統合方法を学びます。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: ef975961ddcd6910b5fba2dea7e9302921f45055
workflow-type: tm+mt
source-wordcount: '5511'
ht-degree: 12%

---


# Dynamic MediaClassicとの統合{#integrating-with-dynamic-media-classic-scene}

AdobeDynamic Mediaクラシックは、リッチメディアアセットを管理、強化、公開、およびWeb、モバイル、電子メール、インターネットに接続されたディスプレイや印刷に配信するためのホストソリューションです。

Dynamic Mediaクラシックを使用するには、Dynamic MediaクラシックとAdobe Experience Managerアセットが相互にやり取りできるようにクラウド設定を設定する必要があります。 このドキュメントでは、Experience ManagerとDynamic Mediaクラシックを設定する方法を説明します。

すべてのDynamic Mediaクラシックコンポーネントをページで使用し、ビデオを操作する方法については、[Dynamic Mediaクラシックを使用する](../assets/scene7.md)を参照してください。

>[!NOTE]
>
>* Dynamic MediaクラシックのDHTMLビューアプラットフォームは、2014年1月31日に正式に提供終了となりました。 詳しくは、[DHTMLビューアの提供終了に関するFAQ](../sites-administering/dhtml-viewer-endoflifefaqs.md)を参照してください。
>* Experience Managerと連携するようにDynamic Mediaクラシックを設定する前に、「[ベストプラクティス](#best-practices-for-integrating-scene-with-aem)」で、Dynamic MediaクラシックとExperience Managerの統合を参照してください。
>* カスタムプロキシ設定でDynamic Mediaクラシックを使用する場合は、HTTPクライアントプロキシ設定の両方を設定する必要があります。これは、Experience Managerの一部の機能では3.x APIを使用し、残りの機能では4.x APIを使用するからです。 3.xは[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)で設定し、4.xは[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)で設定します。

>



## Experience Manager/Dynamic Mediaクラシック統合とDynamic Media{#aem-scene-integration-versus-dynamic-media}

Experience Managerユーザーは、Dynamic Mediaと連携する2つのソリューションから選択できます。 次のいずれかを使用できます。

* Experience ManagerのインスタンスをDynamic Mediaクラシックと統合します。
* Experience Managerに統合されたDynamic Mediaを使う。

次の条件を使用して、どちらのソリューションを選択するかを決定します。

* リッチメディアアセットが公開と配信のためにDynamic Mediaクラシックに存在する&#x200B;**既存の** Dynamic Mediaクラシックのお客様で、これらのアセットをSites (WCM)オーサリングやExperience Managerアセットと統合する場合は、このドキュメントで説明する[Experience Manager/Dynamic Mediaクラシックポイントツーポイント統合](#aem-scene-point-to-point-integration)を使用します。

* リッチメディア配信のニーズを持つ&#x200B;**新しい** Experience Managerのお客様の場合は、[Dynamic Mediaオプション](#aem-dynamic-media)を選択します。 このオプションは、既存の S7 アカウントを持たず、システムに多くのアセットを保存している場合に最も有用です。

* 場合によっては、両方のソリューションを使用します。 [二重使用のシナリオ](/help/sites-administering/scene7.md#dual-use-scenario)は、そのシナリオを説明します。

### Experience Manager/Dynamic Mediaクラシックポイントツーポイント統合{#aem-scene-point-to-point-integration}

このソリューションのアセットを使用して作業する場合、次のいずれかの操作をおこないます。

* アセットを直接Dynamic Mediaクラシックにアップロードし、**Dynamic Mediaクラシック**&#x200B;コンテンツブラウザーを介してアクセスして、ページオーサリングや
* Experience Managerアセットにアップロードして、Dynamic Mediaクラシックへの自動公開を有効にする&#x200B;**アセット**&#x200B;コンテンツブラウザーを介して、ページのオーサリングにアクセス

この統合に使用するコンポーネントは、[デザインモードの&#x200B;**Dynamic Mediaクラシック**&#x200B;コンポーネント領域にあります。](/help/sites-authoring/author-environment-tools.md#page-modes)

### Experience ManagerDynamic Media{#aem-dynamic-media}

Experience ManagerDynamic Mediaは、Experience Managerプラットフォーム内で直接Dynamic Mediaクラシック機能を統合したものです。

このソリューションのアセットを使用して作業する場合、次のワークフローに従います。

1. 1つの画像およびビデオアセットをExperience Managerに直接アップロードします。
1. Experience Manager内でビデオを直接エンコードする。
1. Experience Manager内で直接画像ベースのセットを作成します。
1. 必要に応じて、画像やビデオにインタラクティブ機能を追加する。

ダイナミックメディア用に使用するコンポーネントは、**[!UICONTROL デザインモード]**&#x200B;の[ダイナミックメディア](/help/sites-authoring/author-environment-tools.md#page-modes)コンポーネント領域にあります。これらには、次が含まれます。

* **[!UICONTROL ダイナミックメディア]** - **[!UICONTROL ダイナミックメディア]**&#x200B;コンポーネントでは、追加しているアセットが画像であるかビデオであるかに応じて、様々なオプションを使用できます。このコンポーネントは画像プリセット、画像ベースのビューア（画像セット、スピンセット、混在メディアセットなど）およびビデオをサポートします。また、ビューアのレスポンシブ性が高く、画面のサイズに基づいて画面のサイズが自動的に変更されます。 すべてのビューアは HTML5 ビューアです。

* **[!UICONTROL インタラクティブメディア]** - **[!UICONTROL インタラクティブ]** メディアコンポーネントは、カルーセルバナー、インタラクティブ画像、インタラクティブビデオなどのアセット用です。このようなアセットは、その中にこのようなホットスポットや画像マップなどのインタラクティブ機能を持ちます。 この部品はスマートです。 つまり、画像を追加するかビデオを追加するかに応じて、様々なオプションがあります。 また、ビューアのレスポンシブ性が高く、画面のサイズに基づいて画面のサイズが自動的に変更されます。 すべてのビューアは HTML5 ビューアです。

### 両方を利用するシナリオ  {#dual-use-scenario}

初期設定では、Dynamic MediaとDynamic Mediaクラシックの両方のExperience Manager統合機能を同時に使用できます。 次の使用例の表では、特定の領域のオン/オフを切り替えた場合について説明します。

Dynamic MediaとDynamic Mediaクラシックを同時に使用するには：

1. Cloud Servicesで[Dynamic Mediaクラシック](#creating-a-cloud-configuration-for-scene)を設定します。
1. 次の中からお使いのユースケースに合致する手順を実行します。

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Dynamic Mediaクラシック統合</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>実行する操作...</strong></td>
    <td><strong>ユースケースのワークフロー</strong></td>
    <td><strong>画像／ビデオ</strong></td>
    <td><strong>ダイナミックメディアコンポーネント</strong></td>
    <td><strong>S7 コンテンツブラウザーとコンポーネント</strong></td>
    <td><strong>Assets から S7 への自動アップロード</strong></td>
    </tr>
    <tr>
    <td>Sites とダイナミックメディアを初めて使用する</td>
    <td>アセットをExperience Managerにアップロードし、Experience ManagerDynamic Mediaコンポーネントを使用して、サイトページにアセットをオーサリングする</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td>
    <td>オフ</td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>小売業界、サイトとDynamic Mediaを初めて使用</td>
    <td>管理と配信のために、非製品アセットをExperience Managerにアップロードします。 PRODUCTアセットをDynamic Mediaクラシックにアップロードし、Experience ManagerとコンポーネントでDynamic Mediaクラシックコンテンツブラウザを使用して、サイトに商品詳細ページを作成します。</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>Assets とダイナミックメディアを初めて使用する</td>
    <td>Experience Managerアセットにアセットをアップロードし、Dynamic Mediaから公開されたURL/埋め込みコードを使用</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td>オフ</td>
    <td>オフ</td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>ダイナミックメディアを使用して初めてテンプレートを作成する</td>
    <td>Dyamic Media を使用して画像とビデオを作成する。Dynamic Mediaクラシックで画像テンプレートを作成し、Dynamic Mediaクラシックコンテンツファインダーを使用して、サイトページにテンプレートを含めます。</td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">オン</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>既存のDynamic Mediaクラシックのお客様で、Sitesを初めてお使いになる方</td>
    <td>Dynamic Mediaクラシックにアセットをアップロードし、Experience ManagerDynamic Mediaクラシックコンテンツブラウザを使用して、サイトページでアセットを検索し、オーサリングする</td>
    <td>オフ</td>
    <td>オフ</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td>オフ</td>
    </tr>
    <tr>
    <td>既存のDynamic Mediaクラシックのお客様で、サイトとアセットを初めてお使いになる場合</td>
    <td>DAMにアセットをアップロードし、配信用に自動的にDynamic Mediaクラシックに公開します。 Experience ManagerDynamic Mediaクラシックコンテンツブラウザを使用して、サイトページでアセットを検索し、オーサリングします。</td>
    <td>オフ</td>
    <td>オフ</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">オン</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">オン</a></p> <p>（手順 4 を参照）</p> </td>
    </tr>
    <tr>
    <td>既存のDynamic Mediaクラシックのお客様と新規のアセット</td>
    <td><p>アセットをExperience Managerにアップロードし、Dynamic Mediaを使用してダウンロード/共有用のレンディションを生成します。 Experience Managerアセットを配信用にDynamic Mediaクラシックに自動的に公開します。</p> <p><strong>重要：</strong> 重複処理とExperience Managerで生成されたレンディションがDynamic Mediaクラシックに同期されません</p> </td>
    <td><p>オン</p> <p>（手順 3 を参照）</p> </td>
    <td>オフ</td>
    <td>オフ</td>
    <td><p><a href="#configuringautouploadingfromaemassets">オン</a></p> <p>（手順 4 を参照）</p> </td>
    </tr>
    </tbody>
    </table>

1. (オプション、（使用事例の表を参照） — [Dynamic Mediaクラウドの設定](/help/assets/config-dynamic.md)と[Dynamic Mediaサーバー](/help/assets/config-dynamic.md)を有効にします。
1. (オプション、「使用事例の表を参照) - 「アセットからDynamic Mediaクラシックへの自動アップロード」を有効にする場合は、次を追加する必要があります。

   1. Dynamic Mediaクラシックへの自動アップロードを設定します。
   1. &lt;a3追加/> **Dam更新アセット**&#x200B;ワークフロー(`https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`)の最後にあるDynamic Mediaワークフローの手順&#x200B;*の後の&#x200B;**Dynamic Mediaクラシックアップロード**の手順*
   1. （オプション）[https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)のMIMEタイプで、Dynamic Mediaクラシックアセットのアップロードを制限します。 このリストにないアセットのMIMEタイプは、Dynamic Mediaクラシックサーバーにアップロードされません。
   1. （オプション）ビデオをDynamic Mediaクラシック設定でセットアップします。 ビデオエンコーディングは、Dynamic MediaとDynamic Mediaクラシックのどちらかまたは両方で同時に有効にできます。 ダイナミックレンディションは、Experience Managerインスタンスでのローカルなプレビューおよび再生に使用されますが、Dynamic Mediaクラシックビデオレンディションは、Dynamic Mediaクラシックサーバーで生成および保存されます。 Dynamic MediaとDynamic Mediaクラシックの両方にビデオエンコーディングサービスを設定する場合は、[ビデオ処理プロファイル](/help/assets/video-profiles.md)をDynamic Mediaクラシックのアセットフォルダーに適用します。
   1. （オプション）[Dynamic Mediaクラシック](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)でセキュアプレビューを設定します。

#### 制限事項 {#limitations}

Dynamic MediaクラシックとDynamic Mediaの両方を有効にしている場合、次の制限があります。

* アセットを選択し、Experience ManagerページのDynamic Mediaクラシックコンポーネントにドラッグして手動でDynamic Mediaクラシックにアップロードすると、機能しません。
* Experience ManagerDynamic Mediaクラシックの同期アセットは、アセットで編集すると自動的にDynamic Mediaクラシックに更新されますが、ロールバック操作では新しいアップロードがトリガーされません。 したがって、ロールバックの直後には、Dynamic Mediaクラシックでは最新バージョンは取得されません。 回避策として、ロールバックの完了後に再度編集する必要があります。
* ある使用例にDynamic Mediaを、別の用途にDynamic Mediaクラシックを統合してDynamic MediaアセットがDynamic Mediaクラシックとやり取りしないようにする必要がある場合は、Dynamic Mediaクラシック設定をDynamic Mediaフォルダに適用しないでください。 また、Dynamic Media設定(処理プロファイル)をDynamic Mediaクラシックフォルダに適用しないでください。

## Dynamic MediaクラシックとExperience Manager{#best-practices-for-integrating-scene-with-aem}の統合のベストプラクティス

Dynamic MediaクラシックをExperience Managerと統合する場合、次の領域で注意が必要な重要なベストプラクティスがいくつかあります。

* 統合のテストドライブ
* 特定のシナリオで推奨されるDynamic Mediaクラシックからのアセットの直接アップロード

[既知の制限](#known-limitations-and-design-implications)を参照してください。

### 統合のテストドライブ {#test-driving-your-integration}

Adobeでは、ルート会社ーがフォルダー全体ではなく、サブフォルダーのみを参照することで、統合をテスト駆動することをお勧めします。

>[!CAUTION]
>
>既存のDynamic Mediaクラシック会社アカウントからアセットを読み込むと、Experience Managerで表示するのに時間がかかる場合があります。 アセット数が多すぎない（例えば、ルートフォルダーに多すぎるアセットが含まれている場合が多く、システムをクラッシュさせる可能性がある）フォルダーを、Dynamic Mediaクラシックで指定してください。

### Experience ManagerアセットからのアセットのアップロードとDynamic Mediaクラシック{#uploading-assets-from-aem-assets-versus-from-scene}からのアセットのアップロード

アセットのアップロードは、アセット（デジタルアセット管理）機能を使用するか、Dynamic Mediaクラシックコンテンツブラウザを使用してExperience Manager内で直接Dynamic Mediaクラシックにアクセスする方法で行うことができます。 どちらを選択するかは、次の要素によって異なります。

* Experience ManagerアセットでまだサポートされていないDynamic Mediaクラシックアセットタイプは、Dynamic Mediaクラシックコンテンツブラウザを使用して、直接Dynamic MediaクラシックからExperience ManagerのWebサイトに追加する必要があります。 例えば、画像テンプレートを使用します。
* Experience ManagerアセットとDynamic Mediaクラシックの両方でサポートされるアセットタイプの場合、アセットのアップロード方法は次の項目に応じて決定します。

   * アセットが現在ある場所、および
   * 共有リポジトリでのそれらの管理の重要度

アセットが既にDynamic Mediaクラシックに存在し、共通のリポジトリで管理することが重要でない場合は、配信のためにDynamic Mediaクラシックに同期するためだけに、Experience Managerアセットに書き出すのは不要です。 アセットを単一のリポジトリに保持し、配信のためにのみDynamic Mediaクラシックと同期することをお勧めします。

## Dynamic Mediaクラシック統合の設定{#configuring-scene-integration}

Experience Managerを設定して、Dynamic Mediaクラシックにアセットをアップロードできます。 CQターゲットフォルダーのアセットは、Experience ManagerからDynamic Mediaクラシック会社アカウントに（自動または手動で）アップロードできます。

>[!NOTE]
>
>Dynamic Mediaクラシックアセットの読み込みには、指定したターゲットフォルダーのみを使用することをお勧めします。 ターゲットフォルダーの外部にあるデジタルアセットは、Dynamic Mediaクラシック設定が有効になっているページのDynamic Mediaクラシックコンポーネントでのみ使用できます。 また、これらはDynamic Mediaクラシックのアドホックフォルダーに配置されます。 アドホックフォルダーがExperience Managerと同期されません(ただし、アセットは、Dynamic Mediaクラシックコンテンツブラウザーで検出可能です)。

Experience Managerと統合するDynamic Mediaクラシックを設定するには、次の手順を実行する必要があります。

1. [クラウド設定の定義](#creating-a-cloud-configuration-for-scene) - AssetsフォルダーとDynamic MediaClassicフォルダーのマッピングを定義します。一方向(Dynamic MediaクラシックへのExperience Managerアセット)のみの同期を行う場合でも、この手順を実行します。
1. [OSGiconsoleで **Adobe CQs7dam Damリスナー**](#enabling-the-adobe-cq-scene-dam-listener)    — 完了を有効にします。
1. Experience Managerアセットを自動的にDynamic Mediaクラシックにアップロードする場合は、そのオプションをオンにし、Dynamic Mediaクラシックを[!UICONTROL DAM更新アセット]ワークフローに追加する必要があります。 また、手動でアセットをアップロードできます。
1. サイドキックへのDynamic Mediaクラシックコンポーネントの追加 この機能により、ユーザーはExperience ManagerページでDynamic Mediaクラシックコンポーネントを使用できます。
1. [Experience Manager](#enabling-scene-for-wcm)  — この手順は、Dynamic Mediaクラシックで作成したビデオプリセットを表示する場合に必要です。また、CQターゲットフォルダーの外部からDynamic Mediaクラシックにアセットを公開する必要がある場合にも必要です。

ここでは、これらのすべての手順の実行方法を説明し、重要な制限を示します。

### Dynamic MediaクラシックとExperience Managerアセットの同期の仕組み{#how-synchronization-between-scene-and-aem-assets-works}

Experience ManagerアセットとDynamic Mediaクラシックの同期を設定する場合は、次の点を理解する必要があります。

#### Experience ManagerアセットからDynamic Mediaクラシックにアップロード{#uploading-to-scene-from-aem-assets}

* Experience Manager内に、Dynamic Mediaクラシックのアップロード用に指定された同期フォルダーがあります。
* デジタルアセットが指定された同期フォルダーに配置されている場合は、Dynamic Mediaクラシックへのアップロードを自動化できます。
* フォルダー内のExperience Managerーとサブフォルダー構造は、Dynamic Mediaクラシックで複製されます。

>[!NOTE]
>
>Experience Managerは、すべてのメタデータをXMPとして埋め込んでからDynamic Mediaクラシックにアップロードするので、メタデータノードのすべてのプロパティはXMPとしてDynamic Mediaクラシックで使用できます。

#### Known limitations and design implications {#known-limitations-and-design-implications}

Experience ManagerアセットとDynamic Mediaクラシック間の同期では、現在、制限/デザイン上の影響は次のとおりです。

<table>
 <tbody>
  <tr>
   <td><strong>制限／設計の意味</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>指定された1つの同期(ターゲット)フォルダ</td>
   <td>Dynamic Mediaクラシックのアップロードでは、Experience Manager内の会社ごとに1つの指定フォルダーしか指定できません。 Dynamic Mediaクラシックの複数の会社アカウントにアクセスする必要がある場合は、複数の設定を作成できます。</td>
  </tr>
  <tr>
   <td>フォルダー構造</td>
   <td>アセットを含む同期フォルダーを削除すると、すべてのDynamic Mediaクラシックリモートアセットは削除されますが、フォルダーは残ります。</td>
  </tr>
  <tr>
   <td>アドホックフォルダー</td>
   <td>WCMのDynamic Mediaクラシックに手動でアップロードされたターゲットフォルダー外のアセットは、Dynamic Mediaクラシックの別のアドホックフォルダーに自動的に配置されます。 このフォルダーは、Experience Managerのクラウド設定で設定します。</td>
  </tr>
  <tr>
   <td>混在メディア</td>
   <td>混在メディアセットはExperience Managerではサポートされていませんが、Experience Managerで表示されます。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>Dynamic MediaクラシックのeCatalogで生成されたPDFは、CQターゲットフォルダーに読み込まれます。</td>
  </tr>
  <tr>
   <td>UI 更新</td>
   <td>Experience ManagerとDynamic Mediaクラシック間で同期を行う場合は、表示の変更に合わせてユーザインターフェイスを更新してください。 </td>
  </tr>
  <tr>
   <td>ビデオサムネール</td>
   <td>ビデオをExperience Managerアセットにアップロードして、Dynamic Mediaクラシック経由でエンコーディングする場合、ビデオのサムネールとエンコードされたビデオがExperience Managerアセットで使用可能になるまでに時間がかかる場合があります（ビデオの処理時間が異なります）。</td>
  </tr>
  <tr>
   <td>ターゲットサブフォルダー</td>
   <td><p>ターゲットフォルダ内のサブフォルダを使用する場合は、場所に関係なく各アセットに一意の名前を使用するか、場所に関係なくアセットが上書きされないようにDynamic Mediaクラシックを設定します。</p> <p>それ以外の場合は、Dynamic Mediaクラシックターゲットサブフォルダーにアップロードされた同じ名前のアセットはアップロードされますが、ターゲットフォルダー内の同じ名前のアセットは削除されます。 </p> </td>
  </tr>
 </tbody>
</table>

### Dynamic Mediaクラシックサーバーの設定{#configuring-scene-servers}

プロキシの背後でExperience Managerを実行する場合、または特別なファイアウォール設定を使用する場合は、異なる地域のホストを明示的に有効にする必要があります。 サーバーは`/etc/cloudservices/scene7/endpoints`内のコンテンツで管理され、必要に応じてカスタマイズできます。 URLをタップし、必要に応じて編集してURLを変更します。 以前のバージョンのExperience Managerでは、これらの値はハードコードされていました。

`/etc/cloudservices/scene7/endpoints.html`に移動すると、一覧に表示されているサーバーが表示されます（URLをタップして編集できます）。

![chlimage_1-296](assets/chlimage_1-296.png)

### Dynamic Mediaクラシック{#creating-a-cloud-configuration-for-scene}のクラウド設定の作成

クラウド設定では、Dynamic MediaクラシックフォルダーとExperience Managerアセットフォルダーのマッピングを定義します。 Experience ManagerアセットをDynamic Mediaクラシックと同期するように設定する必要があります。 詳しくは、同期の仕組みを参照してください。

>[!CAUTION]
>
>既存のDynamic Mediaクラシック会社アカウントからアセットを読み込むと、Experience Managerで表示するのに時間がかかる場合があります。 アセット数が多すぎないDynamic Mediaクラシックのフォルダーを指定していることを確認してください。 例えば、ルートフォルダーに含まれるアセットが多すぎる場合があります。
>
>統合をテストする場合は、ルート会社ーがサブフォルダー全体ではなく、サブフォルダーのみを指すようにします。

>[!NOTE]
>
>複数の設定を指定できます。1つのクラウド設定は、Dynamic Mediaクラシック会社の1人のユーザーを表します。 他のDynamic Mediaクラシック会社またはユーザにアクセスする場合は、複数の設定を作成する必要があります。

Experience ManagerがアセットをDynamic Mediaクラシックに公開できるように設定するには：

1. Experience Managerアイコンをタップし、**[!UICONTROL 導入/Cloud Services]**&#x200B;に移動して、AdobeDynamic Mediaクラシックにアクセスします。

1. 「**[!UICONTROL 今すぐ設定]**」をタップします。

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 「**[!UICONTROL タイトル]**」フィールド、およびオプションで「**[!UICONTROL 名前]**」フィールドで、適切な情報を入力します。「**[!UICONTROL 作成]**」をタップします。

   >[!NOTE]
   >
   >さらに構成を作成する場合、**[!UICONTROL 親構成]**&#x200B;フィールドが表示されます。
   >
   >親設定は&#x200B;**変更しない**&#x200B;でください。親設定の変更は、統合を解除する可能性があります。

1. Dynamic Mediaクラシックアカウントの電子メールアドレス、パスワード、地域を入力し、**[!UICONTROL Dynamic Mediaクラシックに接続]**&#x200B;をタップします。 Dynamic Mediaクラシックサーバに接続している場合は、ダイアログが拡張され、さらに多くのオプションが表示されます。

1. **[!UICONTROL 会社]**&#x200B;名と&#x200B;**[!UICONTROL ルートパス]**&#x200B;を入力します。 この情報は、パブリッシュされたサーバ名と、指定するパスです。 公開済みのサーバー名がわからない場合は、Dynamic Mediaクラシックで、**[!UICONTROL セットアップ/アプリケーション設定]**&#x200B;に移動します)。

   >[!NOTE]
   >
   >Dynamic Mediaクラシックのルートパスは、接続先のDynamic MediaクラシックExperience Managerです。 特定のフォルダーに絞り込むことができます。

   >[!CAUTION]
   >
   >Dynamic Mediaクラシックフォルダのサイズによっては、ルートフォルダの読み込みに時間がかかる場合があります。 また、Dynamic MediaクラシックのデータはExperience Managerストレージを超える可能性があります。 正しいフォルダーを読み込んでいることを確認してください。読み込むデータが多すぎると、システムが停止する可能性があります。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 「**[!UICONTROL OK]**」をクリックします。Experience Managerが設定を保存します。

>[!NOTE]
>
>再接続する場合：
>
>* 公開時にDynamic Mediaクラシックに再接続する場合、公開時または再接続時にパスワードをリセットしても機能しません（作成者インスタンスの問題ではありません）。
>* 地域、会社名などの値を変更した場合は、Dynamic Mediaクラシックに再接続する必要があります。 設定オプションが変更されたが保存されていない場合、Experience Managerは設定が有効であることを誤って示します。 必ず再接続するようにします。

>



### Adobe CQDynamic MediaクラシックDamリスナーを有効にする{#enabling-the-adobe-cq-scene-dam-listener}

Adobe CQDynamic MediaクラシックDamリスナーを有効にします。このリスナーは、デフォルトで無効になっています。

有効にするには：

1. [!UICONTROL ツール]アイコンをタップし、**[!UICONTROL 操作/Webコンソール]**&#x200B;に移動します。 Web コンソールが開きます。
1. **[!UICONTROL Adobe CQDynamic MediaクラシックDamリスナー]**&#x200B;に移動し、「**[!UICONTROL 有効]**」チェックボックスをオンにします。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 「**[!UICONTROL 保存]**」をタップします。

### 設定可能なタイムアウトをDynamic Mediaクラシックアップロードワークフローに追加{#adding-configurable-timeout-to-scene-upload-workflow}

Dynamic Mediaクラシックを使用してビデオエンコーディングを処理するようにExperience Managerインスタンスを設定した場合、デフォルトでは、アップロードジョブで35分のタイムアウトが発生します。 より長時間実行される可能性のあるビデオエンコーディングジョブに対応するために、次の設定を指定できます。

1. **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**&#x200B;に移動します。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 「**[!UICONTROL Active job timeout]**」フィールドの数値を目的の値に変更します。負以外の数値であれば、任意の数値を指定できます。単位は秒です。デフォルトでは、この数値は2100に設定されています。

   >[!NOTE]
   >
   >ベストプラクティス：ほとんどのアセットが長くても数分以内に収集されます（画像など）。ただし、例えば大きいビデオなどの場合は、長い処理時間を収容するために、タイムアウト値を7200秒（2時間）に増やします。 それ以外の場合は、このDynamic Mediaクラシックアップロードジョブは、JCRメタデータで&#x200B;**[!UICONTROL UploadFailed]**&#x200B;としてマークされます。

1. 「**[!UICONTROL 保存]**」をタップします。

### Experience Managerアセットからの自動アップロード{#autouploading-from-aem-assets}

Experience Manager6.3.2以降では、Experience Managerアセットは、アセットがCQターゲットフォルダー内にある場合、Asset ManagerにアップロードされたデジタルアセットがDynamic Mediaクラシックに更新されるように設定されます。

アセットがExperience Managerアセットに追加されると、自動的にアップロードされ、Dynamic Mediaクラシックに公開されます。

>[!NOTE]
>
>Experience ManagerアセットからDynamic Mediaクラシックに自動アップロードする場合の最大ファイルサイズは500 MBです。

Experience Managerアセットからの自動アップロードを設定するには：

1. Experience Managerアイコンをタップし、**[!UICONTROL 導入/Cloud Services]**&#x200B;に移動し、Dynamic Mediaの見出しの下の「利用可能な設定」で、**[!UICONTROL dms7 (Dynamic Media]**)をタップします
1. 「**[!UICONTROL 詳細]**」タブをタップし、「**[!UICONTROL 自動アップロードを有効にする]**」チェックボックスを選択して、「**[!UICONTROL OK]**」をタップします。 次に、DAM Assetワークフローを設定して、Dynamic Mediaクラシックへのアップロードを含める必要があります。

   >[!NOTE]
   >
   >アセットを非公開状態にしてDynamic Mediaクラシックにプッシュする方法については、[Dynamic Mediaクラシックにプッシュされたアセットの状態（公開/未公開）の設定](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)を参照してください。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Experience Managerのようこそページに戻り、**[!UICONTROL ワークフロー]**&#x200B;をタップします。 「**DAM アセットの更新**」ワークフローをダブルクリックして開きます。
1. サイドキックで、**[!UICONTROL ワークフロー]**&#x200B;コンポーネントに移動し、**[!UICONTROL Dynamic Mediaクラシック]**&#x200B;を選択します。 **[!UICONTROL Dynamic Mediaクラシック]**&#x200B;をワークフローにドラッグし、**[!UICONTROL 保存]**&#x200B;をタップします。 ターゲットフォルダー内のExperience Managerアセットに追加されたアセットは、Dynamic Mediaクラシックに自動的にアップロードされます。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 自動化後にアセットを追加する場合、アセットがCQターゲットフォルダーに配置されていないと、そのアセットはDynamic Mediaクラシックにアップロードされません。
   >* Experience Managerは、すべてのメタデータをXMPとして埋め込んでからDynamic Mediaクラシックにアップロードするので、メタデータノードのすべてのプロパティはXMPとしてDynamic Mediaクラシックで使用できます。


### Dynamic Mediaクラシックにプッシュされたアセットの状態（公開/未公開）の設定{#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Experience ManagerアセットからDynamic Mediaクラシックにアセットをプッシュする場合は、アセットを自動的に公開する（初期設定の動作）か、非公開状態のDynamic Mediaクラシックに公開します。

実稼動前にステージング環境でアセットをテストする場合は、Dynamic Mediaクラシックにアセットをすぐに公開しないことが考えられます。 Dynamic Mediaクラシックのセキュアテスト環境でExperience Managerを使用すると、アセットを非公開状態で直接Dynamic Mediaクラシックにプッシュできます。

Dynamic Mediaクラシックのアセットは、セキュアプレビューを通じて引き続き使用できます。 Experience Manager内でアセットが公開された場合にのみ、Dynamic Mediaクラシックアセットも実稼動環境に移行します。

アセットをDynamic Mediaクラシックにプッシュしたときに、すぐにアセットを公開する場合は、オプションを設定する必要はありません。 この機能はデフォルトの動作です。

ただし、Dynamic Mediaクラシックにアセットをプッシュして自動的に公開しないようにするには、この節では、Experience ManagerとDynamic Mediaクラシックを設定してこの機能を実行する方法について説明します。

#### アセットを非公開のDynamic Mediaクラシックにプッシュするための前提条件{#prerequisites-to-push-assets-to-scene-unpublished}

アセットを公開せずにDynamic Mediaクラシックにプッシュするには、次の設定を行う必要があります。

1. [Admin Console を使用して、サポートケースを作成します。](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) サポートケースで、Dynamic Mediaクラシックアカウントのセキュアプレビューを有効にするようにリクエストします。
1. [Dynamic Mediaクラシックアカウントのセキュアプレビューを設定するには、に従ってください。](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

以下の手順は、Dynamic Mediaクラシックで安全なテスト設定を作成する場合と同じです。

>[!NOTE]
>
>インストール環境がUNIX® 64ビットのオペレーティングシステムの場合は、設定する必要がある他の設定オプションについて、[https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)を参照してください。

#### 非公開状態でのアセットのプッシュに関する既知の制限  {#known-limitations-for-pushing-assets-in-unpublished-state}

この機能を使用する場合は、次の制限事項に注意してください。

* バージョン管理のサポートはありません。
* アセットが既にExperience Managerで発行されていて、後続のバージョンが作成されている場合、その新しいバージョンは、ライブから実稼動に直ちに発行されます。 アクティベーションに対する公開は、アセットの最初の公開でのみ動作します。

>[!NOTE]
>
>アセットを即座に公開する場合は、「**[!UICONTROL セキュアプレビューを有効にする]**」を「**[!UICONTROL すぐに]**」に設定したままにし、**[!UICONTROL 自動アップロードを有効にする]**&#x200B;機能を使用することをお勧めします。

### Dynamic Mediaクラシックにプッシュされたアセットの状態を非公開{#setting-the-state-of-assets-pushed-to-scene-as-unpublished}として設定

>[!NOTE]
>
>ユーザがExperience Managerでアセットを公開すると、S7アセットが本番用/ライブアセットに自動的にトリガーされます(アセットはセキュリティで保護されたプレビュー/非公開ではなくなります)。

Dynamic Mediaクラシックにプッシュされたアセットの状態を非公開に設定するには：

1. Experience Managerアイコンをタップし、**[!UICONTROL 導入/Cloud Services]**&#x200B;に移動し、**[!UICONTROL Dynamic Mediaクラシック]**&#x200B;をタップして、Dynamic Mediaクラシックで設定を選択します。
1. 「**[!UICONTROL 詳細]**」タブをタップします。**[!UICONTROL セキュア表示を有効にする]**&#x200B;ドロップダウンメニューで、**[!UICONTROL 「AEM公開アクティベーション]**&#x200B;上」を選択して、アセットを公開せずにDynamic Mediaクラシックにプッシュします。 (デフォルトでは、この値は&#x200B;**[!UICONTROL すぐに]**&#x200B;に設定されます。ここで、Dynamic Mediaクラシックアセットは直ちに公開されます)。

   アセットを公開する前のテストの詳細については、[Dynamic Mediaクラシックドキュメント](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)を参照してください。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 「**[!UICONTROL OK]**」をタップします。

セキュアプレビューを有効にすると、アセットが非公開のセキュアプレビューサーバーにプッシュされます。

セキュリティで保護されたプレビューが有効かどうかを確認するには、Experience ManagerのページでDynamic Mediaクラシックコンポーネントに移動します。 「**[!UICONTROL 編集]**」をタップします。アセットのURLに表示されるセキュリティで保護されたプレビューサーバがあります。 Experience Managerで公開した後、ファイル参照内のサーバードメインがプレビューURLから実稼動URLに更新されます。

### WCMのDynamic Mediaクラシックを有効にする{#enabling-scene-for-wcm}

WCMでのDynamic Mediaクラシックの有効化は、次の2つの理由で行う必要があります。

* これにより、ページオーサリング用のユニバーサルビデオプロファイルのドロップダウンリストが可能になります。 このリストがない場合、**[!UICONTROL ユニバーサルビデオプリセット]**&#x200B;ドロップダウンは空になり、設定できません。
* デジタルアセットがターゲットフォルダーにない場合は、ページのプロパティでそのページに対してDynamic Mediaクラシックを有効にすると、そのアセットをDynamic Mediaクラシックにアップロードできます。 次に、アセットをDynamic Mediaクラシックコンポーネントにドラッグ&amp;ドロップします。 通常の継承ルールが適用されます（子ページは親ページから設定を継承します）。

WCMに対してDynamic Mediaクラシックを有効にする場合、他の設定と同様、継承ルールが適用されます。 WCM用のDynamic Mediaクラシックは、タッチ操作向けまたは従来のユーザーインターフェイスで有効にできます。

#### タッチ操作向けユーザーインターフェイスでWCM用のDynamic Mediaクラシックを有効にする{#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

タッチ操作向けUIでWCMに対してDynamic Mediaクラシックを有効にするには：

1. Experience Managerアイコンをタップし、**[!UICONTROL サイト]**&#x200B;に移動してから、（言語固有ではなく）Webサイトのルートページに移動します。

1. ツールバーで、[!UICONTROL 設定]アイコンを選択し、**[!UICONTROL プロパティを開く]**&#x200B;をタップします。

1. 「**[!UICONTROL Cloud Services]**」をタップし、「**[!UICONTROL 追加設定]**」をタップして、「**[!UICONTROL Dynamic Mediaクラシック]**」を選択します。
1. **[!UICONTROL AdobeDynamic Mediaクラシック]**&#x200B;ドロップダウンリストで、目的の設定を選択し、「**[!UICONTROL OK]**」をタップします。

   ![chlimage_1-303](assets/chlimage_1-303.png)

   この設定のDynamic Mediaクラシックのビデオプリセットは、そのページと子ページのDynamic MediaクラシックビデオコンポーネントとのExperience Managerで使用できます。

#### クラシックユーザーインターフェイスでWCM用のDynamic Mediaクラシックを有効にする{#enabling-scene-for-wcm-in-the-classic-user-interface}

クラシックUIでWCMのDynamic Mediaクラシックを有効にするには：

1. Experience Managerで、「**[!UICONTROL Webサイト]**」をタップし、（言語固有ではなく）Webサイトのルートページに移動します。

1. サイドキックで、**[!UICONTROL ページ]**&#x200B;アイコンをタップし、**[!UICONTROL ページのプロパティ]**&#x200B;をタップします。

1. **[!UICONTROL Cloud Services/追加サービス/Dynamic Mediaクラシック]**&#x200B;をタップします。
1. **[!UICONTROL AdobeDynamic Mediaクラシック]**&#x200B;ドロップダウンリストで、目的の設定を選択し、「**[!UICONTROL OK]**」をタップします。

   この設定のDynamic Mediaクラシックのビデオプリセットは、そのページと子ページのDynamic MediaクラシックビデオコンポーネントとのExperience Managerで使用できます。

### デフォルト設定の設定 {#configuring-a-default-configuration}

複数のDynamic Mediaクラシック設定がある場合は、そのうち1つをDynamic Mediaクラシックコンテンツブラウザのデフォルトとして指定できます。

特定の時点で、デフォルトとしてマークできるDynamic Mediaクラシック設定は1つだけです。 デフォルト設定は、Dynamic Mediaクラシックコンテンツブラウザにデフォルトで表示される会社アセットです。

デフォルト設定を設定するには：

1. Experience Managerアイコンをタップし、**[!UICONTROL 導入/Cloud Services]**&#x200B;に移動し、**[!UICONTROL Dynamic Mediaクラシック]**&#x200B;をタップして、Dynamic Mediaクラシックで設定を選択します。
1. 設定を開くには、「**[!UICONTROL 編集]**」をタップします。

1. 「**[!UICONTROL 一般]**」タブで、「**[!UICONTROL デフォルトの設定]**」チェックボックスをオンにして、Dynamic Mediaクラシックコンテンツブラウザーに表示されるデフォルトの会社とルートパスにします。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >1 つの設定しかない場合、「**[!UICONTROL デフォルト設定]**」チェックボックスを選択しても、効果はありません。

### アドホックフォルダーの設定  {#configuring-the-ad-hoc-folder}

アセットがCQターゲットフォルダーにない場合に、アセットがDynamic Mediaクラシックでアップロードされるフォルダーを設定できます。 CQターゲットーフォルダー外からのアセットの公開を参照してください。

アドホックフォルダーを設定するには：

1. Experience Managerアイコンをタップし、**[!UICONTROL 導入/Cloud Services]**&#x200B;に移動し、**[!UICONTROL Dynamic Mediaクラシック]**&#x200B;をタップして、Dynamic Mediaクラシックで設定を選択します。
1. 設定を開くには、「**[!UICONTROL 編集]**」をタップします。

1. 「**[!UICONTROL 詳細]**」タブをタップします。「**[!UICONTROL アドホックフォルダー]**」フィールドで、**アドホック**&#x200B;フォルダーを変更できます。デフォルトでは、**name_of_the_company/CQ5_adhoc** です。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### ユニバーサルプリセットの設定 {#configuring-universal-presets}

ビデオコンポーネント用のユニバーサルプリセットを設定するには、[ビデオ](/help/assets/s7-video.md)を参照してください。

## MIMEタイプベースのアセットを有効にする/Dynamic Mediaクラシックアップロードジョブパラメーターのサポート{#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Digital Asset Manager/Dynamic Mediaクラシックアセットの同期によってトリガーされる、設定可能なDynamic Mediaクラシックアップロードジョブパラメーターを有効にできます。

特に、[Experience Manager] [Webコンソールの構成]パネルの[OSGi (Open Service Gateway initiative)]領域で、MIMEタイプによって受け入れられるファイル形式を構成します。 次に、JCR(Java™ Content Repository)の各MIMEタイプで使用される個々のアップロードジョブのパラメータをカスタマイズできます。

**MIME タイプベースのアセットを有効にするには：**

1. Experience Managerアイコンをタップし、**[!UICONTROL ツール/操作/Webコンソール]**&#x200B;に移動します。
1. Adobe Experience ManagerWebコンソールの設定パネルの&#x200B;**[!UICONTROL OSGi]**&#x200B;メニューで、**[!UICONTROL 設定]**&#x200B;をタップします。
1. 「名前」列で、**[!UICONTROL Adobe CQDynamic MediaクラシックアセットのMIMEタイプ「サービス]**」を探してタップし、設定を編集します。
1. 「MIMEタイプのマッピング」領域で、任意のプラス記号(+)をタップして、MIMEタイプを追加します。

   [サポートされているMIMEタイプ](/help/assets/assets-formats.md#supported-mime-types)を参照してください。

1. テキストフィールドに、新しいMIMEタイプ名を入力します。

   例えば、`EPS=application/postscript` OR `PSD=image/vnd.adobe.photoshop`のように`<file_extension>=<mime_type>`と入力します。

1. 設定ウィンドウの右下隅の「**[!UICONTROL 保存]**」をタップします。
1. Experience Managerに戻り、左側のレールでCRXDE Liteをタップします。
1. CRXDE Liteページの左側のナビゲーションバーの`/etc/cloudservices/scene7/<environment>`に移動します（実際の名前は`<environment>`に置き換えます）。
1. `<environment>`を展開（実際の名前は`<environment>`に置き換えます）すると、`mimeTypes`ノードが表示されます。
1. 先ほど追加したmimeTypeをタップします。

   例えば、`mimeTypes > application_postscript` OR `mimeTypes > image_vnd.adobe.photoshop`です。

1. CRXDE Lite ページの右側で、「**[!UICONTROL プロパティ]**」タブをタップします。
1. **[!UICONTROL jobParam]**&#x200B;の値フィールドに、Dynamic Mediaクラシックアップロードジョブパラメータを指定します。

   例：`psprocess="rasterize"&psresolution=120`

   使用できるアップロードジョブのパラメーターについて詳しくは、[AdobeDynamic MediaクラシックImage Production System API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html)を参照してください。

   >[!NOTE]
   >
   >PSDファイルをアップロードし、レイヤー抽出を使用してテンプレートとして処理する場合は、**[!UICONTROL jobParam]**&#x200B;の値フィールドに次の値を入力します。
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >PSDファイルに「レイヤー」が含まれていることを確認します。 厳密に1つの画像、またはマスクを含む画像の場合、処理するレイヤーがないので、画像として処理されます。

1. CRXDE Lite ページの左上隅の「**[!UICONTROL すべて保存]**」をタップします。

## Dynamic MediaクラシックとExperience Managerの統合のトラブルシューティング{#troubleshooting-scene-and-aem-integration}

Experience ManagerとDynamic Mediaクラシックの統合で問題が発生する場合は、次の解決策のシナリオを参照してください。

**Dynamic Mediaクラシックへのデジタルアセットの公開に失敗する場合：**

* アップロードするアセットが&#x200B;**[!UICONTROL CQターゲット]**&#x200B;フォルダー内にあることを確認します(このフォルダーは、Dynamic Mediaクラシッククラウド設定で指定します)。
* そうでない場合は、**[!UICONTROL CQ ad hoc]**&#x200B;フォルダーへのアップロードを許可するために、そのページの&#x200B;**[!UICONTROL ページプロパティ]**&#x200B;でクラウド設定を行う必要があります。

* ログの情報を確認します。

**ビデオプリセットが表示されない場合：**

* **[!UICONTROL ページのプロパティ]**&#x200B;で、そのページのクラウド設定が設定されていることを確認します。ビデオプリセットは、Dynamic Mediaクラシックビデオコンポーネントで使用できます。

**ビデオアセットがExperience Managerで再生されない場合：**

* 正しいビデオコンポーネントを使用していることを確認します。Dynamic Mediaクラシックビデオコンポーネントは、foundation Videoコンポーネントとは異なります。 [Foundation VideoコンポーネントとDynamic Mediaクラシックビデオコンポーネント](/help/assets/s7-video.md)を参照してください。

**Experience Manager内の新規または変更されたアセットがDynamic Mediaクラシックに自動的にアップロードされない場合：**

* アセットが CQ ターゲットフォルダーにあることを確認します。CQターゲットフォルダー内のアセットのみが自動的に更新されます(Experience Managerアセットを自動的にアップロードするように設定している場合)。
* Cloud Servicesの設定で「自動アップロードを有効にする」が設定されていること、およびDAM Assetワークフローが更新され、保存されていて、Dynamic Mediaクラシックのアップロードが含まれていることを確認してください。
* 画像をDynamic Mediaクラシックターゲットフォルダーのサブフォルダーにアップロードする場合は、次のいずれかの操作を行います。

   * 場所に関係なく、すべてのアセットの名前が一意であることを確認します。そうしないと、メインターゲットフォルダーのアセットが削除され、サブフォルダーのアセットだけが残ります。
   * Dynamic Mediaクラシックアカウントのセットアップ領域で、Dynamic Mediaクラシックがアセットを上書きする方法を変更します。 サブフォルダー内の同じ名前のアセットを使用する場合、場所に関係なく、アセットを上書きするようにDynamic Mediaクラシックを設定しないでください。

**削除したアセットまたはフォルダーが、Dynamic MediaクラシックとExperience Managerの間で同期されない場合：**

* Experience Managerアセットで削除されたアセットとフォルダは、Dynamic Mediaクラシックの同期フォルダに引き続き表示されます。 手動で削除します。

**ビデオのアップロードに失敗した場合**

* ビデオのアップロードに失敗し、Experience Managerを使用してDynamic Mediaクラシック統合を通じてビデオをエンコードする場合は、「[Dynamic Mediaクラシックアップロードワークフローへの設定可能なタイムアウトの追加](#adding-configurable-timeout-to-scene-upload-workflow)」を参照してください。

>[!CAUTION]
>
>既存のDynamic Mediaクラシック会社アカウントからアセットを読み込むと、Experience Managerで表示するのに時間がかかる場合があります。 アセット数が多すぎないDynamic Mediaクラシックのフォルダーを指定していることを確認してください。 例えば、ルートフォルダーに含まれるアセットが多すぎる場合があります。
>
>統合をテストする場合は、ルート会社ーがサブフォルダー全体ではなく、サブフォルダーのみを指すようにします。

