---
title: 設定の基本概念
seo-title: 設定の基本概念
description: AEM の設定方法を学習します。
seo-description: AEM の設定方法を学習します。
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
translation-type: tm+mt
source-git-commit: 8f35717324cd2c1524fb2cf931b3ce21be05729a
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 81%

---


# 設定の基本概念{#basic-configuration-concepts}

Adobe Experience Manager（AEM）は、すべてのパラメーターにデフォルト値を割り当てた状態でインストールされるので、特別な設定をしなくても、そのまま実行できます。ただし、ユーザー固有の要件に合わせて細かい設定をすることもできます。

AEM では様々な設定をおこなえます。

* 一部の設定は[すべてのプロジェクトインストールに共通の設定](#primary-configuration-considerations)になっており、実際のプロジェクトに適しているかどうかの確認が必要です。
* 機能やシステムのパフォーマンスおよび安定性に関する設定については[細かい調整](#further-configuration-considerations)をするのが一般的ですが、必須ではありません。
* その他に、AEM の一定のオプション機能用にのみ必要な設定があります（これらについては該当する機能と合わせて説明します）。

設定を変更する際には、その設定の種類に応じて、次のいずれかの方法を使用します。

* **Adobe CQウェブコンソール**

   これは、OSGiバンドルとサービスを設定する際の標準的な場所です。

   詳細および推奨プラクティスについては、「OSGiの [設定](/help/sites-deploying/configuring-osgi.md) 」を参照してください。

* **リポジトリ**

   OSGi設定のサブセットは、リポジトリで使用できます。 そのため、リポジトリのコンテンツをコピーまたはレプリケートすることにより、同一の設定を再作成できます。実行モードに応じて、独自の設定をリポジトリに追加することもできます。

   詳しくは、[リポジトリでの OSGi 設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)、特に[リポジトリへの新しい設定の追加](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)を参照してください。

* **ファイルシステム**

   いくつかの構成ファイルがファイルシステム内に存在します。

* **AEM WCM**

   AEM WCM 内で様々な設定をおこなえます。多くは、レプリケーションエージェントなどの[ツール](/help/sites-administering/tools-consoles.md)コンソールを使用します。

>[!NOTE]
>
>Adobe Experience Manager で作業をする際には、いくつかの方法で OSGi サービスの設定を管理できます（コンソールまたはリポジトリノード）。
>
>詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

>[!NOTE]
>
>AEM の設定は簡単ですが、次の点に注意する必要があります。
>
>変更内容によっては、アプリケーションに大きな影響が及ぶ場合があります。したがって、AEM の設定を開始する前に必要な経験と知識があることを確認し、本当に必要な変更のみをおこなうようにしてください。OSGi コンソール経由でおこなわれた変更は、実行中のシステムに&#x200B;**即時に**&#x200B;適用されます（再起動は不要です）。

## 設定に関する主な考慮事項 {#primary-configuration-considerations}

このリストでは、新しいプロジェクトに共通して設定される主な領域の詳細を説明します。すべてが必要なわけではありませんが、リストを読んで検討し、実際のプロジェクトに該当するものを確認してください。

このリストでは、各設定項目の簡単な概要と、詳細を説明するページへのリンクを提供します。

### セキュリティチェックリスト {#security-checklist}

[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)には、重要な設定問題がいくつかリストされています。これを読んで、実際のインストールに必要な対処をおこなってください。

### デフォルトの UI の設定 - タッチ操作向けまたはクラシック {#configuring-the-default-ui-touch-optimized-or-classic}

AEM では次の 2 つの UI を使用できます。

* タッチ操作向け UI
* クラシック UI

必要な UI を、[ルートマッピング](/help/sites-deploying/osgi-configuration-settings.md)を使用して設定できます。

>[!NOTE]
>
>UI の選択について詳しくは、[UI の選択](/help/sites-authoring/select-ui.md)を参照してください。

### IPv4 と IPv6 {#ipv-and-ipv}

AEM のすべての要素（リポジトリ、Dispatcher など）は、IPv4 と IPv6 の両方のネットワークにインストールできます。

特別な設定は不要で、必要になったときにネットワークのタイプに応じた形式を使用して IP アドレスを指定するだけでよいので、運用はシームレスです。

つまり、IP アドレスを指定する必要がある場合には、次の形式から（必要に応じて）選択できます。

* IPv6アドレス

   for example `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4アドレス

   for example `https://123.1.1.4:4502`

* サーバー名

   for example, `https://www.yourserver.com:4502`

* the default case of `localhost` will be interpreted for both IPv4 and IPv6 network installations

   for example, `http://localhost:4502`

### バージョンのパージ {#version-purging}

AEM の標準インストールでは、（コンテンツの更新後に）ページをアクティベートするたびに、新しいバージョンのページまたはノードが作成されます。サイドキックの「**バージョン管理**」タブを使用すると、要求に応じて追加のバージョンを作成することもできます。これらのバージョンはすべてリポジトリに格納され、必要に応じて復元できます。

格納されたバージョンはパージされないので、時間の経過と共にリポジトリのサイズが大きくなっていきます。そこで、管理が必要になります。

詳しくは、[バージョンのパージ](/help/sites-deploying/version-purging.md)を参照してください。特に、新しいバージョンが作成されたときに古いバージョンをパージするように AEM を設定する方法については、[バージョンマネージャー](/help/sites-deploying/version-purging.md#version-manager)を参照してください。

### ログ {#logging}

AEM では、次の設定が可能です。

* 中央のログサービスのグローバルパラメーター
* 要求データのログ（要求情報用の特殊なログ設定）
* 個々のサービス固有の設定;例えば、個々のログファイルやログメッセージの形式

詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。

### 実行モード {#run-modes}

実行モードを使用すると、オーサーまたはパブリッシュ、テスト、開発、イントラネットなど、特定の目的に合わせて AEM インスタンスを調整できます。

これをおこなうには、各実行モードの設定パラメーターのコレクションを定義します。設定パラメーターの基本セットがすべての実行モードに適用され、その後、具体的な環境の目的に合わせて追加のセットを調整できます。これらが必要に応じて適用されます。

設定はすべて 1 つのリポジトリに格納され、**実行モード**&#x200B;を設定することでアクティベートされます。

詳しくは、[実行モード](/help/sites-deploying/configure-runmodes.md)を参照してください。

### シングルサインオン {#single-sign-on}

シングルサインオン（SSO）は、ユーザーが認証の資格情報（ユーザー名、パスワードなど）を一度入力すれば、その後は複数のシステムにアクセスできるようにするものです。個別のシステム（信頼された認証として知られる）が認証を実行し、Adobe Experience Manager に対してユーザーの資格情報を提供します。Adobe Experience Manager がそのユーザーのアクセス権を確認し、適用します（つまり、ユーザーがアクセスを許可されているリソースを決定します）。

詳しくは、[シングルサインオン](/help/sites-deploying/single-sign-on.md)を参照してください。

### リソースマッピング {#resource-mapping}

リソースマッピングは、リダイレクト、バニティー URL および AEM 用の仮想ホストを定義するために使用します。

例えば、これらのマッピングを使用すると次のことが可能です。

* Prefix all requests with `/content` so that the internal structure is hidden from the visitors to your website.
* Define a redirect so that all requests to the `/content/en/gateway` page of your website are redirected to `https://gbiv.com/`.

詳しくは、[リソースマッピング](/help/sites-deploying/resource-mapping.md)を参照してください。

### レプリケーション、リバースレプリケーションおよびレプリケーションエージェント {#replication-reverse-replication-and-replication-agents}

レプリケーションエージェントは AEM の中核であり、次の目的で使用されます。

* オーサー環境からパブリッシュ環境へコンテンツを[公開（アクティベート）](/help/sites-authoring/publishing-pages.md)
* Dispatcher キャッシュからコンテンツを明示的にフラッシュ
* ユーザー入力（フォーム入力など）をパブリッシュ環境からオーサー環境（オーサー環境の制御下）に戻す。

詳しくは、[レプリケーション](/help/sites-deploying/replication.md)を参照してください。

### OSGi 設定 {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) はAEMのテクノロジスタックの基本要素です。AEMの複合バンドルとその設定を制御するために使用されます。

プロジェクト実装に関連する様々なバンドルのリストについては、[OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md)を参照してください（バンドルに基づいてリストされています）。リストされているすべての設定に調整が必要なわけではなく、一部の設定は AEM の動作を説明する目的で記載されています。

AEM と連携する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

### LDAP の設定 {#configuring-ldap}

LDAP 認証は、Active Directory などの（中央の）LDAP ディレクトリに格納されているユーザーを認証するために必要です。これにより、ユーザーアカウントの管理に必要な労力が軽減されます。

LDAP 認証はリポジトリレベルでおこなわれるので、リポジトリによって直接処理されます。For further details, see [Configuring LDAP with AEM](/help/sites-administering/ldap-config.md).

AEM 内のユーザー管理（アクセス権の割り当てを含む）について詳しくは、[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

### Dispatcher の設定 {#configuring-the-dispatcher}

ディスパッチャーは、Adobe Experience Managerのキャッシュおよびロードバランシングのツールで、エンタープライズクラスのWebサーバーと組み合わせて使用できます。

詳しくは、[Dispatcher ](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)を参照してください。特に、設定の詳細については、[Dispatcher の設定](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html)を参照してください。

### AEM LiveCycle Connector の設定 {#configuring-aem-livecycle-connector}

With the release of the AEM Doc Services and AEM Doc Security, we now have the capability to invoke the LiveCycle doc services to render an XFA form, convert a document to PDF and policy protect a document. Please read [AEM LiveCycle Connector](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) for more details.

### ジョブのオフロードとトポロジの管理 {#job-offloading-and-topology-administration}

[オフロード](/help/sites-deploying/offloading.md)によって、トポロジ内の Experience Manager インスタンス間で処理タスクが配布されます。オフロードでは、特定の Experience Manager インスタンスを使用して、特定のタイプの処理を実行できます。処理を特化することによって、利用可能なサーバーリソースを最大限に使用できます。

トポロジは、オフロードに参加する疎結合された Experience Manager クラスターです。クラスターは 1 つ以上の Experience Manager サーバーインスタンスで構成されます（単一のインスタンスがクラスターと見なされます）。

トポロジメンバーシップの表示または変更方法について詳しくは、[トポロジの管理](/help/sites-deploying/offloading.md#administering-topologies)を参照してください。

### ようこそコンソールの設定 {#configuring-the-welcome-console}

クラシック UI のようこそコンソールには、AEM 内の様々なコンソールおよび機能へのリンクのリストが表示されます。

表示可能なリンクを設定することもできます。詳しくは、[ようこそコンソールの設定](/help/sites-developing/customizing-the-welcome-console.md)を参照してください。

### パフォーマンスの設定 {#configuring-for-performance}

[パフォーマンス](/help/sites-deploying/configuring-performance.md)はプロジェクトの鍵となります。パフォーマンスを最適化するために AEM（および基盤となるリポジトリ）の特定の要素を設定できます。

詳しくは、[パフォーマンスの設定](/help/sites-deploying/configuring-performance.md#configuring-for-performance)を参照してください。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 共有データストア {#shared-data-store}

リポジトリ・データ・ストアは、大きなバイナリのストレージを別の領域に固有のリポジトリからオフロードするために使用され、リポジトリ・ツリー内の同じバイナリ（例えばイメージ）の複数のインスタンスが1回だけ格納されます。

この「1 回の格納で複数回参照する」機能を拡張し、それぞれのデータストアが共有ファイルシステムの同じ場所を参照するように設定すると、単一のリポジトリツリーだけでなく、完全に別々の複数のリポジトリにも対応できます。

このようなデータストアは、同じクラスター内の別々のノード、同じインストール内の別々のパブリッシュインスタンスやオーサーインスタンス、さらには別々のインストールのまったく別々のインスタンスの間でも、共有可能です。

詳しくは、[ノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)を参照してください。

## 設定に関するその他の考慮事項 {#further-configuration-considerations}

### HTTP over SSL の有効化 {#enabling-http-over-ssl}

HTTP over SSL を有効にして、サーバーへの接続のセキュリティを強化できます。

詳しくは、[HTTP over SSL の有効化](/help/sites-administering/ssl-by-default.md)を参照してください。

### AEM ポータルとポートレット {#aem-portals-and-portlets}

ポータルとは、パーソナライズ、シングルサインオン、別々のソースからのコンテンツ統合を提供し、情報システムのプレゼンテーションレイヤーをホストする Web アプリケーションです。ポートレットコンポーネントでも、ポートレットをページに埋め込むことができます。CQ5 WCM で提供されているコンテンツにアクセスするために、ポータルサーバーを CQ5 Portal Director Portlet に組み込むことができます。これをおこなうには、ポートレットをインストールして設定し、ポータルページに追加します。

詳しくは、「 [ポータルとポートレット](/help/sites-administering/aem-as-portal.md) 」を参照してください。

### 静的オブジェクトの有効期限 {#expiration-of-static-objects}

アイコンなどの静的オブジェクトは変化しません。したがって、不必要なトラフィックを減らすために、静的オブジェクトを（ある程度の期間は）期限切れにならないように設定する必要があります。

詳しくは、[静的オブジェクトの有効期限](/help/sites-deploying/expiration-static-objects.md)を参照してください。

### Java プロセスでファイルを開く {#open-files-in-the-java-process}

個々の Java プロセスがファイルにアクセスする場合がありますが、これにはシステムリソースが必要です。この理由から、プロセスごとに同時にアクセスできるファイル数の上限が定義されています。これを超えると、例外エラーが発生する場合があります。

If the AEM process exceeds this maximum, then the message &quot; `too many open files`&quot; will be seen in `error.log`.

このような例外を回避するには、次の処理をおこなう必要があります。

1. AEMプロセスで使用している開いているファイルの数を確認します。

   このチェックを行う方法は、インスタンスを実行しているプラットフォームに応じて異なります。 lsof(Unix)やProcess Explorer(Windows)などのユーティリティを使用できます。

   この値は、開発およびテスト中に監視する必要があります。

   * ファイルが必要に応じて閉じられていることを確認するため
   * 様々な状況下での必要な最大値を特定するため

1. 許可する最大値を設定します。

   この新しい値は、現在のニーズと将来のピークの両方に適している必要があるので、現在のニーズを重複することをお勧めします。

   デフォルトでは、 `serverctl` は次 `CQ_MAX_OPEN_FILES` に設定し `8192`ます。これは、ほとんどのシナリオで十分です。

### リッチテキストエディターの設定 {#configuring-the-rich-text-editor}

**リッチテキストエディター**（**RTE**）では、テキストコンテンツを編集するための幅広い[機能](/help/sites-authoring/rich-text-editor.md)が提供されており、アイコン、選択ボックス、メニューを追加することによって WYSIWYG エクスペリエンスを実現できます。

詳しくは、[リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md)を参照してください。

### ページ編集のための取り消しの設定 {#configuring-undo-for-page-editing}

ページ編集操作の取り消し／やり直しコマンドの動作を制御するためのプロパティがいくつかあります。これらのプロパティの設定については、[ページ編集のための取り消しの設定](/help/sites-administering/config-undo.md)を参照してください。

### ビデオコンポーネントの設定 {#configuring-the-video-component}

[ビデオコンポーネント](/help/sites-authoring/default-components-foundation.md#video)を使用すると、ページに定義済みの標準提供ビデオ要素を配置できます。

適切なトランスコーディングをおこなうには、管理者が個別に [FFmpeg をインストール](/help/sites-administering/config-video.md#install-ffmpeg)する必要があります。また、HTML5 要素で使用するように[ビデオプロファイルを設定](/help/sites-administering/config-video.md#configure-video-profiles)することもできます。

### レポートの設定とカスタマイズ {#configuring-and-customizing-reports}

インスタンスの状態を監視および分析しやすいように、CQ ではデフォルトのレポートが提供されており、個々の要件に合わせて設定できます。

詳しくは、[レポートのカスタマイズの基本](/help/sites-administering/reporting.md#the-basics-of-report-customization)を参照してください。

### 電子メール通知の設定 {#configuring-email-notification}

CQ は、次のようなユーザーに電子メール通知を送信します。

* 変更やレプリケーションなど、ページイベントを購読したことがある
* フォーラムイベントを購読したことがある
* ワークフローで手順を実行する必要がある

詳しくは、[電子メール通知の設定](/help/sites-administering/notification.md)を参照してください。

### ページインプレッションの有効化 {#enabling-page-impressions}

ページインプレッションは、クラシック UI のサイト管理コンソールの「**インプレッション数**」列に表示されます。ページインプレッションの取得を有効にするには、次の設定をおこなう必要があります。

* パブリッシュインスタンス上：

   * [Day CQ WCM Page Statistics](/help/sites-deploying/osgi-configuration-settings.md)

* オーサーインスタンス上：

   * [Adobeページインプレッショントラック](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>オーサー環境の Adobe Page Impressions Tracker の設定では、トラッキングサービスへの匿名リクエストが許可されます。

