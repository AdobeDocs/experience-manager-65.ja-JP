---
title: ページの差分
seo-title: Page Diff
description: ページの差分表示を使用すると、2 つのページを並べて比較し、差分をハイライト表示できます。
seo-description: The page diff feature allows for the convenient side-by-side comparison of two pages with their differences highlighted.
uuid: 5af8b466-5922-4fe6-9eae-7bad99be23e0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8386a16a-9d47-46d5-bc60-5f290c59e60e
docset: aem65
exl-id: 3beea5cd-5ae0-485b-8dfc-8b3a23c11586
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 96%

---

# ページの差分 {#page-diff}

## はじめに {#introduction}

コンテンツ作成は反復的なプロセスです。効率的なオーサリングでは、ある反復から他の反復で何が変化したかを知る必要があります。あるページバージョンを見てから別のページバージョンを見るのは非効率的であり、エラーが発生しやすくなります。ある作成者が、現在のページを他のバージョンと並べて簡単に比較できるようにしたいと考えます。

ページの差分表示を使用すると、2 つのページを並べて比較し、差分をハイライト表示できます。

>[!TIP]
>
>この機能の技術的詳細については、[開発とページの差分](/help/sites-developing/pagediff.md#operation-details)を参照してください。

## 使用方法 {#use}

並列比較による差分表示では、次のものを比較できます。

* [バージョン](/help/sites-authoring/working-with-page-versions.md#comparing-a-version-with-current-page) - ページの以前のバージョンとその現在の状態
* [ライブコピー](/help/sites-administering/msm-livecopy.md#comparing-a-live-copy-page-with-a-blueprint-page) - ライブコピーとそのブループリント
* [ローンチ](/help/sites-authoring/launches-editing.md#comparing-a-launch-page-to-its-source-page) - ローンチとそのソース
* [言語コピー](/help/sites-administering/tc-manage.md#comparing-language-copies) - （再）翻訳前と（再）翻訳後のページ

それらのコンテキスト内で差分の確認を開始する方法については、それぞれのトピックを参照してください。

### 差分の表示 {#presentation-of-differences}

比較対象のコンテンツに関わらず、差分の表示は同じです。

* 差分の確認を開始したときに選択されたコンテンツが左側に表示されます（差分のエントリポイント）。
* 比較対象のコンテンツが右側に表示されます（選択されたコンテンツの比較対象となるもの）。

例えば、バージョンを比較する場合、現在のバージョンが左側に表示され、以前のバージョンが右側に表示されます。

両方のページのソースは、ブラウザーウィンドウ上部のヘッダーバーにはっきりと表示されます。

![ヘッダーに表示されるソース](assets/chlimage_1-109.png)

差分によりコンポーネントおよび HTML レベルの変更が検出されます。変更された項目は、異なる色でハイライト表示されます。

**コンポーネントの変更点**

* ライトグリーン - 追加されたコンポーネント
* ピンク - 削除されたコンポーネント

**HTML の変更点**

* ダークグリーン - 追加された HTML
* 赤 - 削除された HTML

>[!NOTE]
>
>言語コピーを比較する場合は、翻訳ですべてが変更され、強調表示をしても意味がないので、強調表示は無効になります。

### 全画面表示および終了 {#fullscreen-and-exiting}

特定のコンテンツに集中するには、並列比較による差分表示のいずれかの「サイド」の全画面表示アイコンをクリックすると、ブラウザーの全画面に拡大することができます。

![全画面モード](do-not-localize/chlimage_1-18.png)

選択されたサイドが画面全体に表示されますが、バーは上部に残るので、2 枚のページを切り替えることができます。

![上部のバーを使用して、ページを切り替えることができます](assets/chlimage_1-110.png)

また全画面表示を終了するアイコンをクリックして、全画面表示を閉じることができます。

![全画面を閉じる](do-not-localize/chlimage_1-19.png)

ヘッダーの「閉じる」ボタンをクリックすることで、並列比較による差分表示はいつでも終了することができます。

## 制限事項 {#limitations}

ページの差分表示で期待どおりに差分が検出されない場合があります。

* バージョンおよびローンチが異なるとき、差分は、パンくずリスト、メニュー、製品リスト、ロゴなどのダイナミックコンポーネント（コンテンツを表示する際にサイト構造に依存するコンポーネント）を考慮しません。
* バージョンの差分表示では、アクセスコントロールポリシーおよびライブコピー関係は再現されません。
* ページを移動すると、移動前に作成したバージョンとの差分を実行できなくなります。

   * 差分で問題が発生した場合は、ページの[タイムライン](/help/sites-authoring/basic-handling.md#timeline)を調べて、ページを移動したかどうかを確認します。

>[!NOTE]
>
>バージョンを互いに比較することはできません。 比較できるのは、現在のバージョンと古いバージョンの組み合わせだけです。変更の強調表示は、必ず現在のバージョンに対しておこなわれます。

>[!NOTE]
>
>ページ差分メカニズムの仕組みおよびページ差分に影響を与える可能性のある制限事項の詳細については、この機能の[開発者向けドキュメント](/help/sites-developing/pagediff.md)を参照してください。
