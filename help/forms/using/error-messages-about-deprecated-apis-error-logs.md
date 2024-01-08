---
title: エラーログにある非推奨 API に関するエラーメッセージ
description: エラーログにある非推奨 API に関するエラーメッセージ
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 100%

---


# エラーログにある非推奨 API に関するエラーメッセージ {#error-messages-about-deprecated-apis-in-error-logs}

この問題は、以下のバージョンに該当します。

* Experience Manager 6.5 Forms

## 問題 {#issue}

* 次のエラーメッセージが error.log ファイルに表示されます。
  ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details`（NPR-38282）

## 解決方法 {#workaround}

1. [Experience Manager Forms サービスパック 13 以降（6.5.13.0以降）](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=ja)をインストールします。
1. 次のリンクを使用して、ソフトウェア配布からパッケージ（解決法を伴った .jar ファイル）をダウンロードします。

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[…]pack/com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar

1. Experience Manager の設定マネージャーを開き、ダウンロードした com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar ファイルをインストールします。

問題が解決しました。