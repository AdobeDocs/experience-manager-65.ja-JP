---
title: ソーシャルグラフの基本事項
description: コミュニティサイトでフォローコンポーネントとフォローコンポーネントを使用して、ソーシャルグラフの基本を学びます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 7%

---

# ソーシャルグラフの基本事項  {#social-graph-essentials}

コミュニティメンバーがフォローする機能 [アクティビティ](essentials-activities.md) その後には、次の 2 つの要素を通じて確立されます。

The `following` コンポーネントは別のリソースに関連付ける必要があります。この関連付けは、 [コミュニティサイト](overview.md#communitiessites).

The `following` コンポーネントは、現在のメンバーをフォローしているメンバー、または現在のメンバーをフォローしているメンバーをリストします。 このメンバー間の関係のソーシャルグラフは、コミュニティサイト用に確立されたユーザープロファイルに含まれます。

## クライアント側の基本事項 {#essentials-for-client-side}

### フォロー {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relationships</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>包含可能な</strong></a></td>
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
   <td>詳しくは、 <a href="socialgraph.md">ソーシャルグラフの使用</a></td>
  </tr>
  <tr>
   <td><strong> オプション<br /> プロパティ</strong></td>
   <td>
    <ul>
     <li>名前： <strong><code>outgoing</code></strong></li>
     <li>型：ブール値</li>
     <li>値：<br />
      <ul>
       <li><i>True </i>- <code>following</code> コンポーネントは、サインインしたメンバーの一覧を表示します <code>follows</code></li>
       <li><i>False </i>- <code>following</code> コンポーネントは、次のメンバーをリストします。 <code>follow </code>サインインしたメンバー</li>
      </ul> </li>
    </ul> <p>デフォルトはです。 <i>true</i> を返します。 オーサーモードで編集ダイアログを使用してこのプロパティを設定することはできません。 プロパティは、 <code>following</code> を使用してノードを作成 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### フォロー {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**包含可能な**](scf.md#add-or-include-a-communities-component) | いいえ |
| **テンプレート** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [ソーシャルグラフ API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [ソーシャルグラフエンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [サーバー側のカスタマイズ](server-customize.md)
