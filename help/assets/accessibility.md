---
title: ' [!DNL Adobe Experience Manager Assets] のアクセシブルな機能およびインターフェイス'
description: 障がいを持つユーザーにとって  [!DNL Adobe Experience Manager] 6.5 [!DNL Assets]  のアクセシビリティ機能がどのように役立つかを説明します。
contentOwner: AG
feature: Asset Management
role: User, Developer, Leader
exl-id: 15555941-99a2-4586-8d7b-b22f3ec17805
solution: Experience Manager, Experience Manager Assets
source-git-commit: 3524c1e6d299576ac9691292fb29eb0cf8a48bc2
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 56%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, and so on.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, and so on.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# [!DNL Adobe Experience Manager Assets] のアクセシビリティ機能 {#accessibility-in-aem-assets}

[!DNL Adobe Experience Manager] を使用すると、コンテンツクリエーターやコンテンツパブリッシャーが素晴らしいエクスペリエンスを Web 上で提供できます。Adobeは、[!DNL Experience Manager] のアクセシビリティを向上させることによって、障害のあるクリエイターを含めるよう努めています。 ソフトウェアは、すべてのタイプのユーザーのニーズに合わせて継続的に強化されています。 視覚障害、聴覚障害、運動障害またはその他の障害を持つ個人を対象とした世界標準に準拠しています。

[!DNL Experience Manager] では、準拠する標準規格、製品のアクセシビリティ機能の概要、準拠レベルを記載した準拠情報を公開しています。アクセシビリティ準拠レポートは、様々な標準規格への準拠レベルを [!DNL Experience Manager] ユーザーが理解するうえで役に立ちます。[!DNL Assets] で行われた機能強化により、すべてのユーザーがキーボード、スクリーンリーダー、拡大鏡などの支援テクノロジーを使用して、インターフェイスを容易に使用できるようになりました。

[!DNL Experience Manager] は、次の標準規格を様々なレベルでサポートしています。

* [Web Content Accessibility Guidelines（WCAG）2.1](https://www.w3.org/TR/wcag/)
* [米国リハビリテーション法改正 508 条](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)
* [W3C の Web Accessibility Initiative による WAI-ARIA（アクセシブルリッチインターネットアプリケーション）仕様](https://www.w3.org/WAI/standards-guidelines/aria/)
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)

準拠レベルの詳細を記載したレポートについては、[アクセシビリティ準拠レポート](https://www.adobe.com/accessibility/compliance.html)（ACR）のページを参照してください。

[!DNL Dynamic Media] のアクセシビリティについて詳しくは、「[ [!DNL Dynamic Media]](/help/assets/accessibility-dm.md) のアクセシビリティ」を参照してください。

## 支援テクノロジー {#at-support}

障害を持つユーザーは、Web コンテンツにアクセスしたりソフトウェア製品を使用したりする際に、多くの場合、ハードウェアとソフトウェアを利用します。これらのツールは、支援テクノロジーと呼ばれます。[!DNL Experience Manager Assets] では、ユーザーがソフトウェアの主要機能を使用する際に、次の種類の支援テクノロジー（AT）と連携動作できます。

* スクリーンリーダーと拡大鏡
* 音声認識ソフトウェア
* キーボードの使用 - ナビゲーションとショートカット
* スイッチコントロール、更新可能な点字ディスプレイ、その他のコンピュータ入力デバイスを含む支援ハードウェア
* UI 拡大ツール

## アクセシブルな [!DNL Experience Manager Assets] の使用例  {#accessible-assets-use-cases}

[!DNL Experience Manager] のアクセシビリティ機能は、[!DNL Experience Manager] ユーザーとその顧客の 2 つの主要な要件に対応しています。

* コンテンツデザイナーやクリエーターには、アクセシブルなコンテンツを作成して公開する機能が提供されます。作成されたコンテンツは、顧客や web サイト訪問者によって使用されます。障がいを持つユーザーは、支援テクノロジーを活用してコンテンツを利用します。詳しくは、「[Web アクセシビリティのガイドライン ](/help/managing/web-accessibility.md)」を参照してください。
* [!DNL Experience Manager] た、障害を持つユーザーや管理者は、コンテンツの作成と管理を行うためのユーザーインターフェイスやコントロールにアクセスできます。 障害を持つユーザーは、支援テクノロジーを使用して、[!DNL Assets] 機能をナビゲート、使用、管理できます。

[!DNL Assets] の主な機能は以前よりもアクセスしやすく、定期的にアップデートされており、グローバル標準への準拠が改善されています。[!DNL Assets] の CRUD 操作には、ある程度のアクセシビリティが組み込まれています。 アセットの追加、管理、検索、配布などの DAM ワークフローには、キーボードショートカット、スクリーンリーダーテキスト、カラーコントラストなどの支援を受けてアクセスできます。

## キーボードの使用のサポート {#keyboard-use}

ポインターでクリックやアクション操作が可能な多くのユーザーインターフェイス要素は、キーボードを使用してを操作することもできます。 キーボードを使用して UI 要素にフォーカスし、適切なアクションを実行できます。ユーザーは、UI 要素に集中したり、キーボードを使用してトリガーを設定したりしなくても、直接キーボードショートカットを使用してコマンドやアクションをトリガーできます。 例えば、ユーザーインターフェイスの左側で、アセットのタイムラインを開くことができます。 キーボードを使用してユーザーインターフェイスコントロールを参照し、`Return` を選択して、キーボードショートカット `Alt + 2` 選択します。

<!-- TBD items:

* The option to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into 'basic handling' info aka article to 'understand and use the workspace'. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the options like delete tag? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets] のキーボードショートカット  {#keyboard-shortcuts}

[!DNL Assets] の下記のアクションは、一覧に示したキーボードショートカットで動作します。[!DNL Experience Manager] コンソールに適用されるほとんどのキーボードショートカットは、[!DNL Assets] にも適用されます。詳しくは、[コンソールのキーボードショートカット](/help/sites-authoring/keyboard-shortcuts.md#keyboard-shortcuts)を参照してください。キーボードショートカットを[有効または無効にする方法](/help/sites-authoring/keyboard-shortcuts.md#deactivating-keyboard-shortcuts)を参照してください。

| ユーザーインターフェイスまたはシナリオ | キーボードショートカット | アクション |
|---|---|---|
| [!DNL Assets] ユーザーインターフェイスの列表示 | 上向き矢印キーと下向き矢印キー | 同じ階層内のファイルやフォルダーに移動します。 |
| [!DNL Assets] ユーザーインターフェイスの列表示 | 左向き矢印キーと右向き矢印キー | 現在のフォルダーの上または下のファイルとフォルダーに移動します。 |
| [!DNL Assets] 内のフォルダーの参照 | `/` | オムニサーチボックスを開いて、検索を呼び出します。 |
| [!DNL Assets] コンソール | &grave; | サイドパネルを切り替えます。 |
| [!DNL Assets] コンソール | `Alt + 1` | コンテンツツリーを開きます。 |
| [!DNL Assets] コンソール | `Alt + 2` | 左側のパネルで[!UICONTROL ナビゲーション]を開きます。 |
| [!DNL Assets] コンソール | `Alt + 3` | 選択したアセットの [!UICONTROL  タイムライン ] を表示します。 |
| [!DNL Assets] コンソール | `Alt + 4` | 選択したアセットのライブコピーの参照を開きます。 |
| [!DNL Assets] コンソール | `Alt + 5` | 検索を開始し、選択したフォルダー内を検索します。 |
| アセットまたはフォルダーが選択されている | Backspace | 選択したアセットまたはフォルダーを削除します。 |
| アセットまたはフォルダーが選択されている | `p` | 選択したアセットのプロパティ ページを開きます。 |
| アセットまたはフォルダーが選択されている | `e` | 選択したアセットを編集します。 |
| アセットまたはフォルダーが選択されている | `m` | 選択したアセットを移動します。 |
| アセットまたはフォルダーが選択されている | `Ctrl + c` | 選択したアセットをコピーします。 |
| アセットまたはフォルダーが選択されている | `Esc` | 選択をキャンセルします。 |
| ダイアログボックスが開き、フォーカスが移動します | `Esc` | ダイアログボックスを閉じます。 |
| DAM 内のフォルダー内 | `Ctrl + v` | コピーしたアセットを貼り付けます。 |
| [!DNL Assets] コンソール | `Ctrl + A` | すべてのアセットを選択します。 |
| アセットプロパティページ | `Ctrl + S` | 変更を保存します。 |
| [!DNL Assets] コンソール | `?` | キーボードショートカットのリストを表示します。 |

## ログインと [!DNL Assets] ユーザーインターフェイスの操作 {#login}

ユーザーは、キーボードを使用してログインフィールドに移動し情報を入力してログインすることができます。 スクリーンリーダーは、ユーザーが誤ったユーザー名とパスワードの組み合わせを入力するたびに、ログインページ上のエラーメッセージを読み上げます。

ログイン後、DAM ユーザーはキーボードを使用して [!DNL Assets] ユーザーインターフェイス内を移動できます。 左側のパネル、メニュー、ユーザープロファイル、検索バー、ファイルとフォルダー、管理および設定などのユーザーインターフェイス要素は、キーボードを使用してナビゲートできます。キーボードのナビゲーション順序は、左から右、上から下です。ユーザーがキーボードを使用して操作すると、UI で、カラーコントラストが向上した、フォーカスされた実用的なオプションがハイライト表示され、スクリーンリーダーが読み上げます。 必要に応じて、スクリーンリーダーは、フォーカスされたメニューオプションの状態（展開、折りたたみ、混在など）を読み上げます。 また、スクリーンリーダーは、表示方法やインターフェイスの配置ではなく、実用的なオプションの目的を通知します。

ユーザーがメニューからヘルプまたはユーザープロファイルオプションを展開すると、スクリーンリーダーは適切なオプションまたはステータスを通知します。 ユーザープロファイルオプションを展開すると、キーボードを使用して使用可能なオプションを選択できるようになりす。例えば、管理者は別のユーザーを装うことができます。ユーザーが[!UICONTROL ヘルプ]オプションから文字列を検索した場合、ナレーターが「ヘルプの検索」を通知して、検索が進行中であることを示します。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## アセットの参照と関連情報の表示 {#browse}

[!DNL Assets] ユーザーインターフェイスでは、キーボードを使用して DAM リポジトリー内のデジタルアセットを参照したり、アセットをプレビューまたはダウンロードしたりできます。 また、生成されたレンディションの表示、ビューの切り替え、タイムライン、バージョン履歴、コメント、参照の確認も行えます。 また、ユーザーはメタデータを表示および管理できます。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close option in a coral-dialog was not accessible through keyboard, due to which user cannot trigger close option through keyboard press in version preview dialog. After fix, user can close dialog through close option using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

アセットリポジトリーを参照する際、次の機能によりアクセシビリティが向上します。

* スクリーンリーダーが、アイコンの名前ではなく目的や機能を示す代替テキストを読み上げます。
* ユーザーは、キーボードのキーを使用して、アセットの参照リストにあるインタラクティブなユーザーインターフェイスオプションにアクセスしてフォーカスできます。
* リスト表示の各行の要素は、スクリーンリーダーによって同じ行の要素としてアナウンスされる。
* `Tab` キーを使用してナビゲーションを行う場合、フォーカスはバージョンプレビューの「閉じる」オプションに移動できる。
* キーボードを使用して参照する場合、ハイライト表示された実用的なユーザーインターフェイスオプションは、コントラストが強化され、視覚的により目立つフォーカスを持ちます。 これにより、フォーカスされた領域がより識別しやすくなる。
* サムネール表示からクイックアクションアイコンを削除するために `Esc` キーを使用しても、最後にフォーカスされたアイテムからはキーボードフォーカスが削除されない。
* アセットを選択した状態で、`Alt + 4` キーボードショートカットを選択すると、左側のパネルに[!UICONTROL 参照]リストが開く。`Tab` キーを使用して、ゼロ以外の参照エントリ間を移動できる。ゼロ以外の参照エントリのみを移動するので、労力とキー操作の節約になる。
* アセットに対するコメントは、アセットタイムラインで使用でき、左側のパネルにキーボードまたはキーボードショートカットを使用してアクセスできる場合があります。
* [!DNL Experience Manager] の[!UICONTROL 表示設定]には、キーボードを使用してアクセスできる。矢印キーを使用して使用可能なカードサイズ間を移動して選択できる。Tab キーで既存の表示設定表示内の他の要素間を移動し設定できる。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## デジタルアセットの管理 {#manage-assets}

CRUD 操作、アセットのダウンロード、メタデータの追加など、多くのアセット管理タスクへのアクセシビリティの程度は異なります。[!DNL Assets] を使用すると、様々な支援テクノロジー（スクリーンリーダーやキーボードなど）を使用してタスクを実行できます。

通常、マーケターや管理者などの役割で行うメタデータ操作では、次の機能によりアクセシビリティが向上します。

* アセット [!UICONTROL  プロパティ ] ページの「[!UICONTROL  保存して閉じる ] オプションに、キーボードを使用してアクセスできるようになりました。
* スクリーンリーダーは、アセットの「プロパティ」の「[!UICONTROL  基本 ]」タブで、選択したタグを削除するオプションを読み上げ [!UICONTROL  し ] す。
* ユーザーは、日付選択ポップアップダイアログボックスをキーボードで使用できます。 日付選択のユーザーインターフェイス要素を使用して、オンタイムとオフタイムを設定し、日付を選択します。
* キーボードを使用したドラッグ機能は、スクリーンリーダーの参照モードの [!UICONTROL  メタデータスキーマエディター ] で正しく機能します。
* ユーザーはキーボードを使用して、フォーカスを「**ユーザーまたはグループの追加**」フィールドに移動できます。

## デジタルアセットの検索 {#search-assets}

すばやくシームレスなアセット検索の経験により、コンテンツの速度が向上します。コンテンツ速度の使用例は、主な [!DNL Assets] 機能の一部です。オムニサーチバーから検索を開始するには、キーボードショートカット `/` を使用するか、スクリーンリーダーと共に使用して、検索オプションをすばやく見つけるこ `Tab` ができます。 検索オプション ![検索オプション](assets/do-not-localize/search_icon.png) にフォーカスがある場合、スクリーンリーダーはオプションの名前を「検索ボタン」として読み上げます。`Return` を押すと、「オムニサーチ」ボックスが開きます。スクリーンリーダーは、検索ボックスに入力されたキーワードのナレーションだけでなく、[!DNL Experience Manager Assets] で提供される提案のナレーションも行います。 矢印キー、`Return`、`Tab`を組み合わせて使用し、様々なオプションにアクセスして検索をトリガーできます。

検索機能のアクセシビリティは次の機能で実現されています。

* スクリーンリーダーで使用できるページタイトルは、ページをアセットの検索ページとして識別するのに役立ちます。
* ユーザーはオムニサーチフィールドでアセットを検索する。オムニサーチフィールドは、キーボードナビゲーションまたはキーボードショートカット `/` を使用して開くことができる。
* ユーザーが検索キーワードの入力を開始すると、候補が自動的に表示されるので、矢印キーを使用して候補の中から選択できる。ハイライト表示された候補は `Return` キーを使用して選択でき、選択した候補に一致するアセットが検索される。
* スクリーンリーダーは、ユーザーが検索結果をフィルタリングする際に、フィルターパネルで混合状態チェックボックスを識別して読み上げることができます。 混合状態では、ネストされたすべての述語がユーザーによって選択されるまで、第 1 レベルのチェックボックスが最後まで有効になります。
* オムニサーチボックスが閉じると、ユーザーのフォーカスが検索オプションに移動する。

検索結果をフィルターする場合：

* 検索結果ページには、スクリーンリーダーのユーザーをより深く理解するための有益なタイトルが表示されます。
* スクリーンリーダーは、検索フィルター内のオプションを展開可能なアコーディオンとして読み上げます。
* スクリーンリーダーは、混合状態オプションを含む述語を読み上げます。

## アセットの共有 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

アセットを共有する場合、次の機能によってアクセシビリティが向上します。

* ユーザーは、リンク共有ダイアログボックスの「メールアドレスを検索/追加」フィールド内にあるキーボードを使用して、フォーカスを移動できます。

* リンク共有ダイアログボックスで、参照モードで移動すると、スクリーンリーダーは、

   * ダイアログボックスが読み込まれたとき、テーブル情報を読み上げません。
   * リストに表示されているすべての候補に移動します。
   * 「メールアドレスを検索／追加」フィールドに対して表示された提案を読み上げる。

## アクセシビリティの高いドキュメント {#accessible-docs}

[!DNL Experience Manager] には、障害を持つユーザー向けのアクセシビリティの高いドキュメントが用意されています。アドビはテンプレートとコンテンツの改善に努めています。現時点では以下の機能が、コンテンツをアクセシブルにするのに役立ちます。

* スクリーンリーダーはテキストを読み上げることができる。
* 画像と図には、代替テキストを使用できます。
* キーボードナビゲーションが可能である。
* コントラスト比は、ドキュメント Web サイトの一部を強調表示するのに役立つ。

## フィードバックの提供 {#a11y-feedback}

アクセシビリティに関するフィードバックを提供、質問し、製品の機能強化をリクエストするには、次の方法を使用し、`access@adobe.com` で電子メールを送信します。

>[!MORELIKETHIS]
>
>* [  [!DNL Dynamic Media]](/help/assets/accessibility-dm.md) のアクセシビリティ機能。
>* [各サービスパックのリリースでおこなわれた機能強化のリリースノート](/help/release-notes/release-notes.md)。
>* [[!DNL Adobe Experience Manager] アクセシビリティガイダンス](/help/managing/web-accessibility.md)
>* [アドビソリューションのアクセシビリティ準拠レポート（ACR）および VPAT リスト](https://www.adobe.com/accessibility/compliance.html)
