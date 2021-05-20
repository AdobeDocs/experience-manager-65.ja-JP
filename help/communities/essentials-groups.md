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
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 44%

---

# コミュニティグループの基本事項  {#community-group-essentials}

コミュニティグループ機能は、パブリッシュ環境およびオーサー環境の権限を持つユーザーが、コミュニティサイト内でサブコミュニティを動的に作成する機能です。

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
   <td><a href="creating-groups.md">コミュニティグループ</a>を参照</td>
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

[グループ機能](functions.md#groups-function)を含むコミュニティサイト構造は、パブリッシュ環境とオーサー環境からの新しい`community groups`の作成をサポートします。 作成したコミュニティグループには、グループのメンバーをリストする`community groups member list`コンポーネントが含まれます。

コミュニティグループページのデザインを提供する1つ以上の[コミュニティグループテンプレート](tools-groups.md)は、[コミュニティサイトテンプレート](sites.md)に機能を追加する際、またはコミュニティグループテンプレート内にネストする際に、グループ機能用に設定できます。

複数のコミュニティグループテンプレートを含めると、作成者向けの[コミュニティグループ](creating-groups.md)の節に示すように、コミュニティサイト用の新しいコミュニティグループを作成する際に、承認済みユーザーにデザインを提示できます。

### ネストされたグループ {#nested-groups}

Communities [FP1](deploy-communities.md#latestfeaturepack) 以降では、グループテンプレートにグループ機能を追加することができ、ネストされたグループ（サブコミュニティ）が許可されます。

コミュニティサイトまたはグループテンプレートにグループ機能が含まれる場合、以下の操作が可能です。：

* オーサー環境にサブコミュニティを作成します。

* パブリッシュ環境でグループを許可するように設定されている場合は、そのグループを作成します。

オーサー環境でグループを作成するときは、まずコミュニティサイトを公開してから、グループを公開する必要があります。コミュニティサイトを公開すると、ACLが設定されているサブコミュニティのメンバーグループを作成せずに、グループのページが公開されます。 したがって、グループが明示的に公開されるまで、制限付き（シークレット）グループが表示される場合があります。

## リンクと関連情報 {#links-and-related-information}

* [ユーザーとユーザーグループの管理](users.md)
* [コミュニティグループコンソール](groups.md)
* [グループ機能](functions.md#groups-function)
* [グループテンプレート](tools-groups.md)
