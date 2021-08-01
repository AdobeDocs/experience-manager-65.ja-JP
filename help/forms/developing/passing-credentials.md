---
title: WS-securityヘッダーを使用して資格情報を渡す方法を教えてください。
description: WS-securityヘッダーを使用して資格情報を渡す方法を説明します
source-git-commit: 9b118ef4f852e3df1e717bb27b9be272caeb0456
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# WS-Securityヘッダーを使用して資格情報を渡す {#using-execute-script-service-aem-forms-jee-workbench}

Webサービスを使用してJEE上のAEM Formsサービスを呼び出す場合、WS-Securityヘッダーを使用して、JEE上のAEM Formsで必要なクライアント認証情報を渡すことができます。 WS-Securityは、クライアント認証、メッセージの機密性、およびメッセージの整合性を実装するSOAP拡張を定義します。 その結果、JEE上のAEM Formsをスタンドアロンサーバーとしてデプロイする場合や、クラスター環境内にデプロイする場合に、JEE上のAEM Formsサービスを呼び出すことができます。

WS-SecurityヘッダーをJEE上のAEM Formsに渡す方法は、Axisで生成されたJavaクラスを使用しているか、サービスのネイティブSOAPスタックを使用している.NETクライアントアセンブリを使用しているかによって異なります。

>[!NOTE]
>
>WS-Securityヘッダーを使用してサービスを呼び出す例として、このトピックでは、Encryptionサービスを呼び出してPDFドキュメントをパスワードで暗号化します。

このドキュメントでは、次のトピックについて説明します。

* Axis生成Javaクラスを使用したクライアント認証を渡す

* Encryptionサービスを呼び出すために必要なAxisライブラリファイルを生成しています

* WS-Securityヘッダーを使用したEncryptionサービスの呼び出し

* .NETクライアントアセンブリを使用してクライアント認証を渡す

* WS-Securityヘッダーを使用したEncryptionサービスの呼び出し


## 要件 {#requirements}

このドキュメントを最大限に活用するには、JEE上のAEM Formsソフトウェアについて確実に理解する必要があります。

>[!MORELIKETHIS]
>
>* [WS-Securityヘッダーを使用して資格情報を渡す](assets/passing-credentials-using-ws-security-headers.pdf)


