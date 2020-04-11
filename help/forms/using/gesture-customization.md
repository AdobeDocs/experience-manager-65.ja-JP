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
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# ジェスチャーのカスタマイズ {#gesture-customization}

AEM Formsアプリケーションのジェスチャーをカスタマイズして、アプリケーションと対話する独自の方法を提供できます。 例えば、新しいジェスチャーを追加して、ジェスチャーまたはスタートポイントを開いたり閉じたりするタスクを追加できます。

## AEM Forms アプリケーションのジェスチャーをカスタマイズするには {#to-customize-gestures-in-aem-forms-app}

AEM Forms アプリケーションで、左スワイプは新しいタスクまたは Startpoint を開き、右スワイプは何もしません。次の例は、AEM Formsアプリケーションで右スワイプジェスチャーを実行したときに新しいタスクまたはStartpointを開く手順を示しています。

1. プロジェクトを開きます。

   * For iOS, open `Capture.xcodeproj` in Xcode
   * Android の場合、Eclipse で Android プロジェクトを開きます。
   * For Windows, open `MWSWindows.sln` in Visual Studio.

1. Navigate to the views folder and open the `task.js` file for editing.

   * In Xcode, navigate to the **Capture > www > wsmobile > js > runtime > views** folder.
   * In Eclipse, navigate to the **assets > www > wsmobile > js > runtime > views** folder.
   * In Visual Studio, navigate to the **MWSWindows > www > wsmobile > js > runtime > views** folder.
   >[!NOTE]
   >
   >task.js ファイルには、タスクリストまたは Startpoint リストに表示されている各タスクまたは Startpoint に関連付けられた Backbone ビューが含まれています。

1. In the `task.js` file, search for the events property of the view.

   イベントプロパティは、次の形式の各エントリを持つマップです。

   `"EventName Selector": "Function"`

   When you trigger a Javascript event named `EventName`on an HTML element specified by `Selector`, the `Function`is called.

1. 検索

   * &quot;tap .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;tap .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;tap .タスク-content&quot; :&quot;onTaskClick&quot;,

      &quot;tap .last_empty_div&quot; :&quot;onTaskClick&quot;,
   これを

   * &quot;swipe .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .タスクコンテンツ&quot;:&quot;onTaskClick&quot;,

      &quot;swipe .last_empty_div&quot; :&quot;onTaskClick&quot;,


1. Save and close the `task.js` file.
1. AEM Forms アプリケーションをビルドし実行します。これで、左スワイプと右スワイプを使用してタスクを開くことができます。

同様に、さまざまな組み合わせのジェスチャー、HTML 要素、および関数に対して、他のビューで変更を行うことができます。
