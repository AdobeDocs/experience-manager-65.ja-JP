---
title: 「通信を作成」UI へのカスタムアクションまたはボタンの追加
seo-title: Add custom action/button in Create Correspondence UI
description: 「通信を作成」UI にカスタムアクションまたはボタンを追加する方法について説明します。
seo-description: Learn how to add custom action/button in Create Correspondence UI
uuid: 1b2b00bb-93ef-4bfe-9fc5-25c45e4cb4b1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 046e3314-b436-47ed-98be-43d85f576789
docset: aem65
feature: Correspondence Management
exl-id: a582ba41-83cb-46f2-9de9-3752f6a7820a
source-git-commit: ba2c753cfd041ccfcd6ba7a45648234290b99d25
workflow-type: ht
source-wordcount: '1881'
ht-degree: 100%

---

# 通信作成 UI へのカスタムアクションボタンの追加 {#add-custom-action-button-in-create-correspondence-ui}

## 概要 {#overview}

Correspondence Management ソリューションでは、「通信を作成」UI にカスタムアクションを追加できます。

このドキュメントのシナリオでは、通信作成ユーザーインターフェイスにボタンを作成し、レターをレビュー用の PDF として電子メールに添付して共有する方法について説明します。

### 前提条件 {#prerequisites}

このシナリオを完了するには、以下が必要になります。

* CRX および JavaScript についての知識
* LiveCycle サーバー

## シナリオ：通信を作成ユーザーインターフェイスにボタンを作成してレビュー用のレターを送信する {#scenario-create-the-button-in-the-create-correspondence-user-interface-to-send-a-letter-for-review}

通信を作成ユーザーインターフェイスにボタンを追加して、ボタンのアクション（ここではレビュー用のレターの送信）を指定するには、次の操作を行います。

1. 通信を作成ユーザーインターフェイスにボタンを追加します
1. ボタンにアクション処理を追加します
1. LiveCycle プロセスを追加してアクション処理を有効化します

### 通信作成ユーザーインターフェイスへのボタンの追加 {#add-the-button-to-the-create-correspondence-user-interface}

1. `https://'[server]:[port]'/[ContextPath]/crx/de` にアクセスし、管理者としてログインします。
1. config フォルダーにある defaultApp フォルダーに類似したパスまたはフォルダー構造で、`defaultApp` という名前のフォルダーを apps フォルダーに作成します。フォルダーの作成手順は次のとおりです。

   1. 次のパスにある **defaultApp** フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

      /libs/fd/cm/config/defaultApp/

      ![ノードをオーバーレイ](assets/1_defaultapp.png)

   1. 「ノードをオーバーレイ」ダイアログに次の値が表示されていることを確認します。

      **パス**：/libs/fd/cm/config/defaultApp/

      **オーバーレイの場所**：/apps/

      **ノードタイプを一致させる**：オン

      ![ノードをオーバーレイ](assets/2_defaultappoverlaynode.png)

   1. 「**OK**」をクリックします。
   1. 「**すべて保存**」をクリックします。

1. /libs 分岐の下にある acmExtensionsConfig.xml ファイルのコピーを /apps branch の下に作成します。

   1. /libs/fd/cm/config/defaultApp/acmExtensionsConfig.xml に移動します。

   1. acmExtensionsConfig.xml ファイルを右クリックして「**コピー**」を選択します。

      ![acmExtensionsConfig.xml をコピー](assets/3_acmextensionsconfig_xml_copy.png)

   1. 「/apps/fd/cm/config/defaultApp/」にある **defaultApp** フォルダーを右クリックし、「**貼り付け**」を選択します。
   1. 「**すべて保存**」をクリックします。

1. apps フォルダーで新しく作成した acmExtentionsConfig.xml のコピーをダブルクリックします。ファイルが開いて編集可能になります。
1. 次のコードを検索します。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <extensionsConfig>
       <modelExtensions>
           <modelExtension type="LetterInstance">
     <customAction name="Preview" label="loc.letterInstance.preview.label" tooltip="loc.letterInstance.preview.tooltip" styleName="previewButton"/>
               <customAction name="Submit" label="loc.letterInstance.submit.label" tooltip="loc.letterInstance.submit.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="SaveAsDraft" label="loc.letterInstance.saveAsDraft.label" tooltip="loc.letterInstance.saveAsDraft.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="Close" label="loc.letterInstance.close.label" tooltip="loc.letterInstance.close.tooltip" styleName="closeButton"/>
           </modelExtension>
       </modelExtensions>
   </extensionsConfig>
   ```

1. レターをメールで送信するには、LiveCycle Forms ワークフローを使用します。次のように、acmExtensionsConfig.xml の modelExtension タグに customAction タグを追加します。

   ```xml
    <customAction name="Letter Review" label="Letter Review" tooltip="Letter Review" styleName="" permissionName="forms-users" actionHandler="CM.domain.CCRCustomActionHandler">
         <serviceName>Forms Workflow -> SendLetterForReview/SendLetterForReviewProcess</serviceName>
       </customAction>
   ```

   ![customAction タグ](assets/5_acmextensionsconfig_xml.png)

   modelExtension タグには、アクションボタンのアクション、権限、外観を設定する customAction 子タグのセットが含まれています。以下は customAction 設定タグの一覧です。

   | **名前** | **説明** |
   |---|---|
   | name | 実行するアクションを表す英数字の名前。このタグの値は必須です。modelExtension タグ内で一意であり、アルファベットで始まる必要があります。 |
   | label | アクションボタンに表示するラベル。 |
   | tooltip | ボタンのツールチップテキスト。ボタンにカーソルを置くと表示されます。 |
   | styleName | アクションボタンに適用するカスタムスタイルの名前。 |
   | permissionName | ユーザーが permissionName で指定されている権限を持っている場合にのみ、対応するアクションが表示されます。permissionName を `forms-users` として指定すると、このオプションにすべてのユーザーがアクセスできます。 |
   | actionHandler | ユーザーがボタンをクリックすると呼び出される ActionHandler クラスの完全修飾名。 |

   上記のパラメーター以外に、customAction には追加の設定を関連付けることができます。これらの追加の設定は、CustomAction オブジェクトを通じて、ハンドラーで使用できるようにすることができます。

   | **名前** | **説明** |
   |---|---|
   | serviceName | customAction に serviceName という名前の子タグが含まれる場合、関連するボタンまたはリンクをクリックすると、serviceName タグで表される名前でプロセスが呼び出されます。このプロセスで Letter PostProcess と同じ署名が使用されていることを確認します。サービス名に「Forms Workflow ->」プレフィックスを追加します。 |
   | タグ名に cm_ プレフィックスが含まれるパラメーター | customAction に cm_ で始まる名前を持つ子タグが含まれる場合、後処理（レター後処理または serviceName タグで表される特別なプロセス）において、これらのパラメーターは、cm_ プレフィックスを取り除いた関連タグの下の入力 XML コードで使用できます。 |
   | actionName | クリックによって発生した後処理の場合、送信された XML には、ユーザーアクションの名前が付いたタグの下に名前の付いた特別なタグが含まれます。 |

1. 「**すべて保存**」をクリックします。

#### /apps branch 内のプロパティファイルを使用したローカルフォルダーの作成 {#create-a-locale-folder-with-properties-file-in-the-apps-branch}

ACMExtensionsMessages.properties ファイルには、通信の作成ユーザーインターフェイス内のさまざまなフィールドのラベルとツールチップメッセージが含まれています。カスタマイズしたアクションやボタンを機能させるために、/apps branch にこのファイルのコピーを作成します。

1. 次のパスにある **locale** フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

   /libs/fd/cm/config/defaultApp/locale

1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

   **パス**：/libs/fd/cm/config/defaultApp/locale

   **オーバーレイの場所**：/apps/

   **ノードタイプを一致させる**：オン

1. 「**OK**」をクリックします。
1. 「**すべて保存**」をクリックします。
1. 次のファイルを右クリックし、「**コピー**」を選択します。

   `/libs/fd/cm/config/defaultApp/locale/ACMExtensionsMessages.properties`

1. 次のパスにある **locale** フォルダーを右クリックし、「**貼り付け**」を選択します。

   `/apps/fd/cm/config/defaultApp/locale/`

   ACMExtensionsMessages.properties ファイルがローカルフォルダーにコピーされます。

1. 新しく追加されたカスタムアクションまたはボタンのラベルをローカライズするには、関連するロケールの ACMExtensionsMessages.properties ファイルを `/apps/fd/cm/config/defaultApp/locale/` に作成します。

   たとえば、この記事で作成したカスタムアクションまたはボタンをローカライズするには、次のエントリを使用して ACMExtensionsMessages_fr.properties という名前のファイルを作成します。

   `loc.letterInstance.letterreview.label=Revue De Lettre`

   同様に、このファイル内にツールチップやスタイルなどのプロパティを追加することができます。

1. 「**すべて保存**」をクリックします。

#### Adobe Asset Composer 構築ブロックバンドルの再起動 {#restart-the-adobe-asset-composer-building-block-bundle}

サーバー側の変更をすべて加えた後、Adobe Asset Composer 構築ブロックバンドルを再起動します。このシナリオでは、サーバーサイドの acmExtensionsConfig.xml および ACMExtensionsMessages.properties ファイルが編集されるため、Adobe Asset Composer 構築ブロックバンドルを再起動する必要があります。

>[!NOTE]
>
>ブラウザーのキャッシュをクリアする必要が生じる場合があります。

1. `https://[host]:'port'/system/console/bundles` にアクセスします。必要に応じて、管理者としてログインします。

1. Adobe Asset Composer 構築ブロックバンドルを検索します。バンドルを再起動します。「停止」をクリックした後、「開始」をクリックします。

   ![Adobe Asset Composer 構築ブロック](assets/6_assetcomposerbuildingblockbundle.png)

Adobe Asset Composer 構築ブロックバンドルを再起動した後、通信を作成ユーザーインターフェイスにカスタムボタンが表示されます。通信を作成ユーザーインターフェイスでレターを開いて、カスタムボタンをプレビューできます。

### ボタンへのアクション処理の追加 {#add-action-handling-to-the-button}

通信を作成ユーザーインターフェイスはデフォルトで、次の場所にある cm.domain.js ファイルの ActionHandler を実装します。

/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccr/js/cm.domain.js

カスタムのアクション処理の場合は、CRX の /apps branch にある cm.domain.js ファイルのオーバーレイを作成します。

アクションまたはボタンをクリックする際のアクションやボタンの処理には、次に対応するためのロジックが含まれています。

* 新しく追加したアクションを表示または非表示にする：actionVisible() 関数をオーバーライドして実行します。
* 新しく追加したアクションを有効または無効にする：actionEnabled() 関数をオーバーライドして実行します。
* ユーザーがボタンをクリックしたときの実際のアクションの処理：handleAction() 関数の実装をオーバーライドして実行します。

1. `https://'[server]:[port]'/[ContextPath]/crx/de` にアクセスします。必要に応じて、管理者としてログインします。

1. apps フォルダーに、次のフォルダーに類似した構造で、CRX の /apps branch に `js` という名前のフォルダーを作成します。

   `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   フォルダーの作成手順は次のとおりです。

   1. 次のパスにある **js** フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。

      `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   1. ノードをオーバーレイダイアログに次の値が表示されていることを確認します。

      **パス**：/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js

      **オーバーレイの場所**：/apps/

      **ノードタイプを一致させる**：オン

   1. 「**OK**」をクリックします。
   1. 「**すべて保存**」をクリックします。

1. 次の手順を使用し、ccrcustomization.js という名前のファイルを js フォルダーに作成し、ボタンのアクション処理のコードを指定します。

   1. 次のパスにある **js** フォルダーを右クリックし、「**作成／ファイルを作成**」を選択します。

      `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

      ファイルに ccrcustomization.js という名前を付けます。

   1. ccrcustomization.js ファイルをダブルクリックして、CRX で開きます。
   1. ファイルに次のコードを貼り付けて、「**すべて保存**」をクリックします。

      ```javascript
      /* for adding and handling custom actions in Extensible Toolbar.
        * One instance of handler will be created for each action.
        * CM.domain.CCRCustomActionHandler is actionHandler class.
        */
      var CCRCustomActionHandler;
          CCRCustomActionHandler = CM.domain.CCRCustomActionHandler = new Class({
              className: 'CCRCustomActionHandler',
              extend: CCRDefaultActionHandler,
              construct : function(action,model){
              }
          });
          /**
           * Called when user user click an action
           * @param extraParams additional arguments that may be passed to handler (For future use)
           */
          CCRCustomActionHandler.prototype.handleAction = function(extraParams){
              if (this.action.name == CCRCustomActionHandler.SEND_FOR_REVIEW) {
                  var sendForReview = function(){
                      var serviceName = this.action.actionConfig["serviceName"];
                      var inputParams = {};
                      inputParams["dataXML"] = this.model.iccData.data;
                      inputParams["letterId"] = this.letterVO.id;
                      inputParams["letterName"] = this.letterVO.name;
                      inputParams["mailId"] = $('#email').val();
                      /*function to invoke the LivecyleService */
                      ServiceDelegate.callJSONService(this,"lc.icc.renderlib.serviceInvoker.json","invokeProcess",[serviceName,inputParams],this.onProcessInvokeComplete,this.onProcessInvokeFail);
                      $('#ccraction').modal("hide");
                  }
                  if($('#ccraction').length == 0){
                      /*For first click adding popup & setting letterName.*/
                      $("body").append(popUp);
                      $("input[id*='letterName']").val(this.letterVO.name);
                      $(document).on('click',"#submitLetter",$.proxy( sendForReview, this ));
                  }
                  $('#ccraction').modal("show");
              }
          };
          /**
           * Should the action be enabled in toolbar
           * @param extraParams additional arguements that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
         CCRCustomActionHandler.prototype.actionEnabled = function(extraParams){
                  /*can be customized as per user requirement*/
                  return true;
          };
          /**
           * Should the action be visible in toolbar
           * @param extraParams additional arguments that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
          CCRCustomActionHandler.prototype.actionVisible = function(extraParams){
              /*Check can be enabled for Non-Preview Mode.*/
              return true;
          };
          /*SuccessHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeComplete = function(response) {
              ErrorHandler.showSuccess("Letter Sent for Review");
          };
          /*FaultHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeFail = function(event) {
              ErrorHandler.showError(event.message);
          };
          CCRCustomActionHandler.SEND_FOR_REVIEW  = "Letter Review";
      /*For PopUp*/
          var popUp = '<div class="modal fade" id="ccraction" tabindex="-1" role="dialog" aria-hidden="true">'+
          '<div class="modal-dialog modal-sm">'+
              '<div class="modal-content">' +
                  '<div class="modal-header">'+
                      '<button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</code></button>'+
                      '<h4 class="modal-title"> Send Review </h4>'+
                  '</div>'+
                  '<div class="modal-body">'+
                      '<form>'+
                          '<div class="form-group">'+
                              '<label class="control-label">Email Id</label>'+
                              '<input type="text" class="form-control" id="email">'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<label  class="control-label">Letter Name</label>'+
                              '<input id="letterName" type="text" class="form-control" readonly>'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<input id="letterData" type="text" class="form-control hide" readonly>'+
                          '</div>'+
                      '</form>'+
                  '</div>'+
                  '<div class="modal-footer">'+
                     '<button type="button" class="btn btn-default" data-dismiss="modal"> Cancel </button>'+
                     '<button type="button" class="btn btn-primary" id="submitLetter"> Submit </button>'+
                  '</div>'+
              '</div>'+
          '</div>'+
      '</div>';
      ```

### LiveCycle プロセスの追加によるアクション<span class="acrolinxCursorMarker"></code>処理の有効化 {#add-the-livecycle-process-to-enable-action-span-class-acrolinxcursormarker-span-handling}

このシナリオでは、以下のコンポーネントを有効にします。これらのコンポーネントは、添付されている components.zip ファイルに含まれています。

* DSC コンポーネント jar（DSCSample.jar）
* レビュープロセス LCA（SendLetterForReview.lca）用の送信レター

components.zip ファイルをダウンロードして解凍し、DSCSample.jar および SendLetterForReview.lca ファイルを取得します。これらのファイルは、次の手順に従って使用します。
[ファイルを入手](assets/components.zip)

#### LiveCycle サーバーの設定と LCA プロセスの実行 {#configure-the-livecycle-server-to-run-the-lca-process}

>[!NOTE]
>
>この手順が必要となるのは、OSGI セットアップを使用していて、実装しているカスタマイズのタイプで LC 統合が必要になる場合に限られます。

LCA プロセスは LiveCycle サーバー上で実行され、サーバーアドレスとログイン情報が必要になります。

1. `https://'[server]:[port]'/system/console/configMgr` にアクセスし、Admin でログインしてください。
1. Adobe LiveCycle Client SDK 設定を見つけて、**編集**（編集アイコン）をクリックしてください。設定パネルが開きます。

1. 次の詳細を入力し、「**保存**」をクリックしてください。

   * **サーバー URL**：LC Server の URL。アクション処理コードはこのレビュー用に送信サービスを使用します。
   * **ユーザー名**：LC Server の管理者ユーザー名
   * **パスワード**：管理者ユーザー名のパスワード

   ![Adobe LiveCycle Client SDK Configuration](assets/3_clientsdkconfiguration.png)

#### LiveCycle アーカイブ（LCA）のインストール {#install-livecycle-archive-lca}

電子メールサービスプロセスを有効にするための必須の LiveCycle プロセスです。

>[!NOTE]
>
>このプロセスの処理を表示するか、独自の類似プロセスを作成するには、Workbench が必要になります。

1. `https:/[lc server]/:[lc port]/adminui` で、LiveCycle® サーバーに管理者としてログインします。

1. **ホーム／サービス／アプリケーションおよびサービス／アプリケーションの管理**&#x200B;に移動します。

1. SendLetterForReview アプリケーションが既に存在する場合は、残りの手順をスキップします。存在しない場合は、次の手順を続行します。

   ![UI 内の SendLetterForReview アプリケーション](assets/12_applicationmanagementlc.png)

1. **インポート**&#x200B;をクリックします。

1. **ファイルを選択**&#x200B;をクリックしてから、SendLetterForReview.lca を選択してください。

   ![SendLetterForReview.lca ファイルを選択します](assets/14_sendletterforreview_lca.png)

1. **プレビュー**&#x200B;をクリックします。

1. **読み込みの完了時にアセットをランタイムにデプロイ**&#x200B;を選択します。

1. 「**インポート**」をクリックします。

#### 許可リストサービスリストへの ServiceName の追加 {#adding-servicename-to-the-allowlist-service-list}

Experience Manager サーバーにアクセスする必要のある LiveCycle サービスを Experience Manager サーバーで指定します。

1. `https:/[host]:'port'/system/console/configMgr` に管理者としてログインします。

1. **Adobe LiveCycle Client SDK Configuration** を検索してクリックします。Adobe LiveCycle Client SDK Configuration パネルが表示されます。
1. サービス名リストで「 + 」アイコンをクリックし、serviceName **SendLetterForReview/SendLetterForReviewProcess** を追加します。

1. 「**保存**」をクリックします。

#### 電子メールサービスの設定 {#configure-the-email-service}

このシナリオでは、Correspondence Management で電子メールを送信できるようにするため、LiveCycle サーバーで電子メールサービスを設定します。

1. 管理者の資格情報を使用して、`https:/[lc server]:[lc port]/adminui` から Livecycle サーバーにログインします。

1. **ホーム／サービス／アプリケーションおよびサービス／サービスの管理**&#x200B;に移動します。

1. **EmailService**&#x200B;を検索してクリックします。

1. **SMTP ホスト**&#x200B;で、メールサービスを設定します。

1. 「**保存**」をクリックします。

#### DSC サービスの設定 {#configure-the-dsc-service}

Correspondence Management API を使用するには、DSCSample.jar（このドキュメントに添付されている components.zip に含まれています）をダウンロードしてから、LiveCycle サーバーにアップロードしてください。DSCSample.jar ファイルが LiveCycle サーバーにアップロードされると、Experience Manager サーバーは DSCSample.jar ファイルを使用して renderLetter API にアクセスします。

詳細は、[AEM Forms と Adobe LiveCycle の接続](/help/forms/using/aem-livecycle-connector.md)を参照してください。

1. DSCSample.jar の cmsa.properties で Experience Manager サーバーの URL を更新します。次の場所にあります。

   DSCSample.jar\com\adobe\livecycle\cmsa.properties

1. 設定ファイルに次のパラメーターを指定します。

   * **crx.serverUrl**=https:/host:port/[context path]/[AEM URL]
   * **crx.username**=Experience Manager のユーザー名
   * **crx.password**=Experience Manager のパスワード
   * **crx.appRoot**=/content/apps/cm

   >[!NOTE]
   >
   >サーバーサイドで変更を加えるたびに LiveCycle サーバーは再起動します。

   DSCSample.jar ファイルは renderLetter API を使用します。renderLetter API について詳しくは、[インターフェイス LetterRenderService](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html)を参照してください。

#### LiveCyle への DSC の読み込み {#import-dsc-to-livecyle}

DSCSample.jar ファイルは renderLetter API を使用して、DSC で入力された XML データの PDF バイトとしてレターをレンダリングします。renderLetter およびその他の API について詳しくは、「[レターのレンダリングサービス](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html)」を参照してください。

1. Livecycle Workbenchを起動してログインします。
1. **Window／表示を確認／コンポーネント**&#x200B;をクリックします。コンポーネント表示が Workbench ES2 に追加されます。

1. 「**コンポーネント**」を右クリックし、「**コンポーネントをインストールt**」を選択します。

1. ファイルブラウザーで **DSCSample.jar** ファイルを選択し、「**開く**」をクリックします。
1. 「**RenderWrapper**」を右クリックし、「**コンポーネントを開始**」を選択します。コンポーネントが起動すると、コンポーネント名の横に緑色の矢印が表示されます。

## レビュー用のレターの送信 {#send-letter-for-review}

レビュー用のレターを送信するためのアクションとボタンを設定した後、次の操作を行います。

1. ブラウザーのキャッシュをクリアします。

1. 通信作成 UI で「**レターをレビュー**」をクリックし、レビュー担当者のメール ID を指定します。

1. 「**送信**」をクリックします。

![sendreview](assets/sendreview.png)

レビュー担当者は、PDF ファイルとして添付されたレターが含まれる電子メールを受信します。
