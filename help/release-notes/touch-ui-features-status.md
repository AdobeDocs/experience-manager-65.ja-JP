---
title: タッチ操作対応 UI 機能のステータス
description: Adobe Experience Managerのタッチ対応UIに関するリリースノートです。
uuid: ceb081cc-7c33-4408-8032-3ac83d461268
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: f736581d-e6ea-4ec8-bfc7-16b9aa592097
docset: aem65
translation-type: tm+mt
source-git-commit: 57bad4e74b2dfd9e389643bfe58ef25564c5c545

---


# タッチ操作対応 UI 機能のステータス{#touch-ui-feature-status}

>[!CAUTION]
>
>[Classic UIはAEM 6.4以降で非推奨](../release-notes/deprecated-removed-features.md) 。アドビでは、クラシックUIの機能強化を今後行う予定はありません。タッチ対応UIの強力な新機能を利用することをお勧めします。

バージョン 6.0 から、AEM では、Adobe Marketing Cloud および全体的なアドビユーザーインターフェイスガイドラインと合致する「タッチ操作対応 UI」と呼ばれる（「タッチ UI」とも呼ばれます）新型ユーザーインターフェイスを採用しています。タッチ操作対応 UI は、従来のデスクトップ指向のインターフェイス（「クラシック UI」と呼ばれます）とほぼ同等の機能を備え、AEM の標準 UI となりました。

ほとんどの機能はタッチ操作対応 UI に搭載されていますが、まだ完成せず、今後のリリースで追加される機能もあります。

AEM 6.5で実装された機能の現在のステータスを次に示します。

For recommendations for customers that upgrade to AEM 6.5, please see [User Interface Recommendations for Customers](/help/sites-deploying/ui-recommendations.md) for details.

>[!NOTE]
>
>このページでは、クラシック UI の機能と同等のものについてのみ説明していることに注意してください。
>
>クラシック UI にない、タッチ操作対応 UI に追加された固有の機能は示されていません。

>[!NOTE]
>
>このリストは、完全を期していますが、あらゆる機能を網羅しているわけではありません。

## 凡例 {#legend}

* **完全**：この機能はタッチ操作対応 UI で完全に利用できます。
* **主に**:この機能は、タッチ操作対応UIでほとんど使用できます。
* **消失**：この機能はタッチ操作対応 UI に存在せず、この操作をおこなうにはクラシック UI を使用する必要があります。
* **置換**：この機能は動作が異なる新しい実装で置換されています。
* **削除**：この機能は、現在タッチ操作対応 UI に存在せず、置換もされません。

## 機能ステータス：サイト管理 {#feature-status-sites-admin}

This is a list of capabilities the classic UI Site Admin ( `/siteadmin`) has and the status in the touch-enabled UI ( `/sites.html`).

<table>
 <tbody>
  <tr>
   <td><strong>機能<br /> </strong></td>
   <td><strong>ステータス<br /> </strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>サイト階層を移動</td>
   <td>完全<br /> </td>
   <td>AEM 6.4では、コンテンツツリービ <a href="/help/sites-authoring/basic-handling.md#content-tree">ューが導入されました</a>。</td>
  </tr>
  <tr>
   <td>ワークフローを開始</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ページを新規作成</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>サイトを新規作成</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ローンチを新規作成</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>Create new livecopy <br /> </td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>フォルダーを作成</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>公開ステータスを表示</td>
   <td>完了</td>
   <td>AEM 6.5以降では、ワークフローの状態がリストビューに表示されます</td>
  </tr>
  <tr>
   <td>検索</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ページをコピー／貼り付け（複製）</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ページを移動</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ページを公開</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>レプリケーション権限なしでページを公開</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>後で公開</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ツリーを公開</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ページを非公開</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>レプリケーション権限なしでページを非公開</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>後で非公開</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>削除</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ロック／ロック解除</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>プロパティを表示／編集</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ページに権限を設定</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>バージョン履歴</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>バージョンを復元</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ツリーおよび削除されたページを復元</td>
   <td>消失</td>
   <td>クラシック UI を使用します。</td>
  </tr>
  <tr>
   <td>古いバージョンと現在のバージョンの違いを表示<br /> </td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ライブコピー操作（ロールアウト）</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>言語コピーを表示</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>検索と置換</td>
   <td>消失<br /> </td>
   <td>クラシック UI を使用します。</td>
  </tr>
  <tr>
   <td>通知インボックス（JCR イベント）</td>
   <td>消失</td>
   <td>クラシック UI を使用します。別の実装で置き換えられます。</td>
  </tr>
  <tr>
   <td>参照</td>
   <td>完了</td>
   <td>AEM 6.5に追加された着信ページリンクの表示。<br /> </td>
  </tr>
 </tbody>
</table>

## 機能ステータス：ページエディター {#feature-status-page-editor}

This is a list of capabilities the classic UI Page Editor ( `/cf#`) has and the status in the touch-enabled ( `/editor.html`).

<table>
 <tbody>
  <tr>
   <td><strong>機能</strong></td>
   <td><strong>ステータス</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>Web ページを編集</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>モバイル Web ページを編集<br /> </td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>デザインインポーターを介して読み込んだコンテンツを編集<br /> </td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>電子メールを編集</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ハイブリッドモバイルアプリの編集</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>フォームを編集</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>オファーを編集</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ワークフローモデルを編集<br /> </td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>コード：編集とプレビュー</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>Responsive Preview<br /> </td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>モード：デザインを編集</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>モード：基礎モード</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>モード：ライブコピーステータス<br /> </td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>注釈を追加</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>プロパティを編集<br /> </td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ページをロールアウト</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ワークフローを開始および表示</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ワークフローパッケージ処理</td>
   <td>ほぼ完全</td>
   <td>タッチ操作対応UIから完全にアクセス可能。 従来のUIに複数のワークフローペイロードが表示されていました。<br /> </td>
  </tr>
  <tr>
   <td>ページをロック／ロック解除</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ページを公開 <br /> </td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>ページを非公開</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>ページをコピー</td>
   <td>削除<br /> </td>
   <td>サイト管理を使用して<a href="/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page">ページをコピー</a>します。<br /> </td>
  </tr>
  <tr>
   <td>ページを移動</td>
   <td>削除</td>
   <td>サイト管理を使用して<a href="/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page">ページを移動</a>します。<br /> </td>
  </tr>
  <tr>
   <td>ページを削除</td>
   <td>削除</td>
   <td>サイト管理を使用して<a href="/help/sites-authoring/managing-pages.md#deleting-a-page">ページを削除</a>します。<br /> </td>
  </tr>
  <tr>
   <td>参照を表示</td>
   <td>削除</td>
   <td>サイト管理を使用して<a href="/help/sites-authoring/author-environment-tools.md#references">詳細な参照リストを表示</a>します。<br /> </td>
  </tr>
  <tr>
   <td>監査ログ</td>
   <td>削除</td>
   <td>サイト管理を使用し、<a href="/help/sites-authoring/author-environment-tools.md#events-timeline">アクティビティレールを開き</a>ます。<br /> </td>
  </tr>
  <tr>
   <td>バージョンを作成</td>
   <td>削除</td>
   <td>サイト管理を使用して<a href="/help/sites-authoring/working-with-page-versions.md#creating-a-new-version">バージョンを新規作成</a>します。<br /> </td>
  </tr>
  <tr>
   <td>バージョンを復元</td>
   <td>削除</td>
   <td>サイト管理を使用して<a href="/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version">バージョンを復元</a>します。</td>
  </tr>
  <tr>
   <td>ローンチを切り替え</td>
   <td>削除</td>
   <td>サイト管理を使用して<a href="/help/sites-authoring/launches-promoting.md">起動を切り替え</a>ます。<br /> </td>
  </tr>
  <tr>
   <td>ページを翻訳</td>
   <td>削除</td>
   <td>サイト管理を使用して<a href="/help/sites-administering/tc-manage.md">翻訳プロジェクトにページを追加</a>します。<br /> </td>
  </tr>
  <tr>
   <td>タイムワープ（日付／時刻を選択してその指定日時の時点のサイトを表示）<br /> </td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>権限を設定</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>クライアントコンテキスト UI<br /> </td>
   <td>置換</td>
   <td>今後は <a href="/help/sites-authoring/ch-previewing.md">ContextHub</a> UI を使用します。</td>
  </tr>
  <tr>
   <td>各種メディアタイプのコンテンツファインダー<br /> </td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>コンポーネントリスト</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>コンポーネントをコピーおよび貼り付け<br /> </td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>クリップボード内のコンポーネントのリスト</td>
   <td>消失</td>
   <td> </td>
  </tr>
  <tr>
   <td>取り消し／やり直し</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>コンテンツをコンポーネントのプレースホルダーにドラッグ＆ドロップ</td>
   <td>完全</td>
   <td> </td>
  </tr>
  <tr>
   <td>コンテンツを parsys プレースホルダーに直接ドラッグ＆ドロップしてコンポーネントを自動作成<br /> </td>
   <td>完全</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 機能ステータス：テキスト、テーブルおよび画像エディター {#feature-status-text-table-and-image-editors}

これは、従来のUIテキスト、テーブル、および画像エディターの機能と、タッチ対応UIのステータスのリストです。

<table>
 <tbody>
  <tr>
   <td><strong>機能</strong></td>
   <td><strong>ステータス </strong></td>
   <td><strong>コメント<br /> </strong></td>
  </tr>
  <tr>
   <td>リッチテキストエディター</td>
   <td>完了</td>
   <td>インプレイス、ダイアログ、フルスクリーンで使用できます。</td>
  </tr>
  <tr>
   <td>RTEプラグインの有効化/無効化</td>
   <td>完全<br /> </td>
   <td>テンプレートエディターを使 <a href="/help/sites-authoring/templates.md">用して実行できま</a>す。</td>
  </tr>
  <tr>
   <td>プレーンテキストにRTEを使用</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：リンクとアンカー</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：文字マップ</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：コピー/貼り付け</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：Microsoft wordから貼り付け<br /> </td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：検索と置換</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：テキスト書式（太字、...）</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：下付き文字と上付き文字</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：両端揃え</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：リスト（箇条書き/番号）</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：段落書式</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：テキストスタイル</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：ソースエディタ（HTMLを編集）<br /> </td>
   <td>完全<br /> </td>
   <td>ダイアログとフルスクリーンでのみ使用できます。<br /> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：スペルチェッカー</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：テーブル（埋め込みテーブルエディター）</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：取り消し/やり直し<br /> </td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>RTEプラグイン：インライン画像を許可する</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>テーブルエディター</td>
   <td>完了</td>
   <td>インプレイス、ダイアログ、フルスクリーンで使用できます。<br /> </td>
  </tr>
  <tr>
   <td>表のセルに画像をドラッグ&amp;ドロップ<br /> </td>
   <td>完了</td>
   <td>使用可能なインライン</td>
  </tr>
  <tr>
   <td>画像エディター<br /> </td>
   <td>完了</td>
   <td>インプレイス、ダイアログ、フルスクリーンで使用できます。<br /> </td>
  </tr>
  <tr>
   <td>IPEプラグインの有効化/無効化</td>
   <td>完了</td>
   <td>AEM 6.3では、テンプレートエディターにUIが <a href="/help/sites-authoring/templates.md">導入されました</a>。</td>
  </tr>
  <tr>
   <td>IPEプラグイン：切り抜き</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPEプラグイン：反転</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>IPEプラグイン：取り消し/やり直し</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>IPEプラグイン：画像マップ</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPEプラグイン：回転</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>IPEプラグイン：ズーム</td>
   <td>完全<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 機能ステータス：ツール {#feature-status-tools}

これは、クラシック UI にある多様なツールおよびタッチ操作対応 UI でのステータスの一覧です。

<table>
 <tbody>
  <tr>
   <td><strong>機能<br /> </strong></td>
   <td><strong>ステータス<br /> </strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>タスク管理</td>
   <td>置換</td>
   <td>6.0では、 <a href="/help/sites-authoring/projects.md">Projects &amp; Tasksが導入されました</a>。<br /> </td>
  </tr>
  <tr>
   <td>ワークフロー受信トレイ<br /> </td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>ページテンプレート設定へのワークフロー(<code>/etc/workflow/wcm/templates.html</code>)</td>
   <td>消失<br /> </td>
   <td>クラシック UI を使用します。</td>
  </tr>
  <tr>
   <td>管理UIのタグ付け<br /> </td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>MSM/Blueprintコントロールセンター</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>Blueprint Manager UI</td>
   <td>完了</td>
   <td> </td>
  </tr>
  <tr>
   <td>ロールアウト設定UI</td>
   <td>消失</td>
   <td>クラシック UI を使用します。</td>
  </tr>
  <tr>
   <td>ユーザー、グループ、権限UI<br /> </td>
   <td>ほとんど完了<br /> </td>
   <td>高度な権限編集を行うには、クラシックUIを使用します。<br /> </td>
  </tr>
  <tr>
   <td>バージョンの削除(<code>/etc/versioning/purge.html</code>)</td>
   <td>消失</td>
   <td>クラシック UI を使用します。</td>
  </tr>
  <tr>
   <td>外部リンクチェック (<code>/etc/linkchecker.html</code>)</td>
   <td>消失</td>
   <td>クラシック UI を使用します。<br /> </td>
  </tr>
  <tr>
   <td>バルクエディタ(<code>/etc/importers/bulkeditor.html</code>)</td>
   <td>消失<br /> </td>
   <td>クラシック UI を使用します。</td>
  </tr>
  <tr>
   <td>サムネールをアップロードして追加または上書き<br /> </td>
   <td>消失</td>
   <td>クラシック UI を使用します。</td>
  </tr>
 </tbody>
</table>

