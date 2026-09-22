---
title: コミュニティグループの基本事項
description: 許可されたユーザーがコミュニティグループ機能を使用して、コミュニティサイト内にサブコミュニティを動的に作成する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%
---
# コミュニティグループの基本事項  {#community-group-essentials}

コミュニティグループ機能は、パブリッシュ環境とオーサー環境の許可されたユーザーが、コミュニティサイト内でサブコミュニティを動的に作成する機能です。

コミュニティ [機能パック 1](deploy-communities.md#latestfeaturepack)の時点では、グループを他のグループ内にネストできます。

## クライアントサイドの基本 {#essentials-for-client-side}

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
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><a href="creating-groups.md"> コミュニティグループ </a>を参照</td>
  </tr>
 </tbody>
</table>

### コミュニティグループ {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/グループ/コンポーネント/hbs/コミュニティグループ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの基本 {#essentials-for-server-side}

* [コミュニティグループ API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [コミュニティグループエンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### Groups関数 {#groups-function}

[Groups関数](functions.md#groups-function)を含むコミュニティサイト構造は、パブリッシュ環境とオーサー環境からの新しい`community groups`の作成をサポートしています。 作成されたコミュニティグループには、グループのメンバーをリストする`community groups member list` コンポーネントが含まれています。

コミュニティ グループ ページのデザインを提供する1つ以上の[ コミュニティ グループ テンプレート ](tools-groups.md)を、グループ関数に設定できます。 これは、関数が[ コミュニティサイトテンプレート ](sites.md)に追加されているか、コミュニティグループテンプレート内にネストされている場合に当てはまります。

複数のコミュニティグループテンプレートを含めると、選択が行われます。 すなわち、コミュニティサイト用にコミュニティグループを作成する際に、許可されたユーザに提示されるデザインの選択である。 作成者については、[ コミュニティグループ ](creating-groups.md)の節を参照してください。

### ネストされたグループ {#nested-groups}

コミュニティ [FP1](deploy-communities.md#latestfeaturepack)の時点では、グループ関数をグループ テンプレートに含めることができるため、ネストされたグループ （サブコミュニティ）を使用できます。

コミュニティサイトまたはグループテンプレートにグループ機能が含まれている場合、次のことが可能です。

* オーサー環境でサブコミュニティを作成します。

* 許可するように設定されている場合は、パブリッシュ環境でグループを作成します。

オーサー環境でグループを作成する場合は、最初にコミュニティサイトを公開してからグループを公開する必要があります。 コミュニティサイトを公開すると、ACLが設定されているサブコミュニティのメンバーグループを作成せずに、グループのページが公開されます。 したがって、制限付き（秘密鍵）グループは、そのグループが明示的に公開されるまで表示される場合があります。

## リンクと関連情報 {#links-and-related-information}

* [ユーザーとユーザーグループの管理](users.md)
* [Communities Groups Console](groups.md)
* [Groups関数](functions.md#groups-function)
* [グループテンプレート](tools-groups.md)
