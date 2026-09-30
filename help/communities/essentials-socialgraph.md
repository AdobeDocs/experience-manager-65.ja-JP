---
title: ソーシャルグラフの基本事項
description: コミュニティサイトで次のコンポーネントとフォローコンポーネントを使用して、ソーシャルグラフの基本について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 6%
---
# ソーシャルグラフの基本事項  {#social-graph-essentials}

コミュニティメンバーが[&#x200B; アクティビティ &#x200B;](essentials-activities.md)に従ってフォローする機能は、次の2つのコンポーネントによって確立されます。

`following` コンポーネントは別のリソースに関連付ける必要があり、この関連付けは[&#x200B; コミュニティサイト &#x200B;](overview.md#communitiessites)の既存のコミュニティメンバーと機能に対して既に確立されています。

`following` コンポーネントには、現在のメンバーに従っているか、現在のメンバーに従っているメンバーが一覧表示されます。 このメンバー間の関係のソーシャルグラフは、コミュニティサイト用に構築されたユーザープロファイルに含まれる。

## クライアントサイドの基本 {#essentials-for-client-side}

### フォロー {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/ソーシャルグラフ/コンポーネント/hbs/関係性</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong> テンプレート </strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>ソーシャルグラフの使用<a href="socialgraph.md">を参照</a></td>
  </tr>
  <tr>
   <td><strong> オプションの<br /> プロパティ</strong></td>
   <td>
    <ul>
     <li>名前： <strong><code>outgoing</code></strong></li>
     <li>型：ブール値</li>
     <li>値：<br />
      <ul>
       <li><i>True </i>- <code>following</code> コンポーネントには、サインインしたメンバーのメンバーが一覧表示されます <code>follows</code></li>
       <li><i>False </i>- <code>following</code> コンポーネントには、<code>follow </code> サインイン メンバーのメンバーが一覧表示されます</li>
      </ul> </li>
    </ul> <p>プロパティが見つからない場合は、デフォルトで<i>true</i>になります。 オーサーモードの編集ダイアログを使用してこのプロパティを設定することはできません。 プロパティは、<a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>を使用して<code>following</code> ノードのインスタンスに追加する必要があります。</p> </td>
  </tr>
 </tbody>
</table>

### フォロー {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**包含可能**](scf.md#add-or-include-a-communities-component) | いいえ |
| **テンプレート** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの基本 {#essentials-for-server-side}

* [ソーシャルグラフ API](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [ソーシャルグラフエンドポイント](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [サーバーサイドのカスタマイズ](server-customize.md)
