---
title: メンバーの貢献度の制限
description: 貢献度制限機能により、スパムから保護するために貢献度を制限できます
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 1%

---

# メンバーの貢献度の制限 {#member-contribution-limits}

## 概要 {#overview}

貢献度制限機能を使用すると、スパムから保護する手段として、コミュニティメンバーの投稿を制限できます。

メンバーに制限がある場合、投稿が許可されている投稿数を超えると、制限を超えていることを示すアラートが表示され、投稿が拒否されます。 その後、コミュニティ メンバーはコミュニティ メッセージ センターにアクセスし、必要に応じて制限を解除できるコミュニティ マネージャに連絡することができます。

貢献度の制限は、から個別に有効にできます [メンバーコンソール](members.md) サイト訪問者が新しいメンバーになった際に自動的に有効になるように設定されている。

メンバーコンソールを使用すると、コミュニティマネージャーがいつでもメンバーの貢献度制限をプロアクティブに削除したり、メンバーがコミュニティマネージャーにそのようなリクエストを行うメッセージを送信したときにプロアクティブに削除したりできます。

## AEM Communities ユーザー生成コンテンツ貢献度制限の設定 {#aem-communities-user-generated-content-contribution-limits-configuration}

この OSGi 設定は次のとおりです。

* 貢献度制限の特性（期間内の投稿数）を定義します。
* 制限に達したときにメンバーがメッセージを送信できるユーザーを識別します。
* 制約を受ける必要のないドメインを識別します。

この OSGi 設定にアクセスするには：

* プライマリパブリッシャーで：
* 管理者権限でログインします。
* へのアクセス [Web コンソール](../../help/sites-deploying/configuring-osgi.md).

   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* を見つける `AEM Communities User Generated Content Contribution Limits Configuration`.
* 編集アイコンを選択します。

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL UGC 貢献度制限の自動適用]**

  オンにすると、ユーザーがコミュニティメンバーとして登録する際に、そのユーザーの貢献度制限が自動的に設定されます。 これはコミュニティメンバーのプロファイルに反映され、 [メンバーコンソール](members.md). ドメインの許可リストのメールアドレスを持つ新しいメンバーに制限はありません。

  デフォルトではオフになっています。

* **[!UICONTROL UGC 制限]**

  コントリビューションの最大数。

  デフォルトは 10 件の投稿です。

* **[!UICONTROL UGC の制限頻度]**

  UGC 制限を制限する期間。

  デフォルトは 60 分です。

* **[!UICONTROL ドメイン]**

  1 つ以上のメールドメインの許可リストリスト。 追加のエントリを作成するには、「+」アイコンを選択します。

  UGC 貢献度制限が自動適用される場合、ドメインの許可リストにメールアドレスを持つユーザーは影響を受けません。 例えば、次の場合：domain `mycompany.com` がドメインのリストに追加された後、メールアドレスを持つメンバーが `me@mycompany.com` は投稿から制限されません。

  デフォルトは空の許可リストです。

* **[!UICONTROL メッセージ受信者]**

  メンバーの貢献度制限を変更できる、メンバーの 1 つ以上の認証可能な ID のリスト。 追加のエントリを作成するには、「+」アイコンを選択します。

  メンバーは、制限に達した場合にのみ、指定されたメンバーにリーチできます。

  デフォルトでは、メッセージ受信者は存在しません。

注意：デフォルト設定の場合、1 時間で投稿が 10 件までに制限されます。
