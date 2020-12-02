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
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 23%

---


# ソーシャルグラフの基本事項   {#social-graph-essentials}

コミュニティのメンバーが[アクティビティ](essentials-activities.md)に従う能力は、次の2つの要素を介して確立されます。

`following`コンポーネントは別のリソースと関連付ける必要があります。この関連付けは、既に[コミュニティサイト](overview.md#communitiessites)の既存のコミュニティのメンバーと機能に対して確立されています。

`following`コンポーネントは、現在のメンバーに続くメンバー、または現在のメンバーの後に続くメンバーをリストします。 会員間の関係のこのソーシャルグラフは、コミュニティサイト用に設定されたユーザプロファイルに含まれる。

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
   <td>不可</td>
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
   <td><a href="socialgraph.md">ソーシャルグラフの使用</a>を参照</td>
  </tr>
  <tr>
   <td><strong> オプションの<br />プロパティ</strong></td>
   <td>
    <ul>
     <li>名前: <strong><code>outgoing</code></strong></li>
     <li>タイプ：Boolean</li>
     <li>値：<br />
      <ul>
       <li><i>True  </i>- <code>following</code> コンポーネントは、現在サインインしているメンバをリストします <code>follows</code></li>
       <li><i>False  </i>- <code>following</code> コンポーネントは、現在サインインしているメンバ <code>follow </code>をリストします。</li>
      </ul> </li>
    </ul> <p>プロパティが見つからない場合は、デフォルトで<i>true</i>に設定されます。 現在、作成者モードで編集ダイアログを使用してこのプロパティを設定することはできません。 <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>を使用して、<code>following </code>ノードのインスタンスにプロパティを追加する必要があります。</p> </td>
  </tr>
 </tbody>
</table>

### フォロー {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**インクルード可能**](scf.md#add-or-include-a-communities-component) | 不可 |
| **テンプレート** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [クライアント側のカスタマイズ](client-customize.md)

## サーバー側の基本事項  {#essentials-for-server-side}

* [ソーシャルグラフ API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [ソーシャルグラフエンドポイント](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [サーバー側のカスタマイズ](server-customize.md)

