---
title: アダプティブフォームの自動保存
seo-title: アダプティブフォームの自動保存
description: アダプティブフォームを設定して、イベントまたは既定の時間間隔に基づいてコンテンツの自動保存を開始することができます。
seo-description: アダプティブフォームを設定して、イベントまたは既定の時間間隔に基づいてコンテンツの自動保存を開始することができます。
uuid: 0fe9a389-269b-438a-9489-d9d1d09558a1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: d519ac4e-6d29-4a69-874e-792acabe87ff
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# アダプティブフォームの自動保存 {#auto-save-an-adaptive-form}

アダプティブフォームを設定して、イベントまたは既定の時間間隔に基づいてコンテンツの自動保存を開始することができます。デフォルトでは、アダプティブフォームのコンテンツは、保存ボタンを押したときなど、ユーザーアクション時に保存されます。自動保存オプションは次のようなときに便利です。

* 匿名ユーザーおよびログインユーザーに対してコンテンツを自動保存する
* ユーザーの介在をほとんどあるいはまったく必要としないでフォームのコンテンツを保存する
* ユーザーのイベントに基づいてフォームのコンテンツの保存を開始する
* 特定の時間間隔が経過したらフォームのコンテンツを繰り返し保存する

## アダプティブフォームの自動保存の有効化 {#enable-autosave-for-an-adaptive-form}

アダプティブフォームの場合、自動保存オプションは最初は有効にはなっていません。自動保存オプションを有効にするには、アダプティブフォームのプロパティの「**自動保存**」セクションで行うことができます。「**自動保存**」セクションには、その他の設定オプションがいくつか用意されています。次の手順を実行して、アダプティブフォームの自動実行オプションを有効にし設定します。

1. To access the auto-save section in the properties, select a component, then tap ![field-level](assets/field-level.png) > **[!UICONTROL Adaptive Form Container]**, and then tap ![cmppr](assets/cmppr.png).
1. 「**[!UICONTROL 自動保存]**」セクションで、自動保存オプションを&#x200B;**[!UICONTROL 有効]**&#x200B;にします。
1. 「**[!UICONTROL アダプティブフォームイベント]**」ボックスで、1 または TRUE を指定して、フォームがブラウザーに読み込まれたときに自動保存を開始します。トリガーされると true を返してフォームのコンテンツの保存を開始する条件式をイベントに指定することもできます。
1. トリガーを指定します。設定に従い、自動保存がトリガーされます。次のオプションがあります。

   * **[!UICONTROL 時刻に基づいた自動保存]**：特定の時間間隔に基づいてコンテンツの保存を開始するには、このオプションを選択します。
   * **[!UICONTROL イベントに基づいた自動保存]**：イベントがトリガーされたときにコンテンツの保存を開始するには、このオプションを選択します。
   トリガーを選択すると、方法の設定ボックスが有効になります。方法の設定ボックスでは、次のことができます。

   * **[!UICONTROL 時刻に基づいた自動保存]**&#x200B;トリガーを選択した場合は、時間間隔を指定します。
   * Specify an event name if you select **[!UICONTROL Event based]** trigger.
   独自の方法を作成してリストに追加することもできます。詳細については、[フォームを自動保存するためのカスタム方法の実装](/help/forms/using/auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p)を参照してください。

1. （時間ベースの自動保存のみ）次の手順を実行して、時間ベースの自動保存のオプションを設定します。

   1. 「**[!UICONTROL この間隔で自動保存]**」ボックスで、時間間隔を秒数で指定します。「間隔」ボックスに指定されている秒数が経過するたびに、フォームは繰り返し保存されます。

1. （イベントベースの自動保存のみ）次の手順を実行して、イベントベースの自動保存のためのオプションを設定します。

   1. In th **Auto save after this event** box, specify a [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) event. 式が TRUE に評価されるたびに、フォームが保存されます。

1. （オプション）匿名ユーザーに対するコンテンツを自動保存するには、「**匿名のユーザーの自動保存を有効にする**」オプションを選択し、「**[!UICONTROL OK]**」をクリックします。

   >[!NOTE]
   >
   >自動保存オプションが匿名ユーザーに対して機能するには、すべてのユーザーにフォームのプレビュー、確認および署名を許可するように Forms Common Configuration Service が設定されていることを確認します。
   >
   >To configure the service, go to AEM Web Console configuration at `https://server:port/system/console/configMgr` and edit the **[!UICONTROL Forms Common Configuration Service]** to choose the **[!UICONTROL All Users]** option in the **[!UICONTROL Allow]** field, and save the configuration.

## アダプティブフォームの自動保存を有効にするカスタム方法の実装 {#implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms}

カスタムイベントを実装して自動保存機能をトリガーできます。次の手順を実行して、カスタムイベントを実装します。

1. クライアントライブラリとクライアントライブラリフォルダーを作成します。詳細手順については、[クライアント側ライブラリの使用ドキュメント](/help/sites-developing/clientlibs.md)を参照してください。

   For example, the following script uses the custom `emailFocusChange`event to trigger the autosave functionality:

   ```
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

1. In the edit mode, select a component, then tap ![field-level](assets/field-level.png) > **[!UICONTROL Adaptive Form Container]**, and then tap ![cmppr](assets/cmppr.png).
1. プロパティで「**[!UICONTROL 基本]**」セクションを開きます。「**[!UICONTROL クライアントライブラリのカテゴリ]**」ボックスに、クライアントライブラリフォルダーの作成時に定義したカテゴリプロパティの値を入力します。
1. 「自動保存」セクションを開きます。「**[!UICONTROL このイベント後に自動保存]**」ボックスで、クライアントライブラリですでに定義されているカスタムイベントを指定します。「**[!UICONTROL OK]**」をクリックします。

