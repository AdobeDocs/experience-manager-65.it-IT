---
title: Notifiche community
description: AEM Communities dispone di notifiche che mostrano eventi di interesse per il membro della community connesso
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# Notifiche community {#communities-notifications}

## Panoramica {#overview}

AEM Communities fornisce una sezione di notifiche che mostra gli eventi di interesse per il membro della community di accesso.

Le notifiche sono simili alle [attività](/help/communities/essentials-activities.md) e alle [sottoscrizioni](/help/communities/subscriptions.md) in quanto potrebbero derivare da:

* Il membro che pubblica il contenuto.
* Il membro che sceglie di seguire un altro membro.
* Il membro che sceglie di seguire argomenti, articoli e altri thread di contenuto specifici.
* Il tag membro (@mention) di un altro membro della community in un contenuto generato dall&#39;utente.

Ciò che distingue le notifiche dalle attività e dagli abbonamenti è:

* Un collegamento alla sezione delle notifiche è sempre presente nell’intestazione di un sito community:

   * Le attività richiedono l&#39;inclusione della funzione [flusso attività](/help/communities/functions.md#activity-stream-function) nella struttura del sito community.
   * Gli abbonamenti richiedono [la configurazione dell&#39;e-mail](/help/communities/email.md).

* L’implementazione delle notifiche avviene tramite canali scalabili e collegabili:

   * Le attività sono disponibili solo sul web.
   * Gli abbonamenti sono disponibili solo tramite e-mail.

A partire da Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack), i canali di notifica disponibili sono:

* Canale Web, accessibile tramite il collegamento `Notifications`.
* Il canale e-mail, disponibile quando l’e-mail è configurata correttamente.

I canali futuri sono mobili e desktop.

### Requisiti {#requirements}

**Configura e-mail**

Affinché il canale e-mail funzioni, l’e-mail deve essere configurata.

Per istruzioni sulla configurazione dell&#39;e-mail, vedere [Configurazione dell&#39;e-mail](/help/communities/analytics.md).

**Attiva Segui**

I componenti devono essere configurati in modo da abilitare quanto segue. Le caratteristiche che consentono di eseguire le operazioni seguenti sono [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md) e [commenti](/help/communities/comments.md).

**Nota**:

* I componenti utilizzati nei [modelli di sito](/help/communities/sites.md) e [modelli di gruppo](/help/communities/tools-groups.md) della community potrebbero essere già configurati per seguire.

* I profili membro sono già configurati per consentire ad altri membri di seguire il processo.

## Notifiche da quanto segue {#notifications-from-following}

![notifiche](assets/notifications.png)

Il pulsante **[!UICONTROL Segui]** consente di seguire le voci come attività, abbonamenti e/o notifiche. Ogni volta che il pulsante **[!UICONTROL Segui]** è selezionato, è possibile attivare o disattivare una selezione. La selezione `Email Subscriptions` è presente solo se configurata.

Se è selezionato un metodo qualsiasi di seguire, il testo del pulsante diventa **[!UICONTROL Segue]**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Verrà visualizzato il pulsante **[!UICONTROL Segui]**:

* Quando si visualizza il profilo di un altro membro.
* In una pagina delle funzioni principali, ad esempio forum, domande e blog:

   * Segue tutte le attività per quella funzione generale.

* Per una voce specifica, ad esempio un argomento forum, una domanda di controllo qualità o un articolo di blog:

   * Segue tutte le attività per quella voce specifica.

## Gestione delle impostazioni di notifica {#managing-notification-settings}

Selezionando il collegamento Impostazioni notifica dalla pagina Notifiche, ogni membro può gestire il modo in cui vengono ricevute le notifiche.

Il canale web è sempre abilitato.

![notifiche14](assets/notifications1.png)

Il canale e-mail, che si basa sulla [configurazione corretta dell&#39;e-mail](/help/communities/email.md), fornisce le stesse impostazioni del canale web.

Per impostazione predefinita, il canale e-mail è disattivato.

![notifiche2](assets/notifications2.png)

Può essere attivata da un membro, ma dipende comunque dalla configurazione dell’e-mail.

![notifiche3](assets/notifications3.png)

## Visualizzazione delle notifiche {#viewing-notifications}

### Notifiche Web {#web-notifications}

Una [procedura guidata ha creato il sito community](/help/communities/sites-console.md) e ora include un collegamento alla funzionalità `Notifications` nella barra dell&#39;intestazione del sito sopra il banner. A differenza dei messaggi, le notifiche vengono create per ogni sito community, mentre i messaggi devono essere abilitati durante il processo di creazione del sito.

Quando si visita il sito pubblicato, se si seleziona il collegamento `Notifications` verranno visualizzate tutte le notifiche per il membro.

![notifiche4](assets/notifications4.png)

### Notifiche e-mail {#email-notifications}

Quando il canale e-mail è abilitato, il membro riceve un messaggio e-mail contenente un collegamento al contenuto sul web.

![notifiche5](assets/notifications5.png)

## Personalizzare le notifiche e-mail {#customize-email-notifications}

Le organizzazioni possono personalizzare le notifiche e-mail [sovrapponendo](/help/communities/client-customize.md#overlays) i modelli in **/libs/settings/community/templates/email/html**.

Ad esempio, per modificare le menzioni e-mail di notifica (per un componente di community), aggiungi una condizione **if** per il verbo **menta** nei modelli dei componenti per i quali hai attivato il supporto di **@mentions**.

Per modificare il modello di notifiche e-mail per i @mention nei commenti del blog, inserisci il modello predefinito all&#39;indirizzo: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
