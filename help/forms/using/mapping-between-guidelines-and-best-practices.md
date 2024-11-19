---
title: Forms Designer でのフォームの作成のガイドラインと最適なアクセシビリティプラクティス
description: Forms Designer でフォームを開発する際のアクセシビリティに関するベストプラクティスとガイドライン。
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 0948231a-bd9e-4d29-946d-2d8c17e27c28
source-git-commit: 16b46340c5e0775d19f22f57bca5ea9ab584c51e
workflow-type: ht
source-wordcount: '3366'
ht-degree: 100%

---

# ガイドラインとベストプラクティス間のマッピング

次の節では、リハビリテーション法第 508 条ガイドラインと WCAG ガイドラインを、このガイドで説明するベストプラクティスにマッピングしています。

## § 1194.21 ガイドラインの説明とベストプラクティス

### 第 508 条 §1194.21：ソフトウェアアプリケーションとオペレーティングシステム

| § 1194.21 ガイドライン | ガイドラインの説明 | コンプライアンスに必要な LiveCycle Designer のベストプラクティス | メモ |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| (a)  | ソフトウェアがキーボードを備えたシステム上で動作するように設計される場合、製品機能は、機能自体または機能を実行した結果を文字によって識別できるキーボードから実行可能でなければならない。 | <li> 2.7 フォームのコントロールがキーボードでアクセスできることの確認 </li><li> 2.6 読み取りとタブ順序が正しいことの確認</li> | |
| (b)  | アプリケーションは、業界標準に従って開発および文書化されたアクセシビリティ機能として特定される他の製品のアクティブ化された機能を、中断または無効にしてはならない。また、アプリケーションは、アクセシビリティ機能のアプリケーションプログラミングインターフェイスがオペレーティングシステムの製造元によって文書化され、製品開発者が使用できる場合、アクセシビリティ機能として特定されるオペレーティングシステムのアクティブ化された機能を中断または無効にしてはならない。 | LiveCycle Designer 固有のテクニックはありません。このガイドラインは PDF フォーム用の Adobe Reader で扱われます。 | |
| (c)  | 入力フォーカスの変化に応じてインタラクティブインターフェイス要素間を移動する、現在のフォーカスを示す明確に定義された画面上の表示を提供する。支援テクノロジーでフォーカスとフォーカスの変化を追跡できるように、フォーカスはプログラムで公開する。 | 2.3 適切なコントロールの選択。フォーカスが視覚的だけでなくプログラムでも公開されるようにするには、常に標準コントロールを使用する。 | |
| (d)  | 支援テクノロジーは、要素の ID、操作、状態など、ユーザーインターフェイス要素に関する十分な情報を利用できる。画像がプログラム要素を表す場合、画像によって伝えられる情報はテキストでも提供する必要がある。 | <ul><li>2.1 フォームをシンプルで使用しやすく保つ</li> <li>2.1.1 コンテンツの動き、点滅、閃光を避ける</li> <li>2.2 フォームプロパティを設定してアクセシビリティ情報を生成</li> <li>2.5 フォームのコントロールに対する正しいラベルの提供</li></ul> | |
| (e)  | コントロール、ステータスインジケーター、またはその他のプログラム要素の特定にビットマップ画像を使用する際、これらの画像に割り当てた意味を、アプリケーションのパフォーマンス全体にわたって一貫させる。 | <ul><li>2.4 画像の代替テキストの提供</li><li> 2.5 フォームのコントロールに対する適切なラベルの提供。この標準は、フォーム上の複数の場所で同じ画像を使用する場合にのみ適用されます。画像ベースのカスタムコントロールの使用はお勧めしません。代わりに、LiveCycle Designer が提供する標準コントロールのみを使用します。コントロールで画像を使用する場合は、常に一貫性のある方法で使用します。</li> | |
| (f)  | テキスト情報は、テキストを表示するオペレーティングシステム機能を通じて提供されるものとする。最小限の情報であるテキストコンテンツ、テキスト入力キャレットの場所、およびテキスト属性は使用可能する。 | 2.3 適切なコントロールの選択。画像を使用してテキスト情報を伝えることは避ける。テキストプロパティをオペレーティングシステムに適切に公開しない可能性があるカスタム入力コンポーネントを使用するのではなく、常に標準コントロールを使用します。 | |
| (g)  | アプリケーションは、ユーザーが選択したコントラストやカラーの選択、およびその他の個別の表示属性を上書きしないものとする。 | LiveCycle Designer 固有のテクニックはありません。 | 可能な限り、基本のデフォルトのシステムカラーを使用します。 |
| (h)  | アニメーションが表示される場合、情報は、ユーザーの選択により、少なくとも 1 つのアニメーション以外の表示モードで表示可能でなければならない。 | 2.1 フォームをシンプルで使用しやすく保つ。フォームでアニメーションを使用しないようにするか、アニメーションを静止画像に置き換えた別のバージョンを提供します。 | |
| (i)  | 情報を伝達したり、アクションを示したり、応答を促したり、視覚的要素を区別したりするための唯一の方法として、カラーコーディングを使用しないものとする。 | 2.8 責任を持ったカラーの使用 | |
| (j)  | 製品によって、ユーザーがカラーとコントラストの設定を調整できる場合、幅広いコントラストレベルを実現できる様々なカラーの選択肢を提供する。 | 適用なし | この機能は、通常、フォーム開発者ではなく、Adobe Reader によって提供されます。 |
| (k)  | ソフトウェアは、閃光または点滅するテキスト、オブジェクトまたはその他の要素で、閃光または点滅の周波数が 2 Hz を超え 55 Hz 未満のものを使用してはならない。 | 2.1.1 コンテンツの動き、点滅、閃光を避ける | |
| (l)  | 電子フォームが使用される場合、フォームは、支援テクノロジーを使用する人々が、フォームの完了および送信に必要な情報、フィールド要素、機能（すべての指示およびキューを含む）にアクセスできるようにする必要がある。 | 2.5 フォームのコントロールに対する正しいラベルの提供 | |

### 法第 508 条 §11942：Web ベースのイントラネットおよびインターネットの情報とアプリケーション

| §11942 ガイドライン | ガイドラインの説明 | コンプライアンスに必要な LiveCycle Designer のベストプラクティス | メモ |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| (a)  | すべてのテキスト以外の要素に相当するテキストを提供する（「alt」,「longdesc」の使用、要素コンテンツ内など）。 | 2.4 画像の代替テキストの提供 | |
| (b)  | マルチメディアプレゼンテーションに対する同等の代替手段は、プレゼンテーションと同期させる。 | 2.12 すべてのマルチメディアコンテンツにアクセスできることの確認 | |
| (c)  | Web ページは、色で伝えられるすべての情報を、カラーなしでも（例えば、コンテキストやマークアップから）利用できるように設計する必要がある。 | 2.8 責任を持ったカラーの使用 | |
| (d)  | ドキュメントは、関連するスタイルシートを必要とせずに読み取れるように整理する。 | 適用なし | |
| (e)  | サーバーサイド画像マップの各アクティブ領域には冗長テキストリンクを提供する。 | 適用なし | |
| (f)  | 使用可能な幾何学図形で領域を定義できない場合を除き、サーバーサイド画像マップの代わりにクライアントサイド画像マップを提供する。 | 適用なし | |
| (g)  | データテーブルの行および列ヘッダーを識別する。 | 2.9 テーブルの見出しセルの指定 | |
| (h)  | マークアップは、2 つ以上の論理レベルの行ヘッダーまたは列ヘッダーを持つデータテーブルのデータセルとヘッダーセルを関連付けるために使用される。 | 2.9 テーブルの見出しセルの指定 | |
| (i)  | フレームには、フレームの特定とナビゲーションを容易にするテキストでタイトルを付ける。 | 適用なし | |
| (j)  | ページは、2Hz ～ 55Hz の周波数で画面がちらつくことを避けるように設計する。 | 2.1 フォームをシンプルで使用しやすく保つ | |
| (k)  | 他の方法でコンプライアンスを達成できない場合は、web サイトをこのパートの規定に準拠させるために、同等の情報または機能を備えたテキストのみのページを提供する。テキストのみのページのコンテンツは、プライマリページが変更されるたびに更新する。 | 適用なし | |
| (l)  | ページがスクリプト言語を使用してコンテンツを表示したり、インターフェイス要素を作成したりする場合、スクリプトによって提供される情報は、支援テクノロジーで読み取ることができる機能的なテキストで識別する。 | 2.11 中断を伴うスクリプトの作成の回避 | |
| (m) | Web ページに、ページコンテンツを解釈するためにクライアントシステム上にアプレット、プラグイン、またはその他のアプリケーションが存在することが必要な場合、そのページは §1194.21(a)～(l) に準拠するプラグインまたはアプレットへのリンクを提供する。 | 適用なし | PDF フォームにリンクする web ページには、Adobe Reader へのリンクを提供する必要があります。 |
| (n) | 電子フォームがオンラインで記入されるように設計されている場合、フォームは、支援テクノロジーを使用する人々が、すべての指示と合図を含む、フォームの記入と送信に必要な情報、フィールド要素、および機能にアクセスできるようにする必要がある。 | 2.5 フォームのコントロールに対する正しいラベルの提供 | |
| (o) | ユーザーが繰り返し表示されるナビゲーションリンクをスキップできるようにする方法を提供する。 | 2.10 ナビゲート可能なフォーム構造の指定 | |
| (p) | 時間制限のある応答が必要な場合は、ユーザーに警告し、より多くの時間が必要であることを示すのに十分な時間を与える。 | 2.11 中断を伴うスクリプトの作成の回避 | |

### WCAG 1.0 優先度 1 チェックポイント

| チェックポイント | チェックポイントの説明 | コンプライアンスに必要な LiveCycle Designer のベストプラクティス | メモ |
|------------|------------------------|-----------------------------------------------------------|-------|
| [1.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-text-equivalent) | テキスト以外のすべての要素に相当するテキストを提供する（「alt」、「longdesc」の使用、要素コンテンツ内など）。これには、画像、テキストのグラフィック表現（シンボルを含む）、イメージマップ領域、アニメーション（GIF のアニメーションなど）、アプレットとプログラムのオブジェクト、アスキーアート、フレーム、スクリプト、リストの箇条書きとして使用される画像、スペーサー、グラフィックボタン、サウンド（ユーザー操作の有無に関係なく再生）、スタンドアロンのオーディオファイル、ビデオのオーディオトラック、およびビデオが含まれます。 | <ul><li>2.4 画像の代替テキストの提供</li> <li>2.12 すべてのマルチメディアコンテンツにアクセスできることの確認</li> | |
| [1.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-redundant-server-links) | サーバーサイド画像マップの各アクティブ領域には冗長テキストリンクを提供する。 | 適用なし | |
| [1.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-auditory-descriptions) | ユーザーエージェントでビジュアルトラックのテキスト相当部分を自動的に読み上げられるようになるまでは、マルチメディアプレゼンテーションのビジュアルトラックの重要な情報について、音声による説明を提供する。 | 2.12 すべてのマルチメディアコンテンツにアクセスできることの確認 | |
| [1.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-synchronize-equivalents) | 時間ベースのマルチメディアプレゼンテーション（映画やアニメーションなど）の場合は、同等の代替手段（ビジュアルトラックのキャプションや音声による説明など）をプレゼンテーションと同期する。 | 2.12 すべてのマルチメディアコンテンツにアクセスできることの確認 | |
| [2.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-convey) | 色で伝えられるすべての情報を、色なしでも（例えば、コンテキストやマークアップから）利用できるようにする。 | 2.8 責任を持ったカラーの使用 | |
| [4.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-changes) | ドキュメントのテキストの自然言語と同等のテキスト（キャプションなど）の変更を明確に特定する。 | 2.13 言語の変更の特定 | |
| [5.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-headers) | データテーブルの場合は、行ヘッダーと列ヘッダーを識別する。 | 2.9 テーブルの見出しセルの指定 | |
| [5.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-structure) | 2 つ以上の論理レベルの行ヘッダーまたは列ヘッダーを持つデータテーブルの場合は、マークアップを使用してデータセルとヘッダーセルを関連付ける | 2.9 テーブルの見出しセルの指定 | |
| [6.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-order-style-sheets) | スタイルシートなしで読み取ることができるようにドキュメントを整理する。例えば、HTML ドキュメントが関連付けられたスタイルシートなしでレンダリングされた場合でも、ドキュメントを読み取ることができる必要がある。 | 適用なし | |
| [6.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-dynamic-source) | 動的コンテンツを変更した際に、動的コンテンツと同等のものが更新されるようにする。 | 2.11 中断を伴うスクリプトの作成の回避 | |
| [6.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-scripts) | スクリプト、アプレット、その他のプログラムによるオブジェクトがオフになっている場合やサポートされていない場合は、ページを使用できるようにする。できない場合は、アクセシブルな代替ページで同等の情報を提供する。 | 2.11 中断を伴うスクリプトの作成の回避 | |
| [7.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-flicker) | ユーザーエージェントでユーザーがちらつきを制御できるようになるまでは、画面でちらつきが発生するのを回避する。 | 2.1 フォームをシンプルで使用しやすく保つ | |
| [9.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-client-side-maps) | 使用可能な図形で領域を定義できない場合を除き、サーバーサイド画像マップの代わりにクライアントサイド画像マップを提供する。 | 適用なし | |
| [11.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-alt-pages) | 最適な方法でアクセシブルなページを作成できない場合は、W3C テクノロジーを使用し、アクセシブルで、同等の情報（または機能）を持ち、アクセシブルでない（元の）ページと同じ頻度で更新される代替ページへのリンクを提供する。 | 適用なし | |
| [12.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-titles) | 各フレームには、フレームの特定とナビゲーションを容易にするタイトルを付ける。 | 適用なし | |
| [14.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-simple-and-straightforward) | サイトのコンテンツに適した、最も明確で最も単純な言葉を使用する。 | 2.1 フォームをシンプルで使用しやすく保つ | |

### WCAG 1.0 優先度 2 チェックポイント

| 優先度 2 チェックポイント | チェックポイントの説明 | コンプライアンスに必要な LiveCycle のベストプラクティス | メモ |
|------------|------------------------|-------------------------------------------------|-------|
| [2.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-contrast) | 色覚障害のあるユーザーが閲覧する際や、白黒の画面で表示した際に、前景と背景色の組み合わせによって十分なコントラストが提供されるようにする。[画像の優先度 2、テキストの優先度 3]。 | 2.8 責任を持ったカラーの使用 | |
| [3.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-markup) | 適切なマークアップ言語が存在する場合は、画像ではなくマークアップを使用して情報を伝える。 | <ul><li>2.1 フォームをシンプルで使用しやすく保つ</li><li> 2.1.1 コンテンツの動き、点滅、閃光を避ける</li> <li>2.2 アクセシビリティ情報を生成するためのフォームプロパティの設定。テキストの画像ではなく、常に実際のテキストを使用します。</li> | |
| [3.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-grammar) | 公開された正式な文法に準拠するドキュメントを作成する。 | | PDF フォームは、Adobe Reader でレンダリングするには、公開済みの PDF 仕様に一致している必要があります。 |
| [3.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-style-sheets) | スタイルシートを使用して、レイアウトとプレゼンテーションを制御する。 | 適用なし | |
| [3.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-relative-units) | マークアップ言語の属性値とスタイルシートのプロパティ値には、絶対単位ではなく相対単位を使用する。 | 適用なし | |
| [3.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-logical-headings) | ヘッダー要素を使用してドキュメント構造を伝え、仕様に従って使用する。 | 2.10 ナビゲート可能なフォーム構造の指定 | |
| [3.6](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-list-structure) | リストとリスト項目を適切にマークアップする。 | 2.10.3 リストのマークアップ。リストとリスト項目の役割を使用して、リストベースのコンテンツをリストとしてマークアップします。 | |
| [3.7](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-quotes) | 引用符をマークアップする。インデントなどの書式設定効果に引用符マークアップを使用しない。 | 適用なし | |
| [5.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-table-for-layout) | テーブルを線形化しても意味が通らない場合、レイアウトにテーブルを使用しない。それ以外の場合、テーブルが意味をなさない場合は、同等の代替テーブル（線形化されたバージョンなど）を提供する。 | LiveCycle 固有のテクニックはありません | LiveCycle フォームのレイアウトでテーブルを使用する理由はありません。代わりに、レイアウトパレットを使用して、フォームフィールドをグリッドパターンで配置します。テーブルヘッダーなどのテーブル固有の機能を使用する場合にのみテーブルを使用します。 |
| [5.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-layout) | レイアウトにテーブルを使用する場合は、視覚的な書式設定の目的で構造マークアップを使用しない。 | LiveCycle 固有のテクニックはありません | |
| [6.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable-scripts) | スクリプトとアプレットの場合、イベントハンドラーが入力デバイスに依存しないことを確認する。 | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| [6.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-fallback-page) | 動的コンテンツにアクセシブルであるか、代替のプレゼンテーションまたはページを提供する。 | 2.11 中断を伴うスクリプトの作成の回避 | |
| [7.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-blinking) | ユーザーエージェントでユーザーが点滅を制御できるようになるまでは、コンテンツの点滅（オンとオフの切り替えなど、一定の速度で表示を変更する）を回避する。 | 2.1 フォームをシンプルで使用しやすく保つ | |
| [7.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-movement) | ユーザーエージェントでユーザーが動きのあるコンテンツを停止できるようになるまでは、ページ内の動きを回避する。 | 2.1 フォームをシンプルで使用しやすく保つ | |
| [7.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-periodic-refresh) | ユーザーエージェントが更新を停止する機能を提供するまでは、定期的に自動更新されるページを作成しない。 | 適用なし | |
| [7.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-auto-forward) | ユーザーエージェントが自動リダイレクトを停止する機能を提供するまでは、マークアップを使用してページを自動的にリダイレクトしない。代わりに、リダイレクトを実行するようにサーバーを設定する。 | 適用なし | |
| [8.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-directly-accessible) | スクリプトやアプレットなどのプログラム要素を直接アクセシブルにするか、支援テクノロジーと互換性を持たせる。[機能が重要であり、他の場所で提示されていない場合は優先度 1、それ以外の場合は優先度 2。] | 2.11 中断を伴うスクリプトの作成の回避 | |
| [9.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable) | 独自のインターフェイスを持つ要素が、デバイスに依存しない方法で操作できることを確認する。 | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| [9.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-device-independent-events) | スクリプトの場合は、デバイスに依存するイベントハンドラーではなく、論理イベントハンドラーを指定する。 | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| [10.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-pop-ups) | ユーザーエージェントが、ユーザーが起動したウィンドウをオフにするまでは、ポップアップやその他のウィンドウを表示したり、ユーザーに通知せずに現在のウィンドウを変更したりしないようにする。 | 2.11 中断を伴うスクリプトの作成の回避 | |
| [10.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-unassociated-labels) | ユーザーエージェントがラベルとフォームコントロール間の明示的な関連付けをサポートするまでは、暗黙的に関連付けられたラベルを持つすべてのフォームコントロールについて、ラベルが適切に配置されていることを確認する。 | 2.5 フォームのコントロールに対する正しいラベルの提供 | |
| [11.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-latest-w3c-specs) | W3C テクノロジーが使用可能でタスクに適している場合は使用し、サポートされている場合は最新バージョンを使用する。 | 適用なし | |
| [11.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-deprecated) | W3C テクノロジーの廃止された機能の使用を避ける。 | 適用なし | |
| [12.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-longdesc) | フレームのタイトルだけでは明確でない場合は、フレームの目的とフレームの関係を説明する。 | 適用なし | |
| [12.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-group-information) | 大きな情報ブロックを、自然で適切な、より管理しやすいグループに分割する。 | 2.10 ナビゲート可能なフォーム構造の指定 | |
| [12.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-associate-labels) | ラベルとコントロールを明示的に関連付ける。 | 2.5 フォームのコントロールに対する正しいラベルの提供 | |
| [13.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-meaningful-links) | 各リンクのターゲットを明確に識別する。 | 2.5 フォームのコントロールに対する正しいラベルの提供 2.5.6 リンクテキストの設定 | |
| [13.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-metadata) | ページやサイトにセマンティック情報を追加するためのメタデータを提供する。 | 適用なし | |
| [13.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-site-description) | サイトの一般的なレイアウトに関する情報（サイトマップや目次など）を提供する。 | 2.10 ナビゲート可能なフォーム構造の指定 | |
| [13.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-clear-nav-mechanism) | 一貫した方法でナビゲーションメカニズムを使用する。 | 2.10 ナビゲート可能なフォーム構造の指定 | マスターページを使用して、一貫性のあるナビゲーションコンテンツを作成する。 |

### WCAG 2.0 達成基準

| 優先度 1 G 2 チェックポイント | コンプライアンスに必要な LiveCycle のベストプラクティス | メモ |
| --- | --- | --- |
| 1.1 [代替テキスト](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv.html) | | |
| 1.1.1 [テキスト以外のコンテンツ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html) | 2.4 画像の代替テキストの提供 | |
| | 2.5 フォームのコントロールに対する正しいラベルの提供 | |
| 1.2 [時間依存メディア](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv.html) | | |
| 1.2.1 [音声のみおよび映像のみ（収録済み）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることの確認 | |
| 1.2.2 [キャプション（収録済み）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることの確認 | |
| 1.2.3 [音声解説または代替メディア（収録済み）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることの確認 | |
| 1.2.4 [キャプション（ライブ）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることの確認 | |
| 1.2.5 [音声解説（収録済み）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることの確認 | |
| 1.2.6 [手話（収録済み）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-sign.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることの確認 | |
| 1.2.7 [拡張音声解説（収録済み）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-extended-ad.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることの確認 | |
| 1.2.8 [代替メディア（収録済み）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-text-doc.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることの確認 | |
| 1.2.9 [音声のみ（ライブ）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-live-audio-only.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることの確認 | |
| 1.3 [適応可能](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation.html) | | |
| 1.3.1 [情報と関係性](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html) | 2.9 テーブルの見出しセルの指定 | |
| 1.3.2 [意味のあるシーケンス](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-sequence.html) | 2.6 読み取りとタブ順序が正しいことの確認 | |
| | 2.10 ナビゲート可能なフォーム構造の指定 | |
| 1.3.3 [感覚的な特徴](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html) | 2.8 責任を持ったカラーの使用 | |
| 1.4 [判別可能](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast.html) | | |
| 1.4.1 [色の使用](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html) | 2.8 責任を持ったカラーの使用 | |
| 1.4.2 [音声の制御](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-dis-audio.html) | LiveCycle 固有のテクニックはありません | |
| 1.4.3 [コントラスト（最低限）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) | 2.8 責任を持ったカラーの使用 | |
| 1.4.4 [テキストのサイズ変更](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html) | LiveCycle 固有のテクニックはありません | |
| 1.4.5 [文字画像](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html) | LiveCycle 固有のテクニックはありません | |
| 1.4.6 [コントラスト（高度）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) | 2.8 責任を持ったカラーの使用 | |
| 1.4.7 [小さな背景音、又は背景音なし](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-noaudio.html) | LiveCycle 固有のテクニックはありません | |
| 1.4.9 [文字画像（例外なし）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-images.html) | LiveCycle 固有のテクニックはありません | |
| 2.1 [キーボード操作可能](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation.html) | | |
| 2.1.1 [キーボード](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html) | 2.6 読み取りとタブ順序が正しいことの確認 | |
| | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| 2.1.2 [キーボードトラップなし](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-trapping.html) | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| 2.1.3 [キーボード（例外なし）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-all-funcs.html) | 2.6 読み取りとタブ順序が正しいことの確認 | |
| | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| 2.2 [十分な時間](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) | | |
| 2.2.1 [タイミング調整可能](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-required-behaviors.html) | LiveCycle 固有のテクニックはありません | |
| 2.2.2 [一時停止、停止、非表示](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html) | 2.1 フォームをシンプルで使用しやすく保つ | |
| 2.2.3 [タイミングなし](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) | LiveCycle 固有のテクニックはありません | |
| 2.2.4 [中断](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) | LiveCycle 固有のテクニックはありません | |
| 2.2.5 [再認証](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-server-timeout.html) | LiveCycle 固有のテクニックはありません | |
| 2.3 [発作] | | |
| 2.3.1 [3 回の閃光、またはしきい値以下](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html) | 2.1 フォームをシンプルで使用しやすく保つ | |
| 2.3.2 [3 回の閃光](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-three-times.html) | 2.1 フォームをシンプルで使用しやすく保つ | |
| 2.4 [ナビゲーション可能](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms.html) | | |
| 2.4.1 [ブロックのスキップ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html) | 2.10 ナビゲート可能なフォーム構造の指定 | |
| 2.4.2 [ページタイトル](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html) | LiveCycle 固有のテクニックはありません | |
| 2.4.3 [フォーカス順序](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-order.html) | 2.6 読み取りとタブ順序が正しいことの確認 | |
| 2.4.4 [リンクの目的（コンテキスト内）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html) | LiveCycle 固有のテクニックはありません | リンクの目的は、リンクされた要素に対して意味のあるテキストを作成者が選択するかどうかによって異なります。 |
| 2.4.5 [複数の手段](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-mult-loc.html) | 2.10 ナビゲート可能なフォーム構造の指定 | |
| 2.4.6 [見出しおよびラベル](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-descriptive.html) | <ul><li>2.5 フォームのコントロールに対する正しいラベルの提供</li><li>2.10 ナビゲート可能なフォーム構造の指定</li> | |
| 2.4.7 [フォーカスの可視化](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-visible.html) | LiveCycle 固有のテクニックはありません | LiveCycle フォームのデフォルトのフォーカスが表示されます。 |
| 2.4.8 [場所](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-location.html) | LiveCycle 固有のテクニックはありません | 適用なし：LiveCycle フォームにはナビゲーション システムは必要ありません。 |
| 2.4.9 [リンクの目的（リンクのみ）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-link.html)  | LiveCycle 固有のテクニックはありません | リンクの目的は、リンクされた要素に対して意味のあるテキストを作成者が選択するかどうかによって異なります。 |
| 2.4.10 [セクション見出し](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-headings.html) | 2.10 ナビゲート可能なフォーム構造の指定 | |
| 3.1 [読み取り可能](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning.html) | | |
| 3.1.1 [ページの言語](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html) | 2.13 自然言語と言語の変更の特定 | |
| 3.1.2 [一部分の言語](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html) | 2.13 自然言語と言語の変更の特定 | |
| 3.1.3 [一般的ではない用語](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-idioms.html) | LiveCycle 固有のテクニックはありません | |
| 3.1.4 [略語](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-located.html) | LiveCycle 固有のテクニックはありません | |
| 3.1.5 [読解レベル](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-supplements.html) | LiveCycle 固有のテクニックはありません | |
| 3.1.6 [発音](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-pronunciation.html) | LiveCycle 固有のテクニックはありません | |
| 3.2 [予測可能](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior.html) | | |
| 3.2.1 [フォーカス時](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-receive-focus.html) | 2.11 中断を伴うスクリプトの作成の回避 | |
| 3.2.2 [入力時](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-unpredictable-change.html) | 2.11 中断を伴うスクリプトの作成の回避 | |
| 3.2.3 [一貫したナビゲーション](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-locations.html) | 2.10 ナビゲート可能なフォーム構造の指定 | |
| 3.2.4 [一貫した識別性](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-functionality.html) | <ul><li>2.3 適切なコントロールの選択</li><li>2.5 フォームのコントロールに対する正しいラベルの提供</li> | |
| 3.2.5 [リクエストに応じた変化](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-no-extreme-changes-context.html) | 2.11 中断を伴うスクリプトの作成の回避 | |
| 3.3 [入力支援](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error.html) | | |
| 3.3.1 [エラーの特定](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-identified.html) |  | LiveCycle Designer には、フォームフィールドを必須としてマークするツールや、フォームの入力検証を実行するツールが用意されています。 |
| 3.3.2 [ラベルまたは説明](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html) | 2.5 フォームのコントロールに対する正しいラベルの提供 | |
| 3.3.3 [エラー修正の提案](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-suggestions.html) |  | LiveCycle Designer には、フォームフィールドを必須としてマークするツールや、フォームの入力検証を実行するツールが用意されています。 |
| 3.3.4 [エラー回避（法務、金融、データ）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible.html) | LiveCycle 固有のテクニックはありません | |
| 3.3.5 [ヘルプ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-context-help.html) | LiveCycle 固有のテクニックはありません | |
| 3.3.6 [エラー回避（すべて）](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible-all.html) | LiveCycle 固有のテクニックはありません | |
| 4.1 [互換性](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat.html) | | |
| 4.1.1 [構文解析](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-parses.html) | LiveCycle 固有のテクニックはありません | |
| 4.1.2 [名前、役割、値](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-rsv.html) | <ul><li>2.3 適切なコントロールの選択</li> <li>2.5 フォームのコントロールに対する正しいラベルの提供</li> | |
