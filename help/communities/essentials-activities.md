---
title: アクティビティストリームの基本事項
description: メンバーが実行した最近のアクティビティのリスト、またはコンテンツの単一のスレッド上の最近のアクティビティのリスト
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 4%

---

# アクティビティストリームの基本事項 {#activity-stream-essentials}

フォーラムやブログへの投稿など、サインインしたコミュニティメンバーのアクティビティは、ストリームに収集され、アクティビティストリームコンポーネントの設定を通じて、様々な方法でフィルタリングおよび表示できます。

コミュニティメンバーが関心のある投稿や他のコミュニティメンバーの投稿をフォローする際に、フォロー機能は別のアクティビティのセットを追加します。

すべて [コミュニティサイト](/help/communities/overview.md#communitiessites) 同じ方法でメンバーアクティビティを表示するサインイン済みメンバーのユーザープロファイルページを含めます。

## 概念  {#concepts}

An *アクティビティストリーム* は、メンバーが実行した最近のアクティビティのリスト、またはフォーラムトピックやブログなどの単一のコンテンツスレッド上での最近のアクティビティのリストです。

メンバーは、別の個人またはコンテンツをフォローすることで、アクティビティストリームをフォローします。

A *ニュースフィード* は、メンバーが続くアクティビティストリームを単一のストリームに結合したものです。

A *[ソーシャルグラフ](/help/communities/essentials-socialgraph.md)* は、あるメンバーと別のメンバーとの次の関係をキャプチャします。

## クライアント側の基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td>
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
