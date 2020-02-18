---
title: SPA用のReactコンポーネントの実装
seo-title: SPA用のReactコンポーネントの実装
description: この記事では、AEM SPA editorを使用して、既存のシンプルなReactコンポーネントを適応させる方法の例を示します。
seo-description: この記事では、AEM SPA editorを使用して、既存のシンプルなReactコンポーネントを適応させる方法の例を示します。
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA用のReactコンポーネントの実装{#implementing-a-react-component-for-spa}

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者は SPA フレームワークを使用してサイトを構築したいと考え、作成者はそうして構築されたサイトのコンテンツを AEM 内でシームレスに編集したいと考えています。

SPA オーサリング機能には、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。この記事では、AEM SPA editorを使用して、既存のシンプルなReactコンポーネントを適応させる方法の例を示します。

>[!NOTE]
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

## 概要 {#introduction}

AEMが必要とし、SPAとSPAエディターの間で確立するシンプルで軽量な契約のおかげで、既存のJavaScriptアプリケーションをAEMのSPAで使用するために適合させるのは簡単なことです。

この記事では、We.Retail JournalサンプルSPAの天気コンポーネントの例を示します。

この記事を読む前に、AEMのSPA [アプリケーションの構造について](/help/sites-developing/spa-getting-started-react.md) 、よく理解しておく必要があります。

## 天気コンポーネント {#the-weather-component}

天気コンポーネントは、We.Retail Journalアプリの左上にあります。 定義した場所の現在の天気が表示され、気象データが動的に取り込まれます。

### ウィジェットの使用 {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

SPA editorでSPAのコンテンツをオーサリングする場合、気象コンポーネントは他のAEMコンポーネントと同様に表示され、ツールバーと共に完成し、編集可能になります。

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

市区町村は、他のAEMコンポーネントと同様に、ダイアログで更新できます。

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

変更は維持され、コンポーネントは新しい天気データを使用して自動的に更新されます。

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### 気象コンポーネントの実装 {#weather-component-implementation}

天気コンポーネントは、 [](https://www.npmjs.com/package/react-open-weather)React Open Weatherと呼ばれる、We.Retail JournalサンプルSPAアプリケーション内のコンポーネントとして機能するように適合された、公開されたReactコンポーネントに基づいています。

以下は、React Open Weatherコンポーネントの使用に関するNPMドキュメントのスニペットです。

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

We.Retail Journalアプリケーションで、カスタマイズした天気コンポ `Weather.js`ーネント()のコードを確認します。

* **16行目**:必要に応じてReact Open Weatherウィジェットが読み込まれます。
* **46行目**:このReactコ `MapTo` ンポーネントは、SPAエディターで編集できるように、対応するAEMコンポーネントに関連付けられます。

* **22～29行**:が定 `EditConfig` 義され、市区町村が設定されているかどうかを確認し、空の場合に値を定義します。

* **行31 ～ 44**:Weatherコンポーネントは、クラスを拡張し、React Open Weatherコ `Component` ンポーネントのNPM使用ドキュメントで定義されている必要なデータを提供し、コンポーネントをレンダリングします。

```
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
import {MapTo} from '@adobe/cq-react-editable-components';

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

バックエンドコンポーネントは既に存在する必要がありますが、フロントエンド開発者は、We.Retail Journal SPAのReact Open Weatherコンポーネントをほとんどコーディングせずに利用できます。

## 次のステップ {#next-step}

AEM用SPAの開発について詳しくは、「AEM用SPAの開発」を [参照してください](/help/sites-developing/spa-architecture.md)。
