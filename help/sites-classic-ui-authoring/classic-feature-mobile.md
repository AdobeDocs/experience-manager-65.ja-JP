---
title: 'モバイルデバイス用のページのオーサリング '
seo-title: Authoring a Page for Mobile Devices
description: モバイルページをオーサリングする場合、ページはモバイルデバイスをエミュレートする方法で表示されます。ページのオーサリング時に、いくつかのエミュレーターを切り替えて、エンドユーザーがページにアクセスしたときの表示を確認できます。
seo-description: When authoring a mobile page, the page is displayed in a way that emulates the mobile device. When authoring the page, you can switch between several emulators to see what the end-user sees when accessing the page.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 100%

---

# モバイルデバイス用のページのオーサリング {#authoring-a-page-for-mobile-devices}

モバイルページをオーサリングする場合、ページはモバイルデバイスをエミュレートする方法で表示されます。ページのオーサリング時に、いくつかのエミュレーターを切り替えて、エンドユーザーがページにアクセスしたときの表示を確認できます。

ページをレンダリングするデバイスの機能に従って、デバイスはカテゴリ機能、スマートおよびタッチにグループ分けされます。エンドユーザーがモバイルページにアクセスするときは、AEM はデバイスを検出して、そのデバイスグループに対応する表現を送信します。

>[!NOTE]
>
>既存の標準サイトに基づいたモバイルサイトを作成するには、標準サイトのライブコピーを作成します。（[様々なチャネル用のライブコピーを作成する](/help/sites-administering/msm-livecopy.md)を参照）。
>
>AEM 開発者は、新しいデバイスグループを作成できます（[デバイスグループフィルターの作成](/help/sites-developing/groupfilters.md)を参照してください）。

次の手順を使用して、モバイルページをオーサリングします。

1. ブラウザーで、**サイト管理者コンソール**&#x200B;に移動します。
1. **Web サイト**／**Geometrixx モバイルデモサイト**／**日本語**&#x200B;の下の&#x200B;**製品**&#x200B;ページを開きます。

1. 別のエミュレーターに切り替えます。それには、次のいずれかを行います。

   * ページの上部にあるデバイスアイコンをクリックします。
   * **サイドキック**&#x200B;の「**編集**」ボタンをクリックし、ドロップダウンメニューでデバイスを選択します。

1. **テキストと画像**&#x200B;コンポーネントを、サイドキックの「モバイル」タブからページにドラッグ＆ドロップします。
1. コンポーネントを編集し、テキストを追加します。「**OK**」をクリックして、変更を保存します。

ページは以下のようになります。

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>オーサーインスタンスのページがモバイルデバイスから要求されると、エミュレーターは無効になります。その後、タッチ操作向け UI を使用してオーサリングを行うことができます。
