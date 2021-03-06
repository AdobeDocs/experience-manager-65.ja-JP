---
title: ハードウェアのサイジングのガイドライン
seo-title: Hardware Sizing Guidelines
description: このサイジングのガイドラインでは、AEM プロジェクトのデプロイに必要なハードウェアリソースの概算値を示します。
seo-description: These sizing guidelines offer an approximation of the hardware resources required to deploy an AEM project.
uuid: 395f9869-17c4-4b9b-99f8-d35a44dd6256
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 8893306f-4bc0-48eb-8448-36d0214caddf
docset: aem65
exl-id: 5837ef4f-d4e0-49d7-a671-87d5547e0d98
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2816'
ht-degree: 98%

---

# ハードウェアのサイジングのガイドライン{#hardware-sizing-guidelines}

このサイジングのガイドラインでは、AEM プロジェクトのデプロイに必要なハードウェアリソースの概算値を示します。サイズの見積もりは、プロジェクトのアーキテクチャ、ソリューションの複雑さ、予想されるトラフィック、プロジェクトの要件に応じて異なります。このガイドを使用すると、具体的なソリューションに必要なハードウェアを特定したり、ハードウェア要件の上限と下限を見積もることができます。

基本的な考慮事項を以下に示します（以下の順序で考慮します）。

* **ネットワーク速度**

   * ネットワーク遅延
   * 利用可能な帯域幅

* **計算速度**

   * キャッシュ効率
   * 予想されるトラフィック
   * テンプレート、アプリケーション、コンポーネントの複雑さ
   * 同時に作業する作成者の数
   * 作成操作（簡易コンテンツ編集、MSM ロールアウトなど）の複雑度

* **I/O パフォーマンス**

   * ファイルまたはデータベースストレージのパフォーマンスと効率

* **ハードドライブ**

   * リポジトリサイズの 2 倍または 3 倍

* **メモリ**

   * Web サイトのサイズ（コンテンツオブジェクト、ページ、ユーザーの数）
   * 同時にアクティブなユーザー／セッションの数

## アーキテクチャ {#architecture}

通常の AEM 設定は、オーサー環境とパブリッシュ環境で構成されます。これらの環境は、基盤となるハードウェアのサイズおよびシステム設定に関して、それぞれ要件が異なります。両方の環境での詳細な考慮事項については、[オーサー環境](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations)と[パブリッシュ環境](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations)の各節で説明します。

通常のプロジェクト設定では、次のようないくつかの環境でプロジェクトのフェーズを分類します。

* **開発環境**
新しい機能の開発や重要な変更を行うために使用します。開発者ごとに開発環境（通常は個人のシステム上でのローカルインストール）を使用して作業することをお勧めします。

* **オーサーテスト環境**
変更を検証するために使用します。テスト環境の数は、プロジェクトの要件によって異なります（個別の QA 用、統合テスト用、ユーザー受け入れテスト用など）。

* **パブリッシュテスト環境**
主にソーシャルコラボレーションのユースケースをテストしたり、オーサーインスタンスと複数のパブリッシュインスタンス間のインタラクションをテストしたりするために使用します。

* **オーサー実稼動環境**
作成者がコンテンツを編集するために使用します。

* **パブリッシュ実稼動環境**
公開済みコンテンツを提供するために使用します。

また、環境は、AEM とアプリケーションサーバーを実行する単一サーバーシステムから、複数のサーバー、複数の CPU で構成される拡張性の高いクラスターインスタンスに至るまで、多岐にわたります。実稼動システムごとに個別のコンピューターを使用し、これらのコンピューターではその他のアプリケーションを実行しないことをお勧めします。

## ハードウェアサイジングに関する一般的なガイドライン {#generic-hardware-sizing-considerations}

この節では、様々な点を考慮しながら、ハードウェア要件を計算する方法について説明します。大規模なシステムの場合、参照構成でシンプルな一連の社内ベンチマークテストを実行することをお勧めします。

特定のプロジェクトに対してベンチマークテストを行う場合は、基本的な作業として、まずパフォーマンスの最適化を実行します。[パフォーマンスの最適化に関するドキュメント](/help/sites-deploying/configuring-performance.md)に記載されている内容を適用してから、ベンチマークテストを実行して、ハードウェアサイジングの計算結果を使用してください。

高度なユースケースの場合、ハードウェアサイジングの要件は、プロジェクトのパフォーマンスを詳細に評価したうえで計算する必要があります。膨大なハードウェアリソースを必要とする高度なユースケースの特徴を次に示します。

* コンテンツのペイロードが大きく、スループットが高い
* カスタマイズされたコード、カスタムワークフロー、サードパーティのソフトウェアライブラリの広範な使用
* サポートされていない外部システムとの統合

### ディスク容量/ハードドライブ {#disk-space-hard-drive}

必要なディスク容量は、主に Web アプリケーションのボリュームとタイプによって決まります。計算では次の項目を考慮する必要があります。

* ページ、アセットおよびリポジトリに保存されているその他のエンティティ（ワークフロー、プロファイルなど）のサイズと量
* 推定されるコンテンツの変更頻度、つまりコンテンツバージョンが作成される頻度
* 生成される DAM アセットレンディションのボリューム
* コンテンツ全体の経時的増大

オンライン、オフラインおよびリビジョンのクリーンアップ中は、ディスク容量が継続的に監視されます。使用可能なディスク容量が臨界値を下回ると、プロセスがキャンセルされます。臨界値はリポジトリの現在のディスクフットプリントの 25 ％で、設定はできません。ディスクのサイズは、予想されるリポジトリの増加分を含めたリポジトリサイズの 2 倍または 3 倍にすることをお勧めします。

データの冗長性を確保するために、独立したディスク（RAID、例えば RAID10）の冗長配列を設定することを検討してください。

>[!NOTE]
>
>実稼働用インスタンスの一時ディレクトリでは、利用可能な容量を 6 GB 以上確保する必要があります。

#### 仮想化 {#virtualization}

AEM は仮想環境でも動作しますが、CPU や I/O などの要素については、物理ハードウェアと純粋に同等と見なすことはできません。ほとんどの場合、I/O 速度は非常に重要です。したがって、通常は、より高速な I/O を選択することをお勧めします。必要なリソースを正確に把握するには、環境のベンチマークテストをおこなう必要があります。

#### AEM インスタンスの並列化 {#parallelization-of-aem-instances}

**フェイルセーフ**

フェールセーフ web サイトは、少なくとも 2 つの別々のシステムにデプロイします。1 つのシステムが故障しても、別のシステムが引き継ぐため、システム障害を補うことができます。

**システムリソースのスケーラビリティ**

すべてのシステムを実行しながらでも、コンピューターのパフォーマンスを向上することができます。このパフォーマンスは、必ずしもクラスターノード数に比例して直線的に向上するわけではなく、技術環境に大きく依存します。詳しくは、[クラスターに関するドキュメント](/help/sites-deploying/recommended-deploys.md)を参照してください。

必要なクラスターノードの推定数は、特定の Web プロジェクトの基本要件および特定のユースケースによって決まります。

* フェイルセーフの観点では、すべての環境において、障害の重大度を特定し、クラスターノードのリカバリー所要時間に基づいて障害補償時間を決定する必要があります。
* スケーラビリティの面から考えると、基本的には書き込み操作数が最も重要です。オーサー環境の場合は[同時に操作している作成者](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel)を、パブリッシュ環境の場合は[ソーシャルコラボレーション](/help/managing/hardware-sizing-guidelines.md#socialcollaborationspecificconsiderations)を参照してください。読み取り操作のみを行うためにシステムにアクセスする場合は、操作を負荷分散することができます。詳しくは、[Dispatcher](https://helpx.adobe.com/jp/experience-manager/brand-portal/user-guide.html) を参照してください。

## オーサー環境用の計算 {#author-environment-specific-calculations}

ベンチマーキングを目的として、Adobe はスタンドアロンのオーサーインスタンス用にいくつかのベンチマークテストを開発しました。

* **ベンチマークテスト 1**
同じような性質を持つ既存の 300 ページを負荷のベースにして、ユーザーが単純なページ作成を行った場合の負荷プロファイルの最大スループットを計算します。実行した手順は、サイトへのログイン、SWF と画像／テキストを使用したページの作成、タグクラウドの追加、ページのアクティベーションです。

   * **結果**
前述のような単純なページ作成作業を 1 個のトランザクションと見なした場合、最大スループット（1 時間あたりのトランザクション数）は 1730 となりました。

* **ベンチマークテスト 2**
新規ページの作成（10 ％）、既存ページの変更（80 ％）、およびページの作成と変更の連続操作（10 ％）の混合を負荷プロファイルとして、その最大スループットを計算します。ページの複雑度はベンチマークテスト 1 のプロファイルの場合と同じです。ページの基本的な変更として、画像を追加し、テキストコンテンツを変更します。この場合も、ベンチマークテスト 1 に定義されたものと同じ複雑度を持つ 300 個のページを基本負荷として、作業をおこないました。

   * **結果**
このような混合操作シナリオの最大スループット（1 時間あたりのトランザクション数）は 3252 となりました。

>[!NOTE]
>
>スループット率から、負荷プロファイル内のトランザクションタイプを区別することはできません。スループットの測定に使用されたアプローチでは、各タイプのトランザクションが固定の比率でワークロードに組み込まれています。

前述の 2 つのテストから、操作のタイプに応じてスループットが変化することは明らかです。システムのサイジングをおこなう際には、環境におけるアクティビティを基準として使用します。（よく見られる）変更などの集中的な操作が減るほど、スループットが向上します。

### キャッシュ {#caching}

オーサー環境では、通常、キャッシングの効率が大幅に低下します。これは、web サイトでは変更が頻繁に行われ、またコンテンツが高度にインタラクティブでパーソナライズされているからです。Dispatcher を使用すると、AEM ライブラリ、JavaScript、CSS ファイル、およびレイアウト画像をキャッシュできます。これにより、作成プロセスの一部の側面が高速化されます。こうしたリソースのブラウザーキャッシングのヘッダーを追加で設定するように Web サーバーを設定すると、HTTP リクエストの数が減り、オーサーの場合と同様にシステムの応答性が向上します。

### 同時操作している作成者 {#authors-working-in-parallel}

オーサー環境で主な制限要因となっているのは、同時操作している作成者の数と、システムに対する作成者の操作の負荷です。したがって、データの共有スループットに基づいてシステムのスケーリングをおこなうことをお勧めします。

このようなシナリオを対象として、Adobe は、オーサーインスタンスからなる 2 つのノードのシェアードナッシングクラスターでベンチマークテストを実行しました。

* **ベンチマークテスト 1a** 
2 つのオーサーインスタンスからなるアクティブ-アクティブ構成のシェアードナッシングクラスターで、すべて類似の性質を持つ 300 個の既存ページを基本負荷として、ユーザーが単純なページ作成作業を行うという負荷プロファイルの最大スループットを計算します。

   * **結果**
前述のような単純なページ作成作業を 1 件のトランザクションと見なした場合、最大スループット（1 時間あたりのトランザクション数）は 2016 となりました。スタンドアロンのオーサーインスタンスに対して同じベンチマークテストを実行した場合と比較して、約 16 ％増加しています。

* **ベンチマークテスト 2b** 
2 つのオーサーインスタンスからなるアクティブ-アクティブ構成のシェアードナッシングクラスターで、負荷プロファイルに新規ページの作成（10 ％）、既存ページの変更（80 ％）、およびページの作成と変更の連続操作（10 ％）が混在する際の最大スループットを計算します。ページの複雑度はベンチマークテスト 1 のプロファイルの場合と同じです。ページの基本的な変更として、画像を追加し、テキストコンテンツを変更します。この場合も、ベンチマークテスト 1 に定義されたものと同じ複雑度を持つ 300 個のページを基本負荷として、作業をおこないました。

   * **結果**
このような混合操作シナリオの最大スループット（1 時間あたりのトランザクション数）は 6288 となりました。スタンドアロンのオーサーインスタンスに対して同じベンチマークテストを実行した場合と比較して、約 93 ％増加しています。

>[!NOTE]
>
>スループット率から、負荷プロファイル内のトランザクションタイプを区別することはできません。スループットの測定に使用されたアプローチでは、各タイプのトランザクションが固定の比率でワークロードに組み込まれています。

前述の 2 つのテストから、AEM で基本的な編集操作をおこなう作成者にとってスケーリングが適切に機能していることは明らかです。一般に、AEM は読み取り操作のスケーリングをおこなうのに最も効果的です。

標準的な Web サイトでは、ほとんどの作成操作がプロジェクトフェーズで行われます。Web サイトを実稼動に移行した後は、同時操作している作成者の数は、通常、（運用モードの）平均値に下がります。

オーサー環境に必要なコンピューター（CPU）の台数は次のように計算できます。

`n = numberOfParallelAuthors / 30`

この式は、作成者が AEM で基本的な操作を実行する場合の CPU スケーリングのガイドラインとして使用できます。システムおよびアプリケーションが最適化されていることが前提となります。ただし、この式は、MSM やアセットなどの高度な機能には当てはまりません（下記の節を参照）。

[並列化](/help/managing/hardware-sizing-guidelines.md#parallelization-of-aem-instances)および[パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)の追加コメントも参照してください。

### ハードウェアに関する推奨事項 {#hardware-recommendations}

通常、オーサー環境では、パブリッシュ環境に推奨されているものと同じハードウェアを使用できます。一般的に、Web サイトのトラフィックは作成システムでは大幅に少なくなっていますが、キャッシュの効率も低下します。ただし、ここで基本的な要因となるのは、同時操作している作成者の数と、システムに対するアクションの種類です。一般に、（オーサー環境の）AEM クラスタリングは読み取り操作のスケーリングを行うのに最も効果的です。言い換えると、AEM クラスターのスケーリングは、基本的な編集操作を行う作成者にとって適切に機能します。

アドビでのベンチマークテストは、以下で構成される Hewlett-Packard ProLiant DL380 G5 ハードウェアプラットフォームで実行されている RedHat 5.5 オペレーティングシステムを使用して行われました。

* 2 基のクアッドコア Intel Xeon X5450 CPU、3.00 GHz
* 8 GB RAM
* Broadcom NetXtreme II BCM5708 ギガビットイーサネット
* HP Smart Array RAID コントローラー、256 MB キャッシュ
* 2 個の 146 GB 10,000 RPM SAS ディスク（RAID0 ストライプセットとして構成）
* SPEC CINT2006 Rate ベンチマークスコア 110

AEM インスタンス実行時の最小ヒープサイズおよび最大ヒープサイズはそれぞれ 256M および 1024M です。

## パブリッシュ環境用の計算 {#publish-environment-specific-calculations}

### キャッシュ効率とトラフィック {#caching-efficiency-and-traffic}

キャッシュ効率は Web サイトの速度を検討するにあたって欠かせない要素です。最適化された AEM システムで、ディスパッチャーなどのリバースプロキシを使用して処理できる 1 秒間あたりのページ数について、次の表に示します。

| キャッシュ率 | ページ/秒（ピーク） | 1 日あたり 100 万ページ（平均） |
|---|---|---|
| 100％ | 1000 ～ 2000 | 35 ～ 70 |
| 99％ | 910 | 32 |
| 95％ | 690 | 25 |
| 90％ | 520 | 18 |
| 60% | 220 | 8 |
| 0% | 100 | 3.5 |

>[!CAUTION]
>
>免責事項：この数値はデフォルトのハードウェア構成に基づいており、使用される個々のハードウェアによって異なる可能性があります。

キャッシュ率とは、ディスパッチャーが AEM にアクセスしなくても返すことができるページの割合です。100 ％は、ディスパッチャーがすべての要求に応答することを表します。0 ％は、AEM がすべてのページの処理をおこなうことを示します。

### テンプレートとアプリケーションの複雑度 {#complexity-of-templates-and-applications}

複雑なテンプレートを使用している場合、AEM でページのレンダリングにかかる時間が増加します。キャッシュから取得されたページでは、このような影響はありません。ただし、全体の応答時間を考慮した場合、ページサイズはパフォーマンスに関係します。複雑なページのレンダリングでは、単純なページのレンダリングと比較して 10 倍の時間がかかることもあります。

### 数式 {#formula}

次の式を使用して、AEM ソリューションの全体的な複雑さを計算で推定できます。

`complexity = applicationComplexity + ((1-cacheRatio) * templateComplexity)`

この複雑さに基づいて、パブリッシュ環境で必要となるサーバー数（または CPU コア数）を次のように求めることができます。

`n = (traffic * complexity / 1000 ) * activations`

この方程式の変数は、次のとおりです。

<table>
 <tbody>
  <tr>
   <td>トラフィック</td>
   <td>予想される 1 秒あたりのピークトラフィック。この数値は、1 日あたりのページヒット数を 35,000 で除算することで推定できます。</td>
  </tr>
  <tr>
   <td>applicationComplexity</td>
   <td><p>単純なアプリケーションを 1、複雑なアプリケーションを 2 として、1 ～ 2 の値を使用します。</p>
    <ul>
     <li>1 - 完全に匿名のコンテンツ指向のサイト</li>
     <li>1.1 - 完全に匿名のコンテンツ指向のサイト。クライアントサイド／ターゲットのパーソナライズゼーションに対応。</li>
     <li>1.5 - 匿名セクションとログインセクションの両方で構成される、コンテンツ指向のサイト。クライアントサイド／ターゲットのパーソナライゼーションに対応。</li>
     <li>1.7 - 匿名セクションとログインセクションの両方で構成される、コンテンツ指向のサイト。クライアントサイド／ターゲットのパーソナライゼーションに対応。一部でユーザー生成コンテンツを使用。</li>
     <li>2 - サイト全体でログインが必要。ユーザー生成コンテンツを幅広く使用。多様なパーソナライゼーション手法を採用。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>cacheRatio</td>
   <td>Dispatcher キャッシュから取得されるページの割合。 すべてのページがキャッシュから取得される場合は 1 を、すべてのページが常に AEM で処理される場合は 0 を使用します。</td>
  </tr>
  <tr>
   <td>templateComplexity</td>
   <td>1 ～ 10 の値でテンプレートの複雑度を指定します。数値が大きいほど、テンプレートが複雑になります。1 ページあたりの平均コンポーネント数が 10 個のサイトには値 1 を使用し、平均コンポーネント数が 40 個のサイトには値 5 を使用し、平均コンポーネント数が 100 個を超えるサイトには値 10 を使用します。</td>
  </tr>
  <tr>
   <td>activations</td>
   <td>1 時間あたりの平均アクティベート数（平均サイズのページおよびアセットのオーサー層からパブリッシュ層へのレプリケーション）を x で除算した数。x は、システムが処理する他のタスクのパフォーマンスに影響しない状態で、システムで実行されるアクティベート数を表します。x = 100 のように、悲観的な初期値をあらかじめ定義しておくこともできます。<br /> </td>
  </tr>
 </tbody>
</table>

複雑な Web サイトの場合は、AEM が受け入れ可能な時間内で要求に応答できるように、より性能の高い Web サーバーが必要となります。

* 4 未満の複雑さ：・ 1024 MB JVM RAM&#42;
・低～中程度のパフォーマンスの CPU

* 複雑度 4 ～ 8:・ 2048 MB JVM RAM&#42;
・中～高性能 CPU

* 複雑さが 8 を超える：・ 4096 MB JVM RAM&#42;
・ハイエンドからハイエンドの CPU

>[!NOTE]
>
>&#42; JVM に必要なメモリに加えて、オペレーティングシステムに十分な RAM を確保します。

## その他のユースケース用の計算 {#additional-use-case-specific-calculations}

デフォルト Web アプリケーション用の計算に加え、次のユースケースに固有の要因を検討する必要がある場合があります。計算後の値は、デフォルトの計算結果に加算されます。

### アセットに関する考慮事項 {#assets-specific-considerations}

デジタルアセットを大規模に処理するには、最適化されたハードウェアリソースが必要になります。最も関連する要因は、画像サイズと、処理された画像のピーク時のスループットです。

16 GB 以上のヒープを割り当て、[Camera Raw パッケージ](/help/assets/camera-raw.md)を使用して Raw 画像を取り込むように、[!UICONTROL DAM アセット更新]ワークフローを設定します。

>[!NOTE]
>
>画像のスループットが高くなった場合、システム I/O に遅れずに対応するための計算リソースが必要になります（その逆も言えます）。例えば、画像のインポートによってワークフローが開始された場合、多数の画像を WebDAV 経由でアップロードすると、ワークフローのバックログが発生する可能性があります。
>
>TarPM、データストアおよび検索インデックスに個別のディスクを使用することで、システム I/O 動作を最適化できます（ただし、検索インデックスは、通常、ローカルに格納しておくことで意味をなします）。

>[!NOTE]
>
>[アセットパフォーマンスガイド](/help/sites-deploying/assets-performance-sizing.md)も参照してください。

### Multi Site Manager {#multi-site-manager}

作成環境で AEM MSM を使用する場合のリソースの消費量は、ユースケースによって大きく異なります。基本的な要因は次のとおりです。

* ライブコピーの数
* ロールアウトの頻度
* ロールアウトするコンテンツツリーのサイズ
* ロールアウトアクションの連携機能

計画したユースケースをテストする際に代表的なコンテンツを引用すると、リソース消費量をより的確に把握できます。スループット計画から結果を推定することで、AEM MSM で別途必要になるリソースを評価できます。

さらに考慮すべき点として、AEM MSM のユースケースで予定よりも多くのリソースが消費されると、同時に作業する作成者はパフォーマンスの低下を感じるようになります。

### AEM Communities のサイジングの考慮事項 {#aem-communities-sizing-considerations}

AEM Communities の機能を含む AEM Sites （コミュニティサイト）には、パブリッシュ環境のサイト訪問者（メンバー）から高レベルのインタラクションがあります。

コミュニティサイトのサイジングで何を考慮するかは、コミュニティメンバーによる予測されるインタラクションと、ページコンテンツの最適なパフォーマンスの重要度が高いかどうかによって異なります。

メンバーによって送信されたユーザー生成コンテンツ（UGC）は、ページコンテンツとは分けて保存されます。AEM プラットフォームではオーサー環境からパブリッシュ環境にサイトコンテンツをレプリケートするノードストアを使用し、AEM Communities では UGC のために単一の共通ストアを使用します。UGC はレプリケートされません。

UGC ストアの場合は、選択したデプロイメントに影響を及ぼすストレージリソースプロバイダー（SRP）を選択する必要があります。
参照先

* [コミュニティコンテンツのストレージ](/help/communities/working-with-srp.md)
* [Communities 用の推奨トポロジ](/help/communities/topologies.md)
