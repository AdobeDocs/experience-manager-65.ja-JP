---
title: ソーシャルグラフの基本事項
seo-title: Social Graph Essentials
description: フォローコンポーネントとフォロー中コンポーネントの概要
seo-description: follow component and following component overview
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 21%

---

# ソーシャルグラフの基本事項  {#social-graph-essentials}

コミュニティメンバーがフォローする機能 [アクティビティ](essentials-activities.md) それに続くものは、次の 2 つの構成要素を通じて確立されます。

この `following` コンポーネントは別のリソースに関連付ける必要があります。この関連付けは、 [コミュニティサイト](overview.md#communitiessites).

この `following` コンポーネントは、現在のメンバーをフォローしているメンバー、または現在のメンバーをフォローしているメンバーをリストします。 このメンバー間の関係のソーシャルグラフは、コミュニティサイト用に確立されたユーザープロファイルに含まれます。

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
   <td>詳しくは、 <a href="socialgraph.md">ソーシャルグラフの使用</a></td>
  </tr>
  <tr>
   <td><strong> <br /> プロパティ（オプション）</strong></td>
   <td>
    <ul>
     <li>名前： <strong><code>outgoing</code></strong></li>
     <li>型：ブール値</li>
     <li>値：<br />
      <ul>
       <li><i>True </i>- <code>following</code> コンポーネントは、現在サインインしているメンバーを一覧表示します <code>follows</code></li>
       <li><i>False </i>- <code>following</code> コンポーネントは次のメンバーをリストします： <code>follow </code>現在サインインしているメンバー</li>
      </ul> </li>
    </ul> <p>デフォルトはです。 <i>true</i> を返します。 現在、オーサーモードで編集ダイアログを使用してこのプロパティを設定することはできません。 プロパティを <code>following </code>ノードを使用 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### フォロー {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**インクルード可能**](scf.md#add-or-include-a-communities-component) | いいえ |
| **テンプレート** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項 {#essentials-for-server-side}

* [ソーシャルグラフ API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [ソーシャルグラフエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [サーバー側のカスタマイズ](server-customize.md)
