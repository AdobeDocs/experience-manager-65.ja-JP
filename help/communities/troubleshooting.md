---
title: トラブルシューティング コミュニティ
description: 既知の問題や懸念事項など、コミュニティのトラブルシューティングについて説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# トラブルシューティング コミュニティ {#troubleshooting}

この節では、コミュニティのトラブルシューティングに関する一般的な懸念と既知の問題について説明します。

## 既知の問題 {#known-issues}

### Dispatcherの再取得に失敗しました {#dispatcher-refetch-fails}

Dispatcher 4.1.5 を新しいバージョンの Jetty で使用している場合、再取得すると、リクエストがタイムアウトするのを待った後、「リモートサーバーから応答を受信できません」という結果になる場合があります。

Dispatcher 4.1.6 以降を使用すると、この問題が解決されます。

### CQ 5.4 からアップグレード後にフォーラムPostにアクセスできない {#cannot-access-forum-post-after-upgrading-from-cq}

フォーラムが CQ 5.4 で作成され、トピックが投稿された後、サイトがAEM 5.6.1 以降にアップグレードされた場合、既存の投稿を表示しようとすると、ページに次のエラーが発生する可能性があります。

パターン文字「a」が無効です
このサーバーの `/content/demoforums/forum-test.html` に対する要求を提供できません。ログには次の内容が含まれています：

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

問題は、com.day.cq.commons.date.RelativeTimeFormat の書式文字列が 5.4 と 5.5 の間で変更され、「ago」の「a」が受け入れられなくなったことです。

したがって、RelativeTimeFormat （） API を使用するコードは、次のように変更する必要があります。

* 追加元：`final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 宛先：`final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

エラーは、オーサーとPublishで異なります。 オーサー環境では、通知なしに失敗し、フォーラムのトピックは表示されません。 Publishでは、ページでエラーがスローされます。

詳しくは、[com.day.cq.commons.date.RelativeTimeFormat](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API を参照してください。

## よくある懸念 {#common-concerns}

### ログの警告：Handlebars を廃止 {#warning-in-logs-handlebars-deprecated}

起動中（最初の起動以外はその後すべて）に、次の警告がログに表示される場合があります。

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` は `com.adobe.cq.social.handlebars.I18nHelper@15bac645` に置き換えられました

[SCF](scf.md#handlebarsjavascripttemplatinglanguage) で使用される `jknack.handlebars.Handlebars` は、独自の i18n ヘルパーユーティリティが付属しているため、この警告は無視しても問題ありません。 起動時には、AEM固有の [i18n ヘルパー ](handlebars-helpers.md#i-n) に置き換えられます。 この警告は、既存のヘルパーの上書きを確認するために、サードパーティライブラリによって生成されます。

### ログの警告：OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

いくつかのソーシャルコミュニティフォーラムのトピックを投稿すると、OakResourceListener processOsgiEventQueue から大量の警告ログと情報ログが出力される場合があります。

これらの警告は無視しても問題ありません。

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### ログのエラー：IndexElementFactory の NoClassDefFoundError {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

AEM 5.6.1 を最新の cq-socialcommunities-pkg-1.4.x またはAEM 6.0 にアップグレードすると、ログファイルにエラーが表示されます。 これは、再起動時にエラーが表示されないことによって示されるように、それ自体が解決される条件の起動時に発生します。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
