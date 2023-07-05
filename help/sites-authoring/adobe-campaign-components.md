---
title: Adobe Campaign コンポーネントとの統合
description: Adobe Campaign と統合すると、ニュースレター用のコンポーネントとフォーム用のコンポーネントを使用できるようになります。
uuid: a858d5ca-aa6e-4bde-92db-a6dcd8b48ae6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9da34dab-7e89-4127-ab26-532687746b2a
docset: aem65
exl-id: d1132fcd-e6a0-44a2-8753-d250f68fbd78
source-git-commit: b3889b1897f0ec0c5bbf60c346b77b2906175904
workflow-type: tm+mt
source-wordcount: '2839'
ht-degree: 99%

---

# Adobe Campaign コンポーネント{#adobe-campaign-components}

Adobe Campaign と統合すると、ニュースレター用のコンポーネントとフォーム用のコンポーネントを使用できるようになります。このドキュメントでは、両方のコンポーネントについて説明します。

>[!CAUTION]
>
>AEM メールコンポーネントは非推奨（廃止予定）となりました。コンテンツとスタイルを結合するメールの性質上、AEM で標準で提供されるメールコンポーネントは、プロジェクトで必要なすべてのコンポーネントにカスタムスタイルを実装する必要があるので、顧客による再利用の機会は限られています。
>
>メールコンポーネントはプロジェクトレベルで実装できます。その方法は、非推奨の AEM メールコンポーネントを見ればわかります。ただし、これらの非推奨コンポーネントは、プロジェクトでは使用しないでください。

## Adobe Campaign ニュースレターコンポーネント {#adobe-campaign-newsletter-components}

すべての Adobe Campaign コンポーネントは、[メールテンプレートのベストプラクティス](/help/sites-administering/best-practices-for-email-templates.md)で大まかに説明されているベストプラクティスに従います。また、Adobe マークアップ言語 [HTL](https://helpx.adobe.com/jp/experience-manager/htl/using/overview.html) をベースとしています。

Adobe Campaign と連携するように設定されているニュースレターまたはメールを開くと、「**Adobe Campaign ニュースレター**」セクションに以下のコンポーネントが表示されます。

* 見出し（Campaign）
* 画像（Campaign）
* リンク（Campaign）
* Scene7 画像テンプレート（Campaign）
* ターゲット参照（Campaign）
* テキストと画像（Campaign）
* テキストおよびパーソナライゼーション（Campaign）

これらのコンポーネントについて、次の節で説明します。

コンポーネントは次のように表示されます。

![chlimage_1-43](assets/chlimage_1-43.png)

### 見出し（Campaign） {#heading-campaign}

見出しコンポーネントは、次のいずれかを表示します。

* 「**タイトル**」フィールドが空の場合は、現在のページ名を表示します。
* 「**タイトル**」フィールドにテキストを指定した場合は、そのテキストを表示します。

**見出し（Campaign）**&#x200B;コンポーネントを直接編集します。ページタイトルを使用する場合は、空のままにします。

![chlimage_1-44](assets/chlimage_1-44.png)

次の項目を設定できます。

* **タイトル**
ページタイトル以外の名前を使用する場合は、ここに入力します。

* **見出しレベル（1、2、3、4）**
HTML の見出しサイズ 1～4 に基づいた見出しレベル。

見出し（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-45](assets/chlimage_1-45.png)

### 画像（Campaign） {#image-campaign}

画像（Campaign）コンポーネントは、指定されたパラメーターに従って、画像とそれに付随するテキストを表示します。

画像をアップロードした後に、編集および操作できます（切り抜き、回転、リンク／タイトル／テキストの追加など）。

画像は、[アセットブラウザー](/help/sites-authoring/author-environment-tools.md#assetsbrowsertouchoptimizedui)からコンポーネントに直接ドラッグ＆ドロップするか、コンポーネントの[設定ダイアログ](/help/sites-authoring/editing-content.md#editconfigurecopycutdeletepastetouchoptimizedui)にドラッグ＆ドロップできます。設定ダイアログから画像をアップロードすることもできます。また、このダイアログボックスでは、画像のすべての定義と操作も制御します。

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>「**代替テキスト**」フィールドに情報を入力する必要があります。入力しないと画像を保存できません。

画像をアップロードした後に、[インプレース編集](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui)を使用して、必要に応じて画像を切り抜いたり回転したりできます。

![インプレース編集ツールバー](do-not-localize/chlimage_1-10.png)

>[!NOTE]
>
>インプレースエディターでは、編集時に、画像の元のサイズと縦横比を使用します。高さと幅のプロパティも指定できます。プロパティで定義したサイズや縦横比の制限は、編集の変更内容を保存するときに適用されます。
>
>インスタンスによっては、[ページのデザイン](/help/sites-developing/designer.md)によって最小および最大の制限が課される場合もあります。これらは、プロジェクト実装時に開発されます。

フルスクリーン編集モードで使用できる追加オプションがいくつか用意されています（マップ、ズームなど）。

![フルスクリーン編集モード](do-not-localize/chlimage_1-11.png)

画像を読み込む際は、次の設定が可能です。

* **マップ**&#x200B;画像をマップするには、「マップ」を選択します。画像マップの作成方法（長方形、多角形など）を指定し、領域が指す位置を指定します。

* **切り抜き**「切り抜き」をクリックして画像を切り抜きます。マウスを使用して画像を切り抜きます。

* **回転**&#x200B;画像を回転するには、「回転」を選択します。画像が目的の向きになるまで繰り返し使用します。

* **消去**
現在の画像を削除します。

* ズームバー（クラシックのみ）
画像のズームインおよびズームアウトを行うには、画像の下（「OK」および「キャンセル」ボタンの上）のスライドバーを使用します。
* **タイトル**
画像のタイトル。

* **代替テキスト**
アクセス可能なコンテンツを作成する際に使用する代替テキスト。

* **リンク先**
Web サイト内のアセットまたはその他のページへのリンクを作成します。

* **説明**
画像の説明。

* **サイズ**
画像の高さと幅を設定します。

>[!NOTE]
>
>「**詳細**」タブの「**代替テキスト**」フィールドに情報を入力する必要があります。入力しない場合は画像を保存できず、次のエラーメッセージが表示されます。
>
>`Validation failed. Verify the values of the marked fields.`
>

画像（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-47](assets/chlimage_1-47.png)

### リンク（Campaign） {#link-campaign}

リンク（Campaign）コンポーネントを使用すると、ニュースレターにリンクを追加できます。

以下の項目を「**表示**」、「**URL 情報**」または「**詳細**」タブで設定できます。

* **リンクキャプション**
リンクのキャプション。ユーザーに表示されるテキストです。

* **リンクツールチップ**
リンクの使用方法に関する追加情報を付加します。

* **LinkType**
ドロップダウンリストで、**カスタム URL** および **アダプティブドキュメント**。このフィールドは必須です。カスタム URL を選択した場合は、リンクの URL を指定できます。アダプティブドキュメントを選択した場合は、ドキュメントのパスを指定できます。

* **追加の URL パラメーター**
追加の URL パラメーターがあれば追加します。「項目を追加」をクリックして、複数の項目を追加します。

>[!NOTE]
>
>「**URL 情報**」タブの「**リンクタイプ**」フィールドに情報を入力する必要があります。入力しない場合はコンポーネントを保存できず、次のエラーメッセージが表示されます。
>
>`Validation failed. Verify the values of the marked fields.`
>

リンク（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-48](assets/chlimage_1-48.png)

### Dynamic Media Classic（Scene7）画像テンプレート（Campaign） {#scene-image-template-campaign}

Dynamic Media Classic（Scene7）画像テンプレートはレイヤー化された画像ファイルで、コンテンツとプロパティをパラメーター化して可変性を持たせることができます。**[!UICONTROL 画像テンプレート]**&#x200B;コンポーネントを使用すると、ニュースレター内で Scene7 テンプレートを使用して、テンプレートパラメーターの値を変更できます。さらに、パラメーターの内部で Adobe Campaign メタデータ変数を使用して、ユーザーごとにパーソナライズされた画像を表示できます。

![chlimage_1-49](assets/chlimage_1-49.png)

コンポーネントを設定するには、「**編集**」をクリックします。このセクションで説明した設定を行うことができます。この Scene7 画像テンプレートについて詳しくは、[Scene7 画像テンプレートコンポーネント](/help/assets/scene7.md#image-template)を参照してください。

さらに、パラメーターパネルには、Scene7 のテンプレート用に定義されたテンプレートパラメーターがすべて一覧表示されます。これらのパラメーターごとに、値の調整、変数の挿入、デフォルト値へのリセットを実行できます。

![chlimage_1-50](assets/chlimage_1-50.png)

### ターゲット参照（Campaign） {#targeted-reference-campaign}

ターゲット参照（Campaign）コンポーネントを使用すると、ターゲット段落への参照を作成できます。

このコンポーネント内で、ターゲットの段落に移動して選択します。

フォルダーアイコンをクリックして、参照する段落に移動します。終了したら、チェックマークをクリックします。

### テキストと画像（Campaign） {#text-image-campaign}

テキストと画像（Campaign）コンポーネントを使用すると、テキストブロックと画像を追加できます。

クリックしてこのコンポーネントを設定する際には、「テキスト」または「画像」を選択します。

![chlimage_1-51](assets/chlimage_1-51.png)

「**テキスト**」を選択すると、インラインエディターが表示されます。

![テキストツールバー](do-not-localize/chlimage_1-12.png)

「**画像**」を選択すると、画像用のインプレースエディターが表示されます。

![画像ツールバー](do-not-localize/chlimage_1-13.png)

画像の操作について詳しくは、[画像（Campaign）コンポーネント](#image-campaign)を参照してください。テキストの操作について詳しくは、[テキストとパーソナライズ機能（Campaign）コンポーネント](#text-personalization-campaign)を参照してください。

テキストおよびパーソナライゼーション（Campaign）コンポーネントや画像（Campaign）コンポーネントと同様に、次の項目を設定できます。

* **テキスト**
テキストを入力します。ツールバーを使用して、書式設定の変更、リストの作成およびリンクの追加を行います。

* **画像**
コンテンツファインダーから画像をドラッグするか、クリックして画像を参照します。必要に応じて、切り抜きや回転を行います。

* **画像のプロパティ**（**詳細画像プロパティ**）
次の項目を指定できます。

   * **タイトル**
ブロックのタイトル。マウスポインターを置くと表示されます。

   * **代替テキスト**
画像を表示できない場合に表示する代替テキスト。

   * **リンク先**
web サイト内のアセットまたはその他のページへのリンクを作成します。

   * **説明**
画像の説明。

   * **サイズ**
画像の高さと幅を設定します。

>[!NOTE]
>
>「**詳細**」タブの「**代替テキスト**」フィールドは必須です。入力されていない場合、コンポーネントを保存できず、次のエラーメッセージが表示されます。
>
>`Validation failed. Verify the values of the marked fields.`
>

テキストと画像（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-52](assets/chlimage_1-52.png)

### テキストおよびパーソナライゼーション（Campaign） {#text-personalization-campaign}

テキストおよびパーソナライゼーション（Campaign）コンポーネントを使用すると、[リッチテキストエディター](/help/sites-authoring/rich-text-editor.md)の機能を備えた WYSIWYG エディターでテキストブロックを入力できます。さらに、このコンポーネントでは、Adobe Campaign のコンテキストフィールドとパーソナライゼーションブロックを使用できます。[パーソナライゼーションの挿入](/help/sites-authoring/campaign.md#inserting-personalization)も参照してください。

フォントの文字、配置、リンク、リスト、インデントなど、多様なアイコンでテキストの書式を設定できます。[タッチ操作向け UI とクラシック UI](/help/sites-authoring/editing-content.md) の機能は基本的に同じですが、ルックアンドフィールは異なります。

![chlimage_1-53](assets/chlimage_1-53.png)

インプレースエディターでは、テキストの追加、位置揃えの変更、リンクの追加と削除、コンテキストフィールドやパーソナライゼーションブロックの追加、フルスクリーンモードの開始を実行することができます。テキスト／パーソナライズ機能の追加が完了したら、チェックマークを選択して変更を保存します（または「x」を選択してキャンセルします）。詳しくは、[インプレース編集](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui)を参照してください。

>[!NOTE]
>
>* 使用できるパーソナライゼーションフィールドは、ニュースレターがリンクされている Adobe Campaign テンプレートによって異なります。
>* ContextHub からペルソナを選択すると、選択したプロファイルのデータでパーソナライゼーションフィールが自動的に置き換えられます。
>
>[パーソナライズ機能の挿入](/help/sites-authoring/campaign.md#inserting-personalization)を参照してください。

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>**nms:seedMember** スキーマまたはその拡張で定義されているフィールドのみが考慮されます。**nms:seedMember** にリンクしているテーブルの属性は使用できません。

## Adobe Campaign フォームコンポーネント {#adobe-campaign-form-components}

Adobe Campaign コンポーネントを使用すると、ユーザーがニュースレターの購読や登録解除、またはユーザープロフィールの更新を行うために入力するフォームを作成できます。詳しくは、[Adobe Campaign Forms の作成](/help/sites-authoring/adobe-campaign-forms.md)を参照してください。

各コンポーネントフィールドは、Adobe Campaign データベースフィールドにリンクできます。使用可能なフィールドは、フィールドに含まれるデータのタイプによって異なります（[コンポーネントとデータタイプ](#components-and-data-type)の節を参照）。Adobe Campaign で受信者スキーマを拡張すると、データタイプが一致するコンポーネントで新しいフィールドが使用できるようになります。

Adobe Campaign と統合するように設定されているフォームを開くと、「**Adobe Campaign**」セクションに以下のコンポーネントが表示されます。

* チェックボックス （Campaign）
* 日付フィールド（Campaign）と日付フィールド／HTML5（Campaign）
* 暗号化されたプライマリキー（Campaign）
* エラー表示（Campaign）
* 非表示の紐付けキー（Campaign）
* 数値フィールド （Campaign）
* オプションフィールド （Campaign）
* 購読チェックリスト（Campaign）
* テキストフィールド （Campaign）

コンポーネントは次のように表示されます。

![chlimage_1-55](assets/chlimage_1-55.png)

このセクションでは、各コンポーネントについて詳しく説明します。

### コンポーネントとデータタイプ {#components-and-data-type}

次の表に、Adobe Campaign プロファイルデータの表示と変更に使用できるコンポーネントを示します。各コンポーネントを Adobe Campaign プロファイルフィールドにマッピングして、フィールドの値を表示し、フォームの送信時にフィールドを更新できます。異なるコンポーネントは、適切なデータタイプのフィールドでのみ使用できます。

<table>
 <tbody>
  <tr>
   <td><p><strong>コンポーネント</strong></p> </td>
   <td><p><strong>Adobe Campaign フィールドのデータタイプ</strong></p> </td>
   <td><p><strong>フィールドの例</strong></p> </td>
  </tr>
  <tr>
   <td><p>チェックボックス （Campaign）</p> </td>
   <td><p>ブール値</p> </td>
   <td><p>今後の連絡は不要（どのチャネルからも）</p> </td>
  </tr>
  <tr>
   <td><p>日付フィールド （Campaign）</p> <p>日付フィールド / HTML 5 （Campaign）</p> </td>
   <td><p>date</p> </td>
   <td><p>生年月日</p> </td>
  </tr>
  <tr>
   <td><p>数値フィールド （Campaign）</p> </td>
   <td><p>数値（byte、short、long、double）</p> </td>
   <td><p>年齢</p> </td>
  </tr>
  <tr>
   <td><p>オプションフィールド （Campaign）</p> </td>
   <td><p>値が関連付けられたバイト</p> </td>
   <td><p>性別</p> </td>
  </tr>
  <tr>
   <td><p>テキストフィールド （Campaign）</p> </td>
   <td><p>文字列</p> </td>
   <td><p>メール</p> </td>
  </tr>
 </tbody>
</table>

### 大部分のコンポーネントに共通の設定 {#settings-common-to-most-components}

Adobe Campaign コンポーネントには、すべてのコンポーネント（暗号化されたプライマリキーコンポーネントと非表示の調整キーコンポーネントを除く）に共通の設定があります。

大部分のコンポーネントでは、次の設定を行うことができます。

#### タイトルとテキスト {#title-and-text}

![chlimage_1-56](assets/chlimage_1-56.png)

* **タイトル**
要素名以外の名前を使用する場合は、ここに入力します。

* **タイトルを非表示にする**
タイトルを表示しない場合は、このチェックボックスをオンにします。

* **説明**
フィールドに説明を追加して、ユーザーに詳しい情報を提供します。

* **値の表示のみ**
値が存在する場合、その値を表示します。

#### Adobe Campaign {#adobe-campaign}

次の項目を設定できます。

* **マッピング**
必要に応じて、Adobe Campaign パーソナライゼーションフィールドを選択します。

* **紐付けキー**
このフィールドを紐付けキーの一部にする場合は、このチェックボックスをオンにします。

![chlimage_1-57](assets/chlimage_1-57.png)

#### 制約 {#constraints}

* **必須** このチェックボックスをオンにすると、このコンポーネントが必須になり、ユーザーは値を入力する必要があります。
* **必須メッセージ** オプションで、このフィールドが必須であることを示すメッセージを追加します。

![chlimage_1-58](assets/chlimage_1-58.png)

#### スタイル設定 {#styling}

* **CSS**
このコンポーネントに使用する CSS クラスを入力します。

![chlimage_1-59](assets/chlimage_1-59.png)

### チェックボックス （Campaign） {#checkbox-campaign}

チェックボックス（Campaign）コンポーネントを使用すると、ユーザーがブーリアンデータタイプの Adobe Campaign プロファイルフィールドを変更できるようになります。例えば、受信者が任意のチャネルからの連絡を希望するかどうかを指定できるチェックボックス（Campaign）コンポーネントを使用できます。

チェックボックス（Campaign）コンポーネントでは、[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)を使用できます。

チェックボックス（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-60](assets/chlimage_1-60.png)

### 日付フィールド（Campaign）と日付フィールド／HTML 5（Campaign） {#date-field-campaign-and-date-field-html-campaign}

日付フィールドを使用して、受信者が日付を指定できるようにします。これは例えば、受信者による生年月日の指定が必要な場合などに有効です。日付の形式は、Adobe Campaign インスタンスで使用されている形式と同じになります。

[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)に加え、次の項目を設定できます。

* **制約 - 制約**ドロップダウン
「**なし**」または「**日付**」を選択して、日付の制約を追加するかかどうかを設定できます。「日付」を選択した場合、ユーザーはこのフィールドに日付形式で値を入力する必要があります。

* **制約メッセージ** さらに、ユーザーに回答の適切な形式を示す、制約メッセージを追加できます。
* **スタイル設定 - 幅** 「**+**」アイコンと「**-**」アイコンをクリックまたはタップするか、数字を入力して、フィールドの幅を調整します。

幅が調整された日付フィールド（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-61](assets/chlimage_1-61.png)

### 暗号化されたプライマリキー (Campaign) {#encrypted-primary-key-campaign}

このコンポーネントでは、Adobe Campaign プロファイルの識別子（Adobe Campaign Standard では&#x200B;**メインリソース識別子**、Adobe Campaign 6.1 では&#x200B;**暗号化されたプライマリキー**）を含んだ URL パラメーターの名前を定義します。

Adobe Campaign プロファイルデータを表示および変更する各フォームには、暗号化されたプライマリキーコンポーネントを含める&#x200B;**必要があります**。

暗号化されたプライマリキー（Campaign）コンポーネントでは、次の項目を設定できます。

* **タイトルとテキスト - 要素名** デフォルト値は encryptedPK です。フォーム上の別の要素名と競合している場合にのみ、要素名を変更する必要があります。2 つのフォームフィールドに同じ要素名を付けることはできません。
* **Adobe Campaign - URL パラメーター** EPK 用の URL パラメーターを追加します。例えば、値 **epk** を使用できます。

暗号化されたプライマリキー（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-62](assets/chlimage_1-62.png)

### エラー表示（Campaign） {#error-display-campaign}

このコンポーネントを使用すると、バックエンドエラーを表示できます。コンポーネントを正しく機能させるには、フォームのエラー処理を転送に設定する必要があります。

エラー表示（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-63](assets/chlimage_1-63.png)

### 非表示の紐付けキー（Campaign） {#hidden-reconciliation-key-campaign}

非表示の紐付けキー（Campaign）コンポーネントを使用して、非表示のフィールドを紐付け整キーの一部としてフォームに追加できます。

非表示の紐付けキー（Campaign）コンポーネントでは、次の項目を設定できます。

* **タイトルとテキスト - 要素名** デフォルト値は reconcilKey です。フォーム上の別の要素名と競合している場合にのみ、要素名を変更する必要があります。2 つのフォームフィールドに同じ要素名を付けることはできません。
* **Adobe Campaign - マッピング** Adobe Campaign パーソナライゼーションフィールドにマッピングします。

非表示の紐付けキー（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-64](assets/chlimage_1-64.png)

### 数値フィールド （Campaign） {#numeric-field-campaign}

数値フィールドを使用すると、受信者が年齢などの数値を入力できるようになります。

[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)に加え、次の項目を設定できます。

* **制約 - 制約**ドロップダウン
「**なし**」または「**数値**」を選択して、数値の制約を追加するかどうかを設定できます。「数値」を選択した場合、ユーザーはこのフィールドに数値で回答を入力する必要があります。

* **制約メッセージ** さらに、ユーザーに回答の適切な形式を示す、制約メッセージを追加できます。
* **スタイル設定 - 幅** 「**+**」アイコンと「**-**」アイコンをクリックまたはタップするか、数字を入力して、フィールドの幅を調整します。

幅が設定された数値フィールド（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-65](assets/chlimage_1-65.png)

### オプションフィールド （Campaign） {#option-field-campaign}

このドロップダウンリストを使用すると、受信者の性別やステータスなどのオプションを選択できます。

オプションフィールド（Campaign）コンポーネントでは、[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)を使用できます。ドロップダウンリストに値を入力するには、Adobe Campaign の記号をクリックまたはタップして Adobe Campaign のパーソナライゼーションフィールドに移動して、適切なフィールドを選択します。

![chlimage_1-66](assets/chlimage_1-66.png)

オプションフィールド（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-67](assets/chlimage_1-67.png)

### 購読チェックリスト（Campaign） {#subscriptions-checklist-campaign}

**購読チェックリスト（Campaign）**&#x200B;コンポーネントを使用して、Adobe Campaign プロファイルに関連付けられた購読を変更できます。

このコンポーネントをフォームに追加すると、利用可能なすべての購読がチェックボックスとして表示されるので、ユーザーに目的の購読を選択させることができます。ユーザーがフォームを送信すると、フォームのアクションタイプ（「**Adobe Campaign：サービスに登録**」または「**Adobe Campaign：サービスの登録解除**」）に応じて、選択されたサービスにユーザーが登録されるか、ユーザーの登録が解除されます。

>[!NOTE]
>
>このコンポーネントは、ユーザーがどのサービスを購読または購読解除しているかを確認しません。

購読チェックリスト（Campaign）コンポーネントでは、[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)を使用できます。（このコンポーネントで利用できる Adobe Campaign 設定はありません）。

購読チェックリスト（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-68](assets/chlimage_1-68.png)

### テキストフィールド （Campaign） {#text-field-campaign}

テキストフィールド（Campaign）コンポーネントを使用すると、名、姓、住所、メールアドレスなどの文字列タイプのデータを入力できます。

[大部分の Adobe Campaign コンポーネントに共通の設定](#settings-common-to-most-components)に加え、次の項目を設定できます。

* **制約 - 制約**ドロップダウン
「**なし**」、「**メール**」または「**名前**（ウムラウトなし）」を選択して、メールアドレスまたは名前の制約を追加するかどうかを設定できます。「メール」を選択した場合は、このフィールドにメールアドレスを入力する必要があります。「名前」を選択した場合は、名前を入力する必要があります（ウムラウトは使用できません）。

* **制約メッセージ** さらに、入力値の適切なフォーマットを示す制約メッセージを追加できます。
* **スタイル設定 - 幅** 「**+**」アイコンと「**-**」アイコンをクリックまたはタップするか、数字を入力して、フィールドの幅を調整します。

テキストフィールド（Campaign）コンポーネントの表示例を以下に示します。

![chlimage_1-69](assets/chlimage_1-69.png)
