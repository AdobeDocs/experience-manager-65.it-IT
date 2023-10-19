---
title: Funzione Flussi di attività
description: Scopri come le attività di un membro della community di accesso vengono raccolte in un flusso che puoi filtrare e visualizzare tramite il componente Flussi di attività.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# Funzione Flussi di attività {#activity-streams-feature}

## Introduzione {#introduction}

Le attività di un membro della community che ha effettuato l’accesso, ad esempio la pubblicazione in un forum o in un blog, vengono raccolte in un flusso che può essere filtrato e visualizzato in vari modi tramite la configurazione di `Activity Streams` componente.

La possibilità di seguire aggiunge un&#39;altra vista delle attività in cui i membri della community seguono i post di interesse o seguono le attività di altri membri della community.

Il documento descrive:

* Aggiunta del componente Flussi di attività a un sito AEM
* Impostazioni di configurazione del componente Flussi attività

### Aggiunta di flussi di attività a una pagina {#adding-activity-streams-to-a-page}

Se si desidera aggiungere un `Activity Streams` a una pagina in modalità di authoring, utilizza il browser Componenti per individuare

* `Communities / Activity Streams`

Trascinalo in una pagina in cui dovrebbero apparire i flussi di attività.

Per informazioni necessarie, visitare il sito [Nozioni di base sui componenti community](/help/communities/basics.md).

Quando [librerie lato client richieste](/help/communities/essentials-activities.md#essentials-for-client-side) sono inclusi, è così che `Activity Streams` viene visualizzato il componente:

![activity-streams](assets/activity-component.png)

### Configurazione dei flussi di attività {#configuring-activity-streams}

Seleziona la inserita `Activity Streams` in modo da poter accedere e selezionare `Configure` che apre la finestra di dialogo per modifica.

![configura](assets/configure-new.png)

Sotto **Attività utente** , specificare le attività da visualizzare:

![attività degli utenti](assets/user-activities.png)

* **Numero massimo di attività**

  Numero di attività da visualizzare

* **Percorso risorsa del flusso**

  Lascia vuoto questo campo per impostare il sito community o il gruppo community come predefinito. Il percorso della risorsa del flusso identifica l’origine delle attività. Il valore predefinito è vuoto.

* **Visualizza la vista Attività utente**

  Se questa opzione è selezionata, la pagina Attività include una scheda che filtra le attività in base a quelle generate all&#39;interno della community dal membro corrente. Il valore predefinito è selezionato.

* **Visualizza la vista Tutte le attività**

  Se questa opzione è selezionata, la pagina delle attività include una scheda che include tutte le attività generate all&#39;interno della comunità a cui il membro corrente ha accesso. Il valore predefinito è selezionato.

* **Visualizza la vista Segui**

  Se questa opzione è selezionata, la pagina attività include una scheda che filtra le attività in base a quelle seguite dal membro corrente. Il valore predefinito è selezionato.

### Vista successiva {#following-view}

I componenti devono essere configurati in modo da abilitare quanto segue. Le funzioni che consentono di: [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [D/R](/help/communities/working-with-qna.md), [calendario](/help/communities/calendar.md), [libreria file](/help/communities/file-library.md), e [commenti](/help/communities/comments.md).

![visualizzazione successiva](assets/following-activities.png)

Il **Segui** fornisce un mezzo per seguire le voci come attività, [notifiche](/help/communities/notifications.md), o [abbonamenti](/help/communities/subscriptions.md). Ogni volta che **Segui** è selezionato, è possibile attivare o disattivare una selezione. Il `Email Subscriptions` La selezione è presente solo se configurata.

Se è selezionato un metodo qualsiasi di seguito, il testo del pulsante diventa **Segue**. Per comodità, è possibile selezionare `Unfollow All` per disattivare tutti i metodi.

Il **Segui** viene visualizzato il pulsante:

* Quando si visualizza il profilo di un altro membro.
* In una pagina delle funzioni principali, ad esempio forum, domande e blog.

   * Segue tutte le attività per quella funzione generale.

* Per una voce specifica, ad esempio un argomento forum, una domanda di controllo qualità o un articolo di blog.

   * Segue tutte le attività per quella voce specifica.

### Informazioni aggiuntive {#additional-information}

Ulteriori informazioni sono disponibili sul sito [Nozioni di base sui flussi di attività](/help/communities/essentials-activities.md) pagina per sviluppatori.
