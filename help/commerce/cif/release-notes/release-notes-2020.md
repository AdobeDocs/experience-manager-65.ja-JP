---
title: AEM Content and Commerce リリースノート 2020
description: Adobe Experience Manager Content and Commerce リリースノート 2020.
exl-id: 440ecd8e-55dc-4606-8678-c65cda1d2b3a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 68%

---

# コマース統合フレームワーク GitHub リリースの概要

## リリース日： 2020 年 11 月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.6.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.6.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 参照サイト | 2020.12.01 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-november}

* 特定のカテゴリページに追加されたテンプレートの継承。 この機能により、すべてのサブカテゴリが特定のトップカテゴリ用に作成されたテンプレートを継承できるので、ビジネスユーザーの効率が向上します。

* Venia 参照用ストアフロントが更新されて、フッターにエクスペリエンスフラグメントを使用できるようになりました。ビジネスユーザーは、AEMオーサリングツールを使用してページフッターを編集できます。

### 改善点 {#what-is-improved-november}

* チェックアウトコンポーネントが改善され、買い物客が宛先の国に入って、米国以外の請求先/配送先住所を許可できるようになりました。

* ナビゲーションコンポーネントが拡張されて、Adobe クライアントデータレイヤーが改善されました。

* 複数のバグ修正。

## リリース日： 2020 年 10 月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.5.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.5.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 参照サイト | 2020.10.27 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-october}

* ビジネスユーザーがAEMコンテンツページにこのコンポーネントをドラッグ&amp;ドロップして、コマースデータを使用してコンテンツページをエンリッチメントできるようにする、新しいカテゴリカルーセルコンポーネントが追加されました。

* CIF コアコンポーネントが拡張され、コマースデータを送信してアドビクライアントのデータレイヤーを強化できるようになりました。Adobeクライアントデータレイヤーは、データを収集し、そのデータを Digital Analytics およびレポートサーバーと通信するための標準化された方法です。 詳しくは、 [Adobeクライアントデータレイヤー](https://github.com/adobe/adobe-client-data-layer/wiki).

* Adobe Commerce 管理 UI 内で設定された SEO メタデータ（タイトル、メタ説明、メタキーワードなど）を自動的に入力するように、製品の詳細ページと製品リストページが拡張されました。

* コマースティーザーコンポーネントのバグを修正しました。

## リリース日：2020年9月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.4.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.4.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 参照サイト | 2020.10.2 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-september}

* Adobe Commerce 2.4.0 スキーマのクエリをサポートします。

* アカウント情報の機能が追加され、買い物客が個人情報を更新できるようになりました。

* 製品リストページと検索結果ページに遅延読み込みのページネーションスタイルが実装され、開発者は、「さらに読み込む」ボタンをページネーションスタイルとして表示するようにこれらのコンポーネントを設定できます。

* パスワードリセットページは、買い物客がアカウントのパスワードを更新/リセットできるように実装されています。

* バンドルされた製品タイプのサポートを利用できます。

* 開発者は、製品カルーセル、関連製品およびおすすめカテゴリリストコンポーネントの HTML タグを、SEO のベストプラクティスに従うように設定できます。

* マイアカウントのバグを修正しました。

* 複数のバグ修正。

## リリース日： 2020 年 8 月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.3.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.3.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 参照サイト | 2020.9.2 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-august}

* コンテンツページとコマースページをサポートするパンくずコンポーネントが追加されました。

* コマースタブがページプロパティに追加され、ランディングページとエクスペリエンスフラグメントの CIF プロパティを表示できるようになりました。

* 検索バーコンポーネントが改善され、プレースホルダーテキストを表示するオプションがサポートされるようになりました

* 製品コンポーネントおよび製品ティーザーコンポーネントの柔軟性が向上し、容易にカスタマイズできるようになりました。

* 製品ティーザーコンポーネントのデフォルトの CTA ボタンラベルを上書きおよび設定できる柔軟性を追加しました。

* アドレス帳コンポーネントが改善され、登録済みの買い物客がチェックアウト時にアドレス帳に保存された配送先住所と請求先住所を選択できるようになりました。

* 複数のバグ修正。

## リリース日：2020年7月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.2.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.2.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF Venia 参照サイト | 2020.8.14 | [リリースノート](https://github.com/adobe/aem-cif-guides-venia/releases) |

### 新機能 {#what-is-new-july}

* CIF Venia 参照サイトが CIF アーキタイプリポジトリーから抽出され、スタンドアロンの GitHub リポジトリーになりました。

* CIF アーキタイプを AEM プロジェクトアーキタイプと統合しました。新規プロジェクトの場合は、 [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)を開始点として使用します。

* アドレス帳管理が追加され、サインインしたユーザーがアドレスを管理できるようになりました。

* CIF クラウド設定 UI では、公開／非公開アクションをサポートしています。

### 改善点 {#what-is-improved-july}

* ログインコンポーネントにユーザードロップダウンに移動して、簡単にアクセスできるようにしました。

* aem-core-cif-react-components パッケージを簡略化しました。

* 複数のバグ修正。

## リリース日：2020年6月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.1.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.1.1 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF アーキタイプ | 0.11.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-june}

これは、Adobe Experience Manager でサポートされている CIF コアコンポーネントの最初のバージョンです。

* 製品リストページと検索結果ページに製品の並べ替えを追加し、買い物客が関連度、価格、製品名に基づいて並べ替えられるようにしました。

* カテゴリフィルタリングの方法を追加し、買い物客がカテゴリに基づいてフィルタリングできるようにしました。

* ACL を直接操作するのではなく、サービスユーザーを介して /conf に確実にアクセスできるように、サービスユーザーマッピングをセキュリティ要件の一環として追加しました。CIF コアコンポーネントは、設定にアクセスする際に、サービスユーザーを使用しなければならなくなりました。

### 改善点 {#what-is-improved-june}

* 製品リストページと検索結果ページに、項目の合計数が表示されます。 買い物客が適用したフィルターが更新されると、項目数が更新されます。

* ファセット検索は、カテゴリクエリと製品検索クエリを組み合わせることで最適化されます。

* ページプレビュー用のカテゴリ／製品ピッカーが cq:catalogPath に従います。

* 複数のバグ修正。

## リリース日：2020年5月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 1.0.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 1.0.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF アーキタイプ | 0.11.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-may}

* Adobe Commerce 2.3.5 スキーマのクエリをサポートします。

* ファセット検索のサポートが検索ページと製品リストページに追加され、買い物客が製品ファセットに基づいて検索結果をフィルタリングできるようになりました。

* SEO 用に PDP/PLP URL をカスタマイズするための新しい OSGi サービスが追加されました。 詳しくは、 [ドキュメント](https://github.com/adobe/aem-core-cif-components).

* クラウド設定の作成時に、製品バインディングが自動的に作成されます。

### 改善点

* 「フォルダーを作成」アクションを表示するようにクラウド設定が拡張されました。

* 複数のバグ修正が適用されました。

## リリース日：2020年4月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 0.10.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 0.10.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF アーキタイプ | 0.10.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-april}

* CIF Connector の設定は統合され、シンプル化されています。 詳しくは、 [はじめに](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=ja) または[新しい AEM CIF プロジェクト設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=ja)を参照してください。

### 改善点 {#what-is-improved-april}

* 登録済みの買い物客をサポートするように、買い物かごとチェックアウトフローが拡張されました。

* すべてのコンポーネントに対して、国際化サポートが拡張されました。

* グループ化された製品と仮想製品のサポートを利用できます。

* 関連製品、製品カルーセルおよびおすすめカテゴリの各コンポーネントが改善されて、オプションのタイトルをサポートするようになりました。

* 複数のバグ修正が適用されました。

## リリース日：2020年2月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 0.9.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 0.9.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF アーキタイプ | 0.9.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-february}

* Adobe Commerce 2.3.4 スキーマのクエリをサポートします。

* カテゴリピッカーに検索のサポートが追加されました。

* 大きなカタログセットをサポートするための、カテゴリリストコンポーネント内のページネーション。

### 改善点 {#what-is-improved-february}

* 割引を表示するように、買い物かごが強化されました。

* 製品の詳細、製品ティーザー、製品リストの各コンポーネントは、高度な価格情報の表示をサポートしています。

* 製品コンソールと製品ピッカーの製品検索が改善されました。

* 複数のバグ修正が適用されました。

## リリース日：2020年1月

| GitHub | バージョン | 詳細なリリースノート |
|:-------|:-----:|---------------------:|
| CIF コネクタ | 0.8.0 | [リリースノート](https://github.com/adobe/commerce-cif-connector/releases) |
| CIF コアコンポーネント | 0.8.0 | [リリースノート](https://github.com/adobe/aem-core-cif-components/releases) |
| CIF アーキタイプ | 0.7.0 | [リリースノート](https://github.com/adobe/aem-cif-project-archetype/releases) |

### 新機能 {#what-is-new-january}

* 顧客がコマースプロジェクトで XF を作成できるように、エクスペリエンスフラグメント（XF）コンポーネントが追加されました。

* 自分のアカウントで使用可能なパスワード機能を変更します。

* AEM CIF サーバーサイドコアコンポーネントで i18n（インターナショナライゼーション）がサポートされます。

* 汎用の関連製品コンポーネントを使用できます。

### 改善点 {#what-is-improved-january}

* 製品ティーザーで CTA ボタンの表示をサポートします。

* おすすめカテゴリリストコンポーネントの画像を変更または選択するオプションが追加されました。

* 製品リストコンポーネントでタイトル／バナーを表示／非表示にするオプションが追加されました。

* 製品カルーセルコンポーネントに適用されたドラッグ&amp;ドロップ機能。

* 複数のバグ修正が適用されました。
