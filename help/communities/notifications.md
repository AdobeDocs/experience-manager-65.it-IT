---
title: Notifiche community
seo-title: Notifiche community
description: I AEM Communities hanno notifiche che mostrano eventi di interesse per il membro della community che ha effettuato l'accesso
seo-description: I AEM Communities hanno notifiche che mostrano eventi di interesse per il membro della community che ha effettuato l'accesso
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---


# Notifiche community {#communities-notifications}

## Panoramica {#overview}

I AEM Communities forniscono una sezione delle notifiche che mostra gli eventi di interesse per i membri della community sottoscritti.

Le notifiche sono simili alle [attività](/help/communities/essentials-activities.md) e alle [sottoscrizioni](/help/communities/subscriptions.md) derivanti da:

* Il contenuto di pubblicazione del membro.
* Il membro che sceglie di seguire un altro membro.
* Il membro che sceglie di seguire argomenti, articoli e altri thread specifici di contenuto.
* Il membro con tag (@reference) un altro membro della community in un contenuto generato dall&#39;utente.

Ciò che distingue le notifiche dalle attività e dalle sottoscrizioni è:

* Un collegamento alla sezione delle notifiche è sempre presente nell&#39;intestazione di un sito community:

   * Le attività richiedono che la funzione [del flusso di](/help/communities/functions.md#activity-stream-function) attività sia inclusa nella struttura del sito della comunità.
   * Le iscrizioni richiedono [la configurazione dell&#39;e-mail](/help/communities/email.md).

* L&#39;implementazione delle notifiche avviene tramite canali scalabili e collegabili:

   * Le attività sono disponibili solo sul Web.
   * Le iscrizioni sono disponibili solo tramite e-mail.

A partire dal [FP1](/help/communities/deploy-communities.md#latestfeaturepack)di Communities, i canali di notifica disponibili sono:

* Canale Web a cui si accede tramite il `Notifications` collegamento.
* Il canale e-mail, disponibile quando l’e-mail è configurata correttamente.

I canali futuri sono mobile e desktop.

### Requisiti {#requirements}

**Configura e-mail**

Affinché il canale e-mail possa funzionare, è necessario configurare l’e-mail.

Per istruzioni sulla configurazione dell’e-mail, consultate [Configurazione dell’e-mail](/help/communities/analytics.md).

**Abilita Follow**

I componenti devono essere configurati per abilitare quanto segue. Le funzioni che consentono di seguire sono [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [filibreria](/help/communities/file-library.md)[](/help/communities/comments.md), commenti.

**Nota**:

* I componenti utilizzati all&#39;interno dei modelli [di](/help/communities/sites.md) sito community e dei modelli [di](/help/communities/tools-groups.md) gruppo possono già essere configurati per essere seguiti.

* I profili dei membri sono già configurati per consentire agli altri membri di seguirli.

## Notifiche dai seguenti {#notifications-from-following}

![notifiche](assets/notifications.png)

Il pulsante **[!UICONTROL Segui]** consente di seguire le voci come attività, iscrizioni e/o notifiche. Ogni volta che si seleziona il pulsante **[!UICONTROL Segui]** , è possibile attivare o disattivare una selezione. La `Email Subscriptions` selezione è presente solo se configurata.

Se è selezionato un metodo di seguito, il testo del pulsante diventa **[!UICONTROL Seguente]**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Verrà visualizzato il pulsante **[!UICONTROL Segui]** :

* Quando si visualizza il profilo di un altro membro.
* In una pagina delle funzioni principali, ad esempio forum, QnA e blog:

   * Segue tutta l&#39;attività per quella funzione generale.

* Per un post specifico, ad esempio un argomento del forum, una domanda QnA o un articolo di blog:

   * Segue tutta l&#39;attività per quella voce specifica.

## Gestione delle impostazioni di notifica {#managing-notification-settings}

Selezionando il collegamento Impostazioni notifica dalla pagina Notifiche, è possibile per ciascun membro gestire il modo in cui vengono ricevute le notifiche.

Il canale Web è sempre abilitato.

![notifications14](assets/notifications1.png)

Il canale e-mail, che si basa sulla corretta [configurazione dell’e-mail](/help/communities/email.md), fornisce le stesse impostazioni del canale Web.

Il canale e-mail è disattivato per impostazione predefinita.

![notifications2](assets/notifications2.png)

Può essere attivata da un membro, ma dipende comunque dalla configurazione dell&#39;e-mail.

![notifications3](assets/notifications3.png)

## Visualizzazione delle notifiche {#viewing-notifications}

### Notifiche Web {#web-notifications}

Una [procedura guidata per la creazione di un sito](/help/communities/sites-console.md) community ora include un collegamento alla `Notifications` funzione nella barra dell&#39;intestazione del sito, sopra il banner. A differenza dei messaggi, le notifiche vengono create per ogni sito community, mentre i messaggi devono essere attivati durante il processo di creazione del sito.

Quando si visita il sito pubblicato, selezionando il `Notifications` collegamento vengono visualizzate tutte le notifiche relative al membro.

![notifications4](assets/notifications4.png)

### Notifiche e-mail {#email-notifications}

Quando il canale e-mail è abilitato, il membro riceve un messaggio e-mail contenente un collegamento al contenuto sul Web.

![notifications5](assets/notifications5.png)

## Personalizzare le notifiche e-mail {#customize-email-notifications}

Le organizzazioni possono personalizzare le notifiche e-mail [sovrapponendo](/help/communities/client-customize.md#overlays) i modelli in **/libs/settings/community/templates/email/html**.

Ad esempio, per modificare i riferimenti alle notifiche e-mail (per un componente community), aggiungete una condizione **if** per il **riferimento** al verbo nei modelli dei componenti per i quali avete attivato il supporto **@menzioni** .

Per modificare il modello di notifiche e-mail per @Menzioni nei commenti del blog, posizionate fuori dalla casella in: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/it**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

