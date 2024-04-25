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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 7%

---

# ソーシャルグラフの基本事項  {#social-graph-essentials}

コミュニティメンバーがフォローする機能 [activities](essentials-activities.md) そして、次の 2 つのコンポーネントを通じて従う必要があります。

この `following` コンポーネントは別のリソースに関連付ける必要があり、この関連付けは、 [コミュニティサイト](overview.md#communitiessites).

この `following` コンポーネントは、現在のメンバーに続くメンバー、または現在のメンバーの後に続くメンバーをリストします。 このメンバー間の関係のソーシャルグラフは、コミュニティサイト用に作成されたユーザープロファイルに含まれます。

## クライアントサイドの基本事項 {#essentials-for-client-side}

### フォロー {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>ソーシャル/ソーシャルグラフ/コンポーネント/hbs/関係</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>includable</strong></a></td>
   <td>いいえ</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> properties</strong></td>
   <td>参照： <a href="socialgraph.md">ソーシャルグラフの使用</a></td>
  </tr>
  <tr>
   <td><strong> optional<br /> プロパティ</strong></td>
   <td>
    <ul>
     <li>名前： <strong><code>outgoing</code></strong></li>
     <li>型：ブール値</li>
     <li>値：<br />
      <ul>
       <li><i>True </i> – が <code>following</code> コンポーネントは、サインインしたメンバーをリストします <code>follows</code></li>
       <li><i>False </i> – が <code>following</code> コンポーネントは、次の操作を行うメンバーを一覧表示します <code>follow </code>ログインしたメンバー</li>
      </ul> </li>
    </ul> <p>デフォルトは <i>true</i> プロパティがない場合。 オーサーモードで編集ダイアログを使用して、このプロパティを設定することはできません。 プロパティは、のインスタンスに追加する必要があります <code>following</code> を使用したノード <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### フォロー {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**includable**](scf.md#add-or-include-a-communities-component) | いいえ |
| **templates** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [クライアントサイドのカスタマイズ](client-customize.md)

## サーバーサイドの初期設定 {#essentials-for-server-side}

* [ソーシャルグラフ API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [ソーシャルグラフのエンドポイント](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [サーバーサイドのカスタマイズ](server-customize.md)
