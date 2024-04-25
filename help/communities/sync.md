---
title: コミュニティのユーザーの同期
description: Adobe Experience Manager Communities でのユーザー同期の仕組みを説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2403'
ht-degree: 7%

---

# コミュニティのユーザーの同期 {#communities-user-synchronization}

## はじめに {#introduction}

Adobe Experience Manager（AEM） Communities では、（設定された権限に応じて）パブリッシュ環境から、 *サイト訪問者* ～になる可能性がある *メンバー*、作成 *ユーザーグループ*、およびを編集します *メンバープロファイル* .

*ユーザーデータ* が参照する *ユーザー*, *ユーザープロファイル*、および *ユーザーグループ*.

*メンバー* 参照： *ユーザー* オーサー環境に登録されたユーザーではなく、パブリッシュ環境に登録されている。

ユーザーデータについて詳しくは、次を参照してください： [ユーザーとユーザーグループの管理](/help/communities/users.md).

## パブリッシュファーム全体でのユーザーの同期 {#synchronizing-users-across-a-publish-farm}

仕様上、パブリッシュ環境で作成されたユーザーデータは、オーサー環境では表示されません。

オーサー環境で作成されるほとんどのユーザーデータは、オーサー環境に保持されることを目的としており、パブリッシュインスタンスへの同期やレプリケートは行われません。

いつ [トポロジ](/help/communities/topologies.md) が [パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm)1 つのパブリッシュインスタンスで行った登録と変更は、他のパブリッシュインスタンスと同期する必要があります。 メンバーは、任意のパブリッシュノードにログインしてデータを表示できる必要があります。

ユーザー同期を有効にすると、ユーザーデータがファームのパブリッシュインスタンス間で自動的に同期されます。

### ユーザー同期の設定手順 {#user-sync-setup-instructions}

パブリッシュファーム全体で同期を有効にする手順について詳しくは、 [ユーザーの同期](/help/sites-administering/sync.md).

## バックグラウンドでのユーザー同期 {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vlt パッケージ**

  これは、パブリッシャーで行われたすべての変更の zip ファイルで、パブリッシャー間で配布する必要があります。 パブリッシャーでの変更は、変更イベントリスナーによって選択されるイベントを生成します。 これにより、すべての変更を含んだ vlt パッケージが作成されます。

* **配布パッケージ**

  Sling の配布情報が含まれます。 これは、コンテンツの配布先と、最後に配布された日時に関する情報です。

## 各種操作の結果 {#what-happens-when}

### コミュニティサイトコンソールからのサイトの公開 {#publish-site-from-communities-sites-console}

オーサー環境で、コミュニティサイトが次から公開されたとき [コミュニティサイトコンソール](/help/communities/sites-console.md)の場合、次のようになります [複製](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) 関連するページと Sling が、動的に作成されたコミュニティユーザーグループ（メンバーシップを含む）を配布します。

### ユーザーがパブリッシュでプロファイルを作成または編集します {#user-is-created-or-edits-profile-on-publish}

仕様上、パブリッシュ環境で作成されたユーザーとプロファイル（自己登録、ソーシャルログイン、LDAP 認証など）は、オーサー環境では表示されません。

トポロジーが[パブリッシュファーム](/help/communities/topologies.md)であり、ユーザー同期が正しく設定されると、Sling 配布を使用して&#x200B;*ユーザー*&#x200B;と&#x200B;*ユーザープロファイル*&#x200B;がパブリッシュファーム間で同期されます。

### パブリッシュ環境に新しいコミュニティグループが作成される {#new-community-group-is-created-on-publish}

パブリッシュインスタンスから開始しますが、実際にはオーサーインスタンスでコミュニティグループの作成が行われます。これにより、新しいサイトページと新しいユーザーグループが作成されます。

プロセスの一環として、新しいサイトページがすべてのパブリッシュインスタンスにレプリケートされます。 動的に作成されたコミュニティユーザーグループとそのメンバーシップは、すべてのパブリッシュインスタンスに配布される Sling です。

### セキュリティコンソールを使用してユーザーやユーザーグループが作成される場合 {#users-or-user-groups-are-created-using-security-console}

仕様上、パブリッシュ環境で作成されたユーザーデータはオーサー環境には表示されず、逆も同様です。

いつ [ユーザー管理とセキュリティ](/help/sites-administering/security.md) コンソールを使用すると、パブリッシュ環境で新しいユーザーを追加でき、ユーザーの同期機能により、新しいユーザーとそのグループメンバーシップがその他のパブリッシュインスタンスに同期されます（必要な場合）。 ユーザー同期により、セキュリティコンソールによって作成されたユーザーグループも同期されます。

### ユーザーが公開時にコンテンツを投稿 {#user-posts-content-on-publish}

ユーザー生成コンテンツ（UGC）の場合、パブリッシュインスタンスに入力されたデータには、経由でアクセスできます [設定済みの SRP](/help/communities/srp-config.md).

## ベストプラクティス {#bestpractices}

デフォルトでは、ユーザー同期はになっています。 **disabled**. ユーザー同期を有効にするには、以下を変更する必要があります。 *既存* OSGi 設定。 ユーザー同期を有効にした結果、新しい設定が追加されることはありません。

ユーザー同期は、ユーザーデータがオーサー環境で作成されていない場合でも、オーサー環境でユーザーデータの配布を管理します。

**前提条件**

1. ）1 つのパブリッシャーでユーザーおよびユーザーグループが既に作成されている場合は、ユーザー同期を設定して有効にする前に、ユーザーデータをすべてのパブリッシャーと[手動で同期](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups)することをお勧めします。

   ユーザー同期を有効にすると、新しく作成したユーザーおよびグループのみが同期されるようになります。

1. 最新のコードがインストールされていることを確認します。

   * [AEM プラットフォームの更新](https://helpx.adobe.com/jp/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities の更新](/help/communities/deploy-communities.md#latestfeaturepack)

AEM Communitiesでユーザー同期を有効にするには、次の設定が必要です。 Sling コンテンツの配布が失敗しないように、これらの設定が正しいことを確認します。

### Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

この設定では、パブリッシャー全体で同期するコンテンツを取得します。 設定はオーサーインスタンス上にあります。 作成者は、そこにあるすべてのパブリッシャーと、すべての情報をどこで同期するかを追跡する必要があります。

設定のデフォルト値は、1 つのパブリッシュインスタンス用です。 ユーザー同期は、複数のパブリッシュインスタンスを同期する場合に役立ちます（パブリッシュファーム用に複数のパブリッシュインスタンスを同期する場合など）。追加のパブリッシュインスタンスを設定に追加する必要があります。

**コンテンツはどのように同期されますか？**

オーサーインスタンスがパブリッシャーのエクスポーターエンドポイントに ping を送信します。 特定のパブリッシャー（n）でユーザーが作成または更新されるたびに、オーサーはエクスポーターエンドポイントおよびエンドポイントからコンテンツを取得します。 [コンテンツをプッシュ](/help/communities/sync.md#main-pars-image-1413756164) （コンテンツの取得元のパブリッシャーとは別のパブリッシャー（n-1）に送信されます）。

Apache Sling Sync Agents を設定するには：

1. AEM オーサーインスタンスに管理者権限でログインします。
1. へのアクセス [Web コンソール](/help/sites-deploying/configuring-osgi.md). 例： [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. を見つける **Apache Sling Distribution Agent - Sync Agents Factory**.

   * 編集する既存の設定を選択します（鉛筆アイコン）。

     名前の確認： **socialpubsync。**

   * 「**有効**」チェックボックスを選択します。
   * を選択 **複数のキューを使用します。**
   * を指定 **エクスポーターエンドポイント** および **インポーターエンドポイント** （エクスポーターエンドポイントとインポーターエンドポイントをさらに追加できます）。

     これらのエンドポイントは、コンテンツの取得元と、コンテンツのプッシュ先を定義します。 オーサーは、指定されたエクスポーターエンドポイントからコンテンツを取得し、コンテンツをパブリッシャー（コンテンツの取得元のパブリッシャーを除く）にプッシュします。

   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite 配布 – 暗号化されたパスワードトランスポート秘密鍵プロバイダー {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

これにより、オーサーからパブリッシュにユーザーデータを同期する権限を持つユーザーとして、オーサーは承認済みユーザーを識別できます。

この [承認済みユーザーが作成されました](/help/sites-administering/sync.md#createauthuser) すべてのパブリッシュインスタンスで、パブリッシャーはオーサーと接続し、オーサー上の Sling 配布を設定できます。 この承認済みユーザーには、必要なものがすべて含まれています [ACL](/help/sites-administering/sync.md#howtoaddacl).

データをパブリッシャーにインストールしたり、パブリッシャーから取得したりするたびに、オーサーは、この設定で設定された資格情報（ユーザー名とパスワード）を使用してパブリッシャーと接続します。

承認済みユーザーを使用してオーサーをパブリッシャーに接続するには：

1. AEM オーサーインスタンスに管理者権限でログインします。
1. へのアクセス [Web コンソール](/help/sites-deploying/configuring-osgi.md).

   例： [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. を見つける **Adobe Granite 配布 – 暗号化されたパスワードトランスポート秘密鍵プロバイダー。**
1. 編集する既存の設定を選択します（鉛筆アイコン）。

   プロパティを検証 **socialpubsync** - **publishUser です。**

1. ユーザー名とパスワードをに設定します。 [承認済みユーザー](/help/sites-administering/sync.md#createauthorizeduser).

   例： **usersync – 管理者**

![granite-paswrd-trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

この設定は、公開元間で同期するデータを設定するために使用されます。 で指定されたパスでデータが作成/更新された場合 **許可されたルート**&#x200B;を選択すると、「var/community/distribution/diff」がアクティブ化され、作成されたレプリケーターがパブリッシャーからデータを取得し、他のパブリッシャーにインストールします。

同期するデータ（ノードパス）を設定するには：

1. パブリッシュインスタンスに対する管理者権限でログインします。
1. へのアクセス [Web コンソール](/help/sites-deploying/configuring-osgi.md).

   例： [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. を見つける **Apache Sling Distribution Agent - Queue Agents Factory**.
1. 編集する既存の設定を選択します（鉛筆アイコン）。

   名前の確認： **socialpubsync -reverse**

1. 「」を選択します **Enabled** チェックボックスをオンにして保存します。
1. でレプリケートされるノードパスを指定 **許可されたルート**.
1. 各について繰り返します **publish** インスタンス。

   ![queue-agents-fact](assets/queue-agents-fact.png)

### Adobe Granite 配布 – 差分監視者ファクトリ {#adobe-granite-distribution-diff-observer-factory}

この構成では、パブリッシャー間でグループメンバーシップが同期されます。
あるパブリッシャー内のグループのメンバーシップを変更しても他のパブリッシャー上のメンバーシップが更新されない場合は、次のことを確認します **ref :members** がに追加されました **検索されたプロパティ名**.

メンバーの同期を確保するには：

1. パブリッシュインスタンスに対する管理者権限でログインします。
1. へのアクセス [Web コンソール](/help/sites-deploying/configuring-osgi.md).

   例： [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. を見つける **Adobe Granite 配布 – 差分監視者ファクトリ**.
1. 編集する既存の設定を選択します（鉛筆アイコン）。

   検証 **エージェント名：socialpubsync -reverse**.

1. 「**有効**」チェックボックスを選択します。
1. を指定 **rep:members** の propertyName の説明として **検索されたプロパティ名**&#x200B;を選択して、保存します。

   ![diff-obs](assets/diff-obs.png)

### Apache Sling 配布トリガー- スケジュール済みトリガーファクトリ {#apache-sling-distribution-trigger-scheduled-triggers-factory}

この設定を使用すると、（パブリッシャーが ping を送信し、変更がオーサーによって取り込まれる）ポーリング間隔を設定して、パブリッシャー間で変更を同期できます。

作成者は 30 秒ごとに公開者をポーリングします（デフォルト）。 フォルダーにパッケージが存在する場合 `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`その後、これらのパッケージを取得し、他のパブリッシャーにインストールします。

ポーリング間隔を変更するには、次の手順に従います。

1. AEM オーサーインスタンスに管理者権限でログインします。
1. へのアクセス [Web コンソール](/help/sites-deploying/configuring-osgi.md)、例： [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. を見つける **Apache Sling 配布トリガー- スケジュール済みトリガーファクトリ**

   * 編集する既存の設定を選択します（鉛筆アイコン）。

     検証 **socialpubsync – スケジュール済みトリガー**

   * 「間隔（秒）」に目的の間隔を設定して、保存します。

   ![スケジュール済みトリガー](assets/scheduled-trigger.png)

### AEM Communities User Sync Listener {#aem-communities-user-sync-listener}

Sling 配布でサブスクリプションとフォローに不一致がある問題については、で次のプロパティを確認してください。 **AEM Communities User Sync Listener** 設定は次のとおりです。

* NodeType
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

購読、フォローおよび通知を同期するには

各AEM パブリッシュインスタンスで以下をおこないます。

1. 管理者権限でログインします。
1. へのアクセス [Web コンソール](/help/sites-deploying/configuring-osgi.md). 例： [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. を見つける **AEM Communities User Sync Listener**.
1. 編集する既存の設定を選択します（鉛筆アイコン）。

   名前の確認： **socialpubsync – スケジュール済みトリガー**

1. 以下を設定します **NodeType**:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   このプロパティで指定されたノードタイプは同期され、通知情報（後続のブログと設定）は異なるパブリッシャー間で同期されます。

1. 同期するフォルダーをすべて追加 **DistributedFolders**. 例：

   `segments/scoring`

   `social/relationships`

   `activities`

1. を **ignorablenodes** コピー先：

   `.tokens`

   `system`

   `rep:cache` （スティッキーセッションが使用されるので、このノードを別のパブリッシャーと同期する必要はありません）。

   ![user-sync-listner](assets/user-sync-listner.png)

### ユニーク Sling ID {#unique-sling-id}

AEM オーサーインスタンスは、Sling ID を使用して、データの発信元と、パッケージの送信先とする必要がある（または必要がない）パブリッシャーを識別します。

パブリッシュファーム内のすべてのパブリッシャーが一意の Sling ID を持っていることを確認します。 Sling ID がパブリッシュファームの複数のパブリッシュインスタンスで同じである場合、ユーザーの同期は失敗します。 パッケージの取得元とインストール先が不明な場合はインストールします。

パブリッシュファーム内のパブリッシャーの Sling ID が一意になるようにするには、各パブリッシュインスタンスで次の手順を実行します。

1. を参照 [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. の値を確認します。 **Sling ID**.

   ![slingid](assets/slingid.png)

   あるパブリッシュインスタンスの Sling ID が他のパブリッシュインスタンスの Sling ID と一致する場合は、次のようにします。

1. 一致する Sling ID を持つパブリッシュインスタンスの 1 つを停止します。
1. が含まれる `crx-quickstart/launchpad/felix` ディレクトリ、検索し、という名前のファイルを削除します。 *sling.id.file です。*

   例えば、Linux システムの場合、次のようになります。

   `rm -i $(find . -type f -name sling.id.file)`

   例えば、Windows システムの場合、次のようになります。

   Windows エクスプローラーを使用して検索する `sling.id.file`

1. パブリッシュインスタンスを起動します。 起動時に新しい Sling ID が割り当てられます。
1. を検証します **Sling ID** が一意になりました。

すべてのパブリッシュインスタンスの Sling ID が一意になるまでこの手順を繰り返します。

### Vault Package Builder Factory {#vault-package-builder-factory}

更新を正しく同期させるには、ユーザー同期用に Vault Package Builder を変更する必要があります。
対象： `/home/users`, a `*/rep:cache` ノードが作成されます。 ノードのプリンシパル名に対してクエリを実行すると、このキャッシュを直接使用できることを見つけるために使用されるキャッシュです。

次の場合、ユーザーの同期を停止できます `rep :cache` ノードはパブリッシャー間で同期されます。

更新がパブリッシャー間で正しく同期されるようにするには、各AEM パブリッシュインスタンスで次の手順を実行します。

1. へのアクセス [Web コンソール](/help/sites-deploying/configuring-osgi.md)

   例： [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. を見つけます。 **Apache Sling Distribution Packaging - Vault Package Builder Factory**

   ビルダー名：socialpubsync-vlt。

1. 編集アイコンを選択します。
1. 2 つのパッケージノードフィルターを追加します。
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. ポリシーの処理
   * 既存の rep :policy ノードを新しいノードで上書きするには、3 番目のパッケージフィルターを追加します `/home/users|+.*/rep:policy`
   * ポリシーが配布されないようにするには、次のように設定します。 `Acl Handling: IGNORE`

   ![Vault パッケージビルダーファクトリ](assets/vault-package-builder-factory.png)

## AEM Communitiesでの Sling 配布のトラブルシューティング {#troubleshoot-sling-distribution-in-aem-communities}

Sling 配布が失敗した場合は、次のデバッグ手順を試します。

1. **チェック対象 [設定が不適切に追加されました](/help/sites-administering/sync.md#improperconfig)**

   複数の設定を追加または編集するのではなく、既存のデフォルト設定を編集する必要があります。
1. **設定を確認**

   すべての [設定](/help/communities/sync.md#bestpractices) で説明されているように、AEM オーサーインスタンスに適切に設定されます。 [ベストプラクティス](/help/communities/sync.md#main-pars-header-863110628).

1. **承認済みユーザー権限の確認**

   パッケージが正しくインストールされていない場合は、 [承認済みユーザー](/help/sites-administering/sync.md#createauthuser) 最初のパブリッシュインスタンスで作成された場合、適切な ACL が設定されています。

   検証するには、以下の手順を実行します [作成承認済みユーザー](/help/sites-administering/sync.md#createauthuser) 変更： [Adobe Granite 配布 – 暗号化されたパスワードトランスポート秘密鍵プロバイダー](/help/sites-administering/sync.md#adobegraniteencpasswrd) 管理者ユーザーの資格情報を使用するようにオーサーインスタンスを設定します。 次に、パッケージを再度インストールしてみてください。 管理者の資格情報でユーザーの同期が正常に機能する場合は、作成された公開ユーザーに適切な ACL がなかったことを意味します。

1. **差分監視者ファクトリ設定を確認します**

   パブリッシュファーム全体で特定のノードのみが同期されない場合（グループメンバーが同期されない場合など）は、次のことを確認します [Adobe Granite 配布 – 差分監視者ファクトリ](/help/sites-administering/sync.md#diffobserver) 設定が有効で、 **rep: members** に設定されています **検索されたプロパティ名**.

1. **AEM Communities User Sync Listener の設定を確認します。** 作成したユーザーが同期されても購読とフォローが機能しない場合は、AEM Communities ユーザー同期リスナーの設定に次の情報があることを確認します。

   * ノードタイプ – に設定 **rep:User, nt:unstructured**, **nt:resource**, **rep:ACL**, **sling:Folder**、および **sling:OrderedFolder**.
   * 無視可能なノード – に設定 **.tokens**, **system**、および **rep :cache**.
   * Distributed Folders：配布するフォルダを設定します。

1. **パブリッシュインスタンスでユーザーの作成時に生成されたログを確認**

   上記の設定が適切に行われているのにユーザー同期が機能しない場合は、ユーザーの作成時に生成されたログを確認します。

   次のように、ログの順序が同じかどうかを確認します。

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

デバッグするには：

1. ユーザー同期を無効にします。
1. AEM オーサーインスタンスで、管理者権限でログインします。

   1. へのアクセス [Web コンソール](/help/sites-deploying/configuring-osgi.md). 例： [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. 設定を見つけます。 **Apache Sling Distribution Agent - Sync Agents Factory**.
   1. の選択を解除 **Enabled** チェックボックスをオンにします。

      オーサーインスタンス（エクスポーターとインポーター）のエンドポイントのユーザー同期を無効にすると無効になり、オーサーインスタンスは静的になります。 この **vlt** オーサーによってパッケージが ping または取得されない。

      次に、パブリッシュインスタンスでユーザーが作成された場合、 **vlt** パッケージの作成先 */var/sling/distribution/packages/ socialpubsync - vlt /data* ノード。 また、作成者がこれらのパッケージを別のサービスにプッシュした場合も同様です。 このデータをダウンロードして抽出すると、他のサービスにプッシュされたすべてのプロパティを確認できます。

1. パブリッシャーに移動し、パブリッシャーでユーザーを作成します。 その結果、イベントが作成されます。
1. を確認します [ログの順序](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities) ユーザーの作成時に作成されます。
1. 次のかどうかを確認します **vlt** パッケージの作成日 **/var/sling/distribution/packages/socialpubsync-vlt/data**.
1. 次に、AEM オーサーインスタンスでユーザー同期を有効にします。
1. パブリッシャーで、のエクスポーターまたはインポーターエンドポイントを変更します **Apache Sling Distribution Agent - Sync Agents Factory**.
パッケージデータをダウンロードして抽出し、他のパブリッシャーにプッシュされたプロパティと、失われたデータをすべて確認できます。
