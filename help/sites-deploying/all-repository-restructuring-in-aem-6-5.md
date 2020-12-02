---
title: AEM 6.5 における共通リポジトリの再構築
seo-title: AEM 6.5 における共通リポジトリの再構築
description: AEM のすべての領域に共通な、AEM 6.5 の新しいリポジトリ構造への移行に必要な変更を加える方法について学びます。
seo-description: AEM のすべての領域に共通な、AEM 6.5 の新しいリポジトリ構造への移行に必要な変更を加える方法について学びます。
uuid: a4bb64e5-387b-4084-9258-54e68db12f3b
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 80bd707f-c02d-4616-9b45-90f6c726abea
translation-type: tm+mt
source-git-commit: 6396660b642fd78ac7f311fa416efe0e0d52a9e3
workflow-type: tm+mt
source-wordcount: '2721'
ht-degree: 75%

---


# AEM 6.5 における共通リポジトリの再構築 {#common-repository-restructuring-in-aem}

AEM 6.5](/help/sites-deploying/repository-restructuring.md)の親ページ[リポジトリの再構築に関する説明に従って、AEM 6.5にアップグレードしたお客様は、このページを使用して、リポジトリの変更に関連する作業量を評価し、すべてのソリューションに影響を与える可能性があります。 一部の変更ではAEM 6.5のアップグレードプロセス中に作業が必要になり、残りの変更は将来のアップグレードまで延期できます。

**6.5 へのアップグレード時におこなう変更**

* [ContextHub 設定](#contexthub-6.5)
* [ワークフローインスタンス](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-instances)
* [ワークフローモデル](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-models)
* [ワークフローランチャー](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-launchers)
* [ワークフロースクリプト](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-scripts)

**今後のアップグレードの前**

* [ContextHub 設定](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#contexthub-configurations)
* [クラシッククラウドサービスデザイン](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-cloud-services-designs)
* [クラシックダッシュボードデザイン](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-dashboards-designs)
* [クラシックレポートデザイン](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#classic-reports-designs)
* [デフォルトデザイン](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#default-designs)
* [Adobe DTM JavaScript エンドポイント](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-javascript-endpoint)
* [Adobe DTM Web-Hook エンドポイント](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#adobe-dtm-web-hook-endpoint)
* [インボックスタスク](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#inbox-tasks)
* [Multi-site Manager のブループリント設定](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#multi-site-manager-blueprint-configurations)
* [AEM プロジェクトダッシュボードガジェット設定](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#aem-projects-dashboard-gadget-configurations)
* [レプリケーション通知電子メールテンプレート](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#replication-notification-e-mail-template)
* [タグ](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)
* [翻訳 Cloud Services](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-cloud-services)
* [翻訳言語](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-languages)
* [翻訳ルール](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-rules)
* [翻訳 Widget クライアントライブラリ](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#translation-widget-client-library)
* [ツリー Activation Web コンソール](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tree-activation-web-console)
* [ベンダー翻訳コネクタクラウドサービス](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#vendor-translation-connector-cloud-services)
* [ワークフロー通知電子メールテンプレート](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

## 6.5 へのアップグレード時におこなう変更 {#with-upgrade}

### ContextHub 設定 {#contexthub-6.5}

AEM 6.4 以降、デフォルトの ContextHub 設定は用意されていません。したがって、サイトのルートレベルでは、使用する構成を示す`cq:contextHubPathproperty`を設定する必要があります。

1. サイトのルートに移動します。
1. ルートページのページのプロパティを開き、「パーソナライズ機能」タブを選択します。
1. 「ContextHub のパス」フィールドに、独自の ContextHub の設定パスを入力します。

また、ContextHub設定では、絶対値ではなく相対値に更新する必要があります。`sling:resourceType`

1. CRX DE LiteでContextHub設定ノードのプロパティを開きます(例：`/apps/settings/cloudsettings/legacy/contexthub`
1. `sling:resourceType`を`/libs/granite/contexthub/cloudsettings/components/baseconfiguration`から`granite/contexthub/cloudsettings/components/baseconfiguration`に変更

ContextHub 設定の `sling:resourceType` は、絶対パスではなく相対パスであることが必要です。

### ワークフローモデル {#workflow-models}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/workflow/models</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/workflow/models</code></p> <p><code>/conf/global/settings/workflow/models</code></p> <p><code>/var/workflow/models</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新規または変更されたワークフローモデルは、/conf/global/workflow/models に移行する必要があります。</p>
    <ol>
     <li>変更したワークフローモデルをローカルの AEM 6.4 開発インスタンスにデプロイし、以前の場所に存在するようにします。</li>
     <li>AEM のツール／ワークフロー／モデルで、AEM のワークフローモデルエディターを使用してワークフローモデルを編集します。</li>
     <li>変更された AEM 提供のワークフローモデルを移行する場合
      <ol>
       <li>ワークフローモデルエディターを開いて、ブラウザのアドレス URL を変更し、パスセグメント /libs/settings/workflow/models を /etc/workflow/models に置き換えます。
        <ul>
         <li>例えば、次のように変更します。<em>http://localhost:4502/editor.html<strong>/libs/settings/workflow/models</strong>/dam/update_asset.html</em><em>http://localhost:4502/editor.html<strong>/etc/workflow/models</strong>/dam/update_asset.html</em></li>
        </ul> </li>
      </ol> </li>
     <li>ワークフローモデルエディターで編集モードを有効にします。ワークフローモデル定義が /conf/global/workflow/models にコピーされます。</li>
     <li>「同期」ボタンをタップして、/var/workflow/models 下のランタイムワークフローモデルへの変更を同期します。</li>
     <li>ワークフローモデル（/conf/global/workflow/models/&lt;workflow-model&gt;）とランタイムワークフローモデル（/var/workflow/models/&lt;workflow-model&gt;）両方をエクスポートし、AEM プロジェクトに統合します。
      <ol>
       <li>例えば、次のようにエクスポートします。
        <ul>
         <li><code>/config/settings/workflow/models/dam/my_workflow_model</code> および </li>
         <li><code>/var/workflow/models/dam/my_workflow_model</code></li>
        </ul> </li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>ワークフローモデルの解決は次の順序でおこなわれます。</p>
    <ol>
     <li><code>/conf/global/settings/workflow/models</code></li>
     <li><code>/libs/settings/workflow/models</code></li>
     <li><code>/etc/workflow/models</code></li>
    </ol> <p>したがって、以前の場所に保存されていた AEM 提供のワークフローモデルのカスタマイズを保持する場合は /conf/global/settings/workflow/models に移動する必要があります。それ以外の場合は /libs/settings/workflow/models で定義される AEM 提供のワークフローモデルに置き換えられます。</p> </td>
  </tr>
 </tbody>
</table>

### ワークフローインスタンス {#workflow-instances}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/var/workflow/instances</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しい場所に合わせるための操作は必要ありません。</p> <p>古いワークフローインスタンスは安全に以前の場所に存在し続け、新しいワークフローインスタンスは新しい場所に作成されます。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>でのすべての明示的なパス参照
    「前の場所」の<code>
     custom
    </code>コードでは、「新しい場所」も考慮に入れる必要があります。 このコードは AEM Workflow API を使用するようにリファクタリングすることをお勧めします。</td>
  </tr>
 </tbody>
</table>

### ワークフローランチャー {#workflow-launchers}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/workflow/launcher/config</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/workflow/launcher/config</code></p> <p><code>/conf/global/settings/workflow/launcher/config</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しい、または変更されたワークフローランチャーは<code>/conf/global/workflow/launcher/config</code>に移行する必要があります。</p>
    <ol>
     <li>新しいまたは変更したワークフローランチャーの設定を「前の場所」から「新しい場所」(<code>/conf/global</code>)にコピーします。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>ワークフローランチャーの解決は、次の順序でおこなわれます。</p>
    <ol>
     <li><code>/conf/global/settings/workflow/launcher</code></li>
     <li><code>/libs/settings/workflow/launcher</code></li>
     <li><code>/etc/workflow/launcher</code></li>
    </ol> <p>したがって、前の場所に残っているAEM提供のワークフローランチャーのカスタマイズを維持する場合は、新しい場所(<code>/conf/global/settings/workflow/launcher</code>)に移動する必要があります。そうでない場合は、<code>/libs/settings/workflow/launcher</code>のAEM提供のワークフローランチャー定義に置き換えられます。</p> </td>
  </tr>
 </tbody>
</table>

### ワークフロースクリプト {#workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/workflow/scripts</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/workflow/scripts</code></p> <p><code>/apps/workflow/scripts</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新規または変更されたワークフロースクリプトを新しい場所に移行し、新しい場所を反映するように参照先ワークフローモデルを更新する必要があります。</p>
    <ol>
     <li>新規または変更されたワークフロースクリプトを以前の場所から新しい場所にコピーします。<br />
      <ul>
       <li><code>/apps/workflow/scripts</code> は、SCMで維持する必要があります。</li>
      </ul> </li>
     <li>ワークフローモデルの以前の場所にある、ワークフロースクリプトへの参照を更新し、新しい場所を指すようにします。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>AEM 6.4 SP1は、リリース時に、6.5まで再構築を延期できるようにします。
     <code>
      upgrade
     </code>.</p> <p>AEM 6.4 SP1 がリリースされる前に AEM 6.4 にアップグレードする場合、この再構築はアップグレードプロジェクトの一環として実行する必要があります。そうしない場合、以前の場所にあるスクリプトを参照するワークフローステップを編集して保存すると、ワークフローステップからワークフロースクリプト参照が完全に削除され、スクリプト選択ドロップダウンでは新しい場所にあるワークスクリプトのみが使用できるようになります。</p> </td>
  </tr>
 </tbody>
</table>

## 将来のアップグレードの前{#prior-to-upgrade}

### ContextHub 設定 {#contexthub-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/cloudsettings</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/cloudsettings</code></p> <p><code>/conf/global/settings/cloudsettings</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudsettings</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新規または変更された ContextHub 設定はすべて新しい場所に移行する必要があり、参照元の AEM Sites ページは新しい場所を反映するように更新する必要があります。</p>
    <ol>
     <li>新規または変更された ContextHub 設定を以前の場所から新しい場所にコピーします。</li>
     <li>該当する AEM 設定を AEM コンテンツ階層と関連付けます。
      <ol>
       <li><strong>「AEM Sites／ページ／ページのプロパティ／詳細タブ／クラウド設定」を使用した AEM Sites のページ階層</strong>。</li>
      </ol> </li>
     <li>前述の AEM コンテンツ階層から、移行された従来の ContextHub 設定をすべて解除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### クラシッククラウドサービスデザイン  {#classic-cloud-services-designs}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/designs/cloudservices</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/wcm/designs/cloudservices</code></p> <p><code>/apps/settings/wcm/designs/cloudservices</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>SCM で管理されており、実行時にデザインダイアログから書き込まれていないデザインの場合：</p>
    <ol>
     <li>前の場所のデザインを新しい場所(<code>/apps</code>)にコピーします。</li>
     <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"> を使用して、デザイン内の CSS、JavaScript、静的リソースを</a>クライアントライブラリ<code>allowProxy = true</code>に変換します。</li>
     <li><span class="code">の前の場所への参照を更新
       <code>
        cq
       </code>:
       <code>
        designPath
       </code></span>プロパティ。</li>
     <li>以前の場所を参照しているページを更新して、新規のクライアントライブラリカテゴリを使用します（これにはページ実装コードの更新が必要です）。</li>
     <li>/etc.clientlibs/.. プロキシサーブレットを介したクライアントライブラリの提供を許可するように AEM Dispatcher のルールを更新します。</li>
    </ol> <p>SCM で管理されていない、デザインダイアログでランタイムを変更したデザイン。</p>
    <ul>
     <li><code>/etc</code>の外にオーサリング可能なデザインを移動しないでください。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### クラシックダッシュボードデザイン  {#classic-dashboards-designs}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/designs/dashboards</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/wcm/designs/dashboards</code></p> <p><code>/apps/settings/wcm/designs/dashboards</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>SCM で管理されており、実行時にデザインダイアログから書き込まれていないデザインの場合：</p>
    <ol>
     <li>デザインを以前の場所から新しい場所（/apps）にコピーします。</li>
     <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"> を使用して、デザイン内の CSS、JavaScript、静的リソースを</a>クライアントライブラリ<code>allowProxy = true</code>に変換します。</li>
     <li>Folio Builder
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>プロパティ。</li>
     <li>以前の場所を参照しているページを更新して、新規のクライアントライブラリカテゴリを使用します（これにはページ実装コードの更新が必要です）。</li>
     <li>/etc.clientlibs/.. プロキシサーブレットを介したクライアントライブラリの提供を許可するように AEM Dispatcher のルールを更新します。</li>
    </ol> <p>SCM で管理されていない、デザインダイアログでランタイムを変更したデザイン。</p>
    <ul>
     <li><code>/etc</code>の外にオーサリング可能なデザインを移動しないでください。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### クラシックレポートデザイン  {#classic-reports-designs}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/designs/reports</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/wcm/designs/reports</code></p> <p><code>/apps/settings/wcm/designs/reports</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>SCM で管理されており、実行時にデザインダイアログから書き込まれていないデザインの場合：</p>
    <ol>
     <li>デザインを以前の場所から新しい場所（/apps）にコピーします。</li>
     <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"> を使用して、デザイン内の CSS、JavaScript、静的リソースを</a>クライアントライブラリ<code>allowProxy = true</code>に変換します。</li>
     <li>Folio Builder
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>プロパティ。</li>
     <li>以前の場所を参照しているページを更新して、新規のクライアントライブラリカテゴリを使用します（これにはページ実装コードの更新が必要です）。</li>
     <li>/etc.clientlibs/.. プロキシサーブレットを介したクライアントライブラリの提供を許可するように AEM Dispatcher のルールを更新します。</li>
    </ol> <p>SCM で管理されていない、デザインダイアログでランタイムを変更したデザイン。</p>
    <ul>
     <li><code>/etc</code>の外にオーサリング可能なデザインを移動しないでください。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### デフォルトデザイン {#default-designs}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/designs/default</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/wcm/designs/default</code></p> <p><code>/apps/settings/wcm/designs/default</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>SCM で管理されており、実行時にデザインダイアログから書き込まれていないデザインの場合：</p>
    <ol>
     <li>デザインを以前の場所から新しい場所（/apps）にコピーします。</li>
     <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"> を使用して、デザイン内の CSS、JavaScript、静的リソースを</a>クライアントライブラリ<code>allowProxy = true</code>に変換します。</li>
     <li>Folio Builder
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>プロパティ。</li>
     <li>以前の場所を参照しているページを更新して、新規のクライアントライブラリカテゴリを使用します（これにはページ実装コードの更新が必要です）。</li>
     <li>/etc.clientlibs/.. プロキシサーブレットを介したクライアントライブラリの提供を許可するように AEM Dispatcher のルールを更新します。</li>
    </ol> <p>SCM で管理されていない、デザインダイアログでランタイムを変更したデザイン。</p>
    <ul>
     <li><code>/etc</code>の外にオーサリング可能なデザインを移動しないでください。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### Adobe DTM JavaScript エンドポイント  {#adobe-dtm-javascript-endpoint}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/clientlibs/dtm</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/var/cq/dtm/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>アクションは必要ありません。</p> <p>公開されている以前の場所は、プライベートの新しい場所のプロキシエンドポイントとして機能します。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### Adobe DTM Web-Hook エンドポイント  {#adobe-dtm-web-hook-endpoint}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/dtm-hook</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/var/cq/dtm/web-hook</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>アクションは必要ありません。</p> <p>公開されている以前の場所は、プライベートの新しい場所のプロキシエンドポイントとして機能します。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### インボックスタスク  {#inbox-tasks}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/var/taskmanagement</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><strong>インボックスのパージメンテナンスタスク</strong>を使用して、必要に応じて以前の場所から古いタスクを削除します。</td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>タスクを新しい場所に移行するための操作は必要ありません。</p>
    <ul>
     <li>以前の場所にあるタスクは引き続き使用でき、機能します。</li>
     <li>新しい場所に新しいタスクが作成されます。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Multi-site Manager のブループリント設定  {#multi-site-manager-blueprint-configurations}

<table>
 <tbody>
  <tr>
   <td><strong><em></em>以前の場所</strong></td>
   <td><code>/etc/blueprints</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/msm</code></p> <p><code>/apps/msm</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td>
    <ol>
     <li>カスタム設定を<code>/etc/blueprints</code>から<code>/apps/msm</code>にコピーします。</li>
     <li>削除 <code>/etc/blueprints</code>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### AEM プロジェクトダッシュボードガジェット設定  {#aem-projects-dashboard-gadget-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/projects/dashboard/gadgets</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/cq/core/content/projects/dashboard/gadgets</code></p> <p><code>/apps/cq/core/content/projects/dashboard/gadgets</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しい、または変更されたAEMプロジェクトダッシュボードガジェットの構成は、新しい場所(<code>/apps</code>)に移行する必要があります。</p>
    <ol>
     <li>新しいまたは変更されたAEMプロジェクトダッシュボードガジェット構成を、前の場所から新しい場所(<code>/apps</code>)にコピーします。
      <ol>
       <li>変更されていないAEMプロジェクトダッシュボードガジェットの構成は、新しい場所(<code>/libs</code>)に存在するので、コピーしないでください。</li>
      </ol> </li>
     <li>以前の場所を参照する AEM プロジェクトテンプレートを適切な新しい場所を指すように更新します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>AEM 6.4 互換パッケージが適用されている場合は、互換パッケージの削除時にリポジトリ調整アクティビティを実行する必要があります。</td>
  </tr>
 </tbody>
</table>

### レプリケーション通知電子メールテンプレート  {#replication-notification-e-mail-template}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/notification/email/default/com.day.cq.replication</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/notification-templates/com.day.cq.replication</code></p> <p><code>/apps/settings/notification-templates/com.day.cq.replication</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しい、または変更されたレプリケーション通知電子メールテンプレートは、新しい場所(<code>/apps</code>)に移行する必要があります。</p>
    <ol>
     <li>新しいまたは変更されたレプリケーション通知電子メールテンプレートを、前の場所から新しい場所(<code>/apps</code>)にコピーします。</li>
     <li>移行されたすべてのレプリケーション通知電子メールテンプレートを以前の場所から削除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>サポートされている唯一の新規レプリケーション通知電子メールテンプレートは、新しいロケールをサポートするものです。</p> <p>レプリケーション通知電子メールテンプレートの解決は次の順序でおこなわれます。</p>
    <ol>
     <li><code>/etc/notification/email/default/com.day.cq.replication</code></li>
     <li><code class="code">/apps/settings/notification-templates/com.day.cq.replication
        </code></li>
     <li><code>/libs/settings/notification-templates/com.day.cq.replication</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### タグ {#tags}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/tags</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/content/cq:tags</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>すべてのタグは<code>/content/cq:tags</code>に移行する必要があります。</p>
    <ol>
     <li>以前の場所から新しい場所にすべてのタグをコピーします。</li>
     <li>以前の場所からすべてのタグを削除します。</li>
     <li>AEM Webコンソールから、<em>https://serveraddress:serverport/system/console/bundles/com.day.cq.cq-tagging</em>にあるDay Communique 5 Tagging OSGiバンドルを再起動し、AEMが「New Location contains」のコンテンツを認識できるようにします。このOSGiバンドルは使用する必要があります。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>Day Communique Tagging OSGi バンドルを再起動しても、以前の場所が空であれば、新しい場所がタグのルートとして登録されるだけです。</p> <p>AEM の TagManager API を活用シてタグを解決するすべての機能については、新しい場所に移行した後も、以前の場所への参照は引き続き機能します。</p> <p>パス<code>/etc/tags</code>を明示的に参照するカスタムコードは、<span class="code">/content/に更新する必要があります
      <code>
       cq
      </code>
      <code>
       :tags
      </code></span>を使用するか、または、この移行と連携してTagManager Java APIを利用できるように書き換えます。</p> </td>
  </tr>
 </tbody>
</table>

### 翻訳 Cloud Services {#translation-cloud-services}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/cloudservices/translation</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/apps/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/global/settings/cloudconfigs/translation/translationcfg</code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/translationcfg</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しい翻訳Cloud Servicesは、新しい場所(<code>/apps</code>、<code>/conf/global</code>、<code>/conf/&lt;tenant&gt;</code>)に移行する必要があります。</p>
    <ol>
     <li>以前の場所にある既存の設定を新しい場所に移行します。
      <ul>
       <li><strong>ツール／クラウドサービス／翻訳クラウドサービス</strong>の AEM オーサリング UI を使用して、新規の翻訳クラウドサービス設定を手動で再作成します。<br /> または </li>
       <li>新しい翻訳Cloud Servicesの設定を「前の場所」から「新しい場所」(<code>/apps</code>、<code>/conf/global</code>、<code>/conf/&lt;tenant&gt;</code>)にコピーします。</li>
      </ul> </li>
     <li>該当する AEM 設定を AEM コンテンツ階層と関連付けます。
      <ol>
       <li>「<strong>AEM Sites／ページ／ページのプロパティ／詳細タブ／クラウド設定</strong>」を使用した AEM Sites のページ階層。</li>
       <li>「<strong>AEM エクスペリエンスフラグメント／エクスペリエンスフラグメント／プロパティ／クラウドサービスタブ／クラウド設定</strong>」を使用した AEM エクスペリエンスフラグメント階層。</li>
       <li>「<strong>AEM エクスペリエンスフラグメント／フォルダー／プロパティ／クラウドサービスタブ／クラウド設定</strong>」を使用した AEM エクスペリエンスフラグメントフォルダー階層。<br /> </li>
       <li><strong>AEM Assets/フォルダー/Cloud Servicesーのプロパティ/フォルダータブ/設定</strong>を介したAEM Assetsフォルダー階層。</li>
       <li><strong>AEMプロジェクト/プロジェクト/プロジェクトのプロパティ/詳細タブ/クラウドの設定</strong>を介したAEMプロジェクト。</li>
      </ol> </li>
     <li>前述の AEM コンテンツ階層から、移行された従来の翻訳クラウドサービスとの関連付けをすべて解除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>翻訳クラウドサービスの解決は次の順序でおこなわれます。</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/translationcfg</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/translationcfg</code></li>
    </ol> <p>移行された翻訳クラウドサービスはAEM 6.4 と互換性がある必要があります。</p> </td>
  </tr>
 </tbody>
</table>

### 翻訳言語  {#translation-languages}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/translation/supportedLanguages</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/translation/supportedLanguages</code></p> <p><code>/apps/settings/translation/supportedLanguages</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しいまたは変更された翻訳言語の定義では、すべての翻訳言語の定義を新しい場所(<code>/apps</code>)に移行する必要があります。</p>
    <ol>
     <li>翻訳言語の定義に追加や変更が行われた場合は、前の場所のすべての翻訳言語の定義を新しい場所(<code>/apps</code>)にコピーします。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>翻訳言語のパス解決は次の順序でおこなわれます。</p>
    <ol>
     <li><code>/etc/translation/supportedLanguages</code></li>
     <li><code>/apps/settings/translation/supportedLanguage</code></li>
     <li><code>/libs/settings/translation/supportedLanguages</code></li>
    </ol> <p>この解決方法はマージオーバーレイをサポートしていません。つまり、解決されたパスにはすべてのサポート言語が含まれている必要があり、高次の解決方法からサポート言語を継承することはありません。</p> </td>
  </tr>
 </tbody>
</table>

### 翻訳ルール  {#translation-rules}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/workflow/models/translation/translation_rules.xml</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/translation/rules/translation_rules.xml</code></p> <p><code>/apps/settings/translation/rules/translation_rules.xml</code></p> <p><code>/conf/global/settings/translation/rules/translation_rules.xml</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>変更した変換ルールXMLファイルは、新しい場所（<code>/apps</code>または<code>/conf/global</code>）に移行する必要があります。</p> <p>1. 変更した 翻訳ルール XML ファイルを以前の場所から新しい場所にコピーします。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>レプリケーション翻訳ルール XML の解決は次の順序でおこなわれます。</p>
    <ol>
     <li><code>/conf/global/settings/translation/rules/translation_rules.xml</code></li>
     <li><code class="code">/apps/settings/translation/rules/translation_rules.xml
        </code></li>
     <li><code class="code">/etc/workflow/models/translation/translation_rules.xml
        </code></li>
     <li><code>/libs/settings/translation/rules/translation_rules.xml</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### 翻訳 Widget クライアントライブラリ {#translation-widget-client-library}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/designs/translation/translationwidget</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/wcm/designs/translation/translationwidget</code></p> <p><code>/apps/settings/wcm/designs/translation/translationwidget</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>SCM で管理されており、実行時にデザインダイアログから書き込まれていないデザインの場合：</p>
    <ol>
     <li>デザインを以前の場所から新しい場所（/apps）にコピーします。</li>
     <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"> を使用して、デザイン内の CSS、JavaScript、静的リソースを</a>クライアントライブラリ<code>allowProxy = true</code>に変換します。</li>
     <li>Folio Builder
      <code>
       cq
      </code>:
      <code>
       designPath
      </code>プロパティ。</li>
     <li>以前の場所を参照しているページを更新して、新規のクライアントライブラリカテゴリを使用します（これにはページ実装コードの更新が必要です）。</li>
     <li>/etc.clientlibs/.. プロキシサーブレットを介したクライアントライブラリの提供を許可するように AEM Dispatcher のルールを更新します。</li>
    </ol> <p>SCM で管理されていない、デザインダイアログでランタイムを変更したデザイン。</p>
    <ul>
     <li><code>/etc</code>の外にオーサリング可能なデザインを移動しないでください。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### ツリー Activation Web コンソール  {#tree-activation-web-console}

| **以前の場所** | `/etc/replication/treeactivation` |
|---|---|
| **新しい場所** | `/libs/replication/treeactivation` |
| **再構築の手引き** | アクションは必要ありません。 |
| **備考** | ツリー Activation Web コンソールは、**ツール／導入／レプリケーション／ツリーをアクティベート**&#x200B;から利用できます。 |

### ベンダー翻訳コネクタクラウドサービス  {#vendor-translation-connector-cloud-services}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/cloudservices/&lt;vendor&gt;</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> <p><code class="code">/apps/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code class="code">/conf/global/settings/cloudconfigs/translation/&lt;vendor&gt;
       </code></p> <p><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translation/&lt;vendor&gt;</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しいベンダー変換コネクタCloud Servicesは、新しい場所（<code>/apps</code>、<code>/conf/global</code>、または<code>/conf/&lt;tenant&gt;</code>）に移行する必要があります。</p>
    <ol>
     <li>以前の場所にある既存の設定を新しい場所に移行します。
      <ul>
       <li><strong>ツール／クラウドサービス／翻訳クラウドサービスの AEM オーサリング UI </strong>を使用して、新しいベンダー翻訳コネクタクラウドサービス設定を手動で作成します。<br /> または </li>
       <li>新しいベンダー変換コネクタCloud Services設定を前の場所から新しい場所(<code>/apps</code>、<code>/conf/global </code>、<code>/conf/&lt;tenant&gt;</code>)にコピーします。</li>
      </ul> </li>
     <li>該当する AEM 設定を AEM コンテンツ階層と関連付けます。
      <ol>
       <li>「<strong>AEM Sites／ページ／ページのプロパティ／詳細タブ／クラウド設定</strong>」を使用した AEM Sites のページ階層。</li>
       <li>「<strong>AEM エクスペリエンスフラグメント／エクスペリエンスフラグメント／プロパティ／クラウドサービスタブ／クラウド設定</strong>」を使用した AEM エクスペリエンスフラグメント階層。</li>
       <li>「<strong>AEM エクスペリエンスフラグメント／フォルダー／プロパティ／クラウドサービスタブ／クラウド設定</strong>」を使用した AEM エクスペリエンスフラグメントフォルダー階層。</li>
       <li><strong>AEM Assets/フォルダー/Cloud Servicesーのプロパティ/フォルダータブ/設定</strong>を介したAEM Assetsフォルダー階層。</li>
       <li><strong>AEMプロジェクト/プロジェクト/プロジェクトのプロパティ/詳細タブ/クラウドの設定</strong>を介したAEMプロジェクト。</li>
      </ol> </li>
     <li>前述の AEM コンテンツ階層から、移行された従来の翻訳クラウドサービスとの関連付けをすべて解除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>翻訳クラウドサービスの解決は次の順序でおこなわれます。</p>
    <ol>
     <li><code>/conf/&lt;tenant&gt;/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/conf/global/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/apps/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
     <li><code>/libs/settings/cloudconfigs/translations/&lt;vendor&gt;</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### ワークフロー通知電子メールテンプレート {#workflow-notification-email-templates}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/workflow/notification</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/workflow/notification</code></p> <p><code>/conf/global/settings/workflow/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>変更されたワークフロー通知電子メールテンプレートは、新しい場所(<code>/conf/global</code>)に移行する必要があります。</p>
    <ol>
     <li>変更されたワークフロー通知電子メールテンプレートを以前の場所から新しい場所にコピーします。</li>
     <li>移行されたワークフロー通知電子メールテンプレートを以前の場所から削除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>ワークフロー通知電子メールテンプレートの解決は、次の順序でおこなわれます。</p>
    <ol>
     <li><code>/etc/workflow/notification</code></li>
     <li><code>/conf/global/settings/workflow/notification</code></li>
     <li><code>/libs/settings/workflow/notification</code></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

### ワークフローパッケージ {#workflow-packages}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/var/workflow/packages</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>以前の場所にある既存のワークフローパッケージは、新しい場所に移行する必要があります。</p>
    <ol>
     <li>以前の場所にある、他のコンテンツによって参照されていない、または不要なワークフローパッケージを削除します。</li>
     <li>以前の場所にある、他のコンテンツによって参照されていないものの、必要とされているワークフローパッケージを新しい場所に移動します。</li>
     <li>他のコンテンツによって参照されているワークフローパッケージはすべて以前の場所に残します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><p>クラシック UI の Miscadmin コンソールで作成されたワークフローパッケージは以前の場所に保持されますが、他のものはすべて新しい場所に保持されます。</p> <p>以前の場所または新しい場所に保存されているワークフローパッケージは、クラシック UI の Miscadmin コンソールで管理できます。</p> </td>
  </tr>
 </tbody>
</table>

