---
title: アダプティブフォーム向けのカスタム送信アクションの作成
seo-title: アダプティブフォーム向けのカスタム送信アクションの作成
description: AEM Forms では、アダプティブフォーム向けのカスタム送信アクションを作成することができます。本記事では、アダプティブフォームにカスタム送信アクションを追加する方法を説明します。
seo-description: AEM Forms では、アダプティブフォーム向けのカスタム送信アクションを作成することができます。本記事では、アダプティブフォームにカスタム送信アクションを追加する方法を説明します。
uuid: fd8e1dac-b997-4e86-aaf6-3507edcb3070
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 2a2e1156-4a54-4b0a-981c-d527fe22a27e
docset: aem65
translation-type: tm+mt
source-git-commit: a399b2cb2e0ae4f045f7e0fddf378fdcd80bb848
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 51%

---


# アダプティブフォーム向けのカスタム送信アクションの作成{#writing-custom-submit-action-for-adaptive-forms}

アダプティブフォームでは、ユーザー指定のデータを処理するために送信アクションが必要です。 送信アクションは、アダプティブフォームを使用して送信するデータに対して実行されるタスクを決定します。 Adobe Experience Manager(AEM)には、ユーザーが送信したデータを使用して実行できるカスタムタスクを示す[OOTB送信アクション](../../forms/using/configuring-submit-actions.md)が含まれています。 例えば、電子メールの送信やデータの保存などのタスクを実行できます。

## 送信アクションのワークフロー {#workflow-for-a-submit-action}

このフローチャートは、アダプティブフォームで「**[!UICONTROL 送信]**」ボタンをクリックしたときにトリガーされる送信アクションのワークフローを示しています。 File Attachment コンポーネントのファイルはサーバーにアップロードされ、フォームデータはアップロードされたファイルの URL で更新されます。クライアント内で、データは JSON 形式で格納されます。クライアントは、指定したデータをメッセージして XML 形式で返信する内部サーブレットに Ajax リクエストを送信します。クライアントは、このデータをアクションフィールドと照合します。データは、Form Submitアクションを通じて、最終サーブレット（Guide Submitサーブレット）に送信されます。 次に、サーブレットが送信アクションにコントロールを転送します。送信アクションは、リクエストを別のスリングリソースに転送したり、ブラウザーを別のURLにリダイレクトしたりできます。

![送信アクションのワークフローを示したフローチャート](assets/diagram1.png)

### XML データ形式 {#xml-data-format}

XMLデータは、**`jcr:data`**&#x200B;リクエストパラメーターを使用してサーブレットに送信されます。 送信アクションは、データを処理するためにパラメーターにアクセスすることができます。次のコードは、XML データの形式を説明しています。フォームモデルに連結されているフィールドは、**`afBoundData`**&#x200B;セクションに表示されます。 バインドされていないフィールドは、`afUnoundData` セクションに表示されます。`data.xml`ファイルの形式について詳しくは、「[アダプティブフォームフィールドの自動埋め込みの概要](../../forms/using/prepopulate-adaptive-form-fields.md)」を参照してください。

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

送信アクションは、HTMLの[input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input)タグを使用して、レンダリングされたフォームHTMLに非表示の入力フィールドを追加できます。 これらの非表示フィールドには、フォーム送信の処理中に必要な値を含めることができます。 フォームの送信時に、これらのフィールド値は、送信アクションが送信処理時に使用できるリクエストパラメーターとしてポストバックされます。 この入力フィールドは、アクションフィールドと呼ばれます。

例えば、フォームの記入にかかる時間も取得する送信アクションでは、非表示の入力フィールド`startTime`と`endTime`を追加できます。

スクリプトを使って、フォームがレンダリングされた時間ならびにフォーム送信前の時間を、それぞれ `startTime` および `endTime` フィールドの値として指定することができます。その後、送信アクションのスクリプト `post.jsp` が、リクエストパラメーターを使ってこれらのフィールドにアクセスし、フォームの記入にかかった合計時間を計算することができます。

### 添付ファイル {#file-attachments}

送信アクションは、File Attachmentコンポーネントを使用してアップロードする添付ファイルを使用することもできます。 送信アクションスクリプトは、スリング [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html) を使ってこれらのファイルにアクセスすることができます。APIの[isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField())メソッドは、リクエストパラメーターがファイルかフォームフィールドかを識別するのに役立ちます。 送信アクション内のリクエストパラメーターを反復することで、File Attachment パラメーターを特定することができます。

次のサンプルコードは、まず、リクエスト内の添付ファイルを特定します。次に、[Get API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get())を使用してファイルにデータを読み込みます。 最後に、データを使用してドキュメントオブジェクトを作成し、リストに追加します。

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

要求されたアクションを実行した後、送信サーバーレットは、リクエストを転送パスに転送します。アクションは、setForwardPath APIを使用して、Guide Submitサーブレットに転送パスを設定します。

アクションによって転送パスが指定されない場合、送信サーバーレットは、リダイレクト URL を使ってブラウザをリダイレクトします。作成者は、アダプティブフォーム編集ダイアログのありがとうございますページ設定を使って、リダイレクト URL を設定します。リダイレクトURLは、送信アクションまたはGuide Submit内のsetRedirectUrl APIを使用して設定することもできます。 また、Guide Submit 内の setRedirectUrl API を使って、リダイレクト URL に送られるリクエストパラメーターを設定することもできます。

>[!NOTE]
>
>リダイレクト URL は、ありがとうございますページ設定を使って作成者が指定します[OOTB Submit ](../../forms/using/configuring-submit-actions.md) Actionは、リダイレクトURLを使用して、転送パスが参照するリソースからブラウザをリダイレクトします。
>
>リクエストをリソースまたはサーブレットに転送するカスタム送信アクションを作成できます。 Adobeでは、転送パスのリソース処理を実行するスクリプトが、処理が完了したときにリダイレクトURLにリクエストをリダイレクトすることを推奨します。

## 送信アクション {#submit-action}

送信アクションは、次を含むsling:Folderです。

* **addfields.jsp**:このスクリプトは、レンダリング中に HTML ファイルに追加されるアクションフィールドを指定します。post.POST.jsp スクリプトでの送信中に必要な非表示の入力パラメーターの追加には、このスクリプトを使用します。
* **dialog.xml**：このスクリプトは、CQ Component ダイアログに似ています。作成者がカスタマイズする設定情報を提供します。 これらのフィールドは、送信アクションを選択した場合に、アダプティブフォーム編集ダイアログの送信アクションタブに表示されます。
* **post.POST.jsp**:送信サーブレットは、送信したデータと前の節の追加データを使用して、このスクリプトを呼び出します。このページで言及されるアクションの実行は、post.POST.jsp スクリプトの実行を意味します。送信アクションをアダプティブフォームに登録し、アダプティブフォーム編集ダイアログに表示するには、次のプロパティをsling:Folderに追加します。

   * ストリング型の **guideComponentType** および値 **fd/af/components/guidesubmittype**
   * **送信アクションが適用されるアダプティブフォームのタイプを指定する文字列型の** guideDataModel。**XFAベースのアダプティブフォームでは** xfaがサポートされ、XSDベースのアダプティブフォームでは **** xsdがサポートされています。**基本** 的には、XDPまたはXSDを使用しないアダプティブフォームがサポートされます。複数のタイプのアダプティブフォームでのアクションを表示するには、対応する文字列を追加します。各文字列はコンマで区切ります。 例えば、XFAベースのアダプティブフォームとXSDベースのアダプティブフォームでアクションを表示するには、**xfa**&#x200B;および&#x200B;**xsd**&#x200B;の値をそれぞれ指定します。

   * **文字列型のjcr:** description。このプロパティの値は、アダプティブフォーム編集ダイアログの送信アクションタブにある送信アクションリストに表示されます。 OOTBアクションは、**/libs/fd/af/components/guidesubmittype**&#x200B;にあるCRXリポジトリに存在します。

## カスタム送信アクションの作成 {#creating-a-custom-submit-action}

次の手順を実行し、CRX リポジトリにデータを保存した後、メール送信を行うカスタム送信アクションを作成します。アダプティブフォームには、CRXリポジトリにデータを保存するOOTB送信アクションStore Content（非推奨）が含まれています。 また、CQには、電子メールの送信に使用できる[Mail](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/mailer/package-summary.html) APIも用意されています。 Mail APIを使用する前に、システムコンソールからDay CQ Mailサービスを[設定](https://docs.adobe.com/docs/en/cq/current/administering/notification.html?wcmmode=disabled#Configuring the Mail Service)します。 Store Content（非推奨）アクションを再利用して、リポジトリにデータを保存できます。 Store Content（廃止）アクションは、CRX リポジトリの /libs/fd/af/components/guidesubmittype/store にあります。

1. URL https://&lt;server>:&lt;port>/crx/de/index.jspでCRXDE Liteにログインします。 /apps/custom_submit_action フォルダー内に sling:Folder プロを持つノードを作成し、名前を store_and_mail に設定します。custom_submit_action フォルダーがすでに存在しない場合は作成します。

   ![sling:Folder をプロパティとするノードの作成を示したスクリーンショット](assets/step1.png)

1. **必須の設定フィールドを指定します。**

   Store追加アクションに必要な設定。 /libs/fd/af/components/guidesubmittype/store から、Store アクションの **cq:dialog** ノードを、/apps/custom_submit_action/store_and_email のアクションフォルダーにコピーします。

   ![アクションフォルダーへのダイアログノードのコピーを示したスクリーンショット](assets/step2.png)

1. **作成者に電子メール設定を促す設定フィールドを指定します。**

   アダプティブフォームには、ユーザーに電子メールを送信する Email アクションもあります。要件に応じて、このアクションをカスタマイズします。/libs/fd/af/components/guidesubmittype/email/dialog に移動します。cq:dialogノード内のノードを、送信アクションのcq:dialogノード(/apps/custom_submit_action/store_and_email/dialog)にコピーします。

   ![メール送信アクションのカスタマイズ](assets/step3.png)

1. **アクションを Adaptive Form Edit ダイアログで使用できるようにします。**

   次のプロパティを store_and_email ノードに追加します。

   * ストリング型の **guideComponentType****** および値 **fd/af/components/guidesubmittype**

   * **タイプ** が **** Stringで値がxfa、xsd、basicの **guideDataModel**

   * **ストリング**&#x200B;型の&#x200B;**jcr:description**&#x200B;および値 **Store and Email Action**

1. 任意のアダプティブフォームを開きます&#x200B;**Start** の隣にある「**Edit**」ボタンをクリックし、アダプティブフォームコンテナの **Edit** ダイアログを開きます。新しいアクションが、**Submit Actions** タブに表示されます。「**Store and Email Action**」を選択すると、ダイアログノードに追加された設定が表示されます。

   ![送信アクション設定ダイアログ](assets/store_and_email_submit_action_dialog.jpg)

1. **アクションを使用してタスクを完了します。**

   post.POST.jsp スクリプトをアクションに追加します。(/apps/custom_submit_action/store_and_mail/)。

   OOTB の Store アクション（post.POST.jsp スクリプト）を実行します。CQの[FormsHelper.runAction](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.slingHttpServletResponse) APIを使用します。をコードに入力して、Storeアクションを実行します。 次のコードを JSP ファイルに追加します。

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   電子メールを送信するために、コードは受信者の電子メールアドレスを設定から読み取ります。 アクションのスクリプトに設定値を取り込むには、次のコードを使って現在のリソースのプロパティを読み込みます。同じく、その他の設定ファイルを読み込むこともできます。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最後に、CQ Mail API を使用してメールを送信します。[SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html)クラスを使用して、次に示すようにEmail Objectを作成します。

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

   アダプティブフォームでアクションを選択します。アクションがメールを送信し、データを保存します。

