---
title: メッセージングの基本事項
description: の操作と、メッセージコンポーネントを使用して web サイトにメッセージ機能を含める方法の詳細について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: b941b5e0-f768-4393-9a9d-ded2cd7d10c4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 5%

---

# メッセージングの基本事項 {#messaging-essentials}

このページでは、メッセージコンポーネントを使用してを Web サイトのメッセージング機能に含める方法の詳細について説明します。

## クライアントサイドの基本事項 {#essentials-for-client-side}

**メッセージを作成**

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>ソーシャル/メッセージング/コンポーネント/hbs/composemessage</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientlibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/composemessage.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/composemessage/clientlibs/composemessage.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><a href="/help/communities/configure-messaging.md" target="_blank"> メッセージングの設定 </a> を参照してください。</td>
  </tr>
  <tr>
   <td><strong>管理設定</strong></td>
   <td><a href="/help/communities/messaging.md">メッセージングの設定</a></td>
  </tr>
 </tbody>
</table>

**メッセージリスト**

（インボックス、送信済み、ごみ箱の場合）

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td><p>ソーシャル/メッセージング/コンポーネント/hbs/messagebox</p> </td>
  </tr>
  <tr>
   <td> <a href="/help/communities/client-customize.md#clientlibs-for-scf" target="_blank"><strong>clientlibs</strong></a></td>
   <td><p>cq.social.hbs.messaging</p> </td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/messagebox.hbs</td>
  </tr>
  <tr>
   <td><strong>css</strong></td>
   <td>/libs/social/messaging/components/hbs/messagebox/clientlibs/messagebox.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><a href="/help/communities/configure-messaging.md" target="_blank"> メッセージングの設定 </a> を参照してください。</td>
  </tr>
  <tr>
   <td><strong>管理設定</strong></td>
   <td><a href="/help/communities/messaging.md" target="_blank">メッセージングの設定</a></td>
  </tr>
 </tbody>
</table>

[&#x200B; クライアントサイドのカスタマイズ &#x200B;](/help/communities/client-customize.md) も参照してください。

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [メッセージングの設定](/help/communities/configure-messaging.md)
* SCF コンポーネント用 [&#x200B; メッセージングクライアント API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/client/api/package-summary.html)
* サービスの [&#x200B; メッセージング API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/api/package-summary.html)
* [&#x200B; メッセージエンドポイント &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/messaging/client/endpoints/package-summary.html)
* [サーバーサイドのカスタマイズ](/help/communities/server-customize.md)

>[!CAUTION]
>
>次の MessageBuilder メソッドでは、文字列パラメーターに末尾のスラッシュ「/」を含める *しないでください*。
>
>* `setInboxPath` （）
>* `setSentItemsPath` （）
>
>次に例を示します。
>
>```
>valid: mb.setInboxPath( "/mail/inbox" );
> not valid: mb.setInboxPath( "/mail/inbox/" );
>```

### コミュニティサイト {#community-site}

ウィザードを使用して作成されたコミュニティサイト構造には、選択した際にメッセージ機能が含まれます。 [&#x200B; コミュニティサイトコンソール &#x200B;](/help/communities/sites-console.md#user-management) の `User Management` 設定を参照してください。

### サンプルコード：メッセージ受信通知 {#sample-code-message-received-notification}

ソーシャルメッセージング機能は、操作（`send`、`marking read`、`marking delete` など）のイベントをスローします。 これらのイベントは、イベントに含まれるデータに対してキャッチおよび実行できます。

次の例は、`message sent` イベントをリッスンし、`Day CQ Mail Service` を使用してすべてのメッセージ受信者にメールを送信するイベントハンドラーです。

サーバーサイドのサンプルスクリプトを試すには、開発環境と、OSGi バンドルを構築する機能が必要です。

1. ` [CRXDE|Lite](https://localhost:4502/crx/de)` に管理者としてログインします。
1. 次のような任意の名前を持つ `bundle node`in `/apps/engage/install` を作成します。

   * 記号名：`com.engage.media.social.messaging.MessagingNotification`
   * 名前：はじめにチュートリアルメッセージ通知
   * 説明：メッセージを受信したユーザーにメール通知を送信するサンプルサービス
   * パッケージ：`com.engage.media.social.messaging.notification`

1. `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/src/main/java/com/engage/media/social/messaging/notification` に移動し、次の操作を行います。

   1. 自動作成された `Activator.java` クラスを削除します。
   1. クラス `MessageEventHandler.java` を作成します。
   1. 以下のコードをコピーして `MessageEventHandler.java` に貼り付けます。

1. 「**すべて保存**」をクリックします。
1. `/apps/engage/install/com.engage.media.social.messaging.MessagingNotification/com.engage.media.social.messaging.MessagingNotification.bnd` に移動し、`MessageEventHandler.java` コードで記述されているすべてのインポート文を追加します。
1. バンドルをビルドします。
1. `Day CQ Mail Service`OSGi サービスが設定されていることを確認します。
1. デモユーザーとしてログインし、別のユーザーにメールを送信します。
1. 受信者は、新しいメッセージに関するメールを受け取ります。

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
