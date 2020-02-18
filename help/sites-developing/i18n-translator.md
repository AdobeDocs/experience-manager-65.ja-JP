---
title: トランスレーターを使用した辞書の管理
seo-title: トランスレーターを使用した辞書の管理
description: AEM には、コンポーネント UI で使用される様々な翻訳テキストを管理するためのコンソールが用意されています
seo-description: AEM には、コンポーネント UI で使用される様々な翻訳テキストを管理するためのコンソールが用意されています
uuid: 4eea3110-e958-473e-8d22-c84fa435edbd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: adf3364c-11f1-45c6-b41d-2c7d48b626f9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# トランスレーターを使用した辞書の管理{#using-translator-to-manage-dictionaries}

AEM には、コンポーネント UI で使用される様々な翻訳テキストを管理するためのコンソールが用意されています。このコンソールは、

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

トランスレーターツールを使用して、英語の文字列とその翻訳を管理します。/apps/myproject/i18nなど、リポジトリで辞書が作成されます。

トランスレーターツールと管理対象の辞書は、他の言語のコンポーネント UI を示すものです。ページやユーザー生成コンテンツを翻訳する場合は、[多言語サイト用コンテンツの翻訳](/help/sites-administering/translation.md)および[ユーザー生成コンテンツの翻訳](/help/communities/translate-ugc.md)を参照してください。

>[!CAUTION]
>
>Only edit dictionaries that are created for your project and reside under `/apps`.
>
>AEM システム辞書もこのツールで使用できます。AEM システム辞書を変更すると AEM UI に問題が発生する可能性があるので、システム辞書は変更しないでください。また、アップグレードすると変更は失われます。AEM system dictionaries are located under `/libs`.

>[!NOTE]
>
>Translatorツールには従来のUIインターフェイスがありますが、これらのフレーズが見つかったインターフェイスに関係なく、フレーズの翻訳に使用されます。

トランスレーターでは、AEM で使用されるテキストと様々な言語の翻訳が横並びになってリストされます。

![chlimage_1-205](assets/chlimage_1-205.png)

英語のテキストと翻訳されたテキストを検索、フィルター、編集できます。翻訳用に辞書を XLIFF 形式で書き出したり、翻訳結果を辞書に読み込んだりすることもできます。

このコンソールから、i18n 辞書を翻訳プロジェクトに追加することもできます。新しいプロジェクトを作成することも、既存プロジェクトに追加することもできます。

1. 「**辞書を翻訳**」をクリックします。

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. 必要に応じて、「作成」オプションまたは「追加」オプションを選択します。ダイアログが表示されます。

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. 必要に応じてフィールドに入力し、「OK」をクリックします。![chlimage_1-208](assets/chlimage_1-208.png)

1. 「**OK**」をクリックするか、ターゲット辞書を表示することができます。

   >[!NOTE]
   >
   >翻訳プロジェクトについて詳しくは、[翻訳プロジェクトの管理](/help/sites-administering/tc-manage.md)を参照してください。

## 辞書の作成 {#creating-a-dictionary}

ローカライズされた UI 文字列の管理用の辞書を作成します。辞書を作成したら、トランスレーターツールを使用して管理できます。

1. CRXDE Lite を使用して、新しい辞書のルートノード（`sling:Folder`）を追加します。これは、言語定義を保持する構造です。

   ` /apps/<projectName>/i18n`

   例：`/apps/myProject/i18n`

1. 必要な言語構造をこのルートの下に追加します。次に例を示します。

   ```shell
   /apps/myProject/i18n [sling:Folder]
       - de.json [nt:file] [mix:language]
           + jcr:language = de
       - fr.json [nt:file] [mix:language]
           + jcr:language = fr
   ```

   >[!NOTE]
   >
   >これは [Sling i18n モジュール](https://sling.apache.org/site/internationalization-support.html)の構造です。

1. Reload the translator and the dictionary path (e.g. `/apps/myProject/i18n`) will be available in the drop-down selector in the toolbar. このパスを選択して、文字列とその翻訳の追加を開始します。

   >[!NOTE]
   >
   >The translator will only save translations for languages that are actually present underneath the path (e.g. `/apps/myProject/i18n`).
   >
   >これらがグリッドに表示される言語に対応していることを確認してください。

## 辞書の文字列の管理 {#managing-dictionary-strings}

トランスレーターツールを使用して、辞書内の文字列を管理します。英語の文字列を追加、変更、削除したり、翻訳済みの文字列を指定したりできます。

>[!CAUTION]
>
>Only edit dictionaries that are created for your project and reside under `/apps`.
>
>AEM システム辞書を変更すると AEM UI に問題が発生する可能性があるので、システム辞書は変更しないでください。また、アップグレードすると変更は失われます。AEM system dictionaries are located under `/libs`.

### 文字列の追加、変更、削除 {#adding-changing-and-removing-strings}

コンポーネントが国際化された辞書に英語の文字列を追加します。使用しない文字列を翻訳してリソースを無駄にしないように、国際化される文字列のみを追加します。

辞書に追加する文字列は、コードに指定されている文字列と正確に一致する必要があります。コードで使用されているデフォルトの英語の文字列と辞書の文字列が一致していないと、必要な場合に翻訳された文字列が UI に表示されません。文字列では大文字と小文字が区別されます。

**翻訳のヒントの入力**

辞書の文字列の「コメント」プロパティを使用して、文字列の意味を明確に伝える情報をトランスレーターに提供します。UI は通常、ユーザーが曖昧な単語の意味を特定するのに役立ちます。ただし、トランスレーターは UI のコンテキストで文字列を参照するわけではありません。翻訳のヒントは、この曖昧さを解消します。例えば、コメントを使用すると、英語の単語リクエストが動詞ではなく名詞として使用されていることを翻訳者が理解しやすくなります。

翻訳のヒントは、同じ文字列に複数の意味がある場合の識別にも役立ちます。例えば、「Search」という単語は名詞と動詞の両方で使用されるので、辞書には異なる翻訳のヒントを持つ 2 つの「Search」のエントリが必要です。正しい文字列が UI で使用されるように、この文字列をリクエストするコードには翻訳のヒントも含まれます。

**インデックス付き変数を含める**

ローカライズされる文字列に変数を追加し、センテンスに文脈に応じた意味を持たせます。例えば、Web アプリケーションにログインした後、ホームページに「Welcome back Administrator.  You have 2 messages in your inbox.」ページのコンテキストに応じて、ユーザー名とメッセージ数が決定されます。

ローカライズされた文字列に変数を含めるには、getメソッドの最初の引数で、変数の場所に角括弧で囲まれたインデックスを配置します。 翻訳のヒントを使用して値を説明します。言語によって使用する文の構造が異なるので、トランスレーターは変数の意味を理解する必要があります。

[翻訳された文字列を要求するコード](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences)は、 コンテキストに従ってインデックス付き変数の値を指定します。

例えば次の文字列は、ユーザーが Web サイトにログインしたときに表示されるもので、辞書に含まれています。

`Welcome back {0}. You have {1} messages.`

次のコメントが変数の説明です。

`{0} = the user name, {1} = the number of items in the user's inbox`

**文字列の変更**

英語の文字列がコード内で変更または削除された場合に、その文字列を変更または削除します。文字列を変更した場合、元の文字列は保持され、変更を反映した新しい文字列が作成されます。文字列を削除する前に、その文字列を使用しているコードがないことを確認してください。

次の手順を使用して、文字列を追加します。

1. Dictionaries（辞書）ドロップダウンメニューで、文字列を追加する辞書を選択します。ドロップダウンメニューには、リポジトリ内の辞書のパスが表示されます。
1. 「Strings and Translations（文字列と翻訳）」テーブルの上にある「追加」をクリックします。

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. Add String（文字列を追加）ダイアログボックスの「String（文字列）」ボックスに、英語の文字列を入力します。「Comment（コメント）」ボックスに、必要に応じてトランスレーター用の翻訳のヒントを入力します。
1. 「OK」をクリックします。
1. 「保存」をクリックします。

   ![chlimage_1-210](assets/chlimage_1-210.png)

次の手順を使用して、辞書内の文字列を変更します。

1. Dictionaries（辞書）ドロップダウンメニューで、変更する文字列が含まれる辞書を選択します。
1. 変更する文字列をダブルクリックします。
1. Edit String（文字列を編集）ダイアログボックスの「Modify String or Comment (Creates a Copy)（文字列またはコメントを変更（コピーを作成））」を選択します。

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. 文字列またはコメントを変更して、「OK」をクリックします。
1. 「保存」をクリックします。

   ![chlimage_1-212](assets/chlimage_1-212.png)

次の手順を使用して、辞書から文字列を削除します。

1. Dictionaries（辞書）ドロップダウンメニューで、文字列を削除する辞書を選択します。
1. 「Remove（削除）」をクリックします。

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. 「保存」をクリックします。

   ![chlimage_1-214](assets/chlimage_1-214.png)

### 文字列の検索 {#searching-for-strings}

トランスレーターの下部にある検索バーには、文字列選択のオプションがあります。

* **** テキストでフィルタ：英語の文字列、コメント、翻訳と一致するパターンです。 パターンの全体または一部に一致する項目のみがテーブルに表示されます。
* **** 変更：任意、変更済み、新規、削除済み：変更され、保存されていない項目を表示します。

   * いすれか：変更、追加または削除された項目を表示します。
   * 変更済み：変更された項目を表示します。
   * 新規：追加された項目を表示します。
   * 削除：削除された項目を表示します。
   * 複数選択：選択されたプロパティに該当するすべての項目を表示します。

* **コメントあり**：トランスレーター用のコメントがある項目を表示します。
* **翻訳の欠落：**
少なくとも 1 つの言語の翻訳が欠落している項目を表示します。

![chlimage_1-215](assets/chlimage_1-215.png)

1. 検索バーで、フィルターオプションを選択します。
1. オプションを使用してフィルター処理するには、「Filter（フィルター）」をクリックします。
1. フィルターを削除して辞書内のすべての項目を表示するには、「Clear（クリア）」をクリックします。

### 翻訳された文字列の編集 {#editing-translated-strings}

英語の文字列を辞書に追加した後、その文字列の翻訳を追加できます。サードパーティによる翻訳をおこなうために[辞書を書き出す](/help/sites-developing/i18n-translator.md#exporting-a-dictionary)こともできます。

1. [プロジェクト専用の辞書](#creating-a-dictionary)を選択します（翻訳を保持するリポジトリ内のパスがその辞書で指定される場合）。例えば、次のように&#x200B;**辞書**&#x200B;を選択します。

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >Only edit dictionaries that are created for your project and reside under `/apps`.
   >
   >AEM システム辞書もこのツールで使用できます。AEM システム辞書を変更すると AEM UI に問題が発生する可能性があるので、システム辞書は変更しないでください。また、アップグレードすると変更は失われます。AEM system dictionaries are located under `/libs`.

1. いずれかの文字列の翻訳されたテキストを編集するには、次のどちらかの手順を使用します。

   * 単一のテキストを編集する対象の文字列に適した言語をダブルクリックします。
   ![chlimage_1-216](assets/chlimage_1-216.png)

   * 目的の文字列の「**String（文字列）**」フィールドまたは「**Comment（コメント）**」フィールドをダブルクリックして、**Edit String（文字列を編集）**&#x200B;ダイアログを開き、必要に応じて翻訳を編集します。「**OK**」をクリックしてダイアログを閉じます。
   ![chlimage_1-217](assets/chlimage_1-217.png)

1. ツールバーの「**保存**」をクリックして変更をコミットします。

   >[!NOTE]
   >
   >「**保存**」の代わりに「**リセットして更新**」をクリックすると、以前のテキストに対する変更がすべて元に戻ります。

## サードパーティのトランスレーターの使用 {#using-third-party-translators}

サードパーティの翻訳サービスの使用をサポートするために、トランスレーターツールで辞書を書き出したり、読み込んだりできます。

### 辞書の書き出し {#exporting-a-dictionary}

サードパーティのサービスが辞書の文字列を翻訳できるように、辞書を XLIFF ファイルに書き出します。

* 辞書を書き出して、英語の単語とある言語に翻訳された単語を含めます。
* 英語の文字列のみの一部またはすべてを書き出します。

XLIFF ファイルを書き出してある言語を含める場合、リポジトリ内の辞書のノード構造がその言語を含んでいる必要があります。その言語が含まれていない場合はエラーが発生します。例えば、フランス語の XLIFF ファイルを書き出す場合、辞書のフォルダーには `mix:language` という名前の `fr` 子ノードが含まれている必要があります（[辞書の作成](/help/sites-developing/i18n-translator.md#creating-a-dictionary)を参照）。

次の手順を使用して、特定の言語の XLIFF ファイルを書き出します。

1. Open the Translation tool `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Dictionaries（辞書）ドロップダウンメニューを使用して、書き出す辞書を選択します。
1. 「Export（書き出し）」／「Export Full XX Xliff（すべての *XX* Xliff を書き出し）」オプションをクリックします。*XX* は DE や FR などの 2 文字の言語コードです。

   新しいタブまたはウィンドウで XLIFF ファイルが開きます。

1. Web ブラウザーのコマンド（ファイル／名前を付けて保存など）を使用して、ページをファイルとしてファイルシステム上に保存します。

次の手順を使用して、英語の文字列のみのすべてまたは一部を書き出します。

1. トランスレーターツールを開きます。`http://<host>:<port>/libs/cq/i18n/translator.html`
1. Dictionaries（辞書）ドロップダウンメニューを使用して、書き出す辞書を選択します。
1. 文字列のサブセットを書き出す場合は、辞書内の書き出す項目を選択します。項目を選択しない場合は、すべての項目が書き出されます。
1. Export（書き出し）／Export Selection As Xliff (Strings Only)（選択対象を Xliff として書き出し（文字列のみ））をクリックします。
1. 表示されたダイアログボックスで、テキストをコピーしてテキストファイルに貼り付けます。

### 辞書の読み込み {#importing-a-dictionary}

XLIFF ファイルを辞書に読み込んで情報を入力します。辞書にある英語の文字列の翻訳が含まれていて、XLIFF ファイルに同じ文字列の異なる翻訳が含まれている場合、辞書の翻訳が置き換えられます。

1. Open the Translation tool `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Import （読み込み）／XLIFF Translations（XLIFF 翻訳）をクリックします。
1. 読み込むファイルを選択して、「OK」をクリックします。

## サポートされる言語の管理 {#managing-supported-lanuages}

トランスレーターツールがサポートし、Web ページのユーザーに提供される言語を追加または削除します。

### 辞書テーブルにリストされている言語の変更 {#changing-languages-listed-in-the-dictionary-table}

トランスレーターツールの辞書テーブルには、次の言語が含まれています。

* de - ドイツ語
* fr - フランス語
* it - イタリア語
* es - スペイン語
* ja - 日本語
* pt-br - ポルトガル語（ブラジル）
* zh-cn - 簡体字中国語
* zh-tw - 繁体字中国語（限定的にサポート）
* ko-kr - 韓国語

次の手順を使用して、言語を追加または削除します。

1. CRXDE Lite を使用して新しいノードを作成します。

   `/etc/languages`

1. このノードでプロパティを作成します。

   * **名前**: `languages`
   * **タイプ**: `Multi-String`
   * **値**：表示する言語のリスト。次に例を示します。

      * fr
      * es
   >[!NOTE]
   >
   >言語コードは小文字で指定する必要があります。

1. CRXDE Lite で「**すべて保存**」をクリックして、トランスレーターを再読み込みします。定義された言語を表示するようにグリッドが更新されます。

   >[!NOTE]
   >
   >The translator will only save translations for languages that are actually [present in the dictionary](#creating-a-dictionary) (i.e. underneath the dictionary path such as `/apps/myProject/i18n`).
   >
   >これらがグリッドに表示される言語に対応していることを確認してください。

### 作成者が言語を使用できるようにする {#making-languages-available-to-authors}

After defing a dictionary for a language new to your AEM instance you need to make this available for selection by the authors (for example, for use in **Preferences**):

1. **セキュリティ**&#x200B;コンソールの&#x200B;**環境設定**&#x200B;で使用可能な言語のリストを変更するには、次の手順を実行します。

   1. アプリケーションコードに次のコードのオーバーレイを作成します。

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. **Web サイト**&#x200B;コンソールから、**環境設定**&#x200B;で言語を使用できるようにするには、アプリケーションで次の変更をおこなう必要があります。

   1. 次の場所にある構造のオーバーレイを作成します。

      `/libs/cq/security/content/tools/userProperties`

   1. オーバーレイ内で、次の場所にある言語のリストを更新します。

      `items/common/items /lang/options`

1. すべての項目を保存して、適切なコンソールを再読み込みします。

### 言語名とデフォルトの国の変更 {#changing-language-names-and-default-countries}

同じ言語が様々な国で使用されています。例えば、米国、英国、オーストラリアではすべて英語を使用しています。This is indicated by a code indicating both language and country such as `en_US`, `en_GB` and `en_AU`.

デフォルトの国はフラグを表示する際に（言語コピーダイアログなどで）使用され、言語コードの国を解決します。

>[!NOTE]
>
>前述のトランスレーターで管理されるローカリゼーションでは、正確な言語のみ使用できます。If the language preference drop down uses `en_uk`, there must be a `en_uk` dictionary in the repository.

デフォルトの定義を変更するには：

1. 言語リストは次の場所に格納されます。

   `/libs/wcm/core/resources/languages`

   このリストを次の場所にコピーしてオーバーレイします。

   `/apps/wcm/core/resources/languages`

   次に、ここにあるリストを変更または拡張します。The property `defaultCountry` on a language node (e.g. `ja`) must contain the full code, such as `ja_jp`, which would define `jp` as the default country for the language `ja`.

1. **CQ WCM 言語マネージャー**&#x200B;を更新します。

   * **言語リスト**：

      リポジトリ内の言語リストのパス。オーバーレイに使用する場所に設定します。

      ```
             /apps/wcm/core/resources/languages
      ```
   OSGi Web コンソールを使用してこの設定をおこなうことができます。

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## 辞書の公開 {#publishing-dictionaries}

辞書を AEM アプリケーションのリリース管理プロセスに組み込みます。例えば、アプリケーションのコンテンツパッケージ内の辞書をデプロイメント用にパブリッシュインスタンスに含めます。この方法には次のような利点があります。

* パブリッシュ環境内の複数のコンポーネントで辞書を利用できます。
* コンポーネント UI 文字列への変更が、更新された翻訳と共にデプロイされます。

同様に、辞書の文字列のテストが、通常のソフトウェア開発ライフサイクルの一環として実行されます。

>[!NOTE]
>
>辞書には、通常の発行機能（複製）を使用しないでください。 代わりに、ディクショナリはコードや設定と同じように扱う必要があります。 これには、ソース管理を使用した変更の追跡、およびコンテンツパッケージを使用した作成者と発行に対する変更の適用が含まれます。

>[!NOTE]
>
>Dispatcher を使用する場合は、[キャッシュされたページを無効にして](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html)、新しい辞書の文字列をレンダリングされたコンポーネント文字列に含める必要があります。

