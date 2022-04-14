---
title: Forms 設定の基本事項
seo-title: Basics of configuring forms
description: インタラクティブなデータキャプチャアプリケーションの作成に役立つ、様々な Forms サービスについて説明します。
seo-description: Learn about the various forms services that help you create interactive data capture applications.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '201'
ht-degree: 100%

---

# Forms 設定の基本事項 {#basics-of-configuring-forms}

Forms サービスを使用すると、通常は Designer で作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。フォーム作成者は、次に示す様々な形式で Forms サービスによってレンダリングされる、単一のフォームデザインを作成します。

* Adobe Reader 内またはブラウザー内の PDF
* XHTML 1.0 に準拠したレンダリングを含む様々なブラウザー環境での HTML
* Adobe Flash Player をサポートする様々なブラウザー環境での form ガイド

Forms サービスについて詳しくは、「[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

管理コンソールの Forms ページを使用して、Forms サービスの動作を設定できます。これらの設定はサービスのすべての呼び出しに適用されます。AEM forms SDK を通じて送信されたパラメーターは、管理コンソールで指定された設定よりも優先されます。ただし、影響を受けるのは特定の呼び出しだけです。

管理コンソールで Forms 設定を変更した後で、「保存」をクリックします。サーバーを再起動しなくても、変更が反映されます。ただし、キャッシュモード設定を指定すると Forms サービスの停止および再起動が必要な場合があります（[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照してください）。
