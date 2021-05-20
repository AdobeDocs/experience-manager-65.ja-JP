---
title: コミュニティのユーザーの同期
seo-title: コミュニティのユーザーの同期
description: ユーザーの同期の仕組み
seo-description: ユーザーの同期の仕組み
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
role: Administrator
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 20%

---

# コミュニティのユーザーの同期 {#communities-user-synchronization}

## はじめに {#introduction}

AEM Communitiesでは、パブリッシュ環境から（設定されている権限に応じて）、*サイト訪問者*&#x200B;が&#x200B;*メンバー*&#x200B;になり、*ユーザーグループ*&#x200B;を作成して、*メンバープロファイル*&#x200B;を編集します。

*ユーザ* ーデータとは、ユーザー *、ユーザープロファイ*&#x200B;ル、ユーザーグ *ループ*  **&#x200B;を指します。

メンバーという用語は、オーサー環境で登録されたユーザーではなく、パブリッシュ環境で登録されたユーザーを指します。****

ユーザーデータについて詳しくは、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。

## パブリッシュファーム間のユーザーの同期  {#synchronizing-users-across-a-publish-farm}

仕様上、パブリッシュ環境で作成されたデータは、オーサー環境では表示されません。

オーサー環境で作成されたほとんどのユーザーデータは、オーサー環境に残されたままとなり、パブリッシュインスタンスには同期もレプリケートもされません。

[トポロジ](/help/communities/topologies.md)が[パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm)の場合、1つのパブリッシュインスタンスに対する登録と変更を他のパブリッシュインスタンスと同期する必要があります。 メンバーは、ログインして、任意のパブリッシュノードでデータを確認できる必要があります。

ユーザーの同期を有効にすると、ファーム内のパブリッシュインスタンス間でユーザーデータが自動的に同期されます。

### ユーザーの同期のセットアップ手順  {#user-sync-setup-instructions}

パブリッシュファーム間で同期を有効にする手順について詳しくは、次を参照してください。

* [ユーザー同期](/help/sites-administering/sync.md)

## バックグラウンドでのユーザー同期{#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vltパッケージ**

   これは、パブリッシャーでおこなわれたすべての変更のzipファイルで、パブリッシャー間で配布する必要があります。 パブリッシャーでの変更は、変更イベントリスナーによって選択されるイベントを生成します。 これにより、すべての変更を含むvltパッケージが作成されます。

* **配布パッケージ**

   Slingの配布情報が含まれます。 これは、コンテンツの配信先と最後に配信された日時に関する情報です。

## ... {#what-happens-when}の場合の影響

### コミュニティのサイトコンソールでのサイトの公開 {#publish-site-from-communities-sites-console}

オーサー環境で、コミュニティサイトを[コミュニティサイトコンソール](/help/communities/sites-console.md)から公開すると、関連するページが[レプリケート](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents)されます。また、Sling によって、動的に作成されたコミュニティユーザーグループ（メンバーシップを含む）が配信されます。

### パブリッシュ環境でのユーザーの作成またはプロファイルの編集  {#user-is-created-or-edits-profile-on-publish}

仕様上、パブリッシュ環境で（自己登録、ソーシャルログイン、LDAP 認証などで）作成されたユーザーやプロファイルはオーサー環境では表示されません。

トポロジが[パブリッシュファーム](/help/communities/topologies.md)で、ユーザー同期が正しく設定されている場合、*ユーザー*&#x200B;と&#x200B;*ユーザープロファイル*&#x200B;は、Sling配布を使用してパブリッシュファーム全体で同期されます。

### パブリッシュ環境での新しいコミュニティグループの作成 {#new-community-group-is-created-on-publish}

パブリッシュインスタンスから開始されたコミュニティグループの作成は、新しいサイトページと新しいユーザーグループに結び付きますが、実際にはオーサーインスタンス上でおこなわれます。

このプロセスの一環として、新しいサイトページがすべてのパブリッシュインスタンスにレプリケートされます。動的に作成されるコミュニティユーザーグループとそのメンバーシップは、Slingですべてのパブリッシュインスタンスに配布されます。

### セキュリティコンソールでのユーザーまたはユーザーグループの作成 {#users-or-user-groups-are-created-using-security-console}

仕様上、パブリッシュ環境で作成されたユーザーデータは、オーサー環境では表示されません。その反対も同様です。

[ユーザー管理およびセキュリティ](/help/sites-administering/security.md)コンソールを使用してパブリッシュ環境で新しいユーザーを追加すると、ユーザーの同期機能により、新しいユーザーとそのグループメンバーシップがその他のパブリッシュインスタンスに同期されます（必要な場合）。ユーザー同期では、セキュリティコンソールを使用して作成したユーザーグループも同期されます。

### ユーザーによるパブリッシュ環境でのコンテンツの投稿 {#user-posts-content-on-publish}

ユーザー生成コンテンツ（UGC）に関しては、パブリッシュインスタンスで入力されたデータへのアクセスは、[設定済みの SRP](/help/communities/srp-config.md) を通じておこなわれます。

## ベストプラクティス {#bestpractices}

デフォルトでは、ユーザー同期は&#x200B;**無効**&#x200B;になっています。ユーザー同期を有効にするには、OSGi の既存の&#x200B;**&#x200B;設定を変更する必要があります。ユーザー同期を有効にした結果、新しい設定が追加されることはありません。

ユーザー同期では、オーサー環境で作成されていないユーザーデータでもその配布の管理はオーサー環境に依存します。

**前提条件**

1. ユーザーとユーザーグループが既に1つのパブリッシャー上に作成されている場合は、ユーザー同期を設定して有効にする前に、[すべてのパブリッシャーに](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups)ユーザーデータを手動で同期することをお勧めします。

   ユーザー同期を有効にすると、新規に作成されたユーザーおよびグループのみが同期されるようになります。

1. 最新のコードがインストールされていることを確認します。

   * [AEM プラットフォームの更新](https://helpx.adobe.com/jp/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities の更新](/help/communities/deploy-communities.md#latestfeaturepack)

AEM Communitiesでユーザー同期を有効にするには、次の設定が必要です。 Slingコンテンツの配布が失敗するのを防ぐために、これらの設定が正しいことを確認します。

### Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

この設定は、パブリッシャー間で同期されるコンテンツを取得します。 設定はオーサーインスタンス上にあります。 作成者は、そこに存在するすべての発行者と、すべての情報を同期する場所を追跡する必要があります。

設定のデフォルト値は、単一のパブリッシュインスタンス用です。 ユーザー同期は、パブリッシュファームなど複数のパブリッシュインスタンスを同期する場合に役立つので、追加のパブリッシュインスタンスを設定に追加する必要があります。

**コンテンツはどのように同期されますか？**

オーサーインスタンスが、パブリッシャーのエクスポーターエンドポイントにpingを発行します。 特定のパブリッシャー(n)でユーザーが作成または更新されるたびに、オーサーはエクスポーターエンドポイントからコンテンツを取得し、[コンテンツ](/help/communities/sync.md#main-pars-image-1413756164)を他のパブリッシャー(n-1)にプッシュします。

Apache Sling Sync Agents設定を設定するには：

1. AEMオーサーインスタンスで管理者権限でログインします。
1. [Webコンソール](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)にアクセスします。 例えば、[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)のようにします。
1. **Apache Sling Distribution Agent - Sync Agents Factory**&#x200B;を探します。

   * 編集用に開く既存の設定を選択します（鉛筆アイコン）。

      名前の確認：**socialpubsync.**

   * 「**有効**」チェックボックスを選択します。
   * **Use Multiple queuesを選択します。**
   * **エクスポーターエンドポイント**&#x200B;と&#x200B;**インポーターエンドポイント**&#x200B;を指定します（エクスポーターとインポーターエンドポイントを追加できます）。

      これらのエンドポイントは、コンテンツの取得元と、コンテンツのプッシュ先を定義します。 オーサーは、指定されたエクスポーターエンドポイントからコンテンツを取得し、（コンテンツを取得したパブリッシャー以外の）パブリッシャーにコンテンツをプッシュします。
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite Distribution - Encrypted Password Transport Secret Provider {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

作成者は、作成者から発行へのユーザーデータの同期権限を持つ、承認されたユーザーを識別できます。

[許可されたユーザーがすべてのパブリッシュインスタンスで](/help/sites-administering/sync.md#createauthuser)を作成すると、発行者はオーサーと接続し、オーサー上でSling配布を設定できます。 この権限を持つユーザーは、必要な[ACL](/help/sites-administering/sync.md#howtoaddacl)をすべて持っています。

パブリッシャーにデータをインストールする場合、またはパブリッシャーからデータを取得する場合は常に、作成者は、この設定で設定された資格情報（ユーザー名とパスワード）を使用してパブリッシャーに接続します。

認証済みユーザーを使用してオーサーとパブリッシャーを接続するには：

1. AEMオーサーインスタンスで管理者権限でログインします。
1. [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします。

   例えば、[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)のようにします。
1. **Password Granite Distribution - Encrypted Password Transport Secret Providerを探します。**
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   プロパティ&#x200B;**socialpubsync** - **publishUser.**&#x200B;を確認します。

1. ユーザー名とパスワードを[許可されたユーザー](/help/sites-administering/sync.md#createauthorizeduser)に設定します。

   例えば、**usersync - admin**&#x200B;のようにします。

![granite-passwrd-trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

この設定は、パブリッシャー間で同期するデータを設定するために使用します。 **許可されたルート**&#x200B;で指定されたパスでデータが作成/更新されると、「var/community/distribution/diff」がアクティブ化され、作成されたレプリケーターがパブリッシャーからデータを取得して他のパブリッシャーにインストールします。

同期するデータ（ノードパス）を設定するには：

1. オーサーインスタンスで管理者権限でログインします。
1. [Webコンソール](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)にアクセスします。

   例えば、[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)のようにします。

1. **Apache Sling Distribution Agent - Queue Agents Factory**&#x200B;を探します。
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   名前の検証：**socialpubsync -reverse**

1. 「**有効**」チェックボックスを選択して保存します。
1. **許可されたルート**&#x200B;に複製するノードパスを指定します。
1. **パブリッシュ**&#x200B;インスタンスごとにこの手順を繰り返します。

   ![queue-agents-fact](assets/queue-agents-fact.png)

### Adobe Granite Distribution - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

この設定は、パブリッシャー間でグループメンバーシップを同期します。
あるパブリッシャーでグループのメンバーシップを変更しても他のパブリッシャーのメンバーシップが更新されない場合は、**ref :members**&#x200B;が&#x200B;**lookプロパティ名**&#x200B;に追加されていることを確認します。

メンバーの同期を確実に行う手順は、次のとおりです。

1. AEMオーサーインスタンスで管理者権限でログインします。
1. [Webコンソール](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)にアクセスします。

   例えば、[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)のようにします。

1. **AdobeGranite Distribution - Diff Observer Factory**&#x200B;を見つけます。
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   **エージェント名を確認します。socialpubsync -reverse**&#x200B;を使用します。

1. 「**有効**」チェックボックスを選択します。
1. **rep:members**&#x200B;を&#x200B;**lookedプロパティ名**&#x200B;のpropertyNameの説明として指定し、「保存」をクリックします。

   ![diff-obs](assets/diff-obs.png)

### Apache Sling Distribution Trigger - Scheduled Triggers Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

この設定を使用すると、（パブリッシャーがpingを送信し、オーサーによって変更が取り込まれた後の）ポーリング間隔を設定して、パブリッシャー間で変更を同期できます。

作成者は、30秒ごとに発行者をポーリングします（デフォルト）。 フォルダー`/var/sling/distribution/packages/  socialpubsync -  vlt /shared`にパッケージが存在する場合は、それらのパッケージを取得し、他のパブリッシャーにインストールします。

ポーリング間隔を変更するには：

1. AEMオーサーインスタンスで管理者権限でログインします。
1. [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします(例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))。
1. **Apache Sling Distributionトリガー- ScheduledトリガーFactory**&#x200B;を探します。

   * 編集用に開く既存の設定を選択します（鉛筆アイコン）。

      **socialpubsync -scheduled-scheduled-トリガー**&#x200B;を確認します。

   * 間隔（秒）を目的の間隔に設定し、保存します。

   ![scheduled-trigger](assets/scheduled-trigger.png)

### AEM Communities User Sync Listener {#aem-communities-user-sync-listener}

Sling配布で、サブスクリプションとフォローに矛盾がある問題については、**AEM Communities User Sync Listener**&#x200B;設定の次のプロパティが設定されているかどうかを確認します。

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

購読、フォロー、通知を同期するには

各AEMパブリッシュインスタンスで、次の操作を実行します。

1. 管理者権限でサインインします。
1. [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします。 例えば、[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)のようにします。
1. **AEM Communities User Sync Listener**&#x200B;を探します。
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   名前の検証：**socialpubsync -scheduled-トリガー**

1. 次の&#x200B;**NodeTypes**&#x200B;を設定します。

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   このプロパティで指定されたノードタイプが同期され、通知情報（続くブログと設定）が異なるパブリッシャー間で同期されます。

1. **DistributedFolders**&#x200B;に同期するすべてのフォルダーを追加します。 例：

   `segments/scoring`

   `social/relationships`

   `activities`

1. **ignorablenodes**&#x200B;を次のように設定します。

   `.tokens`

   `system`

   `rep:cache` （スティッキーセッションを使用するので、このノードを別のパブリッシャーに同期する必要はありません）。

   ![user-sync-listner](assets/user-sync-listner.png)

### 一意の Sling ID{#unique-sling-id} の節を参照してください 

AEMオーサーインスタンスは、Sling IDを使用して、データの送信元と、パッケージの送り先（または送り先の不要な発行者）を特定します。

パブリッシュファーム内のすべてのパブリッシャーが一意のSling IDを持っていることを確認します。 Sling IDがパブリッシュファーム内の複数のパブリッシュインスタンスに対して同じである場合、ユーザーの同期は失敗します。 作成者は、パッケージの取得元とインストール先を知りません。

パブリッシュファーム内のパブリッシャーの一意のSling IDを確保するには、各パブリッシュインスタンスで次の手順を実行します。

1. [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings)を参照します。
1. **Sling ID**&#x200B;の値を確認します。

   ![slingid](assets/slingid.png)

   あるパブリッシュインスタンスの Sling ID が他のパブリッシュインスタンスの Sling ID と一致する場合は、次のようにします。

1. Sling IDが一致するパブリッシュインスタンスの1つを停止します。
1. `crx-quickstart/launchpad/felix`ディレクトリで、*sling.id.file.*&#x200B;という名前のファイルを探して削除します。

   例えば、Linuxシステムの場合は、次のようになります。

   `rm -i $(find . -type f -name sling.id.file)`

   例えば、Windowsシステムの場合は、次のようになります。

   Windowsエクスプローラーを使用して、`sling.id.file`を検索します。

1. 発行インスタンスを起動します。起動時に、新しいSling IDが割り当てられます。
1. **Sling ID**&#x200B;が一意になったことを検証します。

すべてのパブリッシュインスタンスの Sling ID が一意になるまでこの手順を繰り返します。

### Vault Package Builder Factory  {#vault-package-builder-factory}

更新を正しく同期するには、ユーザ同期用にVaultパッケージビルダを変更する必要があります。
`/home/users`に`*/rep:cache`ノードが作成されます。 これは、ノードのプリンシパル名に対してクエリを実行すると、このキャッシュを直接使用できることを見つけるために使用されるキャッシュです。

`rep :cache`ノードがパブリッシャー間で同期されると、ユーザーの同期が停止する場合があります。

パブリッシャー間で更新が適切に同期されるようにするには、各AEMパブリッシュインスタンスで次の手順を実行します。

1. [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします。

   例えば、[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)のようにします。
1. **Apache Sling Distribution Packaging - Vault Package Builder Factory**&#x200B;を探します。

   ビルダー名：socialpubsync-vlt.

1. 編集アイコンを選択します。
1. 2つのパッケージノードフィルターを追加します。
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. ポリシーの処理
   * 既存のrep :policyノードを新しいノードで上書きするには、3つ目のパッケージフィルターを追加します。`/home/users|+.*/rep:policy`
   * ポリシーの配布を防ぐには、次のように設定します。`Acl Handling: IGNORE`

   ![Vaultパッケージビルダーファクトリ](assets/vault-package-builder-factory.png)

## AEM Communities {#troubleshoot-sling-distribution-in-aem-communities}でのSling配布のトラブルシューティング

Sling配布が失敗した場合は、次のデバッグ手順を試してください。

1. **不適切に追加された [設定を確認する](/help/sites-administering/sync.md#improperconfig)**

   複数の設定を追加または編集せずに、既存のデフォルト設定を編集する必要があります。
1. **設定の確認**

   [ベストプラクティス](/help/communities/sync.md#main-pars-header-863110628)で説明されているように、AEMオーサーインスタンスで[設定](/help/communities/sync.md#bestpractices)がすべて適切に設定されていることを確認します。

1. **承認されたユーザー権限の確認**

   パッケージが正しくインストールされていない場合は、最初のパブリッシュインスタンスで作成された[許可されたユーザー](/help/sites-administering/sync.md#createauthuser)に正しいACLが含まれていることを確認します。

   これを検証するには、[作成した認証済みAdobe](/help/sites-administering/sync.md#createauthuser)の代わりに、オーサーインスタンス上の[ユーザーGranite Distribution - Encrypted Password Transport Secret Provider](/help/sites-administering/sync.md#adobegraniteencpasswrd)の設定を、管理者ユーザーの資格情報を使用するように変更します。 次に、パッケージのインストールを再試行します。 ユーザー同期が管理者の資格情報で正常に機能する場合は、作成されたパブリッシュユーザーに適切なACLがないことを意味します。

1. **差分監視者ファクトリ設定を確認する**

   特定のAdobeのみがパブリッシュファーム全体で同期されない場合（例えば、グループメンバーが同期されない場合）は、[ノードのGranite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver)設定が有効になっていて、**rep:メンバ**&#x200B;は&#x200B;**lookプロパティ名**&#x200B;に設定されます。

1. **AEM Communities User Sync Listenerの設定を確認します。** 作成したユーザーが同期され、サブスクリプションとフォローが機能しない場合は、AEM Communities User Sync Listener設定に次の項目が含まれていることを確認します。

   * ノードタイプ — **rep:User、nt:unstructured**、**nt:resource**、**rep:ACL**、**sling:Folder**、および&#x200B;**sling:OrderedFolder**&#x200B;に設定します。
   * 無視可能なノード — **.tokens**、**system**、**rep :cache**&#x200B;に設定します。
   * [分散フォルダ]：配布するフォルダに設定します。

1. **パブリッシュインスタンスでのユーザー作成時に生成されたログを確認する**

   上記の設定が適切に設定されているにもかかわらずユーザー同期が機能していない場合は、ユーザーの作成時に生成されるログを確認します。

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

1. ユーザーの同期を無効にします。
1. AEMオーサーインスタンスで、管理者権限でログインします。

   1. [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします。 例えば、[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)のようにします。
   1. 設定&#x200B;**Apache Sling Distribution Agent - Sync Agents Factory**&#x200B;を探します。
   1. 「**有効**」チェックボックスの選択を解除します。

      オーサーインスタンスでユーザー同期を無効にすると、（エクスポーターとインポーター）エンドポイントが無効になり、オーサーインスタンスは静的になります。 **vlt**&#x200B;パッケージは、作成者によってpingまたは取得されません。

      ユーザーがパブリッシュインスタンス上で作成された場合、 **vlt**&#x200B;パッケージが&#x200B;*/var/sling/distribution/packages/ socialpubsync - vlt /data*&#x200B;ノードに作成されます。 作成者がこれらのパッケージを別のサービスにプッシュした場合。 このデータをダウンロードして抽出し、他のサービスにプッシュされるすべてのプロパティを確認できます。

1. 投稿者に移動し、投稿者でユーザーを作成します。 その結果、イベントが作成されます。
1. ユーザーの作成時に作成されたログ](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)の[順序を確認します。
1. **vlt**&#x200B;パッケージが&#x200B;**/var/sling/distribution/packages/socialpubsync-vlt/data**&#x200B;に作成されているかどうかを確認します。
1. 次に、AEMオーサーインスタンスでユーザー同期を有効にします。
1. パブリッシャーで、**Apache Sling Distribution Agent - Sync Agents Factory**内のエクスポーターまたはインポーターエンドポイントを変更します。
パッケージデータをダウンロードして抽出し、他のパブリッシャーにプッシュされるすべてのプロパティと、どのデータが失われるかを確認できます。
