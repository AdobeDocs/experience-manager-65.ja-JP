---
title: リリース車両定義の更新
seo-title: リリース車両定義の更新
description: この記事では、完全リリース、機能パック、サービスパックなど、AEM の各種リリースについて詳しく説明します。
seo-description: この記事では、完全リリース、機能パック、サービスパックなど、AEM の各種リリースについて詳しく説明します。
uuid: 388fb6f5-0249-41e2-a460-1bb4cd0f8494
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 32695db5-d62d-4959-8a24-3d56b4a19904
translation-type: tm+mt
source-git-commit: 6a5a8e64c6eaab816d07d8206601849c974d1e26
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 75%

---


# AEM Updateリリース車の定義{#update-release-vehicle-definitions}

このドキュメントでは、アドビから提供される完全リリース、機能パック、サービスパックなど、Adobe Experience Manager（AEM）の各種リリースについて詳しく説明します。

>[!Note]
>
>AEMアップデートリリースのリリーススケジュールについては、 [AEMアップデートリリースロードマップを参照してください。](https://helpx.adobe.com/experience-manager/update-releases-roadmap.html)

## 完全リリース {#full-release}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td>
    <ul>
     <li>予定されたリリース</li>
     <li>リリースノートで定義されている、特定のバージョンに対するアップグレードパスをサポート</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>
    <ul>
     <li>メジャーリリースのバージョン番号は、数式X+1.Y.Zに基づいて増加します。 </li>
     <li>マイナーリリースのバージョン番号は、X.Y+1.Z という式に基づいて大きくなります。</li>
    </ul> <p>ここで、Xはプライマリ・バージョン番号、Yはセカンダリ・バージョン番号、Zはパッチ番号を表します。</p> </td>
  </tr>
  <tr>
   <td><strong>含まれるもの</strong></td>
   <td>
    <ul>
     <li>新機能</li>
     <li>機能強化</li>
     <li>バグの修正</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>ドキュメント</strong></td>
   <td>
    <ul>
     <li>リリースノートはドキュメントポータルで入手できます。</li>
     <li>機能、機能強化およびバグの修正に関するドキュメントは、ドキュメントポータルで入手できます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>タイミング</strong></td>
   <td>毎年</td>
  </tr>
  <tr>
   <td><strong>入手可能性とインストール</strong></td>
   <td>
    <ul>
     <li>スタンドアロンの製品インストーラーとして提供されます。</li>
     <li>Licensing WebサイトおよびManaged Services Licensing Webサイトから入手可能</li>
     <li>コンテンツリポジトリの移行が必要な場合があります。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>テストのレベル</strong></td>
   <td>QA によって完全に検証済み</td>
  </tr>
 </tbody>
</table>

## サービスパック {#service-pack}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td>
    <ul>
     <li>予定されたリリース</li>
     <li>現在はロールバック不可</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>
    <ul>
     <li>パッチのリリース番号は 1 桁の数字です。</li>
     <li>インストール後、X.Y.Z.SPxの式に基づいて、インストール済みのリリース番号のパッチ桁を増やします。</li>
     <li>ここで、Xはプライマリ・バージョン番号、Yはセカンダリ・バージョン番号、Zはパッチ番号を表します。 x はサービスパック番号です。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>含まれるもの</strong></td>
   <td>
    <ul>
     <li>新機能</li>
     <li>機能強化</li>
     <li>バグの修正</li>
     <li>Common Interest 機能パック（ある場合）</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>ドキュメント</strong></td>
   <td>
    <ul>
     <li>リリースノートはドキュメントポータルで入手できます。</li>
     <li>機能、機能強化およびバグの修正に関するドキュメントは、ドキュメントポータルで入手できます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>タイミング</strong></td>
   <td>毎四半期</td>
  </tr>
  <tr>
   <td><strong>入手可能性とインストール</strong></td>
   <td>
    <ul>
     <li>パッケージとして提供</li>
     <li>パッケージ共有で入手可能</li>
     <li>既存機能のインストールが必要</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>テストのレベル</strong></td>
   <td>
    <ul>
     <li>すべての修正が QA 検証済み</li>
     <li>自動実行を使用したパッケージ全体の健全性</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 累積修正パック  {#cumulative-fix-pack-aem}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td>
    <ul>
     <li>複数の修正を一度にリリースする提供モデル</li>
     <li>個々のコンポーネントからなるコンテンツパッケージを含む集積コンテンツパッケージ</li>
     <li>ホットフィックスのロールオーバーであり、機能強化は含まない</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td><p>X.Y.Z.CFPx</p> <p>ここで、Xはプライマリ・バージョン番号、Yはセカンダリ・バージョン番号、Zはパッチ番号を表します。 x は累積サービスパック番号です。</p> </td>
  </tr>
  <tr>
   <td><strong>含まれるもの</strong></td>
   <td><p>CFP は、指定された日付以降のすべてのコンポーネントの修正を含む、累積修正パックです。例えば、CFP3 を適用する場合、CFP3 = CFP1 + CFP2 です。</p> </td>
  </tr>
  <tr>
   <td><strong>ドキュメント</strong></td>
   <td>リリースノートはドキュメントポータルで入手できます。</td>
  </tr>
  <tr>
   <td><strong>タイミング</strong></td>
   <td>四分位数</td>
  </tr>
  <tr>
   <td><strong>入手可能性とインストール</strong></td>
   <td>
    <ul>
     <li>パッケージとして提供</li>
     <li>パッケージ共有で入手可能</li>
     <li>リリースされている最新のサービスパックに依存</li>
     <li>CFP は他に依存しません。ユーザーは依存関係の検索や解決を気にする必要はありません。CFP は、最新リリースのサービスパック上にインストールする必要があります。</li>
     <li>CFP は、単一パッケージとしてインストールでき、エクスペリエンスを向上させます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>テストのレベル</strong></td>
   <td>統合レベルでの QA 検証済みおよび回帰テスト</td>
  </tr>
 </tbody>
</table>

## オーバーレイ {#overlay}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>overlay-&lt;ticket ID&gt;</td>
  </tr>
  <tr>
   <td><strong>含まれるもの</strong></td>
   <td>JS ファイルまたは JSP ファイルのバグの修正</td>
  </tr>
  <tr>
   <td><strong>ドキュメント</strong></td>
   <td>なし</td>
  </tr>
  <tr>
   <td><strong>タイミング</strong></td>
   <td>必要に応じて</td>
  </tr>
  <tr>
   <td><strong>入手可能性とインストール</strong></td>
   <td>
    <ul>
     <li>AEM カスタマーケアがパッケージとして提供</li>
     <li>サービスパックまたはフルリリースに必ずしも含まれていない</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>テストのレベル</strong></td>
   <td>カスタマーケアによって検証済み</td>
  </tr>
 </tbody>
</table>

## 機能パック {#feature-pack}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td>
    <ul>
     <li>機能パックはアドオン機能であり、サービスパックを通じて提供されます。AEMバージョンの最後のService Packがリリースされた場合、アドビは将来、その機能パックを提供しなくなります。</li>
     <li>機能パックには、製品の機能強化が含まれます。以降の製品リリースで予定されているが、アドビの製品管理部門の決定に基づいて予定より早く提供されます。</li>
     <li>機能は常に次のメジャーリリースに統合され、顧客が必要とする AEM バージョンに移植されます。</li>
     <li>Common Interest 機能パックと GA 機能パックは次のサービスパックに統合されます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>cq-&lt;Release Version&gt;-featurepack-&lt;featurepack ID&gt;-&lt;featurepack version&gt;</td>
  </tr>
  <tr>
   <td><strong>含まれるもの</strong></td>
   <td>
    <ul>
     <li>新機能</li>
     <li>機能強化</li>
     <li>バグの修正（製品の増分アップデート）</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>ドキュメント</strong></td>
   <td>ドキュメントは helpx.adobe.com で入手できます。</td>
  </tr>
  <tr>
   <td><strong>タイミング</strong></td>
   <td>製品領域によって異なります。</td>
  </tr>
  <tr>
   <td><strong>入手可能性とインストール</strong></td>
   <td>
    <ul>
     <li>サービスパックを使用して配信</li>
     <li>パッケージ共有で入手可能. お客様は、パッケージ共有を通じてアドビの利用条件に同意します。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>テストのレベル</strong></td>
   <td>一般提供の機能パックは QA 検証済み</td>
  </tr>
 </tbody>
</table>

* [1]: OAKの修正は、個々のホットフィックスとしては提供されません。 しかし、以降の累積 Oak ホットフィックスに含まれます。必要に応じて、最新の COFP 上で診断ビルドを利用できます。前提条件は、最新の COFP を実行していることです。診断ビルドは、ホットフィックスと同じレベルの品質保証を提供するだけです。したがって、累積修正パック、サービスパックまたは製品リリースと同じレベルの品質保証を提供するものではありません。最終的な修正は、次のCFPで提供されます。

