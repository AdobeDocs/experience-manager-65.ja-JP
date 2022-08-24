---
title: エラーログの非推奨 API に関するエラーメッセージ
description: エラーログの非推奨 API に関するエラーメッセージ
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 8%

---


# エラーログの非推奨 API に関するエラーメッセージ {#error-messages-about-deprecated-apis-in-error-logs}

この問題は、次のバージョンに適用されます。

* Experience Manager6.5 Forms

## 問題 {#issue}

* 次のエラーメッセージが error.log ファイルに表示されます。
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details`（NPR-38282）

## 解像度 {#workaround}

1. インストール [Experience Manager Forms Service Pack 13 以降 (6.5.13.0以降 )](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=ja)
1. 次のリンクを使用して、ソフトウェア配布からパッケージ（解像度の指定された.jar ファイル）をダウンロードします。

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]pack/com.adobe

1. Experience Managerの設定マネージャーを開き、ダウンロードした com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar ファイルをインストールします。

問題が解決しました。