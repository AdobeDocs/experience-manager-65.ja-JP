---
title: タッチ操作対応 UI 機能のステータス
description: タッチ対応UI [!DNL Adobe Experience Manager] に関するリリースノートです。
translation-type: tm+mt
source-git-commit: d938f52766154b68df2f6db2c8c49a0ad97e7e6d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 48%

---


# タッチ操作対応 UI 機能のステータス {#touch-ui-feature-status}

AEM 6.4以降の [Classic UIは非推奨](../release-notes/deprecated-removed-features.md)。 Adobeでは、クラシックUIの機能はさらに強化されません。タッチ操作対応UIの強力な新機能を利用することをお勧めします。

Starting with version 6.0, AEM introduced a new user interface referred as the &quot;touch-enabled UI&quot; (simply called &quot;Touch UI&quot;) that is aligned to the [!DNL Adobe Experience Cloud] and to the overall Adobe user interface guidelines. ほぼ機能のパリティに達したので、これは従来のデスクトップ指向インターフェイスを「クラシックUI」と呼ぶのに対し、AEMの標準UIになりました。

ほとんどの機能はタッチ操作対応 UI に搭載されていますが、まだ完成せず、今後のリリースで追加される機能もあります。

次のリストは、AEM 6.5で実装された機能の現在のステータスを示しています。

For recommendations for customers that upgrade to AEM 6.5, see [User interface recommendations for customers](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>このページでは、従来のUIと機能が同等になっているだけです。 タッチ対応UIに追加され、タッチ対応UIに固有の機能で、クラシックUIには表示されません。

>[!NOTE]
>
>このリストは、完成を目指していますが、完全なものではありません。

## 凡例 {#legend}

* **完了**: この機能は、タッチ対応UIで完全に使用できます。
* **主に**: この機能は、ほとんどの場合タッチ対応UIで利用できます。
* **消失**：この機能はタッチ操作対応 UI に存在せず、この操作をおこなうにはクラシック UI を使用する必要があります。
* **置換**：この機能は動作が異なる新しい実装で置換されています。
* **削除**：この機能は、現在タッチ操作対応 UI に存在せず、置換もされません。

## 機能ステータス：サイト管理 {#feature-status-sites-admin}

This is a list of capabilities the classic UI Site Admin (`/siteadmin`) has and the status in the touch-enabled UI (`/sites.html`).

| 機能 | ステータス | コメント |
|--- |--- |--- |
| サイト階層を移動 | 完了 | AEM 6.4では、 [コンテンツツリー表示が導入されました](/help/sites-authoring/basic-handling.md#content-tree)。 |
| ワークフローを開始 | 完了 |  |
| ページを新規作成 | 完全 |  |
| サイトを新規作成 | 完全 |  |
| ローンチを新規作成 | 完全 |  |
| 新しいlivecopyを作成する | 完了 |  |
| フォルダーを作成 | 完全 |  |
| 公開ステータスを表示 | 完了 | AEM 6.5を起動すると、ワークフローのステータスがリスト表示に表示されます。 |
| 検索 | 完了 |  |
| ページのコピー&amp;ペースト(重複) | 完了 |  |
| ページを移動 | 完全 |  |
| ページを公開 | 完全 |  |
| レプリケーション権限なしでページを公開 | 完全 |  |
| 後で公開 | 完全 |  |
| ツリーを公開 | 完全 |  |
| ページを非公開 | 完全 |  |
| レプリケーション権限なしでページを非公開 | 完全 |  |
| 後で非公開 | 完了 |  |
| 削除 | 完全 |  |
| ロック／ロック解除 | 完全 |  |
| プロパティを表示／編集 | 完全 |  |
| ページに権限を設定 | 完全 |  |
| バージョン履歴 | 完了 |  |
| バージョンを復元 | 完了 |  |
| ツリーおよび削除されたページを復元 | 消失 | クラシック UI を使用します。 |
| 古いバージョンと現在のバージョンの違いを表示 | 完了 |  |
| ライブコピー操作（ロールアウト） | 完全 |  |
| 言語コピーを表示 | 完全 |  |
| 検索と置換 | 消失 | クラシック UI を使用します。 |
| 通知インボックス(JCRイベント) | 消失 | クラシック UI を使用します。別の実装で置き換えられます。 |
| 参照 | 完了 | AEM 6.5に追加された着信ページリンクの表示。 |

## 機能ステータス：ページエディター {#feature-status-page-editor}

This is a list of capabilities the classic UI Page Editor (`/cf#`) has and the status in the touch-enabled (`/editor.html`).

| 機能 | ステータス | コメント |
|--- |--- |--- |
| Web ページを編集 | 完全 |  |
| モバイル Web ページを編集 | 完了 |  |
| デザインインポーターを介して読み込んだコンテンツを編集 | 完了 |  |
| 電子メールを編集 | 完全 |  |
| ハイブリッドモバイルアプリの編集 | 完了 |  |
| フォームを編集 | 完了 |  |
| オファーを編集 | 完了 |  |
| ワークフローモデルを編集 | 完了 |  |
| モード： 編集とプレビュー | 完了 |  |
| レスポンシブプレビュー | 完了 |  |
| モード：デザインを編集 | 完全 |  |
| モード：基礎モード | 完全 |  |
| モード：ライブコピーステータス | 完了 |  |
| 注釈を追加 | 完全 |  |
| プロパティの編集 | 完了 |  |
| ロールアウトページ | 完了 |  |
| 開始と表示のワークフロー | 完了 |  |
| ワークフローパッケージの処理 | ほぼ完全 | タッチ操作対応UIから完全にアクセス可能 従来のUIでは、複数のワークフローペイロードが表示されています。 |
| ページをロック／ロック解除 | 完全 |  |
| ページを発行 | 完了 |  |
| ページを非公開 | 完全 |  |
| ページをコピー | 削除 | サイト管理を使用して[ページをコピー](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page)します。 |
| ページを移動 | 削除 | サイト管理を使用して[ページを移動](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page)します。 |
| ページを削除 | 削除 | サイト管理を使用して[ページを削除](/help/sites-authoring/managing-pages.md#deleting-a-page)します。 |
| 参照を表示 | 削除 | Use Site Admin to see the [detailed reference list](/help/sites-authoring/author-environment-tools.md#references). |
| 監査ログ | 削除 | サイト管理を使用し、[アクティビティレールを開き](/help/sites-authoring/author-environment-tools.md#events-timeline)ます。 |
| バージョンを作成 | 削除 | サイト管理を使用して[バージョンを新規作成](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version)します。 |
| バージョンを復元 | 削除 | サイト管理を使用して[バージョンを復元](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version)します。 |
| ローンチを切り替え | 削除 | サイト管理を使用して[起動を切り替え](/help/sites-authoring/launches-promoting.md)ます。 |
| ページを翻訳 | 削除 | サイト管理を使用して[翻訳プロジェクトにページを追加](/help/sites-administering/tc-manage.md)します。 |
| タイムワープ（日付／時刻を選択してその指定日時の時点のサイトを表示） | 完了 |  |
| 権限を設定 | 完全 |  |
| クライアントコンテキスト UI | 置換 | 今後は [ContextHub](/help/sites-authoring/ch-previewing.md) UI を使用します。 |
| 各種メディアタイプのコンテンツファインダー | 完了 |  |
| コンポーネントリスト | 完了 |  |
| コンポーネントのコピーと貼り付け | 完了 |  |
| クリップボード内のコンポーネントのリスト | 消失 |  |
| 取り消し／やり直し | 完全 |  |
| コンテンツをコンポーネントのプレースホルダーにドラッグ | 完了 |  |
| コンポーネントの自動作成を使用して、コンテンツをparsysプレースホルダーに直接ドラッグ | 完了 |  |

## 機能ステータス：テキスト、テーブルおよび画像エディター {#feature-status-text-table-and-image-editors}

これは、クラシックUIテキスト、テーブル、および画像エディターの機能と、タッチ対応UIのステータスのリストです。

| 機能 | ステータス | コメント |
|--- |--- |--- |
| リッチテキストエディター | 完了 | インプレイス、ダイアログ、フルスクリーンで使用できます。 |
| RTEプラグインの有効化/無効化 | 完了 | テンプレートエディターを使用して実行でき [ます](/help/sites-authoring/templates.md)。 |
| プレーンテキストにRTEを使用 | 完了 |  |
| RTEプラグイン： リンクとアンカー | 完了 |  |
| RTEプラグイン： 文字マップ | 完了 |  |
| RTEプラグイン： コピー/貼り付け | 完了 |  |
| RTEプラグイン： Microsoft Wordから貼り付け | 完了 |  |
| RTEプラグイン： 検索と置換 | 完了 |  |
| RTEプラグイン： テキスト書式（太字、...） | 完了 |  |
| RTEプラグイン： 下付き文字と上付き文字 | 完了 |  |
| RTEプラグイン： 均等配置 | 完了 |  |
| RTEプラグイン： リスト（箇条書き/数字） | 完了 |  |
| RTEプラグイン： 段落書式 | 完了 |  |
| RTEプラグイン： テキストスタイル | 完了 |  |
| RTEプラグイン： ソースエディタ（HTMLを編集） | 完了 | ダイアログとフルスクリーンでのみ使用できます。 |
| RTEプラグイン： スペルチェッカー | 完了 |  |
| RTEプラグイン： テーブル（埋め込みテーブルエディタ） | 完了 |  |
| RTEプラグイン： 取り消し/やり直し | 完了 |  |
| RTEプラグイン： インライン画像を許可する | 完了 |  |
| テーブルエディタ | 完了 | インプレイス、ダイアログ、フルスクリーンで使用できます。 |
| 画像を表のセルにドラッグ | 完了 | 使用可能なインライン |
| 画像エディター | 完了 | インプレイス、ダイアログ、フルスクリーンで使用できます。 |
| IPEプラグインの有効化/無効化 | 完了 | AEM 6.3では、テン [プレートエディターにUIが追加されました](/help/sites-authoring/templates.md)。 |
| IPEプラグイン： 切り抜き | 完了 |  |
| IPEプラグイン： 反転 | 完了 |  |
| IPEプラグイン： 取り消し/やり直し | 完了 |  |
| IPEプラグイン： 画像マップ | 完了 |  |
| IPEプラグイン： 回転 | 完了 |  |
| IPEプラグイン： ズーム | 完了 |  |

## 機能ステータス：ツール {#feature-status-tools}

これは、クラシック UI にある多様なツールおよびタッチ操作対応 UI でのステータスの一覧です。

| 機能 | ステータス | コメント |
|--- |--- |--- |
| タスク管理 | 置換 | 6.0で導入されたプロジェクトとタスク。 |
| ワークフロー受信トレイ | 完了 |  |
| ページへのワークフローテンプレートの設定(`/etc/workflow/wcm/templates.html`) | 消失 | クラシック UI を使用します。 |
| 管理UIのタグ付け | 完了 |  |
| MSM/Blueprintコントロールセンター | 完了 |  |
| Blueprint Manager UI | 完了 |  |
| ロールアウト設定UI | 消失 | クラシック UI を使用します。 |
| ユーザー、グループ、権限UI | ほとんど完了 | 高度な権限編集には、クラシックUIを使用します。 |
| Purge Versions(`/etc/versioning/purge.html`) | 消失 | クラシック UI を使用します。 |
| 外部リンクチェック (`/etc/linkchecker.html`) | 消失 | クラシック UI を使用します。 |
| バルクエディタ(`/etc/importers/bulkeditor.html`) | 消失 | クラシック UI を使用します。 |
| サムネールをアップロードして追加または上書き | 消失 | クラシック UI を使用します。 |
