---
title: ' [!DNL Adobe Stock] アセットを管理'
description: ' [!DNL Adobe Experience Manager] 内から  [!DNL Adobe Stock]  アセットを、検索、取得、ライセンス、管理します。ライセンスされたアセットをその他のデジタルアセットとして使用します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 92%

---


# [!DNL Adobe Experience Manager Assets] での [!DNL Adobe Stock] アセットの使用 {#use-adobe-stock-assets-in-aem-assets}

[!DNL Adobe Stock] エンタープライズプランと [!DNL Experience Manager Assets] を統合すると、[!DNL Experience Manager] の強力なアセット管理機能を使用して、ライセンスが必要なアセットをクリエイティブプロジェクトやマーケティングプロジェクトに幅広く活用できます。

[!DNL Adobe Stock] サービスは、あらゆるクリエイティブプロジェクトに使用できる、適切にキュレーションされ、著作権使用料が不要で質の高い何百万点もの写真、ベクター、イラスト、ビデオ、テンプレートおよび 3D アセットを提供します。[!DNL Experience Manager] ユーザーは、[!DNL Experience Manager] に保存されている [!DNL Adobe Stock] アセットの検出、プレビューおよびライセンスの取得を、[!DNL Experience Manager] インターフェイスからすばやく実行できます。

## 前提条件 {#prerequisites}

統合には、[enterprise [!DNL Adobe Stock] プラン](https://stockenterprise.adobe.com/)が必要です。

## [!DNL Experience Manager] と [!DNL Adobe Stock] の統合 {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager] と [!DNL Adobe Stock] の間でやり取りができるようにするには、[!DNL Experience Manager] 内で IMS 設定と [!DNL Adobe Stock] 設定を作成します。

>[!NOTE]
>
>統合は、組織の [!DNL Experience Manager] 管理者と [!DNL Admin Console] 管理者のみ実行できます。統合の実行には管理者特権が必要です。

### IMS 設定の作成 {#create-an-ims-configuration}

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。「**[!UICONTROL 作成]**」をクリックし、**[!UICONTROL クラウドソリューション]**／**[!UICONTROL Adobe Stock]** を選択します。
1. 既存の証明書を再使用するか、「**[!UICONTROL 新しい証明書を作成]**」を選択します。
1. 「**[!UICONTROL 証明書を作成]**」をクリックします。証明書を作成したら、公開鍵をダウンロードします。「**[!UICONTROL 次へ]**」をクリックします。
1. ダウンロードした公開鍵を [!DNL Adobe Developer Console] サービスアカウントに追加します。「**[!UICONTROL 次へ]**」をクリックします。すぐに値を指定する場合は、[!UICONTROL Adobe IMS テクニカルアカウント設定]画面を開いたままにします。
1. [アドビ開発者コンソール](https://console.adobe.io)にアクセスします。自身のアカウントに、統合するために必要な、組織の管理者権限があることを確認します。
1. 「**[!UICONTROL 新しいプロジェクトを作成]**」をクリックし、「**[!UICONTROL API を追加]**」をクリックします。使用可能な API のリストから **[!UICONTROL Adobe Stock]** を選択します。「[!UICONTROL OAUTH 2.0 Web]」を選択します。表示される様々な値を設定およびコピーします。
1. [!DNL Experience Manager] で、「**[!UICONTROL タイトル]**」、「**[!UICONTROL 認証サーバー]**」、「**[!UICONTROL API キー]**」、「**[!UICONTROL クライアントの秘密鍵]**」および「**[!UICONTROL ペイロード]**」の各フィールドに適切な値を指定します。これらの値について詳しくは、[JWT 認証クイックスタート](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)を参照してください。

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### [!DNL Experience Manager] での [!DNL Adobe Stock] 設定の作成 {#create-adobe-stock-configuration-in-aem}

1. [!DNL Experience Manager] で、**[!UICONTROL ツール]**／**[!UICONTROL Cloud Services]**／**[!UICONTROL Adobe Stock]** に移動します。
1. 「**[!UICONTROL 作成]**」をクリックして設定を作成し、その設定を既存の IMS 設定に関連付けます。環境パラメーターとして「`PROD`」を選択します。
1. 「**[!UICONTROL ライセンスが必要なアセットのパス]**」フィールドの場所をそのまま残します。この場所を [!DNL Adobe Stock] アセットを保存する場所に変更しないでください。
1. すべての必須プロパティを追加して作成を完了します。「**[!UICONTROL 保存して閉じる]**」をクリックします。
1. アセットのライセンスを取得できる [!DNL Experience Manager] ユーザーまたはグループを追加します。

>[!NOTE]
>
>複数の [!DNL Adobe Stock] 設定がある場合は、ユーザ環境設定パネルで目的の設定を選択します。[!DNL Experience Manager]ホームページからパネルにアクセスするには、ユーザーアイコンをクリックし、**[!UICONTROL ユーザー環境設定]**/**[!UICONTROL Stock Configuration]**&#x200B;をクリックします。

## [!DNL Experience Manager] での [!DNL Adobe Stock] アセットの使用と管理 {#usemanage}

この機能を使用すると、[!DNL Experience Manager Assets] で [!DNL Adobe Stock] アセットを操作できます。[!DNL Experience Manager] のユーザーインターフェイス内から [!DNL Adobe Stock] アセットを検索し、必要なアセットのライセンスを取得できます。

[!DNL Experience Manager] 内で [!DNL Adobe Stock] アセットのライセンスを取得すると、そのアセットを通常のアセットと同様に使用および管理できます。ユーザーは [!DNL Experience Manager] 内でアセットの検索およびプレビュー、アセットのコピーおよび公開、[!DNL Brand Portal] でのアセットの共有、[!DNL Experience Manager] デスクトップアプリケーション経由でのアセットのアクセスおよび使用をおこなうことができます。

![ワークス [!DNL Adobe Stock] ペースからのアセットの検索と結果のフィルタリ [!DNL Adobe Experience Manager] ング](assets/adobe-stock-search-results-workspace.png)

*図：インターフェイスから [!DNL Adobe Stock] アセットを検索し、結果をフィルタリ [!DNL Experience Manager] ングします。*

**A.**[!DNL Adobe Stock] 指定された ID のアセットと類似しているアセットを検索します。**B.** 選択した形状や向きと一致するアセットを検索します。**C.** サポートされているアセットタイプのいずれかを検索します。**D.** フィルターウィンドウを開く／折りたたみます。**E.** 選択したアセットのライセンスを取得して に保存します。[!DNL Experience Manager]**F.**[!DNL Experience Manager] アセットを透かし付きで に保存します。**G.**[!DNL Adobe Stock] 選択したアセットと類似したアセットを Web サイトで調べます。**H.**[!DNL Adobe Stock] 選択したアセットを Web サイトに表示します。**I.** 検索結果から選択したアセットの数。**J.** カード表示とリスト表示を切り替えます。

### アセットの検索 {#find-assets}

[!DNL Experience Manager] ユーザーは、[!DNL Experience Manager] と [!DNL Adobe Stock] の両方でアセットを検索できます。検索場所を [!DNL Adobe Stock] に限定しない場合は、[!DNL Experience Manager] と [!DNL Adobe Stock] からの検索結果が表示されます。

* [!DNL Adobe Stock] アセットを検索するには、**[!UICONTROL ナビゲーション]**／**[!UICONTROL アセット]**／**[!UICONTROL Adobe Stock を検索]**&#x200B;をクリックします。

* [!DNL Adobe Stock] と [!DNL Experience Manager Assets] にまたがるアセットを検索するには、「![検索](assets/do-not-localize/search_icon.png)」をクリックします。

また、アセットを選択するには、検索バーに「`Location: Adobe Stock`」と入力します。[!DNL Adobe Stock][!DNL Experience Manager] は、検索されたアセットに対する高度なフィルタリング機能を備えており、サポートされているアセットのタイプや画像の向き、ライセンスの状態などのフィルターを使用して、必要なアセットをすばやく見つけることができます。

>[!NOTE]
>
>[!DNL Adobe Stock] から検索されたアセットは [!DNL Experience Manager] に表示されるだけです。[アセットを保存](/help/assets/aem-assets-adobe-stock.md#saveassets)するか、[アセットにライセンスを付与して保存](/help/assets/aem-assets-adobe-stock.md#licenseassets)した後でないと、[!DNL Adobe Stock] アセットを取得して [!DNL Experience Manager] リポジトリに保存することはできません。既に [!DNL Experience Manager] に保存されているアセットが表示され、参照やアクセスが簡単にできるようにハイライトされます。また、[!DNL Stock] アセットは、ソースが [!DNL Stock] であることを示すいくつかの追加メタデータとともに保存されます。

![検索結果での検索フィルター [!DNL Experience Manager] および強調表示 [!DNL Adobe Stock] されたアセット](assets/aem-search-filters2.jpg)

*図：[!DNL Experience Manager] の検索フィルターと、検索結果内でハイライトされている [!DNL Adobe Stock] アセット。*

### 必要なアセットの保存と表示 {#saveassets}

[!DNL Experience Manager] に保存するアセットを選択します。上部ツールバーの「[!UICONTROL 保存]」をクリックし、アセットの名前と保存場所を指定します。ライセンスが不要なアセットはローカルに透かし付きで保存されます。

アセットの検索を次回実行すると、保存済みのアセットは、[!DNL Experience Manager Assets] で使用可能であることを示すバッジ付きでハイライトされます。

>[!NOTE]
>
>最近追加されたアセットには、ライセンスが許諾されていることを示すバッジではなく、新しいアセットであることを示すバッジが表示されます。

### アセットのライセンス取得 {#licenseassets}

[!DNL Adobe Stock] エンタープライズプランの割り当てを使用することで、[!DNL Adobe Stock] アセットのライセンスを取得できます。ライセンスを許諾されたアセットは透かしなしで保存され、[!DNL Experience Manager Assets] で検索することも使用することも可能になります。

![ア [!DNL Adobe Stock] セットをライセンス認証して保存するダイアログ  [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)

*図：[!DNL Experience Manager Assets] で [!DNL Adobe Stock] アセットのライセンスを取得して保存するダイアログ。*

### メタデータおよびアセットプロパティへのアクセス {#access-metadata-and-asset-properties}

メタデータ（[!DNL Experience Manager] に保存されているアセットの [!DNL Adobe Stock] メタデータプロパティを含む）にアクセスしてプレビューし、アセットの&#x200B;**[!UICONTROL ライセンス参照]**&#x200B;を追加できます。ただし、ライセンス参照の更新は [!DNL Experience Manager] と [!DNL Adobe Stock] Web サイトの間で同期されません。

ユーザーは、ライセンスを許諾されたアセットとライセンスを許諾されていないアセットの両方を表示できます。

![保存されているアセットのメタデータとライセンス参照の表示、アクセス](assets/metadata_properties.jpg)

*図：保存されているアセットのメタデータとライセンス参照の表示、アクセス。*

## 既知の制限事項 {#known-limitations}

* **編集画像の警告が表示されない**：画像のライセンスを取得する場合、ユーザーは画像が「編集のみ使用」かどうか確認できません。管理者は誤用を防ぐために、Admin Console から編集用アセットへのアクセスをオフにできます。

* **間違ったライセンスの種類が表示される**：[!DNL Experience Manager] で、アセットに対して正しくないライセンスタイプが表示される可能性があります。[!DNL Adobe Stock] Web サイトにログインすると、ライセンスタイプを確認できます。

* **参照フィールドとメタデータが同期されない**：ユーザーがライセンス参照フィールドを更新すると、そのライセンス参照情報は [!DNL Experience Manager] で更新されますが、[!DNL Adobe Stock] Web サイト上では更新されません。同様に、[!DNL Adobe Stock] Web サイトで参照フィールドを更新すると、更新情報が [!DNL Experience Manager] には反映されません。

>[!MORELIKETHIS]
>
>* [アセットの [!DNL Adobe Stock] 使用に関するビデオチュートリアル [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [[!DNL Adobe Stock] エンタープライズプランヘルプ](https://helpx.adobe.com/jp/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] FAQ](https://helpx.adobe.com/jp/stock/faq.html)

