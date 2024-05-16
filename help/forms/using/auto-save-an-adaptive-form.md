---
title: アダプティブフォームを自動保存
description: アダプティブフォームを設定して、イベントまたは既定の時間間隔に基づいてコンテンツの自動保存を開始できます。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: ff9bf466-228d-40e6-9389-15c1f2ed1d2e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '736'
ht-degree: 100%

---

# アダプティブフォームの自動保存 {#auto-save-an-adaptive-form}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

アダプティブフォームを設定して、イベントまたは既定の時間間隔に基づいてコンテンツの自動保存を開始できます。デフォルトでは、アダプティブフォームのコンテンツは、保存ボタンを押したときなど、ユーザーアクション時に保存されます。自動保存オプションは次のようなときに便利です。

* 匿名ユーザーおよびログインユーザーに対してコンテンツを自動保存する
* ユーザーの介在をほとんど或いはまったく必要としないでフォームのコンテンツを保存する
* ユーザーのイベントに基づいてフォームのコンテンツの保存を開始する
* 特定の時間間隔が経過するたびにフォームのコンテンツを繰り返し保存する

## アダプティブフォームの自動保存を有効にする {#enable-autosave-for-an-adaptive-form}

アダプティブフォームの場合、自動保存オプションは最初は有効にはなっていません。自動保存オプションは、アダプティブフォームのプロパティの「**自動保存**」セクションで有効にすることができます。「**自動保存**」セクションには、その以外の設定オプションがいくつか用意されています。次の手順を実行して、アダプティブフォームの自動実行オプションを有効にし設定します。

1. プロパティの「自動保存」セクションにアクセスするには、コンポーネントを選択して、![フィールドレベル](assets/field-level.png)／**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択して、「![cmppr](assets/cmppr.png)」を選択します。
1. 「**[!UICONTROL 自動保存]**」セクションで、自動保存オプションを&#x200B;**[!UICONTROL 有効]**&#x200B;にします。
1. **[!UICONTROL アダプティブフォームイベント]**&#x200B;ボックスで、1 または TRUE を指定して、フォームがブラウザーに読み込まれたときに自動保存を開始します。トリガーされて true を返したときにフォームのコンテンツの保存を開始する条件式をイベントに指定することもできます。
1. トリガーを指定します。設定に従い、自動保存がトリガーされます。以下のオプションがあります。

   * **[!UICONTROL 時刻ベース]**：指定の時間間隔に基づいてコンテンツの保存を開始するには、このオプションを選択します。
   * **[!UICONTROL イベントベース]**：イベントがトリガーされたときにコンテンツの保存を開始するには、このオプションを選択します。

   トリガーを選択すると、方法の設定ボックスが有効になります。方法の設定ボックスでは、次のことができます。

   * **[!UICONTROL 時刻ベース]**&#x200B;のトリガーを選択した場合は、時間間隔を指定します。
   * **[!UICONTROL イベントに基づく]**&#x200B;トリガーを選択した場合は、イベントの名前を指定します。

   独自の方法を作成してリストに追加することもできます。詳しくは、[フォームを自動保存するためのカスタム方法を実装](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)を参照してください。

1. （時間ベースの自動保存のみ）次の手順を実行して、時間ベースの自動保存のオプションを設定します。

   1. **[!UICONTROL この間隔で自動保存]**&#x200B;ボックスで、時間間隔を秒数で指定します。間隔ボックスに指定されている秒数が経過するたびに、フォームは繰り返し保存されます。

1. （イベントベースの自動保存のみ）次の手順を実行して、イベントベースの自動保存のためのオプションを設定します。

   1. 「**このイベントの後に自動保存**」ボックスで、[GuideBridge](https://helpx.adobe.com/jp/aem-forms/6/javascript-api/GuideBridge.html) イベントを指定します。式が TRUE に評価されるたびに、フォームが保存されます。

1. （オプション）匿名ユーザーに対するコンテンツを自動的に保存するには、「**匿名ユーザーの自動保存を有効にする**」オプションを選択し、「**[!UICONTROL OK]**」をクリックします。

   >[!NOTE]
   >
   >自動保存オプションを匿名ユーザーに対して機能させるには、すべてのユーザーがフォームのプレビュー、確認および署名を行えるように Forms 共通設定サービスが設定されていることを確認します。
   >
   >このサービスを設定するには、`https://server:port/system/console/configMgr` にある AEM web コンソール設定に移動して **[!UICONTROL Forms 共通設定サービス]** を編集し、「**[!UICONTROL 許可]**」フィールドで「**[!UICONTROL すべてのユーザー]**」オプションを選択して、設定を保存します。

## アダプティブフォームの自動保存を有効にするカスタム方法を実装 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

カスタムイベントを実装して自動保存機能をトリガーできます。次の手順を実行して、カスタムイベントを作成し実装します。

1. クライアントライブラリとクライアントライブラリフォルダーを作成します。手順について詳しくは、[クライアント側ライブラリの使用ドキュメント](/help/sites-developing/clientlibs.md)を参照してください。

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

1. 編集モードでコンポーネントを選択し、![field-level](assets/field-level.png)／**[!UICONTROL アダプティブフォームコンテナ]**／![cmppr](assets/cmppr.png) を選択します。
1. プロパティで「**[!UICONTROL 基本]**」セクションを開きます。**[!UICONTROL クライアントライブラリのカテゴリ]**&#x200B;ボックスで、クライアントライブラリフォルダーの作成時に定義したカテゴリプロパティの値を入力します。
1. 「自動保存」セクションを開きます。**[!UICONTROL このイベント後に自動保存]**&#x200B;ボックスで、クライアントライブラリで既に定義されているカスタムイベントを指定します。「**[!UICONTROL OK]**」をクリックします。
