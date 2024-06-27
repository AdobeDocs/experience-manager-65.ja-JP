---
title: Output、Forms および DoR（レコードのドキュメント）サービスとの接続の問題
description: SP19 以降の AEM Forms 接続エラーを解決します。シームレスな解決策として、サーバーを停止し、Microsoft Visual C++ をインストールし、サーバーを再起動します。Output、Forms、DoR サービスのトラブルシューティングをします。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
exl-id: bd58099c-08cd-4056-afb6-a5935454429a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '168'
ht-degree: 100%

---

# Output サービス、Forms サービスまたは DoR（レコードのドキュメント）サービスを使用できない {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## 問題

AEM Forms 6.5 サービスパック 19 をインストールした後、Output サービス、Forms サービスまたは DoR（レコードのドキュメント）サービスを使用しようとすると、`Connection to failed service` エラーが発生することがあります。

## 解決策

この問題を解決するには、次の手順に従います。

1. AEM 6.5 Forms インスタンスを停止します。
1. AEM 6.5 Forms がインストールされているコンピューターに、[Visual Studio 2015、2017、2019、2022 用の 64 ビット版の Microsoft Visual C++ 再頒布可能パッケージ](https://learn.microsoft.com/ja-jp/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)をダウンロードしてインストールします。
1. AEM Forms サーバーを再起動します。

   >[!NOTE]
   >
   > SDK を再起動するには、「Ctrl + C」コマンドを使用することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。


>[!NOTE]
>
>
> 以前のバージョンがインストールされている場合でも、再頒布可能パッケージをインストールします。
