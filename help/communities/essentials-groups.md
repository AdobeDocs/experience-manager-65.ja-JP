---
title: コミュニティグループの基本事項
description: 承認済みユーザーがコミュニティグループ機能を使用して、コミュニティサイト内にサブコミュニティを動的に作成する方法を説明します。
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
source-wordcount: '404'
ht-degree: 4%

---

# コミュニティグループの基本事項  {#community-group-essentials}

コミュニティグループ機能は、権限のあるユーザーがパブリッシュ環境とオーサー環境からサブコミュニティをコミュニティサイト内に動的に作成する機能です。

Communities [&#x200B; 機能パック 1](deploy-communities.md#latestfeaturepack) の時点で、グループを他のグループ内にネストすることができます。

## クライアントサイドの基本事項 {#essentials-for-client-side}

### コミュニティグループのメンバーリスト {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/グループ/コンポーネント/hbs/communitygroupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>properties</strong></td>
   <td><a href="creating-groups.md"> コミュニティグループ </a> を参照</td>
  </tr>
 </tbody>
</table>

### コミュニティグループ {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/グループ/コンポーネント/hbs/コミュニティ グループ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [&#x200B; コミュニティグループ API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [&#x200B; コミュニティグループエンドポイント &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [サーバーサイドのカスタマイズ](server-customize.md)

### Groups 関数 {#groups-function}

[Groups 関数 &#x200B;](functions.md#groups-function) を含むコミュニティサイト構造は、パブリッシュ環境とオーサー環境からの新しい `community groups` の作成をサポートしています。 作成されたコミュニティグループには、グループのメンバーをリストする `community groups member list` コンポーネントが含まれています。

コミュニティグループページのデザインを提供する 1 つ以上の [&#x200B; コミュニティグループテンプレート &#x200B;](tools-groups.md) をグループ機能用に設定できます。 これは、関数が [&#x200B; コミュニティサイトテンプレート &#x200B;](sites.md) に追加されている場合や、コミュニティグループテンプレート内にネストされている場合に当てはまります。

複数のコミュニティグループテンプレートを含めると、選択することになります。 つまり、コミュニティサイトのコミュニティグループを作成する際に、権限のあるユーザーに提示されるデザインの選択です。 作成者については、[&#x200B; コミュニティグループ &#x200B;](creating-groups.md) の節を参照してください。

### ネストされたグループ {#nested-groups}

コミュニティ [FP1](deploy-communities.md#latestfeaturepack) の時点で、Groups 関数をグループテンプレートに含めることができるので、ネストされたグループ（サブコミュニティ）が可能になります。

コミュニティサイトまたはグループテンプレートにグループ機能が含まれている場合は、次の操作を行うことができます。

* オーサー環境でサブコミュニティを作成します。

* パブリッシュ環境にグループを作成します（許可するように設定されている場合）。

オーサー環境でグループを作成する場合、まずコミュニティサイトを公開してから、グループを公開する必要があります。 コミュニティサイトを公開すると、ACL が設定されたサブコミュニティのメンバーグループは作成されずに、グループのページが公開されます。 したがって、制限された（秘密鍵）グループは、そのグループが明示的に公開されるまで表示される場合があります。

## リンクと関連情報 {#links-and-related-information}

* [ユーザーとユーザーグループの管理](users.md)
* [コミュニティグループコンソール](groups.md)
* [Groups 関数](functions.md#groups-function)
* [グループテンプレート](tools-groups.md)
