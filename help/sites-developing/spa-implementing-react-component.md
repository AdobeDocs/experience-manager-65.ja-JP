---
title: SPA への React コンポーネントの実装
description: この記事では、Adobe Experience Manager（AEM）SPA Editor で動作するように既存のシンプルな React コンポーネントを適応させる方法の例を示します。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: ht
source-wordcount: '523'
ht-degree: 100%

---


# SPA への React コンポーネントの実装 {#implementing-a-react-component-for-spa}

単一ページアプリケーション（SPA）により、web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを Adobe Experience Manager（AEM）内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、AEM SPA Editor で動作するように既存のシンプルな React コンポーネントを適応させる方法の例を示します。

{{ue-over-spa}}

## はじめに {#introduction}

AEM によって要求され、AEM と SPA Editor の間で確立されたシンプルで軽量な契約により、既存の JavaScript アプリケーションを使用して AEM で SPA と共に使用するよう手順は非常に簡単です。

本記事では、We.Retail Journal のサンプル SPA に天気予報のコンポーネントを搭載した例を紹介します。

この記事を読む前に、[AEM の SPA アプリケーション](/help/sites-developing/spa-getting-started-react.md)の構造について知っておく必要があります。

>[!CAUTION]
>このドキュメントでは、[We.Retail Journal アプリ](https://github.com/adobe/aem-sample-we-retail-journal)をデモ目的でのみ使用します。どのプロジェクト作業にも使用しないでください。
>
>AEM プロジェクトでは、[AEM プロジェクトアーキタイプ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=ja)を活用します。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を活用します。

## 天気予報コンポーネント {#the-weather-component}

天気予報コンポーネントは、We.Retail ジャーナルアプリケーションの左上にあります。気象データを動的に取得し、定義された場所の現在の天気を表示します。

### Weather Widget の使用 {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

SPA エディターで SPA のコンテンツをオーサリングする際、天気予報コンポーネントは他の AEM コンポーネントと同様に表示され、ツールバーも完備しており、編集可能です。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

市区町村は、他の AEM コンポーネントと同様に、ダイアログで更新できます。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

変更が保持され、コンポーネント自体は新しい天気データを使用して自動的に更新されます。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 天気予報コンポーネントの実装 {#weather-component-implementation}

天気コンポーネントは、[React Open Weather](https://www.npmjs.com/package/react-open-weather) と呼ばれる、公開されている React コンポーネントに基づいています。これは、We.Retail ジャーナルサンプル SPA アプリケーション内でコンポーネントとして機能するように適応されています。

React Open Weather コンポーネントの使用に関する NPM ドキュメントのスニペットを以下に示します。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

We.Retail ジャーナルアプリケーションでカスタマイズされた天気予報コンポーネント（`Weather.js`）のコードを確認します。

* **16 行目**：React Open Weather ウィジェットは、必要に応じて読み込まれます。
* **46 行目**：この `MapTo` 関数は、この React コンポーネントを SPA エディターで編集できるように、対応する AEM コンポーネントに関連付けます。

* **22 ～ 29 行目**：この `EditConfig` が定義され、市区町村が設定されているかどうかを確認し、空の場合は値を定義します。

* **31 ～ 44 行目**：天気予報コンポーネントは、`Component` クラスを拡張し、React Open Weather コンポーネントの NPM 使用に関するドキュメントで定義されている必要なデータを提供し、コンポーネントをレンダリングします。

```javascript
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

バックエンドコンポーネントが既に存在している必要がありますが、フロントエンドデベロッパーは、コーディングをほとんど行わずに We.Retail ジャーナル SPA の React Open Weather コンポーネントを使用できます。

## 次のステップ {#next-step}

AEM の SPA 開発について詳しくは、[AEM の SPAの開発](/help/sites-developing/spa-architecture.md)の記事を参照してください。
