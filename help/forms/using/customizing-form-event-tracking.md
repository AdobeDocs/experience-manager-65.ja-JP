---
title: フォームのイベント追跡のカスタマイズ
seo-title: フォームのイベント追跡のカスタマイズ
description: ユーザーが 60 秒以上フォームにとどまると、fieldvisit イベントがトリガーされ、フィールドの詳細が Adobe SiteCatalyst に送信されます。
seo-description: ユーザーが 60 秒以上フォームにとどまると、fieldvisit イベントがトリガーされ、フィールドの詳細が Adobe SiteCatalyst に送信されます。
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 77%

---

# フォームのイベント追跡のカスタマイズ  {#customizing-form-event-tracking}

Analytics が有効になっているアダプティブフォームでは次のイベントがデフォルトで追跡されます。

<table>
 <tbody>
  <tr>
   <th>イベント</th>
   <th>使用可能な変数</th>
  </tr>
  <tr>
   <td>render</td>
   <td>formName、formTitle、formInstance、source</td>
  </tr>
  <tr>
   <td>abandon</td>
   <td>formNam、formTitle、formInstance、source</td>
  </tr>
  <tr>
   <td>保存</td>
   <td>formName、formTitle、formInstance、panelName、source</td>
  </tr>
  <tr>
   <td>submit</td>
   <td>formName、formTitle、formInstance、source</td>
  </tr>
  <tr>
   <td>エラー</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle</td>
  </tr>
  <tr>
   <td>help</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle</td>
  </tr>
  <tr>
   <td>fieldVisit</td>
   <td>formName、formTitle、fieldName、fieldTitle、panelTitle<br /> </td>
  </tr>
  <tr>
   <td>panelVisit</td>
   <td>formName、formTitle、panelName、panelTitle</td>
  </tr>
 </tbody>
</table>

## fieldVisit イベントのタイムアウトのカスタマイズ  {#customizing-the-field-visit-event-timeout}

AEM Forms のデフォルト設定では、ユーザーが 60 秒以上フィールドにとどまると、`fieldvisit` イベントがトリガーされ、フィールドの詳細が Adobe Analytics に送信されます。AEM Configuration コンソール（/system/console/configMgr）で、AEM Forms Analytics Configuration の下にある Field time tracking baseline をカスタマイズすると、タイムアウト制限を調整できます。

## 追跡イベントのカスタマイズ  {#customizing-the-tracking-events}

`/libs/afanalytics/js/custom.js`ファイルの`trackEvent`関数を変更して、イベント追跡をカスタマイズできます。 アダプティブフォームで追跡中のイベントが発生すると、`trackEvent` 関数が呼び出されます。`trackEvent`関数は、次の2つのパラメーターを受け取ります。`eventName`と`variableValueMap`が含まれます。

*eventName*&#x200B;引数と&#x200B;*variableValueMap*&#x200B;引数の値を評価して、イベントの追跡動作を変更できます。 例えば、ある一定数のイベントが発生した場合、Analytics サーバーに情報を送信するように指定できます。また、次のカスタマイズを実行できます。

* イベントが送信されるまでのしきい値を設定できます。
* アクションを決定する状態を維持できます。例えば、 *fieldVisit*&#x200B;は、最後のイベントのタイムスタンプに基づいてダミーのイベントをプッシュします。
* `pushEvent` 関数を使用して Analytics サーバーにイベントを送信できます。**

* Analytics サーバーにイベントを一切プッシュしないようにすることもできます。

### サンプル {#sample}

次の例では、各&#x200B;*fieldName*&#x200B;属性の&#x200B;*error*&#x200B;イベントの状態が維持されます。 エラーが再発した場合にのみ、Analytics サーバーにイベントが送信されます。

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## panelVisit イベントのカスタマイズ {#customizing-the-panelvisit-event}

デフォルトの AEM Forms セットアップでは、60 秒ごとに、アダプティブフォームを含むウィンドウがアクティブになっているかどうかがチェックされます。ウィンドウがアクティブな場合、`panelVisit`イベントがAdobe Analyticsに対してトリガーされます。 そうすることで、そのドキュメントまたはフォームがアクティブであることを確認し、対応するフォームまたはドキュメントでの滞在時間を計算できます。

>[!NOTE]
>
>アクティビティの確認と滞在時間の計算に使用されるイベント名は、&quot;panelVisit&quot; です。このイベントは、上記の表に記載されているパネル訪問イベントとは異なります。

`/libs/afanalytics/js/custom.js`ファイル内のscheduleHeartBeatCheck関数を変更して、Adobe Analyticsに送信されるイベントを定期的に変更または停止できます。
