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
source-git-commit: b827c8acb1db158060d209c819fc72ffbfeca65f

---


# AEM Updateリリースの車両定義{#update-release-vehicle-definitions}

このドキュメントでは、アドビから提供される完全リリース、機能パック、サービスパックなど、Adobe Experience Manager（AEM）の各種リリースについて詳しく説明します。

>[!N注]
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
     <li>メジャーリリースのバージョン番号は、X+1.Y.Zという式に基づいて増加します。 </li>
     <li>マイナーリリースのバージョン番号は、X.Y+1.Z という式に基づいて大きくなります。</li>
    </ul> <p>ここで、Xはプライマリバージョン番号、Yはセカンダリバージョン番号、Zはパッチ番号です。</p> </td>
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
     <li>WebサイトのライセンスおよびManaged ServicesライセンスWebサイトから利用可能</li>
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
     <li>インストール後、X.Y.Z.SPxの式に基づいて、インストール済みのリリース番号パッチ桁を増やします。</li>
     <li>ここで、Xはプライマリバージョン番号、Yはセカンダリバージョン番号、Zはパッチ番号です。 x はサービスパック番号です。</li>
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
   <td><p>X.Y.Z.CFPx</p> <p>ここで、Xはプライマリバージョン番号、Yはセカンダリバージョン番号、Zはパッチ番号です。 x は累積サービスパック番号です。</p> </td>
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
   <td>四分の一</td>
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

## Oak 累積修正パック {#oak-cumulative-fix-pack}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td>
    <ul>
     <li>標準の CFP に似ていますが、Oak 関連の修正のみが含まれています。</li>
     <li>COFP は他に依存しません（依存関係なし）。ユーザーは依存関係の検索や解決を気にする必要はありません。[1]</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>oak &lt;version&gt;</td>
  </tr>
  <tr>
   <td><strong>含まれるもの</strong></td>
   <td>COFP は、特定の 1.x バージョンに関するすべての Oak コンポーネントの修正を含む、累積修正パックです。例えば、COHF 1.x.3 を適用する場合、COHF 1.x.3 = COHF 1.x.1 + COHF 1.x.2 です。</td>
  </tr>
  <tr>
   <td><strong>ドキュメント</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>タイミング</strong></td>
   <td><p>必要に応じて</p> </td>
  </tr>
  <tr>
   <td><strong>入手可能性とインストール</strong></td>
   <td>
    <ul>
     <li>エクスペリエンスを向上させるために、COFP のインストールプロセスが単純化されました（すべてのコンポーネントに対して 1 つのパッケージをインストールするだけです）。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>テストのレベル</strong></td>
   <td><p>QA 検証済み</p> </td>
  </tr>
 </tbody>
</table>

## ホットフィックス {#hot-fix}

<table>
 <tbody>
  <tr>
   <td><strong>定義</strong></td>
   <td><p>不可欠なサービスの品質を大幅に低下させたり、業務活動に大きな影響を与えたりする製品の欠陥を解決するために作成された、1 つ以上のファイルを含むパッケージ。 </p> </td>
  </tr>
  <tr>
   <td><strong>命名</strong></td>
   <td>cq-&lt;Release Version&gt;-hotfix-&lt;hotfix ID&gt;-&lt;hotfix version&gt;</td>
  </tr>
  <tr>
   <td><strong>含まれるもの</strong></td>
   <td>特定の問題に対する修正を含みます。</td>
  </tr>
  <tr>
   <td><strong>ドキュメント</strong></td>
   <td>公開ホットフィックスのリリースノートは、AEM サポートポータルを通じた顧客からのリクエストに基づいてのみ入手可能です。</td>
  </tr>
  <tr>
   <td><strong>タイミング</strong></td>
   <td>必要に応じて</td>
  </tr>
  <tr>
   <td><strong>入手可能性とインストール</strong></td>
   <td>
    <ul>
     <li>パッケージとして提供</li>
     <li>パッケージ共有で入手可能</li>
     <li>リリースされている最新のサービスパックに依存</li>
     <li>大部分のホットフィックスは、特に指定がない限り、スタンドアロンです。どのような順序でもインストールできます。依存関係要素の「パッケージ共有の詳細」タブから確認できます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>テストのレベル</strong></td>
   <td>
    <ul>
     <li>カスタマーケアによって検証済み</li>
     <li>AEM のホットフィックスには、サービスパックや製品リリースと同じレベルの品質保証がありません。したがって、高品質なデプロイメントプロセスの一環として、まずステージング環境で検証する必要があります。</li>
    </ul> </td>
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
     <li>サービスパックやフルリリースには必ずしも含まれていない</li>
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
     <li>機能パックはアドオン機能であり、サービスパックを通じて提供されます。AEMバージョンが最後のService packをリリースしている場合、アドビは将来その機能パックを提供しません。</li>
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

* [1]:OAKの修正は、個々のホットフィックスとして提供されません。 しかし、以降の累積 Oak ホットフィックスに含まれます。必要に応じて、最新の COFP 上で診断ビルドを利用できます。前提条件は、最新の COFP を実行していることです。診断ビルドは、ホットフィックスと同じレベルの品質保証を提供するだけです。したがって、累積修正パック、サービスパックまたは製品リリースと同じレベルの品質保証を提供するものではありません。最終修正は次のCFPで提供されます。

