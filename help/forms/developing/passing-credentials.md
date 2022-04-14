---
title: WS-security ヘッダーを使用して認証情報を渡す方法は？
description: WS-security ヘッダーを使用して認証情報を渡す方法を学ぶ
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
source-git-commit: de38dbb9d0ce523543c11e665c02034f4b38f1e6
workflow-type: ht
source-wordcount: '219'
ht-degree: 100%

---

# WS-Security ヘッダーを使用した資格情報の受け渡し {#using-execute-script-service-aem-forms-jee-workbench}

Web サービスを使用して JEE サービスで AEM Forms を呼び出す場合、WS-Security ヘッダーを使用して、JEE で AEM Forms に必要なクライアント認証情報を渡すことができます。WS-Security は、クライアント認証、メッセージの機密性、およびメッセージの整合性を実装するための SOAP 拡張機能を定義します。その結果、JEE 上の AEM Forms がスタンドアロンサーバーとして、またはクラスター化された環境内にデプロイされている場合、JEE サービス上で AEM Forms を呼び出すことができます。

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

