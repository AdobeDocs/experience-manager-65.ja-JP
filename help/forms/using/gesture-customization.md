---
title: ジェスチャーのカスタマイズ
seo-title: ジェスチャーのカスタマイズ
description: AEM Forms アプリケーションでジェスチャーをカスタマイズ
seo-description: AEM Forms アプリケーションでジェスチャーをカスタマイズ
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 39%

---

# ジェスチャーのカスタマイズ {#gesture-customization}

AEM Formsアプリのジェスチャーをカスタマイズして、アプリを操作するための独自の方法を提供できます。 例えば、タスクやStartpointを開く、または閉じるための新しいジェスチャーを追加できます。

## AEM Forms アプリケーションのジェスチャーをカスタマイズするには {#to-customize-gestures-in-aem-forms-app}

AEM Forms アプリケーションで、左スワイプは新しいタスクまたは Startpoint を開き、右スワイプは何もしません。次の例は、AEM Formsアプリで右スワイプジェスチャーを実行したときに新しいタスクまたはStartpointを開く手順を示しています。

1. プロジェクトを開きます。

   * iOSの場合は、Xcodeで`Capture.xcodeproj`を開きます。
   * Android の場合、Eclipse で Android プロジェクトを開きます。
   * Windowsの場合は、Visual Studioで`MWSWindows.sln`を開きます。

1. viewsフォルダーに移動し、編集用に`task.js`ファイルを開きます。

   * Xcodeで、 **Capture > www > wsmobile > js > runtime > views**&#x200B;フォルダーに移動します。
   * Eclipseで、 **assets > www > wsmobile > js > runtime > views**&#x200B;フォルダーに移動します。
   * Visual Studioで、 **MWSWindows > www > wsmobile > js > runtime > views**&#x200B;フォルダーに移動します。

   >[!NOTE]
   >
   >task.js ファイルには、タスクリストまたは Startpoint リストに表示されている各タスクまたは Startpoint に関連付けられた Backbone ビューが含まれています。

1. `task.js`ファイルで、ビューのeventsプロパティを検索します。

   eventsプロパティは、次の形式の各エントリとマップされます。

   `"EventName Selector": "Function"`

   `Selector`で指定されたHTML要素に`EventName`という名前のJavaScriptイベントをトリガーすると、`Function`が呼び出されます。

1. 検索

   * 「tap .taskContentArea」:&quot;onTaskClick&quot;,

      「tap .taskOpenArea」:&quot;onTaskClick&quot;,

      「tap .task-content」:&quot;onTaskClick&quot;,

      &quot;tap .last_empty_div&quot; :&quot;onTaskClick&quot;,
   これを

   * &quot;swipe .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .task-content&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .last_empty_div&quot; :&quot;onTaskClick&quot;,


1. `task.js` ファイルを保存して閉じます。
1. AEM Forms アプリケーションをビルドし実行します。これで、左スワイプと右スワイプを使用してタスクを開くことができます。

同様に、さまざまな組み合わせのジェスチャー、HTML 要素、および関数に対して、他のビューで変更を行うことができます。
