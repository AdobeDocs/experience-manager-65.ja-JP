---
title: コミュニティのトラブルシューティング
description: 既知の問題を含むコミュニティのトラブルシューティング
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: ef4f4108-c485-4e2e-a58f-ff64eee9937e
source-git-commit: 3d80ea6a6fbad05afcdd1f41f4b9de70921ab765
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 1%

---

# コミュニティのトラブルシューティング {#troubleshooting}

この節では、コミュニティのトラブルシューティングに関する一般的な問題と既知の問題について説明します。

## 既知の問題 {#known-issues}

### Dispatcher の再取得に失敗 {#dispatcher-refetch-fails}

新しいバージョンの Jetty で Dispatcher 4.1.5 を使用する場合、リフェッチを実行すると、リクエストがタイムアウトするのを待った後に「リモートサーバーから応答を受け取れません」となる場合があります。

Dispatcher 4.1.6 以降を使用すると、この問題が解決します。

### CQ 5.4 からのアップグレード後にフォーラム投稿にアクセスできない {#cannot-access-forum-post-after-upgrading-from-cq}

フォーラムが CQ 5.4 で作成され、トピックが投稿された後で、サイトがAEM 5.6.1 以降にアップグレードされた場合、既存の投稿を表示しようとすると、ページで次のエラーが発生する場合があります。

無効なパターン文字「a」は次に対する要求を処理できません： `/content/demoforums/forum-test.html` このサーバーとログには次の情報が含まれます。

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

問題は、com.day.cq.commons.date.RelativeTimeFormat の書式文字列が 5.4 から 5.5 に変更され、「ago」の「a」は受け入れられなくなったことです。

したがって、RelativeTimeFormat() API を使用するコードは、次の値を変更する必要があります。

* 送信元: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* To: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

失敗は、オーサーとパブリッシュで異なります。 オーサー環境では、警告なく失敗し、フォーラムトピックは表示されません。 公開すると、ページ上でエラーがスローされます。

詳しくは、 [com.day.cq.commons.date.RelativeTimeFormat](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) API を参照してください。

## 一般的な懸念事項 {#common-concerns}

### ログ内の警告：Handlebars は非推奨 {#warning-in-logs-handlebars-deprecated}

起動時（最初ではなく、その後のすべて）に、次の警告がログに表示される場合があります。

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` は、 `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

この警告は、 `jknack.handlebars.Handlebars`、使用元 [SCF](scf.md#handlebarsjavascripttemplatinglanguage)には、独自の i18n ヘルパーユーティリティが付属しています。 起動時に、AEM固有の [i18n ヘルパー](handlebars-helpers.md#i-n). この警告は、既存のヘルパーの上書きを確認するために、サードパーティのライブラリによって生成されます。

### ログ内の警告：OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

複数の Social Communities フォーラムトピックを投稿すると、OakResourceListener processOsgiEventQueue から大量の警告と情報ログが発生する可能性があります。

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

AEM 5.6.1 GA を最新の cq-socialcommunities-pkg-1.4.x またはAEM 6.0 にアップグレードすると、起動時にログファイルにエラーが表示され、再起動時にエラーが見つからないことを示す条件が解決されます。

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
