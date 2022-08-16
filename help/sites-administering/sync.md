---
title: ユーザー同期
seo-title: User Synchronization
description: AEM でのユーザー同期について説明します。
seo-description: Learn about user synchronization in AEM.
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Security
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '2427'
ht-degree: 100%

---

# ユーザー同期{#user-synchronization}

## はじめに {#introduction}

デプロイメントが[パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm)であるとき、メンバーはすべてのパブリッシュノードにログインしてその中のデータを閲覧できる必要があります。

パブリッシュ環境で作成されたユーザーとユーザーグループ（ユーザーデータ）は、オーサー環境では必要ありません。

オーサー環境で作成されたほとんどのユーザーデータはオーサー環境に残るものと想定されており、パブリッシュインスタンスにはコピーされません。

他のパブリッシュインスタンスが同じユーザーデータにアクセスするには、1 つのパブリッシュインスタンスに加えられた登録と変更をそれらのパブリッシュインスタンスに同期する必要があります。

 AEM 6.1 では、ユーザー同期を有効にすると、ユーザーデータがファーム内のパブリッシュインスタンス全体に自動的に同期され、オーサー環境には作成されません。

## Sling 配布 {#sling-distribution}

ユーザーデータは [ACL](/help/sites-administering/security.md) と共に Oak JCR の下のレイヤーの [Oak Core](/help/sites-deploying/platform.md) に格納され、[Oak API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html) を使用してアクセスできます。アップデートの頻度が少ない場合は、[Sling コンテンツ配布](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md)（Sling 配布）を使用してユーザーデータを他のパブリッシュインスタンスに同期するのが適切です。

従来のレプリケーションと比較して、Sling 配布を使用してユーザーを同期する利点は次のとおりです。

* パブリッシュインスタンスで作成された&#x200B;*ユーザー*、*ユーザープロファイル*&#x200B;および&#x200B;*ユーザーグループ*&#x200B;がオーサー環境に作成されません

* Sling 配布により JCR イベントにプロパティが設定されることで、レプリケーションが無限に繰り返されることなく、パブリッシュ側のイベントリスナーで実行できます
* Sling 配布は派生元でないパブリッシュインスタンスにのみユーザーデータを送信するので、不要なトラフィックが発生しません
* ユーザーノードで設定された [ACL](/help/sites-administering/security.md) が同期に含まれます

>[!NOTE]
>
>セッションが必要な場合は、SSO ソリューションか定着セッションを使用して、別のパブリッシャーに切り替わった際にはお客様にログインしてもらうことをお勧めします。

>[!CAUTION]
>
>ユーザー同期が有効化されている場合でも、***administrators*** グループの同期はサポートされません。代わりに、「差分のインポート」が失敗した旨を示すログがエラーログに記録されます。
>
>このため、デプロイメントがパブリッシュファームで、**administrators** グループに対してユーザーが追加または削除された場合、変更は各パブリッシュインスタンスに対して手動で実行する必要があります。

## ユーザー同期の有効化 {#enable-user-sync}

>[!NOTE]
>
>デフォルトでは、ユーザー同期は `disabled` になっています。
>
>ユーザー同期を有効にするには、OSGi の既存の設定を変更する必要があります&#x200B;*。*
>
>ユーザー同期を有効にした結果、新しい設定が追加されることはありません。

ユーザー同期では、オーサー環境で作成されていないユーザーデータでもその配布の管理はオーサー環境に依存します。すべてではありませんが、設定の大多数はオーサー環境にあり、それをオーサー環境またはパブリッシュ環境で実行するかどうかは各手順で明確に識別します。

ユーザー同期の有効化に必要な手順と、[トラブルシューティング](#troubleshooting)の節を以下に示します。

### 前提条件 {#prerequisites}

1. ）1 つのパブリッシャーでユーザーおよびユーザーグループが既に作成されている場合は、ユーザー同期を設定して有効にする前に、ユーザーデータをすべてのパブリッシャーと[手動で同期](#manually-syncing-users-and-user-groups)することをお勧めします。

ユーザー同期を有効にすると、新規に作成されたユーザーおよびグループのみが同期されるようになります。

1. 最新のコードがインストールされていることを確認します。

* [AEM プラットフォームの更新](https://helpx.adobe.com/jp/experience-manager/kb/aem62-available-hotfixes.html)
* [AEM Communities の更新](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

**ユーザー同期の有効化**

* **オーサー環境で**

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * `Apache Sling Distribution Agent - Sync Agents Factory` を見つけます。

      * 編集する既存の設定を選択します（鉛筆アイコン）
検証 `name`：**`socialpubsync`**

      * 「`Enabled`」チェックボックスをオンにします
      * 「`Save`」を選択します。


![](assets/chlimage_1-20.png)

### 2. 承認済みユーザーの作成 {#createauthuser}

**権限の設定**&#x200B;この承認済みユーザーが手順 3 のオーサー環境での Sling 配布の設定に使用されます。

* **各パブリッシュインスタンスで**

   * 管理者権限でログインします
   * [セキュリティコンソール](/help/sites-administering/security.md)にアクセスします

      * 例： [https://localhost:4503/useradmin](https://localhost:4503/useradmin)
   * 新しいユーザーを作成します

      * 例：`usersync-admin`
   * このユーザーを **`administrators`** ユーザーグループに追加します
   * [このユーザーに対する ACL を /home に追加します](#howtoaddacl)

      * `Allow jcr:all` 制限付きで `rep:glob=*/activities/*`



>[!CAUTION]
>
>新しいユーザーを作成する必要があります。
>
>* デフォルトで割り当てられるユーザーは **`admin`** です。
>* `communities-user-admin user.` を使用しないでください。
>


#### ACL の追加方法 {#addacls}

* CRXDE Lite にアクセスします

   * 例： [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* `/home` ノードを選択します
* 右側のペインで「`Access Control`」タブを選択します
* `+` ボタンを選択して、ACL エントリを追加します

   * **プリンシパル**：*ユーザー同期用に作成されたユーザーを検索*
   * **タイプ**：`Allow`
   * **権限**：`jcr:all`
   * **制限** rep:glob: `*/activities/*`
   * 「**OK**」を選択します。

* 「**すべて保存**」を選択します。

![](assets/chlimage_1-21.png)

関連トピック

* [アクセス権限の管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* トラブルシューティングの節の[応答処理中の操作の例外の変更](#modify-operation-exception-during-response-processing)。

### 3. Adobe Granite Distribution - Encrypted Password Transport Secret Provider {#adobegraniteencpasswrd}

**権限の設定**

**`administrators`**ユーザーグループのメンバーである承認済みユーザーがすべてのパブリッシュインスタンスで作成されたら、ユーザーデータをオーサー環境からパブリッシュ環境に同期する権限があるその承認済みユーザーをオーサー環境で識別する必要があります。

* **オーサー環境で**

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name` を見つけます。
   * 編集する既存の設定を選択します（鉛筆アイコン）
検証 `property name`：**`socialpubsync-publishUser`**

   * 手順 2 でパブリッシュ環境で作成した[承認済みユーザー](#createauthuser)のユーザー名とパスワードを設定します

      * 例：`usersync-admin`


![](assets/chlimage_1-22.png)

### 4. Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

**ユーザー同期の有効化**

* **パブリッシュ環境で**：

   * 管理者権限でサインインします。
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * `Apache Sling Distribution Agent - Queue Agents Factory` を見つけます

      * 編集する既存の設定を選択します（鉛筆アイコン）
検証 `Name`：`socialpubsync-reverse`

      * 「`Enabled`」チェックボックスをオンにします
      * 「`Save`」を選択します
   * 各パブリッシュインスタンスで**繰り返します**



![](assets/chlimage_1-23.png)

### 5. Adobe Social Sync - Diff Observer Factory {#diffobserver}

**グループ同期の有効化**

* **各パブリッシュインスタンスで**：

   * 管理者権限でサインインします。
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * **`Adobe Social Sync - Diff Observer Factory`** を見つけます

      * 編集する既存の設定を選択します（鉛筆アイコン）。

         `agent name` が `socialpubsync-reverse` であることを確認します

      * 「`Enabled`」チェックボックスをオンにします
      * 「`Save`」を選択します


![](assets/screen-shot_2019-05-24at090809.png)

### 6. Apache Sling Distribution Trigger - Scheduled Triggers Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**（オプション）ポーリング間隔の変更**

デフォルトでは、オーサー環境では 30 秒ごとに変更をポーリングします。この間隔を変更するには、以下の手順を実行します。

* **オーサー環境で**

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * `Apache Sling Distribution Trigger - Scheduled Triggers Factory` を見つけます

      * 編集する既存の設定を選択します（鉛筆アイコン）。

         * `Name` が `socialpubsync-scheduled-trigger` であることを確認します
      * 「`Interval in Seconds`」に任意の間隔を指定します
      * 「`Save`」を選択します。



![](assets/chlimage_1-24.png)

## 複数のパブリッシュインスタンスの設定 {#configure-for-multiple-publish-instances}

デフォルトの設定は、単一のパブリッシュインスタンス用の設定です。ユーザー同期を有効にする理由は、複数のパブリッシュインスタンス（パブリッシュファーム用になど）を同期することなので、追加のパブリッシュインスタンスを Sync Agents Factory に追加する必要があります。

### 7. Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory-1}

**パブリッシュインスタンスを追加するには：**

* **オーサー環境で**

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * `Apache Sling Distribution Agent - Sync Agents Factory` を見つけます。

      * 編集する既存の設定を選択します（鉛筆アイコン）
検証 `Name`：`socialpubsync`


![](assets/chlimage_1-25.png)

* **Exporter Endpoints**
各パブリッシャーにエクスポーターエンドポイントが必要です。例えば、パブリッシャーが localhost:4503 と 4504 の 2 つの場合、以下の 2 つのエントリが必要です。

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **Importer Endpoints**
各パブリッシャーにインポーターエンドポイントが必要です。例えば、パブリッシャーが localhost:4503 と 4504 の 2 つの場合、次の 2 つのエントリが必要です。

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* 「`Save`」を選択します

### 8. AEM Communities User Sync Listener {#aem-communities-user-sync-listener}

**（オプション）追加の JCR ノードの同期**

複数のパブリッシュインスタンス間で同期するカスタムデータがある場合は、次のようにします。

* **各パブリッシュインスタンスで**：

   * 管理者権限でサインインします。
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：`https://localhost:4503/system/console/configMgr`
   * `AEM Communities User Sync Listener`を見つけます。
   * 編集する既存の設定を選択します（鉛筆アイコン）
次を確認します`Name`：`socialpubsync-scheduled-trigger`


![](assets/chlimage_1-26.png)

* **ノードタイプ** 
同期するノードタイプのリストです。sling:Folder 以外のすべてのノードタイプがここにリストされます（sling:folder は別個に処理されます）。
同期されるノードタイプのデフォルトのリストは次のとおりです。

   * rep:User
   * nt:unstructured
   * nt:resource

* **Ignorable Properties** 
何らかの変更が検出された場合に無視されるプロパティのリストです。これらのプロパティに対する変更は、他の変更の副作用として同期される場合がありますが（同期は常にノードレベルで行われるので）、これらのプロパティに対する変更そのものが同期をトリガーすることはありません。
無視されるデフォルトのプロパティは次のとおりです。

   * cq:lastModified

* **Ignorable Nodes** 
同期中に完全に無視されるサブパスです。このサブパスの下にあるものはどのタイミングでも同期されません。
無視されるデフォルトのノードは次のとおりです。

   * .tokens
   * system

* **Distributed Folders** 
同期が不要であるのでほとんどの sling:Folders は無視されます。数少ない例外を次に示します。
同期されるデフォルトのフォルダーは次のとおりです。

   * segments/scoring
   * social/relationships
   * activities

### 9. 一意の Sling ID {#unique-sling-id}

>[!CAUTION]
>
>2 つ以上のパブリッシュインスタンスで Sling ID が一致すると、ユーザーグループの同期が失敗します。

Sling ID がパブリッシュファームの複数のパブリッシュインスタンスで同じである場合、ユーザーグループは同期されません。

すべての Sling ID の値が異なることを確認するには、各パブリッシュインスタンスで次の手順を実行します。

1. `http://<host>:<port>/system/console/status-slingsettings`を参照してください。
1. **Sling ID** の値を確認します。

![](assets/chlimage_1-27.png)

あるパブリッシュインスタンスの Sling ID が他のパブリッシュインスタンスの Sling ID と一致する場合は、次のようにします。

1. Sling ID が一致するパブリッシュインスタンスの一方を停止する
1. crx-quickstart/launchpad/felix ディレクトリで

   * *sling.id.file* という名前のファイルを検索して削除する

      * 例えば、Linux システムの場合、次のようになります。
         `rm -i $(find . -type f -name sling.id.file)`

      * 例えば、Windows システムの場合、次のようになります。
         `use windows explorer and search for *sling.id.file*`

1. パブリッシュインスタンスを開始する

   * スタートアップ時に新しい Sling ID が割り当てられる

1. **Sling ID** が一意であることを確認する

すべてのパブリッシュインスタンスの Sling ID が一意になるまでこの手順を繰り返します。

## Vault Package Builder Factory {#vault-package-builder-factory}

更新が適切に同期されるようにするには、ユーザー同期用に Vault Package Builder を変更する必要があります。

* 各 AEM パブリッシュインスタンスで
* [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

   * 例：[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* `Apache Sling Distribution Packaging - Vault Package Builder Factory`を見つけます。 

   * `Builder name: socialpubsync-vlt`

* 編集アイコンを選択します。
* 2 つを追加 `Package Node Filters`：

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* ポリシーの処理：

   * 既存の rep:policy ノードを新しいノードで上書きするには、3 つ目のパッケージフィルターを追加します

      * `/home/users|+.*/rep:policy`
   * ポリシーが配布されないようにするには、次のように設定します

      * `Acl Handling:` `IGNORE`


![Vault Package Builder Factory](assets/vault-package-builder-factory.png)

## 特定状況での動作 {#what-happens-when}

### ユーザーがパブリッシュ環境でプロファイルを自身で登録または編集する場合 {#user-self-registers-or-edits-profile-on-publish}

仕様上、パブリッシュ環境で作成されたユーザーとプロファイル（自己登録）は、オーサー環境では表示されません。

トポロジが[パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm)であり、ユーザー同期が正しく設定されると、Sling 配布を使用して*ユーザー*と&#x200B;*ユーザープロファイル*&#x200B;がパブリッシュファーム間で同期されます。

### セキュリティコンソールでのユーザーまたはユーザーグループの作成 {#users-or-user-groups-are-created-using-security-console}

仕様上、パブリッシュ環境で作成されたユーザーデータは、オーサー環境では表示されません。その反対も同様です。

[ユーザー管理およびセキュリティ](/help/sites-administering/security.md)コンソールを使用してパブリッシュ環境で新しいユーザーを追加すると、ユーザーの同期機能により、新しいユーザーとそのグループメンバーシップがその他のパブリッシュインスタンスに同期されます（必要な場合）。ユーザー同期により、セキュリティコンソールによって作成されたユーザーグループも同期されます。

## トラブルシューティング {#troubleshooting}

### ユーザー同期をオフラインにする方法 {#how-to-take-user-sync-offline}

[パブリッシャーを削除](#how-to-remove-a-publisher)したり、[データを手動で同期](#manually-syncing-users-and-user-groups)したりするためにユーザー同期をオフラインにするには、配布キューが空であり、静止している必要があります。

配布キューの状態をチェックするには：

* オーサー環境で:

   * [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) を使用する場合

      * `/var/sling/distribution/packages`内で次のエントリを探します

         * `distrpackage_*`という名前パターンを持つフォルダーノード
   * [パッケージマネージャー](/help/sites-administering/package-manager.md)を使用する場合

      * （まだインストールされていない）保留中のパッケージを探します

         * `socialpubsync-vlt*`という名前パターンを持つもの
         * 作成者 `communities-user-admin`


配布キューが空である場合は、ユーザー同期を無効にします。

* オーサー環境で

   * [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory) の「`Enabled`」チェックボックスをオフにします

タスク完了後にユーザー同期を再び有効にするには：

* オーサー環境で

   * [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory) の「`Enabled`」チェックボックスをオンにします

### ユーザー同期診断 {#user-sync-diagnostics}

ユーザー同期診断は、設定をチェックして問題の特定を試みるツールです。

オーサー環境で、メインコンソールから&#x200B;**ツール／操作／診断／ユーザー同期診断**&#x200B;の順に移動します。

結果はユーザー同期診断コンソールに表示されます。

ユーザー同期が有効になっていない場合は、次のように表示されます。

![](assets/chlimage_1-28.png)

#### パブリッシャーに対する診断の実行方法 {#how-to-run-diagnostics-for-publishers}

診断がオーサー環境から実行された場合は、成否の結果に[情報]セクションが含まれています。このセクションには、設定済みのパブリッシュインスタンスのリストが確認用に表示されます。

このリストには、診断が実行される各パブリッシュインスタンスの URL が記載されています。URL パラメーター `syncUser` が診断の URL に追加され、その値は[手順 2](#createauthuser) で作成した&#x200B;*承認済み同期ユーザー* に設定されています。

**注意**：URL を起動するには、*承認済み同期ユーザー*&#x200B;がそのパブリッシュインスタンスに既にログインしている必要があります。

![](assets/chlimage_1-29.png)

### 正しく追加されていない設定 {#configuration-improperly-added}

ユーザー同期が正しく機能しないのは、主に余分な設定が追加されていることが原因です&#x200B;*。*&#x200B;代わりに、既存のデフォルト設定を&#x200B;*編集*&#x200B;する必要があります。

Web コンソールに表示される、編集されたデフォルトの設定は次のとおりです。複数のインスタンスが表示される場合は、追加の設定を削除してください。

#### （オーサー）Apache Sling Distribution Agent - Sync Agents Factory 1 つ {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![](assets/chlimage_1-30.png)

#### （オーサー）Apache Sling Distribution トランスポート認証情報 - ユーザ認証情報に基づく DistributionTransportSecretProvider 1 つ {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![](assets/chlimage_1-31.png)

#### （パブリッシュ）Apache Sling Distribution Agent - Queue Agents Factory 1 つ {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![](assets/chlimage_1-32.png)

#### （パブリッシュ）Adobe Social Sync - Diff Observer Factory 1 つ {#publish-one-adobe-social-sync-diff-observer-factory}

![](assets/chlimage_1-33.png)

#### （オーサー）Apache Sling Distribution Trigger - Scheduled Triggers Factory 1 つ {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![](assets/chlimage_1-34.png)

### 応答処理中の操作の例外の変更 {#modify-operation-exception-during-response-processing}

ログに次の内容が表示される場合：

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

その後その節を検証します [2.承認済みユーザーの作成](#createauthuser)に正しく従っていることを確認してください。

この節では、すべてのパブリッシュインスタンスに存在する承認済みユーザーを作成し、それらをオーサー環境の「秘密鍵プロバイダー」OSGi 設定で特定する方法について説明します。デフォルトでは、ユーザーは `admin` です。

承認済みユーザーは **`administrators`** ユーザーグループのメンバーにして、そのグループの権限は変更しないでください。

承認済みユーザーは、すべてのパブリッシュインスタンスに対する次の権限および制限を明示的に保持している必要があります。

| **path** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | &#42;/activities/&#42; |
| /home/users | X | &#42;/activities/&#42; |
| /home/groups | X | &#42;/activities/&#42; |

承認済みユーザーは、`administrators` グループのメンバーであるので、すべてのパブリッシュインスタンスに対する次の権限があります。

| **パス** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### ユーザーグループ同期の失敗 {#user-group-sync-failed}

2 つ以上のパブリッシュインスタンスで Sling ID が一致すると、ユーザーグループの同期が失敗します。

[9.一意の Sling ID](#unique-sling-id) の節を参照してください

### ユーザーおよびユーザーグループの手動同期 {#manually-syncing-users-and-user-groups}

* ユーザーおよびユーザーグループが存在するパブリッシャーで：

   * [ユーザー同期が有効になっている場合は無効にします](#how-to-take-user-sync-offline)
   * `/home` の[パッケージを作成](/help/sites-administering/package-manager.md#creating-a-new-package)します

      * パッケージの編集時

         * 「フィルター」タブ／フィルターを追加／ルートパス：`/home`
         * 「詳細」タブ／AC の処理：`Overwrite`
   * [パッケージをエクスポート](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)


* その他のパブリッシュインスタンスで：

   * [パッケージをインポートします](/help/sites-administering/package-manager.md#installing-packages)

ユーザー同期を設定したり、有効にしたりするには、手順 1（[Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)）に進みます。

### パブリッシャーが使用不能になった場合 {#when-a-publisher-becomes-unavailable}

パブリッシュインスタンスが使用不能になっても、今後オンラインに戻る場合は削除しないでください。パブリッシャーに対する変更はキューに入れられ、パブリッシャーがオンラインに戻った時点で処理されます。

パブリッシュインスタンスがオンラインに戻ることがない場合や永続的にオフラインのままである場合は、削除する必要があります。そのままにしておくと、キューの蓄積によってオーサー環境のディスク使用量が著しく増加します。

パブリッシャーが停止した場合、オーサー環境のログに次のような例外が記録されます。

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### パブリッシャーの削除方法 {#how-to-remove-a-publisher}

[Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory) からパブリッシャーを削除するには、配布キューが空であり、静止している必要があります。

* オーサー環境で：

   * [ユーザー同期をオフラインにする](#how-to-take-user-sync-offline)
   * [手順 7](#apache-sling-distribution-agent-sync-agents-factory)に従って、次の両方のサーバーリストからパブリッシャーを削除します。

      * `Exporter Endpoints`
      * `Importer Endpoints`
   * ユーザー同期を再び有効にする

      * [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory) の「`Enabled`」チェックボックスをオンにします
