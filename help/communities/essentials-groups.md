---
title: コミュニティグループの基本事項
seo-title: コミュニティグループの基本事項
description: コミュニティサイトを動的に作成する
seo-description: コミュニティサイトを動的に作成する
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 44%

---


# コミュニティグループの基本事項  {#community-group-essentials}

コミュニティグループ機能は、サブコミュニティを発行ユーザーと作成者環境から許可されたユーザーがコミュニティサイト内で動的に作成する機能です。

Communities [機能パック 1](deploy-communities.md#latestfeaturepack) 以降、別のグループ内でグループをネストできるようになりました。

## クライアント側の基本事項 {#essentials-for-client-side}

### コミュニティグループメンバーリスト {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td>See <a href="creating-groups.md">Community Group</a></td>
  </tr>
 </tbody>
</table>

### コミュニティグループ {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [コミュニティグループ API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [コミュニティグループエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### グループ機能 {#groups-function}

A community site structure that includes a [Groups function](functions.md#groups-function) will support the creation of new `community groups` from the publish and author environments. The community group created will include a `community groups member list` component that will list the members of the group.

One or more [community group templates](tools-groups.md), which provide the design of the community group page(s), may be configured for the Groups function when the function is being added to a [community site template](sites.md) or nested within a community group template.

The inclusion of multiple community group templates results in a choice of design being presented to the authorized user at the time a new community group is created for the community site, as shown in the section on [community groups](creating-groups.md) for authors.

### ネストされたグループ {#nested-groups}

Communities [FP1](deploy-communities.md#latestfeaturepack) 以降では、グループテンプレートにグループ機能を追加することができ、ネストされたグループ（サブコミュニティ）が許可されます。

コミュニティサイトまたはグループテンプレートにグループ機能が含まれる場合、以下の操作が可能です。：

* 作成者環境でサブコミュニティを作成します。

* グループを許可するように設定されている場合は、公開環境でグループを作成します。

オーサー環境でグループを作成するときは、まずコミュニティサイトを公開してから、グループを公開する必要があります。コミュニティサイトを公開すると、ACLが設定されているサブコミュニティのメンバーグループを作成せずに、グループのページが公開されます。 したがって、制限付き（秘密）グループは、グループが明示的に公開されるまで表示できます。

## リンクと関連情報 {#links-and-related-information}

* [ユーザーとユーザーグループの管理](users.md)
* [コミュニティグループコンソール](groups.md)
* [グループ機能](functions.md#groups-function)
* [グループテンプレート](tools-groups.md)

