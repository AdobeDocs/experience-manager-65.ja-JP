---
title: レターとインタラクティブ通信の後処理
seo-title: レターの後処理
description: 後処理 correspondence Managementのレターの数を使用すると、印刷や電子メールなどのAEMおよびFormsの後処理を作成し、それらをレターに統合できます。
seo-description: Correspondence Management のレターの後処理を使用すると、印刷や電子メールなどの AEM および Forms の後処理を作成し、それらをレターに統合できます。
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# レターとインタラクティブ通信の後処理{#post-processing-of-letters-and-interactive-communications}

## 後処理 {#post-processing}

エージェントはレターおよびインタラクティブ通信上で後処理のワークフローを関連付けて実行できます。実行する後処理は、レターテンプレートのプロパティビューで選択できます。最終レターを電子メールで送信したり、印刷したり、ファックスしたり、あるいはアーカイブしたりするための後処理を設定できます。

![後処理](assets/ppoverview.png)

後処理をレターとインタラクティブ通信に関連付けるには、まず後処理を設定する必要があります。送信済みのレターに対してワークフローを実行するには、次の2種類があります。

1. **フォームワークフロー：** JEE上のAEM Formsのプロセス管理ワークフロー。 Instructions for setting up [Forms Workflow](#formsworkflow).

1. **AEMワークフロー：** AEMワークフローは、送信済みレターの後処理としても使用できます。 [AEM Workflowの設定手順です](../../forms/using/aem-forms-workflow.md)。

## Forms のワークフロー {#formsworkflow}

1. In AEM, open Adobe Experience Manager Web Console Configuration for your server using the following URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Config Manager](assets/2configmanager-1.png)

1. このページで AEM Forms Client SDK Configuration を探し、それをクリックして展開します。
1. In Server URL, enter the name of your AEM Forms on JEE server, login details, and then click **Save**.

   ![Livecycle サーバーの名前を入力します。](assets/1cofigmanager.png)

1. ユーザー名とパスワードを指定します。
1. sun.util.calendarが「ファイアウォールのデシリアライゼーション設定」に追加されていることを確認します。

   「ファイアウォールの設定のデシリアライゼーション」に移動し、「パッケージプリフィックスのホワイトリストクラス」の下で、sun.util.calendarを追加します。

1. これで、サーバーがマッピングされ、JEE上のAEM Formsの後処理が、レターの作成時にAEMユーザーインターフェイスで使用できるようになります。

   ![リスト表示された後処理を使ってレター画面を作成します](assets/0configmanager.png)

1. 処理／サービスを認証するには、処理の名前をコピーし、Adobe Experience Manager Web Console Configurations ページ／AEM Forms Client SDK Configuration に戻ってこのプロセスを新しいサービスとして追加します。

   For example, if the drop-down in Properties page of letter displays name of the process as Forms Workflow -> ValidCCPostProcess/SaveXML, add a Service Name as `ValidCCPostProcess/SaveXML`.

1. JEE 上の AEM Forms ワークフローを使用して後処理を行うには、必要なパラメーターと出力を設定します。パラメーターのデフォルト値を以下に示します。

   Go to the Adobe Experience Manager Web Console Configurations page > **[!UICONTROL Correspondence Management Configurations]** and set up the following parameters:

   1. **inPDFDoc (PDFドキュメントパラメータ):** 入力としてのPDFドキュメント。 この入力はレンダリングされたレターを入力として含みます。示されたパラメータ名は設定可能です。 Correspondence Management設定から設定できます。
   1. **inXMLDoc （XMLデータパラメータ）:** 入力としてのXMLドキュメント。 この入力には、XML形式でユーザーが入力したデータが含まれます。
   1. **inXDPDoc (XDPドキュメントパラメータ):** 入力としてのXMLドキュメント。 この入力には、基になるレイアウト(XDP)が含まれます。
   1. **inAttachmentDocs (Attachmentドキュメントパラメータ):** リスト入力パラメータ。 この入力には、すべての添付ファイルが入力として含まれます。
   1. **redirectURL（リダイレクトURLの出力）:** リダイレクト先のURLを示す出力タイプ。
   フォームワークフローでは、「**[!UICONTROL Correspondence Management の設定]**」で指定した名前を使用して、PDF ドキュメントパラメーターまたは XML データパラメーターのいずれかを入力値として指定する必要があります。これは、後処理ドロップダウンにリスト表示する処理に対しては必須です。

## パブリッシュインスタンスでの設定 {#settings-on-the-publish-instance}

1. にログインしま `https://localhost:publishport/aem/forms`す。
1. 「**[!UICONTROL レター]**」に移動して、パブリッシュインスタンスで使用可能な発行済みレターを表示します。
1. AEM DS の設定を行います。詳しくは、「[AEM DS の設定](../../forms/using/configuring-the-processing-server-url-.md)」を参照してください。

>[!NOTE]
>
>Forms ワークフローまたは AEM ワークフローを使用している場合は、発行サーバーから送信を行う前に、DS 設定サービスを構成する必要があります。このサービスを構成しないと、フォームの送信が失敗します。

## レターインスタンスの取得 {#letter-instances-retrieval}

保存されたレターインスタンスに対しては、LetterInstanceService 内で定義されている次の API を使用して、レターインスタンスの取得やレターインスタンスの削除といった作業を実行できます。

<table>
 <tbody>
  <tr>
   <td><strong>サーバーサイド API</strong></td>
   <td><strong>操作名</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td><p>公開 LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>ICCException；をスロー </p> </td>
   <td>getLetterInstance</td>
   <td>指定したレターインスタンスを取得します </td>
  </tr>
  <tr>
   <td>公開ボイドdeleteLetterInstance(String letterInstanceId)がICCException；をスロー </td>
   <td>deleteLetterInstance </td>
   <td>指定したレターインスタンスを削除しました </td>
  </tr>
  <tr>
   <td>リストgetAllLetterInstances(クエリ)がICCException；をスロー </td>
   <td>getAllLetterInstances </td>
   <td>このAPIは、入力パラメーターに基づいてレターインスタンスをクエリします。 すべてのレターインスタンスを取得するには、クエリパラメーターをヌルとして渡すことができます。<br /> </td>
  </tr>
  <tr>
   <td>公開ブールletterInstanceExists(String letterInstanceName)がICCException；をスロー </td>
   <td>letterInstanceExists </td>
   <td>LetterInstanceが指定した名前で存在するかどうかを確認します。 </td>
  </tr>
 </tbody>
</table>

## 後処置をレターに関連付け {#associating-a-post-process-with-a-letter}

CCR ユーザーインターフェイスで、次の手順を実行して後処理をレターに関連付けます。

1. Hover over a letter and tap **View Properties**.
1. 「**編集**」を選択します。
1. 基本のプロパティで、後処理ドロップダウンを使用して、レターに関連付ける後処理を選択します。AEM および Forms 関連の両方の後処理がドロップダウンリストに表示されます。
1. 「**保存**」をタップします。
1. 「後処理」でのレターの設定が完了したら、レターを発行します。必要な場合は、パブリッシュインスタンスの AEM DS 設定サービスで、処理 URL を指定します。これにより、後処理が処理インスタンス上で実行されるようになります。

## ドラフトレターインスタンスの再読み込み{#reloaddraft}

ドラフトレターインスタンスは、次の URL を使ってユーザーインターフェイス内で再読み込みできます。

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID：送信済みレターインスタンスの一意の ID.

ドラフトレターの保存について詳しくは、「[ドラフトの保存とレターインスタンスの送信](../../forms/using/create-correspondence.md#savingdrafts)」を参照してください。
