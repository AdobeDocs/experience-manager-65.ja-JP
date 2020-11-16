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

As described on the parent [Repository Restructuring in AEM 6.5](/help/sites-deploying/repository-restructuring.md) page, customers upgrading to AEM 6.5 should use this page to assess the work effort associated with repository changes impacting the AEM Assets Solution. 一部の変更ではAEM 6.5のアップグレードプロセス中に作業が必要になり、残りの変更は将来のアップグレードまで延期できます。

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

## 今後のアップグレードの前 {#prior-to-upgrade}

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
     <li>電子メ <code>/libs/settings/dam/notification</code> ールテンプレートは、からにコピーする必要があ <strong><code>/etc/notification/email/default</code></strong> ります <strong><code>/apps/settings/notification/email/default</code></strong>
      <ol>
       <li>Because the destination is in<strong> <code>/apps</code></strong> this change should be persisted in SCM.</li>
      </ol> </li>
     <li>Remove the folder: <strong><code>/etc/dam/notification/email/default</code></strong> after the e-mail templates within it have been moved.<br />
      <ol>
       <li>If no updates were made to the e-mail template under<strong> <code>/etc/notification/email/default</code></strong>, the folder can be removed as the original e-mail template exists under <strong><code>/libs/settings/notification/email/default</code></strong> as part of AEM 4 install.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### 従来のアセット共有デザイン {#classic-asset-share-designs}

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
     <li>Copy the designs from the Previous Location to the New Location under <code>/apps</code>.</li>
     <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank"> を使用して、デザイン内の CSS、JavaScript、静的リソースを</a>クライアントライブラリ<code>allowProxy = true</code>に変換します。</li>
     <li><code>cq:designPath</code>AEM／DAM 管理／アセット共有ページ／ページのプロパティ／詳細タブ／デザインフィールド<strong>を使用して、</strong> プロパティで以前の場所への参照を更新します。</li>
     <li>以前の場所を参照しているすべてのページを更新して、新しいクライアントライブラリカテゴリを使用するようにします。それには、ページの実装コードを更新する必要があります。</li>
     <li>Update the Dispatcher rules to allow serving of Client Libraries via the <code>/etc.clientlibs/</code> proxy servlet.</li>
    </ol> <p>For any Designs that are not managed in SCM, and modified run-time via Design Dialogs, do not move authorable designs out of <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### アセットダウンロード電子メール通知テンプレート {#download-asset-e-mail-notification-template}

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
     <li>The updated e-mail template should be copied from <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> to <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong>
      <ol>
       <li>Because the destination is in<strong> <code>/apps</code></strong> this change should be persisted in SCM.</li>
      </ol> </li>
     <li>Remove the folder: <code>/etc/dam/workflow/notification/email/downloadasset </code>after the e-mail templates within it have been moved.<br />
      <ol>
       <li>If no updates were made to the e-mail template under<strong> <code>/etc</code></strong>, the folder can be removed as the orginal e-mail template exists under <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> as part of AEM 6.4 install.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>While <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> is technically supported for look-up (takes precedence before /apps via usual Sling CAConfig lookup, but after <code>/etc</code>) the template could be placed in <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. ただし、電子メールテンプレートを容易に編集できる実行時 UI がないので、これはお勧めできません。</td>
  </tr>
 </tbody>
</table>

### サンプル DRM ライセンス {#example-drm-licenses}

| **以前の場所** | `/etc/dam/drm/licenses/` |
|---|---|
| **新しい場所** | `/libs/settings/dam/drm` |
| **再構築の手引き** | 該当なし |
| **備考** | 該当なし |

### リンク共有電子メール通知テンプレート {#link-share-e-mail-notification-template}

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
     <li>The updated e-mail template should be copied from <strong><code>/etc/dam/adhocassetshare</code></strong> to <strong><code>/apps/settings/dam/adhocassetshare</code></strong>
      <ol>
       <li>Because the destination is in<strong> <code>/apps</code></strong> this change should be persisted in SCM.</li>
      </ol> </li>
     <li>Remove the folder: <strong><code>/etc/dam/adhocassetshare</code></strong> after the e-mail templates within it have been moved.<br />
      <ol>
       <li>If no updates were made to the e-mail template under<strong> <code>/etc</code></strong>, the folder can be removed as the original e-mail template exists under <strong><code>/libs/settings/dam/adhocassetshare</code></strong> as part of AEM 6.4 install.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>While <code>/conf/global/settings/dam/adhocassetshare</code> is technically supported for look-up (it takes precedence before <code>/apps</code> via usual Sling CAConfig lookup, but after <code>/etc</code>), the template can be placed in <code>/conf/global/settings/dam/adhocassetshare</code>. ただし、電子メールテンプレートの編集を容易にするランタイムUIがないので、この方法はお勧めしません</td>
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
     <li>カスタムスクリプトまたは変更済みスクリプトをから <strong><code>/etc/dam/indesign/scripts</code></strong> にコピー <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br />
      <ol>
       <li>Only copy new or modified scripts as unmodified scripts provided by AEM will be available via <strong><code>/libs/settings</code></strong> in AEM 6.5</li>
      </ol> </li>
     <li>メディア抽出プロセスワークフローステップを使用するすべてのワークフローモデルを見つけて、以下をおこないます。
      <ol>
       <li>For each instance of the Workflow Step, update the paths in config to point explicitly at the proper scripts under<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> or <strong><code>/libs/settings/dam/indesign/scripts</code></strong> as appropriate.</li>
      </ol> </li>
     <li>完全に削除<strong><code>/etc/dam/indesign/scripts</code></strong> 。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>It is recommended customized scripts be stored under <code>/apps</code>, since that is the location where code should be stored.</td>
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
   <td><p>Project level customizations need to be cut and pasted under equivalent <code>/apps</code> or <code>/conf</code> paths as applicable.</p> <p>AEM 6.4 のリポジトリ構造に合わせるには：</p>
    <ol>
     <li>変更したビデオ設定をからにコピー <code>/etc/dam/video</code> します。 <code>/apps/settings/dam/video</code></li>
     <li>削除 <code>/etc/dam/video</code></li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### ビューアプリセット設定 {#viewer-preset-configurations}

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
     <li>you will have to run a migration script to move the node from <code>/etc</code> to <code>/conf</code>. The script is located at <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>または、設定を編集できます。編集した設定は新しい場所に自動保存されます。</li>
    </ul> <p>Note that you do not have to adjust their copyURL/embed code to point to <code>/conf</code>. The existing request to <code>/etc</code> will be re-routed to the correct content from <code>/conf</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### その他 {#misc2}

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
   <td><p>Adjust any references to point to the new resources under <code>/libs</code> using the <code>/etc.clientlibs/</code> allow proxy prefix.</p> <p>最後に、 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

