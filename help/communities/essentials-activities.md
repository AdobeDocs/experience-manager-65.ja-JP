---
title: アクティビティストリームの基本事項
seo-title: Activity Stream Essentials
description: メンバーが実行した最近のアクティビティのリスト、または単一のコンテンツスレッドの最近のアクティビティのリスト
seo-description: List of recent activites performed by a member or a list of recent activities on a single thread of content
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 62%

---

# アクティビティストリームの基本事項 {#activity-stream-essentials}

フォーラムまたはブログへの投稿など、サインインしているコミュニティメンバーのアクティビティを 1 つのストリームにまとめ、アクティビティストリームコンポーネントの設定を使用して、さまざまな方法でフィルタリングしたり、表示したりできます。

コミュニティメンバーが関心のある投稿や他のコミュニティメンバーをフォローしているときは、フォロー機能によって、別のアクティビティセットが追加されます。

どの[コミュニティサイト](/help/communities/overview.md#communitiessites)にも、サインインしているメンバーのユーザープロファイルページが用意されており、メンバーのアクティビティが同じ形式で表示されます。

## 概念  {#concepts}

An *アクティビティストリーム* は、メンバーが実行した最近のアクティビティのリスト、またはフォーラムトピックやブログなどの単一のコンテンツスレッド上での最近のアクティビティのリストです。

メンバーは、別の個人やコンテンツをフォローすることによって、アクティビティストリームをフォローできます。

ニュースフィード&#x200B;**&#x200B;とは、メンバーがフォローしている複数のアクティビティストリームを単一のストリームに統合したものです。

*[ソーシャルグラフ](/help/communities/essentials-socialgraph.md)*&#x200B;とは、メンバー間のフォロー関係を表したものです。

## クライアント側の基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>詳しくは、 <a href="/help/communities/activities.md">アクティビティストリーム機能</a></td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](/help/communities/client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [アクティビティストリーム API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [アクティビティストリームリスナー API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [サーバー側のカスタマイズ](/help/communities/server-customize.md)

### アクティビティストリーム機能 {#activity-stream-function}

を含むコミュニティサイト構造 [アクティビティストリーム関数](/help/communities/functions.md#activity-stream-function)（設定済みを含む） `activity streams` コンポーネント。
