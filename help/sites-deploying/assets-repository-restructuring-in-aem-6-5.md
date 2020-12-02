---
title: AEM 6.5 における Assets リポジトリの再構築
seo-title: AEM 6.5 における Assets リポジトリの再構築
description: AEM 6.5 for Assets の新しいリポジトリ構造に移行するために必要な変更を加える方法について説明します。
seo-description: AEM 6.5 for Assets の新しいリポジトリ構造に移行するために必要な変更を加える方法について説明します。
uuid: 0e3d8163-6274-4d1b-91c7-32ca927fb83c
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 212930fc-3430-4a0a-842c-2fb613ef981f
translation-type: tm+mt
source-git-commit: d20ddba254c965e1b0c0fc84a482b7e89d4df5cb
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 50%

---


# AEM 6.5 における Assets リポジトリの再構築 {#assets-repository-restructuring-in-aem}

AEM 6.5](/help/sites-deploying/repository-restructuring.md)の親ページ[リポジトリの再構築に関する説明に従い、AEM 6.5にアップグレードしたお客様は、このページを使用して、AEM Assets・ソリューションに影響を与えるリポジトリの変更に関連する作業量を評価する必要があります。 一部の変更ではAEM 6.5のアップグレードプロセス中に作業が必要になり、残りの変更は将来のアップグレードまで延期できます。

**6.5 へのアップグレード時におこなう変更**

* [その他](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**今後のアップグレードの前**

* [アセット／収集イベント電子メール通知テンプレート](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [従来のアセット共有デザイン](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [アセットダウンロード電子メール通知テンプレート](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [サンプル DRM ライセンス](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [リンク共有電子メール通知テンプレート](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
* [InDesign ワークフロースクリプト](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#indesign-workflow-scripts)
* [ビデオトランスコーディング設定](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#video-transcoding-configurations)
* [その他](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc2)

## 6.5 へのアップグレード時におこなう変更 {#with-upgrade}

### その他 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td>/etc/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td>/var/dam/jobs</td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>カスタムコードがこの場所に依存している（コードがこのパスに明示的に依存している）場合は、アップグレード前に、新しい場所を使用するようにコードを更新する必要があります。JCR 内の特定パスへの依存を減らすために Java API が利用可能な場合は、Java API を使用することをお勧めします。</p> <p>クライアントがダウンロードする zip ファイルを一時的に保存するための場所。クライアントがアセットのダウンロードを要求するので、更新する必要はありません。新しい場所にファイルが生成されます。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

## 将来のアップグレードの前{#prior-to-upgrade}

### アセット／収集イベント電子メール通知テンプレート {#asset-collection-event-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/notification/email/default</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/dam/notification</code></p> <p><code>/apps/settings/dam/notification</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>電子メールテンプレートが顧客によって変更されている場合は、新しいリポジトリ構造に合わせるために次の操作を実行します。</p>
    <ol>
     <li><code>/libs/settings/dam/notification</code>電子メールテンプレートは<strong><code>/etc/notification/email/default</code></strong>から<strong><code>/apps/settings/notification/email/default</code></strong>にコピーする必要があります
      <ol>
       <li>宛先は<strong> <code>/apps</code></strong>にあるので、この変更はSCM内に保持する必要があります。</li>
      </ol> </li>
     <li>フォルダの削除：<strong><code>/etc/dam/notification/email/default</code></strong>内の電子メールテンプレートが移動された後。<br />
      <ol>
       <li><strong> <code>/etc/notification/email/default</code></strong>の下の電子メールテンプレートに更新が行われなかった場合は、AEM 4のインストールの一環として<strong><code>/libs/settings/notification/email/default</code></strong>の下に元の電子メールテンプレートが存在するので、フォルダーを削除できます。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### 従来のアセット共有デザイン  {#classic-asset-share-designs}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/designs/assetshare</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/wcm/designs/assetshare</code></p> <p><code>/apps/settings/wcm/designs/assetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>SCM で管理されており、実行時にデザインダイアログから書き込まれていないデザインについては、次の操作を実行して最新のモデルに合わせます。</p>
    <ol>
     <li>デザインを「前の場所」から「<code>/apps</code>の下の新しい場所」にコピーします。</li>
     <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"> を使用して、デザイン内の CSS、JavaScript、静的リソースを</a>クライアントライブラリ<code>allowProxy = true</code>に変換します。</li>
     <li><code>cq:designPath</code>AEM／DAM 管理／アセット共有ページ／ページのプロパティ／詳細タブ／デザインフィールド<strong>を使用して、</strong> プロパティで以前の場所への参照を更新します。</li>
     <li>以前の場所を参照しているすべてのページを更新して、新しいクライアントライブラリカテゴリを使用するようにします。それには、ページの実装コードを更新する必要があります。</li>
     <li><code>/etc.clientlibs/</code>プロキシサーブレットを介したクライアントライブラリの提供を許可するようにディスパッチャールールを更新します。</li>
    </ol> <p>SCMで管理されないデザインや、デザインダイアログを使用して実行時に変更されたデザインに対しては、許可可能なデザインを<code>/etc</code>から移動しないでください。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### アセットダウンロード電子メール通知テンプレート  {#download-asset-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/dam/workflow/notification/email/downloadasset</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/dam/workflownotification/email/downloadasset</code></p> <p><code>/apps/settings/dam/workflownotification/email/downloadasset</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>電子メールテンプレート（<strong>downloadasset</strong> または <strong>transientworkflowcompleted</strong>）が変更されている場合は、以下の手順に従って新しい構造に合わせます。</p>
    <ol>
     <li>更新した電子メールテンプレートを<strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong>から<strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>にコピーする必要があります
      <ol>
       <li>宛先は<strong> <code>/apps</code></strong>にあるので、この変更はSCM内に保持する必要があります。</li>
      </ol> </li>
     <li>フォルダの削除：<code>/etc/dam/workflow/notification/email/downloadasset </code>その中の電子メールテンプレートが移動された後。<br />
      <ol>
       <li><strong> <code>/etc</code></strong>の下で電子メールテンプレートに更新が行われなかった場合、AEM 6.4のインストールの一環として<strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong>の下に元の電子メールテンプレートが存在するので、フォルダーを削除できます。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>は、ルックアップ用に技術的にサポートされていますが（通常のSling CAConfig参照で/appsの前に優先されますが、<code>/etc</code>の後に優先されます）、テンプレートは<code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>に配置できます。 ただし、電子メールテンプレートを容易に編集できる実行時 UI がないので、これはお勧めできません。</td>
  </tr>
 </tbody>
</table>

### サンプル DRM ライセンス  {#example-drm-licenses}

| **以前の場所** | `/etc/dam/drm/licenses/` |
|---|---|
| **新しい場所** | `/libs/settings/dam/drm` |
| **再構築の手引き** | 該当なし |
| **備考** | 該当なし |

### リンク共有電子メール通知テンプレート  {#link-share-e-mail-notification-template}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/dam/adhocassetshare</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/dam/adhocassetshare</code></p> <p><code>/apps/settings/dam/adhocassetshare</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>電子メールテンプレートが顧客によって変更されている場合は、新しいリポジトリ構造に合わせるために以下を実行します。</p>
    <ol>
     <li>更新した電子メールテンプレートを<strong><code>/etc/dam/adhocassetshare</code></strong>から<strong><code>/apps/settings/dam/adhocassetshare</code></strong>にコピーする必要があります
      <ol>
       <li>宛先は<strong> <code>/apps</code></strong>にあるので、この変更はSCM内に保持する必要があります。</li>
      </ol> </li>
     <li>フォルダの削除：<strong><code>/etc/dam/adhocassetshare</code></strong>内の電子メールテンプレートが移動された後。<br />
      <ol>
       <li><strong> <code>/etc</code></strong>の下で電子メールテンプレートに更新が行われなかった場合は、AEM 6.4のインストールの一環として<strong><code>/libs/settings/dam/adhocassetshare</code></strong>の下に元の電子メールテンプレートが存在するので、フォルダーを削除できます。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td><code>/conf/global/settings/dam/adhocassetshare</code>は、ルックアップ用に技術的にサポートされていますが（通常のSling CAConfig参照を介して<code>/apps</code>の前に優先されますが、<code>/etc</code>の後に優先されます）、テンプレートは<code>/conf/global/settings/dam/adhocassetshare</code>に配置できます。 ただし、電子メールテンプレートの編集を容易にするランタイムUIがないので、この方法はお勧めしません</td>
  </tr>
 </tbody>
</table>

### InDesign ワークフロースクリプト {#indesign-workflow-scripts}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/dam/indesign/scripts</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/dam/indesign</code></p> <p><code>/apps/settings/dam/indesign</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>新しいリポジトリ構造に合わせるには：</p>
    <ol>
     <li>すべてのカスタムスクリプトまたは変更済みスクリプトを<strong><code>/etc/dam/indesign/scripts</code></strong>から<strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />にコピー
      <ol>
       <li>AEM 6.5では、AEMが提供する未変更のスクリプトとして、新しいスクリプトまたは変更されたスクリプトのみを<strong><code>/libs/settings</code></strong>経由で利用できます</li>
      </ol> </li>
     <li>メディア抽出プロセスワークフローステップを使用するすべてのワークフローモデルを見つけて、以下をおこないます。
      <ol>
       <li>ワークフロー手順の各インスタンスに対して、必要に応じて<strong> <code>/apps/settings/dam/indesign/scripts</code></strong>または<strong><code>/libs/settings/dam/indesign/scripts</code></strong>の下の適切なスクリプトを明示的に示すように、configのパスを更新します。</li>
      </ol> </li>
     <li><strong> <code>/etc/dam/indesign/scripts</code></strong>を完全に削除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>カスタマイズしたスクリプトは<code>/apps</code>の下に保存することをお勧めします。これは、コードを保存する必要がある場所です。</td>
  </tr>
 </tbody>
</table>

### ビデオトランスコーディング設定 {#video-transcoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/dam/video</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/dam/video</code></p> <p><code>/apps/settings/dam/video</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>プロジェクトレベルのカスタマイズは、必要に応じて、切り取って同等の<code>/apps</code>または<code>/conf</code>パスの下に貼り付ける必要があります。</p> <p>AEM 6.4 のリポジトリ構造に合わせるには：</p>
    <ol>
     <li>変更したビデオ設定を<code>/etc/dam/video</code>から <code>/apps/settings/dam/video</code></li>
     <li>削除 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### ビューアプリセット設定  {#viewer-preset-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/dam/presets/viewer</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><p><code>/libs/settings/dam/dm/presets/viewer</code></p> <p><code>/conf/global/settings/dam/dm/presets/viewer</code></p> </td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>既製のビューアプリセットの場合は、新しい場所でのみ使用できます。</p> <p>カスタムビューアプリセットの場合：</p>
    <ul>
     <li>ノードを<code>/etc</code>から<code>/conf</code>に移動するには、移行スクリプトを実行する必要があります。 スクリプトは<em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em>にあります。</li>
     <li>または、設定を編集できます。編集した設定は新しい場所に自動保存されます。</li>
    </ul> <p>copyURL/embedコードを<code>/conf</code>を指すように調整する必要はありません。 <code>/etc</code>への既存のリクエストは、<code>/conf</code>から正しいコンテンツに再ルーティングされます。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### その他  {#misc2}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><p><code>/etc/clientlibs/foundation/asseteditor</code></p> <p><code>/etc/clientlibs/foundation/assetshare</code></p> <p><code>/etc/clientlibs/foundation/assetinsights</code></p> </td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/libs/dam/clientlibs</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p><code>/etc.clientlibs/</code> allow proxy prefixを使用して、<code>/libs</code>の下の新しいリソースを指す参照を調整します。</p> <p>最後に、 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

