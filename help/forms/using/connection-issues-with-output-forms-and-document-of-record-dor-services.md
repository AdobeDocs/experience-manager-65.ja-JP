---
title: Output、Forms、および（レコードのドキュメント）DoR サービスとの接続の問題
description: SP19 以降のAEM Forms接続エラーを解決します。 シームレスなソリューションのために、Microsoft Visual C++を停止してインストールし、サーバーを再起動します。 Output、Forms、DoR サービスのトラブルシューティング。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
exl-id: bd58099c-08cd-4056-afb6-a5935454429a
source-git-commit: 15d85c48727cfcb7cb1f9de4da5dad9df674c0bd
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 1%

---

# Output サービス、Formsサービス、またはレコードのドキュメント (DoR) サービスを使用できません {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## 問題

AEM Forms 6.5 Service Pack 19 をインストールした後、Output サービス、Formsサービスまたはレコードのドキュメント (DoR) サービスを使用しようとすると、 `Connection to failed service` エラー。

## 解決策

問題を解決するには：

1. AEM 6.5 Formsインスタンスを停止します。
1. をダウンロードしてインストールする [Visual Studio 2015、2017、2019、2022 用の 64 ビット版のMicrosoft Visual C++再頒布可能パッケージ](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) AEM 6.5 Formsがインストールされているコンピューター上。
1. AEM Formsサーバーを再起動します。


>[!NOTE]
>
>
> 以前のバージョンがインストールされている場合でも、再配布可能パッケージをインストールしてください。