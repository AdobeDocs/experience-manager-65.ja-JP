---
title: メンバーの貢献度の制限
description: 貢献度制限機能では、迷惑メールから保護するために貢献度を制限できます
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 3%
---
# メンバーの貢献度の制限 {#member-contribution-limits}

## 概要 {#overview}

貢献度制限機能では、スパムから保護する手段として、コミュニティメンバーの貢献度を制限できます。

メンバーが制限されている場合、許可された投稿数を超えた投稿は、制限を超えたことを示すアラートになり、投稿は拒否されます。 その後、コミュニティメンバーはコミュニティメッセージセンターに行き、必要に応じて制限を取り除くことができるコミュニティマネージャーに連絡することができます。

貢献度制限は、[ メンバーコンソール ](members.md)から個別に有効にしたり、サイト訪問者が新しいメンバーになったときに自動的に有効にするように設定したりできます。

メンバーコンソールを使用すると、コミュニティマネージャーがメンバーに対して貢献制限をいつでも積極的に削除したり、メンバーがそのような要求を行う際にコミュニティマネージャーにメッセージを送信すると、事後的に削除したりできます。

## AEM Communitiesのユーザー生成コンテンツ貢献度制限の設定 {#aem-communities-user-generated-content-contribution-limits-configuration}

このOSGi設定：

* 貢献度制限の特性（期間内の投稿数）を定義します。
* 制限に達したときに、メンバーがメッセージを送信できるユーザーを識別します。
* 制約を受けないドメインを特定します。

このOSGi設定に到達するには：

* プライマリ発行者：
* 管理者権限でログインします。
* [Web コンソール ](../../help/sites-deploying/configuring-osgi.md)にアクセスします。

  * 例：[http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* `AEM Communities User Generated Content Contribution Limits Configuration` を見つけます。
* 編集アイコンを選択します。

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL UGC貢献度制限の自動適用]**

  オンにすると、コミュニティメンバーとして登録する際に、ユーザーの貢献度制限が自動的に設定されます。 これはコミュニティメンバーのプロファイルに反映され、[ メンバーコンソール ](members.md)で有効/無効にできます。 ドメインの許可リストからメールアドレスを持つ新しいメンバーは制限されません。

  デフォルトはオフです。

* **[!UICONTROL UGC制限]**

  寄付の上限。

  デフォルトは10件です。

* **[!UICONTROL UGC制限の頻度]**

  UGCの制限を制限する期間。

  デフォルトは60分です。

* **[!UICONTROL ドメイン]**

  1つ以上のメールドメインの許可リストリスト。 「+」アイコンを選択して、追加のエントリを作成します。

  ドメインのドメインにメールアドレスを持つユーザーは、UGCの貢献度制限が自動的に適用されても影響を受けません。 例えば、ドメイン `mycompany.com`がドメインのリストに追加された場合、メールアドレス `me@mycompany.com`を持つメンバーが投稿を制限されることはありません。

  デフォルトは空の許可リストです。

* **[!UICONTROL メッセージ受信者]**

  メンバーの貢献制限を変更できる、1つ以上の承認可能なメンバーのIDのリスト。 「+」アイコンを選択して、追加のエントリを作成します。

  メンバーは、制限に達した場合にのみ、指定されたメンバーに連絡できます。

  デフォルトでは、メッセージ受信者はありません。

注意：デフォルト設定では、1時間以内に投稿は10件までという制限があります。
