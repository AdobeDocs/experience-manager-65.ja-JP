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
translation-type: tm+mt
source-git-commit: e4456e80059479ca874681e20f8546f29ac92597

---


# メンバーの貢献度の制限 {#member-contribution-limits}

## 概要 {#overview}

貢献度の制限機能を使用すると、スパムからの保護手段として、コミュニティメンバーの貢献度を制限できます。

制限されているメンバーが貢献度の許可される数を超えて投稿すると、制限を超えたので、投稿が拒否されたことを伝えるアラートが表示されます。コミュニティのメンバーは、コミュニティメッセージセンターに行き、必要に応じて制限を解除できるコミュニティマネージャーに問い合わせることができます。

貢献度の制限は、[メンバーコンソール](members.md)から個別に有効にすることや、サイト訪問者が新たにメンバーになると自動的に有効になるよう設定することができます。

メンバーコンソールを使用すると、コミュニティマネージャーがメンバーに対して貢献度の制限を事前に削除したり、メンバーがリクエストを行ったコミュニティマネージャーにメッセージを送信する際に、貢献度の制限を再度削除したりできます。

## AEM Communities ユーザー生成コンテンツの貢献度の制限の設定 {#aem-communities-user-generated-content-contribution-limits-configuration}

次のOSGi設定：

* 貢献度の制限（期間内の投稿数）の特性を定義します。
* 制限に達した場合に、メンバーが誰にメッセージを送信できるかを識別します。
* 制限を必要としないドメインを識別します。

この OSGi 設定にアクセスするには、次の手順に従います。

* プライマリパブリッシャ：
* 管理者権限でサインインします。
* Access the [Web Console](../../help/sites-deploying/configuring-osgi.md).

   * For example, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)

* Locate `AEM Communities User Generated Content Contribution Limits Configuration`.
* 編集アイコンを選択します。

![chlimage_1-127](assets/chlimage_1-127.png)

* **[!UICONTROL UGC貢献度制限の自動適用]**

   このオプションを選択すると、コミュニティメンバーとして登録する際に、ユーザーに対して貢献度の制限が自動的に設定されます。 This is reflected in the community member&#39;s profile and may be enabled/disabled from the [members console](members.md). ホワイトリストに記載されたドメインの電子メールアドレスを持つ新しいメンバーは、制限されません。

   初期設定はオフです。

* **[!UICONTROL UGCの制限]**

   貢献の最大数。

   初期設定は 10 件です。

* **[!UICONTROL UGC制限頻度]**

   UGC制限を制限する期間。

   初期設定は 60 分です。

* **[!UICONTROL ドメイン]**

   1 つ以上の電子メールドメインのホワイトリスト。+アイコンを選択して、追加のエントリを作成します。

   電子メールアドレスのドメインがホワイトリストに登録されているユーザーに UGC の貢献度の制限が自動的に適用されることはありません。例えば、ドメイン `mycompany.com` がドメインリストに追加されている場合、電子メールアドレスが `me@mycompany.com` のメンバーは投稿の制限を受けません。

   初期設定では、ホワイトリストは空です。

* **[!UICONTROL メッセージ受信者]**

   メンバーの貢献度の制限を変更できるメンバーの 1 つ以上の認証可能な ID のリスト。+アイコンを選択して、追加のエントリを作成します。

   メンバーは、制限に達した場合にのみ、指定されたメンバーに連絡できます。

   初期設定では、メッセージの受信者はいません。

注意：デフォルトの設定では、1時間の間に10件の投稿が制限されます。
