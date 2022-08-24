---
title: トラブルシューティング
seo-title: Troubleshooting
description: 既知の問題を含むコミュニティのトラブルシューティング
seo-description: Troubleshooting Community including Known Issues
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 82%

---

# トラブルシューティング {#troubleshooting}

ここでは、一般的な問題および既知の問題について説明します。

## 既知の問題 {#known-issues}

### ディスパッチャーの再取得でエラーが発生する {#dispatcher-refetch-fails}

ディスパッチャー 4.1.5 を新しいバージョンの Jetty と共に使用する場合、再取得によって、要求がタイムアウトするまで待機した後、「リモートサーバーから応答を受信できません」というエラーが発生することがあります。

ディスパッチャー 4.1.6 以降を使用すると、この問題は解決します。

### CQ 5.4 からのアップグレード後にフォーラム投稿にアクセスできない {#cannot-access-forum-post-after-upgrading-from-cq}

CQ 5.4 でフォーラムが作成され、トピックが投稿された後、サイトが AEM 5.6.1 以降にアップグレードされた場合、既存の投稿を表示しようとすると、ページに次のエラーが表示されることがあります。

無効なパターン文字「a」は次に対する要求を処理できません： `/content/demoforums/forum-test.html` このサーバーとログには次の情報が含まれます。

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

この問題は、com.day.cq.commons.date.RelativeTimeFormat の形式文字列が 5.4 と 5.5 の間に変更され、「ago」を表す「a」が許可されなくなったというものです。

したがって、RelativeTimeFormat() API を使用するコードは、以下を変更する必要があります。

* 送信元: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* To: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

障害は、オーサー環境とパブリッシュ環境で異なります。オーサー環境では、エラーは表示されず、フォーラムトピックが表示されないだけです。パブリッシュ環境では、ページにエラーが表示されます。

詳しくは、[com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API を参照してください。

## 一般的な問題 {#common-concerns}

### ログ内の警告：Handlebars の廃止 {#warning-in-logs-handlebars-deprecated}

起動時（初回ではなく、2 回目以降のすべての起動時）に、次の警告がログに表示されることがあります。

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` は、 `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

この警告は、 `jknack.handlebars.Handlebars`、使用元 [SCF](scf.md#handlebarsjavascripttemplatinglanguage)には、独自の i18n ヘルパーユーティリティが付属しています。 起動時に、AEM 固有の [i18n ヘルパー](handlebars-helpers.md#i-n)に置き換えられます。この警告は、既存のヘルパーのオーバーライドを確認するためにサードパーティのライブラリによって生成されます。

### ログ内の警告：OakResourceListener の processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

ソーシャルコミュニティの多数のフォーラムトピックを投稿すると、OakResourceListener の processOsgiEventQueue から大量の警告および情報ログが生成されることがあります。

これらの警告は無視しても問題ありません。

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### ログ内のエラー：IndexElementFactory の NoClassDefFoundError {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

AEM 5.6.1 GA を最新の cq-socialcommunities-pkg-1.4.x または AEM 6.0 にアップグレードすると、ある状態での起動時にログファイルにエラーが記録されますが、再起動時にエラーは表示されず、自動的に解決されます。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
