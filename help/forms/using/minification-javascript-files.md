---
title: JavaScript ファイルの縮小
description: AEM Forms Workspace のカスタマイズ後に縮小コードを生成して Web 用の JS ファイルを最適化するための手順です。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 29%

---

# JavaScript ファイルの縮小 {#minification-of-the-javascript-files}

縮小により、ソースコードから、空白、新しい行、コメントなどの冗長な文字が削除されます。 これにより、コードのサイズが小さくなるので、パフォーマンスが向上します。 縮小化は機能に影響を与えませんが、コードの読みやすさが低下します。

セマンティックの変更用に縮小コードを生成するには、次の手順に従います。

1. src-package の `client-html/src/main/webapp/js` を filesystem にコピーします。

   >[!NOTE]
   >
   >パッケージに関する詳細については、「[AEM Forms Workspace のカスタマイズの概要](/help/forms/using/introduction-customizing-html-workspace.md)」を参照してください。

1. モデルやビューの追加または更新の場合は、client-html/src/main/webapp/js の下にある `main.js` のパスを更新します。

   例えば、新しい Sharequeue モデル (mySharequeue) を追加する場合は、次のように変更します。

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   To

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. エイリアスの変更や追加が `main.js` にある場合は、`registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` をアップデートします。

   例えば、新しい Sharequeue モデル (mySharequeue) を追加する場合は、次のように変更します。

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   To

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. client-html/src/main/webapp/js/minifier で、次のコマンドを実行します。

   ```shell
   mvn clean install
   ```

   縮小された main.js と registry.js を使用して、client-html/src/main/webapp/js の下に縮小された —files フォルダーが生成されます。

>[!NOTE]
>
>縮小は、64 ビット JVM でのみ機能します。

>[!NOTE]
>
>縮小した場合は、アップグレードに影響が出ます。
