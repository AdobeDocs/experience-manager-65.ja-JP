---
title: e コマース統合フレームワーク
description: AEM e コマースは、マーケターが web、モバイル、ソーシャルの各タッチポイントにまたがって、ブランド化され、カスタマイズされたショッピングエクスペリエンスを提供するのに役立ちます。
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 100%

---

# e コマース {#ecommerce}

* [概念 ](/help/commerce/cif-classic/administering/concepts.md)
* [管理（汎用）](/help/commerce/cif-classic/administering/generic.md)

アドビでは、2 つのバージョンの Commerce 統合フレームワークを提供しています。

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF オンプレミス</p> </th>
   <th><p>CIF クラウド</p> </th>
  </tr>
  <tr>
   <td><p>サポートされている AEM バージョン</p> </td>
   <td><p>AEM オンプレミスまたは AMS 6.x</p> </td>
   <td>AEM AMS 6.4 と 6.5</td>
  </tr>
  <tr>
   <td><p>バックエンド</p> </td>
   <td>
    <ul>
     <li>AEM、Java</li>
     <li>モノリシック統合、ビルド前のマッピング（テンプレート）</li>
     <li>JCR リポジトリ</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java および JavaScript</li>
     <li>JCR リポジトリに格納されていないコマースデータ</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>フロントエンド</p> </td>
   <td><p>AEM サーバーサイドでレンダリングされたページ</p> </td>
   <td>混在型ページアプリケーション（ハイブリッドレンダリング）</td>
  </tr>
  <tr>
   <td><p>製品カタログ</p> </td>
   <td>
    <ul>
     <li>AEM の製品インポーター、エディター、キャッシュ</li>
     <li>AEM またはプロキシページを含む標準のカタログ</li>
    </ul> </td>
   <td>
    <ul>
     <li>製品の読み込みなし</li>
     <li>汎用テンプレート</li>
     <li>コネクター経由のオンデマンドデータ</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>スケーラビリティ</p> </td>
   <td>
    <ul>
     <li>最大で数百万の製品をサポートできます（ユースケースによって異なります）</li>
     <li>Dispatcher でのキャッシュ</li>
    </ul> </td>
   <td>
    <ul>
     <li>ボリューム制限なし</li>
     <li>Dispatcher または CDN でのキャッシュ</li>
    </ul> </td>
  </tr>
  <tr>
   <td>標準化されたデータモデル</td>
   <td>不可</td>
   <td>可、Adobe Commerce GraphQL スキーマ</td>
  </tr>
  <tr>
   <td>入手方法</td>
   <td><p>使用可能。SAP Commerce Cloud（拡張機能は AEM 6.4 および Hybris 5（デフォルト）をサポートするように更新され、Hybris 4 との互換性を維持）</p> <p>Salesforce Commerce Cloud（AEM 6.4 をサポートするためにオープンソース化されたコネクター）</p> </td>
   <td>GitHub を通じてオープンソースで使用可能。Adobe Commerce（2.3.2（デフォルト）をサポート、2.3.1 と互換性あり）</td>
  </tr>
  <tr>
   <td>用途</td>
   <td>限定的なユースケース：小規模で静的なカタログの読み込みが必要なシナリオなど</td>
   <td>大部分のユースケースで推奨されるソリューション</td>
  </tr>
 </tbody>
</table>

e コマースは、商品情報管理（PIM）と連動して、オンラインストアでの商品の販売に焦点を合わせた web サイトの以下のアクティビティを扱います。

* 商品の作成、ライフタイム、陳腐化
* 価格管理
* トランザクション管理
* カタログ全体の管理
* ライブおよび一元化されたストレージレコード
* web インターフェイス

AEM e コマースは、マーケターが web、モバイル、ソーシャルの各タッチポイントにまたがって、ブランド化され、カスタマイズされたショッピングエクスペリエンスを提供するのに役立ちます。AEM オーサリング環境を使用すると、対象となる訪問者のコンテキストやマーチャンダイジング戦略に基づいて、以下のようなページやコンポーネントをカスタマイズできます。

* 製品ページ
* 買い物かごのコンポーネント
* チェックアウトコンポーネント

これらを実装すると、商品情報にリアルタイムでアクセスできるようになります。リアルタイムでアクセスすることにより、以下を実現できます。

* 商品情報の整合性
* 価格
* 在庫管理インベントリ
* 買い物かごの状態のバリエーション

>[!NOTE]
>
>この統合フレームワークを外部 e コマースプロバイダーと連携して利用するには、まず必要なパッケージをインストールする必要があります。詳しくは、[e コマースのデプロイ](/help/commerce/cif-classic/deploying/ecommerce.md)を参照してください。
>
>e コマース機能の拡張について詳しくは、[e コマースの開発](/help/commerce/cif-classic/developing/ecommerce.md)を参照してください。

## 主な機能 {#main-features}

AEM e コマースの主な機能は次のとおりです。

* プロジェクトで実現できる機能を示す、以下のような様々な&#x200B;**標準 AEM コンポーネント**&#x200B;があります。

   * 商品の表示
   * 買い物かご
   * チェックアウト
   * 最近表示した製品
   * 割引券
   * その他

  ![Geometrixx コンポーネントの例](/help/sites-administering/assets/chlimage_1-130.png)

  >[!NOTE]
  >
  >AEM が提供するこの統合フレームワークを利用すると、特定の e コマースエンジンに依存しないコマース機能を実現する追加の AEM コンポーネントを作成することもできます。

* **検索** - 次のいずれかを使用します。

   * AEM 検索
   * e コマースシステムの検索
   * サードパーティの検索
   * またはこれらの組み合わせ

  ![検索の例](/help/sites-administering/assets/chlimage_1-131.png)

* フルブラウザーウィンドウやモバイルデバイスなど、**複数のチャネルにコンテンツを表示する** AEM 機能を使用します。これにより、訪問者が必要とする形式でコンテンツが提供されます。

  ![モバイルビューの例](/help/sites-administering/assets/chlimage_1-132.png)

* **[AEM e コマースフレームワーク](#the-framework)**&#x200B;に基づいて独自の統合実装を開発する機能。

  現在利用できる 2 つの実装は、どちらも同じベース、つまり一般的な API（フレームワーク）上に構築されています。統合に必要な機能を実装するだけで、新しい統合を実装することができます。すべての新しい実装はインターフェイスを使用する（したがって実装から独立している）ので、フロントエンドコンポーネントを使用できます。

* **買い物客のデータとアクティビティに基づく、エクスペリエンス主導のコマース**&#x200B;を開発できる見込みがあります。これにより、以下のような様々なシナリオを実現できます。

   * 例えば、合計注文金額が特定の金額を超えた場合に送料を下げることができます。
   * 別の例では、プロファイル データ（位置情報など）を使用した季節限定オファーを提供できる場合もあります。必要な場合は、その他の要因に応じて、再度これらのオファーをハイライト表示できます。

  以下の例では、買い物かごの中身が 75 ドル未満なので、ティーザーが 1 つ表示されています。

  ![クライアントコンテキストを含む買い物かご](/help/sites-administering/assets/chlimage_1-133.png)

  買い物かごの中身が 75 ドルを超えると、このティーザーは次のように変更されます。

  ![変更後のクライアントコンテキストを含む買い物かご](/help/sites-administering/assets/chlimage_1-134.png)

* また、次のようなその他の機能も含まれます。

   * 買い物かごの中身をセッションをまたいで保持
   * 詳細な注文履歴
   * カタログの迅速な更新

## フレームワーク {#the-framework}

フレームワークの詳細については、[概念](/help/commerce/cif-classic/administering/concepts.md)の節で説明しますが、以下でフレームワークの概要を簡単に説明しておきます。

### フレームワークとは {#what}

* この統合フレームワークは、API、機能を説明するための一連のコンポーネントおよび接続方法の例を示すいくつかの拡張機能を提供します。
* フレームワークは、プロジェクトの実装に必要な基本構造を提供します。
* このフレームワークは拡張可能です。
* このフレームワークには、そのまま使用できるデフォルトのサイトはありません。フレームワークを実際の仕様に適合させるには、ある程度の開発作業が必要です。

### 使用する理由 {#why}

* カスタマイズされた e コマースサイトを迅速に実現するために必要な基本メカニズムを提供します。
* 実際の e コマースサイトの開発に必要な柔軟性を提供します。
* ベストプラクティスを示します。
