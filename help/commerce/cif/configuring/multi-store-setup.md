---
title: コマースマルチストアの設定
description: 複数のストア表示を Adobe Commerce から AEM にマッピングする方法を説明します。これにより、マルチテナントおよび多言語のユースケースをプロジェクトでサポートできます。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 1d4e9b7b-848b-4007-b884-dd48682d62e8
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 100%

---

# コマースマルチストアの設定 {#multi-store}

AEM CIF コアコンポーネントは複数の AEM サイト構造で使用でき、基盤となる GraphQL クライアントの実装は異なる Adobe Commerce ストア／ストア表示に接続できます。これにより、複雑なマルチストア／マルチサイトの設定をプロジェクトに実装できます。

複数の Adobe Commerce ストア表示を Adobe Experience Manager Sites と統合するためのオプションについて詳しく説明するビデオチュートリアルです。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

地域とロケールをまたいでサイトをグローバルに管理するために、AEM マルチサイト管理のライブコピー機能および言語コピー機能を Commerce Integration Framework と組み合わせて使用できます。

推奨される設定は、AEM サイトと Adobe Commerce ストア表示の間に 1 対 1 の関係を使用することです。

AEM サイトと AEM CIF コアコンポーネントを専用のストア表示に接続するには、次の手順に従います。

## 設定 {#configuration}

1. [Adobe Commerce の web サイト、ストア、表示](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)に記載されているパターンに従って、複数のストアや表示を設定します。

2. AEM と Adobe Commerce 間の接続が動作していることを確認します。

3. 次の手順に従って、CIF Cloud Service 設定の子設定を作成します。

   * AEM で、ツール／一般／[設定ブラウザー](/help/sites-administering/configurations.md#using-configuration-browser)に移動します。
   * 作成したベース設定を選択します。
   * 上記のポイント 2 で説明した手順を使用して、新しい設定を作成します。

   この新しい設定は、基本設定の子設定として作成されます。ツール／一般／設定ブラウザーに移動して、設定を作成できるようになっています。

   >[!TIP]
   >
   > コマースカタログは、ID または UID を使用して対処できます。UID は Adobe Commerce 2.4.2 で導入されました。コマースバックエンドでバージョン 2.4.2 以降の GraphQL スキーマがサポートされている場合のみ、これを有効にしてください。

4. AEM Sites に子設定を割り当てます。

   * AEM Sites コンソールに移動します。
   * サイト構造の地域または言語ルート（Venia サンプルページの場合は /content/venia/us _または_ /content/venia/us/en）に移動します。
   * ページを選択し、ページのプロパティを開きます。
   * 「詳細」タブを選択します。
   * `Configuration` セクションで、手順で作成した設定を選択します。

## その他のリソース

* [Adobe Commerce の web サイト、ストア、表示](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF コアコンポーネント - マルチストア／サイト設定](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [マルチサイトマネージャの使用](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html?lang=ja)
* [コンテンツの再利用：マルチサイトマネージャとライブコピー](/help/sites-administering/msm.md)
