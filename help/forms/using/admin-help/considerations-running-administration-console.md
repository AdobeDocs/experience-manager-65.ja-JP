---
title: 管理コンソールを実行する際の考慮事項
description: このドキュメントでは、管理コンソールを実行する際に考慮すべき点をいくつか示します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 11%

---

# 管理コンソールを実行する際の考慮事項 {#considerations-when-running-administrationconsole}

管理コンソールを実行する際には、次の点に注意してください。

* URL `https://[hostname]:'port'/adminui`を指定して管理コンソールにアクセスする場合、指定するホスト名にアンダースコア文字を含めることはできません。そうしないと、管理コンソールの一部の領域へのリンクが正しく機能しない場合があります。
* 日本語 OS 上の Windows エクスプローラーで管理コンソールを実行すると、次の問題が発生する場合があります。

   * リンクをクリックすると、期待したリンクではなく、ログインページに戻ります。
   * リンクをクリックすると、権限エラーが表示されます。

  ベストプラクティスは、Mozilla Firefox などの別のブラウザーから管理コンソールを実行して、リンクが失敗しないようにすることです。

* 管理コンソールで検索を実行する際には、バックスラッシュ文字 () を使用しないでください。
