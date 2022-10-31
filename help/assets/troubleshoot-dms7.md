---
title: Dynamic Media のトラブルシューティング - Scene7 モード
description: Dynamic Media を Scene7 モードで実行している場合のトラブルシューティング。
uuid: 77e04ccf-33dc-4d2f-8950-318d4b008f74
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 0d48c031-d3ee-4143-b739-a79ba28fd63a
docset: aem65
role: User, Admin
exl-id: d4507059-a54d-4dc9-a263-e55dfa27eeb1
feature: Troubleshooting
mini-toc-levels: 3
source-git-commit: 9c3df2491f99fe31e4b64b47442dd583af06974e
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 100%

---

# Dynamic Media のトラブルシューティング - Scene7 モード{#troubleshooting-dynamic-media-scene-mode}

以下のドキュメントでは、**dynamicmedia_scene7** 実行モードで実行している Dynamic Media のトラブルシューティングについて説明します。

## セットアップと設定 {#setup-and-configuration}

以下の手順で、Dynamic Media が適切に設定されていることを確認します。

* 開始コマンドに `-r dynamicmedia_scene7` 実行モード引数を含めます。
* 使用可能な Dynamic Media 機能パックの&#x200B;*前に*、最初にすべての Adobe Experience Manager 6.4 累積修正パック（CFP）がインストールされていることを確認します。
* オプションの機能パック 18912 がインストールされていることを確認します。

   このオプションの機能パックは、FTP サポートが必要な場合や、Dynamic Media Classic から Dynamic Media にアセットを移行する場合に使用します。

* クラウドサービスのユーザーインターフェイスに移動して、「**[!UICONTROL 利用可能な設定]**」の下に割り当てられたアカウントが表示されることを確認します。
* `Dynamic Media Asset Activation (scene7)` レプリケーションエージェントが有効になっていることを確認します。

   このレプリケーションエージェントは、「作成者のエージェント」にあります。

## 一般（すべてのアセット） {#general-all-assets}

次に全般的なヒントやテクニックを示します。

### アセット同期ステータスプロパティ {#asset-synchronization-status-properties}

CRXDE Lite で次のアセットプロパティを見直すと、 Experience Manager から Dynamic Media へのアセットの同期に成功したことが確認できます。

| **プロパティ** | **例** | **説明** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | ノードが Dynamic Media にリンクされていることを示す全般的インジケーター。 |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** またはエラーテキスト | Dynamic Media へのアセットアップロードのステータス。 |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Dynamic Media のリモートアセットへの URL を生成するには、これを入力する必要があります。 |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **success** または **failed:`<error text>`** | セット（スピンセット、画像セットなど）、画像プリセット、ビューアプリセット、アセットの画像マップの更新、編集された画像などの同期ステータス。 |

### 同期のログ {#synchronization-logging}

同期のエラーと問題は `error.log`（Experience Manager サーバーディレクトリの `/crx-quickstart/logs/`）に記録されます。ログにはほとんどの問題の根本原因を突き止めるのに十分な情報が記録されますが、Sling コンソール（[https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)）を通じて `com.adobe.cq.dam.ips` パッケージのログレベルをデバッグに引き上げると、さらに詳しい情報を集めることができます。

### 移動、コピー、削除 {#move-copy-delete}

移動、コピーまたは削除の処理を実行する前に次をおこなってください。

* 画像やビデオの移動、コピーまたは削除操作の前に `<object_node>/jcr:content/metadata/dam:scene7ID` の値が存在することを確認します。
* 画像やビューアプリセットの移動、コピーまたは削除操作の前に `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` の値が存在することを確認します。
* 上記のメタデータ値がない場合、移動、コピーまたは削除処理の前に、アセットを再アップロードする必要があります。

### バージョン管理 {#version-control}

既存の Dynamic Media アセット（同じ名称、同じ場所）を置換する際、双方のアセットを保持またはバージョンを置換／作成の選択が可能です。

* 両方を保持すると、公開済みアセット URL の名前が一意なアセットが作成されます。例えば、`image.jpg` は元のアセットで、`image1.jpg` は新しくアップロードされたアセットです。

* Dynamic Media - Scene7 モードの配信ではバージョン作成はサポートされていません。配信の既存アセットが新しいバージョンに置き換わります。

## 画像とセット {#images-and-sets}

画像とセットで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>デバッグの方法</strong></td>
   <td><strong>解決策</strong></td>
  </tr>
  <tr>
   <td>アセットの詳細表示で URL／埋め込みコードのコピーボタンにアクセスできない</td>
   <td>
    <ol>
     <li><p>CRX/DE に移動します。</p>
      <ul>
       <li>JCR 内のプリセット <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> が定義されているかどうかを確認します。この場所は、Experience Manager 6.x から 6.4 にアップグレードし、移行をオプトアウトした場合に適用されます。それ以外の場合、場所は <code>/conf/global/settings/dam/dm/presets/viewer</code> になります。</li>
       <li>JCR のアセットに <code>dam:scene7FileStatus</code><strong> </strong> があり、それが「メタデータ」で <code>PublishComplete</code> と表示されていることを確認します。</li>
      </ul> </li>
    </ol> </td>
   <td><p>ページを更新するか、別のページに移動してから戻ります（サイドレール JSP を再コンパイルする必要があります）。</p> <p>それでも解決しない場合：</p>
    <ul>
     <li>アセットを公開します。</li>
     <li>アセットを再度アップロードして公開します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>設定エディターのアセットセレクターが永続的に読み込み中の状態になっている</td>
   <td><p>6.4 で解決予定の既知の問題です。</p> </td>
   <td><p>セレクターを閉じて再度開きます。</p> </td>
  </tr>
  <tr>
   <td>セットの編集でアセットを選択した後、<strong>選択</strong>ボタンが有効にならない</td>
   <td><p> </p> <p>6.4 で解決予定の既知の問題です。</p> <p> </p> </td>
   <td><p>アセットセレクターで別のフォルダーを選択してから、アセットの選択に戻ります。</p> </td>
  </tr>
  <tr>
   <td>スライドを切り替えた後、カルーセルホットスポットが移動する</td>
   <td><p>すべてのスライドが同じサイズであることを確認します。</p> </td>
   <td><p>カルーセルにはすべて同じサイズの画像のみを利用します。</p> </td>
  </tr>
  <tr>
   <td>Dynamic Media ビューアで画像がプレビューされない</td>
   <td><p>アセットのメタデータプロパティに <code>dam:scene7File</code> が含まれていることを確認します（CRXDE Lite）。</p> </td>
   <td><p>すべてのアセットの処理が終わるまで待ちます。</p> </td>
  </tr>
  <tr>
   <td>アップロードしたアセットがアセットセレクターに表示されない</td>
   <td><p>アセットのプロパティ <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> が <code>processed</code> であることを確認します（CRXDE Lite）。</p> </td>
   <td><p>すべてのアセットの処理が終わるまで待ちます。</p> </td>
  </tr>
  <tr>
   <td>アセットの処理がまだ開始していないときに、カード表示のバナーに「<strong>新規</strong>」と表示される</td>
   <td>アセットの <code>jcr:content</code> &gt; <code>dam:assetState</code> を確認します。<code>unprocessed</code> の場合は、アセットの処理がワークフローで開始されていません。</td>
   <td>ワークフローがアセットの処理を始めるまで待ちます。</td>
  </tr>
  <tr>
   <td>画像やセットでビューア URL や埋め込みコードが表示されない</td>
   <td>ビューアプリセットが公開されているかどうかを確認します。</td>
   <td><p><strong>ツール</strong>／<strong>アセット</strong>／<strong>ビューアプリセット</strong>に移動し、ビューアプリセットを公開します。</p> </td>
  </tr>
 </tbody>
</table>

## ビデオ {#video}

ビデオで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

<table>
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>デバッグの方法</strong></td>
   <td><strong>解決策</strong></td>
  </tr>
  <tr>
   <td>ビデオをプレビューできない</td>
   <td>
    <ul>
     <li>フォルダーにビデオプロファイルが割り当てられていることを確認します（サポートされていないファイル形式の場合）。サポートされていない場合、画像だけが表示されます。</li>
     <li>ビデオプロファイルには AVS セットを生成するためのエンコーディングプリセットが 2 つ以上含まれている必要があります（MP4 ファイルでは 1 つのエンコーディングがビデオコンテンツとして扱われます。サポートされていないファイルでは、処理されていないものと同じ扱いになります）。</li>
     <li>メタデータで <code>dam:scene7File</code> の <code>dam:scene7FileAvs</code> を確認して、ビデオの処理が終了したことを確かめます。</li>
    </ul> </td>
   <td>
    <ol>
     <li>ビデオプロファイルをフォルダーに割り当てます。</li>
     <li>エンコーディングプリセットを 2 つ以上含むよう、ビデオプロファイルを編集します。</li>
     <li>ビデオの処理が終わるのを待ちます。</li>
     <li>ビデオを再読み込みする前に、Dynamic Media エンコーディングビデオワークフローが実行されていないことを確認します。<br /> </li>
     <li>ビデオを再度アップロードします。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>ビデオがエンコードされていない</td>
   <td>
    <ul>
     <li>実行モードが <code>dynamicmedia_scene7</code> であることを確認します。</li>
     <li>Dynamic Media クラウドサービスが設定されていることを確認します。</li>
     <li>ビデオプロファイルがアップロードフォルダーに関連付けられていることを確認します。</li>
    </ul> </td>
   <td>
    <ol>
     <li>次を使用して Experience Manager インスタンスを確認します。 <code>-r dynamicmedia_scene7</code></li>
     <li>クラウドサービスページで Dynamic Media 設定が正しくセットアップされていることを確認します。</li>
     <li>フォルダーにビデオプロファイルがあることを確認します。そのビデオプロファイルも確認します。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>ビデオの処理に時間がかかりすぎる</td>
   <td><p>ビデオのエンコーディングがまだ進行中か、エラー状態になっているかを判断するには：</p>
    <ul>
     <li>ビデオのステータスを確認します。<code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>ワークフローコンソールでビデオを監視します。<code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; 「インスタンス」タブ、「アーカイブ」タブ、「エラー」タブ。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ビデオレンディションがない</td>
   <td><p>ビデオがアップロードされても、エンコードされたレンディションがない場合：</p>
    <ul>
     <li>フォルダーにビデオプロファイルが割り当てられていることを確認します。</li>
     <li>メタデータで <code>dam:scene7FileAvs</code> を確認して、ビデオの処理が終了したことを確かめます。</li>
    </ul> </td>
   <td>
    <ol>
     <li>ビデオプロファイルをフォルダーに割り当てます。</li>
     <li>ビデオの処理が終わるのを待ちます。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## ビューア {#viewers}

ビューアで問題が発生している場合、次のトラブルシューティングガイドに従ってください。

### 問題：ビューアプリセットが公開されていない {#viewers-not-published}

**デバッグの方法**

1. サンプルマネージャー診断ページ `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html` に移動します。
1. 計算された値を確認します。正しく動作すると、次のように表示されます。`_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets` です。

   >[!NOTE]
   >
   >Dynamic Media クラウドの設定後、ビューアアセットが同期するまで 10 分ほどかかることがあります。

1. アクティブでないアセットが残る場合は、「**アクティブでないアセットをすべて表示**」ボタンのどちらかを選択して詳細を確認してください。

**解決策**

1. 管理ツールのビューアプリセットリスト（`https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`）に移動します。
1. すべてのビューアプリセットを選択したあと、「**公開**」を選択します。
1. サンプルマネージャーに戻り、アクティブでないアセット数がゼロになったことを確認します。

### 問題：ビューアプリセットのアートワークが、アセット詳細のプレビューまたは URL をコピー／埋め込みコードで 404 を返す {#viewer-preset-404}

**デバッグの方法**

CRXDE Lite で以下を行います。

1. Dynamic Media 同期フォルダー内の `<sync-folder>/_CSS/_OOTB` フォルダー（例えば `/content/dam/_CSS/_OOTB`）に移動します。
1. 問題のあるアセットのメタデータノードを見つけます（例えば `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`）。
1. `dam:scene7*` プロパティがあることを確認します。アセットの同期と公開に成功した場合は `dam:scene7FileStatus` が **PublishComplete** に設定されています。
1. 次のプロパティと文字列リテラルの値を連結して Dynamic Media に直接アートワークを要求します。

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
例： 
`https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**解決策**

サンプルアセットまたはビューアプリセットのアートワークが同期されていないか、公開されてない場合は、コピー／同期処理全体をやり直します。

1. CRXDE Lite に移動します。
1. `<sync-folder>/_CSS/_OOTB` を削除します。
1. CRX パッケージマネージャー（`https://localhost:4502/crx/packmgr/`）に移動します。
1. リストでビューアパッケージを検索します（`cq-dam-scene7-viewers-content` で始まります）。
1. 「**再インストール**」を選択します。
1. クラウドサービスページで、Dynamic Media 設定ページに移動した後、Dynamic Media - Scene7 設定の設定ダイアログボックスを開きます。
1. 何も変更せず、「**保存**」をクリックします。この保存アクションで、サンプルアセット、ビューアプリセット CSS およびアートワークを作成および同期するロジックが、再度トリガーされます。

### 問題：ビューアプリセットのオーサリングで画像プレビューが読み込まれない {#image-preview-not-loading}

**解決策**

1. Experience Manager で、Experience Manager ロゴを選択してグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**／**[!UICONTROL 一般]**／**[!UICONTROL CRXDE Lite]** に移動します。
1. 左側のパネルで、次の場所にあるサンプルコンテンツフォルダーに移動します。

   `/content/dam/_DMSAMPLE`

1. `_DMSAMPLE` フォルダーを削除します。
1. 左側のパネルで、次の場所にあるプリセットフォルダーに移動します。

   `/conf/global/settings/dam/dm/presets/viewer`

1. `viewer` フォルダーを削除します。
1. CRXDE Lite ページの左上隅付近にある「**[!UICONTROL すべて保存]**」を選択します。
1. CRXDE Lite ページの左上隅にある「**ホームに戻る**」アイコンを選択します。
1. [Cloud Services の Dynamic Media 設定](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)を再作成します。
