---
title: Componenti di OSGi Events for Communities
seo-title: OSGi Events for Communities Components
description: Gli eventi OSGi vengono inviati che possono attivare listener asincroni
seo-description: OSGi events are sent that can trigger asynchronous listeners
uuid: 317e2add-689d-4c99-ae38-0703b6649cb7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 25b7ac08-6cdc-4dd5-a756-d6169b86f9ab
exl-id: 8049d797-e758-44c2-a89b-51d2b2fca8dc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 4%

---

# Componenti di OSGi Events for Communities  {#osgi-events-for-communities-components}

## Panoramica {#overview}

Quando i membri interagiscono con le funzioni di Communities, vengono inviati eventi OSGi che possono attivare listener asincroni, come notifiche o gamification (punteggio e contrassegno).

Di un componente [SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) L’istanza registra gli eventi come `actions` che si verificano per `topic`. SocialEvent include un metodo per restituire un `verb` associato all’azione. C&#39;è un *n-1* rapporto tra `actions` e `verbs`.

Per i componenti di Communities forniti nella versione, le tabelle seguenti descrivono `verbs` definiti per ciascuna `topic` disponibile per l&#39;uso.

## Argomenti e verbi {#topics-and-verbs}

[Componente calendario](calendar-basics-for-developers.md)
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea un evento calendario |
| AGGIUNGI | Commenti dei membri su un evento calendario |
| AGGIORNA | Modifica dell&#39;evento o del commento del calendario del membro |
| ELIMINA | L&#39;evento calendario o il commento del membro viene eliminato |

[Componente Commenti](essentials-comments.md)
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea un commento |
| AGGIUNGI | Risposte del membro al commento |
| AGGIORNA | Modifica del commento del membro |
| ELIMINA | Il commento del membro è soppresso |

[Componente libreria file](essentials-file-library.md)
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea una cartella |
| ATTACCO | Il membro carica un file |
| AGGIORNA | Il membro aggiorna una cartella o un file |
| ELIMINA | Un membro elimina una cartella o un file |

[Componente Forum](essentials-forum.md)
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descrizione** |
|---|---|
| POST | Argomento forum per i membri |
| AGGIUNGI | Risposta del membro all&#39;argomento del forum |
| AGGIORNA | Argomento o risposta del forum del membro è modificato |
| ELIMINA | L&#39;argomento del forum o la risposta del membro è cancellata |

[Componente Journal](blog-developer-basics.md)
SocialEvent `topic`= com/adobe/cq/social/journal

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea un articolo di blog |
| AGGIUNGI | Commenti su un articolo del blog |
| AGGIORNA | Articolo o commento del blog del membro è modificato |
| ELIMINA | L&#39;articolo o il commento del blog del membro è cancellato |

[Componente QnA](qna-essentials.md)
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descrizione** |
|---|---|
| POST | Il membro crea una domanda QnA |
| AGGIUNGI | Il membro crea una risposta QnA |
| AGGIORNA | La domanda o la risposta QnA del membro viene modificata |
| SELEZIONA | La risposta del membro è selezionata |
| ANNULLA | La risposta del membro è deselezionata |
| ELIMINA | La domanda o la risposta QnA del membro viene eliminata |

[Componente Recensioni](reviews-basics.md)
SocialEvent `topic`= com/adobe/cq/social/review

| **Verbo** | **Descrizione** |
|---|---|
| POST | Membro: revisione |
| AGGIORNA | Revisione del membro |
| ELIMINA | La revisione del membro è soppressa |

[Componente di valutazione](rating-basics.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbo** | **Descrizione** |
|---|---|
| AGGIUNGI VALUTAZIONE | Il contenuto del membro è stato valutato |
| RIMUOVI VALUTAZIONE | Il contenuto del membro è stato valutato in modo negativo |

[Componente di voto](essentials-voting.md)
SocialEvent `topic`= com/adobe/cq/social/tally

| **Verbo** | **Descrizione** |
|---|---|
| AGGIUNGI VOTO | Il contenuto del deputato è stato votato |
| RIMUOVI VOTO | Il contenuto del deputato è stato respinto |

**Componenti abilitati per la moderazione**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descrizione** |
|---|---|
| RIFIUTA | Il contenuto del membro è negato |
| FLAG-AS INAPPROPRIATO | Il contenuto del membro è contrassegnato |
| NON APPROPRIATO | Il contenuto del membro non è contrassegnato |
| ACCETTARE | Il contenuto del membro è approvato dal moderatore |
| CHIUDI | Il membro chiude il commento alle modifiche e alle risposte |
| APERTO | Il membro riapre il commento |

## Eventi per componenti personalizzati {#events-for-custom-components}

Per un componente personalizzato, la [Classe astratta SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html) deve essere esteso d per registrare gli eventi del componente come `actions`che si verificano per `topic`.

L&#39;evento personalizzato sostituisce il metodo `getVerb()` in modo che `verb`viene restituito per ogni `action`. La `verb` restituita per un’azione può essere comunemente utilizzata (ad esempio `POST`) o uno specializzato per il componente (ad esempio `ADD RATING`). C&#39;è un *n-1* rapporto tra `actions`e `verbs`.

>[!NOTE]
>
>Assicurati che un&#39;estensione personalizzata sia registrata con una classificazione inferiore a qualsiasi implementazione esistente nel prodotto.

### Pseudo-codice per evento componente personalizzato {#pseudo-code-for-custom-component-event}

[org.osgi.service.event.Event](https://osgi.org/javadoc/r4v41/org/osgi/service/event/Event.html);
[com.adobe.cq.sosocial.scf.core.SocialEvent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/scf/core/SocialEvent.html);
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

## Esempio di EventListener per filtrare i dati del flusso di attività {#sample-eventlistener-to-filter-activity-stream-data}

È possibile ascoltare gli eventi allo scopo di modificare ciò che appare nel flusso di attività.

Il seguente esempio di pseudo-codice rimuove gli eventi DELETE per il componente Commenti dal flusso di attività.

### Pseudo-codice per EventListener {#pseudo-code-for-eventlistener}

Richiede [pacchetto di funzionalità più recente](deploy-communities.md#latestfeaturepack).

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
