---
title: モバイルデバイス用のページのオーサリング
seo-title: Authoring a Page for Mobile Devices
description: モバイル用にオーサリングするときは、複数のエミュレーターを切り替えて、エンドユーザー向けの表示を見ることができます。
seo-description: When authoring for mobile, you can switch between several emulators to see what the end-user sees
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 100%

---

# モバイルデバイス用のページのオーサリング {#authoring-a-page-for-mobile-devices}

モバイルページをオーサリングする場合、ページはモバイルデバイスをエミュレートする方法で表示されます。ページのオーサリング時に、いくつかのエミュレーターを切り替えて、エンドユーザーがページにアクセスしたときの表示を確認できます。

ページをレンダリングするデバイスの機能に従って、デバイスはカテゴリ機能、スマートおよびタッチにグループ分けされます。エンドユーザーがモバイルページにアクセスするときは、AEM はデバイスを検出して、そのデバイスグループに対応する表現を送信します。

>[!NOTE]
>
>既存の標準サイトに基づいたモバイルサイトを作成するには、標準サイトのライブコピーを作成します。（[様々なチャネル用のライブコピーを作成する](/help/sites-administering/msm-livecopy.md)を参照）。
>
>AEM 開発者は、新しいデバイスグループを作成できます（「[デバイスグループフィルターの作成](/help/sites-developing/groupfilters.md)」を参照）。

次の手順を使用して、モバイルページをオーサリングします。

1. グローバルナビゲーションから&#x200B;**サイト**&#x200B;コンソールを開きます。
1. **We.Retail**／**アメリカ合衆国**／**英語**&#x200B;のページを開きます。

1. **プレビュー**&#x200B;モードに切り替えます。
1. ページ上部のデバイスアイコンをクリックして、必要なエミュレーターに切り替えます。
1. コンポーネントをコンポーネントブラウザーからページにドラッグ&amp;ドロップします。

ページは次のようになります。

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>モバイルデバイスからオーサーインスタンスのページが要求されると、エミュレーターは無効になります。
