---
title: WS-Security ヘッダーを使用した資格情報の受け渡し
description: WS-security ヘッダーを使用して資格情報を渡す方法を学ぶ
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 100%
---
# WS-Security ヘッダーを使用した資格情報の受け渡し {#using-execute-script-service-aem-forms-jee-workbench}

Web サービスを使用して JEE 上の AEM Forms サービスを呼び出す場合、WS-Security ヘッダーを使用して、JEE 上の AEM Forms に必要なクライアント認証情報を渡すことができます。 WS-Security は、クライアント認証、メッセージの機密性、およびメッセージの整合性を実装するための SOAP 拡張機能を定義します。 その結果、JEE 上の AEM Forms がスタンドアロンサーバーとして、またはクラスター化された環境内にデプロイされている場合、JEE サービス上で AEM Forms を呼び出すことができます。

WS-Security ヘッダーを JEE 上の AEM Forms に渡す方法は、Axis で生成された Java クラスを使用しているか、サービスのネイティブ SOAP スタックを使用する .NET クライアントアセンブリを使用しているかによって異なります。

>[!NOTE]
>
>WS-Security ヘッダーを使用してサービスを呼び出す例として、このトピックでは、暗号化サービスを呼び出すことにより、パスワードを使用して PDF ドキュメントを暗号化します。

ここでは、以下のトピックについて説明します。

* Axisで生成された Java クラスを使用してクライアント認証を渡す

* 暗号化サービスを呼び出すために必要な Axis ライブラリファイルの生成

* WS-Security ヘッダーを使用した暗号化サービスの呼び出し

* .NET クライアントアセンブリを使用してクライアント認証を渡す

* WS-Security ヘッダーを使用した暗号化サービスの呼び出し


## 要件 {#requirements}

このドキュメントを最大限に活用するには、JEE ソフトウェア上の AEM Forms についてよく理解する必要があります。

>[!MORELIKETHIS]
>
>* [WS-Security ヘッダーを使用して資格情報を渡す](assets/passing-credentials-using-ws-security-headers.pdf)
