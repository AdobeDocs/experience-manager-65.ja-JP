---
title: アクティビティストリームの基本事項
description: メンバーによって実行された最近のアクティビティのリスト、またはコンテンツの単一スレッド上の最近のアクティビティのリスト
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 4%
---
# アクティビティストリームの基本事項 {#activity-stream-essentials}

フォーラムやブログへの投稿など、ログインしたコミュニティメンバーのアクティビティは、アクティビティストリームコンポーネントの設定を通じて、様々な方法でフィルタリングおよび表示できるストリームに収集されます。

フォロー機能は、コミュニティメンバーが関心のある投稿や他のコミュニティメンバーをフォローする際に、別の一連のアクティビティを追加します。

すべての[ コミュニティサイト ](/help/communities/overview.md#communitiessites)には、ログイン済みメンバーのユーザープロファイルページが含まれており、同じ方法でメンバーアクティビティが表示されます。

## 概念 {#concepts}

*アクティビティストリーム*&#x200B;は、メンバーによって実行された最近のアクティビティのリスト、またはフォーラムのトピックやブログなどのコンテンツの単一スレッド上の最近のアクティビティのリストです。

メンバーは、別の個人やコンテンツをフォローすることで、アクティビティストリームをフォローできます。

*ニュースフィード*&#x200B;は、メンバーが後に続くアクティビティストリームを単一ストリームに結合したものです。

*[ソーシャルグラフ](/help/communities/essentials-socialgraph.md)*&#x200B;は、あるメンバーと別のメンバーの次の関係をキャプチャします。

## クライアントサイドの基本 {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/アクティビティストリーム/コンポーネント/hbs/アクティビティストリーム</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>包含可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td><a href="/help/communities/activities.md"> アクティビティストリーム機能</a>を参照</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](/help/communities/client-customize.md)

## サーバーサイドの基本 {#essentials-for-server-side}

* [Activity Streams API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [Activity Streams リスナーAPI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [サーバーサイドのカスタマイズ](/help/communities/server-customize.md)

### アクティビティストリーム機能 {#activity-stream-function}

[Activity Stream関数](/help/communities/functions.md#activity-stream-function)を含むコミュニティサイト構造には、設定済みの`activity streams` コンポーネントが含まれています。
