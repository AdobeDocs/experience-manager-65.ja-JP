---
title: ソーシャルグラフの基本事項
seo-title: ソーシャルグラフの基本事項
description: フォローコンポーネントとフォロー中コンポーネントの概要
seo-description: フォローコンポーネントとフォロー中コンポーネントの概要
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# ソーシャルグラフの基本事項  {#social-graph-essentials}

The ability for a Community member to follow [activities](essentials-activities.md) as well as be followed is established through two components:

The `following` component must be associated with another resource, and this association is already established for existing Communities members and features in a [community site](overview.md#communitiessites).

The `following` component lists the members that are either following the current member or are being followed by the current member. コミュニティサイト用に設定されたユーザプロファイルに、会員間の関係のソーシャルグラフを含む。

## クライアント側の基本事項 {#essentials-for-client-side}

### フォロー {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relationships</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>インクルード可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>テンプレート</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>See <a href="socialgraph.md">Using Social Graph</a></td>
  </tr>
  <tr>
   <td><strong> optional<br /> property</strong></td>
   <td>
    <ul>
     <li>名前: <strong><code>outgoing</code></strong></li>
     <li>タイプ：Boolean</li>
     <li>値:<br />
      <ul>
       <li><i>True </i>— コンポ <code>following</code> ーネントは、現在ログインしているメンバをリストします。 <code>follows</code></li>
       <li><i>False </i>— コンポ <code>following</code> ーネントは、現在サインインして <code>follow </code>いるメンバをリストします。</li>
      </ul> </li>
    </ul> <p>Defaults to <i>true</i> if the property is missing. 現在、作成者モードで編集ダイアログを使用してこのプロパティを設定することはできません。 The property must be added to an instance of the <code>following </code>node using <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### フォロー {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**インクルード可能&#x200B;**](scf.md#add-or-include-a-communities-component) | いいえ |
| **テンプレート** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [ソーシャルグラフ API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [ソーシャルグラフエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [サーバー側のカスタマイズ](server-customize.md)

