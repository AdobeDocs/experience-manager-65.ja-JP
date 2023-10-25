---
title: ユーザー同期
description: AEMでのユーザー同期の内部機能について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Security
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '2502'
ht-degree: 48%

---


# ユーザー同期{#user-synchronization}

## はじめに {#introduction}

デプロイメントが [パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm)のメンバーは、任意のパブリッシュノードにログインして、自分のデータを表示できる必要があります。

パブリッシュ環境で作成されたユーザーとユーザーグループ（ユーザーデータ）は、オーサー環境では必要ありません。

オーサー環境で作成されたほとんどのユーザーデータは、オーサー環境にとどまり、パブリッシュインスタンスにはコピーされません。

1 つのパブリッシュインスタンスでおこなわれた登録と変更を、他のパブリッシュインスタンスと同期して、同じユーザーデータにアクセスできるようにする必要があります。

AEM 6.1 以降では、ユーザーの同期が有効になっている場合、ユーザーデータはファーム内のパブリッシュインスタンス間で自動的に同期され、オーサー環境では作成されません。

## Sling 配布 {#sling-distribution}

ユーザーデータは [ACL](/help/sites-administering/security.md) と共に Oak JCR の下のレイヤーの [Oak Core](/help/sites-deploying/platform.md) に格納され、[Oak API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/oak/api/package-tree.html) を使用してアクセスできます。頻繁に更新されない場合、を使用して他のパブリッシュインスタンスとユーザーデータを同期させるのは妥当です。 [Sling コンテンツ配布](https://github.com/apache/sling-old-svn-mirror/blob/trunk/contrib/extensions/distribution/README.md) （Sling 配布）。

従来のレプリケーションと比較して、Sling 配布を使用してユーザーを同期する利点は次のとおりです。

* *ユーザー*, *ユーザープロファイル*、および *ユーザーグループ* パブリッシュで作成済みは、オーサーで作成されません

* Sling 配布により JCR イベントにプロパティが設定されることで、レプリケーションが無限に繰り返されることなく、パブリッシュ側のイベントリスナーで実行できます
* Sling 配布では、ユーザーデータを非開始のパブリッシュインスタンスにのみ送信するので、不要なトラフィックは不要になります
* ユーザーノードで設定された [ACL](/help/sites-administering/security.md) が同期に含まれます

>[!NOTE]
>
>セッションが必要な場合は、SSO ソリューションかスティッキーセッションのどちらかを使用し、別のパブリッシュインスタンスに切り替えられた場合はユーザーにログインしてもらうことをお勧めします。

>[!CAUTION]
>
>ユーザー同期が有効化されている場合でも、**administrators** グループの同期はサポートされません。代わりに、「差分をインポート」できなかった場合は、エラーログに記録されます。
>
>したがって、デプロイメントがパブリッシュファームの場合、ユーザーが **管理者** グループの作成時に変更を加える場合は、各パブリッシュインスタンスで手動で変更する必要があります。

## ユーザー同期の有効化 {#enable-user-sync}

>[!NOTE]
>
>デフォルトでは、ユーザー同期は `disabled` になっています。
>
>ユーザー同期を有効にするには、OSGi の既存の設定を変更する必要があります&#x200B;*。*
>
>ユーザー同期を有効にした結果、新しい設定が追加されることはありません。

ユーザー同期では、作成者環境でユーザーデータが作成されていない場合でも、ユーザーデータの配布を管理する際に作成者環境が必要となります。 すべての設定はオーサー環境で行われるわけではありませんが、各手順で、オーサー環境とパブリッシュ環境のどちらで実行するかが明確に示されます。

ユーザー同期の有効化に必要な手順と、[トラブルシューティング](#troubleshooting)の節を以下に示します。

### 前提条件 {#prerequisites}

1. ユーザーとユーザーグループが既に 1 つのパブリッシュインスタンス上に作成されている場合は、次の操作を行うことをお勧めします。 [手動同期](#manually-syncing-users-and-user-groups) ユーザー同期を設定して有効にする前に、すべてのパブリッシュインスタンスに対してユーザーデータを送信します。

ユーザー同期を有効にすると、新規に作成されたユーザーおよびグループのみが同期されるようになります。

1. 最新のコードがインストールされていることを確認します。

* [AEM プラットフォームの更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=ja)
* [AEM Communities の更新](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

**ユーザー同期を有効にする**

* **オーサー環境で**

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * `Apache Sling Distribution Agent - Sync Agents Factory` を見つけます。

      * 既存の設定を選択し、編集用に開く（鉛筆アイコン）確認 `name`: **`socialpubsync`**

      * 「`Enabled`」チェックボックスをオンにします
      * 「`Save`」を選択します。

![Apache Sling Distribution Agent](assets/chlimage_1-20.png)

### 2. 承認済みユーザーの作成 {#createauthuser}

**権限の設定**

手順 3 で、許可されたユーザーを使用して、オーサー環境で Sling 配布を設定します。

* **各パブリッシュインスタンスで**

   * 管理者権限でログインします
   * [セキュリティコンソール](/help/sites-administering/security.md)にアクセスします

      * 例： [https://localhost:4503/useradmin](https://localhost:4503/useradmin)

   * ユーザーの作成

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
* ACL エントリを追加するには、 `+` ボタン

   * **プリンシパル**：*ユーザー同期用に作成されたユーザーを検索*
   * **タイプ**：`Allow`
   * **権限**：`jcr:all`
   * **制限** rep:glob: `*/activities/*`
   * 「**OK**」を選択します

* 「**すべて保存**」を選択します

![ACL ウィンドウの追加](assets/chlimage_1-21.png)

関連トピック

* [アクセス権限の管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* トラブルシューティングの節の[応答処理中の操作の例外の変更](#modify-operation-exception-during-response-processing)。

### 3. Adobe Granite Distribution - Encrypted Password Transport Secret Provider {#adobegraniteencpasswrd}

**権限の設定**

承認されたユーザーが、 **`administrators`** ユーザーグループがすべてのパブリッシュインスタンスで作成された場合、許可されたユーザーは、オーサーインスタンスからパブリッシュインスタンスにユーザーデータを同期する権限を持っていると認識される必要があります。

* **作成者**

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * `com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name` を見つけます。
   * 編集用に開くには、既存の設定（鉛筆アイコン）を選択します。確認 `property name`: **`socialpubsync-publishUser`**

   * ユーザー名とパスワードを [認証済みユーザー](#createauthuser) 手順 2 でパブリッシュで作成

      * 例：`usersync-admin`

![暗号化されたパスワードトランスポート秘密鍵プロバイダー](assets/chlimage_1-22.png)

### 4. Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

**ユーザー同期を有効にする**

* **各パブリッシュインスタンスで**:

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * `Apache Sling Distribution Agent - Queue Agents Factory` を見つけます

      * 編集用に開くには、既存の設定（鉛筆アイコン）を選択します。確認 `Name`: `socialpubsync-reverse`

      * 「`Enabled`」チェックボックスをオンにします
      * 「`Save`」を選択します。

   * **繰り返し** 各パブリッシュインスタンスに対して

![Queue Agents Factory](assets/chlimage_1-23.png)

### 5. Adobe Social Sync - Diff Observer Factory {#diffobserver}

**グループ同期の有効化**

* **各パブリッシュインスタンスで**:

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * **`Adobe Social Sync - Diff Observer Factory`** を見つけます

      * 編集用に開くには、既存の設定（鉛筆アイコン）を選択します。

        `agent name` が `socialpubsync-reverse` であることを確認します

      * 「`Enabled`」チェックボックスをオンにします
      * 「`Save`」を選択します。

![Diff Observer Factory](assets/screen-shot_2019-05-24at090809.png)

### 6. Apache Sling Distribution Trigger - Scheduled Triggers Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**（オプション）ポーリング間隔の変更**

デフォルトでは、オーサーは 30 秒ごとに変更をポーリングします。 この間隔を変更するには、以下の手順を実行します。

* **作成者**

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * `Apache Sling Distribution Trigger - Scheduled Triggers Factory` を見つけます。

      * 編集用に開くには、既存の設定（鉛筆アイコン）を選択します。

         * `Name` が `socialpubsync-scheduled-trigger` であることを確認します

      * 「`Interval in Seconds`」に任意の間隔を指定します
      * 「`Save`」を選択します。

![Scheduled Triggers Factory](assets/chlimage_1-24.png)

## 複数のパブリッシュインスタンスの設定 {#configure-for-multiple-publish-instances}

デフォルトの設定は、1 つのパブリッシュインスタンス用です。 ユーザーの同期を有効にする理由は、パブリッシュファームの場合など、複数のパブリッシュインスタンスを同期するためなので、追加のパブリッシュインスタンスを Sync Agents Factory に追加する必要があります。

### 7. Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory-1}

**パブリッシュインスタンスを追加するには：**

* **作成者**

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * `Apache Sling Distribution Agent - Sync Agents Factory` を見つけます。

      * 編集用に開くには、既存の設定（鉛筆アイコン）を選択します。確認 `Name`: `socialpubsync`

![Sync Agents Factory](assets/chlimage_1-25.png)

* **エクスポーターエンドポイント**
各パブリッシュインスタンスには、エクスポーターエンドポイントが必要です。 例えば、パブリッシュインスタンスが 2 つある場合、localhost:4503 と 4504 には、次の 2 つのエントリが存在するはずです。

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **インポーターエンドポイント**
各パブリッシュインスタンスにインポーターエンドポイントが必要です。 例えば、パブリッシュインスタンスが 2 つある場合、localhost:4503 と 4504 には、次の 2 つのエントリが存在するはずです。

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* 「`Save`」を選択します

### 8. AEM Communities User Sync Listener {#aem-communities-user-sync-listener}

**（オプション）追加の JCR ノードの同期**

複数のパブリッシュインスタンス間で同期するカスタムデータがある場合は、次のようにします。

* **各パブリッシュインスタンスで**:

   * 管理者権限でログインします
   * [Web コンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

      * 例：`https://localhost:4503/system/console/configMgr`

   * `AEM Communities User Sync Listener`を見つけます。
   * 編集用に開くには、既存の設定（鉛筆アイコン）を選択します。確認 `Name`: `socialpubsync-scheduled-trigger`

![AEM Communities User Sync Listener](assets/chlimage_1-26.png)

* **ノードタイプ**
これは、同期されるノードタイプのリストです。 sling:Folder 以外のノードタイプをここにリストする必要があります（sling:folder は別に処理されます）。
同期されるノードタイプのデフォルトのリストは次のとおりです。

   * rep:User
   * nt:unstructured
   * nt:resource

* **無視可能なプロパティ**
これは、変更が検出された場合に無視されるプロパティのリストです。 これらのプロパティに対する変更は、他の変更の副作用として ( 同期は常にトリガーレベルにあるので ) 同期される場合がありますが、これらのプロパティに対する変更は、それ自体ではノード同期されません。
無視されるデフォルトのプロパティは次のとおりです。

   * cq:lastModified

* **無視可能なノード**
同期中に無視されるサブパス。 これらのサブパスの下には、いつでも何も同期されません。
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
>2 つ以上のパブリッシュインスタンス間で Sling ID が一致する場合、ユーザーグループの同期は失敗します。

Sling ID がパブリッシュファーム内の複数のパブリッシュインスタンスに対して同じ場合、ユーザーグループは同期されません。

すべての Sling ID の値が異なることを検証するには、各パブリッシュインスタンスで次の手順を実行します。

1. `http://<host>:<port>/system/console/status-slingsettings`を参照してください。
1. **Sling ID** の値を確認します。

![Sling ID の値の確認](assets/chlimage_1-27.png)

パブリッシュインスタンスの Sling ID が他のパブリッシュインスタンスの Sling ID と一致する場合は、次のようになります。

1. 一致する Sling ID を持つパブリッシュインスタンスの 1 つを停止します。
1. crx-quickstart/launchpad/felix ディレクトリで

   * *sling.id.file* という名前のファイルを検索して削除する

      * 例えば、Linux®システムの場合：
        `rm -i $(find . -type f -name sling.id.file)`

      * 例えば、Windows システムの場合、次のようになります。
        `use windows explorer and search for *sling.id.file*`

1. パブリッシュインスタンスを起動します。

   * 起動時に、新しい Sling ID が割り当てられます

1. **Sling ID** が一意であることを確認する

すべてのパブリッシュインスタンスに一意の Sling ID が割り当てられるまで、これらの手順を繰り返します。

## Vault Package Builder Factory {#vault-package-builder-factory}

更新を正しく同期するには、ユーザ同期用に Vault パッケージビルダーを変更する必要があります。

* 各AEMパブリッシュインスタンスで
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

## 各種操作の結果 {#what-happens-when}

### パブリッシュ環境でのユーザーの自己登録またはプロファイルの編集 {#user-self-registers-or-edits-profile-on-publish}

仕様上、パブリッシュ環境で作成されたユーザーとプロファイル（自己登録）は、オーサー環境では表示されません。

トポロジーが[パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm)であり、ユーザー同期が正しく設定されると、Sling 配布を使用して&#x200B;*ユーザー*&#x200B;と&#x200B;*ユーザープロファイル*&#x200B;がパブリッシュファーム間で同期されます。

### セキュリティコンソールを使用してユーザーやユーザーグループが作成される場合 {#users-or-user-groups-are-created-using-security-console}

設計上、パブリッシュ環境で作成されたユーザーデータは、オーサー環境にも反対にも表示されません。

次の場合に [ユーザー管理とセキュリティ](/help/sites-administering/security.md) コンソールは、パブリッシュ環境で新しいユーザーを追加するために使用され、必要に応じて、ユーザー同期は新しいユーザーとそのグループメンバーシップを他のパブリッシュインスタンスと同期します。 また、ユーザー同期は、セキュリティコンソールを使用して作成されたユーザーグループを同期します。

## トラブルシューティング {#troubleshooting}

### ユーザー同期をオフラインにする方法 {#how-to-take-user-sync-offline}

ユーザー同期をオフラインにするには、次の手順に従います。 [パブリッシュインスタンスを削除する](#how-to-remove-a-publish-instance) または [データの手動同期](#manually-syncing-users-and-user-groups)を指定する場合、配布キューは空で静止している必要があります。

配布キューの状態をチェックするには：

* 作成者：

   * [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) を使用する場合

      * `/var/sling/distribution/packages`内で次のエントリを探します

         * `distrpackage_*`という名前パターンを持つフォルダーノード

   * [パッケージマネージャー](/help/sites-administering/package-manager.md)を使用する場合

      * （まだインストールされていない）保留中のパッケージを探します

         * `socialpubsync-vlt*`という名前パターンを持つもの
         * 作成者 `communities-user-admin`

配布キューが空である場合は、ユーザー同期を無効にします。

* 作成者

   * [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory) の「`Enabled`」チェックボックスをオフにします

タスクが完了したら、ユーザー同期を再度有効にします。

* 作成者

   * [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory) の「`Enabled`」チェックボックスをオンにします

### ユーザー同期診断 {#user-sync-diagnostics}

ユーザー同期診断は、設定をチェックして問題の特定を試みるツールです。

作成者の場合は、メインコンソールから **ツール、操作、診断、ユーザー同期診断。**

ユーザー同期診断コンソールを入力するだけで結果が表示されます。

ユーザー同期が有効になっていない場合は、次のように表示されます。

![ユーザー同期診断が有効になっていない警告](assets/chlimage_1-28.png)

#### パブリッシュインスタンスの診断を実行する方法 {#how-to-run-diagnostics-for-publish-instances}

診断をオーサー環境から実行した場合、パス/失敗の結果には [情報] 設定済みのパブリッシュインスタンスのリストを確認するためのセクションを表示しています。

リストには、そのインスタンスの診断を実行する各パブリッシュインスタンスの URL が含まれます。 URL パラメーター `syncUser` が診断の URL に追加され、その値は[手順 2](#createauthuser) で作成した&#x200B;*承認済み同期ユーザー* に設定されています。

**注意**:URL を起動する前に、 *認証済み同期ユーザー* は、既にそのパブリッシュインスタンスにサインインしている必要があります。

![パブリッシュインスタンスの診断](assets/chlimage_1-29.png)

### 正しく追加されていない設定 {#configuration-improperly-added}

ユーザー同期が正しく機能しないのは、主に余分な設定が追加されていることが原因です&#x200B;*。*&#x200B;代わりに、既存のデフォルト設定を&#x200B;*編集*&#x200B;する必要があります。

Web コンソールに表示される、編集されたデフォルトの設定は次のとおりです。複数のインスタンスが表示される場合は、追加の設定を削除してください。

#### （オーサー）1 つの Apache Sling Distribution Agent - Sync Agents Factory {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![Web コンソールの編集済みのデフォルト設定ビュー](assets/chlimage_1-30.png)

#### （オーサー）1 つの Apache Sling Distribution トランスポート資格情報 — ユーザー資格情報に基づく DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![Web コンソールの編集済みのデフォルト設定ビュー](assets/chlimage_1-31.png)

#### （パブリッシュ）1 つの Apache Sling 配布エージェント — Queue Agents Factory {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![Web コンソールの編集済みのデフォルト設定ビュー](assets/chlimage_1-32.png)

#### （公開）1 つのAdobe Social Sync - Diff Observer Factory {#publish-one-adobe-social-sync-diff-observer-factory}

![Web コンソールの編集済みのデフォルト設定ビュー](assets/chlimage_1-33.png)

#### （オーサー）1 つの Apache Sling 配布トリガー — スケジュール済みトリガーファクトリ {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![Web コンソールの編集済みのデフォルト設定ビュー](assets/chlimage_1-34.png)

### 応答処理中の操作の例外の変更 {#modify-operation-exception-during-response-processing}

ログに次の内容が表示される場合：

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

その後その節を検証します [2. 承認済みユーザーの作成](#createauthuser)に正しく従っていることを確認してください。

この節では、すべてのパブリッシュインスタンスに存在する承認済みユーザーを作成し、オーサーの「シークレットプロバイダー」OSGi 設定で識別する方法について説明します。 デフォルトでは、ユーザーは `admin` です。

承認済みユーザーは **`administrators`** ユーザーグループのメンバーにして、そのグループの権限は変更しないでください。

権限を持つユーザーは、すべてのパブリッシュインスタンスに対して、次の権限と制限を明示的に持っている必要があります。

| **path** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | &#42;/activities/&#42; |
| /home/users | X | &#42;/activities/&#42; |
| /home/groups | X | &#42;/activities/&#42; |

を `administrators` グループに属している場合、権限を持つユーザーは、すべてのパブリッシュインスタンスに対して次の権限を持っている必要があります。

| **path** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### ユーザーグループ同期の失敗 {#user-group-sync-failed}

2 つ以上のパブリッシュインスタンス間で Sling ID が一致する場合、ユーザーグループの同期は失敗します。

[9. 一意の Sling ID](#unique-sling-id) の節を参照してください

### ユーザーおよびユーザーグループの手動同期 {#manually-syncing-users-and-user-groups}

* ユーザーとユーザーグループが存在するパブリッシュインスタンス上：

   * [ユーザー同期が有効になっている場合は無効にします](#how-to-take-user-sync-offline)
   * `/home` の[パッケージを作成](/help/sites-administering/package-manager.md#creating-a-new-package)します

      * パッケージの編集時

         * 「フィルター」タブ／フィルターを追加／ルートパス：`/home`
         * 「詳細」タブ／AC の処理：`Overwrite`

   * [パッケージをエクスポート](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)

* 他のパブリッシュインスタンスの場合：

   * [パッケージをインポートします](/help/sites-administering/package-manager.md#installing-packages)

ユーザー同期を設定したり、有効にしたりするには、手順 1（[Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)）に進みます。

### パブリッシュインスタンスが使用できなくなった場合 {#when-a-publish-instance-becomes-unavailable}

パブリッシュインスタンスが使用できなくなった場合、将来オンラインに戻る場合は削除しないでください。 変更はパブリッシュインスタンスのキューに入れられ、オンラインに戻ると、変更が処理されます。

パブリッシュインスタンスがオンラインに戻らない場合、恒久的にオフラインになる場合は、削除する必要があります。キューの構築により、オーサー環境でのディスク容量の使用量が目立つからです。

パブリッシュインスタンスがダウンした場合、オーサーログには次のような例外があります。

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### パブリッシュインスタンスを削除する方法 {#how-to-remove-a-publish-instance}

パブリッシュインスタンスを [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)を指定する場合、配布キューは空で静止している必要があります。

* 作成者：

   * [ユーザー同期をオフラインにする](#how-to-take-user-sync-offline)
   * follow [手順 7](#apache-sling-distribution-agent-sync-agents-factory) 両方のサーバーリストからパブリッシュインスタンスを削除するには：

      * `Exporter Endpoints`
      * `Importer Endpoints`

   * ユーザー同期を再び有効にする

      * [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory) の「`Enabled`」チェックボックスをオンにします
