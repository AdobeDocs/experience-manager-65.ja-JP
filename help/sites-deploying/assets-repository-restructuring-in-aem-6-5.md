---
title: AEM 6.5 における Assets リポジトリの再構築
description: Adobe Experience Manager(AEM)6.5 for Assets の新しいリポジトリ構造に移行するために必要な変更を行う方法を説明します。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 28ddd23c-5907-4356-af56-ebc7589a2b5d
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 48%

---

# AEM 6.5 における Assets リポジトリの再構築 {#assets-repository-restructuring-in-aem}

親の説明に従って [AEM 6.5 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md) このページでは、Adobe Experience Manager(AEM)6.5 にアップグレードするお客様は、このページを使用して、AEM Assetsソリューションに影響を与えるリポジトリの変更に関連する作業量を評価する必要があります。 一部の変更は AEM 6.5 アップグレードプロセス中に作業が必要ですが、それ以外は今後のアップグレードまで延期できます。

**6.5 へのアップグレード時におこなう変更**

* [その他](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#misc)

**今後のアップグレードの前に**

* [アセット／コレクションイベントのメール通知テンプレート](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#asset-collection-event-e-mail-notification-template)
* [従来のアセット共有デザイン](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#classic-asset-share-designs)
* [アセットダウンロードのメール通知テンプレート](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#download-asset-e-mail-notification-template)
* [サンプル DRM ライセンス](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#example-drm-licenses)
* [リンク共有のメール通知テンプレート](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md#link-share-e-mail-notification-template)
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
   <td><p>カスタムコードがこの場所（つまり、コードがこのパスに明示的に依存）している場合は、アップグレードする前に新しい場所を使用するようにコードを更新する必要があります。 理想的には、Java™ API を使用して、JCR 内の特定のパスへの依存を減らすことができます。</p> <p>クライアントがダウンロードする zip ファイルを保持する一時的な場所。 クライアントがアセットのダウンロードをリクエストするので、更新する必要はありません。 新しい場所にファイルが生成されます。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

## 今後のアップグレードの前に {#prior-to-upgrade}

### アセット／コレクションイベントのメール通知テンプレート {#asset-collection-event-e-mail-notification-template}

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
   <td><p>電子メールテンプレートが顧客によって変更された場合は、次の操作を実行して、新しいリポジトリ構造に合わせます。</p>
    <ol>
     <li><code>/libs/settings/dam/notification</code> メールテンプレートを <strong><code>/etc/notification/email/default</code></strong> から <strong><code>/apps/settings/notification/email/default</code></strong> にコピーする必要があります。
      <ol>
       <li>宛先が<strong> <code>/apps</code></strong>の場合、この変更は SCM に保持されます。</li>
      </ol> </li>
     <li><strong><code>/etc/dam/notification/email/default</code></strong> フォルダー内のメールテンプレートを移動したら、このフォルダーを削除します。<br />
      <ol>
       <li><strong> <code>/etc/notification/email/default</code></strong> 内のメールテンプレートが更新されていない場合は、このフォルダーを削除してかまいません。インストールされた AEM 4 の一部として元のメールテンプレートが <strong><code>/libs/settings/notification/email/default</code></strong> に存在するからです。</li>
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
   <td><p>SCM で管理され、実行時にデザインダイアログを介して書き込まれないデザインに対して、次の操作を実行して最新のモデルに合わせます。</p>
    <ol>
     <li>デザインを以前の場所から <code>/apps</code> 内の新しい場所にコピーします。</li>
     <li>デザイン内の CSS、JavaScript、静的リソースをに変換する <a href="/help/sites-developing/clientlibs.md#creating-client-library-folders" target="_blank">クライアントライブラリ</a> 次を使用 <code>allowProxy = true</code>.</li>
     <li>の以前の場所への参照を更新 <code>cq:designPath</code> ～を通じて財産を所有する <strong>AEM / DAM 管理者/アセット共有ページ/ページプロパティ/詳細タブ/デザインフィールド</strong>.</li>
     <li>新しいクライアントライブラリカテゴリを使用するには、以前の場所を参照しているページを更新します。 これには、ページ実装コードを更新する必要があります。</li>
     <li>Dispatcher のルールを更新し、 <code>/etc.clientlibs/</code> プロキシサーブレット。</li>
    </ol> <p>SCM で管理されず、デザインダイアログを介して実行時に変更されたデザインの場合は、オーサリング可能なデザインをから移動しないでください。 <code>/etc</code>.</p> </td>
  </tr>
  <tr>
   <td><strong>メモ</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### アセットダウンロードのメール通知テンプレート {#download-asset-e-mail-notification-template}

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
   <td><p>電子メールテンプレート (<strong>downloadasset</strong> または <strong>transientworkflowcompleted</strong>) が変更された後、以下の手順に従って新しい構造に合わせます。</p>
    <ol>
     <li>更新されたメールテンプレートを <strong><code>/etc/dam/workflow/notification/email/downloadasset</code></strong> から <strong><code>/apps/settings/dam/workflow/notification/email/downloadasset</code></strong> にコピーします。
      <ol>
       <li>宛先が<strong> <code>/apps</code></strong>の場合、この変更は SCM に保持されます。</li>
      </ol> </li>
     <li><code>/etc/dam/workflow/notification/email/downloadasset </code> フォルダー内のメールテンプレートを移動したら、このフォルダーを削除します。<br />
      <ol>
       <li><strong> <code>/etc</code></strong> 内のメールテンプレートが更新されていない場合は、このフォルダーを削除してかまいません。インストールされた AEM 6.4 の一部として元のメールテンプレートが <strong><code>/libs/settings/dam/workflownotification/email/downloadasset</code></strong> に存在するからです。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>While <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code> は、参照に対して技術的にサポートされます ( 通常の Sling CAConfig 参照によって/apps の前、ただし <code>/etc</code>) テンプレートを <code>/conf/global/settings/dam/workflownotification/email/downloadasset</code>. ただし、電子メールテンプレートの編集を容易にするランタイム UI がないので、この方法はお勧めしません。</td>
  </tr>
 </tbody>
</table>

### サンプル DRM ライセンス {#example-drm-licenses}

| **以前の場所** | `/etc/dam/drm/licenses/` |
|---|---|
| **新しい場所** | `/libs/settings/dam/drm` |
| **再構築の手引き** | 該当なし |
| **備考** | 該当なし |

### リンク共有のメール通知テンプレート {#link-share-e-mail-notification-template}

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
   <td><p>メールテンプレートが顧客によって変更されている場合は、新しいリポジトリ構造に合わせるために以下を実行します。</p>
    <ol>
     <li>更新されたメールテンプレートを <strong><code>/etc/dam/adhocassetshare</code></strong> から <strong><code>/apps/settings/dam/adhocassetshare</code></strong> にコピーします。
      <ol>
       <li>宛先が<strong><code>/apps</code></strong>の場合、この変更は SCM に保持されます。</li>
      </ol> </li>
     <li><strong><code>/etc/dam/adhocassetshare</code></strong> フォルダー内のメールテンプレートを移動したら、このフォルダーを削除します。<br />
      <ol>
       <li><strong> <code>/etc</code></strong> 内のメールテンプレートが更新されていない場合は、このフォルダーを削除してかまいません。インストールされた AEM 6.4 の一部として元のメールテンプレートが <strong><code>/libs/settings/dam/adhocassetshare</code></strong> に存在するからです。</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>While <code>/conf/global/settings/dam/adhocassetshare</code> は、参照に対して技術的にサポートされます ( 参照は、 <code>/apps</code> 通常の Sling CAConfig 参照を介して、しかし、 <code>/etc</code>) の代わりに使用する場合、テンプレートを <code>/conf/global/settings/dam/adhocassetshare</code>. ただし、メールテンプレートを容易に編集できる実行時 UI がないので、これはお勧めできません。</td>
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
     <li>すべてのカスタムスクリプトまたは変更済みスクリプトを <strong><code>/etc/dam/indesign/scripts</code></strong> から <strong><code>/apps/settings/dam/indesign/scripts</code></strong><br /> にコピーします。
      <ol>
       <li>AEMが提供する未変更のスクリプトは、 <strong><code>/libs/settings</code></strong> AEM 6.5 の場合</li>
      </ol> </li>
     <li>メディア抽出プロセスワークフローステップを使用するすべてのワークフローモデルを探し、以下の操作を実行します。
      <ol>
       <li>ワークフローステップのインスタンスごとに、config のパスを更新して、<strong> <code>/apps/settings/dam/indesign/scripts</code></strong> または <strong><code>/libs/settings/dam/indesign/scripts</code></strong>（該当する場合）内の適切なスクリプトを明示的に指すようにします。</li>
      </ol> </li>
     <li><strong> <code>/etc/dam/indesign/scripts</code></strong> を完全に削除します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>カスタマイズしたスクリプトは、コードの格納先である <code>/apps</code> 内に格納することをお勧めします。</td>
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
   <td><p>プロジェクトレベルのカスタマイズは、同等の下で切り取り&amp;貼り付ける必要があります <code>/apps</code> または <code>/conf</code> 該当するパス。</p> <p>AEM 6.4 のリポジトリ構造に合わせるには：</p>
    <ol>
     <li>変更されたビデオ設定を <code>/etc/dam/video</code> からコピーし、次の場所に貼り付けます： <code>/apps/settings/dam/video</code></li>
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
   <td><p>標準提供のビューアプリセットの場合、新しい場所でのみ使用できます。</p> <p>カスタムビューアプリセットの場合：</p>
    <ul>
     <li>移行スクリプトを実行して、次の場所からノードを移動 <code>/etc</code> から <code>/conf</code>. スクリプトは、 <em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>または、設定を編集すると、新しい場所に自動保存されます。</li>
    </ul> <p>次を指すように copyURL/埋め込みコードを調整する必要はありません。 <code>/conf</code>. に対する既存のリクエスト <code>/etc</code> が次の正しいコンテンツにリルーティングされます： <code>/conf</code>.</p> </td>
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
   <td><p><code>/libs</code> 内の新しいリソースを指すようにすべての参照を調整します。それには、<code>/etc.clientlibs/</code> を使用してプロキシプレフィックスを許可します。</p> <p>最後に、移行した clientlibs のフォルダーを / / から削除して、クリーンアップをおこないます。 <code>/etc/clientlibs/foundation/</code></p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>
