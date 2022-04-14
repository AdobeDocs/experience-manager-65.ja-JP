---
title: Adobe Experience Manager 6.5 における Dynamic Media リポジトリの再構築
description: Experience Manager 6.5 の Dynamic Media の新しいリポジトリ構造に移行するために、必要な変更を行う方法について説明します。
uuid: e26d61a4-47b6-493a-9ba2-4c58b200ddd9
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 61cd5751-0dc8-48e0-873e-3a64899489bb
feature: Upgrading
exl-id: 4e736924-74ea-431a-be19-1c4ff022f464
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: ht
source-wordcount: '413'
ht-degree: 100%

---

# Adobe Experience Manager 6.5 における Dynamic Media リポジトリの再構築 {#dynamic-media-repository-restructuring-in-aem}

親ページの [Adobe Experience Manage 6.5 のリポジトリ再構築](/help/sites-deploying/repository-restructuring.md)に記載されているように、Experience Manager 6.5 にアップグレードするユーザーは、このページを使用して、Dynamic Media に影響を与えるリポジトリの変更に関連する作業量を評価する必要があります。一部の変更は Experience Manager 6.5 アップグレードプロセス中に作業する必要がありますが、それ以外は将来のアップグレードまで延期できます。

**今後のアップグレードの前に**

* [カスタム適応ビデオエンコーディング設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#custom-adaptive-video-encoding-configurations)
* [Dynamic Media（DMS7）クラウド設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#dynamic-media-dms-cloud-configuration)
* [Dynamic Media（DM ハイブリッド）クラウドサービスの設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#cloudserviceconfiguration)
* [Dynamic Media - YouTube クラウドサービスの設定](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#youtubecloudserviceconfiguration)
* [その他](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md#misc)

## 今後のアップグレードの前に {#prior-to-upgrade}

### カスタムアダプティブビデオのエンコーディング設定  {#custom-adaptive-video-encoding-configurations}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/dam/video/dynamicmedia</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/video/jcr:content</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>次の移行スクリプトを使用して、新しい場所に移行できます：</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>または、Experience Manager UI で設定を編集すると、変更内容が新しい場所に保存されます。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media（DMS7）クラウド設定 {#dynamic-media-dms-cloud-configuration}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/conf/global/settings/cloudservices/dmscene7</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>ユーザーはこの場所で移行スクリプトを実行できます。<br /> </p>
    <ul>
     <li><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></li>
     <li>Dynamic Media OSGi バンドルを再起動します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

### Dynamic Media（DM ハイブリッド）クラウドサービス設定 {#cloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/conf/global/settings/dam/dm/cloudservices/dynamicmediaservices</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>最新のモデルに合わせるには、以下の移行スクリプトを実行できます:</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.jso</em></p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media - YouTube クラウドサービス設定  {#youtubecloudserviceconfiguration}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/cloudservices/youtube</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/libs/settings/dam/dm/youtube</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>1. YouTube からすべての動画を非公開にする<br /> 2.古い場所からすべてのチャネルをコピーするなど、新規のタッチ UI を使用して（<code>/conf</code> から） YouTube 設定を作成します。<br /> 3.すべての動画を YouTube に公開しなおします。</p> <p>このワークフローにより、新しい YouTube URL が生成されます。新規のタッチ UI YouTube 設定を作成する前に URL を非公開にしなければ、プロパティの下に複数の YouTube URL が表示されます。これは、再作成されたチャネルは機会があれば再度公開されるためです。つまり、プロパティの下に不要な URL が表示されていることになります。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし<br /> </td>
  </tr>
 </tbody>
</table>

### その他 {#misc}

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/dam/imageserver/macros</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/conf/global/settings/dam/dm/presets/macro</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>ユーザーは以下の移行スクリプトを実行できます。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> <p>または、Experience Manager UI で設定を編集すると、変更内容が新しい場所に保存されます。</p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td>
   <td><code>/etc/dam/presets/analytics</code></td>
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td>
   <td><code>/libs/settings/dam/dm/analytics</code></td>
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td>
   <td><p>ユーザーは以下の移行スクリプトを実行できます。</p> <p><em>https://serveraddress:serverport/libs/settings/dam/dm/presets.migratedmcontent.json</em></p> </td>
  </tr>
  <tr>
   <td><strong>備考</strong></td>
   <td>該当なし</td>
  </tr>
 </tbody>
</table>
