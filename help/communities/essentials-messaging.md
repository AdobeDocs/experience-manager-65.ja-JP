---
title: メッセージングの基本事項
seo-title: メッセージングの基本事項
description: メッセージングコンポーネントの概要
seo-description: メッセージングコンポーネントの概要
uuid: e0dad45e-d84d-4b28-b357-aded1c5d2605
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 98f70093-e786-4555-8aaa-d0df4c977dc0
docset: aem65
exl-id: b941b5e0-f768-4393-9a9d-ded2cd7d10c4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 34%

---

# メッセージングの基本事項 {#messaging-essentials}

このページでは、メッセージングコンポーネントを使用してメッセージング機能を Web サイトに組み込む方法の詳細をまとめています。

## クライアント側の基本事項  {#essentials-for-client-side}

**メッセージを作成**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/composemessage</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><a href="/help/communities/configure-messaging.md" target="_blank">メッセージングの設定</a>を参照してください。</td>
  </tr>
  <tr>
   <td><strong>管理設定</strong></td>
   <td><a href="/help/communities/messaging.md">メッセージの設定</a></td>
  </tr>
 </tbody>
</table>

**メッセージリスト**

（インボックス、送信済み、ごみ箱）

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>social/messaging/components/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientllibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><a href="/help/communities/configure-messaging.md" target="_blank">メッセージングの設定</a>を参照してください。</td>
  </tr>
  <tr>
   <td><strong>管理設定</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">メッセージの設定</a></td>
  </tr>
 </tbody>
</table>

[クライアント側のカスタマイズ](/help/communities/client-customize.md)も参照してください。

## サーバー側の基本事項  {#essentials-for-server-side}

* [メッセージングの設定](/help/communities/configure-messaging.md)
* [SCFコンポーネントの](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html) メッセージングクライアントAPI
* [メッセージング API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/api/package-summary.html)（サービス用）
* [メッセージングエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [サーバー側のカスタマイズ](/help/communities/server-customize.md)

>[!CAUTION]
>
>次のMessageBuilderメソッドの文字列パラメーターは、**&#x200B;ではなく、末尾にスラッシュ「/」を含める必要があります。
>
>* `setInboxPath`()
>* `setSentItemsPath`()

>
>
以下に例を示します。
>
>
```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### コミュニティサイト {#community-site}

ウィザードを使用して作成されたコミュニティサイト構造には、選択時にメッセージング機能が含まれます。 [コミュニティサイトコンソール](/help/communities/sites-console.md#user-management)の`User Management`設定を参照してください。

### サンプルコード：メッセージ受信通知 {#sample-code-message-received-notification}

ソーシャルメッセージ機能では、操作に関するイベント（例：`send`、`marking read`、`marking delete`）がスローされます。 これらのイベントは、イベントに含まれるデータに対して実行されるアクションをキャッチできます。

次の例は、`message sent`イベントをリッスンし、`Day CQ Mail Service`を使用してすべてのメッセージ受信者に電子メールを送信するイベントハンドラーです。

サーバー側のサンプルスクリプトを試すには、開発環境とOSGiバンドルを構築する機能が必要です。

1. ` [CRXDE|Lite](https://localhost:4502/crx/de)`に管理者としてログインします。
1. `/apps/engage/install`内に、次のような任意の名前の`bundle node`を作成します。

   * 記号名：`com.engage.media.social.messaging.MessagingNotification`
   * 名前：入門チュートリアルのメッセージ通知
   * 説明：ユーザーがメッセージを受信したときに電子メール通知を送信するサービスの例
   * パッケージ: `com.engage.media.social.messaging.notification`

1. `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification`に移動し、次の操作を行います。

   1. 自動的に作成された`Activator.java`クラスを削除します。
   1. クラス`MessageEventHandler.java`を作成します。
   1. 以下のコードをコピーして`MessageEventHandler.java`に貼り付けます。

1. 「**すべて保存**」をクリックします。
1. `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd`に移動し、`MessageEventHandler.java`コードに記述されているように、すべてのimport文を追加します。
1. バンドルをビルドします。
1. `Day CQ Mail Service`OSGiサービスが設定されていることを確認します。
1. デモユーザーとしてログインし、別のユーザーに電子メールを送信します。
1. 受信者に、新しいメッセージに関するEメールが届きます。

#### MessageEventHandler.java {#messageeventhandler-java}

```java
package com.engage.media.social.messaging.notification;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.api.resource.ResourceResolverFactory;
import org.apache.sling.api.resource.Resource;
import org.apache.commons.mail.Email;
import org.apache.commons.mail.EmailException;
import org.apache.commons.mail.SimpleEmail;
import org.apache.commons.mail.HtmlEmail;
import java.util.List;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import com.adobe.cq.social.messaging.api.Message;
import com.adobe.cq.social.messaging.api.MessagingEvent;
import com.day.cq.mailer.MessageGatewayService;
import com.day.cq.mailer.MessageGateway;

@Component(immediate=true)
@Service(EventHandler.class)
@Properties({
        @Property(name = "event.topics", value = "com/adobe/cq/social/message")
})
public class MessagingEventHandler implements EventHandler {
    private Logger logger = LoggerFactory.getLogger(MessagingEventHandler.class);

    @Reference
    ResourceResolverFactory resourceResolverFactory;

    @Reference
    private MessageGatewayService messageGatewayService;

    ResourceResolver resourceResolver=null;
    MessageGateway messageGateway=null;

    public void sendMail(String from, String to,String subject, String content){
        Email email = new SimpleEmail();
        messageGateway = messageGatewayService.getGateway(SimpleEmail.class);
        try {
         email.addTo(to);
            email.addReplyTo(from);
            email.setFrom(from);
            email.setMsg(content);
            email.setSubject(subject);
         messageGateway.send(email);
        } catch(EmailException ex) {
            logger.error("MessageNotificaiton : Error sending email : "+ex.getMessage());
        }
        logger.info("**** MessageNotification **** Mail sent to " + to);
    }

    public void handleEvent(Event event) {
        //Get Message Path and originator User's ID from event
        String messagePath = (String) event.getProperty("path");
        String senderId = (String) event.getProperty("userId");
        MessagingEvent.MessagingActions action = (MessagingEvent.MessagingActions) event.getProperty("action");
        try{
            if(MessagingEvent.MessagingActions.MessageSent.equals(action)){
                resourceResolver = resourceResolverFactory.getAdministrativeResourceResolver(null);

                //Read message
                Resource resource = resourceResolver.getResource(messagePath);
                Message msg = resource.adaptTo(Message.class);

                //Get list of recipient Ids from message
                //For Getting Started Tutorial, Id is same as email. If that is not the case in your site,
                //an additional step is needed to retrieve the email for the Id
                List<String> reclist = msg.getRecipientIdList();
                for(int i=0;i<reclist.size();i++){
                    //Send Email using Mailing Service
                    sendMail("admin@cqadmin.qqq",reclist.get(i),"New message on Getting Started Tutorial", "Hi\nYou have received a new message from  " +  senderId + ". To read it, sign in to Getting Started Tutorial.\n\n-Engage Admin");
                }
            }
        } catch(Exception ex){
            logger.error("Error getting message info : " + ex.getMessage());
        } finally {
            resourceResolver.close();
        }

    }
}
```
