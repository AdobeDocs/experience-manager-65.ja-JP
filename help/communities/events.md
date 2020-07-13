---
title: コミュニティコンポーネントの OSGi イベント
seo-title: コミュニティコンポーネントの OSGi イベント
description: 非同期リスナーを呼び出す OSGi イベントが送信されます
seo-description: 非同期リスナーを呼び出す OSGi イベントが送信されます
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 42%

---


# コミュニティコンポーネントの OSGi イベント  {#osgi-events-for-communities-components}

## 概要 {#overview}

メンバーがコミュニティ機能と対話する際には、通知やゲーミフィケーション（スコアおよびバッジ）のような非同期リスナーを呼び出す OSGi イベントが送信されます。

A component&#39;s [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) instance records the events as `actions` that occur for a `topic`. The SocialEvent includes a method to return a `verb` associated with the action. There is an *n-1* relationship between `actions` and `verbs`.

For the Communities components delivered in the release, the following tables describe the `verbs` defined for each `topic` available for use.

## トピックと動詞 {#topics-and-verbs}

[カレンダーコンポーネント](calendar-basics-for-developers.md) SocialEvent `topic`=  = com/adobe/cq/social/calendar

| **動詞** | **説明** |
|---|---|
| POST | カレンダーイベントの作成 |
| ADD | カレンダーイベントに対するメンバーコメント |
| UPDATE | メンバーのカレンダーイベントまたはコメントが編集されました |
| DELETE | メンバーのカレンダーイベントまたはコメントが削除されました |

[コメントコンポーネント](essentials-comments.md) SocialEvent `topic`=  = com/adobe/cq/social/comment

| **動詞** | **説明** |
|---|---|
| POST | メンバがコメントを作成する |
| ADD | コメントへのメンバの返信 |
| UPDATE | メンバーのコメントが編集されます |
| DELETE | メンバーのコメントが削除されました |

[ファイルライブラリコンポーネント](essentials-file-library.md) SocialEvent `topic`=  = com/adobe/cq/social/fileLibrary

| **動詞** | **説明** |
|---|---|
| POST | メンバーがフォルダーを作成 |
| ATTACH | メンバーはファイルをアップロードします |
| UPDATE | メンバーがフォルダーまたはファイルを更新 |
| DELETE | メンバーがフォルダーまたはファイルを削除しました |

[フォーラムコンポーネント](essentials-forum.md) SocialEvent `topic`=  = com/adobe/cq/social/forum

| **動詞** | **説明** |
|---|---|
| POST | メンバーがフォーラムトピックを作成します |
| ADD | フォーラムトピックへのメンバーの返信 |
| UPDATE | メンバーのフォーラムトピックまたは返信が編集されました |
| DELETE | メンバーのフォーラムトピックまたは返信が削除されました |

[ジャーナルコンポーネント](blog-developer-basics.md) SocialEvent `topic`=  = com/adobe/cq/social/journal

| **動詞** | **説明** |
|---|---|
| POST | 会員がブログ記事を作成する |
| ADD | ブログ記事に対するメンバーコメント |
| UPDATE | 会員のブログ記事またはコメントが編集されました |
| DELETE | 会員のブログ記事またはコメントが削除されました |

[Q&amp;A コンポーネント](qna-essentials.md) SocialEvent `topic` = com/adobe/cq/social/qna

| **動詞** | **説明** |
|---|---|
| POST | メンバがQnA質問を作成します |
| ADD | メンバはQnA応答を作成します |
| UPDATE | メンバーのQnAの質問または回答が編集されました |
| SELECT | メンバの回答が選択されました |
| UNSELECT | メンバーの回答が選択解除されました |
| DELETE | メンバーのQnAの質問または回答が削除されました |

[レビューコンポーネント](reviews-basics.md) SocialEvent `topic`=  = com/adobe/cq/social/review

| **動詞** | **説明** |
|---|---|
| POST | メンバーがレビューを作成 |
| UPDATE | メンバーのレビューが編集されます |
| DELETE | メンバーのレビューが削除されました |

[評価コンポーネント](rating-basics.md) SocialEvent `topic`=  = com/adobe/cq/social/tally

| **動詞** | **説明** |
|---|---|
| ADD RATING | 会員のコンテンツが評価済みです |
| REMOVE RATING | 会員のコンテンツが評価されていません |

[投票コンポーネント](essentials-voting.md) SocialEvent `topic`=  = com/adobe/cq/social/tally

| **動詞** | **説明** |
|---|---|
| ADD VOTING | 会員のコンテンツが投票済み |
| REMOVE VOTING | 会員のコンテンツが投票済みになりました |

**モデレート対応コンポーネント** SocialEvent `topic`=  = com/adobe/cq/social/moderation

| **動詞** | **説明** |
|---|---|
| DENY | 会員の内容が拒否されました |
| FLAG-AS-INAPPROPRIATE | メンバーのコンテンツにフラグが付けられます |
| UNFLAG-AS-INAPPROPRIATE | メンバーのコンテンツにフラグが付けられていません |
| ACCEPT | メンバーのコンテンツがモデレーターによって承認されている |
| CLOSE | メンバーが編集と返信に対するコメントを閉じる |
| OPEN | メンバーがコメントを再度開きます |

## カスタムコンポーネントのイベント {#events-for-custom-components}

For a custom component, the [SocialEvent abstract class](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) must be extended d to record the component&#39;s events as `actions`that occur for a `topic`.

The custom event would override the method `getVerb()` so that an appropriate `verb`is returned for each `action`. The `verb` returned for an action may be one commonly used (such as `POST`) or one specialized for the component (such as `ADD RATING`). There is an *n-1* relationship between `actions`and `verbs`.

>[!NOTE]
>
>カスタム拡張が製品の既存の実装よりも低いランクで登録されていることを確認します。


### カスタムコンポーネントイベントの疑似コード {#pseudo-code-for-custom-component-event}

[org.osgi.service.イベント.イベント](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.soscial.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
[com.adobe.granite.activitystreams.ObjectTypes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ObjectTypes.html);
[com.adobe.granite.activitystreams.Verbs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/Verbs.html);

```java
package com.mycompany.recipe;

import org.osgi.service.event.Event;
import com.adobe.cq.social.scf.core.SocialEvent;
import com.adobe.granite.activitystreams.ObjectTypes;
import com.adobe.granite.activitystreams.Verbs;

/*
 * The Recipe type, passed to RecipeEvent(), would be a custom Recipe class
 * that extends either
 * com.adobe.cq.social.scf.SocialComponent
 * or
 * com.adobe.cq.social.scf.SocialCollectionComponent
 * See https://docs.adobe.com/docs/en/aem/6-2/develop/communities/scf/server-customize.html
 */

/**
 * Defines events that are triggered on a custom component, "Recipe".
 */
public class RecipeEvent extends SocialEvent<RecipeEvent.RecipeActions> {

    private static final long serialVersionUID = 1L;
    protected static final String PARENT_PATH = "PARENT_PATH";

    /**
     * The event topic suffix for Recipe events
     */
    public static final String RECIPE_TOPIC = "recipe";

    /**
     * @param recipe - the recipe resource on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final Recipe recipe, final String userId, final RecipeEvent.RecipeActions action) {
        String recipePath = recipe.getResource().getPath();
        String parentPath = (recipe.getParentComponent() != null) ?
                             recipe.getParentComponent().getResource().getPath() :
                             recipe.getSourceComponentId();
        this(recipePath, userId, parentPath, action);
    }

    /**
     * @param recipePath - the path to the recipe resource (jcr node) on which the event was triggered
     * @param userId - the user id of the user who triggered the action
     * @param parentPath - the path to the parent node of the recipe resource
     * @param action - the recipe action that triggered this event
     */
    public RecipeEvent(final String recipePath, final String userId, final String parentPath) {
        super(RECIPE_TOPIC, recipePath, userId, action,
              new BaseEventObject(recipePath, ObjectTypes.ARTICLE),
              new BaseEventObject(parentPath, ObjectTypes.COLLECTION),
              new HashMap<String, Object>(1) {
            private static final long serialVersionUID = 1L;
            {
                if (parentPath != null) {
                    this.put(PARENT_PATH, parentPath);
                }

            }
        });
    }

    private RecipeEvent (final Event event) {
      super(event);
    }

    /**
     * List of available recipe actions that can trigger a recipe event.
     */
    public static enum RecipeActions implements SocialEvent.SocialActions {
        RecipeAdded,
        RecipeModified,
        RecipeDeleted;

        @Override
        public String getVerb() {
            switch (this) {
                case RecipeAdded:
                    return Verbs.POST;
                case RecipeModified:
                    return Verbs.UPDATE;
                case RecipeDeleted:
                    return Verbs.DELETE;
                default:
                    throw new IllegalArgumentException("Unsupported action");
            }
        }
    }

}
```

## アクティビティストリームデータをフィルターするサンプルの EventListener {#sample-eventlistener-to-filter-activity-stream-data}

アクティビティストリームに現れる内容を変更するために、イベントをリスニングできます。

次の疑似コードのサンプルでは、コメントコンポーネントの DELETE イベントをアクティビティストリームから削除します。

### EventListener の疑似コード {#pseudo-code-for-eventlistener}

[最新の機能パック](deploy-communities.md#latestfeaturepack)が必要です。

```java
package my.company.comments;

import java.util.Collections;
import java.util.Map;

import org.apache.commons.lang.StringUtils;
import org.apache.felix.scr.annotations.Activate;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Modified;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.osgi.PropertiesUtil;
import org.osgi.service.component.ComponentContext;

import com.adobe.cq.social.activitystreams.listener.api.ActivityStreamProviderExtension;
import com.adobe.cq.social.commons.events.CommentEvent.CommentActions;
import com.adobe.cq.social.scf.core.SocialEvent;

@Service
@Component(metatype = true, label = "My Comment Delete Event Filter",
        description = "Prevents comment DELETE events from showing up in activity streams")
public class CommentDeleteEventActivityFilter implements ActivityStreamProviderExtension {

    @Property(name = "ranking", intValue = 10)
    protected int ranking;

    @Activate
    public void activate(final ComponentContext ctx) {
        ranking = PropertiesUtil.toInteger(ctx.getProperties().get("ranking"), 10);
    }

    @Modified
    public void update(final Map<String, Object> props) {
        ranking = PropertiesUtil.toInteger(props.get("ranking"), 10);
    }

    @Override
    public boolean evaluate(final SocialEvent<?> evt, final Resource resource) {
        if (evt.getAction() != null && evt.getAction() instanceof SocialEvent.SocialActions) {
            final SocialEvent.SocialActions action = evt.getAction();
            if (StringUtils.equals(action.getVerb(), CommentActions.DELETED.getVerb())) {
                return false;
            }
        }
        return true;
    }

    @Override
    public Map<String, ? extends Object> getActivityProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public Map<String, ? extends Object> getActorProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String getName() {
        return "My Comment Delete Event Filter";
    }

    @Override
    public Map<String, ? extends Object> getObjectProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    /* Ensure a custom extension is registered with a ranking lower than any existing implementation in the product. */
    @Override
    public int getRanking() {
        return this.ranking;
    }

    @Override
    public Map<String, ? extends Object> getTargetProperties(final SocialEvent<?> arg0, final Resource arg1) {
        return Collections.<String, Object>emptyMap();
    }

    @Override
    public String[] getStreamProviderPid() {
        return new String[]{"*"};
    }

}
```

