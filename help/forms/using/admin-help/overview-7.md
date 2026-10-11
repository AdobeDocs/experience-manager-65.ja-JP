---
title: Forms 設定の基本事項
description: インタラクティブなデータ収集アプリケーションの作成に役立つ、様々な Forms サービスについて説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
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
source-wordcount: '200'
ht-degree: 100%
---
# Forms 設定の基本事項 {#basics-of-configuring-forms}

Forms サービスを使用すると、通常は Designer で作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータ収集クライアントアプリケーションを作成できます。 フォーム作成者は、次に示す様々な形式で Forms サービスによってレンダリングされる、単一のフォームデザインを作成します。

* Adobe Reader 内またはブラウザー内の PDF
* XHTML 1.0 に準拠したレンダリングを含む様々なブラウザー環境での HTML
* Adobe Flash Player をサポートする様々なブラウザー環境でのフォームガイド

Forms サービスについて詳しくは、[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

管理コンソールの Forms ページを使用して、Forms サービスの動作を設定できます。 これらの設定はサービスのすべての呼び出しに適用されます。 AEM Forms SDK を通じて送信されたパラメーターは、管理コンソールで指定された設定を上書きします。ただし、影響を受けるのは特定の呼び出しだけです。

管理コンソールで Forms 設定を変更した後で、「保存」をクリックします。 サーバーを再起動しなくても、変更が反映されます。 ただし、キャッシュモード設定を指定すると Forms サービスの停止および再起動が必要な場合があります （[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照）。
