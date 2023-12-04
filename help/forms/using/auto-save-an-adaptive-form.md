---
title: アダプティブフォームの自動保存
seo-title: Auto-save an adaptive form
description: アダプティブフォームを設定して、イベントまたは事前定義された時間間隔に基づいてコンテンツの自動保存を開始することができます
seo-description: You can configure an adaptive form to automatically start saving the content based on an event or a pre-defined time-interval
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Adaptive Forms
exl-id: 948b2c12-895d-49e3-a943-d8fe87174fc4
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 38%

---

# アダプティブフォームの自動保存 {#auto-save-an-adaptive-form}

<span class="preview"> Adobeでは、最新の拡張可能なデータキャプチャを使用することをお勧めします [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja) 対象： [新しいアダプティブFormsの作成](/help/forms/using/create-an-adaptive-form-core-components.md) または [AEM SitesページへのアダプティブFormsの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を示すものであり、優れたユーザーエクスペリエンスを実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成するより従来的な方法について説明します。</span>

アダプティブフォームを設定して、イベントまたは事前定義された時間間隔に基づいてコンテンツの保存を自動的に開始することができます。 デフォルトでは、アダプティブフォームのコンテンツは、保存ボタンを押したときなど、ユーザーの操作時に保存されます。 自動保存オプションは、次の場合に役立ちます。

* 匿名ユーザーおよびログインユーザー向けにコンテンツを自動的に保存
* ユーザーの介入をほとんどまたはほとんど必要とせずにフォームのコンテンツを保存する
* ユーザーイベントに基づいてフォームのコンテンツの保存を開始する
* 指定した時間間隔の後で繰り返しフォームのコンテンツを保存する

## アダプティブフォームの自動保存を有効にする {#enable-autosave-for-an-adaptive-form}

アダプティブフォームの場合、自動保存オプションは初期状態では有効になっていません。 自動保存オプションは、 **自動保存** 」セクションを使用して、アダプティブフォームのプロパティに関する情報を入力できます。 「**自動保存**」セクションには、その以外の設定オプションがいくつか用意されています。次の手順を実行して、アダプティブフォームの自動実行オプションを有効にし設定します。

1. プロパティの自動保存セクションにアクセスするには、コンポーネントを選択し、「 ![フィールドレベル](assets/field-level.png) > **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択し、 ![cmppr](assets/cmppr.png).
1. Adobe Analytics の **[!UICONTROL 自動保存]** セクション **[!UICONTROL 有効にする]** 自動保存オプション。
1. Adobe Analytics の **[!UICONTROL アダプティブフォームイベント]** ボックスに 1 を指定するか、TRUE を指定すると、フォームがブラウザに読み込まれたときに自動的にフォームの保存が開始されます。 また、イベントの条件式を指定すると、そのイベントがトリガーされて true が返され、フォームのコンテンツの保存が開始されます。
1. トリガー。 自動保存は、設定に基づいてトリガーされます。 以下のオプションがあります。

   * **[!UICONTROL 時刻ベース]**：指定の時間間隔に基づいてコンテンツの保存を開始するには、このオプションを選択します。
   * **[!UICONTROL イベントベース]**：イベントがトリガーされたときにコンテンツの保存を開始するには、このオプションを選択します。

   「トリガー」を選択すると、「方法の設定」ボックスが有効になります。 「方法の設定」ボックスでは、次の操作を実行できます。

   * **[!UICONTROL 時刻ベース]**&#x200B;のトリガーを選択した場合は、時間間隔を指定します。
   * **[!UICONTROL イベントに基づく]**&#x200B;トリガーを選択した場合は、イベントの名前を指定します。

   また、独自のカスタム方法を作成してリストに追加することもできます。 詳しくは、 [フォームを自動保存するためのカスタム方法の実装](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p).

1. （時間ベースの自動保存のみ）次の手順を実行して、時間ベースの自動保存のオプションを設定します。

   1. Adobe Analytics の **[!UICONTROL この間隔で自動保存]** ボックスに、時間間隔を秒単位で指定します。 「間隔」ボックスに指定した秒数が経過すると、フォームは繰り返し保存されます。

1. （イベントベースの自動保存のみ）次の手順を実行して、イベントベースの自動保存のオプションを設定します。

   1. 「**このイベントの後に自動保存**」ボックスで、[GuideBridge](https://helpx.adobe.com/jp/aem-forms/6/javascript-api/GuideBridge.html) イベントを指定します。式が TRUE に評価されるたびに、フォームが保存されます。

1. （オプション）匿名ユーザーに対するコンテンツを自動的に保存するには、「**匿名ユーザーの自動保存を有効にする**」オプションを選択し、「**[!UICONTROL OK]**」をクリックします。

   >[!NOTE]
   >
   >自動保存オプションを匿名ユーザーに対して機能させるには、すべてのユーザーがフォームのプレビュー、確認および署名を行えるように Forms 共通設定サービスが設定されていることを確認します。
   >
   >このサービスを設定するには、`https://server:port/system/console/configMgr` にある AEM web コンソール設定に移動して **[!UICONTROL Forms 共通設定サービス]** を編集し、「**[!UICONTROL 許可]**」フィールドで「**[!UICONTROL すべてのユーザー]**」オプションを選択して、設定を保存します。

## アダプティブフォームの自動保存を有効にするカスタム方法を実装する {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

カスタムイベントを実装して自動保存機能をトリガー化できます。 次の手順を実行して、カスタムイベントを作成し実装します。

1. クライアントライブラリとクライアントライブラリフォルダーを作成します。 詳細な手順については、 [クライアント側ライブラリドキュメントの使用](/help/sites-developing/clientlibs.md).

   例えば、次のスクリプトでは、カスタムの `emailFocusChange` イベントを使用して自動保存機能をトリガーしています。

   ```javascript
   window.addEventListener("bridgeInitializeStart", function (){
       guideBridge.connect(function () { guideBridge.on("elementFocusChanged", function (event,data) {
           if(data.target.name === 'Email') {
               guideBridge.trigger("emailFocusChange");
           }
       });
      });
   });
   ```

   >[!NOTE]
   >
   >クライアントライブラリフォルダーの作成時に、カテゴリプロパティが定義されます。カテゴリプロパティに割り当てた値を書き留めておきます。

1. アダプティブフォームを作成者モードで開きます。

1. 編集モードで、コンポーネントを選択し、「 」を選択します。 ![フィールドレベル](assets/field-level.png) > **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択し、 ![cmppr](assets/cmppr.png).
1. プロパティで、 **[!UICONTROL 基本]** 」セクションに入力します。 Adobe Analytics の **[!UICONTROL クライアントライブラリカテゴリ]** 「 」ボックスに、クライアントライブラリフォルダーの作成時に定義した category プロパティの値を入力します。
1. 「自動保存」セクションを開きます。 Adobe Analytics の **[!UICONTROL このイベント後に自動保存]** ボックスに、クライアントライブラリで既に定義されているカスタムイベントを指定します。 「**[!UICONTROL OK]**」をクリックします。
