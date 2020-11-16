---
title: モバイルデバイス用のページのオーサリング
seo-title: モバイルデバイス用のページのオーサリング
description: モバイル用にオーサリングするときは、複数のエミュレーターを切り替えて、エンドユーザー向けの表示を見ることができます。
seo-description: モバイル用にオーサリングするときは、複数のエミュレーターを切り替えて、エンドユーザー向けの表示を見ることができます。
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 89%

---


# モバイルデバイス用のページのオーサリング{#authoring-a-page-for-mobile-devices}

モバイルページをオーサリングする場合、ページはモバイルデバイスをエミュレートする方法で表示されます。ページのオーサリング時に、いくつかのエミュレーターを切り替えて、エンドユーザーがページにアクセスしたときの表示を確認できます。

ページをレンダリングするデバイスの機能に従って、デバイスはカテゴリ機能、スマートおよびタッチにグループ分けされます。エンドユーザーがモバイルページにアクセスするときは、AEM はデバイスを検出して、そのデバイスグループに対応する表現を送信します。

>[!NOTE]
>
>既存の標準サイトに基づいたモバイルサイトを作成するには、標準サイトのライブコピーを作成します。(See [Creating a Live Copy for Different Channels](/help/sites-administering/msm-livecopy.md).)
>
>AEM 開発者は、新しいデバイスグループを作成できます。(See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)

次の手順を使用して、モバイルページをオーサリングします。

1. グローバルナビゲーションから&#x200B;**サイト**&#x200B;コンソールを開きます。
1. Open the page **We.Retail** -> **United States** -> **English**.

1. **プレビューモードに切り替えます** 。
1. ページ上部のデバイスアイコンをクリックして、必要なエミュレーターに切り替えます。
1. コンポーネントをコンポーネントブラウザーからページにドラッグ&amp;ドロップします。

ページは次のようになります。

![mobilepademu](assets/mobileipademu.png)

>[!NOTE]
>
>オーサーインスタンスのページがモバイルデバイスから要求されると、エミュレーターは無効になります。

