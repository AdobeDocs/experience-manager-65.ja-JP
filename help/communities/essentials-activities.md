---
title: アクティビティストリームの基本事項
description: メンバーによって実行された最近のアクティビティのリスト、またはコンテンツの単一スレッドにおける最近のアクティビティのリスト
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 4%

---

# アクティビティストリームの基本事項 {#activity-stream-essentials}

フォーラムやブログへの投稿など、ログインしたコミュニティメンバーのアクティビティは、アクティビティストリームコンポーネントの設定を通じて様々な方法でフィルタリングおよび表示されるストリームに収集されます。

フォロー機能を使用すると、コミュニティメンバーが興味のある投稿や他のコミュニティメンバーをフォローする場合に、別のアクティビティを追加できます。

すべて [コミュニティサイト](/help/communities/overview.md#communitiessites) 同じ方法でメンバーアクティビティを表示するサインイン メンバーのユーザープロファイル ページを含めます。

## 概念  {#concepts}

An *アクティビティストリーム* は、メンバーによって実行された最近のアクティビティのリスト、またはフォーラムのトピックやブログなど、コンテンツの単一スレッドにおける最近のアクティビティのリストです。

メンバーは、別の個人またはコンテンツに従って、アクティビティストリームをフォローできます。

A *ニュース フィード* は、メンバーの後に続くアクティビティストリームを 1 つのストリームに結合したものです。

A *[ソーシャルグラフ](/help/communities/essentials-socialgraph.md)* あるメンバーから別のメンバーへの次の関係をキャプチャします。

## クライアントサイドの基本事項 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/アクティビティストリーム/コンポーネント/hbs/アクティビティストリーム</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>参照： <a href="/help/communities/activities.md">アクティビティストリーム機能</a></td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](/help/communities/client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [アクティビティストリーム API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [アクティビティストリームリスナー API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [サーバーサイドのカスタマイズ](/help/communities/server-customize.md)

### アクティビティストリーム機能 {#activity-stream-function}

を含むコミュニティサイト構造 [アクティビティストリーム関数](/help/communities/functions.md#activity-stream-function)、設定済みのを含む `activity streams` コンポーネント。
