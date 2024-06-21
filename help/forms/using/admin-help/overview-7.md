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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 100%

---

# Forms 設定の基本事項 {#basics-of-configuring-forms}

Forms サービスを使用すると、通常は Designer で作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータ収集クライアントアプリケーションを作成できます。フォーム作成者は、次に示す様々な形式で Forms サービスによってレンダリングされる、単一のフォームデザインを作成します。

* Adobe Reader 内またはブラウザー内の PDF
* XHTML 1.0 に準拠したレンダリングを含む様々なブラウザー環境での HTML
* Adobe Flash Player をサポートする様々なブラウザー環境でのフォームガイド

Forms サービスについて詳しくは、[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

管理コンソールの Forms ページを使用して、Forms サービスの動作を設定できます。これらの設定はサービスのすべての呼び出しに適用されます。AEM Forms SDK を通じて送信されたパラメーターは、管理コンソールで指定された設定よりも優先されます。ただし、影響を受けるのは特定の呼び出しだけです。

管理コンソールで Forms 設定を変更した後で、「保存」をクリックします。サーバーを再起動しなくても、変更が反映されます。ただし、キャッシュモード設定を指定すると Forms サービスの停止および再起動が必要な場合があります（[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照）。
