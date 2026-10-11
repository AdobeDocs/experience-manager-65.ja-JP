---
title: AEM Forms Workspace でのサードパーティアプリケーションの統合
description: AEM Forms Workspace で Correspondence Management などのサードパーティアプリケーションを統合します。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 39a3f7db-549f-47f3-8d4f-42d583a4532d
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 97%
---
# AEM Forms Workspace でのサードパーティアプリケーションの統合{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms Workspace では、フォームおよびドキュメントでタスクの割り当ておよび完了アクティビティの管理をサポートしています。 これらのフォームおよびドキュメントは、XDP、PDF、HTML、または Flex 形式にレンダリングされた XDP フォーム、Flex® フォーム、またはガイド（非推奨）にすることができます。

これらの機能はさらに拡張されます。 AEM Forms では、AEM Forms Workspace と同じ機能をサポートするサードパーティアプリケーションとの統合をサポートしています。 この機能の共通の部分は、割り当てのワークフローとタスクの事後承認です。 AEM Forms では、AEM Forms エンタープライズユーザーに単一の統合された操作性を提供することによって、タスクの割り当てやサポートされているアプリケーションの承認などのすべてを AEM Forms Workspace 経由で処理できるようにします。

例として、AEM Forms Workspace との統合にサンプル候補として Correspondence Management を考慮してみましょう。 Correspondence Management には、「レター」という概念があります。レターをレンダリングし、レターに対してアクションを実行できます。

## Correspondence Management アセットの作成 {#create-correspondence-management-assets}

まず、AEM Forms Workspace にレンダリングされたサンプル Correspondence Management テンプレートを作成します。 詳しくは、[レターテンプレートを作成](../../forms/using/create-letter.md)を参照してください。

Correspondence Management テンプレートにその URL でアクセスして Correspondence Management テンプレートが正常にレンダリングすることができるかどうか確認します。 URL は `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;` のようなパターンを持っています。

ここで、`encodedLetterId` は URL エンコードされたレター ID です。 ワークベンチで Workspace タスクにレンダリングプロセスを定義する場合は、同じレター ID を指定します。

## AEM Workspace でレターをレンダリングして送信するタスクを作成 {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

これらの手順を実行する前に、次のグループのメンバーであることを確認してください。

* cm-agent-users
* Workspace ユーザー

詳しくは、[ユーザーの追加と設定](/help/forms/using/admin-help/adding-configuring-users.md)を参照してください。

AEM Workspace でレターをレンダリングして送信するタスクを作成するには、次の手順を実行します。

1. ワークベンチを起動します。 ローカルホストに管理者としてログインします。
1. ファイル／新規／アプリケーションをクリックします。 アプリケーション名フィールドで、`CMDemoSample` を入力して「終了」をクリックします。
1. 「`CMDemoSample/1.0`」を選択して、「`NewProcess`」を右クリックします。 名前フィールドで、`CMRenderer` を入力して「終了」をクリックします。
1. スタートポイントアクティビティピッカーをドラッグして設定します。

   1. プレゼンテーションデータで、「CRX アセットの使用」を選択します。

      ![useacrxasset](assets/useacrxasset.png)

   1. アセットを参照します。 フォームアセットの選択ダイアログの「レター」タブに、サーバー上のすべてのレターが表示されます。

      ![「レター」タブ](assets/letter_tab_new.png)

   1. 適切なレターを選択して、「**OK**」をクリックします。

1. 「アクションプロファイルの管理」をクリックします。 アクションプロファイルの管理ダイアログが表示されます。 レンダリングプロセスと送信プロセスが正しく選択されていることを確認します。
1. データ XML ファイルを使用してレターを開くために、データの準備プロセスで適切なデータファイルを参照して選択します。
1. 「OK」をクリックします。
1. スタートポイント出力とタスク添付ファイルの変数を定義します。 定義した変数には、スタートポイント出力とタスクの添付ファイルのデータが格納されます。
1. （オプション）ワークフローに別のユーザーを追加するには、アクティビティピッカーをドラッグして設定し、ユーザーに割り当てます。 カスタムラッパー（以下のサンプルを参照）を作成するか、DSC（以下参照）をダウンロードしてインストールし、レターテンプレート、スタートポイント出力、タスクの添付ファイルを展開します。

   カスタムラッパーのサンプルは次のとおりです。

   ```javascript
   public LetterInstanceInfo getLetterInstanceInfo(Document dataXML) throws Exception {
   try {
   if(dataXML == null)
   throw new Exception("dataXML is missing");
   
   CoreService coreService = getRemoteCoreService();
   if (coreService == null)
   throw new Exception("Unable to retrive service. Please verify connection details.");
   Map<String, Object> result = coreService.getLetterInstanceInfo(IOUtils.toString(dataXML.getInputStream(), "UTF-8"));
   LetterInstanceInfo letterInstanceInfo = new LetterInstanceInfo();
   
   List<Document> attachmentDocs = new ArrayList<Document>();
   List<byte[]> attachments = (List<byte[]>)result.get(CoreService.ATTACHMENT_KEY);
   if (attachments != null){
   for (byte[] attachment : attachments)
   { attachmentDocs.add(new Document(attachment)); }
   
   }
   letterInstanceInfo.setLetterAttachments(attachmentDocs);
   
   byte[] updateLayout = (byte[])result.get(CoreService.LAYOUT_TEMPLATE_KEY);
   if (updateLayout != null)
   { letterInstanceInfo.setLetterTemplate(new Document(updateLayout)); }
   
   else
   { throw new Exception("template bytes missing while getting Letter instance Info."); }
   
   return letterInstanceInfo;
   } catch (Exception e)
   { throw new Exception(e); }
   
   }
   ```

   [&#x200B; ファイルを取得](assets/dscsample.zip)
   DSCのダウンロード：サンプル DSCは、上記のDSCSample.zip ファイルで入手できます。 DSCSample.zip ファイルをダウンロードして展開します。 DSC サービスを使用する前に、設定する必要があります。 [DSC サービスを設定](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p)を参照してください。

   アクティビティを定義ダイアログで、適切なアクティビティ（getLetterInstanceInfo など）を選択し、「**OK**」をクリックします。

1. アプリケーションをデプロイします。 指示があったら、アセットをチェックインして保存します。
1. https://'[server]:[port]'/lc/content/ws の AEM Forms Workspace にログインします。
1. 追加したタスクである CMRenderer を開きます。 Correspondence Management レターが表示されます。

   ![cminworkspace](assets/cminworkspace.png)

1. 必要なデータを入力してレターを送信します。 ウィンドウが閉じます。 このプロセスでは、手順 9 のワークフローで指定したユーザーにタスクが割り当てられます。

   >[!NOTE]
   >
   >「送信」ボタンは、レター内の必要な変数がすべて入力されるまで有効になりません。
