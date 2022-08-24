---
title: アダプティブフォームの自動保存
seo-title: Auto-save an adaptive form
description: アダプティブフォームを設定して、イベントまたは既定の時間間隔に基づいてコンテンツの自動保存を開始することができます。
seo-description: You can configure an adaptive form to automatically start saving the content based on an event or a pre-defined time-interval
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
feature: Adaptive Forms
exl-id: 948b2c12-895d-49e3-a943-d8fe87174fc4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 100%

---

# アダプティブフォームの自動保存 {#auto-save-an-adaptive-form}

アダプティブフォームを設定して、イベントまたは既定の時間間隔に基づいてコンテンツの自動保存を開始することができます。デフォルトでは、アダプティブフォームのコンテンツは、保存ボタンを押したときなど、ユーザーアクション時に保存されます。自動保存オプションは次のようなときに便利です。

* 匿名ユーザーおよびログインユーザーに対してコンテンツを自動保存する
* ユーザーの介在をほとんどあるいはまったく必要としないでフォームのコンテンツを保存する
* ユーザーのイベントに基づいてフォームのコンテンツの保存を開始する
* 特定の時間間隔が経過したらフォームのコンテンツを繰り返し保存する

## アダプティブフォームの自動保存の有効化 {#enable-autosave-for-an-adaptive-form}

アダプティブフォームの場合、自動保存オプションは最初は有効にはなっていません。自動保存オプションを有効にするには、アダプティブフォームのプロパティの「**自動保存**」セクションで行うことができます。「**自動保存**」セクションには、その以外の設定オプションがいくつか用意されています。次の手順を実行して、アダプティブフォームの自動実行オプションを有効にし設定します。

1. プロパティの「自動保存」セクションにアクセスするには、コンポーネントを選択して、![フィールドレベル](assets/field-level.png)／**[!UICONTROL アダプティブフォームコンテナ]**／ ![cmppr](assets/cmppr.png) の順にタップします。
1. 「**[!UICONTROL 自動保存]**」セクションで、自動保存オプションを&#x200B;**[!UICONTROL 有効]**&#x200B;にします。
1. 「**[!UICONTROL アダプティブフォームイベント]**」ボックスで、1 または TRUE を指定して、フォームがブラウザーに読み込まれたときに自動保存を開始します。トリガーされると true を返してフォームのコンテンツの保存を開始する条件式をイベントに指定することもできます。
1. トリガーを指定します。設定に従い、自動保存がトリガーされます。以下のオプションがあります。

   * **[!UICONTROL 時刻ベース]**：指定の時間間隔に基づいてコンテンツの保存を開始するには、このオプションを選択します。
   * **[!UICONTROL イベントベース]**：イベントがトリガーされたときにコンテンツの保存を開始するには、このオプションを選択します。

   トリガーを選択すると、方法の設定ボックスが有効になります。方法の設定ボックスでは、次のことができます。

   * **[!UICONTROL 時刻ベース]**&#x200B;のトリガーを選択した場合は、時間間隔を指定します。
   * **[!UICONTROL イベントに基づく]**&#x200B;トリガーを選択した場合は、イベントの名前を指定します。

   独自の方法を作成してリストに追加することもできます。詳細については、[フォームを自動保存するためのカスタム方法の実装](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)を参照してください。

1. （時間ベースの自動保存のみ）次の手順を実行して、時間ベースの自動保存のオプションを設定します。

   1. 「**[!UICONTROL この間隔で自動保存]**」ボックスで、時間間隔を秒数で指定します。「間隔」ボックスに指定されている秒数が経過するたびに、フォームは繰り返し保存されます。

1. （イベントベースの自動保存のみ）次の手順を実行して、イベントベースの自動保存のためのオプションを設定します。

   1. 「**このイベントの後に自動保存**」ボックスで、[GuideBridge](https://helpx.adobe.com/jp/aem-forms/6/javascript-api/GuideBridge.html) イベントを指定します。式が TRUE に評価されるたびに、フォームが保存されます。

1. （オプション）匿名ユーザーに対するコンテンツを自動的に保存するには、「**匿名ユーザーの自動保存を有効にする**」オプションを選択し、「**[!UICONTROL OK]**」をクリックします。

   >[!NOTE]
   >
   >自動保存オプションを匿名ユーザーに対して機能させるには、すべてのユーザーがフォームのプレビュー、確認および署名を行えるように Forms 共通設定サービスが設定されていることを確認します。
   >
   >このサービスを設定するには、`https://server:port/system/console/configMgr` にある AEM web コンソール設定に移動して **[!UICONTROL Forms 共通設定サービス]** を編集し、「**[!UICONTROL 許可]**」フィールドで「**[!UICONTROL すべてのユーザー]**」オプションを選択して、設定を保存します。

## アダプティブフォームの自動保存を有効にするカスタム方法の実装 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

カスタムイベントを実装して自動保存機能をトリガーできます。次の手順を実行して、カスタムイベントを実装します。

1. クライアントライブラリとクライアントライブラリフォルダーを作成します。詳細手順については、[クライアント側ライブラリの使用ドキュメント](/help/sites-developing/clientlibs.md)を参照してください。

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

1. 編集モードでコンポーネントを選択し、![フィールドレベル](assets/field-level.png)／**[!UICONTROL アダプティブフォームコンテナ]**／![cmppr](assets/cmppr.png) をタップします。
1. プロパティで「**[!UICONTROL 基本]**」セクションを開きます。「**[!UICONTROL クライアントライブラリのカテゴリ]**」ボックスに、クライアントライブラリフォルダーの作成時に定義したカテゴリプロパティの値を入力します。
1. 「自動保存」セクションを開きます。「**[!UICONTROL このイベント後に自動保存]**」ボックスで、クライアントライブラリですでに定義されているカスタムイベントを指定します。「**[!UICONTROL OK]**」をクリックします。
