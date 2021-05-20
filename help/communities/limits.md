---
title: メンバーの貢献度の制限
seo-title: メンバーの貢献度の制限
description: スパムから保護するために、貢献度の制限機能を使用して、貢献度を制限できます
seo-description: スパムから保護するために、貢献度の制限機能を使用して、貢献度を制限できます
uuid: 99b2a855-3f0d-41a0-9572-517a7f29af9f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d855aac2-f34d-402f-9dc3-c7ad494b45f2
role: Administrator
exl-id: d00a8eb2-47ce-425a-a312-f043f82912be
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 43%

---

# メンバーの貢献度の制限  {#member-contribution-limits}

## 概要 {#overview}

貢献度の制限機能を使用すると、スパムからの保護手段として、コミュニティメンバーの貢献度を制限できます。

制限されているメンバーが貢献度の許可される数を超えて投稿すると、制限を超えたので、投稿が拒否されたことを伝えるアラートが表示されます。コミュニティメンバーは、コミュニティメッセージセンターに移動し、必要に応じて制限を削除できるコミュニティマネージャーに問い合わせることができます。

貢献度の制限は、[メンバーコンソール](members.md)から個別に有効にすることや、サイト訪問者が新たにメンバーになると自動的に有効になるよう設定することができます。

メンバーコンソールを使用すると、コミュニティマネージャーがメンバーの貢献度の制限を事前に削除したり、メンバーがその要求を行うコミュニティマネージャーにメッセージを送信した場合にリアクティブに削除したりできます。

## AEM Communities ユーザー生成コンテンツの貢献度の制限の設定 {#aem-communities-user-generated-content-contribution-limits-configuration}

次のOSGi設定：

* 貢献度の制限（期間内の投稿数）の特性を定義します。
* 制限に達したときにメッセージを送信できるメンバーを識別します。
* 制限が必要でないドメインを識別します。

この OSGi 設定にアクセスするには、次の手順に従います。

* プライマリパブリッシャーで、次の手順を実行します。
* 管理者権限でサインインします。
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセスします。

   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* `AEM Communities User Generated Content Contribution Limits Configuration`を探します。
* 編集アイコンを選択します。

![configure-limits](assets/configure-limits.png)

* **[!UICONTROL UGC貢献度の制限の自動適用]**

   オンにすると、ユーザーがコミュニティメンバーとして登録する際に、ユーザーに対して貢献度の制限が自動的に設定されます。 これはコミュニティメンバーのプロファイルに反映され、[メンバーコンソール](members.md)で有効/無効にできます。 ドメインのからEメールアドレスを許可リスト持つ新しいメンバーは、制限されません。

   初期設定はオフです。

* **[!UICONTROL UGCの制限]**

   投稿の最大数。

   初期設定は 10 件です。

* **[!UICONTROL UGCの制限の頻度]**

   UGCの制限を制限する期間。

   初期設定は 60 分です。

* **[!UICONTROL ドメイン]**

   1つ以許可リスト上のEメールドメインのリスト。 「+」アイコンを選択して、追加のエントリを作成します。

   ドメインのにEメールアドレ許可リストスを持つユーザーは、UGCの貢献度の制限が自動的に適用されても影響を受けません。 例えば、ドメイン `mycompany.com` がドメインリストに追加されている場合、電子メールアドレスが `me@mycompany.com` のメンバーは投稿の制限を受けません。

   初期設定は空の許可リスト。

* **[!UICONTROL メッセージ受信者]**

   メンバーの貢献度の制限を変更できるメンバーの 1 つ以上の認証可能な ID のリスト。「+」アイコンを選択して、追加のエントリを作成します。

   メンバーは、制限に達した場合にのみ、指定されたメンバーに連絡できます。

   初期設定では、メッセージの受信者はいません。

注意：デフォルトの設定では、1時間以内に10件の投稿に制限されます。
