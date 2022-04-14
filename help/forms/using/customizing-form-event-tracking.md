---
title: フォームのイベント追跡のカスタマイズ
seo-title: Customizing form event tracking
description: ユーザーが 60 秒以上フォームにとどまると、fieldvisit イベントがトリガーされ、フィールドの詳細が Adobe SiteCatalyst に送信されます。
seo-description: If a user spends more than 60 seconds on a field, a fieldvisit event is triggered and the details of the field are sent to Adobe SiteCatalyst.
uuid: 2f790085-2f1a-45be-9a69-6100c76dcae0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 60d67c6b-5994-42ef-b159-ed6edf5cf9d4
exl-id: d0280a15-5d0d-49cf-bce9-ad1c40530eae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '446'
ht-degree: 100%

---

# フォームのイベント追跡のカスタマイズ {#customizing-form-event-tracking}

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
   <td>formName、formTitle、formInstance、panelName、panelTitle</td>
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

## fieldVisit イベントのタイムアウトのカスタマイズ {#customizing-the-field-visit-event-timeout}

AEM Forms のデフォルト設定では、ユーザーが 60 秒以上フィールドにとどまると、`fieldvisit` イベントがトリガーされ、フィールドの詳細が Adobe Analytics に送信されます。AEM Configuration コンソール（/system/console/configMgr）で、AEM Forms Analytics Configuration の下にある Field time tracking baseline をカスタマイズすると、タイムアウト制限を調整できます。

## 追跡イベントのカスタマイズ {#customizing-the-tracking-events}

`/libs/afanalytics/js/custom.js` ファイルの `trackEvent` 関数を変更すると、イベント追跡をカスタマイズできます。アダプティブフォームで追跡中のイベントが発生すると、`trackEvent` 関数が呼び出されます。`trackEvent` 関数は 2 つのパラメーター（`eventName` および `variableValueMap`）を受け取ります。

*eventName* および *variableValueMap* 引数の値を評価して、イベントの追跡動作を変更できます。例えば、ある一定数のイベントが発生した場合、Analytics サーバーに情報を送信するように指定できます。また、次のカスタマイズを実行できます。

* イベントが送信されるまでのしきい値を設定できます。
* アクションを決定する状態を維持できます。例えば、*fieldVisit* は、最後のイベントのタイムスタンプに基づいてダミーのイベントをプッシュします。
* `pushEvent` 関数を使用して Analytics サーバーにイベントを送信できます。**

* Analytics サーバーにイベントを一切プッシュしないようにすることもできます。

### サンプル {#sample}

以下の例では、各 *fieldName* 属性の *error* イベントの状態が維持されています。エラーが再発した場合にのみ、Analytics サーバーにイベントが送信されます。

```javascript
case 'error':
        if(errorOccurred[variableValueMap.fieldName] == true) {
            pushEvent(eventName, variableValueMap)
        }
        errorOccurred[variableValueMap.fieldName] = true;
        break;
```

## panelVisit イベントのカスタマイズ {#customizing-the-panelvisit-event}

デフォルトの AEM Forms セットアップでは、60 秒ごとに、アダプティブフォームを含むウィンドウがアクティブになっているかどうかがチェックされます。ウィンドウがアクティブであれば、`panelVisit` イベントが Adobe Analytics に対してトリガされます。そうすることで、そのドキュメントまたはフォームがアクティブであることを確認し、対応するフォームまたはドキュメントでの滞在時間を計算できます。

>[!NOTE]
>
>アクティビティの確認と滞在時間の計算に使用されるイベント名は、&quot;panelVisit&quot; です。このイベントは、上記の表に記載されているパネル訪問イベントとは異なります。

`/libs/afanalytics/js/custom.js` ファイルで提供されている scheduleHeartBeatCheck 関数を変更して、定期的に Adobe Analytics に送信されるこのイベントを変更または停止できます。
