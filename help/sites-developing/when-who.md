---
title: テスト - 実行のタイミングとテスター
seo-title: Testing - when and with whom?
description: 様々な役割のユーザーがテストに参加できます。また、プロジェクト開発の様々な段階でテストを実行できます
seo-description: Various roles can be involved in testing and at various stages of project development
uuid: 431e8f06-80eb-4fb3-a4c7-2580608b0a1c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 6148f8e6-ab62-4eb8-8a2d-c431b8318000
exl-id: 5a16be40-eede-4a47-b03b-3993e285232e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 100%

---

# テスト - 実行のタイミングとテスター{#testing-when-and-with-whom}

様々な役割のユーザーがテストに参加できます。また、プロジェクト開発の様々な段階でテストを実行できます。

<table>
 <tbody>
  <tr>
   <td>テストチーム</td>
   <td>責任の範囲 </td>
   <td>When...</td>
  </tr>
  <tr>
   <td>開発チーム</td>
   <td>開発チームは単体テストと一部の統合テストに責任を持ちます。</td>
   <td>これらのテストはテストチェーンの最初にあたるものですが、開発中は繰り返し、範囲を広げながら実施されます。</td>
  </tr>
  <tr>
   <td>品質保証チーム</td>
   <td><p>機能テストとパフォーマンステストをおこなう（適切な規模の）品質保証チームが必要です。</p> <p>彼らは中立的な、専任のテスターです。「開発者が自分の成果物をテストしてはならない」というのはソフトウェア開発の鉄則です。</p> <p>このチームのメンバーは、業務プロジェクトチーム、パートナーまたは顧客のチームから集められる場合があります。</p> </td>
   <td><p>現実的に可能な限り速やかに、最初の機能リリースをこのチームのテスターに引き渡す必要があります。初期の中間リリースでは数多くのバグが生じる可能性がありますが、それによって、重大な問題を早い段階で見つけることができます。</p> </td>
  </tr>
  <tr>
   <td>顧客のテストチーム</td>
   <td><p>選択したプロジェクトモデルによっては、顧客チームのメンバー（特に顧客サイトの作成者）にテストに参加してもらう場合があります。</p> <p>これには次のような利点があります。</p>
    <ul>
     <li><p>開発中のプロジェクトを顧客に体験してもらえる。</p> </li>
     <li><p>早い段階で顧客からのフィードバックが得られる。</p> </li>
     <li><p>ユーザーは過去の経験に基づいて要望を述べる傾向にあり、できる限り早い段階から顧客をテストに参加させれば、新プロジェクトを実際に体験する機会が増える<i>。</i></p> </li>
    </ul> </td>
   <td><p>早い段階から参加してもらうことが理想ですが、顧客に使用してもらうリリースは、ある程度完成したものであり、安定している必要があります。</p> <p>第一印象が重要だからです。</p> </td>
  </tr>
 </tbody>
</table>
