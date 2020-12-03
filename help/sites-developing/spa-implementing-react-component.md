---
title: SPA用のReactコンポーネントの実装
seo-title: SPA用のReactコンポーネントの実装
description: この記事では、AEM SPAエディタでシンプルで既存のReactコンポーネントを適用する方法の例を紹介します。
seo-description: この記事では、AEM SPAエディタでシンプルで既存のReactコンポーネントを適用する方法の例を紹介します。
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 16%

---


# SPA用のReactコンポーネントの実装{#implementing-a-react-component-for-spa}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、AEM SPAエディタでシンプルで既存のReactコンポーネントを適用する方法の例を紹介します。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## 概要 {#introduction}

AEMが必要とし、SPAとSPAエディタの間で確立するシンプルで軽量な契約のおかげで、AEMのSPAでの使用に合わせて既存のJavaScriptアプリケーションを使用し、適応させるのは簡単です。

この記事では、Web.RetailジャーナルサンプルSPAの天気コンポーネントの例を説明します。

この記事を読む前に、AEM](/help/sites-developing/spa-getting-started-react.md)のSPAアプリケーションの[構造を理解しておく必要があります。

>[!CAUTION]
>このドキュメントでは、[We.Retailジャーナルアプリ](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)は、デモ目的でのみ使用します。 どのプロジェクト作業にも使用しないでください。
>
>AEM プロジェクトでは、 [AEM プロジェクトアーキタイプ](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/developing/archetype/overview.html)を活用します。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を活用します。

## 気象コンポーネント{#the-weather-component}

気象コンポーネントは、We.Retailジャーナルアプリの左上にあります。 定義した場所の現在の天気が表示され、気象データが動的に引き出されます。

### Weatherウィジェットの使用{#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

SPA EditorでSPAのコンテンツをオーサリングする場合、気象コンポーネントは他のAEMコンポーネントと同様に表示され、ツールバーと共に完成し、編集可能です。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

他のAEMコンポーネントと同様に、ダイアログで都市を更新できます。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

この変更は維持され、コンポーネントは新しい気象データで自動的に更新されます。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 気象コンポーネントの実装{#weather-component-implementation}

天気コンポーネントは、実際には、We.RetailジャーナルサンプルSPAアプリケーション内のコンポーネントとして機能するように設計された、[React Open Weather](https://www.npmjs.com/package/react-open-weather)と呼ばれる、一般に利用可能なReactコンポーネントに基づいています。

以下は、React Open Weatherコンポーネントの使用に関するNPMドキュメントのスニペットです。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

We.Retailジャーナルアプリケーションで、カスタマイズした天気コンポーネント(`Weather.js`)のコードを確認します。

* **16行目**:React Open Weatherウィジェットが必要に応じて読み込まれます。
* **46行目**:この `MapTo` 関数は、このReactコンポーネントを対応するAEMコンポーネントに関連付け、SPAエディタで編集できるようにします。

* **22～29行**:が定義 `EditConfig` され、市区町村が設定されているかどうかをチェックし、空の場合は値を定義します。

* **31 ～ 44行**:Weatherコンポーネントは、 `Component` クラスを拡張し、React Open WeatherコンポーネントのNPM使用ドキュメントで定義されている必要なデータを提供し、コンポーネントをレンダリングします。

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

バックエンドコンポーネントは既に存在する必要がありますが、フロントエンド開発者は、Web.RetailジャーナルSPAのReact Open Weatherコンポーネントをコード化することなく利用できます。

## 次のステップ {#next-step}

AEM用SPAの開発について詳しくは、「[AEM用SPAの開発](/help/sites-developing/spa-architecture.md)」を参照してください。
