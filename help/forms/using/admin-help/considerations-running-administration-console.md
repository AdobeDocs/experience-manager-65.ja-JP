---
title: 管理コンソール実行時の考慮事項
seo-title: Considerations when running AdministrationConsole
description: 管理コンソール実行時のいくつかの考慮事項について説明します。
seo-description: This document lists a few points to consider when running Administration Console.
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '130'
ht-degree: 100%

---

# 管理コンソール実行時の考慮事項 {#considerations-when-running-administrationconsole}

管理コンソールの実行時には、以下のことを考慮してください。

* URL `https://[hostname]:'port'/adminui`を指定して管理コンソールにアクセスする場合、指定するホスト名にアンダースコア文字を含めることはできません。アンダースコア文字を含めると、管理コンソールの一部の領域へのリンクが正しく機能しない場合があります。
* 日本語の OS 上の Windows エクスプローラーで管理コンソールを実行すると、次の問題が発生することがあります。

   * リンクをクリックすると、予期するリンクではなく、ログインページに戻る。
   * リンクをクリックすると、アクセス権エラーが表示される。

   ベストプラクティスとしては、Mozilla Firefox などの別のブラウザーから管理コンソールを実行し、リンクの失敗がないことを確認します。

* 管理コンソールで検索を実行するときはバックスラッシュ文字（）を使用しないでください。
