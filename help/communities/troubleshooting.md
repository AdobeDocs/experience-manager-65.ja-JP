---
title: コミュニティのトラブルシューティング
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
source-wordcount: '370'
ht-degree: 0%

---

# コミュニティのトラブルシューティング {#troubleshooting}

このセクションには、コミュニティのトラブルシューティング時の一般的な懸念事項と既知の問題が含まれています。

## 既知の問題 {#known-issues}

### Dispatcherの再取得に失敗する {#dispatcher-refetch-fails}

新しいバージョンのJettyでDispatcher 4.1.5を使用している場合、リフェッチの結果、リクエストのタイムアウトを待った後に「リモートサーバーからレスポンスを受け取ることができません」になることがあります。

Dispatcher 4.1.6以降を使用すると、この問題を解決できます。

### CQ 5.4からのアップグレード後にフォーラム投稿にアクセスできない {#cannot-access-forum-post-after-upgrading-from-cq}

CQ 5.4でフォーラムが作成され、トピックが投稿された後、サイトがAEM 5.6.1以降にアップグレードされた場合、既存の投稿を表示しようとすると、ページでエラーが発生する可能性があります。

不正なパターン文字「a」
このサーバー上の`/content/demoforums/forum-test.html`にリクエストを送信できません。ログには次のものが含まれています。

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

問題は、「ago」の「a」が受け入れられなくなるように、com.day.cq.commons.date.RelativeTimeFormatの書式文字列が5.4から5.5の間で変更されたことです。

したがって、RelativeTimeFormat （） APIを使用するすべてのコードは、次のように変更する必要があります。

* 差出人：`final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* 宛先：`final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

失敗は、オーサーとパブリッシュで異なります。 オーサーでは、静かに失敗し、単にフォーラムのトピックを表示しません。 「公開」で、ページ上のエラーがスローされます。

詳しくは、[com.day.cq.commons.date.RelativeTimeFormat](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) APIを参照してください。

## 共通の懸念 {#common-concerns}

### ログ内の警告：Handlebarsは非推奨です {#warning-in-logs-handlebars-deprecated}

起動中（最初ではなく、それ以降のすべての起動中）に、次の警告がログに表示される場合があります。

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'`は`com.adobe.cq.social.handlebars.I18nHelper@15bac645`に置き換えられました

この警告は、[SCF](scf.md#handlebarsjavascripttemplatinglanguage)が独自のi18n ヘルパーユーティリティを備えた`jknack.handlebars.Handlebars`として安全に無視できます。 起動時に、AEM固有の[i18n ヘルパー](handlebars-helpers.md#i-n)に置き換えられます。 この警告は、既存のヘルパーの上書きを確認するために、サードパーティライブラリによって生成されます。

### ログの警告：OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

複数のソーシャルコミュニティフォーラムのトピックを投稿すると、OakResourceListener processOsgiEventQueueから膨大な警告ログと情報ログが生成される場合があります。

これらの警告は安全に無視できます。

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### ログのエラー：IndexElementFactoryのNoClassDefFoundError {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

AEM 5.6.1を最新のcq-socialcommunities-pkg-1.4.xまたはAEM 6.0にアップグレードすると、ログファイルにエラーが発生します。 これは、起動時にエラーが表示されないことが示すように、自分自身を解決する条件の起動中に発生します。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
