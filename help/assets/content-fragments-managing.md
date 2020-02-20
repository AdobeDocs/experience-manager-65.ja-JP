---
title: コンテンツフラグメントの管理
seo-title: コンテンツフラグメントの管理
description: コンテンツフラグメントはアセットとして保存されるので、主にアセットコンソールから管理します。
seo-description: コンテンツフラグメントはアセットとして保存されるので、主にアセットコンソールから管理します。
uuid: 675e1a6b-2583-488f-bbb4-210daed3e1b0
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: 21a18d60-f3fe-4048-9949-8416b5cb4596
docset: aem65
translation-type: tm+mt
source-git-commit: 9cab3284e8aab996363da7eaa7c5a175044d9592

---


# コンテンツフラグメントの管理{#managing-content-fragments}

コンテンツフラグメントは&#x200B;**アセット**&#x200B;として保存されるので、主に&#x200B;**アセット**&#x200B;コンソールから管理します。

>[!NOTE]
>
>コンテンツフラグメントは、ページのオーサリングで使用します。[コンテンツフラグメントを使用したページのオーサリング](/help/sites-authoring/content-fragments.md)を参照してください。

## コンテンツフラグメントの作成 {#creating-content-fragments}

### コンテンツモデルの作成 {#creating-a-content-model}

構造化コンテンツを含むコンテンツフラグメントを作成する前に、[コンテンツフラグメントモデル](/help/assets/content-fragments-models.md)を有効にして作成できます。

>[!NOTE]
>
>単純なコンテンツフラグメントに使用されるテンプレートについて詳しくは、[コンテンツフラグメントの開発](/help/sites-developing/customizing-content-fragments.md)を参照してください。

### コンテンツフラグメントの作成 {#creating-a-content-fragment}

コンテンツフラグメントの作成方法は基本的に単純なフラグメントと構造化フラグメントで同じです。

1. フラグメントを作成する&#x200B;**アセット**&#x200B;フォルダーに移動します。
1. 「**作成**」を選択し、「**コンテンツフラグメント**」を選択して、ウィザードを開きます。
1. ウィザードの最初の手順では、新しいフラグメントの基盤を指定することを求められます。

   * 以下を指定します。

      * [テンプレート](/help/sites-developing/content-fragment-templates.md) - **単純なフラグメント**&#x200B;など

      * [モデル](/help/assets/content-fragments-models.md) - **空港**&#x200B;モデルなど、構造化コンテンツを必要とするフラグメントの作成に使用されます
   * 使用可能なテンプレートとモデルがすべて表示されます。
   選択した後、「**次へ**」を使用して続けます。

   ![cfm-6420-15](assets/cfm-6420-15.png)

1. In the **Properties** step specify:

   * **基本**

      * **タイトル**

          フラグメントタイトル。

          必須です。

      * **説明**

      * **タグ**
   * **アドバンス**

      * **名前**

         名前がURLの形成に使用されます。

          必須。タイトルから自動的に派生しますが、変更が可能です。


1. 「**作成**」を選択して操作を完了してから、編集するためにフラグメントを&#x200B;**開く**&#x200B;か、「**完了**」でコンソールに戻ります。

## コンテンツフラグメントのアクション {#actions-for-a-content-fragment}

**アセット**&#x200B;コンソールでは、次のいずれかからコンテンツフラグメントに対して様々なアクションを使用できます。

* ツールバーから。フラグメントを選択すると、該当するすべてのアクションを使用できるようになります。
* [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)として。個別のフラグメントカードに使用可能なアクションのサブセット。

![cfm-6420-17](assets/cfm-6420-17.png)

フラグメントを選択して、次の適用可能なアクションを含むツールバーを表示します。

* **ダウンロード**

   * フラグメントを ZIP ファイルとして保存します。要素、バリエーション、メタデータを含めるかどうかを定義できます。

* **作成**
* **チェックアウト**
* **プロパティ**

   * フラグメントのメタデータを表示したり、編集したりできます。

* **編集**

   * Allows you to [open the fragment for editing content](/help/assets/content-fragments-variations.md) together with its elements, variations, associated content and metadata.

* **タグを管理**
* **コレクションに追加**

   * フラグメントをコレクションに追加します。
   * これは、[コレクションをフラグメントと関連付ける](/help/assets/content-fragments-assoc-content.md#adding-associated-content)際に実行できます。

* **コピー**／**貼り付け**

* **移動**
* **クイック公開**
* **公開を管理**
* **削除**

>[!NOTE]
>
>Many of these are [standard actions for Assets](/help/assets/managing-assets-touch-ui.md) and/or the [AEM desktop app](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html).

## フラグメントエディターを開く {#opening-the-fragment-editor}

編集するためにフラグメントを開くには：

>[!CAUTION]
>
>コンテンツフラグメントを編集するには、[適切な権限](/help/sites-developing/customizing-content-fragments.md#asset-permissions)が必要になります。問題が発生している場合は、システム管理者にお問い合わせください。

1. **Assets** コンソールを使用して、コンテンツフラグメントの場所に移動します。
1. フラグメントを開いて編集するには、以下のいずれかを実行します。

   * フラグメントまたはフラグメントリンクをクリック／タップ（これはコンソールビューによって異なります）。
   * Selecting the fragment, then **Edit** from the toolbar.
   フラグメントエディターが開きます。

   ![cfm-6420-18](assets/cfm-6420-18.png)

   >[!NOTE]
   >
   >1. フラグメントがコンテンツページで既に参照されている場合は、メッセージが表示されます。
   >
   >
   >2. The side panel can be hidden/shown using the **Toggle Side Panel** icon.

1. サイドパネルのアイコンを使用して、3 つのモデル間を移動します。

   * バリエーション：[コンテンツの編集](#editing-the-content-of-your-fragment)と[バリエーションの管理](#creating-and-managing-variations-within-your-fragment)

   * [注釈](/help/assets/content-fragments-variations.md#annotating-a-content-fragment)
   * [関連コンテンツ](#associating-content-with-your-fragment)
   * [メタデータ](#viewing-and-editing-the-metadata-properties-of-your-fragment)
   ![cfm-10](assets/cfm-10.png)

1. 変更を加えた後、必要に応じて「**保存**」または「**キャンセル**」をクリックします。

   >[!NOTE]
   >
   >「**保存**」または「**キャンセル**」のどちらをクリックした場合も、エディターが終了します。これらの両方のオプションがコンテンツフラグメントにどのように動作するかについて詳しくは、[保存、キャンセルおよびバージョン](#save-cancel-and-versions)を参照してください。

## 保存、キャンセルおよびバージョン {#save-cancel-and-versions}

>[!NOTE]
>
>バージョン[を作成／比較したり元に戻したりする操作は、タイムラインから](/help/assets/content-fragments-managing.md#timeline-for-content-fragments)もおこなえます。

エディターには次の 2 つのオプションがあります。

* **保存**

   最後の変更を保存し、エディターを終了します。

   >[!CAUTION]
   >
   >コンテンツフラグメントを編集するには、[適切な権限](/help/sites-developing/customizing-content-fragments.md#asset-permissions)が必要になります。問題が発生している場合は、システム管理者にお問い合わせください。

   >[!NOTE]
   >
   >エディターを開いたまま、一連の変更を加えてから「**保存**」を選択することもできます。

   >[!CAUTION]
   >
   >「**保存**」では、変更を保存するだけでなく、参照を更新し、必要に応じてディスパッチャーがフラッシュされます。これらの変更が処理されるまでに時間がかかることがあります。このため、大きなシステムや複雑なシステム、高負荷のシステムのパフォーマンスに影響することがあります。
   >
   >
   >「**保存**」を使用する際はこの点に留意し、フラグメントエディターを迅速に開いて、変更をおこない、保存してください。

* **キャンセル**

   最後の変更を保存せずにエディターを終了します。

コンテンツフラグメントを編集する際には、AEM によって自動的にバージョンが作成されます。これにより、変更内容を&#x200B;**キャンセル**&#x200B;しても以前のコンテンツを復元できるようになります。

1. When a content fragment is opened for editing AEM checks for the existence of the cookie-based token that indicates whether an *editing session* exists:

   1. トークンが見つかると、そのフラグメントは既存の編集セッションの一部であるとみなされます。
   2. トークンが&#x200B;**&#x200B;ないときにユーザーが編集を開始すると、バージョンが作成され、この新しい編集セッションのトークンがクライアントに送られ、cookie に保存されます。

2. **&#x200B;アクティブな編集セッションがあるとき、編集中のコンテンツは自動的に 600 秒ごとに保存されます（デフォルト）。

   >[!NOTE]
   >
   >The auto save interval is configurable using the `/conf` mechanism.
   >
   >
   >デフォルト値については、以下を参照してください。
   >
   >
   >`/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. If the user selects to **Cancel** the edit, the version created at the start of the editing session is restored and the token is removed to end the editing session.
4. If the user selects to **Save** the edits, the updated elements/variations are persisted and the token is removed to end the editing session.

## フラグメントのコンテンツの編集 {#editing-the-content-of-your-fragment}

フラグメントを開いたら、「[バリエーション](/help/assets/content-fragments-variations.md)」タブを使用してコンテンツをオーサリングできます。

## フラグメント内のバリエーションの作成と管理 {#creating-and-managing-variations-within-your-fragment}

マスターコンテンツを作成したら、そのコンテンツの[バリエーション](/help/assets/content-fragments-variations.md)を作成して管理できます。

## コンテンツをフラグメントと関連付ける {#associating-content-with-your-fragment}

フラグメントに[コンテンツを関連付ける](/help/assets/content-fragments-assoc-content.md)こともできます。これにより関連性を付加して、フラグメントをコンテンツページに追加するときに、アセット（画像など）を（オプションで）フラグメントと一緒に使用できるようになります。

## フラグメントのメタデータ（プロパティ）の表示と編集 {#viewing-and-editing-the-metadata-properties-of-your-fragment}

「[メタデータ](/help/assets/content-fragments-metadata.md)」タブを使用し、フラグメントのプロパティを表示して編集できます。

## コンテンツフラグメントのタイムライン {#timeline-for-content-fragments}

[タイムライン](/help/assets/managing-assets-touch-ui.md#timeline)では標準のオプションに加え、コンテンツフラグメントに固有の情報とアクションの両方が提供されます。

* バージョン、コメントおよび注釈に関する情報の表示
* バージョンに関するアクション

   * **[このバージョンに戻す](#reverting-to-a-version)**（既存のフラグメントを選択してから特定のバージョンを選択）

   * **[現在のバージョンと比較](#comparing-fragment-versions)**（既存のフラグメントを選択してから特定のバージョンを選択）

   * **ラベル**&#x200B;や&#x200B;**コメント**&#x200B;の追加（既存のフラグメントを選択してから特定のバージョンを選択）

   * **バージョンとして保存**（既存のフラグメントを選択してからタイムライン下部の上矢印を選択）

* 注釈に関するアクション

   * **削除**

>[!NOTE]
>
>コメントは次のとおりです。
>
>* すべてのアセットの標準機能
>* タイムラインで追加
>* フラグメントアセットに関連付けられる
>
>
注釈（コンテンツフラグメント用）は次のとおりです。
>
>* フラグメントエディターで入力
>* フラグメント内の選択されたテキストセグメントに固有
>



次に例を示します。

![cfm-6420-19-2019](assets/cfm-6420-19-2019.png)

## フラグメントのバージョンの比較 {#comparing-fragment-versions}

特定のバージョンを選択したら、「[タイムライン](/help/assets/content-fragments-managing.md#timeline-for-content-fragments)」から「**現在のバージョンと比較**」アクションを利用できるようになります。

これにより、次の情報が表示されます。

* **現在**（最新）のバージョン（左）

* 選択されたバージョン **v&lt;*x.y*>**（右）

これらは左右に並んで表示されます。この画面について以下で説明します。

* すべての相違点がハイライト表示されます

   * 削除されたテキスト - 赤
   * 挿入されたテキスト - 緑
   * 置き換えられたテキスト - 青

* フルスクリーンアイコンを使用すれば、どちらかのバージョンで開いた後で、並列表示に切り替えることができます
* 特定のバージョンに&#x200B;**戻す**&#x200B;ことができます
* 「**完了**」を選択すると、コンソールに戻ります

>[!NOTE]
>
>フラグメントの比較中にフラグメントコンテンツを編集することはできません。

![cfm-6420-20](assets/cfm-6420-20.png)

## 特定のバージョンに戻す  {#reverting-to-a-version}

次の方法で特定のバージョンのフラグメントに戻すことができます。

* 直接[タイムライン](/help/assets/content-fragments-managing.md#timeline-for-content-fragments)から。

   必要なバージョンを選択した後、「**このバージョンに戻す**」アクションを選択します。

* [あるバージョンと現在のバージョンを比較](/help/assets/content-fragments-managing.md#comparing-fragment-versions)し、選択したバージョンに&#x200B;**戻す**&#x200B;ことができます。

## フラグメントの公開と参照 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>フラグメントがモデルに基づいている場合、その[モデルが公開されている](/help/assets/content-fragments-models.md#publishing-a-content-fragment-model)ことを確認してください。
>
>まだ公開されていないモデルのコンテンツフラグメントを公開すると、選択リストにそのことが示され、モデルがフラグメントと共に公開されます。

コンテンツフラグメントを使用するには、パブリッシュ環境で公開する必要があります。次の方法で公開できます。

* 作成後に **Assets** コンソールから。
* [フラグメントを使用するページを公開](/help/sites-authoring/content-fragments.md#publishing)するとき。フラグメントはページ参照にリスト表示されます。

>[!CAUTION]
>
>フラグメントが公開または参照（あるいは両方）された後に、作成者がフラグメントを開いて編集しようとすると警告が表示され、フラグメントを変更すると、参照されているページにも影響が及ぶことが警告されます。

## フラグメントの削除 {#deleting-a-fragment}

フラグメントを削除するには：

1. **Assets** コンソールで、コンテンツフラグメントの場所に移動します。
2. フラグメントを選択します。

   >[!NOTE]
   >
   >**削除**&#x200B;アクションはクイックアクションとして実行できません。

3. ツールバーから「**削除**」を選択します。
4. 「**削除**」アクションを確認します。

   >[!CAUTION]
   >
   >If the fragment is already referenced in a page you will then see a warning message and be required to confirm that you want to proceed with a **Force Delete**. フラグメントはコンテンツフラグメントコンポーネントと一緒に、すべてのコンテンツページから削除されます。

