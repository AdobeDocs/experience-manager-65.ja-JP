---
title: 今日のお知らせの設定
seo-title: Setting the message of the day
description: 今日のメッセージを使用すると、Workspace ユーザーインターフェイスのようこそページに表示するメッセージを設定できます。
seo-description: The message of the day let you set a message to be displayed on the Welcome page in the Workspace user interface.
uuid: 9c664438-6fc0-498e-bb3f-4c6bcb9414a7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c2b3a412-70c2-4257-bfb4-1430bb1f8891
exl-id: d8bab1c4-b830-4491-9486-d7e7f4dc2c99
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 27%

---

# 今日のお知らせの設定 {#setting-the-message-of-the-day}

Workspace ユーザーインターフェイスのようこそページに表示するメッセージを設定できます。

必要に応じて、AdobeFlash® Player でサポートされているHTMLタグを使用して、テキストの外観を書式設定できます。

* &lt;a> アンカータグ
* &lt;b> 太字タグ
* &lt;br> タグを解除
* &lt;font> フォントタグ
* &lt;img> 画像タグ
* &lt;i> 斜体タグ
* &lt;li> リスト項目タグ
* &lt;p> 段落タグ
* &lt;span> スパンタグ
* &lt;textformat> テキスト形式タグ
* &lt;u> タグに下線を引く

サポートされているタグについて詳しくは、[Flex Language Reference](https://flex.apache.org/) の TextField クラスの `htmlText` ロパティの定義を参照してください。

## 今日のメッセージを設定 {#set-the-message-of-the-day}

1. 管理コンソールで、サービス/Workspace/今日のメッセージをクリックします。
1. 「今日のメッセージ」ボックスに、ようこそ画面に表示するテキストを入力します。
1. 「保存」をクリックします。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。
