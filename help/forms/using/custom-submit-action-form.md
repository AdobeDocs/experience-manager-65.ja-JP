---
title: アダプティブフォーム向けのカスタム送信アクションの作成
description: AEM Forms では、アダプティブフォーム向けのカスタム送信アクションを作成することができます。この記事では、アダプティブフォームのカスタム送信アクションを追加する手順について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c3d0dac-4e19-4eb3-a43d-909d526acd55
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 91%

---

# アダプティブフォーム向けのカスタム送信アクションの作成 {#writing-custom-submit-action-for-adaptive-forms}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/custom-submit-action-form.html?lang=ja) |
| AEM 6.5 | この記事 |

アダプティブフォームでは、ユーザー指定のデータを処理するために、送信アクションが必要となります。送信アクションとは、アダプティブフォームを使って送信されるデータに対して実行されるタスクを決定するものです。Adobe Experience Manager (AEM) の [標準の送信アクション](../../forms/using/configuring-submit-actions.md) ユーザーが送信したデータを使用して実行できるカスタムタスクを示す 例えば、メール送信やデータの格納などのタスクを実行することができます。

## 送信アクションのワークフロー {#workflow-for-a-submit-action}

このフローチャートは、アダプティブフォームで「**[!UICONTROL 送信]**」ボタンをクリックしたときにトリガーされる送信アクションのワークフローを表しています。添付ファイルコンポーネント内のファイルがサーバーにアップロードされ、フォームデータはアップロードされたファイルの URL を使用して更新されます。クライアント内では、データは JSON 形式で保存されます。クライアントは内部サーブレットに Ajax リクエストを送信し、サーブレットは指定したデータを処理して XML 形式で返します。クライアントは、このデータをアクションフィールドと照合します。そして、Form Submit アクションを通して、データを最終サーブレット（Guide Submit サーブレット）に送信します。次に、サーブレットが送信アクションにコントロールを転送します。送信アクションは、異なるスリングリソースにリクエストを転送するか、ブラウザーを別の URL にリダイレクトさせることができます。

![送信アクションのワークフローを示したフローチャート](assets/diagram1.png)

### XML データ形式 {#xml-data-format}

XML データは、**`jcr:data`** リクエストパラメーターを使ってサーブレットへと送信されます。送信アクションは、パラメーターにアクセスしてデータを処理できます。次のコードは、XML データの形式を説明しています。フォームモデルにバインドされているフィールドは、**`afBoundData`** セクションに表示されます。バインドされていないフィールドは、`afUnoundData` セクションに表示されます。`data.xml` ファイルの形式について詳しくは、[アダプティブフォームフィールドの自動埋め込みの概要](../../forms/using/prepopulate-adaptive-form-fields.md)を参照してください。

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### アクションフィールド {#action-fields}

送信アクションは、HTML の [input](https://developer.mozilla.org/ja-jp/docs/Web/HTML/Element/Input) タグを使って、レンダリングされたフォームの HTML に非表示の入力フィールドを追加することができます。これらの非表示のフィールドには、フォーム送信の処理中に必要な値を含めることができます。フォーム送信時に、これらのフィールド値は、送信アクションが送信処理中に使用することのできるリクエストパラメーターとしてポストバックされます。この入力フィールドは、アクションフィールドと呼ばれます。

例えば、フォームの記入にかかった時間も取得する送信アクションであれば、`startTime` および `endTime` のフィールドを非表示で追加することができます。

スクリプトを使って、フォームがレンダリングされた時間ならびにフォーム送信前の時間を、それぞれ `startTime` および `endTime` フィールドの値として指定することができます。その後、送信 ActionScript `post.jsp` が、リクエストパラメーターを使用してこれらのフィールドにアクセスし、フォームの記入にかかった合計時間を計算することができます。

### 添付ファイル {#file-attachments}

送信アクションは、ファイル添付コンポーネントを使ってアップロードされた添付ファイルを使用することもできます。送信アクションスクリプトは、スリング [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html) を使ってこれらのファイルにアクセスすることができます。API の [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) メソッドは、リクエストパラメーターがファイルであるかフォームフィールドであるかを特定するのに役立ちます。送信アクション内のリクエストパラメーターを反復することで、File Attachment パラメーターを特定することができます。

次のサンプルコードは、まず、リクエスト内の添付ファイルを特定します。続いて、このコードは、[Get API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()) を使ってファイルにデータを読み込みます。最後に、データを使用してドキュメントオブジェクトを作成し、それをリストに追加します。

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### 転送パスおよびリダイレクト URL {#forward-path-and-redirect-url}

要求されたアクションを実行した後、送信サーブレットは、リクエストを転送パスに転送します。アクションが、setForwardPath API を使って Guide Submit サーブレットに転送パスを作成します。

アクションによって転送パスが指定されない場合、送信サーブレットは、リダイレクト URL を使ってブラウザーをリダイレクトします。作成者は、アダプティブフォーム編集ダイアログの「ありがとうございます」ページ設定を使って、リダイレクト URL を設定します。リダイレクト URL は、送信アクションまたは Guide Submit 内の setRedirectUrl API を通して設定することもできます。また、Guide Submit サーブレット内の setRedirectParameters API を使って、リダイレクト URL に送られるリクエストパラメーターを設定することもできます。

>[!NOTE]
>
>リダイレクト URL は、「ありがとうございます」ページ設定を使って作成者が指定します。[標準の送信アクション](../../forms/using/configuring-submit-actions.md) リダイレクト URL を使用して、転送パスが参照するリソースからブラウザーをリダイレクトします。
>
>リクエストをリソースまたはサーブレットに転送するカスタム送信アクションを作成することができます。転送パスのリソース処理を実行するスクリプトによっておこなわれるリダイレクト URL へのリクエストのリダイレクトは、処理が完了したときにおこなわれるように設定することをお勧めします。

## 送信アクション {#submit-action}

送信アクションは、次のファイルを含む sling:Folder です。

* **addfields.jsp**：このスクリプトは、レンディション中に HTML ファイルに追加されるアクションフィールドを指定します。post.POST.jsp スクリプトでの送信中に必要な非表示の入力パラメーターの追加には、このスクリプトを使用します。
* **dialog.xml**：このスクリプトは、CQ コンポーネントダイアログに似ています。作成者がカスタマイズする設定情報を提供します。フィールドは、送信アクションを選択するときに、アダプティブフォーム編集ダイアログの送信アクションタブに表示されます。
* **post.POST.jsp**：送信サーブレットは、送信されたデータおよび前のセクションからの追加データで、このスクリプトを呼び出します。このページで言及されるアクションの実行は、post.POST.jsp スクリプトの実行を意味します。送信アクションをアダプティブフォームに登録して、アダプティブフォーム編集ダイアログに表示するには、以下のプロパティを `sling:Folder`:

   * 文字列型で値が **fd/af/components/guidesubmittype** の **guideComponentType**
   * 送信アクションが適用されるアダプティブフォームのタイプを指定する文字列型の **guideDataModel****xfa** は、XFA ベースのアダプティブフォームでサポートされており、また **xsd** は、XSD ベースのアダプティブフォームでサポートされています。**basic** は、XDP や XSD を使用しないアダプティブフォームでサポートされています。複数のタイプのアダプティブフォームでのアクションを表示するには、対応する文字列を追加します。各文字列はカンマで区切ります。例えば、XFA および XSD ベースのアダプティブフォームでアクションを表示したい場合、**xfa** および **xsd** を値にそれぞれ指定します。

   * 文字列型の **jcr:description**。このプロパティの値は、アダプティブフォーム編集ダイアログボックスの「送信アクション」タブにある「送信アクション」リストに表示されます。 CRX リポジトリ内の場所に、標準のアクションが存在します。 **/libs/fd/af/components/guidesubmittype**.

## カスタム送信アクションの作成 {#creating-a-custom-submit-action}

次の手順を実行し、CRX リポジトリにデータを保存した後、メール送信をおこなうカスタム送信アクションを作成します。アダプティブフォームには、CRX リポジトリにデータを保存する、標準の送信アクション Store Content（非推奨）が含まれています。 さらに、CQ には、メール送信に使用される [Mail](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja) API が含まれています。Mail API を使用する前に、システムコンソールを通して Day CQ Mail サービスを[設定](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja&amp;wcmmode=disabled)します。リポジトリーにデータを保存するには、コンテンツを格納アクション（非推奨）を再利用できます。コンテンツを格納アクション（非推奨）は、CRX リポジトリーの /libs/fd/af/components/guidesubmittype/store にあります。

1. URL https://&lt;server>:&lt;port>/crx/de/index.jspから、CRXDE Lite にログインします。/apps/custom_submit_action フォルダー内に sling:Folder プロパティを持つノードを作成し、名前を store_and_mail に設定します。custom_submit_action フォルダーが存在しない場合は作成します。

   ![sling:Folder プロパティを持つノードの作成を示したスクリーンショット](assets/step1.png)

1. **必須の設定フィールドを指定します。**

   格納アクションに必要な設定を追加します。/libs/fd/af/components/guidesubmittype/store から、格納アクションの **cq:dialog** ノードを、/apps/custom_submit_action/store_and_email のアクションフォルダーにコピーします。

   ![アクションフォルダーへのダイアログノードのコピーを示したスクリーンショット](assets/step2.png)

1. **作成者にメール設定を促す設定フィールドを指定します。**

   アダプティブフォームには、ユーザーにメールを送信するメール送信アクションもあります。要件に応じて、このアクションをカスタマイズします。/libs/fd/af/components/guidesubmittype/email/dialog に移動します。cq:dialog ノード内のノードを、送信アクションの cq:dialog ノード（/apps/custom_submit_action/store_and_email/dialog）にコピーします。

   ![メール送信アクションのカスタマイズ](assets/step3.png)

1. **アクションをアダプティブフォーム編集ダイアログで使用できるようにします。**

   次のプロパティを store_and_email ノードに追加します。

   * **文字列**&#x200B;型の **guideComponentType** および値 **fd/af/components/guidesubmittype**

   * **文字列**&#x200B;型の **guideDataModel** と値 **xfa、xsd、basic**

   * **文字列**&#x200B;型の **jcr:description** と値 **Store and Email Action**

1. 任意のアダプティブフォームを開きます。「**開始**」の横にある「**編集**」ボタンをクリックし、アダプティブフォームコンテナの&#x200B;**編集**&#x200B;ダイアログを開きます。新しいアクションが、「**送信アクション**」タブに表示されます。**格納およびメール送信アクション**&#x200B;を選択すると、ダイアログノードに追加された設定が表示されます。

   ![送信アクション設定ダイアログ](assets/store_and_email_submit_action_dialog.jpg)

1. **アクションを使用してタスクを完了します。**

   post.POST.jsp スクリプトをアクションに追加します（/apps/custom_submit_action/store_and_mail/）。

   そのまま使用できるストアアクション (post.POST.jsp スクリプト ) を実行します。 CQ がコード内で提供する [FormsHelper.runAction](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)（java.lang.String、java.lang.String、org.apache.sling.api.resource.Resource、org.apache.sling.api.SlingHttpServletRequest、org.apache.sling.api.SlingHttpServletResponse）API を、格納アクション内で実行します。次のコードを JSP ファイルに追加します。

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   メールを送信するために、コードが受信者のメールアドレスを設定から読み取ります。アクションのスクリプトに設定値を取り込むには、次のコードを使用して現在のリソースのプロパティを読み込みます。同様に、他の設定ファイルも読み取ることができます。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最後に、CQ Mail API を使用してメールを送信します。[SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) クラスを使って、次に示すとおりに Email Object を作成します。

   >[!NOTE]
   >
   >JSP ファイルの名前が post.POST.jsp になっていることを確認してください。

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   アダプティブフォームでアクションを選択します。アクションによりメールが送信され、データが保存されます。
