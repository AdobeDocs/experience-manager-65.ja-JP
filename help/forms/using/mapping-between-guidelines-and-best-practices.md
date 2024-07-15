---
title: Forms Designer でフォームを作成するためのガイドラインとアクセシビリティに関するベストプラクティス
description: Forms designer でフォームを開発する際のアクセシビリティに関するベストプラクティスとガイドライン。
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 38fb132f0eb5b710745db11e7ddf59efc0f0ae95
workflow-type: tm+mt
source-wordcount: '3366'
ht-degree: 2%

---

# ガイドラインとベストプラクティス間のマッピング

以下の節では、508 条と WCAG のガイドラインを、このガイドで説明するベストプラクティスにマッピングしています。

## § 1194.21 ガイドラインの説明とベストプラクティス

### 第 508 条§1194.21：ソフトウェアアプリケーションとオペレーティングシステム

| § 1194.21 ガイドライン | ガイドラインの説明 | コンプライアンスのために必要なLiveCycleDesignerのベストプラクティス | 備考 |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| イ | ソフトウェアがキーボードを備えたシステム上で動作するように設計される場合、製品機能は、機能自体または機能を実行した結果を文字によって識別できるキーボードから実行可能でなければならない。 | <li> 2.7 フォームのコントロールがキーボードでアクセスできることの確認 </li><li> 2.6 読み取りとタブの順序が正しいことを確認する</li> | |
| ロ | アプリケーションは、アクセシビリティ機能として特定された他の製品のアクティブ化された機能を、業界標準に従って開発および文書化された場所で、中断または無効化してはなりません。 また、アプリケーションは、アクセシビリティ機能として識別されたオペレーティング システムのアクティブ化された機能を中断または無効化してはなりません。これらのアクセシビリティ機能のアプリケーション プログラミング インターフェイスは、オペレーティング システムの製造元によって文書化されており、製品開発者が使用できる状態になっています。 | LiveCycleのDesigner固有のテクニックはありません。このガイドラインは、PDF forms向けのAdobe Readerで処理されます。 | |
| ハ | 入力フォーカスの変化に応じてインタラクティブインターフェイス要素間を移動する、現在のフォーカスを示す明確に定義された画面上の表示が提供されなければならない。 フォーカスは、支援テクノロジーがフォーカスとフォーカスの変化を追跡できるように、プログラム的に公開する必要があります。 | 2.3 適切なコントロールを選択するフォーカスがプログラム的にも視覚的にも確実に公開されるようにするには、常に標準のコントロールを使用します。 | |
| ニ | 支援テクノロジーは、要素の ID、操作、状態など、ユーザーインターフェイス要素に関する十分な情報を利用できる必要があります。 画像がプログラム要素を表す場合は、画像によって伝えられる情報もテキストで使用できる必要があります。 | <ul><li>2.1 フォームをシンプルで使いやすくします</li> <li>2.1.1 コンテンツの移動、点滅、閃光を避ける</li> <li>2.2 フォームプロパティを設定してアクセシビリティ情報を生成する</li> <li>2.5 フォームのコントロールに対する正しいラベルの提供</li></ul> | |
| ホ | ビットマップ画像を使用してコントロール、ステータス インジケータ、またはその他のプログラム要素を識別する場合、これらの画像に割り当てられる意味は、アプリケーションのパフォーマンス全体で一貫していなければなりません。 | <ul><li>2.4 画像の代替テキストの提供</li><li> 2.5 フォームのコントロールに対して適切なラベルを提供するこの規格は、フォーム上の複数の場所で同じ画像を使用する場合にのみ適用されます。 画像ベースのカスタムコントロールの使用はお勧めしません。 代わりに、LiveCycleDesignerが提供する標準のコントロールのみを使用します。 コントロール内で画像を使用する場合は、常に一貫性のある方法で使用するようにしてください。</li> | |
| （へ） | テキスト情報は、テキストを表示するためのオペレーティングシステム機能を通じて提供されるものとします。 使用可能にする必要のある最小限の情報は、テキストコンテンツ、テキスト入力キャレットの場所およびテキスト属性です。 | 2.3 適切なコントロールを選択する画像を使用してテキスト情報を伝えないようにします。 テキストプロパティをオペレーティングシステムに正しく公開しない可能性のあるカスタム入力コンポーネントを使用するのではなく、常に標準コントロールを使用します。 | |
| （g） | アプリケーションは、ユーザーが選択したコントラストおよび色の選択、およびその他の個々の表示属性を上書きしないものとします。 | LiveCycleDesigner固有のテクニックがありません | 可能な限り、基本のデフォルトのシステムカラーを使用します。 |
| （チ） | アニメーションが表示される場合、情報は、ユーザの選択により、少なくとも 1 つの非アニメーション表示モードで表示可能でなければならない。 | 2.1 フォームをシンプルで使いやすいものにするフォームでアニメーションを使用しないようにするか、アニメーションを静的な画像に置き換える別のバージョンを提供します。 | |
| （1） | 色分けは、情報を伝達する、行動を示す、応答を促す、または視覚的要素を区別する唯一の方法として使用してはならない。 | 2.8 責任を持って色を使用 | |
| （ヌ） | 製品がユーザーに色とコントラストの設定を調整することを許可する場合、様々なコントラストレベルを生成できる様々な色の選択が提供されなければならない。 | 適用なし | この機能は、通常、フォーム開発者ではなく、Adobe Readerによって提供されます。 |
| （か） | ソフトウェアは、閃光または点滅するテキスト、オブジェクトまたはその他の要素で、閃光または点滅の周波数が 2 Hz を超え 55 Hz 未満のものを使用してはなりません。 | 2.1.1 コンテンツの移動、点滅、閃光を避ける | |
| （五十） | 電子フォームが使用される場合、フォームは、支援テクノロジーを使用する人々が、フォームの完了および送信に必要な情報、フィールド要素、機能（すべての指示およびキューを含む）にアクセスできるようにする必要があります。 | 2.5 フォームのコントロールに対する正しいラベルの提供 | |

### 第 508 条§11942:Web ベースのイントラネットおよびインターネットの情報とアプリケーション

| §11942 ガイドライン | ガイドラインの説明 | コンプライアンスのために必要なLiveCycleDesignerのベストプラクティス | 備考 |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| イ | テキスト以外のすべての要素に相当するテキストを提供する（「alt」、「longdesc」を介して、または要素コンテンツ内で）。 | 2.4 画像の代替テキストの提供 | |
| ロ | マルチメディア プレゼンテーションに対する同等の代替手段は、プレゼンテーションと同期されなければならない。 | 2.12 すべてのマルチメディアコンテンツにアクセスできるようにする | |
| ハ | Web ページは、色で伝えられるすべての情報が、例えばコンテキストやマークアップなどから、色なしで利用できるように設計する必要があります。 | 2.8 責任を持って色を使用 | |
| ニ | 文書は，関連するスタイルシートを必要とすることなく，読み取り可能なように整理しなければならない。 | 適用なし | |
| ホ | サーバーサイド画像マップのアクティブな領域ごとに冗長なテキストリンクを提供する必要があります。 | 適用なし | |
| （へ） | 利用可能な幾何学的形状で領域を定義できない場合を除き、サーバーサイドのイメージマップの代わりにクライアントサイドのイメージマップを提供する。 | 適用なし | |
| （g） | データテーブルの行および列ヘッダーを識別する必要があります。 | 2.9 表の見出しセルの提供 | |
| （チ） | マークアップは、2 つ以上の論理レベルの行見出しまたは列見出しを持つデータ テーブルのデータ セルとヘッダーセルを関連付けるために使用する必要があります。 | 2.9 表の見出しセルの提供 | |
| （1） | フレームには，フレーム識別及びナビゲーションを容易にする文字を付さなければならない。 | 適用なし | |
| （ヌ） | ページは、2 Hz を超え 55 Hz 未満の周波数で画面がちらつくのを避けるように設計する必要があります。 | 2.1 フォームをシンプルで使いやすくします | |
| （か） | 他の方法では準拠を達成できない場合は、同等の情報または機能を持つテキストのみのページを提供し、web サイトがこの部分の規定に準拠するようにします。 テキストのみのページのコンテンツは、プライマリページが変更されるたびに更新されます。 | 適用なし | |
| （五十） | ページがコンテンツの表示やインターフェイス要素の作成にスクリプト言語を使用する場合、スクリプトから提供される情報は、支援テクノロジーで読み取ることができる機能テキストで識別される必要があります。 | 2.11 中断を伴うスクリプト作成を避ける | |
| （わ） | Web ページで、ページコンテンツを解釈するためにアプレット、プラグイン、またはその他のアプリケーションがクライアントシステムに存在する必要がある場合、ページは、§1194.21 （a）から（l）に準拠するプラグインまたはアプレットへのリンクを提供する必要があります。 | 適用なし | PDF formsにリンクする web ページには、Adobe Readerへのリンクを指定する必要があります。 |
| （n） | 電子フォームがオンラインで完成するように設計される場合、フォームは、支援テクノロジーを使用する人々が、フォームの完成と送信に必要な情報、フィールド要素、機能（すべての指示とキューを含む）にアクセスできるようにする必要があります。 | 2.5 フォームのコントロールに対する正しいラベルの提供 | |
| （o） | ユーザが繰り返しナビゲーション・リンクをスキップすることを可能にする方法が提供されなければならない。 | 2.10 ナビゲーション可能なフォーム構造を提供する | |
| （タ） | 時間制限のある応答が必要な場合、ユーザーに警告を発し、より多くの時間が必要であることを示すのに十分な時間を与えます。 | 2.11 中断を伴うスクリプト作成を避ける | |

### WCAG 1.0 Priority 1 チェックポイント

| チェックポイント | チェックポイントの説明 | コンプライアンスのために必要なLiveCycleDesignerのベストプラクティス | 備考 |
|------------|------------------------|-----------------------------------------------------------|-------|
| [1.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-text-equivalent) | テキスト以外のすべての要素に相当するテキストを指定します（「alt」、「longdesc」の使用、要素コンテンツなど）。 これには、イメージ、テキストのグラフィカル表現（シンボルを含む）、イメージマップ領域、アニメーション（GIFのアニメーションなど）、アプレットとプログラムのオブジェクト、アスキーアート、フレーム、スクリプト、リストブレットとして使用されるイメージ、スペーサー、グラフィカルボタン、サウンド（ユーザーの操作の有無に関係なく再生）、スタンドアロンオーディオファイル、ビデオのオーディオトラック、およびビデオが含まれます。 | <ul><li>2.4 画像の代替テキストの提供</li> <li>2.12 すべてのマルチメディアコンテンツにアクセスできるようにする</li> | |
| [1.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-redundant-server-links) | サーバーサイド画像マップの各アクティブな領域に冗長なテキストリンクを提供します。 | 適用なし | |
| [1.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-auditory-descriptions) | ユーザーエージェントが視覚的なトラックに相当するテキストを自動的に読み上げるまで、マルチメディアプレゼンテーションの視覚的なトラックの重要な情報を聴覚的に説明します。 | 2.12 すべてのマルチメディアコンテンツにアクセスできるようにする | |
| [1.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-synchronize-equivalents) | 時間ベースのマルチメディアプレゼンテーション（例：映画またはアニメーション）の場合は、同等の代替手段（例：視覚的なトラックのキャプションや聴覚的な説明）をプレゼンテーションと同期させます。 | 2.12 すべてのマルチメディアコンテンツにアクセスできるようにする | |
| [21](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-convey) | 色で伝えられるすべての情報を、色なしで（例えばコンテキストやマークアップから）利用できるようにしてください。 | 2.8 責任を持って色を使用 | |
| [41](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-changes) | ドキュメントのテキストの自然言語の変化と、それに相当するテキスト（キャプションなど）の変化を明確に識別する。 | 2.13 言語の変更の特定 | |
| [51](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-headers) | データテーブルの場合は、行ヘッダーと列ヘッダーを特定します。 | 2.9 表の見出しセルの提供 | |
| [52](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-structure) | 行見出しまたは列見出しの論理レベルが 2 つ以上あるデータ テーブルでは、マークアップを使用してデータ セルと見出しセルを関連付けます。 | 2.9 表の見出しセルの提供 | |
| [61](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-order-style-sheets) | ドキュメントを整理して、スタイルシートなしで読み取れるようにします。 例えば、HTMLドキュメントが関連付けられたスタイルシートなしでレンダリングされる場合でも、そのドキュメントを読み取ることができる必要があります。 | 適用なし | |
| [62](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-dynamic-source) | 動的コンテンツが変更された場合は、動的コンテンツに相当するものが更新されます。 | 2.11 中断を伴うスクリプト作成を避ける | |
| [6.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-scripts) | スクリプト、アプレット、その他のプログラムによるオブジェクトの表示がオフになっている場合やサポートされていない場合は、ページを使用できるようにします。 それが不可能な場合は、アクセス可能な別のページで同等の情報を提供します。 | 2.11 中断を伴うスクリプト作成を避ける | |
| [71](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-flicker) | ユーザーエージェントでユーザーのちらつきを制御できるようになるまで、画面のちらつきを回避します。 | 2.1 フォームをシンプルで使いやすくします | |
| [91](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-client-side-maps) | サーバーサイドの画像マップの代わりに、クライアントサイドの画像マップを提供します。ただし、領域を使用可能な幾何学的形状で定義できない場合を除きます。 | 適用なし | |
| [114](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-alt-pages) | 最適な方法でアクセス可能なページを作成できず、W3C テクノロジーを使用し、アクセス可能で、同等の情報（または機能）を持ち、アクセスできない（元の）ページと同じ頻度で更新される代替ページへのリンクを提供できない場合。 | 適用なし | |
| [121](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-titles) | フレームの識別とナビゲーションを容易にするために、各フレームにタイトルを付けます。 | 適用なし | |
| [141](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-simple-and-straightforward) | サイトのコンテンツに適した、最も明確で最も単純な言語を使用します。 | 2.1 フォームをシンプルで使いやすくします | |

### WCAG 1.0 の優先度 2 のチェックポイント

| 優先度 2 チェックポイント | チェックポイントの説明 | コンプライアンスに必要なLiveCycleのベストプラクティス | 備考 |
|------------|------------------------|-------------------------------------------------|-------|
| [22](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-contrast) | 色不足のあるユーザーが表示した場合や、白黒の画面で表示した場合は、前景色と背景色の組み合わせによって十分なコントラストが提供されるようにします。 [ 画像の優先度 2、テキストの優先度 3]。 | 2.8 責任を持って色を使用 | |
| [31](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-markup) | 適切なマークアップ言語が存在する場合は、情報を伝えるために画像ではなくマークアップを使用してください。 | <ul><li>2.1 フォームをシンプルで使いやすくします</li><li> 2.1.1 コンテンツの移動、点滅、閃光を避ける</li> <li>2.2 アクセシビリティ情報を生成するためのフォームプロパティの設定テキストの画像ではなく、常に実際のテキストを使用します。</li> | |
| [32](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-grammar) | 公開された形式文法に合わせて検証するドキュメントを作成します。 | | Adobe Readerでレンダリングするには、PDF formsが公開済みのPDF仕様と一致する必要があります。 |
| [33](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-style-sheets) | スタイルシートを使用して、レイアウトと表示を制御します。 | 適用なし | |
| [34](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-relative-units) | マークアップ言語の属性値とスタイルシートのプロパティ値には、絶対単位ではなく相対単位を使用します。 | 適用なし | |
| [35](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-logical-headings) | ヘッダー要素を使用してドキュメント構造を伝え、仕様に従って使用します。 | 2.10 ナビゲーション可能なフォーム構造を提供する | |
| [36](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-list-structure) | リストおよびリスト項目を適切にマークアップします。 | 2.10.3 リストのマークアップ リストベースのコンテンツを、リストおよびリスト項目の役割を使用してリストとしてマークアップします。 | |
| [37](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-quotes) | 見積をマークアップします。 インデントなどの書式設定効果に引用符マークアップを使用しないでください。 | 適用なし | |
| [53](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-table-for-layout) | 線形化したときにテーブルが意味を成さない限り、レイアウトにテーブルを使用しないでください。 そうしないと、テーブルが意味を成さない場合は、同等の代替手段（線形化バージョンの可能性あり）を提供します。 | 特別なLiveCycle方法はない | LiveCycleフォームでレイアウトにテーブルを使用する理由はありません。 代わりに、レイアウトパレットを使用して、グリッドパターン内にフォームフィールドを配置します。 テーブルヘッダーなど、テーブル固有の機能を利用する場合にのみ、テーブルを使用します。 |
| [54](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-layout) | テーブルがレイアウトに使用されている場合は、視覚的な書式設定を目的として構造マークアップを使用しないでください。 | 特別なLiveCycle方法はない | |
| [6.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable-scripts) | スクリプトおよびアプレットの場合は、イベント ハンドラーが入力デバイスに依存していないことを確認してください。 | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| [6.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-fallback-page) | 動的コンテンツがアクセス可能であること、または代替のプレゼンテーションやページを提供していることを確認します。 | 2.11 中断を伴うスクリプト作成を避ける | |
| [72](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-blinking) | ユーザーエージェントでユーザーが点滅を制御できるようになるまでは、コンテンツを点滅させないようにします（例えば、オンとオフを切り替えるなど、一定の割合でプレゼンテーションを変更する）。 | 2.1 フォームをシンプルで使いやすくします | |
| [73](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-movement) | ユーザーエージェントでユーザーが移動コンテンツの凍結を許可するまでは、ページ内の移動を避けてください。 | 2.1 フォームをシンプルで使いやすくします | |
| [74](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-periodic-refresh) | ユーザーエージェントが更新を停止する機能を提供するまで、自動更新ページを定期的に作成しないでください。 | 適用なし | |
| [75](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-auto-forward) | ユーザーエージェントが自動リダイレクトを停止する機能を提供するまでは、ページの自動的なリダイレクトにマークアップを使用しないでください。 代わりに、リダイレクトを実行するようにサーバーを設定します。 | 適用なし | |
| [81](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-directly-accessible) | スクリプトやアプレットなどのプログラム要素を直接アクセスできるようにしたり、支援テクノロジーと互換性を持たせたりします [ 機能が重要で他の場所には提示されない場合は優先度 1、それ以外の場合は優先度 2]。 | 2.11 中断を伴うスクリプト作成を避ける | |
| [920](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable) | 独自のインターフェイスを持つ要素を、デバイスに依存しない方法で操作できることを確認します。 | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| [930](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-device-independent-events) | スクリプトの場合は、デバイスに依存するイベント・ハンドラではなく、論理イベント・ハンドラを指定します。 | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| [101](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-pop-ups) | ユーザーエージェントが、ユーザーが起動したウィンドウをオフにするまで、ポップアップやその他のウィンドウを表示せず、ユーザーに通知せずに現在のウィンドウを変更しないでください。 | 2.11 中断を伴うスクリプト作成を避ける | |
| [102](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-unassociated-labels) | ユーザーエージェントがラベルとフォームコントロールの明示的な関連付けをサポートするまで、暗黙的にラベルが関連付けられたすべてのフォームコントロールに対して、ラベルが正しい位置に配置されていることを確認します。 | 2.5 フォームのコントロールに対する正しいラベルの提供 | |
| [111](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-latest-w3c-specs) | W3C テクノロジーは、利用可能かつタスクに適している場合は使用し、サポートされている場合は最新のバージョンを使用します。 | 適用なし | |
| [112](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-deprecated) | W3C テクノロジーの非推奨（廃止予定）の機能を回避する。 | 適用なし | |
| [1220](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-longdesc) | フレームの目的とフレームの関係を、フレームタイトルだけでは明確でない場合は説明します。 | 適用なし | |
| [123](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-group-information) | 情報の大きなブロックを、自然で適切な、より管理しやすいグループに分割します。 | 2.10 ナビゲーション可能なフォーム構造を提供する | |
| [124](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-associate-labels) | ラベルをコントロールに明示的に関連付けます。 | 2.5 フォームのコントロールに対する正しいラベルの提供 | |
| [131](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-meaningful-links) | 各リンクのターゲットを明確に識別します。 | 2.5 フォームのコントロールに対する正しいラベルの提供 2.5.6 リンクテキストの提供 | |
| [132](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-metadata) | ページやサイトに意味情報を追加するメタデータを提供する。 | 適用なし | |
| [133](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-site-description) | サイトの一般的なレイアウトに関する情報（サイトマップや目次など）を提供します。 | 2.10 ナビゲーション可能なフォーム構造を提供する | |
| [134](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-clear-nav-mechanism) | 一貫した方法でナビゲーションメカニズムを使用します。 | 2.10 ナビゲーション可能なフォーム構造を提供する | マスターページを使用して、一貫性のあるナビゲーションコンテンツを作成します。 |

### WCAG 2.0 成功基準

| 優先度 1 G 2 のチェックポイント | コンプライアンスに必要なLiveCycleのベストプラクティス | 備考 |
| --- | --- | --- |
| 1.1 [ 代替テキスト ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv.html) | | |
| 1.1.1 [ テキスト以外のコンテンツ ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html) | 2.4 画像の代替テキストの提供 | |
| | 2.5 フォームのコントロールに対する正しいラベルの提供 | |
| 1.2 [ 時間ベースのメディア ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv.html) | | |
| 1.2.1 [ 音声のみおよび映像のみ（収録済み） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることを確認する | |
| 1.2.2 [ キャプション（収録済み） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることを確認する | |
| 1.2.3 [ 音声解説または代替メディア（収録済み） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることを確認する | |
| 1.2.4[ キャプション（ライブ） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることを確認する | |
| 1.2.5 [ 音声解説（収録済み） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることを確認する | |
| 1.2.6 [ 手話（収録済み） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-sign.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることを確認する | |
| 1.2.7 [ 拡張音声解説（収録済み） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-extended-ad.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることを確認する | |
| 1.2.8 [ 代替メディア（収録済み） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-text-doc.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることを確認する | |
| 1.2.9[ 音声のみ（ライブ） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-live-audio-only.html) | 2.12 すべてのオーディオおよびビデオコンテンツにアクセスできることを確認する | |
| 1.3 [ 適応可能 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation.html) | | |
| 1.3.1 [ 情報と関係性 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html) | 2.9 表の見出しセルの提供 | |
| 1.3.2 [ 意味のあるシーケンス ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-sequence.html) | 2.6 読み取りとタブの順序が正しいことを確認する | |
| | 2.10 ナビゲーション可能なフォーム構造を提供する | |
| 1.3.3 [ 感覚的な特徴 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html) | 2.8 責任を持って色を使用 | |
| 1.4[ 判別可能 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast.html) | | |
| 1.4.1 [ 色の使用 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html) | 2.8 責任を持って色を使用 | |
| 1.4.2 [ 音声の制御 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-dis-audio.html) | 特別なLiveCycle方法はない | |
| 1.4.3[ コントラスト（最低限） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) | 2.8 責任を持って色を使用 | |
| 1.4.4 [ テキストのサイズ変更 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html) | 特別なLiveCycle方法はない | |
| 1.4.5 [ 文字画像 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html) | 特別なLiveCycle方法はない | |
| 1.4.6[ コントラスト（強調） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) | 2.8 責任を持って色を使用 | |
| 1.4.7[ 低い、またはバックグラウンド音声なし ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-noaudio.html) | 特別なLiveCycle方法はない | |
| 1.4.9 [ 文字画像（例外なし） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-images.html) | 特別なLiveCycle方法はない | |
| 2.1 [ キーボードによるアクセス ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation.html) | | |
| 2.1.1 [ キーボード ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html) | 2.6 読み取りとタブの順序が正しいことを確認する | |
| | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| 2.1.2 [ キーボードトラップなし ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-trapping.html) | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| 2.1.3 [ キーボード（例外なし） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-all-funcs.html) | 2.6 読み取りとタブの順序が正しいことを確認する | |
| | 2.7 フォームのコントロールがキーボードでアクセスできることの確認 | |
| 2.2[ 十分な時間 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) | | |
| 2.2.1 [ タイミング調整可能 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-required-behaviors.html) | 特別なLiveCycle方法はない | |
| 2.2.2 [ 一時停止、停止、非表示 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html) | 2.1 フォームをシンプルで使いやすくします | |
| 2.2.3 [ タイミングなし ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) | 特別なLiveCycle方法はない | |
| 2.2.4[ 中断 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) | 特別なLiveCycle方法はない | |
| 2.2.5[ 再認証 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-server-timeout.html) | 特別なLiveCycle方法はない | |
| 2.3[ 発作 ] | | |
| 2.3.1[3Flashまたはしきい値以下 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html) | 2.1 フォームをシンプルで使いやすくします | |
| 2.3.2 [3 つのFlash](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-three-times.html) | 2.1 フォームをシンプルで使いやすくします | |
| 2.4[ ナビゲート可能 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms.html) | | |
| 2.4.1 [ ブロックのバイパス ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html) | 2.10 ナビゲーション可能なフォーム構造を提供する | |
| 2.4.2 [ ページタイトル ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html) | 特別なLiveCycle方法はない | |
| 2.4.3 [ フォーカス順序 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-order.html) | 2.6 読み取りとタブの順序が正しいことを確認する | |
| 2.4.4[ リンクの目的（コンテキスト内） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html) | 特別なLiveCycle方法はない | リンクの目的は、リンクされた要素に対して意味のあるテキストを作成者が選択するかどうかによって異なります。 |
| 2.4.5[ 複数の手段 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-mult-loc.html) | 2.10 ナビゲーション可能なフォーム構造を提供する | |
| 2.4.6 [ 見出しおよびラベル ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-descriptive.html) | <ul><li>2.5 フォームのコントロールに対する正しいラベルの提供</li><li>2.10 ナビゲーション可能なフォーム構造を提供する</li> | |
| 2.4.7[ フォーカスの可視化 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-visible.html) | 特別なLiveCycle方法はない | LiveCycleフォームのデフォルトのフォーカスは表示されています。 |
| 2.4.8[ 場所 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-location.html) | 特別なLiveCycle方法はない | 該当なし：ナビゲーションフォームにはLiveCycleシステムは必要ありません。 |
| 2.4.9[ リンクの目的（リンクのみ） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-link.html) | 特別なLiveCycle方法はない | リンクの目的は、リンクされた要素に対して意味のあるテキストを作成者が選択するかどうかによって異なります。 |
| 2.4.10 [ セクション見出し ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-headings.html) | 2.10 ナビゲーション可能なフォーム構造を提供する | |
| 3.1[ 読み取り可能 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning.html) | | |
| 3.1.1 [ ページの言語 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html) | 2.13 自然言語および言語の変化を特定する | |
| 3.1.2 [ 一部分の言語 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html) | 2.13 自然言語および言語の変化を特定する | |
| 3.1.3 [ 変わった言葉 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-idioms.html) | 特別なLiveCycle方法はない | |
| 3.1.4[ 略語 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-located.html) | 特別なLiveCycle方法はない | |
| 3.1.5[ 読み取りレベル ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-supplements.html) | 特別なLiveCycle方法はない | |
| 3.1.6 [ 発音 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-pronunciation.html) | 特別なLiveCycle方法はない | |
| 3.2[ 予測可能 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior.html) | | |
| 3.2.1[ フォーカス時 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-receive-focus.html) | 2.11 中断を伴うスクリプト作成を避ける | |
| 3.2.2 [ 入力時 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-unpredictable-change.html) | 2.11 中断を伴うスクリプト作成を避ける | |
| 3.2.3 [ 一貫したナビゲーション ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-locations.html) | 2.10 ナビゲーション可能なフォーム構造を提供する | |
| 3.2.4 [ 一貫性のある識別 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-functionality.html) | <ul><li>2.3 適切なコントロールの選択</li><li>2.5 フォームのコントロールに対する正しいラベルの提供</li> | |
| 3.2.5 [ リクエストに応じた変更 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-no-extreme-changes-context.html) | 2.11 中断を伴うスクリプト作成を避ける | |
| 3.3[ 入力支援 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error.html) | | |
| 3.3.1 [ エラーの特定 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-identified.html) |  | LiveCycleDesignerには、フォームフィールドを必須としてマークし、フォームの入力検証を実行するためのツールが用意されています。 |
| 3.3.2 [ ラベルまたは説明 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html) | 2.5 フォームのコントロールに対する正しいラベルの提供 | |
| 3.3.3 [ エラー修正 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-suggestions.html) |  | LiveCycleDesignerには、フォームフィールドを必須としてマークし、フォームの入力検証を実行するためのツールが用意されています。 |
| 3.3.4 [ エラー回避（法務、金融、データ） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible.html) | 特別なLiveCycle方法はない | |
| 3.3.5[ ヘルプ ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-context-help.html) | 特別なLiveCycle方法はない | |
| 3.3.6 [ エラー回避（すべて） ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible-all.html) | 特別なLiveCycle方法はない | |
| 4.1[ 互換性あり ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat.html) | | |
| 4.1.1 [ 構文解析 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-parses.html) | 特別なLiveCycle方法はない | |
| 4.1.2[ 名前、役割、値 ](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-rsv.html) | <ul><li>2.3 適切なコントロールの選択</li> <li>2.5 フォームのコントロールに対する正しいラベルの提供</li> | |



