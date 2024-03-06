---
title: ヘッドレスアプリケーションの運用開始方法
description: AEM ヘッドレスデベロッパージャーニーのこの部分では、ヘッドレスアプリケーションを実稼働環境にデプロイする方法について説明します。
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 98%

---

# ヘッドレスアプリケーションの運用開始方法 {#go-live}

[AEM ヘッドレスデベロッパージャーニー](overview.md)のこの部分では、ヘッドレスアプリケーションを実稼働環境にデプロイする方法を説明します。

## これまでの説明内容 {#story-so-far}

AEM ヘッドレスジャーニーの前のドキュメント [AEM Assets API を使用してコンテンツを更新する方法](update-your-content.md)では、API を使用して AEM の既存のヘッドレスコンテンツを更新する方法を説明し、以下を達成できました。

* AEM Assets HTTP API を理解する

この記事は、これらの基本事項に基づいているので、独自の AEM ヘッドレスプロジェクトの運用開始準備をする方法を理解できます。

## 目的 {#objective}

このドキュメントは、AEM ヘッドレス公開パイプラインと、アプリケーションの運用を開始する前に認識しておく必要があるパフォーマンスに関する考慮事項を理解するうえで役に立ちます。

* AEM SDK と必要な開発ツールの把握
* 運用開始前にコンテンツをシミュレートするためのローカル開発ランタイムのセットアップ
* AEM のコンテンツのレプリケーションとキャッシュに関する基本事項の理解
* ローンチ前のアプリケーションのセキュリティ確保とスケーリング
* パフォーマンスとデバッグの問題の監視

## AEM SDK {#the-aem-sdk}

AEM SDK は、カスタムコードのビルドとデプロイに使用されます。ヘッドレスアプリケーションを開発し運用開始前にテストするために主に使用するツールです。次のアーティファクトで構成されます。

* クイックスタート JAR - オーサーインスタンスとパブリッシュインスタンスの両方をセットアップするために使用できる実行可能な JAR ファイル
* Dispatcher ツール - Windows および UNIX ベースシステム用の Dispatcher モジュールとその依存関係
* Java™ API JAR - AEM に対応した開発に使用できる、許可されたすべての Java™ API を公開する Java™ JAR／Maven 依存関係
* Javadoc JAR - Java™ API JAR の Javadoc

## その他の開発ツール {#additional-development-tools}

AEM SDK に加えて、コードとコンテンツのローカル開発およびテストを容易にする下記の追加ツールが必要です。

* Java™
* Git
* Apache Maven
* Node.js ライブラリ
* 任意の IDE

AEM は Java™ アプリケーションなので、AEM as a Cloud Service の開発をサポートするには、Java™ および Java™ SDK をインストールする必要があります。

Git は、ソースコントロールの管理、Cloud Manager への変更内容のチェックイン、さらにそれらを実稼動インスタンスにデプロイするために使用します。

AEM Maven プロジェクトアーキタイプから生成されたプロジェクトをビルドするために、AEM では Apache Maven を使用します。主要な IDE はすべて Maven との統合をサポートしています。

Node.js は、AEM プロジェクトの `ui.frontend` サブプロジェクトのフロントエンドアセットを操作するために使用される JavaScript ランタイム環境です。Node.js は npm と一緒に配布され、JavaScript の依存関係の管理に使用される事実上の Node.js パッケージマネージャーとなっています。

## AEM システムのコンポーネントの概要 {#components-of-an-aem-system-at-a-glance}

 次に、AEM 環境の構成要素を見てみましょう。

完全な AEM 環境は、オーサー、パブリッシュ、Dispatcher で構成されます。運用開始前にコードおよびコンテンツをプレビューしやすくするために、これらと同じコンポーネントがローカル開発ランタイムで使用可能です。

* **オーサーサービス**&#x200B;では、内部ユーザーがコンテンツの作成、管理およびプレビューを行います。

* **パブリッシュサービス**&#x200B;は「実稼働」環境と考えられ、通常はエンドユーザーがやり取りする場所になります。コンテンツは、オーサーサービスで編集および承認された後、パブリッシュサービスに配信（レプリケート）されます。AEM ヘッドレスアプリケーションで最も一般的なデプロイメントパターンは、実稼動版のアプリケーションを AEM パブリッシュサービスに接続させることです。

* **Dispatcher** は、AEM Dispatcher モジュールで拡張された静的 web サーバーです。パブリッシュインスタンスで生成された Web ページをキャッシュしてパフォーマンスを向上します。

## ローカル開発ワークフロー {#the-local-development-workflow}

ローカル開発プロジェクトは Apache Maven をベースに構築され、ソース管理に Git を使用します。プロジェクトを更新するために、開発者は、Eclipse、Visual Studio Code、IntelliJ など、好みの統合開発環境を使用できます。

ヘッドレスアプリケーションによって取り込まれるコードまたはコンテンツのアップデートをテストするには、アップデートをローカルの AEM ランタイムにデプロイします。これには、AEM オーサーサービスおよびパブリッシュサービスのローカルインスタンスが含まれます。

アップデートが最も重要な場所でアップデートをテストすることが大切なので、ローカル AEM ランタイムの各コンポーネントの違いに注意してください。例えば、オーサーインスタンスでコンテンツのアップデートをテストしたり、パブリッシュインスタンスで新しいコードをテストしたりします。

実稼動システムでは、Dispatcher と HTTP Apache サーバーは常に AEM パブリッシュインスタンスの前に配置されます。これらは AEM システムのキャッシュサービスとセキュリティサービスを提供するので、Dispatcher に対してもコードとコンテンツのアップデートをテストすることが最も重要です。

## ローカル開発環境でのコードとコンテンツのローカルプレビュー {#previewing-your-code-and-content-locally-with-the-local-development-environment}

AEM ヘッドレスプロジェクトのローンチの準備をするには、プロジェクトの構成要素がすべて正常に機能していることを確認する必要があります。

それには、コード、コンテンツおよび設定をすべて 1 つにまとめ、ローカル開発環境でテストして運用開始準備を行う必要があります。

ローカル開発環境は、次の 3 つの主な領域で構成されます。

1. AEM プロジェクト - AEM 開発者の作業対象となるすべてのカスタムコード、設定およびコンテンツを含みます
1. ローカル AEM ランタイム - AEM プロジェクトからコードをデプロイする際に使用される、AEM オーサーサービスおよびパブリッシュサービスのローカルバージョン
1. ローカル Dispatcher ランタイム - Dispatcher モジュールを含んだ Apache httpd Web サーバーのローカルバージョン。

ローカル開発環境をセットアップしたら、静的な Node サーバーをローカルにデプロイすることで、React アプリに対するコンテンツ提供をシミュレートできます。

ローカル開発環境のセットアップと、コンテンツのプレビューに必要なすべての依存関係について詳しくは、[実稼動デプロイメントのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html)を参照してください。

## AEM ヘッドレスアプリケーションの運用開始準備 {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

次に、以下に説明するベストプラクティスに従って、AEMヘッドレスアプリケーションを起動できるように準備します。

### ローンチ前にヘッドレスアプリケーションのセキュリティを確保 {#secure-and-scale-before-launch}

1. GraphQL リクエストの[認証](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md)を準備

### モデル構造と GraphQL 出力 {#structure-vs-output}

* 15 KB を超える JSON コード（gzip で圧縮）を出力するクエリを作成しないようにします。長い JSON ファイルの場合、クライアントアプリケーションで解析する際に大量のリソースを消費します。
* フラグメント階層のネストレベルは 5 以内にします。レベルを増やすと、コンテンツ作成者は変更の影響を考慮しにくくなります。
* モデル内の依存関係階層を使用したクエリをモデル化するのではなく、複数オブジェクトクエリを使用します。これにより、多くのコンテンツ変更を行うことなく、JSON 出力の再構築をより長期的に柔軟に行うことができます。

### CDN キャッシュヒット率の最大化 {#maximize-cdn}

* サーフェスからライブコンテンツをリクエストする場合を除き、直接の GraphQL クエリは使用しません。
   * 可能な限り、永続的クエリを使用します。
   * CDN がキャッシュできるよう、CDN の TTL 値を 600 秒以上に指定します。
   * AEM は既存のクエリに対するモデル変更の影響を計算できます。
* CDN へのクライアントトラフィックを減らし、より高い TTL を割り当てるため、JSON ファイル／GraphQL クエリをコンテンツ変更率の低いものと高いものに分けます。これにより、CDN でのオリジンサーバーに対する JSON の再検証が最小限に抑えられます。
* CDN からコンテンツを能動的に無効にするには、ソフトパージを使用します。これにより、CDN は、キャッシュミスを引き起こすことなくコンテンツを再ダウンロードできます。

>[!NOTE]
>
>CDN とキャッシングについて詳しくは、[その他のリソース](#additional-resources)を参照してください。

### ヘッドレスコンテンツのダウンロード時間の短縮 {#improve-download-time}

* HTTP クライアントで必ず HTTP/2 を使用します。
* HTTP クライアントで gzip に対するリクエストには必ず Accept ヘッダーを付けます。
* JSON および参照先アーティファクトをホストするために使用するドメインの数を最小限に抑えます。
* `Last-modified-since` を使用してリソースを更新します。
* JSON ファイルで `_reference` 出力を使用すると、完全な JSON ファイルを解析しなくても、アセットのダウンロードを開始できます。

<!-- End of CDN Review -->

## 実稼動へのデプロイ {#deploy-to-production}

実稼動環境へのデプロイは、Maven を使用してデプロイする&#x200B;*従来の* AEM インスタンスがあるか、または Adobe Managed Services（AMS）上にあり、つまり Cloud Manager を使用しているかどうかによって異なります。

## Maven を使用した実稼動環境へのデプロイ {#deploy-to-production-maven}

Maven を使用した&#x200B;*従来の*&#x200B;デプロイメント（AMS 以外）の概要については、[WKND チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html#build)を参照してください。

## Cloud Manager を使用した実稼動環境へのデプロイ {#deploy-to-production-cloud-manager}

Cloud Manager を使用して AMS を使用している場合、すべてがテスト済みで正常に動作することを確認した後、コードの更新を [Cloud Manager の一元化された Git リポジトリ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=ja)にプッシュできます。

アップデートが Cloud Manager にアップロードされたら、[Cloud Managerの CI／CD パイプライン](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html?lang=ja)を使用して、アップデートを AEM にデプロイできます。

<!-- Cannot find a parallel link -->
<!--
You can start deploying your code by using the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## パフォーマンスの監視 {#performance-monitoring}

AEM ヘッドレスアプリケーションの使用時に最高のユーザーエクスペリエンスを得るには、以下に説明するように、主要パフォーマンス指標を監視することが重要です。

* アプリのプレビューバージョンと実稼動バージョンの動作を検証する
* AEM ステータスページで現在のサービス稼働状況を確認する
* パフォーマンスレポートにアクセスする
   * 配信のパフォーマンス
      * オリジンサーバー - 呼び出し数、エラー率、CPU 負荷、ペイロードトラフィックを確認する
   * オーサーのパフォーマンス
      * ユーザー数、リクエスト数および読み込み数を確認する
* アプリおよびスペース固有のパフォーマンスレポートにアクセスする
   * サーバーが起動したら、一般的な指標が緑／オレンジ／赤のどれになっているかを確認し、アプリの具体的な問題を特定する
   * アプリやスペース（Photoshop デスクトップ、ペイウォールなど）にフィルタリングされた上記と同じレポートを開く
   * Splunk ログ API を使用してサービスやアプリケーションのパフォーマンスにアクセスする
   * その他の問題が発生した場合は、カスタマーサポートに連絡する

## トラブルシューティング {#troubleshooting}

### デバッグ {#debugging}

デバッグに対する一般的なアプローチとして、次のベストプラクティスに従います。

* アプリケーションのプレビューバージョンで機能とパフォーマンスを検証する
* アプリケーションの実稼動バージョンで機能とパフォーマンスを検証する
* コンテンツフラグメントエディターの JSON プレビューを使用して検証する
* クライアントアプリケーションまたは配信の問題があるかどうかを確認するには、クライアントアプリケーションで JSON を調べます。
* キャッシュされたコンテンツまたは AEM に関する問題がないかを確認するには、GraphQLを使用して JSON を調べます。

### サポートへのバグの登録 {#logging-a-bug-with-support}

さらにサポートが必要な場合に備え、サポートにバグを効率的に記録するには、次の手順に従います。

* 必要に応じて、問題のスクリーンショットを撮る
* 問題の再現方法を説明する
* 問題が再現するコンテンツを説明する
* AEM サポートポータルを通じて問題を適切な優先度で登録する

## ジャーニーの完了  {#journey-ends}

おめでとうございます。AEM ヘッドレスデベロッパージャーニーが完了し、以下を理解できました。

* ヘッドレスコンテンツ配信とヘッドフルコンテンツ配信の違い
* AEM のヘッドレス機能
* AEM ヘッドレスプロジェクトを編成する方法
* AEM でヘッドレスコンテンツを作成する方法
* AEM でヘッドレスコンテンツを取得および更新する方法
* AEM ヘッドレスプロジェクトの運用を開始する方法
* 運用開始後の作業。

皆さんは初めての AEM ヘッドレスプロジェクトの運用を既に開始しているか、またはそのために必要な知識はすべて習得できています。お疲れ様でした。

### 単一ページアプリケーションの調査 {#explore-spa}

AEM でヘッドレスストアを停止する必要はありません。[ジャーニーの「はじめに」のパート](getting-started.md#integration-levels)では、AEM でヘッドレス配信と従来のフルスタックモデルをサポートできるだけでなく、両方の利点を組み合わせたハイブリッドモデルもサポートできることを簡単に説明しました。

このような柔軟性がプロジェクトに必要な場合は、さらにジャーニーのオプションパート [AEM で単一ページアプリケーション（SPA）を作成する方法](create-spa.md)に進んでください。

## その他のリソース {#additional-resources}

* [AEM 開発ガイド](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=ja)

* [WKND チュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ja)

* [AEM 用の Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=ja)

* CDN キャッシュ

   * [CDN キャッシュの制御](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja#controlling-a-cdn-cache)

   * [CDN Rewriter](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html?lang=ja) の設定（*CDN Rewriter の検索*）

* [ヘッドレス CMS としての AEM の概要](/help/sites-developing/headless/introduction.md)
* [AEM 開発者ポータル](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ja)
* [AEM のヘッドレスに関するチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ja)
