---
title: コミュニティグループの基本事項
description: コミュニティサイトの動的な作成
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: 681d1e6bd885b801b930e580d95645f160f17cea
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 4%

---

# コミュニティグループの基本事項  {#community-group-essentials}

コミュニティグループ機能を使用すると、パブリッシュ環境およびオーサー環境から許可されたユーザーがコミュニティサイト内でサブコミュニティを動的に作成できます。

コミュニティの時点 [機能パック 1](deploy-communities.md#latestfeaturepack)の場合、グループを他のグループ内にネストすることが可能です

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
   <td>詳しくは、 <a href="creating-groups.md">コミュニティグループ</a></td>
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

* [コミュニティグループ API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [コミュニティグループエンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [サーバー側のカスタマイズ](server-customize.md)

### グループ機能 {#groups-function}

を含むコミュニティサイト構造 [グループ機能](functions.md#groups-function) 新しい `community groups` パブリッシュ環境およびオーサー環境から。 作成したコミュニティグループには、 `community groups member list` グループのメンバーをリストするコンポーネント。

1 つ以上 [コミュニティグループテンプレート](tools-groups.md)（コミュニティグループページのデザインを提供）は、関数を [コミュニティサイトテンプレート](sites.md) またはコミュニティグループテンプレート内にネストされている

複数のコミュニティグループテンプレートを組み込むと、コミュニティサイト用に新しいコミュニティグループを作成する際に、承認済みユーザーに提示するデザインを選択できます (「 [コミュニティグループ](creating-groups.md) 作成者向け

### ネストされたグループ {#nested-groups}

コミュニティの時点 [FP1](deploy-communities.md#latestfeaturepack)を使用すると、グループ機能をグループテンプレート内に組み込むことができ、ネストされたグループ（サブコミュニティ）に対して使用できます。

コミュニティサイトまたはグループテンプレートにグループ機能が含まれている場合、次の操作が可能です。

* オーサー環境にサブコミュニティを作成します。

* グループを許可するように設定されている場合は、パブリッシュ環境でグループを作成します。

オーサー環境でグループを作成する場合は、まずコミュニティサイトを公開し、次にグループを公開する必要があります。 コミュニティサイトを公開すると、ACL が設定されているサブコミュニティのメンバーグループを作成せずに、グループのページが公開されます。 したがって、制限付き（シークレット）グループは、グループが明示的に公開されるまで表示される場合があります。

## リンクと関連情報 {#links-and-related-information}

* [ユーザーとユーザーグループの管理](users.md)
* [コミュニティグループコンソール](groups.md)
* [グループ機能](functions.md#groups-function)
* [グループテンプレート](tools-groups.md)
